---
title: Förväntad analys av livstidsvärde (LTV) för Pro
description: Lär dig hur du skapar en kontrollpanel som hjälper dig att förstå kundens livstidsvärde och kundernas förväntade livstidsvärde.
exl-id: e353b92a-ff3b-466b-b519-4f86d054c0bc
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# Förväntad analys av livstidsvärde

Det här avsnittet visar hur du skapar en instrumentpanel som hjälper dig att förstå kundens livstidsvärde och kundernas förväntade livstidsvärde.

![](../../assets/exp-lifetim-value-anyalysis.png)

Den här analysen är endast tillgänglig för Pro-kontokunder med den nya arkitekturen. Om ditt konto har åtkomst till `Persistent Views` funktionen under `Manage Data` på den nya arkitekturen och följer instruktionerna här för att själv bygga denna analys.

Innan du börjar, vill du bekanta dig med [cohort report builder.](../dev-reports/cohort-rpt-bldr.md)

## Beräknade kolumner

Kolumner att skapa på **order** register om använder **30-dagars månader**:

* [!UICONTROL Column name]: `Months between first order and this order`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]: A = `Seconds between customer's first order date and this order`
* 
   [!UICONTROL Datatype]: `Integer`
* **Definition:**`case when A is null then null when A <= 0 then '1'::int else (ceil(A)/2629800)::int end`

* [!UICONTROL Column name]: `Months since order`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]: A = `created_at`
* 
   [!UICONTROL Datatype]: `Integer`
* Definition: `case when created_at is null then null else (ceil((extract(epoch from current_timestamp) - extract(epoch from created_at))/2629800))::int end`

Kolumner att skapa på **`orders`** register om använder **kalender** månader:

* [!UICONTROL Column name]: `Calendar months between first order and this order`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column inputs]:
   * `A` = `created_at`
   * `B` = `Customer's first order date`

* 
   [!UICONTROL Datatype]: `Integer`
* Definition: `case when (A::date is null) or (B::date is null) then null else ((date_part('year',A::date) - date_part('year',B::date))*12 + date_part('month',A::date) - date_part('month',B::date))::int end`

* [!UICONTROL Column name]: `Calendar months since order`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]: `A` = `created_at`
* 
   [!UICONTROL Datatype]: `Integer`
* **Definition:**`case when A is null then null else ((date_part('year',current_timestamp::date) - date_part('year',A::date))*12 + date_part('month',current_timestamp::date) - date_part('month',A::date))::int end`

* [!UICONTROL Column name]: `Is in current month? (Yes/No)`
* [!UICONTROL Column type]: `Same Table`
* 
   [!UICONTROL Column equation]: `CALCULATION`
* [!UICONTROL Column input]: A = `created_at`
* 
   [!UICONTROL Datatype]: `String`
* Definition: `case when A is null then null when (date_trunc('month', current_timestamp::date))::varchar = (date_trunc('month', A::date))::varchar then 'Yes' else 'No' end`

## Mått

### Mätinstruktioner

Mätvärden som ska skapas

* **Distinkta kunder efter första orderdatum**
   * Om du aktiverar gästorder använder du `customer_email`

* I **`orders`** table
* Detta mått utför en **Antal distinkta värden**
* På **`customer_id`** kolumn
* Beställd av **`Customer's first order date`** tidsstämpel

>[!NOTE]
>
>Se till att [lägga till alla nya kolumner som dimensioner till mått](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) innan du skapar nya rapporter.

## Rapporter

### Rapportinstruktioner

**Förväntade intäkter per kund per månad**

* Mått `A`: `Revenue (hide)`
   * `Calendar months between first order and this order` `<= X` (Välj ett rimligt tal för X, till exempel 24 månader)
   * `Is in current month?` = `No`

* 
   [!UICONTROL-mått]: `Revenue`
* [!UICONTROL Filter]:

* Mått `B`: `All time customers (hide)`
   * `Is in current month?` = `No`

* [!UICONTROL Metric]: `New customers by first order date`
* [!UICONTROL Filter]:

* Mått `C`: `All time customers by month since first order (hide)`
   * `Calendar months since order` `<= X`
   * `Is in current month?` = `No`

* [!UICONTROL Metric]: `New customers by first order date`
* [!UICONTROL Filter]:

* [!UICONTROL Formula]: `Expected revenue`
* [!UICONTROL Formula]: `A / (B - C)`
* 

   [!UICONTROL Format]: `Currency`

Annan diagraminformation

* [!UICONTROL Time period]: `All time`
* Tidsintervall: `None`
* [!UICONTROL Group by]: `Calendar months between first order and this order` - visa alla
* Ändra `group by` för `All time customers` metrisk till oberoende med pennikonen bredvid `group by`
* Redigera `Show top/bottom` fält enligt följande:
   * [!UICONTROL Revenue]: `Top 24 sorted by Calendar months between first order and this order`
   * [!UICONTROL All time customers]: `Top 24 sorted by All time customers`
   * [!UICONTROL All time customers by month since first order]: `Top 24 sorted by All time customers by month since first order`

**Genomsnittlig intäkt per månad per kohort**

* Mått `A`: `Revenue`
* 
   [!UICONTROL Metric view]: `Cohort`
* [!UICONTROL Cohort date]: `Customer's first order date`
* [!UICONTROL Perspective]: `Average value per cohort member`

**Ackumulerade genomsnittliga intäkter per månad per kohort**

* Mått `A`: `Revenue`
* 
   [!UICONTROL Metric view]: `Cohort`
* [!UICONTROL Cohort date]: `Customer's first order date`
* [!UICONTROL Perspective]: `Cumulative average value per cohort member`

När du har kompilerat alla rapporter kan du ordna dem på kontrollpanelen som du vill. Resultatet kan se ut som bilden överst på sidan.

Om du stöter på några frågor när du skapar den här analysen eller bara vill engagera Professional Services-teamet, [kontakta support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
