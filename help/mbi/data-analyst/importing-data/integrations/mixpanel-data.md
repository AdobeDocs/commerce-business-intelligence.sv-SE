---
title: Förväntade data från blandpanelen
description: Utforska huvuddatatabellerna som du kan importera från Mixpanel till [!DNL Commerce Intelligence] konto.
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '204'
ht-degree: 0%

---

# Förväntat [!DNL Mixpanel] data

Efter [du har anslutit din [!DNL Mixpanel] konto](../integrations/mixpanel.md)kan du använda [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) för att enkelt spåra relevanta datafält för analys.

I det här avsnittet beskrivs de huvuddatatabeller som du kan importera från [!DNL Mixpanel] i [!DNL Commerce Intelligence] konto. Följande tabeller kommer att skapas i Datan Warehouse efter anslutningen [!DNL Mixpanel]. Om du vill visa alla fält som är tillgängliga för spårning klickar du på länkarna i tabellnamnskolumnen.

>[!NOTE]
>
>På grund av begränsningarna i [!DNL Mixpanel] API, historiska data - data som är äldre än sju (7) dagar från datumet för anslutningen till [!DNL Commerce Intelligence] - replikeras inte.

| **Tabellnamn** | **Beskrivning** |
|-----|-----|
| [`mixpanel\_export`](https://developer.mixpanel.com/reference/raw-data-export-api#datafeed) | Tabellen innehåller råa händelsedata, inklusive händelse-, händelsedatum- och plattformskucket. |
| [`mixpanel\_funnels`](https://developer.mixpanel.com/reference/raw-data-export-api#funnels-default) | Den här tabellen innehåller data om dina trattar, inklusive tratt-ID, trattlängden (# av dagar som användaren måste slutföra tratten) samt start- och slutdatum för tratten. |
| [`mixpanel\_engage`](https://developer.mixpanel.com/reference/raw-data-export-api#engage-default) | Detta innehåller data från People Analytics, inklusive sessions-ID:n, sid- och användarinformation samt datum/tid då användaren senast sågs. |

{style="table-layout:auto"}

## Relaterad dokumentation

* [Ansluter [!DNL Mixpanel]](../integrations/mixpanel.md)
* [Återautentisera integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
