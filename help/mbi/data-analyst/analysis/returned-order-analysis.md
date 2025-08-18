---
title: Analyserar returnerade order
description: Lär dig hur du konfigurerar en kontrollpanel som ger en detaljerad analys av butikernas intäkter.
exl-id: 6a948561-45b7-4813-9661-ab42197ca5bd
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# Returnerade order

I det här avsnittet visas hur du konfigurerar en kontrollpanel som innehåller en detaljerad analys av butikens resultat.

![](../../assets/detailed-returns-dboard.png)

Innan du börjar måste du vara [Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html)-kund och se till att ditt företag använder tabellen `enterprise\_rma` för returer.

Den här analysen innehåller [avancerade beräknade kolumner](../data-warehouse-mgr/adv-calc-columns.md).

## Komma igång

Kolumner att spåra

* **`enterprise_rma`** eller **`rma`**-tabell
* **`entity_id`**
* **`status`**
* **`order_id`**
* **`customer_id`**
* **`date_requested`**

* **`enterprise_rma_item_entity`** eller **`rma_item_entity`**-tabell
* **`entity_id`**
* **`rma_entity_id`**
* **`qty_returned`**
* **`status`**
* **`order_item_id`**
* **`product_name`**
* **`product_sku`**

Filteruppsättningar att skapa

* **`enterprise_rma`**-tabell
* Filteruppsättningsnamn: `Returns we count`
* Filteruppsättningslogik:
   * Platshållare - ange din egna logik här

* **`enterprise_rma_item_entity`**-tabell
* Filteruppsättningsnamn: `Returns items we count`
* Filteruppsättningslogik:
   * Platshållare - ange din egna logik här

### Beräknade kolumner

Kolumner att skapa

* **`enterprise_rma`**-tabell
* **`Order's created at`**
* Välj en definition: `Joined Column`
* [!UICONTROL Create Path]:
* &#x200B;
  [!UICONTROL Many]: `enterprise_rma.order_id`
* &#x200B;
  [!UICONTROL One]: `sales_flat_order.entity_id`

* Välj en [!UICONTROL table]: `sales_flat_order`
* Välj en [!UICONTROL column]: `created_at`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's order number`**
* Välj en definition: `Joined Column`
* Välj en [!UICONTROL table]: `sales_flat_order`
* Välj en [!UICONTROL column]: `Customer's order number`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Time between order's created_at and date_requested`** skapas av en analytiker som en del av din `[RETURNS ANALYSIS]`-biljett

* **`enterprise_rma_item_entity`**-tabell
* **`return_date_requested`**
* Välj en definition: `Joined Column`
* [!UICONTROL Create Path]:
   * &#x200B;
     [!UICONTROL Many]: `enterprise_rma_item_entity.rma_entity_id`
   * &#x200B;
     [!UICONTROL One]: `enterprise_rma.entity_id`

* Välj en [!UICONTROL table]: `enterprise_rma`
* Välj en [!UICONTROL column]: `date_requested`
   * `enterprise_rma_item_entity.rma_entity_id = enterprise_rma.entity_id`

* **`Return item total value (qty_returned * price)`** skapas av en analytiker som en del av din `[RETURNS ANALYSIS]`-biljett

* **`sales_flat_order`**-tabell
* **`Order contains a return? (1=yes/0=No)`**
* Välj en definition: `Exists`
* Välj en [!UICONTROL table]: `enterprise_rma`
   * `enterprise_rma.order_id = sales_flat_order.entity_id`

* **`Customer's previous order number`** skapas av en analytiker som en del av din `[RETURNS ANALYSIS]`-biljett
* **`Customer's previous order contains return? (1=yes/0=no)`** skapas av en analytiker som en del av din `[RETURNS ANALYSIS]`-biljett

>[!NOTE]
>
>Om du bara är intresserad av att analysera arbetstider för sekunder till upplösning eller sekunder till första svar, ska du meddela analytikern när du begär biljetten.

### Mått

