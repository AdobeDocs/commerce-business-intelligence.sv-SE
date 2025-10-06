---
title: Kupongkodanalys (grundläggande)
description: Läs mer om hur ert företag presterar i form av kuponger är ett intressant sätt att segmentera era order och bättre förstå kundernas vanor.
exl-id: 0d486259-b210-42ae-8f79-cd91cc15c2c2
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---

# Kupongkodsanalys

Att förstå kupongresultaten i ert företag är ett intressant sätt att segmentera era order och bättre förstå kundvanor.

I det här avsnittet beskrivs stegen som krävs för att skapa den här analysen för att förstå hur kupongköpta kunder fungerar, se trender och spåra användningen av enskilda kupongkoder.

![Kontrollpanel för kupongkodanalys som visar användnings- och prestandamått](../../assets/coupon_analysis_dash_720.png)<!--{: width="807" height="471"}-->

## Komma igång

Först en anteckning om hur kupongkoder spåras. Om en kund har tillämpat en kupong på en order händer tre saker:

* En rabatt visas i beloppet `base_grand_total` (ditt `Revenue`-mått i Commerce Intelligence)
* Kupongkoden lagras i fältet `coupon_code`. Om det här fältet är NULL (tomt) är ordern inte kopplad till någon kupong.
* Det rabatterade beloppet lagras i `base_discount_amount`. Beroende på din konfiguration kan det här värdet vara negativt eller positivt.

Från och med Commerce 2.4.7 kan kunden lägga till mer än en kupongkod i en order. I detta fall:

* Alla kupongkoder som används lagras i fältet `coupon_code` i `sales_order_coupons`. Den första kupongkoden som används lagras också i fältet `coupon_code` i `sales_order`. Om det här fältet är NULL (tomt) är ordern inte kopplad till någon kupong.

## Bygga ett mått

Det första steget är att skapa ett nytt mått med följande steg:

* Navigera till **[!UICONTROL Manage Data > Metrics > Create New Metric]**.

* Välj `sales_order`.
* Det här måttet utför en **summa** i kolumnen **base_rabatt_amount** som sorteras av **created_at**.
   * [!UICONTROL Filters]:
      * Lägg till `Orders we count` (sparad filteruppsättning)
      * Lägg till följande:
         * `coupon_code`**ÄR INTE**`[NULL]`
      * Ge måttet ett namn, till exempel `Coupon discount amount`.

## Skapa en instrumentpanel

* När måttet har skapats:
   * Navigera till [!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**.
   * Ge instrumentpanelen ett namn som `_Coupon Analysis_`.

* Här skapar du och lägger till alla rapporter.

## Skapar rapporter

* **Nya rapporter:**

>[!NOTE]
>
>[!UICONTROL Time Period]** för varje rapport visas som `All-time`. Du kan ändra detta efter dina analysbehov. Adobe rekommenderar att alla rapporter på den här instrumentpanelen täcker samma tidsperiod, till exempel `All time`, `Year-to-date` eller `Last 365 days`.

* **Beställningar med kuponger**
   * &#x200B;
     [!UICONTROL -mått]: `Orders`
      * Lägg till filter:
         * [`A`] `coupon_code` **ÄR INTE** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL -intervall]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`

* **Beställningar utan kuponger**
   * &#x200B;
     [!UICONTROL -mått]: `Orders`
      * Lägg till filter:
         * [`A`] `coupon_code` **IS** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL -intervall]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`

* **Nettointäkter från order med kuponger**
   * &#x200B;
     [!UICONTROL -mått]: `Revenue`
      * Lägg till filter:
         * [`A`] `coupon_code` **ÄR INTE** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL -intervall]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Rabatter från kuponger**
   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL -intervall]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Inkomster för genomsnittlig livstid: Kuponghanterade kunder**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Lägg till filter:
         * [`A`] `Customer's first order's coupon_code` **ÄR INTE** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL -intervall]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Inkomster för livslängd i genomsnitt: Kunder som inte har kuponganskaffats**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Lägg till filter:
         * [A] `Customer's first order's coupon_code` **IS**`[NULL]`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL -intervall]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Kuponganvändningsinformation (första gången beställningen)**
   * Mått `1`: `Orders`
      * Lägg till filter:
         * [`A`] `coupon_code` **ÄR INTE**`[NULL]`
         * [`B`] `Customer's order number` **Lika med** `1`

   * Mått `2`: `Revenue`
      * Lägg till filter:
         * [`A`] `coupon_code` **ÄR INTE**`[NULL]`
         * [`B`] `Customer's order number` **Lika med** `1`

      * Byt namn: `Net revenue`

   * Mått `3`: `Coupon discount amount`
      * Lägg till filter:
         * [`A`] `coupon_code` **ÄR INTE**`[NULL]`
         * [`B`] `Customer's order number` **Lika med** `1`

   * Skapa formel: `Gross revenue`
      * [!UICONTROL Formula]: `(B – C)`
      * &#x200B;
        [!UICONTROL Format]: `Currency`

   * Skapa formel:**% rabatt**
      * Formel: `(C / (B - C))`
      * &#x200B;
        [!UICONTROL Format]: `Percentage`

   * Skapa formel: `Average order discount`
      * [!UICONTROL Formula]: `(C / A)`
      * &#x200B;
        [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL -intervall]: `None`
   * &#x200B;
     [!UICONTROL -diagramtyp]: `Table`

* **Genomsnittlig livstidsintäkt per kupong för första ordern**
   * [!UICONTROL Metric]:**Genomsnittlig livstidsintäkt**
      * Lägg till filter:
         * [`A`] `coupon_code` **IS**`[NULL]`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL -intervall]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Kuponganvändningsinformation (första gången beställningen)**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Lägg till filter:
         * [`A`] `Customer's first order's coupon_code` **ÄR INTE** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * &#x200B;
     [!UICONTROL -intervall]: `None`
   * [!UICONTROL Group by]: `Customer's first order's coupon_code`
   * &#x200B;
     [!UICONTROL -diagramtyp]: **Column**

* **Nya kunder per kupong/icke-kupongförvärv**
   * Mått `1`: `New customers`
      * Lägg till filter:
         * [`A`] `Customer's first order's coupon_code` **ÄR INTE** `[NULL]`

      * [!UICONTROL Rename]: `Coupon acquisition customer`

   * Mått `2`: `New customers`
      * Lägg till filter:
         * [`A`] `coupon_code` **IS**`[NULL]`

      * [!UICONTROL Rename]: `Non-coupon acquisition customer`

   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `By Month`
   * [!UICONTROL Chart type]: `Stacked Column`

När du har skapat rapporterna kan du se bilden högst upp i det här avsnittet för att se hur du kan ordna rapporterna på din kontrollpanel.

>[!NOTE]
>
>Från och med Adobe Commerce 2.4.7 kan kunderna använda tabellerna **quote_coupons** och **sales_order_coupons** för att få insikter om hur kunderna använder flera kuponger.

![Tabellrelationsdiagram för multikuponganalys](../../assets/multicoupon_relationship_tables.png)
