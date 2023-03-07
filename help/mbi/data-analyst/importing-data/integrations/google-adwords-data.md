---
title: Förväntade Google Adwords-data
description: Lär dig hur du kan använda Data warehouse Manager för att enkelt spåra relevanta datafält för analys.
exl-id: b0085683-7bb1-4da2-b343-4309e4796f0c
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---

# Förväntade Google Adwords-data

Efter [du har anslutit din [!DNL Google Adwords] konto](../integrations/google-adwords.md)kan du använda [data warehouse Manager](../../data-warehouse-mgr/tour-dwm.md) för att enkelt spåra relevanta datafält för analys.

Det finns två tabeller som kan replikeras till Data warehouse: `campaigns[account-id]` och `adwords[account-id]`.

The `campaigns` table *ska användas som standard* så att du kan börja med att synkronisera alla relevanta fält från tabellen.

The `adwords` tabellen innehåller fyra kolumner som inte finns i `campaigns` tabell:

* `keyword`
* `adContent`
* `adDestinationUrl`
* `adGroup`

När du är intresserad av att göra en analys som tar hänsyn till dessa attribut måste du använda `adwords` tabell.

>[!IMPORTANT]
>
>Den här tabellen exkluderar rader där alla fyra kolumnerna är `null`.

Här följer en titt på det förväntade schemat för båda tabellerna:

## `Campaigns` table

The `campaigns` tabellen innehåller följande kolumner:

| **Kolumn** | **Beskrivning** |
|-----|-----|
| `\_id` | Registrets primärnyckel |
| `accountId` | Konto-ID |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | Totalt antal klick för dagen |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adcost) | Total kostnad för kampanjen för dagen |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] Kampanj-ID |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | Kampanjnamn (till exempel [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=time&amp;jump=ga_date) | Datumet då kampanjen kördes |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_impressions) | Antal visningar för dagen |
| `profileId` | Profil-ID |
| `profileName` | Profilnamnet |
| `\_updated\_at` | Datum och tid för den senaste uppdateringen för den här raden |

{style="table-layout:auto"}

## AdWords table

The `adwords` tabellen innehåller följande kolumner:

| **Kolumn** | **Beskrivning** |
|-----|-----|
| `\_id` | Registrets primärnyckel |
| `accountId` | Konto-ID |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | Totalt antal klick för dagen |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adcost) | Total kostnad för kampanjen för dagen |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | [!DNL Adwords] Kampanj-ID |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | Kampanjnamn (till exempel [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=time&amp;jump=ga_date) | Datumet då kampanjen kördes |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_impressions) | Antal visningar för dagen |
| `profileId` | Profil-ID |
| `profileName` | Profilnamnet |
| `\_updated\_at` | Datum och tid för den senaste uppdateringen för den här raden |
| `keyword` | Nyckelordet för kampanjen |
| `adContent` | Den första textraden för onlinekampanjen |
| `adDestinationUrl` | Den URL som [!DNL Adwords] refererad trafik |
| `adGroup` | Namnet på [!DNL Adwords] annonsgrupp |

{style="table-layout:auto"}

Med dessa data kan du börja skapa [mått ](../../../data-user/reports/ess-manage-data-metrics.md) och [rapporter](../../../tutorials/using-visual-report-builder.md) baserat på utgiftsdata och [skapa avkastning på investeringen](../../analysis/roi-ad-camp.md).

## Konsoliderade tabeller

Adobe rekommenderar att du skapar en `consolidated ad spend` tabell för att kombinera data från alla era olika annonskällor till en enda tabell. På så sätt kan ni använda en enda uppsättning mätvärden för annonsanalys.

Utan en konsoliderad tabell, om du skapar en vacker kontrollpanel på `adwords` måste du replikera rapporten eller skapa dubblettvärden för att jämföra data med [!DNL Facebook Ads] data. Genom att använda en konsoliderad tabell kan du smidigt införliva [!DNL Facebook Ads] data med befintliga [!DNL Adwords] rapporter. Ni kan även segmentera per annonsplattform.

Om du redan har synkroniserat fälten ovan kan du kontakta oss för att konsolidera dina annonskostnader.
