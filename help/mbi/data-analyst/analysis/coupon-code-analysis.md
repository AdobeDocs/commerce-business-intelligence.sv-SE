---
title: Kupongprestanda
description: Lär dig hur du analyserar din kupongprestanda.
exl-id: f6565e33-18ee-4f85-ade0-fd361854475b
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: d8fc96a58b72c601a5700f35ea1f3dc982d76571
workflow-type: tm+mt
source-wordcount: '1228'
ht-degree: 0%

---

# Avancerad kupongkodanalys

Att förstå hur ert företag presterar i form av kuponger är ett intressant sätt att segmentera era order och också bättre förstå era kunder. I det här avsnittet går du igenom stegen för att skapa analyser för att förstå vilka kunder du köper med hjälp av kuponger, hur de fungerar och spåra allmän kuponganvändning.

![](../../assets/coupon_analysis_-_analysis_library.png)<!--{: width="800" height="375"}-->

Den här analysen innehåller [avancerade beräknade kolumner](../data-warehouse-mgr/adv-calc-columns.md).

## Komma igång

Som ett första steg måste du se till att följande kolumner synkroniseras med Datan Warehouse. Om de inte är det, kan du följa upp dem genom att gå till `Manage Data` > `Data Warehouse` och synkronisera följande:

* tabellen **sales\_flat\_order**
* **kupong\_kod**
* **bas\_rabatt\_belopp**

## Beräknade kolumner

Kolumner som ska skapas oavsett gästorderprincip:

* `sales\_flat\_order`-tabell
* **Beställningen har kupong?**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `coupon\_code`

   * &#x200B;

     [!UICONTROL -datatyp]: `String`
   * [!UICONTROL Calculation]: skiftläge när `A` är null så slutar `No coupon` else `Coupon`

* **\[INPUT\] customer\_id - kupongkod**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `customer\_id`
      * `B`: `coupon\_code`

   * [!UICONTROL Datatype]-sträng
   * [!UICONTROL Calculation]: `concat(A,' - ',B)`

* **Antal order med den här kupongen**
   * [!UICONTROL Column type]: `Same Table => EVENT\_NUMBER`
   * Händelseägare:`INPUT customer_id - coupon code`
   * Händelsenivå: `created\_at`
   * [!UICONTROL Filters]: `Orders we count` filteruppsättning

Ytterligare kolumner som ska skapas om gästorder INTE stöds:

* `customer\_entity`-tabell
   * **Kundens första order innehöll en kupong? (Kupong/ingen kupong)**
   * [!UICONTROL Column type]: `Many to One => MAX`
   * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
   * Välj en [!UICONTROL column]: `Order has coupon applied? (Coupon/No coupon)`
   * [!UICONTROL Filters]:
      * `A`: `Orders we count`
      * `B`: `Customer's order number = 1`

   * **Kundens första orderkupong**
      * [!UICONTROL Column type]: `Many to One => MAX`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * Välj en [!UICONTROL column]: `coupon\_code`
      * [!UICONTROL Filter]:
         * `A`: `Orders we count`
         * `B`: `Customer's order number = 1`

   * **Kundens livstid antal kuponger som används**
      * [!UICONTROL Column type]: `Many to One => COUNT`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * [!UICONTROL Filter]:
         * `A`: `Orders we count`
         * `B`: `Order has coupon applied? (Coupon/No coupon) = Coupon`

   * **Kund som förvärvar kupong eller kund som inte förvärvar kupong**
      * [!UICONTROL Column type]: `Same Table => CALCULATION`
      * [!UICONTROL Inputs]:
         * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`

      * &#x200B;

        [!UICONTROL -datatyp]: `String`
      * [!UICONTROL Calculation]: **case when A=&#39;Coupon&#39; then &#39;Coupon purchase customer&#39; else &#39;Non-coupon purchase customer&#39; end**

   * **Procent av kundens order med kupong**
      * [!UICONTROL Column type]: `Same Table => CALCULATION`
      * [!UICONTROL Inputs]:
         * `A`: `User's lifetime number of coupons used`
         * `B`: `User's lifetime number of orders`

      * &#x200B;

        [!UICONTROL -datatyp]: `Decimal`
      * [!UICONTROL Calculation]: **case when A is null or B is null or B=0 then null else A/B end**

   * **Kundens kuponganvändning**
      * [!UICONTROL Column type]: `Same Table => Calculation`
      * [!UICONTROL Inputs]:
         * `A`: `Percent of customer's orders with coupon`

      * &#x200B;

        [!UICONTROL -datatyp]: `String`
      * [!UICONTROL Calculation]: **case when A is null then null when A=0 then &#39;Never used coupon&#39; when A&lt;0.5 then &#39;Most full price&#39; when A=0.5 then &#39;50/50&#39; when A=1 then &#39;Coupons only&#39; when A>0.5 then &#39;Most coupon&#39; else &#39;Undefined&#39; end**

