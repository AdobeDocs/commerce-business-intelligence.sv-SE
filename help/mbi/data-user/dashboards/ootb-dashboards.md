---
title: Inkluderade instrumentpaneler
description: Lär dig hur du kontrollerar hälsan hos viktiga mätvärden som intäkter från användarlivstid, antal upprepade köp med mera, och därmed skapar en stabil grund för framtida utforskande.
exl-id: f50fc417-e5d4-401c-9baa-cda1468196a2
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '958'
ht-degree: 0%

---

# Inkluderade instrumentpaneler

[!DNL Adobe] erbjudanden `eCommerce` och `SaaS` Startpaket. Dessa paket, som skapats av analytiker från Adobe, innehåller en anpassad uppsättning instrumentpaneler och rapporter för din datamängd. Analyserna i dessa paket gör det möjligt att kontrollera hälsan hos viktiga mätvärden som användarlivstidsintäkter, antal upprepade köp med mera, vilket skapar en stabil grund för framtida utforskande.

>[!NOTE]
>
>Tillgängligheten för vissa instrumentpaneler beror på din datamängd.

Om du har frågor eller är intresserad av att lägga till ett paket i ditt konto, skicka ett [supportbiljett](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) om du behöver hjälp.

## Översikt

The `executive overview` Kontrollpanelen byggs från diagram som finns på andra instrumentpaneler. Den här instrumentpanelen är en översikt på hög nivå över dina data och innehåller diagram som skulle granskas dagligen, medan andra instrumentpaneler innehöll mer detaljerad information. Till att börja med anges den som standardinstrumentpanel för varje konto.

En allmän uppsättning diagram ingår. Adobe rekommenderar att du skräddarsyr den här instrumentpanelen efter dina behov genom att lägga till andra diagram som du använder mest.

## Kohortanalys

The `cohort analysis` Instrumentpanelen innehåller en uppsättning diagram som visar den genomsnittliga intäktsökningen under användarens livstid och ökningen av inkrementella intäkter grupperade efter registreringscohorts. Detta visar om kundens livstidsvärde, kundens värde för ett företag, ökar med tiden och även identifierar trender kring LTV-tillväxten. Som standard *alla registrerade användare (köpare och icke-köpare) redovisas* i den genomsnittliga LTV-beräkningen - se [cohort analysis topic](../../data-analyst/dev-reports/cohort-rpt-bldr.md).

Kontrollpanelen kan även innehålla kohortdiagram som analyserar användarnas livstidsintäkter från en viss förvärvskälla, kanal eller demografi (t.ex. New York eller Kalifornien). Detta är för att visa hur du kan analysera LTV för specifika segment i din användarbas och se om en grupp eller en annan ger högre LTV över tiden.

Mer information om kohorter finns i [Utför kohortanalys](../../data-analyst/dev-reports/cohort-rpt-bldr.md).

Om du för närvarande inte spårar källan för kundvärvning kan du läsa [Spåra översikt över källdata för användarförvärv](../../data-analyst/analysis/google-track-user-acq.md).

## E-postsammanfattning

The `Email Summary` Instrumentpanelen innehåller en exempeluppsättning diagram som kan användas i en automatisk daglig e-postsammanfattning. Se [skapa automatiska e-postsammanfattningar](../../data-user/export-data/email-summaries.md) om du vill ha mer information om hur du konfigurerar e-postsammanfattningar.  

## Bevarandehälsa

The `Retention health` på kontrollpanelen visas hur din användarbas gör om sina inköp.

