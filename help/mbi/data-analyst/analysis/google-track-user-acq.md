---
title: Google Analytics - Spåra översikt över källdata för användarförvärv
description: Lär dig segmentera data utifrån källa för kundvärvning.
exl-id: 2ce3e4f9-4741-4ada-b822-ec6a5ca94497
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: 3098909fdccb726108c24f2424e4ba4c1db9d1c2
workflow-type: tm+mt
source-wordcount: '774'
ht-degree: 1%

---

# Segmentering efter källa för kundvärvning

>[!NOTE]
>
>Processen nedan stöder inte [!DNL Google Universal Analytics].

Förmågan att segmentera data med hjälp av källan för kundvärvning är avgörande för att er marknadsföringsplan ska kunna hanteras effektivt. Genom att känna till nya användares anskaffningskälla kan ni visa vilka kanaler som ger störst avkastning, och teamet kan tryggt tilldela marknadsföringsbudgeten.

Om du inte redan spårar källor för kundvärvning i din databas, [!DNL Adobe Commerce Intelligence] kan hjälpa dig att komma igång:

## Spåra källa för kundvärvning

[!DNL Adobe] rekommenderar att du använder två metoder för att spåra hänvisningsdata baserat på dina inställningar:

### (Alternativ 1) Spåra källdata för orderreferenser via [!DNL Google Analytics E-Commerce]

Om du [!DNL Google Analytics E-Commerce] för att spåra din beställning och dina säljdata kan du använda [!DNL [Google Analytics E-Commerce Connector]](../importing-data/integrations/google-ecommerce.md) för att synkronisera varje orders hänvisningskälldata. På så sätt kan du segmentera intäkter och order efter hänvisningskälla (till exempel `utm_source` eller `utm_medium`). Ni får också en känsla av kundvärvningskällor via [!DNL Commerce Intelligence] anpassade dimensioner som `User's first order source`.

### (Alternativ 2) Spara [!DNL Google Analytics]&#39; hämta källdata i databasen

