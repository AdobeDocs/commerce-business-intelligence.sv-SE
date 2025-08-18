---
title: Cohort Report Builder for Non-Date Based Cohorts
description: Lär dig att gruppera användare efter en liknande aktivitet eller attribut.
exl-id: c7b85ce9-113c-4ffc-855f-3d53fe2347d8
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 76c5329c3f55570fa4e46601e902dc5a09e319e7
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 0%

---

# [!DNL Cohort Report Builder] för ej datumbaserade kohorter

[`Cohort Report Builder`](../dev-reports/cohort-rpt-bldr.md) är bra på att hjälpa handlare att studera hur olika undergrupper av användare beter sig över tid. Tidigare har `Cohort Report Builder` optimerats för att gruppera användare efter en gemensam `cohort date` (t.ex. uppsättningen med alla kunder som gjorde sitt första köp under en viss månad). Funktionen `Non-Date Based Cohort` ger dig nu möjlighet att gruppera användare efter en liknande aktivitet eller attribut. Titta på några exempel på användning av den här funktionen.

## Användningsexempel

Det här är ingen omfattande lista, men här finns några möjliga analyser som kan utföras med den här funktionen.

* Undersöker intäkterna för kunder som förvärvats från [!DNL Google] jämfört med [!DNL Facebook]
* Analysera kunder vars första köp gjordes i USA jämfört med Kanada
* Se hur kunder som förvärvats från olika annonskampanjer beter sig

## Så här skapar du en analys

1. Klicka på **[!UICONTROL Report Builder]** på den vänstra fliken eller **[!UICONTROL Add Report** > **Create Report]** på en kontrollpanel.

1. Klicka på `Report Builder Selection` bredvid alternativet **[!UICONTROL Create Report]** på skärmen `Visual Report Builder`.

### Lägga till ett mått

Nu när du befinner dig i `Report Builder` lägger du till det mått som du vill utföra analysen på (exempel: `Revenue` eller `Orders`).

>[!NOTE]
>
>Inbyggda [!DNL Google Analytics]-mått är inte kompatibla med `Cohort Report Builder`. Målet för det här exemplet är att titta på intäkter över tid för förstahandskunder som förvärvats via olika [!DNL Google Analytics]-källor.

### Växla `Metric View` till `Cohort`

![1-växlingsvy för att kohort](../../assets/1-toggle-metric-view-to-cohort.png)

Då öppnas ett nytt fönster där du kan konfigurera informationen i kohortrapporten.

Fem specifikationer krävs för att skapa en Cohortrapport:

1. Gruppera kohorterna
1. Välja kohorter
1. Tidsstämpel för åtgärd
1. Tidsintervall för första åtgärd för kohort
1. Tidsintervall efter kohortförekomst

![kohort-groups](../../assets/2-cohort-groups.png)<!--{: width="200" height="224"}-->



#### &#x200B;1. Gruppera `cohorts`

`Cohorts` grupperas efter en beteendeegenskap, i det här exemplet `Customer's first order GA source`. De alternativ som är tillgängliga här är kolumner som redan har angetts som `groupable` för måttet.

#### &#x200B;2. Välja kohorter

Du kan visa alla resultat för den angivna egenskapen. Eftersom detta kan resultera i många `cohorts` kan du välja det specifika `cohorts` (som motsvarar de olika värden som är tillgängliga för `Customer's first order GA source`) som du behöver.

![kohort-groups](../../assets/4-cohort-groups.png)<!--{: width="300" height="338"}-->

#### 3. `Action timestamp`

På så sätt kan du välja en annan datumbaserad kolumn än den kolumn som måttet skapas i. Nedan tittar du på hur du väljer det tidsintervall som gäller för den angivna `action timestamp`.

#### 4. `Cohort first action time range`

Här väljer du datumintervallet som innehåller `cohorts action timestamp` (så kunder som gjorde den första beställningen från november 2017 till oktober 2018). Det kan vara ett rörligt datumintervall eller ett fast datumintervall.

#### 5. `Time range after cohort occurrence`

Vill du visa `cohorts` över tiden per månad, vecka eller år? Här gör du dessa val. Under det avsnittet väljer du `time range` efter att `cohort action timestamp` har inträffat. Detta visar t.ex. 12 månaders data för de kunder som gjorde den första beställningen under tidsperioden.

![cohort-first-action-time-range](../../assets/5-cohort-first-action-time-range.png)<!--{: width="400" height="557"}-->

>[!NOTE]
>
>[!UICONTROL Filters] som tillämpas på dina mått förblir intakta när du växlar mellan `Standard`- och `Cohort`-vyer.

### Relaterad

Se [`Perspectives`](../../data-analyst/dev-reports/cohort-rpt-bldr.md).
