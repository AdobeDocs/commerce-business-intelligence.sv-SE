---
title: Öka avkastningen på era annonskampanjer
description: Lär dig mer om några olika metoder för att utvärdera hur kampanjen fungerar.
exl-id: 4f2bf408-eeaf-4dbf-b62e-89426734640a
role: Admin, User
feature: Data Warehouse Manager, Reports, Campaigns
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1237'
ht-degree: 0%

---

# Reklamkampanjer och avkastning

[!DNL Adobe Commerce Intelligence] gör att du enkelt kan [kombinera information om reklamkostnader och intäkter](../../data-analyst/importing-data/integrations/google-adwords.md) från databasen. Detta hjälper er att identifiera vilka kampanjer som ger störst avkastning på investeringen. I det här avsnittet beskrivs några olika metoder för att utvärdera hur kampanjen fungerar.

## Förutsättningar

* Importera era reklamkostnadsuppgifter:
   * [Koppla samman [!DNL Google AdWords] till [!DNL Commerce Intelligence]](../importing-data/integrations/google-adwords.md): Detta synkroniserar dina [!DNL Adwords] utgifter i [!DNL Commerce Intelligence]
   * [Överför andra annonskostnadsuppgifter](../importing-data/connecting-data/import-offline-ad-data.md): Detta rekommenderas för kanaler utan direktanslutning till [!DNL Commerce Intelligence]
   * Om du importerar kostnadsdata från flera källor kan du [konsolidera](../../best-practices/consolidating-your-tables.md) data i [!DNL Commerce Intelligence]. Bara [skicka en supportanmälan](../../guide-overview.md#Submitting-a-Support-Ticket).
* [Spåra kanaldata för kundvärvning](../analysis/google-track-user-acq.md)

## Kampanjer för att värva användare

Kampanjer som riktar sig till kundvärvning kan mätas ur många olika perspektiv, bland annat:

1. Antalet nya användare som skaffats av kampanjer
1. Konverteringsgraden från registrering till inköp av kampanjer
1. Avkastningen på kampanjerna baseras på det genomsnittliga värdet för användarlivstid (LTV)

Analyserna (1) och (2) ovan utforskas i en separat självstudiekurs om [identifiera era främsta marknadsföringskanaler](../analysis/most-value-source-channel.md). Här utforskar du analys (3) för att mäta kampanjens avkastning över tid. Detta ger svar på om användare som förvärvats från en viss kampanj genererade tillräckligt många intäkter för att täcka kostnaden för förvärvet.

>[!NOTE]
>
>I det här exemplet antas att alla kampanjkostnader uteslutande användes för att förvärva nya användare. I själva verket delas kampanjkostnaden också med att köpa okonverterade besök, upprepa köpare och så vidare. Genom att anta att alla kostnader används för att förvärva nya registrerade användare, redovisar den resulterande avkastningen för det värsta scenariot (högsta kostnaden per förvärv). Du kan vara säker på att den faktiska avkastningen är högre än din beräkning.
>
>Exempel: Om ni spenderade 20 dollar på en kampanj som genererade 10 nya användare och 10 återkommande köpare, blir den faktiska kostnaden per ny användare 1 USD. Men med antagandet att alla kostnader gick till att förvärva nya användare blir kostnaden per förvärv $2.

**1. Börja med att skapa ett diagram som segmenterar era annonskostnader efter kampanjer:**

1. Skapa en [!UICONTROL Metric] som summerar dina utgifter över tid
1. Gå till [!UICONTROL Data > Metrics]
1. Välj `Add New Metric` och väljer [!DNL `Adwords...`] tabell som spelar in [!DNL AdWords] kostnadsdata.
1. Ge mätverktyget ett namn (till exempel [!UICONTROL AdWord Cost])
1. Utför en **Summa** på `adCost` kolumn i [!DNL Adwords...] tabell (Ändra) sorterad efter `date` kolumn.
   ![](../../assets/success-add-new-metric.png)<!--="500" height="303"}-->
1. Klicka `Back to Metric List` längst upp och gå till en kontrollpanel.

1. Skapa en rapport som segmenterar utgifter efter kampanjer
1. Klicka på en kontrollpanel [!UICONTROL Add Report > Create report]
1. Välj [!UICONTROL Adword Cost] mått som du just har skapat
1. Ange [!UICONTROL Time period] till `All-time`och [!UICONTROL Interval] till `None`
1. Under `Group by` flik, lägga till `campaign` as [!UICONTROL grouping field]och klicka `Add All` i lådan.
1. Den här rapporten visar din heltidsinformation [!DNL AdWords] kostnad per kampanj

