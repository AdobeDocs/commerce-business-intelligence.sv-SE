---
title: Genomsnittlig tid för första inköpsrapport
description: Lär dig hur du använder rapporten för genomsnittlig tid för första inköp.
exl-id: c18734ce-0ae0-4e84-b9d0-eb2c21a5c3a5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 330832e2668024b00edb2b7c49b92bb042bd004a
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# Genomsnittlig tid för första inköpsrapport

Många Adobe-kunder har ett mätvärde och diagram med namnet `Average time to first purchase`, som visar den genomsnittliga tiden mellan en grupps registreringsdatum och första inköpsdatum. Data blir nästan alltid långsammare när tiden närmar sig dagens läge.

![genomsnittlig tid till första beställningen](../../assets/average-time-to-first-order.png)

Detta beror på att dessa nyare kunder ännu inte har haft möjlighet att generera några inköp som gjorts mer än en månad efter deras anslutningsdatum. Eftersom användare som aldrig har gjort ett köp inte alls ingår (förrän de har gjort ett köp), innebär detta en minskning av den genomsnittliga prisnivån för nyare kundgrupper.

Det finns några andra möjliga sätt att se på detta mätresultat som ger mindre förtjänster. Se ett exempel.

## Exempel: Utför en `cohort`-analys av första order

Det kan finnas ett diagram på din `Users`-instrumentpanel med namnet `Time to first order cohort`. Den här rapporten använder måttet `Distinct buyers`, grupperar användare efter `cohort` veckors eller månaders registrering och visar förhållandet (mellan `0` och `1`) för användare som gjorde ett första köp de följande veckorna eller månaderna efter registreringen.

Diagrammet kan visa att för användare som registrerade i december 2014 gjorde `0.56` (eller `56%`) en första beställning per månad 2 (till exempel januari 2015).

Denna kohortanalys är en bra indikator på användaraktiveringshastigheten över tid. Om det här diagrammet börjar platåa eller läggas samman, och du fortfarande inte konverterar till nästan 100 % till köpare, kan det vara dags att aktivera de återstående användarna via e-postkampanjer.
