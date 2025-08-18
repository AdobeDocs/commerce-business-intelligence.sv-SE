---
title: Öka avkastningen på era annonskampanjer
description: Lär dig mer om några olika metoder för att utvärdera hur kampanjen fungerar.
exl-id: 4f2bf408-eeaf-4dbf-b62e-89426734640a
role: Admin, User
feature: Data Warehouse Manager, Reports, Campaigns
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1247'
ht-degree: 0%

---

# Advertising Campaigns and ROI

Med [!DNL Adobe Commerce Intelligence] kan du enkelt [kombinera annonsdata och intäktsdata](../../data-analyst/importing-data/integrations/google-adwords.md) från din databas. Detta hjälper er att identifiera vilka kampanjer som ger störst avkastning på investeringen. I det här avsnittet beskrivs några olika metoder för att utvärdera hur kampanjen fungerar.

## Förutsättningar

* Importera era reklamkostnadsuppgifter:
   * [Anslut din [!DNL Google AdWords] till [!DNL Commerce Intelligence]](../importing-data/integrations/google-adwords.md): Detta synkroniserar dina [!DNL Adwords] utgifter i [!DNL Commerce Intelligence]
   * [Överför andra marknadsföringskostnadsdata](../importing-data/connecting-data/import-offline-ad-data.md): Detta rekommenderas för kanaler utan direktanslutning till [!DNL Commerce Intelligence]
   * Om du importerar kostnadsdata från flera källor kan du [konsolidera](../../best-practices/consolidating-your-tables.md) data i [!DNL Commerce Intelligence]. [skicka bara en supportanmälan](../../guide-overview.md#Submitting-a-Support-Ticket).
* [Spåra kanaldata för kundvärvning](../analysis/google-track-user-acq.md)

## Kampanjer för att värva användare

Kampanjer som riktar sig till kundvärvning kan mätas ur många olika perspektiv, bland annat:

1. Antalet nya användare som skaffats av kampanjer
1. Konverteringsgraden från registrering till inköp av kampanjer
1. Avkastningen på kampanjerna baseras på det genomsnittliga värdet för användarlivstid (LTV)

Analyser (1) och (2) ovan utforskas i en separat självstudiekurs om [hur du identifierar dina viktigaste marknadsföringskanaler](../analysis/most-value-source-channel.md). Här utforskar du analys (3) för att mäta kampanjens avkastning över tid. Detta ger svar på om användare som förvärvats från en viss kampanj genererade tillräckligt många intäkter för att täcka kostnaden för förvärvet.

>[!NOTE]
>
>I det här exemplet antas att alla kampanjkostnader uteslutande användes för att förvärva nya användare. I själva verket delas kampanjkostnaden också med att köpa okonverterade besök, upprepa köpare och så vidare. Genom att anta att alla kostnader används för att förvärva nya registrerade användare, redovisar den resulterande avkastningen för det värsta scenariot (högsta kostnaden per förvärv). Du kan vara säker på att den faktiska avkastningen är högre än din beräkning.
>
>Exempel: Om ni spenderade 20 dollar på en kampanj som genererade 10 nya användare och 10 återkommande köpare, är den faktiska kostnaden per ny användare 1 USD. Men med antagandet att alla kostnader gick till att förvärva nya användare blir kostnaden per förvärv $2.

**1. Börja med att skapa ett diagram som segmenterar annonskostnaden efter kampanjer:**

1. Skapa en [!UICONTROL Metric] som summerar din utgift över tid
1. Gå till [!UICONTROL Data > Metrics]
1. Välj `Add New Metric` och välj den [!DNL `Adwords...`]-tabell som registrerar dina [!DNL AdWords]-kostnadsdata.
1. Ge måttet ett namn i måttredigeraren (till exempel [!UICONTROL AdWord Cost])
1. Använd listrutorna för att utföra en **summa** i kolumnen `adCost` i tabellen [!DNL Adwords...] (Ändra) som ordnas av kolumnen `date`.
   ![](../../assets/success-add-new-metric.png)<!--="500" height="303"}-->
1. Klicka `Back to Metric List` överst och gå till en instrumentpanel.

1. Skapa en rapport som segmenterar utgifter efter kampanjer
1. Klicka på [!UICONTROL Add Report > Create report] på en kontrollpanel
1. Välj det [!UICONTROL Adword Cost]-mått som du nyss skapade
1. Ange [!UICONTROL Time period] till `All-time` och [!UICONTROL Interval] till `None`
1. Lägg till `Group by` som `campaign` under fliken [!UICONTROL grouping field] och klicka på `Add All` i rutan.
1. Den här rapporten visar din [!DNL AdWords]-kostnad per kampanj hela tiden

