---
title: Minska tiden för uppdateringscykeln
description: Lär dig hur du minskar tiden för uppdateringscykeln.
exl-id: 0b211e2d-770f-480d-a7fb-8d10e3e7272e
role: Admin, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---

# Minska behandlingstiden för uppdateringscykler

[!DNL Adobe Commerce Intelligence] synkroniseras med din databas under dagen för att replikera nya data, så att du ser till att den senaste informationen alltid visas på instrumentpanelerna.

Många faktorer kan öka uppdateringstiden med redan lång tid. Vissa replikeringsmetoder, högre kontrollfrekvenser och antalet kontrollpaneler och diagram är bara några få deltagare. I det här avsnittet beskrivs några tips om hur du kan minska uppdateringstiderna.

## Minska frekvensen för ny kontroll

I en databastabell kan det finnas datakolumner med ändringsbara värden. I en **order**-tabell kan det till exempel finnas en kolumn med namnet **status**. När en order skrivs till databasen från början kan statuskolumnen innehålla värdet `pending`. Ordningen replikeras i din [Data Warehouse](../data-analyst/data-warehouse-mgr/tour-dwm.md) med det här `pending`-värdet.

Ändringsbara kolumner måste [omkontrolleras för uppdaterade värden](../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) över tiden. Som standard kontrollerar [!DNL Commerce Intelligence] om de här kolumnerna under varje uppdatering, men om det finns en stor mängd data som ska kontrolleras och replikeras kan det påverka uppdateringstiden negativt. I stället för att köra omkontroller under varje uppdatering rekommenderar Adobe att du ställer in frekvensen för omkontroll till varje dag, vecka eller månad.

## Använd inkrementella replikeringsmetoder

Som nämnts ovan står långa uppdateringstider direkt i relation till hur mycket data som måste kontrolleras och replikeras. [Inkrementella replikeringsmetoder](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md) kan avsevärt minska mängden data som bearbetas under uppdateringscykeln. Om det är möjligt rekommenderar Adobe att du använder dessa metoder eller ändrar databasen så att den stöder en stegvis metod.

## Ta bort oanvända diagram från instrumentpaneler

I slutet av uppdateringscykeln utför [!DNL Commerce Intelligence] en cacheåtgärd för alla diagram. I ett cacheminne lagras data så att framtida informationsförfrågningar kan slutföras snabbare. I [!DNL Commerce Intelligence] innebär det att instrumentpaneler läses in snabbt eftersom diagram inte behöver fråga efter data varje gång de läses in.

Eftersom [!DNL Commerce Intelligence] bara utför cacheåtgärder för diagram som hittas i en instrumentpanel, minskar uppdateringstiden om du tar bort oanvända diagram från instrumentpanelerna. Kom ihåg att samma diagram kan finnas på flera kontrollpaneler - kontakta teamet för att kontrollera att även oanvända diagram har tagits bort.

>[!NOTE]
>
>Diagrammet tas inte bort när du tar bort diagram från kontrollpanelen. Du kan [lägga till den igen när som helst](../data-user/dashboards/add-charts-dashboard.md).

## Optimera databasen för analys

Förutom att utvärdera omkontrollfrekvenser, replikeringsmetoder och diagramanvändning kan du även [optimera databasen för analys](../best-practices/opt-db-analysis.md).

## Radbrytning

Om din uppdateringstid fortfarande verkar långsam även efter att du har implementerat dessa rekommendationer, [kontaktar du supportteamet](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
