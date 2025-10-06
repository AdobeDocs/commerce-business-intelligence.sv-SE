---
title: Formler i Report Builder
description: Lär dig hur formler kan användas i Report Builder.
exl-id: 7a0ad07a-5bcc-474f-95bc-ccc2b74073b2
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 0%

---

# Formler i `Report Builder`

I [`Report Builder`](../../tutorials/using-visual-report-builder.md) kan du skapa kraftfulla visualiseringar med [definierade mått](../../data-user/reports/ess-manage-data-metrics.md) i ditt konto. Genom att kombinera dessa mätvärden i en formel kan ni få ytterligare insikter från era data. I det här avsnittet går vi igenom hur formler kan användas i `Report Builder` - så att du kan hoppa in!

## Vad är en `formula`? {#what}

I `Report Builder` är en `formula` bara en kombination av ett eller flera mått baserat på någon matematisk logik. Ett typiskt exempel ser ut så här:

![Formelexempel som visar beräkning i Report Builder](../../assets/formula-example.png)

I det här exemplet använder du en `Number of orders metric (A)` och en `Distinct buyers metric (B)`, och målet är att svara på frågan: vilket är det genomsnittliga antalet order som mina köpare gör varje månad? Formelns parametrar är:

* `Definition`: Här använder du matematik på indatavärden. I det här exemplet, där antalet order divideras med antalet distinkta köpare, anger vi det genomsnittliga antalet order. Definitionen är därför (A/B).

* `Format`: Returnerar din formel ett tal, en tidsperiod eller ett valutabelopp? Bredvid formelns definition finns en listruta som du kan använda för att ange returens format. I det här fallet är det ett tal.

* `Miscellaneous`: Formelns tidsstämpel, grupperingar, perspektiv och filter ärvs alla av dess indatavärden. Det finns ingenting att göra här!

## Hur kan jag använda `formulas` i mina rapporter? {#how}

Nu när du har gått igenom grunderna kan du titta på några exempel.

### Exempel: Jag vill ta reda på vilken procentandel av min intäkt som kan tillskrivas förstagångsbeställningar.

![Använder formler för att hitta procentandelen av intäkt som härrör från förstagångsorder](../../assets/first_time_orders.gif)

I det här exemplet har du använt måtten `Revenue` och `Revenue (first time orders)`. Genom att dividera `Revenue (first time orders)(B)`-måttet med `Revenue metric (A)` och ange returformatet till `Percent`, kan du hitta procentandelen intäkter som kan tilldelas förstagångsorder.

### Exempel: Jag vill veta vilken den genomsnittliga intäkten per order är när jag gör och inte erbjuder en `promo code`.

![Använda formler för att hitta genomsnittsinkomsten per order med och utan kampanjkoder](../../assets/promo_code.gif)

I det här exemplet har du använt måtten `Revenue` och `Number of orders`. Svaret på den här frågan består av två steg - dela `Revenue (A)` med `Number of orders (B)` och ange returformatet till `Currency`. Därefter tillät du endast formelresultatet (`Avg. Revenue per order`) att visa och gruppera resultaten efter `Promo code`.

### Exempel: Jag vill veta hur mina nya kunders UTM-källor distribueras.

![Använder formler för att hitta distributionen av nya kunders UTM-källor](../../assets/distro.gif)

Att hitta svaret på den här frågan innehåller några steg:

1. Först lade du till måttet `New Customers` och sedan grupperade efter `utm_source - all`. Det här är måttet `A`, eller `New Customers (grouped)`.

1. Därefter duplicerade du måttet `New Customers (grouped)` och ställde in det till att använda en oberoende dimension. Mått `B` - `New customers (ungrouped)` - visar totalt antal nya kunder.

1. När du har dolt båda måtten anger du formeldefinitionen till `A/B`. Detta delar `New customers (grouped)` med `New Customers (ungrouped)`.

1. Sedan anger du resultatformatet till `Percent`.

I det här exemplet använde du perspektivet `Stacked Columns` för att visa resultaten per månad. På så sätt kan vi jämföra distributionen av nya kunder månadsvis.

## Radbrytning {#wrapup}

Märkte du i exemplen ovan att formelns `timestamp`, `groupings`, `perspectives` och `filters` ärvs från indatamätningarna? Kom ihåg att formler kan användas för att använda `perspectives` och [oberoende tidsalternativ](../../tutorials/time-options-visual-rpt-bldr.md){: target="_blank"}, precis som mätvärden kan.

`Report Builder`Kontakta support[ om du har ytterligare frågor om hur du använder formler i ](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
