---
title: Google Analytics och UTM Attribution
description: Läs om Google Analytics källattribueringsprocess.
exl-id: 48b8a3d3-f1ac-4d3f-8f65-db1245c9ae0a
role: Admin, Data Architect, Data Engineer, User
feature: Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '760'
ht-degree: 0%

---

# [!DNL Google Analytics] och UTM-attribut

Det är viktigt att [spåra källan för användarförvärv](../../data-analyst/analysis/google-track-user-acq.md) för att [identifiera de annonskampanjer som fungerar bäst](../../data-analyst/analysis/most-value-source-channel.md). I det här avsnittet utforskas källattribueringsprocessen [!DNL Google Analytics]. Med andra ord, vilken del av informationen som registreras när.

## Vad är attribuering?

`Attribution` handlar om att ange en hänvisningskälla för en viss aktivitet. Dessa aktiviteter är vanligtvis makrokonverteringar eller mikrokonverteringar, vilket är makron som **köp**, mikroobjekt som **registrering, e-postregistrering, bloggkommentar** och så vidare.

Helst registreras en hänvisningskälla varje gång en konverteringshändelse inträffar. Men hur bestäms källan?

I verkligheten kommer användarna ofta från många olika källor innan de slår till/utför en mikro- eller makrokonvertering. De kan t.ex. komma till webbplatsen via organiska tjänster, sedan lämna platsen, sedan komma via betalsökningar, sedan lämna platsen och sedan komma direkt till själva webbplatsen. Den här källspårningsinformationen tillhandahålls ofta till webbplatsen via UTM-parametrar, men det finns mer avancerade system där ute också. Fokusera på [UTM](https://support.google.com/analytics/answer/1033867?hl=en&ref_topic=1032998) för dina syften.

## Hur attributerar [!DNL Google Analytics] hänvisningskällor via UTM-parametrar?

När UTM-parametrarna anges på URL:en tolkas de ut och placeras i en [!DNL Google Analytics] [cookie](https://en.wikipedia.org/wiki/HTTP_cookie) . Om en webbplats inte har [!DNL Google Analytics] är det ingen mening med att ha UTM. [!DNL Google Analytics] har regler för hur den hanterar en användare som träffar flera URL:er med UTM:er under sin livstid (mer senare). Om webbplatsen är konfigurerad för att hämta UTM-parametrar till en extern databas replikeras det som finns i [!DNL Google Analytics]-cookien vid konverteringen till databasen när en mikro- eller makrokonvertering inträffar.

## Första klicket kontra sista klicket

### Senaste klickattribuering

Den senaste klickattribueringen är den vanligaste attribueringsmodellen som används av [!DNL Google Analytics]. I det här fallet representerar [!DNL Google Analytics]-cookien UTM-parametrarna för den senaste källan före konverteringshändelsen, och detta [registreras i databasen](../../data-analyst/analysis/google-track-user-acq.md). Cookien [!DNL Google Analytics] skriver bara över de tidigare UTM-parametrarna om användaren klickar på en ny URL som innehåller en ny uppsättning UTM-parametrar.

Som exempel kan nämnas en användare som först besöker en webbplats via [!DNL Google Analytics] *betald sökning*, sedan returnerar via *organisk sökning* och slutligen återgår till *webbplatsen direkt* eller via en *e-postlänk* **utan UTM-parametrar** före konverteringshändelsen. I det här exemplet säger cookien [!DNL Google Analytics] att användarens källa är organisk, eftersom detta är den sista källan före konverteringen. Användarens *sökväg* innan den sista konverteringshändelsen ignoreras. Om användaren i stället besökte webbplatsen från en e-postlänk med UTM skulle cookien [!DNL Google Analytics] ange att källan är &quot;e-post&quot;. Om det finns befintliga UTM-parametrar i cookien, och användaren kommer in direkt, visar [!DNL Google Analytics]-cookien UTM-parametrarna i stället för&quot;direct&quot;.

>[!NOTE]
>
>En specifik användares [!DNL Google Analytics]-cookie-parametrar tas bort när cookien [upphör](https://developers.google.com/analytics/devguides/collection/analyticsjs/cookie-usage) eller när en användare rensar sina cookies i webbläsaren.*

### Första klickattribuering

Med vissa betalda attribueringsverktyg kan du fånga &quot;pankakestacken&quot; med källor i en användares sökväg. I den situationen, i ovanstående exempel, skulle först klickattribuering tala om för oss betalsökningar. En del webbplatser kan också implementera egna cookies som används för att ta en packlårstack och lagra den första källan i sin databas.

## Hur analyserar man attribuering?

[!DNL Google Analytics] har en del robusta funktioner i webbgränssnittet som gör att du kan utföra fyra olika attribueringsmodeller:

1. klicka först
1. senaste klickningen
1. linjärt (dividera intäkten jämnt över alla källor i banan)
1. viktad (anpassad attribuering)

Nu när du förstår vad attribueringsmodellen för varje mikro- eller makrokonvertering är blir frågan&quot;Vad gör du med en användares totala konverteringar?&quot;.  Titta till exempel på de UTM-minnen som spelats in baserat på GA:s logik för senaste klickning:

* Användarregister under organisk
* Användarens första köp under betald sökning $5.00
* Användarens andra köp via e-post $50.00
* Användarens tredje köp under 10,00 USD

Här frågar du: &quot;Hur mycket fick jag i intäkter från betalsökningar? Från e-post?  Från organiska?&quot; Man kan säga att svaren är 5, 50 och 10 (oavsett vad den sista källan var), eller också kan man säga att man tilldelar alla intäkter till den första källan (alla 65 går till organisk). Du kan också använda en viktad analys eller använda den linjära modellen (det vill säga ungefär 22 stycken).

## Relaterad dokumentation

* [Spåra hänvisningskälla för order via [!DNL Google Analytics] E-Commerce](../importing-data/integrations/google-ecommerce.md)
* [Spåra hänvisningskälla för användare i databasen](../analysis/google-track-user-acq.md)
* [Spåra användarenhetsdata, webbläsardata och operativsystemsdata i databasen](../analysis/google-track-user-acq.md)
* [Upptäck era mest värdefulla förvärvskällor och kanaler](../analysis/most-value-source-channel.md)
* [Anslut ditt [!DNL Google Adwords] konto](../importing-data/integrations/google-adwords.md)
* [Öka avkastningen på era annonskampanjer](../analysis/roi-ad-camp.md)
* [Fem bästa tillvägagångssätt för UTM-taggning i  [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
