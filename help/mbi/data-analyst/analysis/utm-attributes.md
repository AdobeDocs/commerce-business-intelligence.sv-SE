---
title: Google Analytics och UTM-attribuering
description: Läs mer om Google Analytics källattribueringsprocessen.
exl-id: 48b8a3d3-f1ac-4d3f-8f65-db1245c9ae0a
role: Admin, Data Architect, Data Engineer, User
feature: Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---

# [!DNL Google Analytics] och UTM-attribut

Det är viktigt att [spåra källa för användarförvärv](../../data-analyst/analysis/google-track-user-acq.md) till [identifiera de annonskampanjer som fungerar bäst](../../data-analyst/analysis/most-value-source-channel.md). Det här avsnittet förklarar [!DNL Google Analytics] källattribueringsprocess. Med andra ord, vilken information som registreras när.

## Vad är attribuering?

`Attribution` handlar om att ange en hänvisningskälla för en viss aktivitet. Sådana aktiviteter är vanligtvis makrokonverteringar eller mikrokonverteringar, vilket är exempel på makron **köp**, mikro saker som **registrering, e-postregistrering, bloggkommentar,** och så vidare.

Helst registreras en hänvisningskälla varje gång en konverteringshändelse inträffar. Men hur bestäms källan?

I verkligheten kommer användarna ofta från många olika källor innan de slår till/utför en mikro- eller makrokonvertering. De kan t.ex. komma till webbplatsen via organiska tjänster, sedan lämna platsen, sedan komma via betalsökningar, sedan lämna platsen och sedan komma direkt till själva webbplatsen. Den här källspårningsinformationen tillhandahålls ofta till webbplatsen via UTM-parametrar, men det finns mer avancerade system där ute också. Fokusera på [UTM](https://support.google.com/analytics/answer/1033867?hl=en&amp;ref_topic=1032998).

## Hur [!DNL Google Analytics] attributreferenskällor via UTM-parametrar?

När UTM-parametrarna anges på URL:en tolkas de ut och placeras i en [!DNL Google Analytics] [cookie](https://en.wikipedia.org/wiki/HTTP_cookie). Om en webbplats inte har [!DNL Google Analytics]är det ingen mening med att ha UTM. [!DNL Google Analytics] har regler för hur den hanterar en användare som träffar flera URL:er med UTM:er under sin livstid (mer därtill senare). Om webbplatsen är konfigurerad att hämta UTM-parametrar till en extern databas när en mikro- eller makrokonvertering inträffar, oavsett vad som finns i [!DNL Google Analytics] cookie vid konverteringen replikeras till databasen.

## Första klickningen kontra sista klickningen

### Senaste klickattribuering

Sista klickattribuering är den vanligaste attribueringsmodellen som används av [!DNL Google Analytics]. I det här fallet [!DNL Google Analytics] cookie representerar UTM-parametrarna för den senaste källan före konverteringshändelsen, och detta är [som registrerats i databasen](../../data-analyst/analysis/google-track-user-acq.md). The [!DNL Google Analytics] cookie skriver bara över de tidigare UTM-parametrarna om användaren klickar på en ny URL som innehåller en ny uppsättning UTM-parametrar.

Tänk dig en användare som först besöker en webbplats via [!DNL Google Analytics] *betalsökningar* returnerar sedan via *organisk sökning*, och till sist kommer tillbaka till *direkt* eller via *e-postlänk* **utan UTM-parametrar** före konverteringshändelsen. I det här exemplet [!DNL Google Analytics] cookie säger att användarens källa är organisk, eftersom det är den sista källan före konverteringen. The *bana* av användaren innan den sista konverteringshändelsen ignoreras. Om användaren i stället besökte webbplatsen via en e-postlänk med UTM, kommer [!DNL Google Analytics] cookie säger att källan är &quot;e-post&quot;. Om det därför finns UTM-parametrar i cookien och användaren kommer in direkt, kommer [!DNL Google Analytics] cookie visar UTM-parametrarna i stället för &quot;direct&quot;.

>[!NOTE]
>
>En specifik användares [!DNL Google Analytics] cookie-parametrar tas bort när cookien [förfaller](https://developers.google.com/analytics/devguides/collection/analyticsjs/cookie-usage)eller när en användare rensar sina cookies i webbläsaren.*

### Första klickattribuering

Med vissa betalda attribueringsverktyg kan du fånga &quot;pankakestacken&quot; med källor i en användares sökväg. I den situationen, i ovanstående exempel, skulle först klickattribuering tala om för oss betalsökningar. En del webbplatser kan också implementera egna cookies som används för att ta en packlårstack och lagra den första källan i sin databas.

## Hur analyserar man attribuering?

[!DNL Google Analytics] har en viss robust funktionalitet i webbgränssnittet som gör att du kan utföra fyra olika attribueringsmodeller:

1. klicka först
1. klicka senast
1. linjärt (dividera intäkterna jämnt över alla källor i banan)
1. viktad (anpassad attribuering)

Nu när du förstår vad attribueringsmodellen för varje mikro- eller makrokonvertering är blir frågan&quot;Vad gör du med en användares totala konverteringar?&quot;.  Titta till exempel på de UTM-minnen som spelats in baserat på GA:s logik för senaste klickning:

* Användarregister under organisk
* Användarens första köp under betald sökning $5.00
* Användarens andra köp via e-post $50.00
* Användarens tredje köp under 10,00 USD

Här frågar du: &quot;Hur mycket fick jag i intäkter från betalsökningar? Från e-post?  Från organiska?&quot; Man kan säga att svaren är 5, 50 och 10 (oavsett vad den sista källan var), eller också kan man säga att man tilldelar alla intäkter till den första källan (alla 65 går till organisk). Du kan också använda en viktad analys eller använda den linjära modellen (det vill säga ungefär 22 stycken).

## Relaterad dokumentation

* [Spåra hänvisningskälla för order via [!DNL Google Analytics] E-handel](../importing-data/integrations/google-ecommerce.md)
* [Spåra hänvisningskälla för användare i databasen](../analysis/google-track-user-acq.md)
* [Spåra användarenhetsdata, webbläsardata och operativsystemsdata i databasen](../analysis/google-track-user-acq.md)
* [Upptäck era mest värdefulla förvärvskällor och kanaler](../analysis/most-value-source-channel.md)
* [Koppla samman [!DNL Google Adwords] konto](../importing-data/integrations/google-adwords.md)
* [Öka avkastningen på era annonskampanjer](../analysis/roi-ad-camp.md)
* [Fem bästa sätten att tagga UTM i [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
