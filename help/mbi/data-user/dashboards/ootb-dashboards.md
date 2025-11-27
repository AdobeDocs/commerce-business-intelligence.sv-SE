---
title: Inkluderade instrumentpaneler
description: Lär dig hur du kontrollerar hälsan hos viktiga mätvärden som intäkter från användarlivstid, antal upprepade köp med mera, och därmed skapar en stabil grund för framtida utforskande.
exl-id: f50fc417-e5d4-401c-9baa-cda1468196a2
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 3a7423c9dd0f957b77baa27b3447a715caad017b
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 0%

---

# Inkluderade instrumentpaneler

[!DNL Adobe] erbjuder `eCommerce`- och `SaaS` startpaket. Dessa paket, som skapats av Adobe analytiker, innehåller en anpassad uppsättning instrumentpaneler och rapporter för din datamängd. Analyserna i dessa paket gör det möjligt att kontrollera hälsan hos viktiga mätvärden som användarlivstidsintäkter, antal upprepade köp med mera, vilket skapar en stabil grund för framtida utforskande.

>[!NOTE]
>
>Tillgängligheten för vissa instrumentpaneler beror på din datamängd.

Om du har frågor eller vill lägga till ett paket till ditt konto skickar du en [supportanmälan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) för hjälp.

## Översikt

Kontrollpanelen `executive overview` har skapats från diagram som finns på andra instrumentpaneler. Den här instrumentpanelen är en översikt på hög nivå över dina data och innehåller diagram som skulle granskas dagligen, medan andra instrumentpaneler innehöll mer detaljerad information. Till att börja med anges den som standardinstrumentpanel för varje konto.

En allmän uppsättning diagram ingår. Adobe rekommenderar att du anpassar den här instrumentpanelen efter dina behov genom att lägga till andra diagram som du använder mest.

## Kohortanalys

Kontrollpanelen `cohort analysis` innehåller en uppsättning diagram som visar den genomsnittliga intäktsökningen för användarlivstid och ökningen av inkrementella intäkter grupperade efter registreringskohorter. Detta visar om kundens livstidsvärde, kundens värde för ett företag, ökar med tiden och även identifierar trender kring LTV-tillväxten. Som standard räknas *alla registrerade användare (köpare och icke-köpare)* i den genomsnittliga LTV-beräkningen - se [kohortanalysavsnittet](../../data-analyst/dev-reports/cohort-rpt-bldr.md).

Kontrollpanelen kan även innehålla kohortdiagram som analyserar användarnas livstidsintäkter från en viss förvärvskälla, kanal eller demografi (t.ex. New York eller Kalifornien). Detta är för att visa hur du kan analysera LTV för specifika segment i din användarbas och se om en grupp eller en annan ger högre LTV över tiden.

Mer information om kohorter finns i [Utför kohortanalys](../../data-analyst/dev-reports/cohort-rpt-bldr.md).

Om du för närvarande inte spårar källan för användarvärvning läser du [Spåra användarvärvning (Source Data Overview)](../../data-analyst/analysis/google-track-user-acq.md).

## E-postsammanfattning

Instrumentpanelen `Email Summary` innehåller en exempeluppsättning diagram som kan användas i en automatisk e-postsammanfattning varje dag. Mer information om hur du konfigurerar e-postsammanfattningar finns i [skapa automatiska e-postsammanfattningar](../../data-user/export-data/email-summaries.md).  

## Bevarandehälsa

Instrumentpanelen `Retention health` visar hur din användarbas upprepade inköpsbeteenden fungerar.

Diagrammet `Time between orders` visar den genomsnittliga och/eller genomsnittliga tiden mellan en användares första och andra ordning, andra och tredje ordning och så vidare. Du kan överväga att använda dessa data för att konfigurera e-postmarknadsföringskampanjer.

Diagrammet `Users by lifetime number of orders` visar det totala antalet användare för varje antal order under en livstid för att ge en allmän översikt över beteendet vid upprepade inköp.  

Diagrammet `Repeat order probability` visar sannolikheten för att en användare med ett visst ordernummer gör ett återkommande köp. Om du vill se sannolikheten för att kunder som har gjort `x` beställningar ska göra `(x+1)` beställningar, behöver du bara dividera antalet personer som har gjort minst `(x+1)` inköp med antalet personer som har gjort minst `x` inköp.

### Exempel

Antal kunder som har gjort ett köp under sin livstid: `90`

Antal kunder som har gjort två köp under sin livstid: `30`

Antal kunder som har gjort tre köp under sin livstid: `10`

I det här exemplet är sannolikheten för upprepade order för kunder som har gjort ett köp under sin livstid för att göra ett andra köp: `(30 + 10) / (30+10+90) = 30.77%`.

## LTV-tillväxt för kunder

Kontrollpanelen `Customer LTV growth` innehåller en uppsättning diagram som identifierar den genomsnittliga intäkten per användare. Diagrammen segmenteras utifrån den genomsnittliga intäkten som genereras inom de första 30, 60, 90 eller 365 dagarna efter registreringen.  

Diagrammets nedre rad visar att dessa medelvärden segmenteras av anskaffningskällor eller demografiska data för att visa vilka grupper av användare som genererar mest intäkter över tid.

## Produktprestanda

Kontrollpanelen `Product Performance` innehåller diagram som visar allmänna produktprestanda genom att visa antalet sålda artiklar och intäkter per artikel och identifiera produkter som presterar bäst.

## Senaste aktivitet

Kontrollpanelen `Recent Activity` visar prestandadata för de senaste 30 dagarna.

## Transaktionshälsa

Kontrollpanelen `Transaction Health` innehåller översiktsdiagram över intäkter, order och genomsnittligt ordervärde. Dessa diagram kan segmenteras av marknadsföringskanaler, demografi eller särskilda kupongkoder.

## Användare att rikta

Kontrollpanelen `Users to target` innehåller tabellformatsdiagram som listar användare med gemensamma inköpsbeteenden. Några exempel:

* Lista över engångsköpare som köpte för `X` månader sedan (som du kanske vill återaktivera)

* Lista över de bästa stavningarna (som du kanske vill behålla lyckliga)

* Lista över de största skulder som varit aktiva de senaste `X` dagarna (som du kanske vill belöna)

Du kan använda dina dataexportverktyg för att skapa e-postlistor med användare med liknande inköpsbeteenden för målmarknadsföring.

## Användaraktivitet

Kontrollpanelen `User activity` innehåller diagram som segmenterar användare efter olika data, inklusive inhämtningskälla, demografiska data och genomsnittlig första beställningstid. Det innehåller även en analys av användarkohorten, inklusive den totala genomsnittliga intäkten för livstid per användarregistreringsmånad.

Diagrammet `% of cohort members who have purchased` är värdefullt eftersom det visar konverteringsgraden (från 0 till 1) för användare baserat på när de registrerar sig (varje rad representerar en kohort med användare). Det visas också när de gör sitt första köp (till exempel i månad 1, 2, 3... efter registreringen). Detta kan visa att 10 % av användarna aktiverade under månad 1, medan antalet växer under månad 2, 3, 4.. och kan komma att platåa senare.

Raderna i det här diagrammet blir vanligtvis vågräta efter en viss tidsperiod. Detta visar att få ytterligare kohortmedlemmar konverterar organiskt efter den punkten - de flesta användare som kommer att göra ett köp har redan gjort det. I nuläget är det högst osannolikt att dessa medlemmar kommer att konvertera till köpare utan ingripande. Att nå ut till dem med anpassade kampanjer eller riktade e-postmeddelanden är ett lågrisksätt att snabbt komma igång med konverteringen av den här befolkningen.