**2. Skapa en rapport som räknar nya användare efter kampanjer:**

1. Klicka på en kontrollpanel **[!UICONTROL Add Report > Create report]**
1. Välj `New users` mått som räknar antalet nya registrerade användare över tiden
1. Ange [!UICONTROL Time period] till `All-time`och [!UICONTROL Interval] till `None`
1. Under `Group by` flik, lägga till `campaign` as `grouping field`och klicka **`Add All`** i kartongen
1. Den här rapporten visar era heltidsregistrerade användare efter kampanjer

**3. Skapa en rapport som segmenterar genomsnittlig användarvänlighet per kampanj:**

1. Klicka på en kontrollpanel **[!UICONTROL Add Report > Create report]**
1. Välj `Average lifetime revenue` mått som beräknar en genomsnittlig användares livstidsintäkt
1. Ange [!UICONTROL Time period] till `All-time`och [!UICONTROL Interval] till `None`
1. Under `Group by` flik, lägga till `campaign` eller `utm\_campaign` as [!UICONTROL grouping field]och klicka `Add All` i kartongen
1. Den här rapporten visar era genomsnittliga intäkter för användarlivstid per kampanjer

**Beräkna avkastningen på kampanjinvesteringen genom att samla dessa tre analyser i en enda rapport:**

1. Klicka på en kontrollpanel **[!UICONTROL Add Report > Create new report]**
1. Lägg till som indata, använd de tre mätvärdena som används ovan. Varje bokstav tilldelas en bokstav (till exempel\[`A`\], \[`B`\] och \[`C`\])
1. [!UICONTROL Cost]: Lägg till den metriska AdWords-kostnaden - det här är variabeln \[A\]. Detta returnerar kostnad per kampanj.
1. [!UICONTROL Users]: Lägg till måtten Nya användare - det här är variabeln \[B\]. Detta returnerar antalet användare per kampanj.
1. [!UICONTROL LTV]: Lägg till den genomsnittliga livslängdsintäkten för måttet - det här är variabeln \[`C`\]. Detta returnerar LTV efter kampanjer.

1. Klicka på ikonen Dölj bredvid ordet Diagram så att du kan fokusera på tabellen
1. Används nu `Add Formula` för att kombinera dessa mätvärden, enligt följande:
1. [!UICONTROL ROI]: Ange formeln `(\[C\]-\[A\]/\[B\])/(\[A\]/\[B\])`, om \[`A`\] representerar `Ad Cost by Campaigns`, \[`B`\] representerar `New users by campaigns`och \[`C`\] `LTV by campaigns`. Detta returnerar förhållandet (genomsnittlig användarkostnad per förvärv - genomsnittlig kostnad per förvärv) / (genomsnittlig kostnad per förvärv)
1. [!UICONTROL Avg Return per User]: Ange formeln **\[`C`\]-(\[`A`\]/\[`B`\])**. Detta returnerar den genomsnittliga marginalen för en användare genom att beräkna (genomsnittlig användarkostnad per förvärv).
1. [!UICONTROL CPA]: Ange formeln **`\[A\]/\[B\]`**. Detta returnerar den faktiska kampanjens kostnad per förvärv.
1. Andra möjliga mätvärden att inkludera från [!DNL AdWords] data innehåller summor  `Impressions` och `adClicks` (från [!DNL AdWords] data), tillsammans med summan `number of orders` som görs via en viss kampanj.
1. Det kan också vara intressant att beräkna avkastningen på investeringen baserat på LTV 30 dagar och 90 dagar efter det att en användare registrerat sig eller gör ett första köp.

1. Du kan klicka och dra mätvärden och formler för att ändra ordning på kolumnerna i rapporten
1. Ge rapporten ett namn och se till att den sparas som en tabell.

## Produktkampanjer

Kör ni produktspecifika annonser? I så fall kan ni mäta avkastningen på dessa kampanjer genom att beräkna intäkter/kostnad för specifika produkter.

