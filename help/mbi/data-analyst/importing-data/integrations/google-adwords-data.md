---
title: Förväntade Google Adwords-data
description: Lär dig hur du kan använda Data Warehouse Manager för att enkelt spåra relevanta datafält för analys.
exl-id: b0085683-7bb1-4da2-b343-4309e4796f0c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 0%

---

# [!DNL Google Adwords] data förväntades

När [du har anslutit ditt [!DNL Google Adwords] konto](../integrations/google-adwords.md) kan du använda [Data Warehouse Manager](../../data-warehouse-mgr/tour-dwm.md) för att enkelt spåra relevanta datafält för analys.

Det finns två tabeller som kan replikeras till Datan Warehouse:

* `campaigns[account-id]`
* `adwords[account-id]`

`campaigns`-tabellen *ska användas som standard*, så du kan börja med att synkronisera alla relevanta fält från den tabellen.

Tabellen `adwords` innehåller fyra kolumner som inte finns i tabellen `campaigns`:

1. `keyword`
1. `adContent`
1. `adDestinationUrl`
1. `adGroup`

När du är intresserad av att göra en analys som tar hänsyn till dessa attribut måste du använda tabellen `adwords`.

>[!IMPORTANT]
>
>Den här tabellen exkluderar rader där alla fyra kolumnerna är `null`.

Nedan visas ett schema över det förväntade schemat för båda tabellerna.

## [!DNL Campaigns]-tabell

Tabellen `campaigns` innehåller följande kolumner:

| **Kolumn** | **Beskrivning** |
|-----|-----|
| `\_id` | Registrets primärnyckel |
| `accountId` | Konto-ID |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | Totalt antal klick för dagen |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adcost) | Total kostnad för kampanjen för dagen |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | Kampanj-ID för [!DNL Adwords] |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | Kampanjnamn (till exempel [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=time&amp;jump=ga_date) | Datumet då kampanjen kördes |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_impressions) | Antal visningar för dagen |
| `profileId` | Profil-ID |
| `profileName` | Profilnamnet |
| `\_updated\_at` | Datum och tid för den senaste uppdateringen för raden |

{style="table-layout:auto"}

## [!DNL AdWords]-tabell

Tabellen `adwords` innehåller följande kolumner:

| **Kolumn** | **Beskrivning** |
|-----|-----|
| `\_id` | Registrets primärnyckel |
| `accountId` | Konto-ID |
| [`adClicks`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adclicks) | Totalt antal klick för dagen |
| [`adCost`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adcost) | Total kostnad för kampanjen för dagen |
| [`adwordsCampaignID`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_adwordscampaignid) | Kampanj-ID för [!DNL Adwords] |
| [`campaign`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=traffic_sources&amp;jump=ga_campaign) | Kampanjnamn (till exempel [utm\_campaign](https://support.google.com/analytics/answer/1033867?hl=en)) |
| [`date`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=time&amp;jump=ga_date) | Datumet då kampanjen kördes |
| [`impressions`](https://ga-dev-tools.google/dimensions-metrics-explorer/#view=detail&amp;group=adwords&amp;jump=ga_impressions) | Antal visningar för dagen |
| `profileId` | Profil-ID |
| `profileName` | Profilnamnet |
| `\_updated\_at` | Datum och tid för den senaste uppdateringen för raden |
| `keyword` | Nyckelordet för kampanjen |
| `adContent` | Den första textraden för onlinekampanjen |
| `adDestinationUrl` | Den URL som [!DNL Adwords] annonser refererade till |
| `adGroup` | Namnet på ad-gruppen [!DNL Adwords] |

{style="table-layout:auto"}

Med hjälp av dessa data kan du börja skapa [mått](../../../data-user/reports/ess-manage-data-metrics.md) och [rapporter](../../../tutorials/using-visual-report-builder.md) baserat på utgiftsdata och [kombinera dem med livstidsintäkterna för att beräkna avkastningen](../../analysis/roi-ad-camp.md).

## Konsoliderade tabeller

[!DNL Adobe] rekommenderar att du skapar en `consolidated ad spend`-tabell för att kombinera data från alla dina olika annonskällor till en enda tabell. På så sätt kan ni använda en enda uppsättning mätvärden för annonsanalys.

Om du inte har någon konsoliderad tabell och du skapar en vacker kontrollpanel i tabellen `adwords` måste du replikera rapporten eller skapa dubblettmått för att jämföra data med dina [!DNL Facebook Ads]-data. Om du använder en konsoliderad tabell kan du sömlöst införliva [!DNL Facebook Ads]-data med dina befintliga [!DNL Adwords]-rapporter. Ni kan även segmentera per annonsplattform.

Om du redan har synkroniserat fälten ovan, [kontaktar du oss](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) för att konsolidera din annonsutgift.
