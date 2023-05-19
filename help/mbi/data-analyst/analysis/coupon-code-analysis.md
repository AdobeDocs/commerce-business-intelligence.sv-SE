---
title: Kupongprestanda
description: Lär dig hur du analyserar din kupongprestanda.
exl-id: f6565e33-18ee-4f85-ade0-fd361854475b
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '1167'
ht-degree: 0%

---

# Avancerad kupongkodanalys

Att förstå hur ert företag presterar i form av kuponger är ett intressant sätt att segmentera era order och också bättre förstå era kunder. I det här avsnittet går du igenom stegen för att skapa analyser för att förstå vilka kunder du köper med hjälp av kuponger, hur de fungerar och spåra allmän kuponganvändning.

![](../../assets/coupon_analysis_-_analysis_library.png)<!--{: width="800" height="375"}-->

Denna analys innehåller [avancerade beräknade kolumner](../data-warehouse-mgr/adv-calc-columns.md).

## Komma igång

Som ett första steg måste du se till att följande kolumner synkroniseras med Data warehouse. Om de inte är det, gå vidare och spåra dem genom att navigera till `Manage Data` > `Data Warehouse`och synkronisera följande:

* **sales\_flat\_order** table
* **kupong\_kod**
* **bas\_rabatt\_belopp**

## Beräknade kolumner

Kolumner som ska skapas oavsett gästorderprincip:

* `sales\_flat\_order` table
* **Har kupong tillämpats på ordern?**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `coupon\_code`
   * 
      [!UICONTROL-datatyp]: `String`
   * [!UICONTROL Calculation]: case when `A` är null då `No coupon` else `Coupon` end


* **\[INPUT\] customer\_id - kupongkod**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `customer\_id`
      * `B`: `coupon\_code`
   * [!UICONTROL Datatype] Sträng
   * [!UICONTROL Calculation]: `concat(A,' - ',B)`


* **Antal order med denna kupong**
   * [!UICONTROL Column type]: `Same Table => EVENT\_NUMBER`
   * Ägare till händelse:`INPUT customer_id - coupon code`
   * Händelsenivå: `created\_at`
   * [!UICONTROL Filters]: `Orders we count` filteruppsättning

Ytterligare kolumner som ska skapas om gästorder INTE stöds:

* `customer\_entity` table
   * **Kundens första order innehöll en kupong? (kupong/ingen kupong)**
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
   * **Kundens livstidsantal använda kuponger**
      * [!UICONTROL Column type]: `Many to One => COUNT`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * [!UICONTROL Filter]:
         * `A`: `Orders we count`
         * `B`: `Order has coupon applied? (Coupon/No coupon) = Coupon`
   * **Kund eller kund som förvärvar kupong**
      * [!UICONTROL Column type]: `Same Table => CALCULATION`
      * [!UICONTROL Inputs]:
         * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`
      * 
         [!UICONTROL-datatyp]: `String`
      * [!UICONTROL Calculation]: **case when A=&#39;Coupon&#39; then &#39;Coupon purchase customer&#39; else &#39;Non-coupon purchase customer&#39; end**
   * **Procent av kundens order med kupong**
      * [!UICONTROL Column type]: `Same Table => CALCULATION`
      * [!UICONTROL Inputs]:
         * `A`: `User's lifetime number of coupons used`
         * `B`: `User's lifetime number of orders`
      * 
         [!UICONTROL-datatyp]: `Decimal`
      * [!UICONTROL Calculation]: **case when A is null or B is null or B=0, then null else A/B end**
   * **Kundens kuponganvändning**
      * [!UICONTROL Column type]: `Same Table => Calculation`
      * [!UICONTROL Inputs]:
         * `A`: `Percent of customer's orders with coupon`
      * 
         [!UICONTROL-datatyp]: `String`
      * [!UICONTROL Calculation]: **fall när A är null, då A=0 och sedan &#39;Används aldrig kupong&#39; när A&lt;0.5 och sedan &#39;Mest fullt pris&#39; när A=0.5 och sedan &#39;50/50&#39; när A=1 och &#39;Endast kuponger&#39; när A>0.5, sedan &#39;Mest kupong&#39; else &#39;Odefinierad&#39; slut**









