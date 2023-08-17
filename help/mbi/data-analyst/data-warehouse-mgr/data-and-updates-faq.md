---
title: Information om data och uppdateringar
description: Lär dig hur du kontrollerar status för uppdateringscykeln.
exl-id: a4a2e487-b826-4888-baf0-9d246a8ff153
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 0%

---

# Information om data och uppdateringar

* [Varför ändrades mina data?](#datachange)
* [Vad är skillnaden mellan en vanlig och tvingad uppdatering?](#regularforcedupdates)
* [Varför tar uppdateringscykeln lång tid?](#updatecycletime)
* [Kan jag få ett meddelande när en uppdateringscykel har slutförts?](#notifyupdate)
* [Varför [!DNL Google ECommerce] data som skiljer sig från min databas?](#ecommdatabase)
* [Hur felsöker jag en diskrepans?](#datadiscrepancy)

## Varför ändrades mina data? {#datachange}

Diagramvärdena kan ändras under dagen på grund av att nya data synkroniseras med Datan Warehouse. Dessutom kan värden för befintliga datakolumner ändras på grund av [omkontroller](../data-warehouse-mgr/cfg-data-rechecks.md). En omkontroll är en process som söker efter ändrade värden i datakolumner, till exempel en orderstatus som flyttas från `open` till `shipped`.

Det finns några olika sätt [för att kontrollera uppdateringscykelns status](../../best-practices/check-update-cycle.md), beroende på användarens behörighetsinställningar.

## Vad är skillnaden mellan en vanlig och tvingad uppdatering? {#regularforcedupdates}

Vanliga uppdateringar är **schemalagd** processer medan framtvingade uppdateringar **manuella processer som du har initierat**. Om du har mörkt ned timmar (eller en tidsperiod där [!DNL Commerce Intelligence] bör inte uppdatera dina data), så tvingar en uppdatering att starta en cykel som inte respekterar begränsningarna för den utmattade perioden.

## Varför tar uppdateringscykeln lång tid? {#updatecycletime}

Många faktorer kan öka uppdateringstiden. Vissa [replikeringsmetoder](../data-warehouse-mgr/cfg-replication-methods.md), [högre omkontrollfrekvenser](../data-warehouse-mgr/cfg-data-rechecks.md)och antalet paneler och diagram är bara några få deltagare. Adobe rekommenderar [konfigurera om vissa inställningar](../../best-practices/reduce-update-cycle-time.md) och [optimera databasen för analys](../../best-practices/opt-db-analysis.md) för att minska uppdateringstiden.

## Kan jag få ett meddelande när en uppdateringscykel har slutförts? {#notifyupdate}

Om en uppdatering pågår finns det en länk på `Connections` sida som du kan använda för att begära ett e-postmeddelande när cykeln är slutförd.

## Varför[!DNL Google ECommerce]data som skiljer sig från min databas? {#ecommdatabase}

Avvikelser mellan [!DNL Google Analytics] och databasen kan uppstå av olika anledningar. Spårning är inte korrekt aktiverat, användare som besöker incognito och klickningshändelser fungerar inte korrekt är bara några exempel. Om era intäkter och beställningar inte ser bra ut, [se det här avsnittet](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html) för att diagnostisera ett problem.

## Hur felsöker jag en diskrepans? {#datadiscrepancy}

Adobe vet att inkonsekventa data kan vara en frustrerande upplevelse. Prova att använda [Checklista för dataavvikelse](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-a-data-discrepancy.html) eller [Självstudiekurs om dataexport](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html) för att diagnostisera problemet. Om du fortfarande stöter, [kontakta support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