I det här avsnittet beskrivs hur du sparar [!DNL Google Analytics] information om inhämtningskanaler i din egen databas, nämligen `source`, `medium`, `term`, `content`, `campaign`och `gclid` parametrar som fanns på en användares första besök på webbplatsen. En förklaring av de här parametrarna finns i [[!DNL Google Analytics] dokumentation](https://support.google.com/analytics/answer/1191184?hl=en#zippy=%2Cin-this-article). Sedan kan du utforska några av de kraftfulla marknadsföringsanalyser som kan utföras med den här informationen i [!DNL Commerce Intelligence].

#### Varför?

Om du bara tittar på standardinställningen [!DNL Google Analytics] konverterings- och förvärvsstatistik får ni inte hela bilden. Även om det är intressant att se antalet konverteringar från organiska sökningar till betalda sökningar, vad kan du göra med den informationen? Borde du spendera mer pengar på betald sökning? Det beror på värdet hos kunder som kommer från den kanalen, vilket inte är något Google Analytics tillhandahåller.

>[!NOTE]
>
>[[!DNL Google Analytics eCommerce Tracking]](https://developers.google.com/analytics/devguides/collection/gajs/gaTrackingEcommerce) minskar problemet genom att transaktionsdata lagras i [!DNL Google Analytics]men den här lösningen fungerar inte för andra webbplatser än e-handelssajter. Vissa verktyg som kohortanalyser är inte heller enkla att göra i [!DNL Google Analytics] gränssnitt.

Vad händer om du vill skicka ett uppföljningserbjudande via e-post till alla kunder som skaffats via en viss e-postkampanj? Eller integrera kundvärvningsdata med CRM-systemet? Detta är omöjligt i [!DNL Google Analytics] - det strider mot användarvillkoren för [!DNL Google Analytics] för att lagra data som identifierar en individ. Men du kan lagra dessa data själv.

#### Metoden

[!DNL Google Analytics] lagrar besökarens hänvisningsinformation i en cookie som anropas `__utmz`. När denna cookie är inställd (av [!DNL Google Analytics] spårningskod) skickas dess innehåll med varje efterföljande begäran till din domän från den användaren. I PHP kan du till exempel kontrollera innehållet i `$_COOKIE['__utmz']` och du ser en sträng som ser ut ungefär så här:

`100000000.12345678.1.1.utmcsr=google|utmccn=(organic)|utmcmd=organic|utmctr=rj metrics`

Det är tydligt att en del data för förvärvskälla är kodade i strängen. Detta testas för att bekräfta att detta är besökarens senaste anskaffningskälla och tillhörande kampanjdata. Nu behöver ni veta hur ni extraherar data.

Den här koden har översatts till en [PHP-bibliotek på github](https://github.com/RJMetrics/referral-grabber-php). Om du vill använda biblioteket `include` en referens till `ReferralGrabber.php` och sedan ringa

`$data = ReferralGrabber::parseGoogleCookie($_COOKIE['__utmz']);`

Den returnerade `$data` arrayen är en karta över nycklarna `source`, `medium`, `term`, `content`, `campaign`, `gclid`och deras respektive värden.

Adobe rekommenderar att du lägger till en tabell i databasen som till exempel kallas `user_referral`, med kolumnerna som: `id INT PRIMARY KEY, user_id INT NOT NULL, source VARCHAR(255), medium VARCHAR(255), term VARCHAR(255), content VARCHAR(255), campaign VARCHAR(255), gclid VARCHAR(255)`. När en användare registrerar sig hämtar du hänvisningsinformationen och sparar den i den här tabellen.

#### Så här använder du dessa data

Nu när du sparar en källa för kundvärvning, hur kan du använda den?

Anta att du använder en SQL-databas och har en `users` tabell med följande struktur:

| ID | E-POST | JOIN_DATE | ACQ_SOURCE | ACQ_MEDIUM |
|--- |--- |--- |--- |--- |
| 1 | john@abc.com | 2012-01-24 | google | organisk |
| 2 | jim@abc.com | 2012-01-24 | google | cpc |
| 3 | joe@def.com | 2012-01-25 | direkt | - |
| 4 | jess@ghi.com | 2012-01-26 | hänskjutande | techcrunch.com |
| 5 | jen@ghi.net | 2012-01-30 | övriga | organisk |
| ... | ... | ... | ... | ... |

För startprogram kan du räkna antalet användare som kommer från varje hänvisningskanal genom att köra följande fråga mot databasen:

`SELECT acq_source, COUNT(id) as user_count FROM users GROUP BY acq_source;`

Resultatet ser ut ungefär så här:

| ACQ_SOURCE | USER_COUNT |
|--- |--- |
| google | 294 |
| direkt | 156 |
| hänskjutande | 55 |
| övriga | 16 |

Detta är intressant, men av begränsad användning. Det du verkligen vill veta är:

* Ökningshastigheten för dessa siffror över tiden
* Inkomstbeloppet som genereras av varje förvärvskälla
* A [kohortanalys](https://en.wikipedia.org/wiki/Cohort_analysis) av användare som kommer från varje källa
* Sannolikheten för att en användare från en av dessa kanaler returneras som kund i framtiden

De frågor som krävs för att utföra dessa analyser är komplexa. Med hjälp av den här informationen kan ni fastställa era mest lönsamma förvärvskanaler och fokusera marknadsföringstiden och pengarna därefter.

### Relaterad

* **[Upptäck era mest värdefulla förvärvskällor och kanaler](../analysis/most-value-source-channel.md)**
* **[Koppla samman [!DNL Google Adwords] konto](../importing-data/integrations/google-adwords.md)**
* **[Öka avkastningen på era annonskampanjer](../analysis/roi-ad-camp.md)**
* **[Hur [!DNL Google Analytics] UTM-attribueringsarbete?](../analysis/utm-attributes.md)**
