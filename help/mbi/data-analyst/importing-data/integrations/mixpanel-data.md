---
title: Förväntade data från blandpanelen
description: Utforska huvuddatatabellerna som du kan importera från Mixpanel till [!DNL MBI] konto.
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 0%

---

# Förväntat [!DNL Mixpanel] data

Efter [du har anslutit din [!DNL Mixpanel] konto](../integrations/mixpanel.md)kan du använda [data warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) för att enkelt spåra relevanta datafält för analys.

I den här artikeln utforskar vi de viktigaste datatabellerna som du kan importera från [!DNL Mixpanel] i [!DNL MBI] konto. Följande tabeller skapas i data warehouse efter att Mixpanel har anslutits. Om du vill visa alla fält som är tillgängliga för spårning klickar du på länkarna i tabellnamnskolumnen.

>[!NOTE]
>
>På grund av begränsningarna i [!DNL Mixpanel] API, historiska data - data som är äldre än sju (7) dagar från datumet för anslutningen till [!DNL MBI] - kommer inte att replikeras.

| **Tabellnamn** | **Beskrivning** |
|-----|-----|
| [`mixpanel\_export`](https://mixpanel.com/docs/api-documentation/exporting-raw-data-you-inserted-into-mixpanel#datafeed) | Tabellen innehåller råa händelsedata, inklusive händelse-, händelsedatum- och plattformskucket. |
| [`mixpanel\_funnels`](https://mixpanel.com/docs/api-documentation/data-export-api#funnels-default) | Den här tabellen innehåller data om dina trattar, inklusive tratt-ID, trattlängden (# av dagar som användaren måste slutföra tratten) samt start- och slutdatum för tratten. |
| [`mixpanel\_engage`](https://mixpanel.com/docs/api-documentation/data-export-api#engage-default) | Detta innehåller data från People Analytics, inklusive sessions-ID:n, sid- och användarinformation samt datum/tid då användaren senast sågs. |

{style=&quot;table-layout:auto&quot;}

## Relaterad dokumentation

* [Ansluter [!DNL Mixpanel]](../integrations/mixpanel.md)
* [Återautentisera integreringar](https://support.magento.com/hc/en-us/articles/360016733151-Reauthenticating-integrations)