* `sales\_flat\_order` table
   * **Kundens första order innehåller kupong? (kupong/ingen kupong)**
      * [!UICONTROL Column type]: `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * Välj en [!UICONTROL column]: `Customer's first order included a coupon? (Coupon/No coupon)`
^
   * **Kundens första orderkupong**
      * [!UICONTROL Column type]: `One to Many => JOINED\_COLUMN`
      * [!UICONTROL Path]: `sales\_flat\_order.customer\_id = customer\_entity.entity\_id`
      * Välj en [!UICONTROL column]: `Customer's first order coupon?`


Ytterligare kolumner som ska skapas om gästorder INTE stöds:

* `sales\_flat\_order` table
   * **Kundens första order innehöll en kupong? (kupong/ingen kupong)** **-** skapat av analytiker som en del av din \[COUPON ANALYSIS\]-biljett
   * **Kundens första orderkupong**{::}**-** skapat av analytiker som en del av din \[COUPON ANALYSIS\]-biljett

* **Kundens livstidsantal använda kuponger**{::}**-** skapat av analytiker som en del av din \[COUPON ANALYSIS\]-biljett
* **Kund eller kund som förvärvar kupong**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `Customer's first order included a coupon? (Coupon/No coupon)`
   * 
      [!UICONTROL-datatyp]: `String`
   * [!UICONTROL Calculation]: **case when A=&#39;Coupon&#39; then &#39;Coupon purchase customer&#39; else &#39;Non-coupon purchase customer&#39; end**


* **Procent av kundens order med kupong**
   * [!UICONTROL Column type]: `Same Table => CALCULATION`
   * [!UICONTROL Inputs]:
      * `A`: `User's lifetime number of coupons used`
      * `B`: `User's lifetime number of orders`
   * 
      [!UICONTROL-datatyp]: `Decimal`
   * [!UICONTROL Calculation]: **case when A is null or B is null or B=0, then null else A/B end**


* **Kundens kuponganvändning**
   * [!UICONTROL Column type]: `Same Table => Calculation`
   * [!UICONTROL Inputs]:
      * `A`: `Percent of customer's orders with coupon`
   * 
      [!UICONTROL-datatyp]: `String`
   * [!UICONTROL Calculation]: **fall när A är null, då A=0 och sedan &#39;Används aldrig kupong&#39; när A&lt;0.5 och sedan &#39;Mest fullt pris&#39; när A=0.5 och sedan &#39;50/50&#39; när A=1 och &#39;Endast kuponger&#39; när A>0.5, sedan &#39;Mest kupong&#39; else &#39;Odefinierad&#39; slut**


## Mått

* **Kupongrabatt**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* I `sales\_flat\_order` table
* Detta mått utför en **Summa**
* På `discount\_amount` kolumn
* Beställd av `created\_at` tidsstämpel
* [!UICONTROL Filter]:

* **Antal kuponger som används**
   * `Orders we count`
   * `Order has coupon applied? (Coupon/No coupon)= Coupon`

* I `sales\_flat\_order` table
* Detta mått utför en **Antal**
* På `entity\_id` kolumn
* Beställd av `created\_at` tidsstämpel
* [!UICONTROL Filter]:

>[!NOTE]
>
>Se till att [lägga till alla nya kolumner som dimensioner till mått](../data-warehouse-mgr/manage-data-dimensions-metrics.md) innan du skapar nya rapporter.

## Rapporter

* **% av kupongförvärvade och icke kupongförvärvade kunder**
   * [!UICONTROL Metric]: `New customers`

* Mått `A`: `Coupon acquisitions`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL-intervall]: `None`
* [!UICONTROL Group by]: `Coupon acquisitions customer` eller `Non coupon acquisition customer`
* 

   [!UICONTROL-diagramtyp]: `Pie`

* **Antal kupongförvärvade och icke kupongförvärvade kunder**
   * [!UICONTROL Metric]: `New customers`

* Mått A: `Coupon acquisitions`
* [!UICONTROL Time period]: `All time`
* [!UICONTROL Interval]: `By Month`
* [!UICONTROL Group by]: `Coupon acquisitions customer` eller `Non coupon acquisition customer`
* [!UICONTROL Chart type]: `Stacked column`

