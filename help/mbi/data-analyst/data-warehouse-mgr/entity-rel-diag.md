---
title: Entitetsrelationsdiagram
description: Lär dig mer om några ER-diagram som hjälper dig att visualisera relationen mellan en handfull vanliga Commerce-databastabeller.
exl-id: de7d419f-efbe-4d0c-95a8-155a12aa93f3
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '319'
ht-degree: 0%

---

# Entitetsrelationsdiagram

Vad är en **[!UICONTROL entity relationship (ER) diagram]**? An `ER` diagram är en visualisering av tabeller i en databas och hur de relaterar till varandra. Den här artikeln innehåller några ER-diagram som hjälper dig att visualisera relationen mellan en handfull vanliga Commerce-databastabeller.

>[!NOTE]
>
>I den här artikeln ser du orden **join**, **relation** och **bana**. De här orden används för att beskriva hur två tabeller är sammankopplade.

## Kärnhandel `ER` Diagram

![4_DB_Chart](../../assets/4_DB_Chart.png)

Detta `ER` diagram representerar relationerna mellan huvudtabellerna i en Commerce-databas. Genom att visa flera relationer samtidigt kan du se hur data skulle kunna relateras i flera tabeller.

Avsnitten nedan innehåller `ER` diagram som är specifika för två tabeller i taget. Om du vill visa ett diagram och tillhörande beskrivning klickar du på rubriken för det avsnittet.

## `customer\_entity & sales\_flat\_order`

![En kund beställer många](../../assets/2_OneCustomerManyOrders.png)

En kund kan göra många beställningar. Relationen mellan de här två tabellerna är `customer\_entity.entity\_id = sales\_flat\_order.customer\_id`

>[!IMPORTANT]
>
>`customer\_entity.entity\_id` är inte lika med `sales\_flat\_order.entity\_id`. Den första kan man tänka sig som en `customer\_id` och den andra kan man tänka sig som `order\_id.`

Inom [!DNL MBI]om sökvägen mellan de två tabellerna inte finns kan du [skapa banan](../data-warehouse-mgr/create-paths-calc-columns.md) på fliken Data warehouse. När du är redo att skapa banan definieras den så här:

![](../../assets/SFO___CE_path.png)

## `sales\_flat\_order & sales\_flat\_order\_item`

![1_OneOrderManyItems](../../assets/1_OneOrderManyItems.png)

En order kan innehålla många artiklar. Relationen mellan de här två tabellerna är `sales\_flat\_order.entity\_id = sales\_flat\_order\_item.order\_id`.

Inom [!DNL MBI]om sökvägen mellan de två tabellerna inte finns kan du [skapa banan](../data-warehouse-mgr/create-paths-calc-columns.md) på fliken Data warehouse. När du är redo att skapa banan definieras den så här:

![](../../assets/SFOI___SFO_path.png)

## `catalog\_product\_entity & sales\_flat\_order\_item`

![3_OneProductManyTimes](../../assets/3_OneProductManyTimes.png)

En produkt kan köpas för många artiklar. Relationen mellan de här två tabellerna är `catalog\_product\_entity.entity\_id = sales\_flat\_order\_item.product`.

Inom [!DNL MBI]om sökvägen mellan de två tabellerna inte finns kan du [skapa banan](../data-warehouse-mgr/create-paths-calc-columns.md) på fliken Data warehouse. När du är redo att skapa banan definieras den så här:

![](../../assets/SFOI___CPE_path.png)
