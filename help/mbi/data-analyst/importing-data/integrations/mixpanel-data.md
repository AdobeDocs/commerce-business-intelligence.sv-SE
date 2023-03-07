---
title: Förväntade data från blandpanelen
description: Utforska huvuddatatabellerna som du kan importera från Mixpanel till [!DNL MBI] konto.
exl-id: 87bd337a-63fa-44cf-b1fe-c2f34ca86029
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 0%

---

# Förväntat [!DNL Mixpanel] data

Efter [du har anslutit din [!DNL Mixpanel] konto](../integrations/mixpanel.md)kan du använda [data warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) för att enkelt spåra relevanta datafält för analys.

I den här artikeln utforskas huvuddatatabellerna som du kan importera från [!DNL Mixpanel] i [!DNL MBI] konto. Följande tabeller skapas i Data warehouse efter att Mixpanel har anslutits. Om du vill visa alla fält som är tillgängliga för spårning klickar du på länkarna i tabellnamnskolumnen.

>[!NOTE]
>
>På grund av begränsningarna i [!DNL Mixpanel] API, historiska data - data som är äldre än sju (7) dagar från datumet för anslutningen till [!DNL MBI] - replikeras inte.

| **Tabellnamn** | **Beskrivning** |
|-----|-----|
| [`mixpanel\_export`](https://developer.mixpanel.com/reference/raw-data-export-api#datafeed) | Tabellen innehåller råa händelsedata, inklusive händelse-, händelsedatum- och plattformskucket. |
| [`mixpanel\_funnels`](https://developer.mixpanel.com/reference/raw-data-export-api#funnels-default) | Den här tabellen innehåller data om dina trattar, inklusive tratt-ID, trattlängden (# av dagar som användaren måste slutföra tratten) samt start- och slutdatum för tratten. |
| [`mixpanel\_engage`](https://developer.mixpanel.com/reference/raw-data-export-api#engage-default) | Detta innehåller data från People Analytics, inklusive sessions-ID:n, sid- och användarinformation samt datum/tid då användaren senast sågs. |

{style="table-layout:auto"}

## Relaterad dokumentation

* [Ansluter [!DNL Mixpanel]](../integrations/mixpanel.md)
* [Återautentisera integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