* **Inkomster för genomsnittlig livstid: Kuponger (90+ dagar)**
   * [!UICONTROL Metric]: `Average lifetime revenue`
   * [!UICONTROL Filter]:
      * Kundens första order innehöll en kupong (kupong/ingen kupong) = kupong

* Mått `A`: `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period]: `X years ago to 90 days ago`
* 
   [!UICONTROL-intervall]: `None`
* 

   [!UICONTROL-diagramtyp]: `Scalar`

* **Inkomster för genomsnittlig livstid: Acq utan kupong (90+ dagar)**
   * [!UICONTROL Metric]: Genomsnittlig intäkt för livstid
   * [!UICONTROL Filter]:
      * Kundens första order innehöll en kupong (kupong/ingen kupong) = ingen kupong

* Mått `A`: `Average lifetime revenue (at least 3 months age)`
* [!UICONTROL Time period]: `X years ago to 90 days ago`
* 
   [!UICONTROL-intervall]: `None`
* 

   [!UICONTROL-diagramtyp]: `Scalar`

* **Genomsnittlig livslängdsintäkt per kupong för första ordern**
   * [!UICONTROL Metric]: `Average lifetime revenue`

* Mått `A`: `Average lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL-intervall]: `None`
* [!UICONTROL Group by]: `Customer's first order's coupon`
* 

   [!UICONTROL-diagramtyp]: `Column`

>[!NOTE]
>
>Om du har många kupongkoder, precis som många kunder, vill du använda en övre/nedre del, t.ex. de tio viktigaste, sorterade efter Avg livstid.

* **Sannolikhet för upprepad order: Kupongförvärv**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * Kundens första order innehöll en kupong (kupong/ingen kupong) = kupong
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * Kundens första order innehöll en kupong (kupong/ingen kupong) = kupong
      * Är kundens senaste order? = Nej
   * 
      [!UICONTROL-formel]: `B/A`
   * [!UICONTROL Format]: `Percentage %`

   * Välj statistiskt signifikant antal från `Customer's by lifetime orders` diagram. När du tittar på diagrammet är det en bra regel att söka efter ordernummer med 30 eller fler kunder i bucket. Beroende på datauppsättningen kan det vara ett stort tal så du kan lägga till 1-10.


* Mått `A`: `Number of orders`
* Mått `B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL-intervall]: `None`
* [!UICONTROL Group by]: `Customer's order number`
* [!UICONTROL Chart type]: `Bar chart`

* **Sannolikhet för upprepad ordning: Icke-kupongförvärv**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * Kundens första order innehöll en kupong (kupong/ingen kupong) = ingen kupong
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * Kundens första order innehöll en kupong (kupong/ingen kupong) = ingen kupong
      * Är kundens senaste order? = Nej
   * 
      [!UICONTROL-formel]: `B/A`
   * [!UICONTROL Format]: `Percentage %`

   * Välj statistiskt signifikant antal från `Customer's by lifetime orders` eller 1-5.



* Mått `A`: `Number of orders`
* Mått `B`: `Number of non last orders`
* [!UICONTROL Formula]: `Repeat order probability`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL-intervall]: `None`
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
   * 
      [!UICONTROL-formel]: `C/B`
   * [!UICONTROL Format]: `Percentage %`




* Mått `A`: `Coupon-acquired customers`
* Mått `B`: `Number of repeat orders`
* Mått `C`: `Number of repeat orders with coupon`
* [!UICONTROL Formula]: `% of repeat orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL-intervall]: `None`
* 

   [!UICONTROL-diagramtyp]: `Table` (kan införliva den här tabellen för bättre visualisering)

* **Icke-kupongförvärvad kunds kuponganvändning (upprepade order)**
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
   * 
      [!UICONTROL-formel]: `C/B`
   * [!UICONTROL Format]: `Percentage %`




* Mått `A`: `Non-coupon-acquired customers`
* Mått `B`: `Number of repeat orders`
* Mått `C`: `Number of repeat orders with coupon`
* [!UICONTROL Formula]: `% of repeat orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL-intervall]: `None`
* 

   [!UICONTROL-diagramtyp]: `Table` (kan införliva den här tabellen för bättre visualisering)

