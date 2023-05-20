---
title: Genomsnittlig tid för första köprapport
description: Lär dig hur du använder rapporten Genomsnittlig tid för första köp.
exl-id: c18734ce-0ae0-4e84-b9d0-eb2c21a5c3a5
source-git-commit: 8de036e2717aedef95a8bb908898fd9b9bc9c3fa
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# Genomsnittlig tid för första köprapport

Många Adobe-kunder har ett mått och en tabell med namnet `Average time to first purchase`, som visar den genomsnittliga tiden mellan en grupp användares registreringsdatum och första inköpsdatum. Data lutar nästan alltid nedåt när tiden närmar sig nutiden.

![genomsnittlig tid till första beställning](../../assets/average-time-to-first-order.png)

Detta beror på att dessa nyare kunder ännu inte har haft möjlighet att generera några inköp som gjorts mer än en månad från deras anslutningsdatum. Eftersom användare som aldrig har gjort ett köp inte ingår alls (tills de gör ett köp), detta snedvrider genomsnittet nedåt för nyare grupper av kunder.

Det finns några andra möjliga sätt att se på detta mätresultat som ger mindre partiskhet. Utforska ett exempel.

## Exempel: Utför en `cohort` analys av första beställningar

Du kan ha ett diagram på `Users` instrumentpanelen har namnet `Time to first order cohort`. I rapporten används `Distinct buyers` mått, grupperar användare efter `cohort` och visar förhållandet (mellan `0` och `1`) för användare som gjorde ett första köp inom de följande veckorna eller månaderna efter registreringen.

Tabellen kan visa att för användare som registrerade i december 2014, `0.56` (eller `56%`) gjorde en första beställning efter månad 2 (till exempel januari 2015).

Denna kohortanalys är en bra indikator på användaraktiveringsgraden över tid. Om diagrammet börjar platta ut eller plana ut, och du fortfarande inte är nära 100% konvertering till köpare, kan det vara dags att aktivera de återstående användarna via e-postkampanjer.
