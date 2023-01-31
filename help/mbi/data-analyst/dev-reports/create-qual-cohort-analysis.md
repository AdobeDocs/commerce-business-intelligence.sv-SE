---
title: Skapa en kvalitativ kohortanalys
description: Läs vad en kvalitativ kohort är, varför du kanske är intresserad av att skapa den här analysen och hur du kan skapa den i [!DNL MBI].
exl-id: 113244e4-409b-4129-b3d4-7a3433539ade
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 0%

---

# Skapa en `Qualitative Cohort Analysis`

Vet du hur din [!DNL Adwords]-förvärvade kundsegment utvecklar sin LTV jämfört med kunder som förvärvats via organiska sökningar? Har du någonsin funderat på att göra en `cohort` analys av olika kundsegment sida vid sida i samma rapport? Om så är fallet, en `qualitative cohort analysis` hjälper dig att svara på de frågorna.

I den här artikeln tittar vi närmare på vad en kvalitativ kohort är, varför du kanske är intresserad av att skapa den här analysen och hur du kan skapa den i [!DNL MBI].

## Vad är `qualitative cohorts`, i alla fall? {#whatare}

`Cohort` analys i allmänhet kan definieras brett som en analys av användargrupper som har liknande egenskaper under sina livscykler. Det gör att du kan identifiera beteendetrender för olika användargrupper.

Se [kohortanalys](https://www.cohortanalysis.com/) - vi skrev webbplatsen på den!

Mest `cohort` analyserar i [!DNL MBI] gruppera användare efter ett gemensamt datum (t.ex. uppsättningen av alla kunder som gjorde sitt första köp under en viss månad). A `qualitative cohort` är lite annorlunda: det är en användargrupp som definieras av en egenskap som inte är tidsbaserad. Några exempel är:

* Alla användare som har hämtats från en annonskampanj
* Uppsättningen med alla användare vars första inköp innehöll en kupong (eller inte)
* Uppsättningen med alla användare som har en viss ålder

## Hur skiljer det sig från det normala? `cohort` builder? {#different}

The [`Cohort Analysis Builder`](../dev-reports/cohort-rpt-bldr.md) är optimerad för gruppering av kohorter med hjälp av en tidsbaserad egenskap. Detta är bra för analyser som fokuserar på ett visst användarsegment (till exempel alla användare som har skaffats via en betalsökningskampanj). I `Cohort Analysis Builder`kan du (1) fokusera på den specifika användargruppen och (2) `cohort` på ett datum (som deras första orderdatum).

Om du vill analysera kohortbeteendet för flera användarsegment i samma kohortrapport (`paid` sökkontra `organic` sökning kontra direkt trafik, kanske?) kan den här mer avancerade analysen skapas i `Report Builder`.

## Vilken information ska jag skicka till support för att konfigurera min analys? {#support}

Skapa en `qualitative cohort` i `Report Builder` engagerar vårt analysteam att skapa [avancerade beräknade kolumner](../data-warehouse-mgr/creating-calculated-columns.md) på de tabeller som behövs.

Om du vill skapa dessa skickar du en [supportanmälan](../../guide-overview.md) (och hänvisa till den här artikeln!). Det här behöver vi veta:

* The `metric` du vill utföra din kohortanalys med och vilken tabell den använder (exempel: `Revenue`, som bygger på `orders` tabell).

* The `user segments` du vill definiera och ange var informationen finns i din databas (exempel: olika värden för `User's referral source`, inbyggt i `users` tabellen och flytta ned till `orders`).

* The `cohort date` vill du att analysen ska använda (exempel: den `User's first order date` tidsstämpel). Det här exemplet gör att vi kan titta på varje segment och fråga `How does a user's revenue grow in the months following their first order date?`.

* The `time interval` som du vill se analysen över (exempel: `weeks`, `months`, eller `quarters` efter `User's first order date`).

När våra analytikerteam har svarat på ovanstående har ni några nya avancerade beräknade kolumner för att ta fram rapporten! Sedan kan du följa instruktionerna nedan.

## Skapa en kvalitativ kohortanalys {#create}

Först vill du lägga till de mätvärden du är intresserad av kohortering, en gång för varje `cohort` du analyserar. I det här exemplet vill vi se kumulativ `Revenue` som görs månader efter en kunds första order, segmenterad av `User's referral source`. Det innebär att vi för varje segment lägger till ett `Revenue` mått och filter för det specifika segmentet:

![](../../assets/qualcohort1.gif)

För det andra bör du göra två ändringar av rapportens tidsalternativ:

1. Ange `time interval` till `None`. Detta beror på att vi så småningom grupperar tidsintervallet som en dimension i stället för att använda de vanliga tidsalternativen.

1. Ange `time range` till det tidsfönster du vill att rapporten ska täcka.

I vårt exempel tittar vi på en `all time` vy av `Revenue`. Efter detta bör du få en serie punkter:

![](../../assets/qualcohort2.gif)

För det tredje ska du göra en justering för att ställa in `cohorts`. Baserat på `cohort date` och `time interval` som du har angett för vårt analysteam har du en dimension i ditt konto som kommer att utföra `cohort` datering. I det här exemplet anropas den anpassade dimensionen `Months between this order and customer's first order date`. Om du använder den här dimensionen bör du:

* `Group by` dimensionen med `group by` option

* Markera alla värden i `dimension` där du är intresserad

* Med `Show top/bottom option`, välj de X månader du är intresserad av och sortera efter `Months between this order and customer's first order date` dimension

Nu kan du se en rad för varje `cohort` som du angav. Titta på vårt exempel nu - vi ser `Revenue` från användare av varje hänvisningskälla, `grouped by` antalet månader mellan den första ordern och efterföljande order. Vi har även lagt till en `Cumulative perspective` för att se `cohorts'` aggregerad tillväxt - se resultattabellen för mer granularitet.

Vad säger det här till oss? Här är den specifika hänvisningskällan `Paid search` är mycket värdefullt den första månaden av en kunds köptid, men inte behåller sin kundbas med upprepade intäkter. while `Direct Traffic` från början till ett lägre belopp, ackumuleras intäkterna under de följande månaderna i ungefär samma takt.

Oberoende av hur du diskar det, `cohort` analys är ett kraftfullt verktyg i analysverktygslådan. Den här typen av analys kan ge en del mycket intressanta insikter om din verksamhet som traditionella `time-based cohorts` kanske inte gör det möjligt för er att fatta bättre datadrivna beslut.
