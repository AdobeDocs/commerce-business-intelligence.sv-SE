---
title: Cohort Report Builder
description: Lär dig mer om analysen av användargrupper som delar liknande egenskaper under sina livscykler.
exl-id: d80c5389-7256-40e0-86e0-49903113f93d
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '1607'
ht-degree: 0%

---

# Cohort Report Builder

Har du någonsin velat studera hur olika delar av dina användare beter sig över tiden? Har du till exempel undrat om användare som registrerar sig under en kampanjperiod har en högre genomsnittlig livstidsintäkt än de som inte gör det? Om svaret är `Yes` är `Cohort Report Builder` det perfekta verktyget för dig. [!DNL Adobe Commerce Intelligence] är optimerad för att utföra den här analysen och göra den relevant för din verksamhet.

## Vad är kohortanalys? {#what}

`Cohort`-analys kan definieras brett som en analys av användargrupper som delar liknande egenskaper under sina livscykler. Det gör att du kan identifiera beteendetrender för olika användargrupper.

Om du vill ha en grundlig introduktion om `cohort`-analys kan du gå igenom [den här sidan](https://www.cohortanalysis.com/).

På din [!DNL Commerce Intelligence]-kontrollpanel är det enkelt att skapa användare `cohorts` baserat på ett `cohort`-datum och ett mätvärde i ditt konto.

## Varför är kohortanalys viktigt? {#important}

Som nämnts ovan kan du med `cohort`-analys identifiera beteendetrender mellan olika användargrupper. Med en god förståelse för hur vissa grupper beter sig kan ni skräddarsy era beslut och utgifter för att maximera försäljningen. Ta till exempel en analys av `cohort` för livstidsintäkt - även om den här typen av analys är fördelaktig av många skäl är den omedelbara en bättre kundvärvningsbeslut.

## Hur skapar jag en egen `cohort`-analys?

### Ny arkitektur

Det här är instruktionerna för att använda `Cohort Report Builder` i den [nya arkitekturen](../../administrator/account-management/new-architecture.md).

1. Klicka på **[!UICONTROL Report Builder]** på den vänstra fliken eller **[!UICONTROL Add Report** > **Create Report]** på en kontrollpanel.

1. Klicka på `Report Builder` bredvid alternativet **[!UICONTROL Create Report]** på markeringsskärmen `Visual Report Builder`.

**Lägger till ett mått**

Nu när du befinner dig i `Report Builder` lägger du till det mått som du vill utföra analysen på (exempel: `Revenue` eller `Orders`).

>[!NOTE]
>
>Inbyggda [!DNL Google Analytics]-mått är inte kompatibla med `Cohort Report Builder`.

**Växla måttvyn till`Cohort`**

![Visuell växlingsfunktion för Report Builder med kohortanalys](../../assets/visual-report-builder-cohort-toggle.png)

Ett nytt fönster öppnas där informationen i rapporten `Cohort` konfigureras.

### Fem specifikationer krävs för att skapa en `Cohort`-rapport:

1. Gruppera `cohorts`
1. Tidsperioden `cohort`
1. Antalet `cohorts` som ska visas
1. Den minsta mängden data som varje `cohort` måste innehålla
1. Tidsintervall efter `cohort` förekomst

#### &#x200B;1. Gruppera `cohorts`

`Cohorts` grupperas efter en tidsstämpel, till exempel **registreringsdatum** eller **första orderdatum**.

>[!NOTE]
>
>Du kan inte använda samma tidsstämpel som måttet är byggt på för datumet `cohort`. För en analys som kräver detta kan du använda `Standard report builder` i stället.

#### &#x200B;2. `Cohort`-tidsperiod

Välj den tidsperiod som `cohorts` ska grupperas efter. Med andra ord, vilken del av tidsstämpeln som du markerade ovan är viktigast: `week`, `month`, `quarter` eller `year`? Din rapport visar data i valfritt intervall som du väljer här

#### &#x200B;3. och 4. Ange antalet `cohorts` som ska visas och hur mycket data varje `cohort` måste ha

De här parametrarna hjälper dig att endast visa `cohorts` som du är intresserad av, och den praktiska `Preview`-rutan längst ned i fönstret visar exakt vilka kohorter som visas i rapporten.

Som standard inkluderas inte aktuell `cohort` om du inte ändrar den minsta mängden data som krävs för varje `cohort` till `0`. I det här fallet innehåller `cohort` för den aktuella tidsperioden endast partiella data.

#### &#x200B;5. Tidsintervall efter `Cohort` förekomst

Med den här funktionen kan du ange det tidsintervall med data som du visar för den markerade `cohorts`. Om du till exempel vill visa `cohorts` varje månad `customer's first order date`, men bara är intresserad av de första tre månaderna med data för varje `cohort` , kan du ange `number of cohorts to view` till `24` och `time range after cohort occurrence` till `3`.

Intervallet för det här värdet ändras med det du har markerat i `cohort time period` och värdet ställs in på `12` som standard. Värdet ändras inte om du inte klickar på kalenderikonen för att redigera det.

![Kohortintervallväljare med datumalternativ](../../assets/cohort-time-range.png)

#### Övriga anmärkningar

* [!UICONTROL Filters]: som tillämpas på dina mått förblir intakta när du växlar mellan `Standard` - och `Cohort`-vyer.

* Se [`Perspectives`](#perspectives).

#### Exempel

Här är ett exempel på hur du kan samla ihop allt. I det här exemplet vill jag checka ut orderbeteendet efter ett köp av en `cohort` för att se om den kohorten kommer tillbaka för att göra upprepade inköp under de kommande sex månaderna.

![Orderkohort](../../assets/crb_example.gif)

### Äldre arkitektur

#### Äldre arkitektur {#personalinfo}

Nedan finns instruktioner som är specifika för den äldre versionen av `Cohort Report Builder`. Om du är intresserad av att använda den nya versionen läser du [Ny arkitektur](../../administrator/account-management/new-architecture.md) för mer information om hur du migrerar till ett [!DNL Commerce Intelligence] nytt arkitekturkonto.

#### Hur skapar jag en egen `cohort`-analys? {#create}

![Skapa en dialogruta för kohortanalys med konfigurationsalternativ](../../assets/create-cohort-analysis.png)

`Cohort`-analys används! Här kan du se hur intäkterna ökar med tiden på kumulativ basis och per användare.

I det här avsnittet får du hjälp med att skapa en egen `cohort`-analys. Exempel (och animerade GIF-filer som demonstrerar processen) finns i avsnittet [Exempel](#examples) i det här avsnittet.

1. Klicka på **[!UICONTROL Report Builder]** på den vänstra fliken eller **[!UICONTROL Add Report** > **Create Report]** på en kontrollpanel.

1. Klicka på `Report Builder Selection` bredvid alternativet **[!UICONTROL Create Report]** på skärmen `Cohort Analysis`.

#### Lägga till ett mått

Nu när du är i `Cohort Report Builder` lägger du till mätvärdet (exempel: `Revenue` eller `Number of orders`) som du vill utföra analysen på.

>[!NOTE]
>
>Inbyggda [!DNL Google Analytics]-mått är inte kompatibla med `Cohort Report Builder`.

#### Välja kohortdatum {#date}

Nästa steg är att ange `cohort date`. Detta är det datum som dina användare grupperas efter. Detta kan till exempel vara `User's first order date` eller `User's registration date`.

>[!NOTE]
>
>Du kan inte använda samma datum som måttet är byggt på (exempel: `created at`) som `cohort date`.

#### Ange intervall och tidsperiod

Ange sedan `Interval` och `Time Period`.

`Interval`
Med alternativet `Interval` kan du ange `length` för `cohorts` . Om värdet till exempel är `Month` mäts rapporten i månader.

Du kan ändra hur dessa intervall visas på x-axeln med menyn **Varaktighet** .

`Time Period`
Använd menyn `Time Period` för att välja den specifika användare `cohorts` som ska analyseras. Du kan visa varje `cohort`, välja från en lista, ange ett tidsintervall eller definiera ett rullande tidsintervall på `cohorts` som ska inkluderas. Om du till exempel har använt alternativet `Specific Cohorts` kan du välja specifika månader att inkludera i analysen:

![Använda menyn `Time Period` för att lägga till specifik `Cohorts`](../../assets/Cohort_Time_Period.gif)

Om du grupperar `cohorts` efter registreringsdatum och sedan väljer april, maj och juni i listan `Specific Cohorts` kommer alla användare som registrerade sig under dessa månader att tas med.

#### Definiera X-axeln

Under `duration` kan du definiera diagrammets X-axelinställningar. Det vill säga hur många tidsperioder varje datapunkt representerar och hur många datapunkter som ska ingå i analysen.

#### Markera tabellen `counting members`

Om du har valt att gruppera användare efter en `cohort date` som har anslutits från en annan tabell kan du se ett `counting members in the … table`-alternativ.

![Alternativ för medlemmar i kohorträkning som visar oberoende kontra kumulativa lägen](../../assets/Cohort_Counting_Members_option.png)

Titta på ett exempel som förstår den här inställningen. Anta att du har skapat en rapportkohortering för ett `Revenue`-mått av `Customer's registration date`. Du vill också använda perspektivet `Average value per cohort member` för att se intäkten per köpare över tiden. Om du vill hitta det genomsnittliga värdet per köpare måste du bestämma hur många köpare som ska divideras med. Är det antalet registrerade kunder i din `customers`-tabell, eller är det antalet distinkta köpare i din `orders table` under samma period?

Den här inställningen besvarar den frågan. Räknade medlemmar i tabellen `customers` inkluderar alla kunder (oavsett om de har gjort ett köp någonsin) i genomsnitt. Räknade medlemmar i tabellen `orders` innehåller endast kunder som har gjort ett köp.

#### Välja ett perspektiv {#perspective}

När du har definierat måttet och hur du vill analysera det kan du välja den `perspective` som du vill använda.

Precis ovanför rapportvisualiseringen finns en listruta med `perspective` inställningar.

Se [Perspektiv](#perspectives).

![Perspektivmenyn Kohort med olika visningsalternativ](../../assets/Cohort_Perspective_Menu.png)

## Exempel på kohortanalys {#examples}

Nu när du har gått igenom hur du skapar en `cohort`-analys kan du titta på några exempel.

### Jag vill veta hur min användare `cohorts` växer över tid.

![Användaren `cohorts` växer över tid](../../assets/cohort1.gif)

I det här exemplet har du analyserat `Revenue`-måttet, grupperat kohorterna efter `customer's first order date` och valt de 8 senaste `cohorts` (som definieras på `Time Period` -menyn) som ska ingå i analysen. Du använde `Cumulative Average Value per Cohort Member` `perspective` för att se hur kohorterna växte över tiden.

### Jag vill i genomsnitt veta hur många order en användare gör vid olika tidpunkter under sin livstid.

(../../assets/cohort2.gif)

I det här exemplet analyserade du måttet `Number of orders`, grupperade dina kohorter efter `customer's first order date` och inkluderade de åtta senaste kohorterna (som definieras på menyn `Time Period`) i analysen. Om du vill se det genomsnittliga antalet order för varje kohort ändrade du `perspective` till `Average Value per Cohort Member`.

### Jag vill förstå hur en användares framtida inköpsaktivitet jämförs med den första månadens aktivitet med verksamheten.

![Jämför en användares framtida inköpsaktivitet med den första aktivitetsmånaden](../../assets/cohort3.gif)

## `Perspectives` {#perspectives}

`Standard`
Detta visar det inkrementella bidraget från en viss kohortgrupp vid en given tidpunkt i livscykeln. (Exempel: Poängen &quot;Vecka 6&quot; visar alla datapunkter som skapats av användare under den sjätte veckan.)

`Average Value per Cohort Member`
Detta delar in `Standard cohort` -analysen i (1) med antalet användare i varje `cohort` -grupp. Detta kan vara användbart för att jämföra kohortresultat för äpplen till äpplen, eftersom inte alla kohortgrupper kan innehålla samma antal användare. Exempelvis den genomsnittliga intäkten för vecka 6 per användare från en viss `cohort`.

`Cumulative`
I `perspective` visas den traditionella `cohort` analysen `cumulative` . Den visar med andra ord det totala bidraget från en viss kohort hittills vid en viss tidpunkt i livscykeln. Till exempel den kumulativa intäkten efter sex veckor för användare från en viss kohort.

`Cumulative Average Value per Cohort Member`
Detta delar in `Cumulative` -analysen i (3) med antalet användare i varje `cohort` -grupp. Den visar den genomsnittliga livstidsavgiften (ofta genomsnittlig livstidsintäkt) per `cohort`-medlem för varje period i `cohort's`-livet. Exempel: den genomsnittliga livstidsintäkten efter sex månader för användare som gick med i juni.

`Percent of First Value (show first value)`
Detta analyserar det sammanlagda `cohort` bidraget vid en viss tidpunkt i en `cohort's` livscykel som en procentandel av deras bidrag under den första perioden. Till exempel intäkterna för månad 6 dividerat med intäkterna för månad 1 för användare som gick med i juni.

`Percent of First Value (hide first value)`
Detta är samma som `perspective` ovan, förutom att värdet 100 % för den första tidsperioden är dolt.

## Radbrytning {#finish}

`Cohort Report Builder` är optimerad för att gruppera användare efter en gemensam `cohort date`. Du kan vara intresserad av att gruppera användarna efter en liknande aktivitet eller ett liknande attribut. Adobe rekommenderar att du checkar ut [den här självstudiekursen om kvalitativa kohorter](../dev-reports/create-qual-cohort-analysis.md) för att komma igång.
