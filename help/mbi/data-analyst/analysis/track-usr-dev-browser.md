---
title: Google Analytics - Spåra användarenhets- och webbläsardata i databasen
description: Lär dig hur många användare som faktiskt loggar in via mobila enheter och hur det påverkar livslängden för dessa användare.
exl-id: 57b1bc45-b139-4370-86ea-2fbd021aa14d
role: Admin, User
feature: Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# [!UICONTROL Google Analytics]-spårning

Med [!UICONTROL Google Analytics] kan du [spara hänvisningskällinformation](../analysis/google-track-user-acq.md) för att förstå varifrån dina mest värdefulla användare kommer. I det här avsnittet beskrivs den plattform (till exempel en enhet eller webbläsare) som användarna arbetar med. På så sätt kan du förstå hur många användare som faktiskt loggar in via mobila enheter och hur det påverkar livslängdsvärdet för dessa användare.

## Sparar användarenhet och webbläsardata

Varje gång en begäran görs till din webbplats skickar användarens webbläsare en User-Agent-sträng med information om plattformen som gör begäran. Här är några exempel på strängen User-Agent:

1. `Mozilla/5.0 (Macintosh; Intel Mac OS X 10\_8\_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/27.0.1453.116 Safari/537.36`
1. `Mozilla/5.0 (Windows NT 6.1; WOW64; rv:17.0) Gecko/17.0 Firefox/17.0`
1. `Mozilla/5.0 (iPhone; U; CPU iPhone OS 4\_0 like Mac OS X; en-us) AppleWebKit/532.9 (KHTML, like Gecko) Version/4.0.5 Mobile/8A293 Safari/6531.22.7`
1.` Mozilla/5.0 (iPad; CPU OS 5\_1 like Mac OS X) AppleWebKit/534.46 (KHTML, like Gecko) Version/5.1 Mobile/9B176 Safari/7534.48.3`
1. `Mozilla/5.0 (Linux; U; Android 2.2; en-us; Nexus One Build/FRF91) AppleWebKit/533.1 (KHTML, like Gecko) Version/4.0 Mobile Safari/533.1`

Om du tittar närmare på strängen ser du att den innehåller information om användarens operativsystem, webbläsare och namnet på den enhet som användaren använder (om den har ett namn). Även om strängarna för användaragenten varierar mycket mellan olika plattformar och till och med versioner av samma plattform, är det i allmänhet sant att plattformsnamnet kommer att finnas någonstans i. Exempel: #1 ovan är en Mac med webbläsaren Chrome, #2 ovan är en Windows-dator med webbläsaren Firefox, #3 är en iPhone, #4 är en iPad och #5 är en Android-enhet.

Servern kan komma åt den här informationen varje gång en begäran görs. I PHP lagras strängen User-Agent i `$_SERVER['HTTP_USER_AGENT']`. I Ruby på Rails lagras den i `request.env['HTTP_USER_AGENT']`. På andra språk och i andra miljöer kan du komma åt den på liknande sätt.

### När ska du registrera dessa data?

[!DNL Adobe] rekommenderar att du lägger till ett nytt fält med namnet `Platform` eller `User-Agent` i databastabellerna `Customers` och `Orders` för att lagra informationen när en användare skapas eller en order placeras. Om du använder en SQL-databas bör det här fältet vara `VARCHAR(255)`. 

>[!NOTE]
>
>Strängen `User-Agent` får vara mycket längre än så, men i praktiken är den sällan längre.

### Hur tolkar jag de användbara segmenten?

Det finns ett antal bibliotek där ute som du kan använda för att tolka strängen `User-Agent` i komponenter som operativsystem, enhet och så vidare. Mer information finns i [ua-parser-projektet](https://github.com/tobie/ua-parser).

Med den här nya informationen kan du bättre förstå hur användare kommer åt din webbplats. Sedan kan ni skräddarsy deras upplevelser eller skapa marknadsföringskampanjer för vissa grupper.

## Relaterad

* [Spåra hänvisningskälla för order via [!DNL Google Anaytics] E-Commerce](../importing-data/integrations/google-ecommerce.md)
* [Spåra hänvisningskälla för användare i databasen](../analysis/google-track-user-acq.md)
* [Upptäck era mest värdefulla förvärvskällor och kanaler](../analysis/most-value-source-channel.md)
* [Anslut ditt [!DNL Google Adwords] konto](../importing-data/integrations/google-adwords.md)
* [Öka avkastningen på era annonskampanjer](../analysis/roi-ad-camp.md)
* [Hur fungerar  [!DNL Google Analytics] UTM-attribuering?](../analysis/utm-attributes.md)
