---
title: Analyserar lagernivåer
description: Lär dig hur du analyserar lagernivåer.
exl-id: 620156c5-7bea-4b36-84c7-e0cb4b5cc8be
role: Admin, Data Architect, Data Engineer, User
feature: Dashboards, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# Analysera lagernivåer

I det här avsnittet visas hur du konfigurerar en instrumentpanel som ger insikter om ditt nuvarande lager och innehåller instruktioner för kunder om både den äldre arkitekturen eller den nya arkitekturen. Du använder den äldre arkitekturen om du inte har alternativet **[!UICONTROL Data Warehouse Views]** på menyn **[!UICONTROL Manage Data]**. Om du har en äldre arkitektur skickar du en [ny supportförfrågan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=sv-SE) med ämnet **[!UICONTROL INVENTORY ANALYSIS]** när du har nått det avsedda avsnittet i instruktionerna för _Beräknade kolumner_ nedan.

## Kolumner att spåra:

### Kolumner som spårar instruktioner

* **[!UICONTROL cataloginventory_stock_item]**-tabell:
   * **`item_id`**
   * **`product_id`**
   * **`qty`**

* **[!UICONTROL catalog_product_entity]**-tabell:
   * **`entity_id`**
   * **`sku`**
   * **`created_at`**

## Beräknade kolumner:

+++ Ny arkitektur

* **[!UICONTROL catalog_product_entity]**-tabell:
   * **`Product's most recent order date`**
      * [!UICONTROL Column type]: `Many to One`
      * &#x200B;
        [!UICONTROL Column equation]: `MAX`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Välj en [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Product's first order date`**
      * [!UICONTROL Column type]: `Many to One`
      * &#x200B;
        [!UICONTROL Column equation]: `MIN`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Välj en [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `Same Table`
      * &#x200B;
        [!UICONTROL Column equation]: `AGE`
      * Välj [!UICONTROL DATETIME column]: `Product's most recent order date`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `Many to One`
      * &#x200B;
        [!UICONTROL Column equation]: `SUM`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Välj en [!UICONTROL column]: `qty_ordered`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `Same Table`
      * &#x200B;
        [!UICONTROL Column equation]: `CALCULATION`
      * [!UICONTROL Column] indata:
         * A: `Product's lifetime number of items sold`
         * B: `Product's first order date`
      * &#x200B;
        [!UICONTROL Datatype]: `Decimal`
      * Definition:
         * case when A is null or B is null else round(A::decimal/(extract(epoch from (current_timestamp - B))::decimal/604800.0),2) end

* **[!UICONTROL cataloginventory_stock_item]**-tabell:
   * **`Sku`**
      * [!UICONTROL Column type]: `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Välj en [!UICONTROL column]: `sku`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Välj en [!UICONTROL column]: `Product's lifetime number of items sold`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Välj en [!UICONTROL column]: `Seconds since product's most recent order date`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Välj en [!UICONTROL column]: `Avg products sold per week (all time)`

   * **`Weeks on hand`**
      * [!UICONTROL Column type]: `Same Table`
      * &#x200B;
        [!UICONTROL Column equation]: `CALCULATION`
      * [!UICONTROL Column] indata:
         * A: `qty`
         * B: `Avg products sold per week (all time)`
      * &#x200B;
        [!UICONTROL Datatype]: `Decimal`
      * Definition:
         * case when A is null or B is null or B = 0.0, then null else round(A::decimal/B,2) end

+++
+++ Äldre arkitektur

* **[!UICONTROL catalog_product_entity]**-tabell:
   * **`Product's most recent order date`**
      * [!UICONTROL Column type]: `Many to One`
      * &#x200B;
        [!UICONTROL Column equation]: `MAX`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Välj en [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Product's first order date`**
      * [!UICONTROL Column type]: `Many to One`
      * &#x200B;
        [!UICONTROL Column equation]: `MIN`
      * [!UICONTROL Path]: `sales_order_item.product_id => catalog_product_entity.entity_id`
      * Välj en [!UICONTROL column]: `created_at`
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `Same Table`
      * &#x200B;
        [!UICONTROL Column equation]: `AGE`
      * Välj DATETIME-kolumn: **`Product's most recent order date`**

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `Many to One`
      * &#x200B;
        [!UICONTROL Column equation]: `SUM`
      * [!UICONTROL Path]: **`sales_order_item.product_id => catalog_product_entity.entity_id`**
      * Välj en [!UICONTROL column]: **`qty_ordered`**
      * [!UICONTROL Filters]:
         * [A] `Ordered products we count`

   * **`Avg products sold per week (all time)`**
      * Skapas av en analytiker när du skickar din **[INVENTORY ANALYSIS]** -supportförfrågan

* **[!UICONTROL cataloginventory_stock_item]**-tabell:
   * **`Sku`**
      * [!UICONTROL Column type]: `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Välj en [!UICONTROL column]: `sku`

   * **`Product's lifetime number of items sold`**
      * [!UICONTROL Column type]: `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Välj en [!UICONTROL column]: `Product's lifetime number of items sold`

   * **`Seconds since product's most recent order date`**
      * [!UICONTROL Column type]: `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Välj en [!UICONTROL column]: `Seconds since product's most recent order date`

   * **`Avg products sold per week (all time)`**
      * [!UICONTROL Column type]: `One to Many`
      * &#x200B;
        [!UICONTROL Column equation]: `JOINED_COLUMN`
      * [!UICONTROL Path]: `cataloginventory_stock_item.product_id => catalog_product_entity.entity_id`
      * Välj en [!UICONTROL column]: `Avg products sold per week (all time)`

   * **`Weeks on hand`**
      * Skapas av en analytiker när du skickar din **[!UICONTROL INVENTORY ANALYSIS]**-supportförfrågan

+++

## Mått

### Mätinstruktioner

* **[!UICONTROL cataloginventory_stock_item]**-tabell:
   * **`Inventory on hand`**: det här måttet utför en
      * **Summa** på
      * **`qty`** kolumn sorterad efter
      * [Ingen]-kolumn

## Rapporter

### Rapportinstruktioner

* **`Inventory on hand by sku`**
   * [!UICONTROL Metric]: `Inventory on hand`
   * [!UICONTROL Time period]: `All time`
   * Tidsintervall: `None`
   * [!UICONTROL Group by]:
      * `Sku`
      * `Weeks on hand`
   * &#x200B;
     [!UICONTROL Chart type]: `Table`

* **`Inventory with less than 2 weeks on hand (order now)`**
   * [!UICONTROL Metric]: `Inventory on hand`
      * [!UICONTROL Filters]:
         * [A] `Weeks on hand` `< 2`

   * [!UICONTROL Time period]: `All time`
   * Tidsintervall: `None`
   * &#x200B;
     [!UICONTROL Group by]: `Sku`
   * &#x200B;
     [!UICONTROL Chart type]: `Table`

* **`Inventory with more than 26 weeks on hand (put on sale)`**
   * [!UICONTROL Metric]: `Inventory on hand`
      * [!UICONTROL Filters]:
         * [A] `Weeks on hand` `> 26`

   * [!UICONTROL Time period]: `All time`
   * Tidsintervall: `None`
   * &#x200B;
     [!UICONTROL Group by]: `Sku`
   * &#x200B;
     [!UICONTROL Chart type]: `Table`

[Kontakta support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=sv-SE) om du får frågor under arbetet med att skapa den här analysen, eller om du bara vill engagera Professional Services-teamet.
