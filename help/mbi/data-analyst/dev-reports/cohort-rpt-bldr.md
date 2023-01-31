---
title: Kohort Report Builder
description: Lär dig mer om analysen av användargrupper som delar liknande egenskaper under sina livscykler.
exl-id: d80c5389-7256-40e0-86e0-49903113f93d
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1599'
ht-degree: 0%

---

# Kohort Report Builder

Har du någonsin velat studera hur olika delar av dina användare beter sig över tiden? Har du till exempel undrat om användare som registrerar sig under en kampanjperiod har en högre genomsnittlig livstidsintäkt än de som inte gör det? Om svaret är `Yes`och sedan `Cohort Report Builder` är det perfekta verktyget för dig. [!DNL MBI] är specifikt optimerat för att utföra den här analysen och göra den relevant för din verksamhet.

## Vad är kohortanalys? {#what}

`Cohort` analys kan definieras brett som en analys av användargrupper som delar liknande egenskaper under sina livscykler. Det gör att du kan identifiera beteendetrender för olika användargrupper.

För en mer detaljerad introduktion på `cohort` analys, [ta en titt här](https://www.cohortanalysis.com/) - vi skrev webbplatsen på den!

I [!DNL MBI] kontrollpanel, är det enkelt att skapa användare `cohorts` baserat på en `cohort` datum och ett mått i ditt konto.

## Varför är kohortanalys viktigt? {#important}

Som nämnts ovan `cohort` Med hjälp av analys kan du identifiera beteendetrender mellan olika användargrupper. Med en god förståelse för hur vissa grupper beter sig kan ni skräddarsy era beslut och utgifter för att maximera försäljningen. Exempel: en livstidsintäkt `cohort` analys - även om den här typen av analys är fördelaktig av många skäl är den omedelbara en bättre kundvärvningsbeslut.

## Hur skapar jag en egen `cohort` analys?

### Ny arkitektur

Det här är instruktionerna för att använda `Cohort Report Builder` på [Ny arkitektur](../../administrator/account-management/new-architecture.md).

1. Klicka **[!UICONTROL Report Builder]** på den vänstra fliken eller **[!UICONTROL Add Report** > **Create Report]** i en kontrollpanel.

1. I `Report Builder` markeringsskärm, klicka **[!UICONTROL Create Report]** bredvid `Visual Report Builder` alternativ.

**Lägga till ett mått**

Nu när vi är i `Report Builder`lägger vi till mätvärden som vi vill utföra analysen på (exempel: `Revenue` eller `Orders`).

>[!NOTE]
>
>Inbyggt [!DNL Google Analytics] mätvärden är inte kompatibla med `Cohort Report Builder`.

**Växla måttvyn till`Cohort`**

![](../../assets/visual-report-builder-cohort-toggle.png)

Då öppnas ett nytt fönster där vi kan konfigurera informationen i `Cohort` Rapport.

### Fem specifikationer krävs för att skapa en `Cohort` rapport:

1. Gruppera `cohorts`
1. The `cohort` tidsperiod
1. Antalet `cohorts` visa
1. Den minsta mängden data per `cohort` måste innehålla
1. Tidsintervall efter `cohort` förekomst

#### 1. Gruppering `cohorts`

`Cohorts` grupperas tillsammans med en tidsstämpel, som **bokföringsdag** eller **första orderdatum**.

>[!NOTE]
>
>Du kan inte använda samma tidsstämpel som måttet är byggt på för `cohort` datum. För en analys som kräver detta kan du använda `Standard report builder` i stället.

#### 2. `Cohort` tidsperiod

Välj den tidsperiod som ska grupperas `cohorts` av. med andra ord, vilken del av tidsstämpeln som du valde ovan är viktigast; den `week`, `month`, `quarter`, eller `year`?  Din rapport visar data i valfritt intervall som du väljer här

#### 3. och 4. Ange antalet `cohorts` för att visa och hur mycket data varje `cohort` måste ha

Med de här parametrarna kan du endast visa `cohorts` som du är intresserad av, och är till nytta `Preview` rutan längst ned i fönstret visar exakt vilka kohorter som kommer att visas i rapporten.

Som standard är den aktuella `cohort` inkluderas inte om du inte ändrar den minsta mängden data som krävs för varje `cohort` till `0`. I det här fallet `cohort` för den aktuella tidsperioden kommer endast att innehålla partiella data.

#### 5. Tidsintervall efter `Cohort` Förekomst

Med den här funktionen kan du ange det tidsintervall med data som du vill visa för den markerade `cohorts`. Om du till exempel vill visa 24 bilder varje månad `cohorts` baserat på `customer's first order date`men du är bara intresserad av de första tre månadernas data för varje `cohort`kan du ange `number of cohorts to view` till `24` och `time range after cohort occurrence` till `3`.

Intervallet för det här värdet ändras med det du har valt i `cohort time period` och värdet är inställt på `12` som standard, värdet ändras inte om du inte klickar på kalenderikonen för att redigera den.

![](../../assets/cohort-time-range.png)

#### Övriga anmärkningar

* [!UICONTROL Filters]: som tillämpas på mätvärdena förblir intakta när du växlar mellan `Standard` och `Cohort` vyer.

* Se [`Perspectives`](#perspectives).

#### Exempel

Här är ett exempel på hur du kan samla ihop allt. I det här exemplet vill jag checka ut orderbeteendet efter en `cohort`Första gången du handlar för att se om den där kohorten kommer tillbaka och gör upprepade inköp under de kommande sex månaderna.

![Orderkohort](../../assets/crb_example.gif)

### Äldre arkitektur

#### Äldre arkitektur {#personalinfo}

Nedan finns instruktioner som är specifika för den äldre versionen av `Cohort Report Builder`. Om du är intresserad av att använda den nya versionen finns mer information i [Ny arkitektur](../../administrator/account-management/new-architecture.md) för mer information om migrering till [!DNL MBI] Nytt arkitekturkonto.

#### Hur skapar jag en egen `cohort` analys? {#create}

![](../../assets/create-cohort-analysis.png)

`Cohort` analys in action! Här kan vi se hur intäkterna ökar med tiden på kumulativ basis och per användare.

I det här avsnittet går vi igenom hur du skapar en egen `cohort` analys. Ta en titt på [Exempel](#examples) i den här artikeln.

1. Klicka **[!UICONTROL Report Builder]** på den vänstra fliken eller **[!UICONTROL Add Report** > **Create Report]** i en kontrollpanel.

1. I `Report Builder Selection` skärm, klicka **[!UICONTROL Create Report]** bredvid `Cohort Analysis` alternativ.

#### Lägga till ett mått

Nu när vi är i `Cohort Report Builder`, låt oss lägga till måttet (exempel: `Revenue` eller `Number of orders`) som vi vill utföra analysen på.

>[!NOTE]
>
>Inbyggt [!DNL Google Analytics] mätvärden är inte kompatibla med `Cohort Report Builder`.

#### Välja kohortdatum {#date}

Nästa steg är att ange `cohort date`. Detta är det datum som dina användare grupperas efter. Detta kan till exempel vara `User's first order date` eller `User's registration date`.

>[!NOTE]
>
>Du kan inte använda samma datum som måttet är byggt på (exempel: `created at`) som `cohort date`.

#### Ange intervall och tidsperiod

Sedan ställer vi in `Interval` och `Time Period`.

`Interval`
The `Interval` kan du ange `length` på `cohorts`. Om detta till exempel är inställt på `Month`, kommer rapporten att mätas i månader.

Du kan ändra hur de här intervallen visas på x-axeln med **Varaktighet** -menyn.

`Time Period`
Använd `Time Period` för att välja den specifika användaren `cohorts` att analysera. Du kan visa var `cohort`, välja från en lista, ange ett tidsintervall eller definiera ett rullande tidsintervall för `cohorts` att inkludera. Om vi till exempel använde `Specific Cohorts` kan vi välja vilka månader som ska ingå i analysen:

![Använda `Time Period` meny för att lägga till specifik `Cohorts`](../../assets/Cohort_Time_Period.gif)

Om vi grupperade våra `cohorts` efter registreringsdatum och sedan välja april, maj och juni i `Specific Cohorts` listan kommer alla användare som är registrerade under dessa månader att tas med.

#### Definiera X-axeln

Under `duration`kan du definiera diagrammets X-axelinställningar. Det vill säga hur många tidsperioder varje datapunkt representerar och hur många datapunkter som ska ingå i analysen.

#### Markera `counting members` table

Om du valde att gruppera användare efter en `cohort date` som har anslutits från en annan tabell kan du se en `counting members in the … table` alternativ.

![](../../assets/Cohort_Counting_Members_option.png)

Låt oss titta på ett exempel för att förstå den här inställningen. Anta att du har byggt en rapport som kohorterar en `Revenue` mått efter `Customer's registration date`. Du ville också använda perspektivet `Average value per cohort member` för att se intäkten per köpare över tid. För att hitta genomsnittsvärdet per köpare måste vi bestämma hur många köpare vi ska dividera med. Är det antalet registrerade kunder i din `customers` eller är det antalet olika köpare i `orders table` under samma tidsperiod?

Den här inställningen besvarar den frågan. Räkna medlemmar i `customers` tabellen omfattar alla kunder (oavsett om de har köpt något eller inte) i genomsnitt. Räkna medlemmar i `orders` tabellen innehåller endast kunder som har gjort ett köp.

#### Välja ett perspektiv {#perspective}

När du har definierat måttet och hur du vill analysera det kan du välja `perspective` som du vill använda.

Precis ovanför rapportvisualiseringen visas en listruta med `perspective` inställningar.

Se [Perspektiv](#perspectives).

![](../../assets/Cohort_Perspective_Menu.png)

## Exempel på kohortanalys {#examples}

Nu när vi har gått igenom hur man skapar en `cohort` -analys, låt oss ta en titt på några exempel.

### Jag vill veta hur min användare `cohorts` växer med tiden.

![Användare `cohorts` växa över tid](../../assets/cohort1.gif)

I det här exemplet analyserade vi `Revenue` metrisk, grupperade våra kohorter efter `customer's first order date`och de 8 senaste `cohorts` (definieras i `Time Period` -menyn) som ska ingå i analysen. För att se hur kohorterna växte över tiden använde vi `Cumulative Average Value per Cohort Member` `perspective`.

### Jag vill i genomsnitt veta hur många order en användare gör vid olika tidpunkter under sin livstid.

!![Average number of orders users make at different points in their lifetimes](../../assets/cohort2.gif

I det här exemplet har vi analyserat `Number of orders` metrisk, grupperade våra kohorter efter `customer's first order date`och innehöll de 8 senaste kohorterna (definieras i `Time Period` i analysen. För att se det genomsnittliga antalet order för varje kohort har vi ändrat `perspective` till `Average Value per Cohort Member`.

### Jag vill förstå hur en användares framtida inköpsaktivitet jämförs med den första månadens aktivitet med verksamheten.

![Jämföra en användares framtida inköpsaktivitet med den första aktivitetsmånaden](../../assets/cohort3.gif)

## `Perspectives` {#perspectives}

`Standard`
Detta visar det inkrementella bidraget från en viss kohortgrupp vid en given tidpunkt i livscykeln. (exempel: Poängen &quot;Vecka 6&quot; visar alla datapunkter som skapats av användare under den sjätte veckan.)

`Average Value per Cohort Member`
Detta delar upp `Standard cohort` analys i (1) av antalet användare i varje `cohort` grupp. Detta kan vara användbart för att jämföra kohortresultat för äpplen till äpplen, eftersom inte alla kohortgrupper kan innehålla samma antal användare. Exempelvis den genomsnittliga intäkten för vecka 6 per användare från en viss `cohort`.

`Cumulative`
Detta `perspective` visar det traditionella `cohort` analys av en `cumulative` bas. Den visar med andra ord det totala bidraget från en viss kohort hittills vid en viss tidpunkt i livscykeln. Till exempel den kumulativa intäkten efter sex veckor för användare från en viss kohort.

`Cumulative Average Value per Cohort Member`
Detta delar upp `Cumulative` analys i (3) av antalet användare i varje `cohort` grupp. Här visas den genomsnittliga livstidsavgiften (ofta genomsnittliga livstidsintäkter) per `cohort` medlem vid varje period i `cohort's` liv. Exempel: den genomsnittliga livstidsintäkten efter sex månader för användare som gick med i juni.

`Percent of First Value (show first value)`
Detta analyserar sammanställningen `cohort` bidrag vid en viss tidpunkt i `cohort's` livscykeln som en procentandel av deras bidrag under den första perioden. Till exempel intäkterna för månad 6 delat med intäkterna för månad 1 för användare som gick med i juni.

`Percent of First Value (hide first value)`
Detta är samma sak som `perspective` ovan, förutom att värdet 100 % för den första tidsperioden är dolt.

## Radbrytning {#finish}

The `Cohort Report Builder` är optimerat för att gruppera användare efter en gemensam `cohort date`. Du kanske är intresserad av att gruppera användarna efter en liknande aktivitet eller attribut - i så fall vill vi gärna hjälpa till! Vi rekommenderar utcheckning [den här självstudiekursen om kvalitativa kohorter](../dev-reports/create-qual-cohort-analysis.md) för att komma igång.
