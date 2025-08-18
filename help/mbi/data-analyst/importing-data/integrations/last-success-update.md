---
title: Förstå resultat mellan databas och SQL Editor
description: Lär dig mer om resultatet mellan databas- och SQL-redigerare.
exl-id: f31f3eef-791a-4984-901e-bc10554031bd
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---

# Databasresultat jämfört med [!DNL SQL Editor] resultat

Du kanske är nyfiken på vad fältet `Last successful update began` innehåller på din `Integrations`-sida:

![Last_success_update.png](../../../assets/Last_successful_update.png)

## Förstå fältet `timestamp`

Den visar start `timestamp` (i tidszonen som angetts för ditt konto) för den _senaste lyckade uppdateringscykeln_ för ditt konto.

- Om någon av de synkroniserade tabellerna stötte på ett problem under den senaste uppdateringscykeln är den här tidsstämpeln *inte uppdaterad*.
- Det kan därför finnas fall där rapporter har uppdaterats med nya data, men den *senaste lyckade uppdateringen som påbörjades* släpar fortfarande efter.

## Identifiera den&quot;riktiga&quot; sista datapunkten

Den senaste datapunkten för en viss integrering bestäms av tidsstämpeln `Last Data Point Received` till höger om varje integrering. Tidsstämpeln avser den sista punkten där Data Warehouse tog emot datapunkter från den källan, oavsett om det är en databas, ett API eller en tredjepartsintegrering.

Adobe rekommenderar att du skapar en snabb *rapport* som utför en [[!DNL SQL]  på den viktigaste tabellen på ditt konto för att kontrollera om data är aktuella i ](../../dev-reports/sql-rpt-bldr.md)specifika tabeller`MAX(timestamp)`. En jämförelse av den här tidsstämpeln med `Last Data Point` visar om problemet påverkade hela kontot eller en delmängd av tabellerna. Adobe rekommenderar att du gör detta i tre till fyra viktiga, ofta använda tabeller.

- Om `MAX(timestamp)`-värdena är senare än `Last Data Point Received` innebär det att en delmängd av tabellerna påverkades, men det övergripande kontots uppdateringscykel är stabil.
- Om värdena `MAX(timestamp)` är lika med eller före `Last Data Point Received` betyder det att kontots uppdateringscykel påverkades. I den här situationen [skickar du en supportanmälan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=sv-SE).
