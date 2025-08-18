---
title: Information om data och uppdateringar
description: Lär dig hur du kontrollerar status för uppdateringscykeln.
exl-id: a4a2e487-b826-4888-baf0-9d246a8ff153
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# Information om data och uppdateringar

* [Varför ändrades mina data?](#datachange)
* [Vad är skillnaden mellan en vanlig och tvingad uppdatering?](#regularforcedupdates)
* [Varför tar uppdateringscykeln lång tid?](#updatecycletime)
* [Kan jag få ett meddelande när en uppdateringscykel har slutförts?](#notifyupdate)
* [Varför skiljer sig  [!DNL Google ECommerce] data från min databas?](#ecommdatabase)
* [Hur felsöker jag en diskrepans?](#datadiscrepancy)

## Varför ändrades mina data? {#datachange}

Diagramvärdena kan ändras under dagen på grund av att nya data synkroniseras med din Data Warehouse. Dessutom kan värden för befintliga datakolumner ändras på grund av [omkontroller](../data-warehouse-mgr/cfg-data-rechecks.md). En omkontroll är en process som söker efter ändrade värden i datakolumner, till exempel en orderstatus som flyttas från `open` till `shipped`.

Det finns några olika sätt [att kontrollera statusen för din uppdateringscykel](../../best-practices/check-update-cycle.md), beroende på användarens behörighetsinställningar.

## Vad är skillnaden mellan en vanlig och tvingad uppdatering? {#regularforcedupdates}

Regelbundna uppdateringar är **schemalagda** processer medan framtvingade uppdateringar är **manuella processer som initierats av dig**. Om du har öppethållande timmar (eller en tidsperiod där [!DNL Commerce Intelligence] inte ska uppdatera dina data) startar en uppdatering som inte uppfyller begränsningarna för den utbrottsperioden.

## Varför tar uppdateringscykeln lång tid? {#updatecycletime}

Många faktorer kan öka uppdateringstiden. Vissa [replikeringsmetoder](../data-warehouse-mgr/cfg-replication-methods.md), [högre kontrollfrekvenser](../data-warehouse-mgr/cfg-data-rechecks.md) och antalet instrumentpaneler och diagram är bara några få medverkande. Adobe rekommenderar att [vissa av dina inställningar ](../../best-practices/reduce-update-cycle-time.md) konfigureras om och [att databasen optimeras för analys](../../best-practices/opt-db-analysis.md) för att minska uppdateringstiden.

## Kan jag få ett meddelande när en uppdateringscykel har slutförts? {#notifyupdate}

Om en uppdatering pågår finns det en länk på sidan `Connections` som du kan använda för att begära ett e-postmeddelande när cykeln har slutförts.

## Varför skiljer sig [!DNL Google ECommerce]data från min databas? {#ecommdatabase}

Skillnader mellan [!DNL Google Analytics] och databasen kan uppstå av olika orsaker. Spårning är inte korrekt aktiverat, användare som besöker incognito och klickningshändelser fungerar inte korrekt är bara några exempel. Om dina intäkter och beställningar inte ser bra ut kan du [läsa det här avsnittet](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html?lang=sv-SE) och diagnostisera ett problem.

## Hur felsöker jag en diskrepans? {#datadiscrepancy}

Adobe vet att inkonsekventa data kan vara en frustrerande upplevelse. Använd [checklistan för dataskvalitet](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-a-data-discrepancy.html?lang=sv-SE) eller [självstudiekursen för dataexport](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html?lang=sv-SE) för att diagnostisera problemet. [Kontakta support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=sv-SE) om du fortfarande stöter på problem.
