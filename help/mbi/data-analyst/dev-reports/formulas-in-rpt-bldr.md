---
title: Formler i Report Builder
description: Lär dig hur formler kan användas i Report Builder.
exl-id: 7a0ad07a-5bcc-474f-95bc-ccc2b74073b2
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# Formler i `Report Builder`

I [`Report Builder`](../../tutorials/using-visual-report-builder.md)kan du skapa kraftfulla visualiseringar med [definierade mått](../../data-user/reports/ess-manage-data-metrics.md) i ditt konto. Genom att kombinera dessa mätvärden i en formel kan ni få ytterligare insikter från era data. Det här avsnittet handlar om hur formler kan användas i `Report Builder` - hoppar in!

## Vad är en `formula`? {#what}

I `Report Builder`, a `formula` är bara en kombination av en eller flera mätvärden som bygger på någon matematisk logik. Ett typiskt exempel ser ut så här:

![](../../assets/formula-example.png)

I det här exemplet använder du `Number of orders metric (A)` och `Distinct buyers metric (B)`och målet är att svara på frågan: vilket är det genomsnittliga antalet order som mina köpare gör varje månad? Formelns parametrar är:

* `Definition`: Här använder du matematik på indatavärden. I det här exemplet, där antalet order divideras med antalet distinkta köpare, anger vi det genomsnittliga antalet order. Definitionen är därför (A/B).

* `Format`: Returnerar din formel ett tal, en tidsperiod eller ett valutabelopp? Bredvid formelns definition finns en listruta som du kan använda för att ange returens format. I det här fallet är det ett tal.

* `Miscellaneous`: Formelns tidsstämpel, grupperingar, perspektiv och filter ärvs alla av dess indatavärden. Det finns ingenting att göra här!

## Hur kan jag använda `formulas` i mina rapporter? {#how}

Nu när du har gått igenom grunderna kan du titta på några exempel.

### Exempel: Jag vill ta reda på vilken procentandel av min intäkt som kan tillskrivas förstagångsbeställningar.

![Använda formler för att hitta procentandelen av intäkt som härrör från förstagångsorder](../../assets/first_time_orders.gif)

I det här exemplet använde du `Revenue` och `Revenue (first time orders)` mätvärden. Genom att dela upp `Revenue (first time orders)(B)` mått efter `Revenue metric (A)` och ange returformatet till `Percent`hittar du den procentandel av intäkterna som kan hänföras till förstagångsbeställningar.

### Exempel: Jag vill veta vad den genomsnittliga intäkten per order är när jag gör det och inte erbjuder en `promo code`.

![Använda formler för att hitta den genomsnittliga intäkten per order med och utan kampanjkoder](../../assets/promo_code.gif)

I det här exemplet använde du `Revenue` och `Number of orders` mätvärden. Svaret på den här frågan är två steg - dela upp `Revenue (A)` av `Number of orders (B)` och ange returformatet till `Currency`. Sedan tillät du endast formelresultatet (`Avg. Revenue per order`) för att visa och gruppera resultaten efter `Promo code`.

### Exempel: Jag vill veta hur mina nya kunders UTM-källor distribueras.

![Använda formler för att hitta distributionen av nya kunders UTM-källor](../../assets/distro.gif)

Att hitta svaret på den här frågan innehåller några steg:

1. Först lade du till `New Customers` och sedan grupperas efter `utm_source - all`. Detta är ett mått `A`, eller `New Customers (grouped)`.

1. Sedan duplicerade du `New Customers (grouped)` mätvärden och ange att de ska använda en oberoende dimension. Mått `B` - `New customers (ungrouped)` - visar det totala antalet nya kunder.

1. När du har dolt båda måtten anger du formeldefinitionen till `A/B`. Detta delar upp `New customers (grouped)` av `New Customers (ungrouped)`.

1. Sedan anger du resultatformatet till `Percent`.

I det här exemplet använde du `Stacked Columns` för att visa resultaten per månad. På så sätt kan vi jämföra distributionen av nya kunder månadsvis.

## Radbrytning {#wrapup}

Observera i exemplen ovan att formeln `timestamp`, `groupings`, `perspectives`och `filters` ärvs från indatavärden? Kom ihåg att formler kan användas `perspectives` och [oberoende tidsalternativ](../../tutorials/time-options-visual-rpt-bldr.md){: target=&quot;_blank&quot;}, precis som mätvärden kan.

Om du har ytterligare frågor om hur du använder formler i `Report Builder`, [kontakta support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
