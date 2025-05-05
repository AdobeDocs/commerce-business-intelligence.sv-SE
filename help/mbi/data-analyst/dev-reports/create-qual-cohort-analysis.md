---
title: Skapa en kvalitativ kohortanalys
description: Läs vad en kvalitativ kohort är, varför du kan vara intresserad av att skapa den här analysen och hur du kan skapa den i Commerce Intelligence.
exl-id: 113244e4-409b-4129-b3d4-7a3433539ade
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---

# Skapa en `Qualitative Cohort Analysis`

Vet du hur era [!DNL Google Adwords]-förvärvade kundsegment utvecklar sin LTV jämfört med de kunder som skaffats via organisk sökning? Har du någonsin funderat på att utföra en `cohort`-analys på olika kundsegment sida vid sida i samma rapport? I så fall kan en `qualitative cohort analysis` hjälpa dig att svara på de frågorna.

Det här avsnittet handlar om vad en kvalitativ kohort är, varför du kan vara intresserad av att skapa den här analysen och hur du kan skapa den i [!DNL Commerce Intelligence].

## Vad är `qualitative cohorts` egentligen? {#whatare}

Analysen av `Cohort` i allmänhet kan definieras brett som en analys av användargrupper som delar liknande egenskaper under sina livscykler. Det gör att du kan identifiera beteendetrender för olika användargrupper.

Se [kohortanalys](https://www.cohortanalysis.com/).

De flesta `cohort` analyserar i [!DNL Commerce Intelligence] gruppanvändare tillsammans efter ett gemensamt datum (t.ex. uppsättningen med alla kunder som gjorde sitt första köp under en viss månad). En `qualitative cohort` är lite annorlunda: det är en användargrupp som definieras av en egenskap som inte är tidsbaserad. Exempel:

* Alla användare som har hämtats från en annonskampanj
* Uppsättningen med alla användare vars första inköp innehöll en kupong (eller inte)
* Uppsättningen med alla användare som har en viss ålder

## Hur skiljer det sig från det vanliga `cohort`-verktyget? {#different}

[`Cohort Analysis Builder`](../dev-reports/cohort-rpt-bldr.md) är optimerad för gruppering av kohorter med hjälp av en tidsbaserad egenskap. Detta är bra för analyser som fokuserar på ett visst användarsegment (till exempel alla användare som har skaffats via en betalsökkampanj). I `Cohort Analysis Builder` kan du (1) fokusera på den specifika användargruppen och (2) `cohort` på ett datum (som deras första orderdatum).

Om du vill analysera kohortbeteendet för flera användarsegment i samma kohortrapport (`paid` sökning kontra `organic` sökning kontra direkt trafik, kanske?) kan den här mer avancerade analysen skapas i `Report Builder` .

## Vilken information ska jag skicka till support för att konfigurera min analys? {#support}

Om du skapar en `qualitative cohort`-rapport i `Report Builder` måste analysteamet i Adobe skapa [avancerade beräknade kolumner](../data-warehouse-mgr/creating-calculated-columns.md) i de nödvändiga tabellerna.

Om du vill skapa dessa skickar du en [supportanmälan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=sv-SE) (och refererar till den här artikeln!). Det här behöver du veta:

* `metric` som du vill utföra din kohortanalys med och vilken tabell den använder (exempel: `Revenue`, som bygger på tabellen `orders`).

* `user segments` som du vill definiera och där den informationen finns i din databas (exempel: olika värden för `User's referral source`, inbyggda i `users`-tabellen och omplacerade ned till `orders`).

* Den `cohort date` som du vill att din analys ska använda (exempel: tidsstämpeln `User's first order date`). I det här exemplet kan vi titta på varje segment och fråga `How does a user's revenue grow in the months following their first order date?`.

* `time interval` som du vill se analysen över (exempel: `weeks`, `months` eller `quarters` efter `User's first order date`).

När analytikerteamet på Adobe har svarat på ovanstående har ni några nya avancerade beräknade kolumner för att ta fram rapporten! Följ sedan instruktionerna nedan.

## Skapa en kvalitativ kohortanalys {#create}

För det första vill du lägga till de mått som du är intresserad av kohortering, en gång för varje `cohort` som du analyserar. I det här exemplet vill du se kumulativa `Revenue` som gjorts månader efter en kunds första order, segmenterade efter `User's referral source`. Det innebär att du för varje segment lägger till ett `Revenue`-mått och filter för det specifika segmentet:

![](../../assets/qualcohort1.gif)

För det andra bör du göra två ändringar av rapportens tidsalternativ:

1. Ange `time interval` som `None`. Detta beror på att du så småningom grupperar tidsintervallet som en dimension i stället för att använda de vanliga tidsalternativen.

1. Ange `time range` till det tidsfönster som du vill att rapporten ska omfatta.

I det här exemplet tittar du på en `all time`-vy av `Revenue`. Efter detta bör du få en serie punkter:

![](../../assets/qualcohort2.gif)

För det tredje justerar du inställningarna för `cohorts`. Baserat på `cohort date` och `time interval` som du har angett för analysteamet i Adobe har du en dimension i ditt konto som utför dateringen `cohort`. I det här exemplet kallas den anpassade dimensionen `Months between this order and customer's first order date`. Om du använder den här dimensionen bör du:

* `Group by` dimensionen med alternativet `group by`

* Välj alla värden för `dimension` som du är intresserad av

* Med `Show top/bottom option` väljer du de X främsta månaderna som du är intresserad av och sorterar efter dimensionen `Months between this order and customer's first order date`

Nu kan du se en rad för varje `cohort` som du har angett. Ta en titt på exemplet nu - du ser `Revenue` från användare av varje hänvisningskälla, `grouped by` antalet månader mellan deras första order och efterföljande order. Exemplet lade också till en `Cumulative perspective` för att se `cohorts'`-aggregerad tillväxt - se resultattabellen för mer granularitet.

Vad säger det här till oss? Här är den specifika hänvisningskällan `Paid search` värdefull den första månaden under en kunds köptid, men behåller inte sin kundbas med upprepade intäkter. Även om `Direct Traffic` startar av till ett lägre belopp ackumuleras intäkterna för efterföljande månader i ungefär samma takt.

Oberoende av hur du diskar det så är `cohort`-analys ett kraftfullt verktyg i analysverktygslådan. Den här typen av analys kan ge dig intressanta insikter om ditt företag som traditionella `time-based cohorts` kanske inte har, vilket gör att du kan fatta bättre datadrivna beslut.
