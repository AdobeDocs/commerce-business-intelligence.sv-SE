---
title: Commerce Churn
description: Lär dig hur du genererar och analyserar din Commerce Churn-kurs.
exl-id: 8775cf0a-114d-4b48-8bd2-fc1700c59a12
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 2%

---

# Kurvfrekvens

I det här avsnittet visas hur du beräknar en **bortfallstakt** för **e-handelskunder**. Till skillnad från SaaS och traditionella prenumerationsföretag har e-handelskunder vanligtvis ingen konkreta **&quot;churn event&quot;** för att visa att de inte längre ska räknas med i era aktiva kunder. Av den anledningen kan du med instruktionerna nedan definiera en kund som&quot;efterfrågad&quot; baserat på den tid som gått sedan den senaste ordern.

![](../../assets/Churn_rate_image.png)

Många kunder vill ha hjälp med att börja förstå vad **tidsram** de bör använda baserat på sina uppgifter. Om du vill använda historiska kundbeteenden för att definiera detta **tidsram för bortfall** kan du bekanta dig med [definiera kurva](../analysis/define-cust-churn.md) ämne. Sedan kan du använda resultatet i formeln för bortfallsfrekvens i instruktionerna nedan.

## Beräknade kolumner

Kolumner att skapa

* **`customer_entity`** table
* **`Customer's last order date`**
   * Välj en [!UICONTROL definition]: `Max`
   * Välj [!UICONTROL table]: `sales_flat_order`
   * Välj [!UICONTROL column]: `created_at`
   * `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]: `Orders we count`

* **`Seconds since customer's last order date`**
   * Välj en [!UICONTROL definition]: `Age`
   * Välj [!UICONTROL column]: `Customer's last order date`

>[!NOTE]
>
>Se till att [lägga till alla nya kolumner som dimensioner till mått](../data-warehouse-mgr/manage-data-dimensions-metrics.md) innan du skapar nya rapporter.

## Mått

* **Nya kunder (efter första orderdatum)**
   * Räknade kunder

>[!NOTE]
>
>Detta mått kan finnas på ditt konto.

* I **`customer_entity`** table
* Det här måttet utför en **Antal**
* På **`entity_id`** kolumn
* Beställd av **`Customer's first order date`** tidsstämpel
* [!UICONTROL Filter]:

* **Nya kunder (efter sista orderdatum)**
   * Räknade kunder

  >[!NOTE]
  >
  >Detta mått kan finnas på ditt konto.

* I **`customer_entity`** table
* Det här måttet utför en **Antal**
* På **`entity_id`** kolumn
* Beställd av **`Customer's last order date`** tidsstämpel
* [!UICONTROL Filter]:

>[!NOTE]
>
>Se till att [lägga till alla nya kolumner som dimensioner till mått](../data-warehouse-mgr/manage-data-dimensions-metrics.md) innan du skapar nya rapporter.

## Rapporter

* **Kurvfrekvens**
   * [!UICONTROL Metric]: Nya kunder (efter första orderdatum)
   * [!UICONTROL Filter]: `Lifetime number of orders Greater Than 0`
   * 
     [!UICONTROL Perspective]: `Cumulative`
   * [!UICONTROL Metric]: `New customers (by last order date)`
   * [!UICONTROL Filter]:
   * Sekunder sedan kundens senaste orderdatum >= [En självdefinierad klippgräns för kunder som blivit bortskurna ]**`^`**
   * `Lifetime number of orders Greater Than 0`

   * [!UICONTROL Metric]: `New customers (by last order date)`
   * [!UICONTROL Filter]: `Lifetime number of orders Greater Than 0`
   * 
     [!UICONTROL Perspective]: Cumulative
   * [!UICONTROL Formula]: `(B / ((A + B) - C)`
   * 
     [!UICONTROL Format]: Percentage

* *Mått `A`:`New customers cumulative`*
* *Mått `B`:`Churned customers by last order date`*
* *Mått `C`:`Customers by last order date cumulative`*
* *`Formula`:`Repeat order probability`*
* *`Time period`:`All time (or custom range)`*
* *`Group by`:`Customer's order number`*
* *`Chart Type`:`Column`*

Nedan finns några vanliga konverteringar för månad > sekund, men Google innehåller andra värden, inklusive konverteringar för vecka > sekunder för anpassade värden som du kanske letar efter.

| **Månader** | **Sekunder** |
|---|---|
| 3 | 7,776,000 |
| 6 | 15,552,000 |
| 9 | 23,328,000 |
| 12 | 31,104,000 |

När du har kompilerat alla rapporter kan du ordna dem på kontrollpanelen som du vill. Resultatet kan se ut som kontrollpanelen ovan.