>[!NOTE]
>
>I det här exemplet antas att alla kampanjkostnader uteslutande användes för att generera inköp av specifika produkter. Om man utgår ifrån att alla kostnader spenderas på att generera inköp, utgör den resulterande avkastningen det värsta scenariot (den högsta kostnaden per inköp). Du kan vara säker på att den faktiska avkastningen är högre än den här beräkningen. Exempel: Om ni spenderade 20 dollar på en kampanj som genererade 10 nya användare och 10 inköp blir den faktiska kostnaden per inköp 1 USD. Under antagandet att alla kostnader gick för att förvärva nya användare är kostnaden per inköp $2.

Innan du börjar [skicka en supportanmälan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) för att koppla följande dimensioner till radobjektregistret (`sales\_flat\_order\_item, order\_item`):

* Orderns källa (om du bara spårar hänvisningskälla på användarnivå ska du ansluta till användarens källa)
* Beställningens kampanj (om du bara spårar hänvisningskälla på användarnivå ska du gå med i användarens kampanj)
* Orderns medium (om du bara spårar hänvisningskälla på användarnivå ska du gå med i användarens medium)

**1. Börja nu med att skapa ett diagram som returnerar intäkter per kampanj för specifika produkter:**

1. Klicka på en kontrollpanel **[!UICONTROL Add Report > Create new report]**
1. Välj `Revenue by items` mått som beräknar intäkt på radartikelnivå
1. Ange [!UICONTROL Time period] till `All-time`och [!UICONTROL Interval] till `None`
1. Under `Filter by` flik, lägga till `product name 'IN'` Produkt `A`, produkt `B`, produkt `C`, ...&quot; och inkludera alla produktnamn som är riktade till din kampanj avgränsade med kommatecken (till exempel `product name 'IN' yellow t-shirt`, `red t-shirt, blue t-shirt`)
1. Under `Group by` flik, lägga till `order's campaign` eller `order's utm\_campaign` as `grouping` och klicka **[!UICONTROL Add All]** i kartongen
1. I den här rapporten visas intäkterna för specifika produkter per kampanj

**2. Om du vill beräkna avkastningen kombinerar du statistik igen i en rapport:**

1. Klicka på en kontrollpanel **[!UICONTROL Add Report > Create new report]**
1. Lägg till `Revenue by items` mätvärden, följa filtret och gruppera efter anvisningar från kampanjen för specifika produkter ovan och klicka på **[!UICONTROL Hide]** under måttets skalära värde
1. Lägg till [!DNL AdWords Cost] mätvärden, följt av filtret och gruppera efter riktning från `Ad cost by campaigns` rapport som du utforskat i `User acquisition campaigns` avsnitt ovan, sedan klicka **[!UICONTROL Hide]** under måttets skalära värde
1. Lägg till formler med de här måtten på plats:
1. [!UICONTROL ROI]: Ange formeln `\[A\]/\[B\]`, if `\[A\]` representerar `Revenue per campaign for specific product(s)` och `\[B\]` representerar `Ad cost by campaigns`. Detta returnerar förhållandet (intäkt för specifika produkter) / (kampanjkostnad)
1. [!UICONTROL Return]: Ange formeln `\[A\]-\[B\]`. Detta returnerar den genomsnittliga marginalen för en användare genom att beräkna (genomsnittlig användarkostnad per förvärv) - (genomsnittlig kostnad per förvärv)
1. (Valfritt) [!UICONTROL Revenue]: Visa `Revenue by items` mätvärden för att se intäkter för specifika produkter per kampanj
1. (Valfritt) [!UICONTROL Cost]: Visa `AdWords Cost` mätvärden för att se kostnaden för kampanjer

1. Ge rapporten ett namn och se till att den sparas som en tabell

**3. Upprepa steg 1 och 2 ovan för var och en av dina annonserade produkter eller produktgrupper.**

## Relaterad dokumentation

* [Spåra hänvisningskälla för order via [!DNL Google Analytics] E-handel](../importing-data/integrations/google-ecommerce.md)
* [Spåra hänvisningskälla för användare i databasen](../analysis/google-track-user-acq.md)
* [Spåra användarenhetsdata, webbläsardata och operativsystemsdata i databasen](../analysis/track-usr-dev-browser.md)
* [Upptäck era mest värdefulla förvärvskällor och kanaler](../analysis/most-value-source-channel.md)
* [Koppla samman [!DNL Google Adwords] konto](../importing-data/integrations/google-adwords.md)
* [Hur [!DNL Google Analytics] UTM-attribueringsarbete?](../analysis/utm-attributes.md)
* [Fem bästa sätten att tagga UTM i [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
