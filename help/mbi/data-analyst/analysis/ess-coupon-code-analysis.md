---
title: Kupongkodanalys (grundläggande)
description: Läs mer om hur ert företag presterar i form av kuponger är ett intressant sätt att segmentera era order och bättre förstå kundernas vanor.
exl-id: 0d486259-b210-42ae-8f79-cd91cc15c2c2
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# Kupongkodsanalys

Att förstå kupongresultaten i ert företag är ett intressant sätt att segmentera era order och bättre förstå kundvanor.

I det här avsnittet beskrivs stegen som krävs för att skapa den här analysen för att förstå hur kupongköpta kunder fungerar, se trender och spåra användningen av enskilda kupongkoder.

![](../../assets/coupon_analysis_dash_720.png)<!--{: width="807" height="471"}-->

## Komma igång

Först en anteckning om hur kupongkoder spåras. Om en kund har tillämpat en kupong på en order händer tre saker:

* Rabatten framgår av `base_grand_total` mängd (din `Revenue` mått i Commerce Intelligence)
* Kupongkoden lagras i `coupon_code` fält. Om det här fältet är NULL (tomt) är ordern inte kopplad till någon kupong.
* Det diskonterade beloppet lagras i `base_discount_amount`. Beroende på din konfiguration kan det här värdet vara negativt eller positivt.

## Bygga ett mått

Det första steget är att skapa ett nytt mått med följande steg:

* Navigera till **[!UICONTROL Manage Data > Metrics > Create New Metric]**.

* Välj `sales_order`.
* Det här måttet utför en **Summa** på **base_rabatt_amount** kolumn, sorterad efter **created_at**.
   * [!UICONTROL Filters]:
      * Lägg till `Orders we count` (Sparad filteruppsättning)
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
>The [!UICONTROL Time Period]** för varje rapport anges som `All-time`. Du kan ändra detta efter dina analysbehov. Adobe rekommenderar att alla rapporter på kontrollpanelen täcker samma tidsperiod, till exempel `All time`, `Year-to-date`, eller `Last 365 days`.

* **Beställningar med kuponger**
   * 
     [!UICONTROL-mått]: `Orders`
      * Lägg till filter:
         * [`A`] `coupon_code` **ÄR INTE** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL-intervall]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`

* **Beställningar utan kuponger**
   * 
     [!UICONTROL-mått]: `Orders`
      * Lägg till filter:
         * [`A`] `coupon_code` **ÄR** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL-intervall]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`

* **Nettointäkter från order med kuponger**
   * 
     [!UICONTROL-mått]: `Revenue`
      * Lägg till filter:
         * [`A`] `coupon_code` **ÄR INTE** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL-intervall]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Rabatter från kuponger**
   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL-intervall]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Inkomster under hela löptiden: Kupongförvärvade kunder**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Lägg till filter:
         * [`A`] `Customer's first order's coupon_code` **ÄR INTE** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL-intervall]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Genomsnittlig livslängdsintäkt: Icke-kupongförvärvade kunder**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Lägg till filter:
         * [A] `Customer's first order's coupon_code` **ÄR**`[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL-intervall]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Kuponganvändningsinformation (första beställningen)**
   * Mått `1`: `Orders`
      * Lägg till filter:
         * [`A`] `coupon_code` **ÄR INTE**`[NULL]`
         * [`B`] `Customer's order number` **Lika med** `1`

   * Mått `2`: `Revenue`
      * Lägg till filter:
         * [`A`] `coupon_code` **ÄR INTE**`[NULL]`
         * [`B`] `Customer's order number` **Lika med** `1`

      * Byt namn:  `Net revenue`

   * Mått `3`: `Coupon discount amount`
      * Lägg till filter:
         * [`A`] `coupon_code` **ÄR INTE**`[NULL]`
         * [`B`] `Customer's order number` **Lika med** `1`

   * Skapa formel: `Gross revenue`
      * [!UICONTROL Formula]: `(B – C)`
      * 
        [!UICONTROL Format]: `Currency`

   * Skapa formel:**% rabatt**
      * Formel: `(C / (B - C))`
      * 
        [!UICONTROL Format]: `Percentage`

   * Skapa formel: `Average order discount`
      * [!UICONTROL Formula]: `(C / A)`
      * 
        [!UICONTROL Format]: `Percentage`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL-intervall]: `None`
   * 
     [!UICONTROL-diagramtyp]: `Table`

* **Genomsnittlig livslängdsintäkt per kupong för första ordern**
   * [!UICONTROL Metric]:**Genomsnittlig intäkt för livstid**
      * Lägg till filter:
         * [`A`] `coupon_code` **ÄR**`[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL-intervall]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Kuponganvändningsinformation (första beställningen)**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Lägg till filter:
         * [`A`] `Customer's first order's coupon_code` **ÄR INTE** `[NULL]`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL-intervall]: `None`
   * [!UICONTROL Group by]: `Customer's first order's coupon_code`
   * 
     [!UICONTROL-diagramtyp]: **Column**

* **Nya kunder per kupong/icke-kupongförvärv**
   * Mått `1`: `New customers`
      * Lägg till filter:
         * [`A`] `Customer's first order's coupon_code` **ÄR INTE** `[NULL]`

      * [!UICONTROL Rename]: `Coupon acquisition customer`

   * Mått `2`: `New customers`
      * Lägg till filter:
         * [`A`] `coupon_code` **ÄR**`[NULL]`

      * [!UICONTROL Rename]: `Non-coupon acquisition customer`

   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `By Month`
   * [!UICONTROL Chart type]: `Stacked Column`

När du har skapat rapporterna kan du se bilden högst upp i det här avsnittet för att se hur du kan ordna rapporterna på din kontrollpanel.
