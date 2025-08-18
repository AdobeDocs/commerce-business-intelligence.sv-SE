---
title: Marknadsföringsavkastning
description: Lär dig hur du konfigurerar en kontrollpanel som spårar din kanalanalys, inklusive avkastning på investering i aggregat och per kampanj.
exl-id: 5de83998-e6cf-478d-bb6a-7a3dc77c2c0c
role: Admin,  User
feature: Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# Marknadsföringsavkastning

>[!NOTE]
>
>Det här avsnittet innehåller instruktioner för klienter som använder den ursprungliga arkitekturen och den nya arkitekturen. Du finns på den [nya arkitekturen](../../administrator/account-management/new-architecture.md) om du har avsnittet&quot;Data Warehouse-vyer&quot; tillgängligt när du har valt&quot;Hantera data&quot; i huvudverktygsfältet.

Om ni spenderar pengar på onlinereklam vill ni följa upp er avkastning på dessa utgifter och fatta datadrivna beslut om ytterligare investeringar. I det här avsnittet visas hur du konfigurerar en kontrollpanel som spårar din kanalanalys, inklusive avkastning på investering i aggregat och per kampanj.

![](../../assets/Marketing_dashboard_example.png)

Innan du börjar vill du ansluta dina [[!DNL [Facebook Ads]]](../importing-data/integrations/facebook-ads.md)-, [[!DNL [Adwords]]](../importing-data/integrations/google-adwords.md)- och [[!DNL [Google Ecommerce]]](../importing-data/integrations/google-ecommerce.md)-konton och hämta ytterligare annonsutgiftsdata online. Den här analysen innehåller [avancerade beräknade kolumner](../data-warehouse-mgr/adv-calc-columns.md).

## Konsoliderade tabeller

**Ursprunglig arkitektur:** Adobe rekommenderar att du skapar en [!DNL Facebook Ads]konsoliderad tabell[!DNL Google Adwords] av alla dina annonskostnader för att samla dina utgifter från olika källor, som **eller**. Du behöver en analytiker som slutför det här steget åt dig. Om du inte har gjort det [skickar du en supportförfrågan](../../guide-overview.md#Submitting-a-Support-Ticket) med ämnet `[MARKETING ROI ANALYSIS]` och en analytiker skapar tabellen.

**Ny arkitektur:** Du kan följa exemplet i [det här analysbibliotekets](../../data-analyst/data-warehouse-mgr/create-dw-views.md) avsnitt. Konsoliderade tabeller kallas nu Data Warehouse Views för den nya arkitekturen.

## Beräknade kolumner

Kolumner att skapa

* **`Consolidated Digital Ad Spend`**-tabell
* **`Campaign name`** har skapats av en Adobe-analytiker som en del av din **[MARKNADSFÖRING av ROI-ANALYS]**-biljett

**Ursprungliga och nya arkitekturer:**

* **`sales_flat_order`**-tabell
   * **`Order's GA campaign`**
      * Välj en definition: `Joined Column`
      * [!UICONTROL Create Path]:
      * &#x200B;
        [!UICONTROL Many]: `sales_flat_order.increment_id`
      * &#x200B;
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
      * [!UICONTROL Path]: sales_flat_order.increment_id = ecommerce###.transactionId
^

* **`customer_entity`**-tabell
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

* **`sales_flat_order`**-tabell
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
* I tabellen **`Consolidated Digital Ad Spend`**
* Detta mått utför en **summa**
* I kolumnen **`adCost`**
* Ordnad efter tidsstämpeln **`date`**

* **Lägg till avtryck**
* I tabellen **`Consolidated Digital Ad Spend`**
* Detta mått utför en **summa**
* I kolumnen **`Impressions`**
* Ordnad efter tidsstämpeln **`Month`**

* **Lägg till klick**
* I tabellen **`Consolidated Digital Ad Spend`**
* Detta mått utför en **summa**
* I kolumnen **`adClicks`**
* Ordnad efter tidsstämpeln **`Month`**

>[!NOTE]
>
>Se till att [lägga till alla nya kolumner som mått i mätvärden](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) innan du skapar nya rapporter.

## Rapporter

* **Annonsering (hela tiden)**
   * [!UICONTROL Metric]: Annonsutgift

* Mått `A`: Annonsutgift
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL -intervall]: `None`
* &#x200B;
  [!UICONTROL Chart Type]: `Scalar`

