---
title: Kohort Report Builder för icke-datumbaserade kohorter
description: Lär dig att gruppera användare efter en liknande aktivitet eller attribut.
exl-id: c7b85ce9-113c-4ffc-855f-3d53fe2347d8
source-git-commit: 6b1bd96a0f9ae8bda3ae8db8ca78ad655079f2a4
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# [!DNL Cohort Report Builder] för ej datumbaserade kohorter

The [`Cohort Report Builder`](../dev-reports/cohort-rpt-bldr.md) är bra att hjälpa handlare att studera hur olika delar av användare beter sig över tid. Tidigare var `Cohort Report Builder` optimerades för att gruppera användare efter en gemensam `cohort date` (t.ex. en uppsättning med alla kunder som gjorde sitt första köp under en viss månad). The `Non-Date Based Cohort` ger dig nu möjlighet att gruppera användare efter en liknande aktivitet eller attribut. Titta på några exempel på användning av den här funktionen.

## Användningsexempel

Det här är ingen omfattande lista, men här finns några möjliga analyser som kan utföras med den här funktionen.

* Granska intäkterna från kunder som förvärvats från [!DNL Google] kontra [!DNL Facebook]
* Analysera kunder vars första köp gjordes i USA och Kanada
* Se hur kunder som förvärvats från olika annonskampanjer beter sig

## Så här skapar du en analys

1. Klicka **[!UICONTROL Report Builder]** på den vänstra fliken eller **[!UICONTROL Add Report** > **Create Report]** i en kontrollpanel.

1. I `Report Builder Selection` skärm, klicka **[!UICONTROL Create Report]** bredvid `Visual Report Builder` alternativ.

### Lägga till ett mått

Nu när du är i `Report Builder`lägger du till de mätvärden som du vill utföra analysen på (exempel: `Revenue` eller `Orders`).

>[!NOTE]
>
>Inbyggt [!DNL Google Analytics] mätvärden är inte kompatibla med `Cohort Report Builder`. Målet med det här exemplet är att se på intäkterna över tiden för förstahandskunder som förvärvats via olika [!DNL Google Analytics] källor.

### Växla `Metric View` till `Cohort`

![1-växlad metrisk vy för kohort](../../assets/1-toggle-metric-view-to-cohort.png)

Då öppnas ett nytt fönster där du kan konfigurera informationen i kohortrapporten.

Fem specifikationer krävs för att skapa en Cohortrapport:

1. Gruppera kohorterna
1. Välja kohorter
1. Tidsstämpel för åtgärd
1. Tidsintervall för första åtgärd för kohort
1. Tidsintervall efter kohortförekomst

![cohort-groups](../../assets/2-cohort-groups.png)<!--{: width="200" height="224"}-->

!![cohort-first-action-time-range]<!--(../../assets/3-cohort-first-action-time-range.png){: width="400" height="554"}-->

#### 1. Gruppering `cohorts`

`Cohorts` grupperas efter en beteendeegenskap, i det här exemplet `Customer's first order GA source`. De alternativ som är tillgängliga här är kolumner som redan är angivna som `groupable` för måttet.

#### 2. Välja kohorter

Du kan visa alla resultat för den angivna egenskapen. Detta kan leda till många `cohorts`kan du välja `cohorts` (som motsvarar de olika värden som är tillgängliga för `Customer's first order GA source`) som du behöver.

![cohort-groups](../../assets/4-cohort-groups.png)<!--{: width="300" height="338"}-->

#### 3. `Action timestamp`

På så sätt kan du välja en annan datumbaserad kolumn än den kolumn som måttet skapas i. Nedan tittar du på hur du väljer det tidsintervall som gäller för den angivna `action timestamp`.

#### 4. `Cohort first action time range`

Här väljer du datumintervallet som innehåller `cohorts action timestamp` (så kunder som gjorde den första beställningen från november 2017 till oktober 2018). Det kan vara ett rörligt datumintervall eller ett fast datumintervall.

#### 5. `Time range after cohort occurrence`

Vill du se `cohorts` över tid per månad, vecka eller år? Här gör du dessa val. Under det avsnittet väljer du `time range` efter `cohort action timestamp` inträffade. Detta visar t.ex. 12 månaders data för de kunder som gjorde den första beställningen under tidsperioden.

![cohort-first-action-time-range](../../assets/5-cohort-first-action-time-range.png)<!--{: width="400" height="557"}-->

>[!NOTE]
>
>[!UICONTROL Filters] som tillämpas på mätvärdena förblir intakta när du växlar mellan `Standard` och `Cohort` vyer.

### Relaterad

Se [`Perspectives`](../../data-analyst/dev-reports/cohort-rpt-bldr.md).