* `sales\_flat\_order`-tabell
   * **Kundens första order innehåller kupong? (Kupong/ingen kupong)**
      * [!UICONTROL Column type]: `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * Välj en [!UICONTROL column]: `Customer's first order included a coupon? (Coupon/No coupon)`
^

   * **Kundens första orderkupong**
      * [!UICONTROL Column type]: `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * Välj en [!UICONTROL column]: `Customer's first order coupon?`

Ytterligare kolumner som ska skapas om gästorder INTE stöds:

* `sales\_flat\_order`-tabell
   * **Kundens första order innehöll en kupong? (Kupong/ingen kupong)** **-** skapades av analytiker som en del av din \[COUPON ANALYSIS\]-biljett
   * **Kundens första orderkupong**{:}**-** skapad av analytiker som en del av din \[COUPON ANALYSIS\]-biljett

* **Kundens livstidsantal kuponger som använts**{:}**-** skapade av analytiker som en del av din \[COUPON ANALYSIS\]-biljett
* **Kund som förvärvar kupong eller kund som inte förvärvar kupong**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`

   * &#x200B;

     [!UICONTROL -datatyp]: `String`
   * [!UICONTROL Calculation]: **case when A=&#39;Coupon&#39; then &#39;Coupon purchase customer&#39; else &#39;Non-coupon purchase customer&#39; end**

* **Procent av kundens order med kupong**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `User's lifetime number of coupons used`
      * `B`: `User's lifetime number of orders`

   * &#x200B;

     [!UICONTROL -datatyp]: `Decimal`
   * [!UICONTROL Calculation]: **case when A is null or B is null or B=0 then null else A/B end**

* **Kundens kuponganvändning**
   * [!UICONTROL Column type]: `Same Table => Calculation`
   * [!UICONTROL Inputs]:
      * `A`: `Percent of customer's orders with coupon`

   * &#x200B;

     [!UICONTROL -datatyp]: `String`
   * [!UICONTROL Calculation]: **case when A is null then null when A=0 then &#39;Never used coupon&#39; when A&lt;0.5 then &#39;Most full price&#39; when A=0.5 then &#39;50/50&#39; when A=1 then &#39;Coupons only&#39; when A>0.5 then &#39;Most coupon&#39; else &#39;Undefined&#39; end**

## Mått

* **Kupongrabatt**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* I tabellen `sales\_flat\_order`
* Detta mått utför en **summa**
* I kolumnen `discount\_amount`
* Ordnad efter tidsstämpeln `created\_at`
* [!UICONTROL Filter]:

* **Antal kuponger som används**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* I tabellen `sales\_flat\_order`
* Detta mått utför ett **antal**
* I kolumnen `entity\_id`
* Ordnad efter tidsstämpeln `created\_at`
* [!UICONTROL Filter]:

