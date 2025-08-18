---
title: ' [!DNL Adobe Analytics] data förväntades'
description: Lär dig hur du ansluter RDS-instansen.
exl-id: 4df66ec1-c7f3-4b02-8f0f-49cada99c14c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# [!DNL Adobe Analytics] data förväntades

Integrationen [!DNL Adobe Analytics] för [!DNL Adobe Commerce Intelligence] använder API:t [Analytics 2.0 ](https://developer.adobe.com/analytics-apis/docs/2.0/#!AdobeDocs/analytics-2.0-apis/master/README.md).

>[!INFO]
>
>För att vara säker på att du får de data du förväntar dig kan du först skapa en rapport i [!DNL Adobe Analytics] Workspace med önskade mått och mått. På så sätt kan du kontrollera om data är kompatibla och tillgängliga.

En tabell per ansluten rapportserie med namnet `report-suite-<ID>` (där `<ID>` är ett unikt ID som genererats av [!DNL Commerce Intelligence]) skapas i din Data Warehouse.

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
| `start_date` | Startdatum för inkluderade data för raden. `start_date` är alltid 0:00 av samma dag inom en rad. |
| `end_date` | Slutdatum för inkluderade data för raden. `end_date` är alltid 23:59 av samma dag inom en rad. |
| `page_views` | Markerat mätvärde: Det totala antalet sidvisningar för den identifierade tidsperioden. |
| `page` | Markerad dimension: Individuella sidnamn med spårade vyer. |

Kontrollera vilka av de valda måtten och måtten som har data tillgängliga i tabellen [!DNL Commerce Intelligence] med alternativen *sync* eller *unsync* på sidan `Data Warehouse`. Kolumner som inte synkroniseras visas i grått. Om du slutar synkronisera en kolumn kan du börja synkronisera den igen senare.

## Aktuella begränsningar

I det här avsnittet beskrivs begränsningar för [!DNL Adobe Analytics]-integreringen för [!DNL Commerce Intelligence].

| Begränsning | Beskrivning |
| --- | --- |
| `Historical data period` | Precis som med andra tredjepartsintegreringar hämtar [!DNL Adobe Analytics]-integreringen en begränsad mängd historiska data och fortsätter sedan att hålla data uppdaterade. Den historiska perioden är konfigurerad till 2 veckor. |
| `Empty component combinations` | Vissa kombinationer av mätvärden och dimensioner innehåller inga data. Om en sådan kombination har valts för replikering utesluter [!DNL Commerce Intelligence] kolumnen från den replikerade tabellen. Om du inte vill välja en sådan kombination kan du först skapa en rapport i [[!DNL Adobe Analytics] Workspace](https://experienceleague.adobe.com/docs/analytics/analyze/analysis-workspace/home.html) för att bekräfta att du har fått de data du förväntar dig. |
| `Re-authorization cadence` | Omauktorisering av integreringen av [!DNL Adobe Analytics] krävs varannan vecka. Gå till sidan Redigera för integreringen och klicka på **[!UICONTROL Re-Authorize with [!DNL Adobe Analytics]]** om du vill återauktorisera. |
| `One dimension per row` | [!DNL Adobe Analytics] tillhandahåller måttdata för en dimension i taget. Om du väljer flera dimensioner under konfigurationen innehåller varje rad i tabellen [!DNL Commerce Intelligence] ett enda dimensionsvärde och null-värden för varje annan dimension. |
