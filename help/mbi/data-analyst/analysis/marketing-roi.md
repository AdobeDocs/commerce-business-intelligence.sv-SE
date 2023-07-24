---
title: Marknadsföringsavkastning
description: Lär dig hur du konfigurerar en kontrollpanel som spårar din kanalanalys, inklusive avkastning på investering i aggregat och per kampanj.
exl-id: 5de83998-e6cf-478d-bb6a-7a3dc77c2c0c
role: Admin,  User
feature: Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---

# Marknadsföringsavkastning

>[!NOTE]
>
>Det här avsnittet innehåller instruktioner för klienter som använder den ursprungliga arkitekturen och den nya arkitekturen. Du är på [ny arkitektur](../../administrator/account-management/new-architecture.md) om du har delen &quot;Vyer i Data warehouse&quot; tillgänglig efter att du har valt &quot;Hantera data&quot; i huvudverktygsfältet.

Om ni spenderar pengar på onlinereklam vill ni följa upp er avkastning på dessa utgifter och fatta datadrivna beslut om ytterligare investeringar. I det här avsnittet visas hur du konfigurerar en kontrollpanel som spårar din kanalanalys, inklusive avkastning på investering i aggregat och per kampanj.

![](../../assets/Marketing_dashboard_example.png)

Innan du börjar vill du ansluta [!DNL [Facebook Ads]](../importing-data/integrations/facebook-ads.md), [!DNL [Adwords]](../importing-data/integrations/google-adwords.md)och [!DNL [Google Ecommerce]](../importing-data/integrations/google-ecommerce.md) konton och ta in ytterligare annonsinformation online. Denna analys innehåller [avancerade beräknade kolumner](../data-warehouse-mgr/adv-calc-columns.md).

## Konsoliderade tabeller