>[!NOTE]
>
>Se till att [lägga till alla nya kolumner som mått i mätvärden](../data-warehouse-mgr/manage-data-dimensions-metrics.md) innan du skapar nya rapporter.

## Rapporter

* **% av kupongförvärvade och icke-kupongförvärvade kunder**
   * [!UICONTROL Metric]: `New customers`

* Mått `A`: `Coupon acquisitions`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL -intervall]: `None`
* [!UICONTROL Group by]: `Coupon acquisitions customer` eller `Non coupon acquisition customer`
* &#x200B;
  [!UICONTROL -diagramtyp]: `Pie`

* **Antal kupongförvärvade och icke-kupongförvärvade kunder**
   * [!UICONTROL Metric]: `New customers`

* Mått A: `Coupon acquisitions`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By Month`
* [!UICONTROL Group by]: `Coupon acquisitions customer` eller `Non coupon acquisition customer`
* [!UICONTROL Chart type]: `Stacked column`

* **Inkomster för genomsnittlig livslängd: Kupongsintäkt. (90+ dagar)**
   * [!UICONTROL Metric]: `Average lifetime revenue`
   * [!UICONTROL Filter]:
      * Kundens första order innehöll en kupong (kupong/ingen kupong) = kupong

* Mått `A`: `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period]: `X years ago to 90 days ago`
* &#x200B;
  [!UICONTROL -intervall]: `None`
* &#x200B;
  [!UICONTROL -diagramtyp]: `Scalar`

* **Inkomster för genomsnittlig livstid: Acq utan kupong. (90+ dagar)**
   * [!UICONTROL Metric]: Inkomster för genomsnittlig livstid
   * [!UICONTROL Filter]:
      * Kundens första order innehöll en kupong (kupong/ingen kupong) = ingen kupong

* Mått `A`: `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period]: `X years ago to 90 days ago`
* &#x200B;
  [!UICONTROL -intervall]: `None`
* &#x200B;
  [!UICONTROL -diagramtyp]: `Scalar`

* **Genomsnittlig livstidsintäkt per kupong för första ordern**
   * [!UICONTROL Metric]: `Average lifetime revenue`

* Mått `A`: `Average lifetime revenue`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL -intervall]: `None`
* [!UICONTROL Group by]: `Customer's first order's coupon`
* &#x200B;
  [!UICONTROL -diagramtyp]: `Column`

>[!NOTE]
>
>Om du har många kupongkoder, precis som många kunder, vill du använda en övre/nedre del, t.ex. de tio viktigaste, sorterade efter Avg livstid.

* **Sannolikhet för upprepade order: kupongförvärv**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * Kundens första order innehöll en kupong (kupong/ingen kupong) = kupong

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * Kundens första order innehöll en kupong (kupong/ingen kupong) = kupong
      * Är kundens senaste order? = Nej
   * &#x200B;

     [!UICONTROL -formel]: `B/A`
   * [!UICONTROL Format]: `Percentage %`

   * Välj statistiskt signifikant siffra i diagrammet `Customer's by lifetime orders`. När du tittar på diagrammet är det en bra regel att söka efter ordernummer med 30 eller fler kunder i bucket. Beroende på datauppsättningen kan det vara ett stort tal så du kan lägga till 1-10.

* Mått `A`: `Number of orders`
* Mått `B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL -intervall]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* [!UICONTROL Chart type]: `Bar chart`

* **Sannolikhet för upprepade order: Icke-kupongförvärv**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * Kundens första order innehöll en kupong (kupong/ingen kupong) = ingen kupong

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * Kundens första order innehöll en kupong (kupong/ingen kupong) = ingen kupong
      * Är kundens senaste order? = Nej

   * &#x200B;

     [!UICONTROL -formel]: `B/A`
   * [!UICONTROL Format]: `Percentage %`

   * Välj statistiskt signifikant siffra i `Customer's by lifetime orders`-diagram eller 1-5.