The `Time between orders` diagram visar den genomsnittliga och/eller genomsnittliga tiden mellan en användares första och andra order, andra och tredje ordning osv. Du kan [överväga att använda dessa data för att konfigurera era e-postmarknadsföringskampanjer](http://blog.rjmetrics.com/acting-on-marketing-data-in-your-rjmetrics-online-dashboard/).

The `Users by lifetime number of orders` diagram visar det totala antalet användare för varje antal order under en livstid för att ge en allmän översikt över upprepade inköpsbeteenden.  

The `Repeat order probability` diagram visar sannolikheten för att en användare med ett visst ordernummer gör ett återkommande köp. Att se sannolikheten för kunder som gjorde `x` order att skapa `(x+1)` order, dividera bara antalet personer som har gjort minst `(x+1)` köp av det antal personer som har gjort minst `x` inköp.

### Exempel

Antal kunder som gjort ett köp under sin livstid: `90`

Antal kunder som gjort två inköp under sin livstid: `30`

Antal kunder som gjort tre inköp under sin livstid: `10`

I det här exemplet är sannolikheten för att kunder som har gjort ett köp under sin livstid ska göra ett andra köp följande: `(30 + 10) / (30+10+90) = 30.77%`.

## LTV-tillväxt för kunder

The `Customer LTV growth` Instrumentpanelen innehåller en uppsättning diagram som visar den genomsnittliga intäkten per användare. Diagrammen segmenteras utifrån den genomsnittliga intäkten som genereras inom de första 30, 60, 90 eller 365 dagarna efter registreringen.  

Diagrammets nedre rad visar att dessa medelvärden segmenteras av anskaffningskällor eller demografiska data för att visa vilka grupper av användare som genererar mest intäkter över tid.

## Produktprestanda

The `Product Performance` Instrumentpanelen innehåller diagram som visar allmänna produktprestanda genom att visa antalet sålda artiklar och intäkter per artikel samt identifiera produkter som presterar bäst.

## Senaste aktivitet

The `Recent Activity` på kontrollpanelen visas prestandadata för de senaste 30 dagarna.

## Transaktionshälsa

The `Transaction Health` kontrollpanelen innehåller översiktsdiagram över intäkter, order och genomsnittligt ordervärde. Dessa diagram kan segmenteras av marknadsföringskanaler, demografi eller särskilda kupongkoder.

## Användare att rikta

The `Users to target` Kontrollpanelen innehåller tabellformatsdiagram som listar användare med specifika inköpsbeteenden gemensamt. Några exempel:

* Lista över engångsköpare som köper `X` för flera månader sedan (som du kanske vill återaktivera)

* Lista över de bästa stavningarna (som du kanske vill behålla lyckliga)

* Lista över de största utgivarna som varit aktiva tidigare `X` dagar (som du kanske vill belöna)

Det är enkelt att använda dataexportverktygen [skapa e-postlistor för användare med liknande inköpsbeteenden för målmarknadsföring](http://blog.rjmetrics.com/creating-contact-lists-for-top-customers/).

## Användaraktivitet

The `User activity` Instrumentpanelen innehåller diagram som segmenterar användare efter olika data, inklusive anskaffningskälla, demografiska data och genomsnittlig första beställningsdag. Det innehåller även en analys av användarkohorten, inklusive den totala genomsnittliga intäkten för livstid per användarregistreringsmånad.

The `% of cohort members who have purchased` diagram är värdefullt eftersom det visar konverteringsgraden (från 0 till 1) för användare baserat på när de registrerar sig (varje rad representerar en kohort med användare). Det visas också när de gör sitt första köp (till exempel i månad 1, 2, 3... efter registreringen). Detta kan visa att 10 % av användarna aktiverade under månad 1, medan antalet växer under månad 2, 3, 4.. och kan komma att platåa senare.

Raderna i det här diagrammet blir vanligtvis vågräta efter en viss tidsperiod. Detta visar att få ytterligare kohortmedlemmar konverterar organiskt efter den punkten - de flesta användare som kommer att göra ett köp har redan gjort det. I nuläget är det högst osannolikt att dessa medlemmar kommer att konvertera till köpare utan ingripande. [Att nå ut till dem med anpassade kampanjer eller riktade e-postmeddelanden är ett lågrisksätt att snabbt komma igång med konverteringen av den här befolkningen.](http://blog.rjmetrics.com/acting-on-marketing-data-in-your-rjmetrics-online-dashboard/)