**Ursprunglig arkitektur:** för att samla era utgifter från olika källor, som [!DNL Facebook Ads] eller [!DNL Google Adwords], Adobe rekommenderar att du skapar en **konsoliderad tabell** av alla era annonskostnader. Du behöver en analytiker som slutför det här steget åt dig. Om du inte har gjort det, [arkivera en supportförfrågan](../../guide-overview.md#Submitting-a-Support-Ticket) med motivet `[MARKETING ROI ANALYSIS]`och en analytiker skapar tabellen.

**Ny arkitektur:** Du kan följa exemplet i [det här analysbiblioteket](../../data-analyst/data-warehouse-mgr/create-dw-views.md) ämne. Konsoliderade tabeller kallas nu Data warehouse-vyer för den nya arkitekturen.

## Beräknade kolumner

Kolumner att skapa

* **`Consolidated Digital Ad Spend`** table
* **`Campaign name`** har skapats av en Adobe-analytiker som en del av **[AVKASTNING PÅ MARKNADSFÖRING]** biljett

**Ursprungliga och nya arkitekturer:**

* **`sales_flat_order`** table
   * **`Order's GA campaign`**
      * Välj en definition: `Joined Column`
      * [!UICONTROL Create Path]:
      * 
        [!UICONTROL Many]: `sales_flat_order.increment_id`
      * 
        [!UICONTROL One]: `ecommerce####.transaction_id`

      * Välj en [!UICONTROL table]: `ecommerce####`
      * Välj en [!UICONTROL column]: `campaign`
      * [!UICONTROL Path]: `sales_flat_order.increment_id = ecommerce#####.transactionID`

   * **`Order's GA medium`**
      * Välj en definition: Ansluten kolumn
      * Välj en [!UICONTROL table]: `ecommerce####`
      * Välj en [!UICONTROL column]: `medium`
      * [!UICONTROL Path]: sales_flat_order.increment_id = ecommerce###.transactionId

   * **`Order's GA source`**
      * Välj en definition: Ansluten kolumn
      * Välj en [!UICONTROL table]: `ecommerce####`
      * Välj en [!UICONTROL column]: `source`
      * [!UICONTROL Path]: sales_flat_order.increment_id = ecommerance###.transactionId ^

* **`customer_entity`** table
* **`Customer's first order GA campaign`**
   * Välj en definition: `Max`
   * Välj en [!UICONTROL table]: `sales_flat_order`
   * Välj en [!UICONTROL column]: `Order's GA campaign`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`Customer's first order GA source`**
   * Välj en definition: `Max`
   * Välj en [!UICONTROL table]: `sales_flat_order`
   * Välj en [!UICONTROL column]: `Order's GA source`
   * [!UICONTROL Path]: sales_flat_order.customer_id = customer_entity.entity_id
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`Customer's first order GA medium`**
   * Välj en definition: `Max`
   * Välj en [!UICONTROL table]: `sales_flat_order`
   * Välj en [!UICONTROL column]: `Order's GA medium`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
   * [!UICONTROL Filter]:
      * `Orders we count`
      * `Customer's order number = 1`

* **`sales_flat_order`** table
* **`Customer's first order GA campaign`**
   * Välj en definition: `Joined Column`
   * Välj en [!UICONTROL table]: `customer_entity`
   * Välj en [!UICONTROL column]: `Customer's first order GA campaign`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA source`**
   * Välj en definition: Ansluten kolumn
   * Välj en [!UICONTROL table]: `customer_entity`
   * Välj en [!UICONTROL column]: `Customer's first order GA source`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

* **`Customer's first order GA medium`**
   * Välj en definition: `Joined Column`
   * Välj en [!UICONTROL table]: `customer_entity`
   * Välj en [!UICONTROL column]: `Customer's first order GA medium`
   * [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`

## Mått

* **Annonsutgift**
* I **`Consolidated Digital Ad Spend`** table
* Detta mått utför en **Summa**
* På **`adCost`** kolumn
* Beställd av **`date`** tidsstämpel

* **Annonsvisningar**
* I **`Consolidated Digital Ad Spend`** table
* Detta mått utför en **Summa**
* På **`Impressions`** kolumn
* Beställd av **`Month`** tidsstämpel

* **Lägg till klick**
* I **`Consolidated Digital Ad Spend`** table
* Detta mått utför en **Summa**
* På **`adClicks`** kolumn
* Beställd av **`Month`** tidsstämpel

>[!NOTE]
>
>Se till att [lägga till alla nya kolumner som dimensioner till mått](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) innan du skapar nya rapporter.

## Rapporter

* **Annonsutgift (hela tiden)**
   * [!UICONTROL Metric]: Annonskostnader

* Mått `A`: Annonskostnader
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL-intervall]: `None`
* 
  [!UICONTROL Chart Type]: `Scalar`

* **Annonsköp av kunder (hela tiden)**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Filterlogik: ([`A`] ELLER [`B`] ELLER [`C`]) OCH [`D`]

* Mått `A`: `Ad customer acquisitions`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL-intervall]: `None`
* 
  [!UICONTROL Chart Type]: `Scalar`

* **Annonsavkastning**
   * [!UICONTROL Metric]: Annonskostnader

   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Filterlogik: ([`A`] ELLER [`B`] ELLER [`C`]) OCH [`D`]

   * [!UICONTROL Metric]: Genomsnittlig intäkt för livstid
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Filterlogik: ([`A`] ELLER [`B`] ELLER [`C`]) OCH [`D`]

   * [!UICONTROL Formula]: `((C - (A / B)) / (A / B))`
   * 
     [!UICONTROL Format]: `Percentage`

* Mått `A`: `Ad Spend (hide)`
* Mått `B`: `Ad customer acquisitions (hide)`
* Mått `C`: `Average LTV (hide)`
* [!UICONTROL Formula]: `Ads ROI`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL-intervall]: `None`
* 
  [!UICONTROL Chart Type]: `Scalar`

* **Beställningar per gastorlek**
   * 
     [!UICONTROL-mått]: `Orders`

* Mått `A`: `Orders`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By Month`
* [!UICONTROL Group by]: `Order's medium`
* 
  [!UICONTROL Chart Type]: `Area`

* **Annonsavkastning per kampanj**
   * [!UICONTROL Metric]: `Ad Spend`

   * [!UICONTROL Metric]:`New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Filterlogik: ([`A`] ELLER [`B`] ELLER [`C`]) OCH [`D`]

   * [!UICONTROL Metric]: Genomsnittlig intäkt för livstid
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Filterlogik: ([`A`] ELLER [`B`] ELLER [`C`]) OCH [`D`]

   * [!UICONTROL Metric]: Genomsnittligt antal order för livslängd
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Filterlogik: ([`A`] ELLER [`B`] ELLER [`C`]) OCH [`D`]

   * [!UICONTROL Formula]: `(A / B)`
   * 
     [!UICONTROL Format]: `Currency`

   * [!UICONTROL Formula]: `(C - (A / B))`
   * 
     [!UICONTROL Format]: `Currency`

   * [!UICONTROL Formula]: `((C - (A / B)) / (A / B))`
   * 
     [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Metric]: `Ad Clicks`

   * [!UICONTROL Metric]: `Ad Impressions`

   * [!UICONTROL Formula]: `(H / I)`
   * 
     [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Formula]: `(A / H)`
   * 
     [!UICONTROL Format]: `Currency`

* Mått `A`: `Ad Spend` (dölj)
* Mått `B`: `Ad customer acquisitions`
* Mått `C`: `Average LTV`
* Mått `D`: `Average lifetime # of orders`
* 
  [!UICONTROL-formel]: `CAC`
* [!UICONTROL Formula]: `Avg return`
* [!UICONTROL Formula]: `Ads ROI`
* Mått `H`: `adClicks`
* Mått `I`: `Impressions`
* 
  [!UICONTROL-formel]: `CTR`
* 
  [!UICONTROL-formel]: `CPC`
* [!UICONTROL Time period]: `All time`
* 
  [!UICONTROL-intervall]: `None`
* 
  [!UICONTROL Group by]: `campaign` (Använd kundens första beställningskampanj för statistik över icke-annonsutgifter)
* 
  [!UICONTROL Chart Type]: `Table`

Om du stöter på några frågor när du skapar den här analysen eller bara vill engagera Professional Services-teamet, [kontakta support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

### Relaterad

* [De bästa metoderna för UTM-taggning i [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
* [Hur [!DNL Google Analytics] UTM-attribueringsarbete?](../analysis/utm-attributes.md)