* Mått `A`: `Number of orders`
* Mått `B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL -intervall]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* [!UICONTROL Chart type]: `Bar chart`

* **Kupongförvärvad kunds kuponganvändning (upprepade order)**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * Kupongförvärvskund eller förvärvskund utan kupong = Kupongförvärv

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * Kundens ordernummer > 1
      * Kundens första order innehöll en kupong? (kupong/ingen kupong) = kupong

   * [!UICONTROL Metric]:`Number of orders`
   * [!UICONTROL Filter]:
      * Kundens ordernummer > 1
      * Kundens första order innehöll en kupong? (kupong/ingen kupong) = kupong
      * Har kupong tillämpats på ordern? (kupong/ingen kupong) = kupong

   * &#x200B;

     [!UICONTROL -formel]: `C/B`
   * [!UICONTROL Format]: `Percentage %`

* Mått `A`: `Coupon-acquired customers`
* Mått `B`: `Number of repeat orders`
* Mått `C`: `Number of repeat orders with coupon`
* [!UICONTROL Formula]: `% of repeat orders with coupon`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL -intervall]: `None`
* &#x200B;
  [!UICONTROL -diagramtyp]: `Table` (kan införliva tabellen för bättre visualisering)

* **Icke-kupongförvärvad kundens rabattnivå (upprepade order)**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * Kupongförvärvskund eller förvärvskund utan kupong = Förvärv utan kupong

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * Kundens ordernummer > 1
      * Kundens första order innehöll en kupong? (kupong/ingen kupong) = ingen kupong

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * Kundens ordernummer > 1
      * Kundens första order innehöll en kupong? (kupong/ingen kupong) = ingen kupong
      * Har kupong tillämpats på ordern? (kupong/ingen kupong) = kupong

   * &#x200B;

     [!UICONTROL -formel]: `C/B`
   * [!UICONTROL Format]: `Percentage %`

* Mått `A`: `Non-coupon-acquired customers`
* Mått `B`: `Number of repeat orders`
* Mått `C`: `Number of repeat orders with coupon`
* [!UICONTROL Formula]: `% of repeat orders with coupon`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL -intervall]: `None`
* &#x200B;
  [!UICONTROL -diagramtyp]: `Table` (kan införliva tabellen för bättre visualisering)

* **Kuponganvändningsinformation (första gången beställningen)**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * Kundens ordernummer = 1
      * Antal order med denna kupong > 10

   * &#x200B;

     [!UICONTROL -mått]: `Revenue`
   * [!UICONTROL Filter]:
      * Kundens ordernummer = 1
      * Antal order med denna kupong > 10

   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Filter]:
      * Kundens ordernummer = 1
      * Antal order med denna kupong > 10

   * [!UICONTROL Formula]: `B-C` (om C är negativt); B+C (om C är positivt)
   * &#x200B;

     [!UICONTROL -format]: `Currency`

   * [!UICONTROL Metric]: `Average order value`
   * [!UICONTROL Filter]:
      * Kundens ordernummer = 1
      * Antal order med denna kupong > 10

* Mått `A`: `First time orders (FTO)`
* Mått `B`: `Revenue from FTO`
* Mått `C`: `Discounts applied to FTO`
* [!UICONTROL Formula]: `Gross revenue from FTO`
* Mått `E`: `Average order value for FTO`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL -intervall]: `None`
* [!UICONTROL Group by]: `coupon code`
* &#x200B;
  [!UICONTROL -diagramtyp]: `Table`
>[!NOTE]
>
>Kvantiteten 10 för &quot;Antal order med denna kupong&quot; är godtycklig. Du kan använda den lämpligaste kvantiteten för det här filtret.

* **Antal order med kupong (all tid)**
   * [!UICONTROL Metric]: `Number of coupons used`

* Mått `A`: `Number or orders with coupon`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL -intervall]: `None`
* &#x200B;
  [!UICONTROL -diagramtyp]: `Scalar`

* **Nettointäkter från order med kuponger (all tid)**
   * &#x200B;

     [!UICONTROL -mått]: `Revenue`
   * [!UICONTROL Filter]:
      * Har kupong tillämpats på ordern? (kupong/ingen kupong) = kupong

* Mått `A`: `Net revenue from orders with coupons`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL -intervall]: `None`
* &#x200B;
  [!UICONTROL -diagramtyp]: `Scalar`

* **Rabatter från kuponger (all tid)**
   * [!UICONTROL Metric]: `Number of coupons used`

* Mått `A`: `Coupon discount amount`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL -intervall]: `None`
* &#x200B;
  [!UICONTROL -diagramtyp]: `Scalar`

* **Antal order med och utan kuponger**
   * [!UICONTROL Metric]: `Number of orders`

* Mått `A`: `Number of orders`
* [!UICONTROL Time period]: `Last 24 months`
* &#x200B;
  [!UICONTROL -intervall]: `None`
* [!UICONTROL Group by]: `Order has coupon applied? (Coupon/No coupon)`
* [!UICONTROL Chart type]: `Stacked column`

* **Kuponganvändning bland upprepande användare**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * Kundens antal beställningar under hela dess livslängd > 1

* Mått `A`: `New customers`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL -intervall]: `None`
* [!UICONTROL Group by]: `Customer's coupon usage`
* &#x200B;
  [!UICONTROL -diagramtyp]: `Pie`

