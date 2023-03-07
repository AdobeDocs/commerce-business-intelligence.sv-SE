---
title: Genomsnittlig tid för första inköpsrapport
description: Lär dig hur du använder rapporten för genomsnittlig tid för första inköp.
exl-id: c18734ce-0ae0-4e84-b9d0-eb2c21a5c3a5
source-git-commit: 8de036e2717aedef95a8bb908898fd9b9bc9c3fa
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# Genomsnittlig tid för första inköpsrapport

Många Adobe-kunder har ett mätvärde och diagram `Average time to first purchase`, som visar den genomsnittliga tiden mellan en grupp användares registreringsdatum och första inköpsdatum. Data blir nästan alltid långsammare när tiden närmar sig dagens läge.

![genomsnittlig tid för första ordern](../../assets/average-time-to-first-order.png)

Detta beror på att dessa nyare kunder ännu inte har haft möjlighet att generera några inköp som gjorts mer än en månad efter deras anslutningsdatum. Eftersom användare som aldrig har gjort ett köp inte alls ingår (förrän de har gjort ett köp), innebär detta en minskning av den genomsnittliga prisnivån för nyare kundgrupper.

Det finns några andra möjliga sätt att se på detta mätresultat som ger mindre förtjänster. Utforska ett exempel.

## Exempel: Utför en `cohort` analys av första order

Du kanske har ett diagram på din `Users` instrumentpanel namngiven `Time to first order cohort`. Den här rapporten använder `Distinct buyers` mått, grupperar användare efter `cohort` veckor eller månader av registreringen och visar förhållandet (mellan `0` och `1`) av användare som gjorde ett första köp de följande veckorna eller månaderna efter registreringen.

Diagrammet kan visa att för användare som registrerade i december 2014 `0.56` (eller `56%`) gjorde en första beställning per månad 2 (till exempel januari 2015).

Denna kohortanalys är en bra indikator på användaraktiveringshastigheten över tid. Om det här diagrammet börjar platåa eller läggas samman, och du fortfarande inte konverterar till nästan 100 % till köpare, kan det vara dags att aktivera de återstående användarna via e-postkampanjer.
