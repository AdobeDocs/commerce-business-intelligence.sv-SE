---
title: Förväntat [!DNL Adobe Analytics] Data
description: Lär dig hur du ansluter RDS-instansen.
exl-id: 4df66ec1-c7f3-4b02-8f0f-49cada99c14c
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# Förväntat [!DNL Adobe Analytics] Data

The [!DNL Adobe Analytics] integration för [!DNL Adobe Commerce Intelligence] använder [Rapporterings-API för Analytics 2.0](https://developer.adobe.com/analytics-apis/docs/2.0/#!AdobeDocs/analytics-2.0-apis/master/README.md).

>[!INFO]
>
>För att vara säker på att du får de data du förväntar dig kan du först skapa en rapport i [!DNL Adobe Analytics] Arbetsyta med önskat mått och mått. På så sätt kan du kontrollera om data är kompatibla och tillgängliga.

Ett register per ansluten rapportsvit anropades `report-suite-<ID>` (där `<ID>` är ett unikt ID som genereras av [!DNL Commerce Intelligence]) skapas i Data warehouse.

Schemat för den här tabellen består av de mått och mått som du valde i konfigurationsprocessen för integrering. Flera ytterligare kolumner genereras också av [!DNL Commerce Intelligence], för identifieringsändamål.

Om du till exempel valde följande mått och dimension under installationen:
- `Metric`: `Page views`
- `Dimension`: `Page`

Tabellen innehåller följande kolumner:

| Kolumnnamn | Beskrivning |
| --- | --- |
| `_id` | Den här kolumnen är primärnyckeln. |
| `_item_hash` | [!DNL Commerce Intelligence] unik identifierare. Den här kolumnen skapas av [!DNL Commerce Intelligence]. |
| `_updated_at` | Den här kolumnen innehåller den senaste gången dataraden uppdaterades. Den har skapats av [!DNL Commerce Intelligence]. |
| `start_date` | Startdatum för inkluderade data för raden. `start_date` är alltid 00:00 på samma dag inom en rad. |
| `end_date` | Slutdatum för inkluderade data för raden. `end_date` är alltid 23:59 samma dag inom en rad. |
| `page_views` | Markerat mätvärde: Det totala antalet sidvisningar för den identifierade tidsperioden. |
| `page` | Vald dimension: Individuella sidnamn med spårade vyer. |

Styr vilka av de valda mätvärdena och dimensionerna som har data tillgängliga i [!DNL Commerce Intelligence] tabell med *synka* eller *osynkad* i `Data Warehouse` sida. Kolumner som inte synkroniseras visas i grått. Om du slutar synkronisera en kolumn kan du börja synkronisera den igen senare.

## Aktuella begränsningar

I det här avsnittet beskrivs begränsningar för [!DNL Adobe Analytics] integration för [!DNL Commerce Intelligence].

| Begränsning | Beskrivning |
| --- | --- |
| `Historical data period` | Precis som med andra tredjepartsintegreringar [!DNL Adobe Analytics] integreringen hämtar en begränsad mängd historiska data och fortsätter sedan att hålla data uppdaterade. Den historiska perioden är konfigurerad till 2 veckor. |
| `Empty component combinations` | Vissa kombinationer av mätvärden och dimensioner innehåller inga data. Om en sådan kombination väljs för replikering, [!DNL Commerce Intelligence] utelämnar kolumnen från den replikerade tabellen. Du kan undvika att välja en sådan kombination genom att först skapa en rapport i dialogrutan [[!DNL Adobe Analytics] Arbetsyta](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html) för att verifiera att ni får de data ni förväntar er. |
| `Re-authorization cadence` | Återgodkännande av [!DNL Adobe Analytics] integrering krävs varannan vecka. Gå till sidan Redigera för integreringen och klicka på **[!UICONTROL Re-Authorize with [!DNL Adobe Analytics]]**. |
| `One dimension per row` | [!DNL Adobe Analytics] innehåller mätdata för en dimension i taget. Om du väljer flera dimensioner under installationen, kan du ange varje rad i [!DNL Commerce Intelligence] tabellen innehåller ett enda dimensionsvärde och null-värden för varje annan dimension. |