**2. Skapa en rapport som räknar nya användare efter kampanjer:**

1. Klicka på **[!UICONTROL Add Report > Create report]** på en kontrollpanel
1. Välj det `New users`-mått som räknar antalet nya registrerade användare över tiden
1. Ange [!UICONTROL Time period] till `All-time` och [!UICONTROL Interval] till `None`
1. Lägg till `Group by` som `campaign` under fliken `grouping field` och klicka på **`Add All`** i rutan
1. Den här rapporten visar era heltidsregistrerade användare efter kampanjer

**3. Skapa en rapport som segmenterar genomsnittlig användares LTV efter kampanjer:**

1. Klicka på **[!UICONTROL Add Report > Create report]** på en kontrollpanel
1. Välj måttet `Average lifetime revenue` som beräknar en genomsnittlig användares livstidsintäkt
1. Ange [!UICONTROL Time period] till `All-time` och [!UICONTROL Interval] till `None`
1. Lägg till `Group by` eller `campaign` som `utm\_campaign` på fliken [!UICONTROL grouping field] och klicka på `Add All` i rutan
1. Den här rapporten visar era genomsnittliga intäkter för användarlivstid per kampanjer

**Slutligen, beräkna kampanjens avkastning genom att samla dessa tre analyser i en rapport:**

1. Klicka på **[!UICONTROL Add Report > Create new report]** på en kontrollpanel
1. Lägg till som indata, använd de tre mätvärdena som används ovan. Varje bokstav tilldelas en bokstav (till exempel\[`A`\], \[`B`\] och \[`C`\])
1. [!UICONTROL Cost]: Lägg till AdWords-kostnaden för mätvärden - det här är variabeln \[A\]. Detta returnerar kostnad per kampanj.
1. [!UICONTROL Users]: Lägg till måtten Nya användare - det här är variabeln \[B\]. Detta returnerar antalet användare per kampanj.
1. [!UICONTROL LTV]: Lägg till genomsnittlig livslängdsintäkt för mått - det här är variabeln \[`C`\]. Detta returnerar LTV efter kampanjer.

1. Klicka på ikonen Dölj bredvid ordet Diagram så att du kan fokusera på tabellen
1. Använd nu `Add Formula` för att kombinera dessa mått, enligt följande:
1. [!UICONTROL ROI]: Ange formeln `(\[C\]-\[A\]/\[B\])/(\[A\]/\[B\])` om \[`A`\] representerar `Ad Cost by Campaigns`, \[`B`\] representerar `New users by campaigns` och \[`C`\] `LTV by campaigns`. Detta returnerar förhållandet (genomsnittlig användarkostnad per förvärv - genomsnittlig kostnad per förvärv) / (genomsnittlig kostnad per förvärv)
1. [!UICONTROL Avg Return per User]: Ange formeln **\[`C`\]-(\[`A`\]/\[`B`\])**. Detta returnerar den genomsnittliga marginalen för en användare genom att beräkna (genomsnittlig användarkostnad per förvärv).
1. [!UICONTROL CPA]: Ange formeln **`\[A\]/\[B\]`**. Detta returnerar den faktiska kampanjens kostnad per förvärv.
1. Andra möjliga mätvärden som ska inkluderas från [!DNL AdWords]-data är summor av `Impressions` och `adClicks` (från [!DNL AdWords]-data), tillsammans med det totala antalet `number of orders` som görs via en viss kampanj.
1. Det kan också vara intressant att beräkna avkastningen på investeringen baserat på LTV 30 dagar och 90 dagar efter det att en användare registrerat sig eller gör ett första köp.

1. Du kan klicka och dra mätvärden och formler för att ändra ordning på kolumnerna i rapporten
1. Ge rapporten ett namn och se till att den sparas som en tabell.

## Produktkampanjer

Kör ni produktspecifika annonser? I så fall kan ni mäta avkastningen på dessa kampanjer genom att beräkna intäkter/kostnad för specifika produkter.