* **Returnerar**
* I tabellen **`enterprise_rma`**
* Detta mått utför ett **antal**
* I kolumnen **`entity_id`**
* Beställd av **`date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **Returnerade objekt**
* I tabellen **`enterprise_rma_item_entity`**
* Detta mått utför en **summa**
* I kolumnen **`qty_approved`**
* Beställd av **`return date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **Returnerat artikeltotalvärde**
* I tabellen **`enterprise_rma_item_entity`**
* Detta mått utför en **summa**
* I kolumnen **`Returned item total value (qty_returned * price)`**
* Beställd av **`return date_requested`**
* [!UICONTROL Filter]: `Returns we count`

* **Genomsnittlig tid mellan beställning och retur**
* I tabellen **`enterprise_rma`**
* Det här måttet utför ett **genomsnitt**
* I kolumnen **`Time between order's created_at and date_requested`**
* Beställd av **`date_requested`**
* [!UICONTROL Filter]: `Returns we count`

>[!NOTE]
>
>Se till att [lägga till alla nya kolumner som mått i mätvärden](../data-warehouse-mgr/manage-data-dimensions-metrics.md) innan du skapar nya rapporter.

### Rapporter

* **Sannolikhet för upprepade order efter att en retur har gjorts**
* Mått `A`: `Number of orders with returns`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Order contains a return? (1=yes/0=No) = 1`
   * `Is in current month? = No`

* Mått `B`: `Non-last orders with returns`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Is customer's last order? (1=yes/0=no) = 0`
   * `Order contains a return? (1=yes/0=No) = 1`

* Formel: Sannolikhet för upprepad ordning
* [!UICONTROL Formula]: `B / A`
* &#x200B;
  [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL -intervall]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* &#x200B;
  [!UICONTROL -diagramtyp]: `Bar`

* **Genomsnittlig tid för att returnera (hela tiden)**
* Mått `A`: `Avg time between order and return`
* [!UICONTROL Metric]: `Avg time between order and return`

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL -intervall]: `None`
* &#x200B;
  [!UICONTROL -diagramtyp]: `Number`

* **Procent av order med returvärde**
* Mått `A`: `Number of orders`
* [!UICONTROL Metric]: `Number of orders`

* Mått `B`: `Orders w/ return`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Order contains a return? (1=yes/0=No) = 1`

* Formel: % av order med returrätt
* [!UICONTROL Formula]: `B / A`
* &#x200B;
  [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL -intervall]: `None`
* [!UICONTROL Chart Type]: `Number - % of orders with return`

* **Intäkter som returneras per månad**
* Mått `A`: `Returned item total value`
* [!UICONTROL Metric]: `Returned item total value`

* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By month`
* &#x200B;
  [!UICONTROL -diagramtyp]: `Line`

* **Kunder som har gjort returer och inte köpt igen**
* Mått `A`: `Number of orders with returns`
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:
   * `Order contains a return? (1=yes/0=No) = 1`
   * `Is customer's last order? (1=yes/0=no) = 1`

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL -intervall]: `None`
* &#x200B;
  [!UICONTROL Group by]: `Customer_email`
* &#x200B;
  [!UICONTROL -diagramtyp]: `Table`

* **Returhastighet per objekt**
* Mått `A`: `Returned items` (Dölj)
* [!UICONTROL Metric]: Returnerade artiklar

* Mått `B`: `Items sold` (Dölj)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]:

* [!UICONTROL Formula]: `Return %`
* [!UICONTROL Formula]: `B / A`
* &#x200B;
  [!UICONTROL Format]: `Percentage`

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL -intervall]: `None`
* [!UICONTROL Group by]: `product_sku AND/OR product_name`
* &#x200B;
  [!UICONTROL -diagramtyp]: `Table`

När du har kompilerat alla rapporter kan du ordna dem på kontrollpanelen som du vill. Resultatet kan se ut som kontrollpanelen ovan.

[Kontakta support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=sv-SE) om du får frågor när du skapar den här analysen eller vill engagera Professional Services-teamet.