* **Kuponganvändningsinformation (första beställningen)**
   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Filter]:
      * Kundens ordernummer = 1
      * Antal order med denna kupong > 10
   * 
      [!UICONTROL-mått]: `Revenue`
   * [!UICONTROL Filter]:
      * Kundens ordernummer = 1
      * Antal order med denna kupong > 10
   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Filter]:
      * Kundens ordernummer = 1
      * Antal order med denna kupong > 10
   * [!UICONTROL Formula]: `B-C` (om C är negativt) B+C (om C är positivt)
   * 

      [!UICONTROL-format]: `Currency`

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
* 
   [!UICONTROL-intervall]: `None`
* [!UICONTROL Group by]: `coupon code`
* 

   [!UICONTROL-diagramtyp]: `Table`
>[!NOTE]
>
>Mängden 10 för &quot;Antal order med denna kupong&quot; är godtycklig. Du kan använda den lämpligaste kvantiteten för det här filtret.

* **Antal order med kupong (all tid)**
   * [!UICONTROL Metric]: `Number of coupons used`

* Mått `A`: `Number or orders with coupon`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL-intervall]: `None`
* 

   [!UICONTROL-diagramtyp]: `Scalar`

* **Nettointäkter från order med kuponger (hela tiden)**
   * 
      [!UICONTROL-mått]: `Revenue`
   * [!UICONTROL Filter]:
      * Har kupong tillämpats på ordern? (kupong/ingen kupong) = kupong

* Mått `A`: `Net revenue from orders with coupons`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL-intervall]: `None`
* 

   [!UICONTROL-diagramtyp]: `Scalar`

* **Rabatter från kuponger (hela tiden)**
   * [!UICONTROL Metric]: `Number of coupons used`

* Mått `A`: `Coupon discount amount`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL-intervall]: `None`
* 

   [!UICONTROL-diagramtyp]: `Scalar`

* **Antal order med och utan kuponger**
   * [!UICONTROL Metric]: `Number of orders`

* Mått `A`: `Number of orders`
* [!UICONTROL Time period]: `Last 24 months`
* 
   [!UICONTROL-intervall]: `None`
* [!UICONTROL Group by]: `Order has coupon applied? (Coupon/No coupon)`
* [!UICONTROL Chart type]: `Stacked column`

* **Kuponganvändning bland återkommande användare**
   * [!UICONTROL Metric]: `New customers`
   * [!UICONTROL Filter]:
      * Kundens antal beställningar > 1

* Mått `A`: `New customers`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL-intervall]: `None`
* [!UICONTROL Group by]: `Customer's coupon usage`
* 

   [!UICONTROL-diagramtyp]: `Pie`

* **Kuponganvändningsinformation**
   * [!UICONTROL Metric]: `Number of orders with coupon`
   * [!UICONTROL Filter]:
      * Antal order med denna kupong > 10
   * 
      [!UICONTROL-mått]: `Revenue`
   * [!UICONTROL Filter]:
      * Antal order med denna kupong > 10
   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Filter]:
      * Antal order med denna kupong > 10
   * [!UICONTROL Formula]: `B-C` (om `C` är negativt), `B+C` (om `C` är positivt)
   * 

      [!UICONTROL-format]: `Currency`

   * [!UICONTROL Formula]: `C/(B-C)` (om `C` är negativt), `C/(B+C)` (om `C` är positivt)
   * 

      [!UICONTROL-format]: `Percentage`

   * [!UICONTROL Metric]: `Average order value`
   * [!UICONTROL Filter]:
      * Antal order med denna kupong > 10
   * 
      [!UICONTROL-formel]: `C/A`
   * 

      [!UICONTROL-format]: `Currency`

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
* 
   [!UICONTROL-intervall]: `None`
* [!UICONTROL Group by]: `coupon code`
* 
   [!UICONTROL-diagramtyp]: `Table`

>[!NOTE]
>
>Mängden 10 för &quot;Antal order med denna kupong&quot; är godtycklig. Du kan använda den lämpligaste kvantiteten för det här filtret.

När du har kompilerat alla rapporter kan du ordna dem på kontrollpanelen som du vill. Resultatet kan se ut som bilden överst på sidan.

Om du stöter på några frågor när du skapar den här analysen eller bara vill engagera Professional Services-teamet, [kontakta support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
