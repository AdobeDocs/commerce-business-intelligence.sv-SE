---
title: Förstå resultat mellan databas och SQL Editor
description: Lär dig mer om resultatet mellan databas- och SQL-redigerare.
exl-id: f31f3eef-791a-4984-901e-bc10554031bd
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---

# Databasresultat jämfört med [!DNL SQL Editor] Resultat

Du kanske är nyfiken på vad `Last successful update began` fältet finns inuti `Integrations` sida:

![Last_success_update.png](../../../assets/Last_successful_update.png)

## Förstå `timestamp` fält

Det visar början `timestamp` (i den tidszon som har angetts för ditt konto) för _senaste lyckade uppdateringscykel_ på ditt konto.

- Om någon av de synkroniserade tabellerna stötte på ett problem under den senaste uppdateringscykeln är tidsstämpeln *inte uppdaterad*.
- Det kan därför finnas fall där rapporter har uppdaterats med nya data, men *Senaste lyckade uppdatering* släpar fortfarande efter.

## Identifiera den&quot;riktiga&quot; sista datapunkten

Den senaste datapunkten för en viss integrering bestäms av `Last Data Point Received` tidsstämpel till höger om varje integrering. Tidsstämpeln avser den sista punkten där Datan Warehouse tog emot datapunkter från den källan, oavsett om det är en databas, ett API eller en tredjepartsintegrering.

För att kontrollera om data är aktuella från *specifika tabeller* rekommenderar Adobe att du skapar en snabbmeny [[!DNL SQL] rapport](../../dev-reports/sql-rpt-bldr.md) som utför en `MAX(timestamp)` på den viktigaste tabellen på ditt konto. Jämför den här tidsstämpeln med `Last Data Point` anger om utgåvan påverkade hela kontot eller en delmängd av tabellerna. Adobe rekommenderar att du gör detta i tre till fyra viktiga, ofta använda tabeller.

- Om `MAX(timestamp)` värden är senare än `Last Data Point Received`innebär det att en delmängd av tabellerna påverkades, men kontots uppdateringscykel är stabil.
- Om `MAX(timestamp)` värdena är lika med eller före `Last Data Point Received`innebär det att kontots uppdateringscykel påverkades. I denna situation [skicka en supportanmälan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
