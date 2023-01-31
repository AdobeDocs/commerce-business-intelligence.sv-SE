---
title: Google Analytics och UTM-attribuering
description: Läs mer om Google Analytics källattribueringsprocessen.
exl-id: 48b8a3d3-f1ac-4d3f-8f65-db1245c9ae0a
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 0%

---

# Google Analytics och UTM-attribuering

Det är viktigt att [spåra källa för användarförvärv](../../data-analyst/analysis/google-track-user-acq.md) till [identifiera de annonskampanjer som fungerar bäst](../../data-analyst/analysis/most-value-source-channel.md). I den här självstudiekursen utforskar vi Google Analytics källattribueringsprocess. Med andra ord, vilken information som registreras när.

## Vad är attribuering?

`Attribution` handlar om att ange en hänvisningskälla för en viss aktivitet. Sådana aktiviteter är vanligtvis makrokonverteringar eller mikrokonverteringar, vilket är exempel på makron **köp**, mikro saker som **registrering, e-postregistrering, bloggkommentar,** och så vidare.

Helst registreras en hänvisningskälla varje gång en konverteringshändelse inträffar. Men hur bestäms källan?

I själva verket kommer användarna ofta från många olika källor innan de slår till/utför en mikro- eller makrokonvertering (de kan till exempel komma till webbplatsen via organiska, sedan lämna den, komma via betalsökningar, sedan lämna den och sedan komma direkt till själva webbplatsen). Den här källspårningsinformationen tillhandahålls ofta till webbplatsen via UTM-parametrar, men det finns mer avancerade system där ute också. För våra syften kommer vi att fokusera på [UTM](https://support.google.com/analytics/answer/1033867?hl=en&amp;ref_topic=1032998).

## Hur [!DNL Google Analytics] attributreferenskällor via UTM-parametrar?

När UTM-parametrarna anges på URL:en tolkas de ut och placeras i en [!DNL Google Analytics] [cookie](https://en.wikipedia.org/wiki/HTTP_cookie). Om en webbplats inte har [!DNL Google Analytics]är det ingen mening med att ha UTM. [!DNL Google Analytics] har regler för hur den hanterar en användare som träffar flera URL:er med UTM:er under sin livstid (mer senare). Om webbplatsen är konfigurerad för att hämta UTM-parametrar till en extern databas kan det hända när en mikro- eller makrokonvertering inträffar, oavsett vad som finns i [!DNL Google Analytics] cookie vid konverteringen replikeras till databasen.

## Första klickningen kontra sista klickningen

### Senaste klickattribuering

Sista klickattribuering är den vanligaste attribueringsmodellen som används av [!DNL Google Analytics]. I det här fallet [!DNL Google Analytics] cookie representerar UTM-parametrarna för den senaste, eller senaste, källan före konverteringshändelsen, och detta är vad [som registrerats i databasen](../../data-analyst/analysis/google-track-user-acq.md). Observera att [!DNL Google Analytics] cookie skriver bara över de tidigare UTM-parametrarna om användaren klickar på en ny URL som innehåller en ny uppsättning UTM-parametrar.

Tänk dig en användare som först besöker en webbplats via [!DNL Google Analytics][!DNL Google Analytics][!DNL Google Analytics] *betalsökningar* returnerar sedan via *organisk sökning*, och till sist kommer tillbaka till *direkt* eller via *e-postlänk* **utan UTM-parametrar** före konverteringshändelsen. I det här exemplet [!DNL Google Analytics] cookie säger att användarens källa är organisk, eftersom detta är den sista källan före konverteringen. The *bana* av användaren innan den sista konverteringshändelsen ignoreras. Om användaren i stället besökte webbplatsen via en e-postlänk med UTM, kommer [!DNL Google Analytics] cookie säger att källan är &quot;e-post&quot;. Om det därför finns UTM-parametrar i cookien och användaren kommer in direkt, kommer [!DNL Google Analytics] cookie visar alltid UTM-parametrar i stället för &quot;direct&quot;.

>[!NOTE]
>
>En specifik användares [!DNL Google Analytics] cookie-parametrar tas bort när cookien [förfaller](https://developers.google.com/analytics/devguides/collection/analyticsjs/cookie-usage), eller när en användare rensar sina cookies i webbläsaren.*)

### Första klickattribuering

Med vissa betalda attribueringsverktyg kan du fånga &quot;pantårtstacken&quot; med källor i en användares sökväg. I den situationen, i det här exemplet, skulle först klickattribuering tala om för oss betalsökningar. En liten del av webbplatserna kan också implementera egna cookies som spelar in en pusselstack och lagrar den första källan i sin databas.

## Hur analyserar man attribuering?

[!DNL Google Analytics] har en del mer robust funktionalitet i webbgränssnittet som gör att du kan utföra fyra olika attribueringsmodeller: första klickningen, sista klickningen, linjär (dividera intäkterna jämnt mellan alla källor i banan) och viktad (anpassad attribuering).

Nu när du förstår vad attribueringsmodellen för varje mikro- eller makrokonvertering är blir frågan vad du gör med en användares totala konverteringar?  Titta till exempel på de UTM-minnen som spelats in baserat på GA:s logik för senaste klickning:

* Användarregister under organisk
* Användarens första köp under betald sökning $5.00
* Användarens andra köp via e-post $50.00
* Användarens tredje köp under 10,00 USD

Här frågar du: Hur stor intäkt fick jag av betalsökningar?  Från e-post?  Från organisk?  Du kan säga att svaren är 5, 50 och 10 (det vill säga, oavsett var den sista källan fanns), eller också kan du säga att du tilldelar alla intäkter till den första källan (det vill säga att alla 65 går till organisk). Du kan också använda en viktad analys eller använda den linjära modellen (det vill säga ungefär 22 stycken).

## Relaterad dokumentation

* [Spåra hänvisningskälla för order via [!DNL Google Analytics] E-handel](../importing-data/integrations/google-ecommerce.md)
* [Spåra hänvisningskälla för användare i databasen](../analysis/google-track-user-acq.md)
* [Spåra användarenhets-, webbläsar- och operativsystemsdata i databasen](../analysis/google-track-user-acq.md)
* [Upptäck era mest värdefulla förvärvskällor och kanaler](../analysis/most-value-source-channel.md)
* [Koppla samman [!DNL Google Adwords] konto](../importing-data/integrations/google-adwords.md)
* [Öka avkastningen på era annonskampanjer](../analysis/roi-ad-camp.md)
* [5 bästa praxis för UTM-taggning i [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