>[!NOTE]
>
>I det här exemplet antas att alla kampanjkostnader uteslutande användes för att generera inköp av specifika produkter. Om man utgår ifrån att alla kostnader spenderas på att generera inköp, utgör den resulterande avkastningen det värsta scenariot (den högsta kostnaden per inköp). Du kan vara säker på att den faktiska avkastningen är högre än den här beräkningen. Exempel: Om ni spenderade 20 USD på en kampanj som genererade 10 nya användare och 10 inköp blir den faktiska kostnaden per inköp 1 USD. Under antagandet att alla kostnader gick för att förvärva nya användare är kostnaden per inköp $2.

Innan du startar [skickar du en supportanmälan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=sv-SE) för att ansluta följande dimensioner till din tabell med radobjekt (`sales\_flat\_order\_item, order\_item`):

* Orderns källa (om du bara spårar hänvisningskälla på användarnivå ska du ansluta till användarens källa)
* Beställningens kampanj (om du bara spårar hänvisningskälla på användarnivå ska du gå med i användarens kampanj)
* Orderns medium (om du bara spårar hänvisningskälla på användarnivå ska du gå med i användarens medium)

**1. Börja nu med att skapa ett diagram som returnerar intäkter per kampanj för specifika produkter:**

1. Klicka på **[!UICONTROL Add Report > Create new report]** på en kontrollpanel
1. Välj det `Revenue by items`-mått som beräknar intäkt på radartikelnivå
1. Ange [!UICONTROL Time period] till `All-time` och [!UICONTROL Interval] till `None`
1. Lägg till `Filter by` Product `product name 'IN'`, Product `A`, Product `B`, ...&quot; på fliken `C` och inkludera alla produktnamn som kampanjens mål avgränsas med ett kommatecken (till exempel `product name 'IN' yellow t-shirt`, `red t-shirt, blue t-shirt`)
1. Lägg till `Group by` eller `order's campaign` som `order's utm\_campaign`-fält under fliken `grouping` och klicka på **[!UICONTROL Add All]** i rutan
1. I den här rapporten visas intäkterna för specifika produkter per kampanj

**2. Om du vill beräkna avkastningen kombinerar du statistik igen i en rapport:**

1. Klicka på **[!UICONTROL Add Report > Create new report]** på en kontrollpanel
1. Lägg till måttet `Revenue by items`, följ filtret och gruppera efter anvisningar från kampanjen för specifika produkter ovan och klicka på **[!UICONTROL Hide]** under måttets skalära värde
1. Lägg nu till måttet [!DNL AdWords Cost], efter filtret och gruppera efter anvisningar från rapporten `Ad cost by campaigns` som du utforskade i avsnittet `User acquisition campaigns` ovan, och klicka sedan på **[!UICONTROL Hide]** under måttets skalära värde
1. Lägg till formler med de här måtten på plats:
1. [!UICONTROL ROI]: Ange formeln `\[A\]/\[B\]`, om `\[A\]` representerar `Revenue per campaign for specific product(s)` och `\[B\]` representerar `Ad cost by campaigns`. Detta returnerar förhållandet (intäkt för specifika produkter) / (kampanjkostnad)
1. [!UICONTROL Return]: Ange formeln `\[A\]-\[B\]`. Detta returnerar den genomsnittliga marginalen för en användare genom att beräkna (genomsnittlig användarkostnad per förvärv) - (genomsnittlig kostnad per förvärv)
1. (Valfritt) [!UICONTROL Revenue]: Visa måttet `Revenue by items` om du vill visa intäkter för specifika produkter per kampanj
1. (Valfritt) [!UICONTROL Cost]: Visa måttet `AdWords Cost` för att se kostnaden för kampanjer

1. Ge rapporten ett namn och se till att den sparas som en tabell

**3. Upprepa steg 1 och 2 ovan för var och en av dina annonserade produkter eller produktgrupper.**

## Relaterad dokumentation

* [Spåra hänvisningskälla för order via [!DNL Google Analytics] E-Commerce](../importing-data/integrations/google-ecommerce.md)
* [Spåra hänvisningskälla för användare i databasen](../analysis/google-track-user-acq.md)
* [Spåra användarenhetsdata, webbläsardata och operativsystemsdata i databasen](../analysis/track-usr-dev-browser.md)
* [Upptäck era mest värdefulla förvärvskällor och kanaler](../analysis/most-value-source-channel.md)
* [Anslut ditt [!DNL Google Adwords] konto](../importing-data/integrations/google-adwords.md)
* [Hur fungerar  [!DNL Google Analytics] UTM-attribuering?](../analysis/utm-attributes.md)
* [Fem bästa tillvägagångssätt för UTM-taggning i  [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