* **Lägg till kundförvärv (hela tiden)**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Filterlogik: ([`A`] ELLER [`B`] ELLER [`C`]) OCH [`D`]

* Mått `A`: `Ad customer acquisitions`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL -intervall]: `None`
* &#x200B;
  [!UICONTROL Chart Type]: `Scalar`

* **Annonsera ROI**
   * [!UICONTROL Metric]: Annonsutgift

   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Filterlogik: ([`A`] ELLER [`B`] ELLER [`C`]) OCH [`D`]

   * [!UICONTROL Metric]: Inkomster för genomsnittlig livstid
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Filterlogik: ([`A`] ELLER [`B`] ELLER [`C`]) OCH [`D`]

   * [!UICONTROL Formula]: `((C - (A / B)) / (A / B))`
   * &#x200B;
     [!UICONTROL Format]: `Percentage`

* Mått `A`: `Ad Spend (hide)`
* Mått `B`: `Ad customer acquisitions (hide)`
* Mått `C`: `Average LTV (hide)`
* [!UICONTROL Formula]: `Ads ROI`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL -intervall]: `None`
* &#x200B;
  [!UICONTROL Chart Type]: `Scalar`

* **Beställningar efter gasturka**
   * &#x200B;
     [!UICONTROL -mått]: `Orders`

* Mått `A`: `Orders`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By Month`
* [!UICONTROL Group by]: `Order's medium`
* &#x200B;
  [!UICONTROL Chart Type]: `Area`

* **Annonsera avkastningen från kampanj**
   * [!UICONTROL Metric]: `Ad Spend`

   * [!UICONTROL Metric]:`New customers`
   * [!UICONTROL Filters]:
      * `User's first order's source LIKE %google%`
      * `User's first order's source LIKE %facebook%`
      * `User's first order's source LIKE %fb%`
      * `User's first order's medium IN cpc, ppc`
      * Filterlogik: ([`A`] ELLER [`B`] ELLER [`C`]) OCH [`D`]

   * [!UICONTROL Metric]: Inkomster för genomsnittlig livstid
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
   * &#x200B;
     [!UICONTROL Format]: `Currency`

   * [!UICONTROL Formula]: `(C - (A / B))`
   * &#x200B;
     [!UICONTROL Format]: `Currency`

   * [!UICONTROL Formula]: `((C - (A / B)) / (A / B))`
   * &#x200B;
     [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Metric]: `Ad Clicks`

   * [!UICONTROL Metric]: `Ad Impressions`

   * [!UICONTROL Formula]: `(H / I)`
   * &#x200B;
     [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Formula]: `(A / H)`
   * &#x200B;
     [!UICONTROL Format]: `Currency`

* Mått `A`: `Ad Spend` (dölj)
* Mått `B`: `Ad customer acquisitions`
* Mått `C`: `Average LTV`
* Mått `D`: `Average lifetime # of orders`
* &#x200B;
  [!UICONTROL -formel]: `CAC`
* [!UICONTROL Formula]: `Avg return`
* [!UICONTROL Formula]: `Ads ROI`
* Mått `H`: `adClicks`
* Mått `I`: `Impressions`
* &#x200B;
  [!UICONTROL -formel]: `CTR`
* &#x200B;
  [!UICONTROL -formel]: `CPC`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL -intervall]: `None`
* &#x200B;
  [!UICONTROL Group by]: `campaign` (Använd kundens första beställningskampanj för statistik över icke-annonsutgift)
* &#x200B;
  [!UICONTROL Chart Type]: `Table`

[Kontakta support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) om du får frågor under arbetet med att skapa den här analysen, eller om du bara vill engagera Professional Services-teamet.

### Relaterad

* [Metodtips för UTM-taggning i  [!DNL Google Analytics]](../../best-practices/utm-tagging-google.md)
* [Hur fungerar  [!DNL Google Analytics] UTM-attribuering?](../analysis/utm-attributes.md)
