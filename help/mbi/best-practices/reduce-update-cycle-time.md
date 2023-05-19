---
title: Minska tiden för uppdatering
description: Lär dig hur du minskar tiden för uppdateringscykeln.
exl-id: 0b211e2d-770f-480d-a7fb-8d10e3e7272e
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# Minska behandlingstiden för uppdateringscykler

[!DNL Adobe Commerce Intelligence] synkroniserar med databasen hela dagen för att replikera nya data, så att du alltid ser den senaste informationen på kontrollpanelerna.

Många faktorer kan öka uppdateringstiden med redan lång tid. Vissa replikeringsmetoder, högre kontrollfrekvenser och antalet kontrollpaneler och diagram är bara några få deltagare. I det här avsnittet diskuteras några bästa metoder för att minska uppdateringstiderna.

## Minska kontrollfrekvens

I en databastabell kan det finnas datakolumner med ändringsbara värden. I en **order** tabellen kan innehålla en kolumn som kallas **status**. När en order skrivs till databasen från början kan statuskolumnen innehålla värdet `pending`. Ordningen replikeras i [data warehouse](../data-analyst/data-warehouse-mgr/tour-dwm.md) med `pending` värde.

Ändringsbara kolumner måste vara [ommarkerad för uppdaterade värden](../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) över tid. Som standard [!DNL Commerce Intelligence] kontrollerar om de här kolumnerna under varje uppdatering, men om det finns en stor mängd data som ska kontrolleras och replikeras kan det påverka uppdateringstiden negativt. I stället för att köra omkontroller under varje uppdatering rekommenderar Adobe att du ställer in frekvensen för omkontroll till varje dag, vecka eller månad.

## Använd inkrementella replikeringsmetoder

Som nämnts ovan står långa uppdateringstider direkt i relation till hur mycket data som måste kontrolleras och replikeras. [Stegvisa replikeringsmetoder](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md) kan avsevärt minska mängden data som behandlas under uppdateringscykeln. Om det är möjligt rekommenderar Adobe att du använder dessa metoder eller ändrar databasen så att den stöder en stegvis metod.

## Ta bort oanvända diagram från instrumentpaneler

I slutet av uppdateringscykeln [!DNL Commerce Intelligence] utför en cacheåtgärd för alla diagram. I ett cacheminne lagras data så att framtida informationsförfrågningar kan slutföras snabbare. I [!DNL Commerce Intelligence]innebär det att kontrollpanelerna läses in snabbt eftersom diagram inte behöver fråga efter data varje gång de läses in.

Sedan [!DNL Commerce Intelligence] utför bara cacheåtgärder för diagram som hittas på en kontrollpanel. Om du tar bort oanvända diagram från kontrollpanelerna tar du bort uppdateringstiden. Kom ihåg att samma diagram kan finnas på flera kontrollpaneler - kontakta teamet för att kontrollera att även oanvända diagram har tagits bort.

>[!NOTE]
>
>Diagrammet tas inte bort när du tar bort diagram från kontrollpanelen. Du kan [lägg till det igen när som helst](../data-user/dashboards/add-charts-dashboard.md).

## Optimera databasen för analys

Förutom att omvärdera kontrollfrekvenser, replikeringsmetoder och diagramanvändning kan du även [optimera databasen för analys](../best-practices/opt-db-analysis.md).

## Radbrytning

Om uppdateringstiden fortfarande verkar långsam även efter att du har implementerat dessa rekommendationer, [kontakta supportteamet](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