* **Kuponganvändningsinformation**
   * [!UICONTROL Metric]: `Number of orders with coupon`
   * [!UICONTROL Filter]:
      * Antal order med denna kupong > 10

   * &#x200B;

     [!UICONTROL -mått]: `Revenue`
   * [!UICONTROL Filter]:
      * Antal order med denna kupong > 10

   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Filter]:
      * Antal order med denna kupong > 10

   * [!UICONTROL Formula]: `B-C` (om `C` är negativt); `B+C` (om `C` är positivt)
   * &#x200B;

     [!UICONTROL -format]: `Currency`

   * [!UICONTROL Formula]: `C/(B-C)` (om `C` är negativt); `C/(B+C)` (om `C` är positivt)
   * &#x200B;

     [!UICONTROL -format]: `Percentage`

   * [!UICONTROL Metric]: `Average order value`
   * [!UICONTROL Filter]:
      * Antal order med denna kupong > 10

   * &#x200B;

     [!UICONTROL -formel]: `C/A`
   * &#x200B;

     [!UICONTROL -format]: `Currency`

   * [!UICONTROL Metric]: `Distinct buyers`
   * [!UICONTROL Filter]:
      * Antal order med denna kupong > 10

* Mått `A`: `Number of orders`
* Mått `B`: `Net revenue from orders`
* Mått `C`: `Total discounts applied`
* [!UICONTROL Formula]: `Gross revenue`
* [!UICONTROL Formula]: `% discounted`
* Mått `F`: `Average net order value`
* [!UICONTROL Formula]: `Average order discount`
* Mått `H`: `Distinct buyers`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL -intervall]: `None`
* [!UICONTROL Group by]: `coupon code`
* &#x200B;
  [!UICONTROL -diagramtyp]: `Table`

>[!NOTE]
>
>Kvantiteten 10 för &quot;Antal order med denna kupong&quot; är godtycklig. Du kan använda den lämpligaste kvantiteten för det här filtret.

När du har kompilerat alla rapporter kan du ordna dem på kontrollpanelen som du vill. Resultatet kan se ut som bilden överst på sidan.

[Kontakta support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) om du får frågor under arbetet med att skapa den här analysen, eller om du bara vill engagera Professional Services-teamet.

>[!NOTE]
>
>Från och med Adobe Commerce 2.4.7 kan kunderna använda tabellerna **quote_coupons** och **sales_order_coupons** för att få insikter om hur kunderna använder flera kuponger.

![](../../assets/multicoupon_relationship_tables.png)
