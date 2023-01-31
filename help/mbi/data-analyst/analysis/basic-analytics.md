---
title: Förstå och bygga upp grundläggande analyser
description: Lär dig förstå och bygga upp grundläggande analyser.
exl-id: 23cea7b3-2e66-40c3-b4bd-d197237782e3
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '3142'
ht-degree: 0%

---

# Grundläggande analyser

När du känner till [!DNL MBI] och har en grundläggande förståelse för verktyget, kommer du att vilja börja skapa rapporter. En av de vanligaste frågorna du kanske har är &quot;Vad ska jag titta på?&quot;

Informationen nedan sammanfattar några av de gemensamma mätvärden och rapporter som du kan finna värdefulla. Det finns redan ett antal rapporter på ditt konto, så kontrollera att du granskar de värden och rapporter som finns på ditt konto för att undvika att skapa dubbletter.

## Tabeller och kolumner som du vill förstå

När du bygger upp ett mätresultat måste du känna till fyra informationsdelar:

1. Tabellen som data finns på,
1. Den specifika åtgärd som du vill utföra,
1. Kolumnen som du vill utföra åtgärden på och
1. Tidsstämpeln som du vill använda för att spåra data.

De tabellnamn vi använder i de här exemplen skiljer sig förmodligen något från kolumn- och tabellnamnen i databasen eftersom varje databas är unik. Referera till nedanstående definitioner om du behöver hjälp med att identifiera en motsvarande tabell eller kolumn i databasen.

## Kundregister

Tabellen innehåller viktig information om varje kund, t.ex. ett unikt kund-ID, e-postadress, datum när kontot skapades osv. I exemplen nedan kommer vi att använda **[!UICONTROL customer_entity]** som namnet på en exempelkundtabell.

Om några av dessa beräkningar inte finns i databasen kan alla administratörsanvändare på kontot skapa dem. Dessutom vill du se till att de här dimensionerna är grupperbara för alla relevanta mått.

**Dimensioner**

* **[!UICONTROL Entity_id]**: En unik identifierare för varje kund. Det kan också vara ett unikt kundnummer eller en e-postadress till kunden, och det bör fungera som referensnyckel till ordertabellen.
* **[!UICONTROL Created_at]**: Det datum då kundens konto skapades och lades till i databasen.
* **[!UICONTROL Customer's lifetime revenue]**: Den totala livstidsintäkten som genererats av en kund.
* **[!UICONTROL Customer's first 30-day revenue]**: Det totala intäktsbelopp som en kund genererat under de första 30 dagarna.
* **[!UICONTROL Customer's lifetime number of orders]**: Antalet order som en kund lägger under sin livstid.
* **[!UICONTROL Customer's lifetime number of coupons]**: Det totala antalet kuponger som en kund använder under sin livstid.
* **[!UICONTROL Customer's first order date]**: Datumet för en kunds första order. Detta kan skilja sig från datumet created_at om en kund inte gjorde en beställning när de skapades.

**Tar ni emot gästorder?**

*I så fall kanske den här tabellen inte innehåller alla dina kunder. Kontakta oss [supportteam](https://support.magento.com/hc/en-us/articles/360016503692) för att säkerställa att era kundanalyser omfattar alla kunder.*

*Är du inte säker på om du godkänner gästbeställningar? Se [det här ämnet](../data-warehouse-mgr/guest-orders.md) för att lära dig mer!*

## Orderregister

I den här tabellen representerar varje rad en ordning. Kolumnerna i den här tabellen innehåller grundläggande information om varje order, t.ex. orderns ID, skapandedatum, status, ID:t för kunden som beställde ordern osv. I exemplen nedan använder vi **[!UICONTROL sales_flat_order]** som namnet på en exempelordertabell.

**Dimensioner**

* **[!UICONTROL Customer_id]**: En unik identifierare för den kund som lade ordern. Detta används ofta för att flytta information mellan kund- och orderregister. I våra exempel förväntar vi oss customer_id på **[!UICONTROL sales_flat_order]** tabell som ska justeras mot **[!UICONTROL entitiy_id]** på **[!UICONTROL customer_entity]** tabell.
* **[!UICONTROL Created_at]**: Det datum då ordern skapades eller placerades.
* **[!UICONTROL Customer_email]**: E-postadressen till den kund som gjorde beställningen. Detta kan också vara den unika identifieraren för kunden.
* **[!UICONTROL Customer's lifetime number of orders]**: En kopia av kolumnen med samma namn på din `Customers` tabell.
* **[!UICONTROL Customer's order number]**: Kundens sekventiella ordernummer som är kopplat till ordern. Om raden du tittar på till exempel är en kunds första order är kolumnen&quot;1&quot;; men om det var kundens 15:e beställning visas&quot;15&quot; för den här beställningen i den här kolumnen. Om den här dimensionen inte finns på din `Customers` bord, fråga vår [supportteam](https://support.magento.com/hc/en-us/articles/360016503692) för att hjälpa dig att bygga den.
* **[!UICONTROL Customer's order number (previous-current)]**: En sammanfogning av två värden i **[!UICONTROL Customer's order number]** kolumn. Den används i en exempelrapport nedan för att visa den förflutna tiden mellan två order. Tiden mellan en kunds första orderdatum och dess andra orderdatum är till exempel&quot;1-2&quot; med den här beräkningen.
* **[!UICONTROL Coupon_code]**: Visar vilka kuponger som användes på varje order.
* **[!UICONTROL Seconds since previous order]**: Tiden (i sekunder) mellan en kunds order.

## Orderartikelregister

I den här tabellen representerar varje rad en artikel som har sålts. Tabellen innehåller information om de artiklar som säljs i varje beställning, t.ex. referensnummer, produktnummer, kvantitet och så vidare. I exemplen nedan använder vi `sales_flat_order_item` som namnet på en exempelorderobjekttabell.

**Dimensioner**

* **[!UICONTROL Item_id]**: Unik identifierare för varje rad i tabellen.
* **[!UICONTROL Order_id]**: Referensnyckeln till `Orders` som anger vilka artiklar som köpts i samma ordning. Om en order innehåller flera artiklar upprepas det här värdet.
* **[!UICONTROL Product_id]**: Om du vill ha information om den specifika produkt som köpts (till exempel färg, storlek) använder du den här kolumnen för att hämta informationen från produkttabellen.
* **[!UICONTROL Order's created_at]**: Tidsstämpeln som beställningen placerades i kopieras vanligtvis till `order line items` tabell från `Orders` tabell.
* **[!UICONTROL Order's coupon_code]**: Liknar `Order's created_at` dimension, kopieras den här kolumnen från din ordertabell.

## Abonnemangstabell

Tabellen används för att hantera din prenumerationsinformation, t.ex. prenumerations-ID, prenumerantens e-postadress, prenumerationens startdatum osv.

**Dimensioner**

* **[!UICONTROL Customer_id]**: En unik identifierare för den kund som lade ordern. Detta är ett vanligt sätt att skapa en sökväg mellan tabellen Kunder och tabellen Beställningar. I våra exempel förväntar vi oss customer_id på **sales_flat_order** tabell som ska justeras mot `entitiy_id` på `customer_entity` tabell.
* **[!UICONTROL Start date]**: Det datum då en kunds prenumeration började.

## Utgiftsregister för marknadsföring

När ni analyserar era marknadsföringsutgifter kan ni inkludera [!DNL Facebook], [!DNL Google AdWords]eller andra källor i analyserna. Om ni har flera olika marknadsföringsresurser kan ni kontakta vår [Tjänstteam](https://business.adobe.com/products/magento/fully-managed-service.html) för att få hjälp med att skapa en konsoliderad tabell för era marknadsföringskampanjer.

**Dimensioner**

* **[!UICONTROL Spend]**: De totala annonskostnaderna. I [!DNL Facebook], det här skulle vara utgiftskolumnen i `facebook_ads_insights_####` tabell. För [!DNL Google AdWords], skulle det vara `adCost` kolumn i `campaigns####` tabell.
* The `####` som läggs till i var och en av tabellerna relateras till det specifika konto-ID:t för din [!DNL Facebook] eller [!DNL Google AdWords] konto.
* **[!UICONTROL Clicks]**: Det totala antalet klick. I [!DNL Facebook], det här är klickkolumnen i `facebook_ads_insights_####` tabell. I [!DNL Google AdWords]blir det kolumnen adClicks i `campaigns####` tabell.
* **[!UICONTROL Impressions]**: Totalt antal visningar. I [!DNL Facebook], det här skulle vara intryck i `facebook_ads_insights_####` tabell. I [!DNL Google AdWords], det är imponerande `campaigns####` tabell.
* **[!UICONTROL Campaign]**: Det totala antalet klick. I [!DNL Facebook], det här skulle vara kolumnen campaign_name i `facebook_ads_insights_####` tabell. I [!DNL Google AdWords], det här skulle vara kampanjkolumnen i `campaigns####` tabell.
* **[!UICONTROL Date]**: Tidsstämpeln som utgiften, klickningarna eller intrycket inträffade för en viss kampanj. I [!DNL Facebook], skulle det vara `date_start` kolumn i `facebook_ads_insights_####` tabell. I [!DNL Google AdWords]blir det datumkolumnen i `campaigns####` tabell.
* **[!UICONTROL Customer's first order's source]**: Orderns källa från en kunds första order. Kontrollera först om du har en kolumn med namnet `customer's first order's source` i ditt konto. Om den här kolumnen inte visas kan du skapa den med hjälp av dessa instruktioner.
* **[!UICONTROL Customer's first order's medium]**: Ordern är ett medium från en kunds första order. Kontrollera först om du har en kolumn med namnet `customer's first order's source` i ditt konto. Om den här kolumnen inte visas kan du skapa den med hjälp av dessa instruktioner.
* **[!UICONTROL Customer's first order's campaign]**: Orderns kampanj från en kunds första order. Kontrollera först om du har en kolumn med namnet `customer's first order's source` i ditt konto. Om den här kolumnen inte visas kan du skapa den med hjälp av dessa instruktioner.

## Vanliga rapporter och mätvärden

Här är några vanliga exempel på rapporter och mätvärden som du kan använda:

* [Kundanalys](#customeranalytics)
* [Orderanalys](#orderanalytics)
* [Marknadsföringsanalys](#mktgspendanalytics)

## Kundanalys {#customeranalytics}

### Nya användare

* **Beskrivning**: Antal nyförvärvade användare under en viss tidsperiod. `New Users` skiljer sig från `Unique Customers`, eftersom `New Users` har en tidsstämpel som ett konto skapades med din tjänst (detta innebär inte att de nödvändigtvis har gjort en beställning) medan `Unique Customers` har placerat minst en order.
* **Måttdefinition**: Detta mått utför en **Antal** av `entity_id` från `customer_entity` tabell sorterad efter `created_at`.
* **Rapportexempel**: Antal nya användare som skapades förra månaden
   * **[!UICONTROL Metric]**: `New Users`
   * **[!UICONTROL Time Range]**: `Last Month`
   * **[!UICONTROL Time Interval]**: `By Day`

![Nya användare](../../assets/New_Users_Last_Month.png)<!--{: width="929"}-->

### Unika kunder

* **Beskrivning**: Antal distinkta kunder under en viss tidsperiod. Det här skiljer sig från `New Users`eftersom det bara spårar kunder som har gjort minst en beställning. En rapport över distinkta kunder spårar bara en kund en gång inom ett givet tidsintervall. Om du anger tidsintervallet till `By Day` och en kund gör mer än ett inköp den dagen räknas kunden bara en gång. Om du vill se det totala antalet inköp ska du titta på `Number of Orders`.
* **Måttdefinition**: Detta mått utför en **Distinkt antal** av `customer_id` från `sales_flat_order` tabell sorterad efter `created_at`.
* **Rapportexempel**: Distinkta kunder per vecka under de senaste 90 dagarna
   * **[!UICONTROL Metric]**: `Distinct Customers`
   * **[!UICONTROL Time Range]**: `Moving range > Last 90 Days`
   * **[!UICONTROL Time Interval]**: `By Day`

![Unika kunder.](../../assets/Unique_customers_last_7_days.png)<!--{: width="929"}-->

### Nya prenumeranter

* **Beskrivning**: Antal nya abonnenter som förvärvats under en viss tidsperiod.
* **Måttdefinition**: Detta mått utför en **Distinkt antal** av `customer_id` från `subscriptions` tabell sorterad efter `start_date`.
* **Rapportexempel**: Nya prenumeranter detta år efter månad
   * **[!UICONTROL Metric]**: `New Subscribers`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 0 Days Ago`
   * **[!UICONTROL Time Interval]**: `By Month`

![Prenumeranter](../../assets/New_Subscribers_This_Year_by_Month.png)<!--{: width="929"}-->

### Upprepa kunder

* **Beskrivning**: Det totala antalet kunder som beställt mer än en order under en tidsperiod. I en rapport om återkommande kunder kan du använda `Distinct Customers` mätvärden och `Customer's Order Number` från `orders` tabell.
* **Mått som används**: `Distinct Customers`
* **Exempel på rapporter**: Antal inköp 2 och 3 förra året
   * **[!UICONTROL Metric]**: `Distinct Customers`
   * **[!UICONTROL Time Range]**: `Moving Range > Last Year`
   * **[!UICONTROL Time Interval]**: `By Month`
   * **[!UICONTROL Group By]**: `Customer's Order Number`väljer `2` och `3`

   ![](../../assets/2nd_and_3rd_purchases_last_year.png)

* **Exempel 2**: Antal återkommande kunder förra året
   * **[!UICONTROL Metric]**: `Distinct Customers`
   * **[!UICONTROL Filters]**: `Customer's Order Number Greater Than 1`
   * **[!UICONTROL Time Range]**: `Moving range > Last Year`
   * **[!UICONTROL Time Interval]**: `By Month`

   ![Upprepa kunder förra året](../../assets/Repeat_customers_last_year.png)<!--{: width="929"}-->

### De vanligaste kunderna efter antal order som gäller hela livet

* **Beskrivning**: En lista över de främsta kunderna baserat på deras totala antal order. Detta ger er en direkt lista över era mest frekventa kunder.
* **Mått som används**: `Orders`
* **Rapportexempel**: De 25 största kunderna efter antal order som gäller under hela löptiden
   * **[!UICONTROL Metric]**: `Orders`
   * **[!UICONTROL Time Range]**: `All Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By]**: `customer_email`
   * **[!UICONTROL Show Top/Bottom]**: Top 25 sorted by Orders

   ![Top 25 Customers by Orders](../../assets/Top_25_customers_by_lifetime_orders.png)<!--{: width="929"}-->

### De främsta kunderna efter livstidsintäkter

* **Beskrivning**: En lista över de främsta kunderna baserad på livstidsintäkter.
* **Mått som används**: `Average Lifetime Revenue`
* **Exempel på rapporter**: Top 25 customers by Lifetime Revenue
   * **[!UICONTROL Metric]**: `Average Lifetime Revenue`
   * **[!UICONTROL Time Range]**: `All time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By]**: `customer_email`
   * **[!UICONTROL Show Top Bottom]**: Top 25 sorted by Lifetime Revenue

   ![De 25 bästa kunderna per intäkt](../../assets/top_25_customers_by_lifetime_revneue.png)<!--{: width="929"}-->

### Genomsnittlig intäkt för livstid per kohort

* **Beskrivning**: Spåra [genomsnittliga livstidsintäkter för distinkta kohorter](../dev-reports/lifetime-rev-cohort-analysis.md) av användare över tiden för att identifiera de mest högpresterande kohorterna. Kohorter grupperas tillsammans efter ett vanligt datum, till exempel första orderdatum eller skapandedatum.
* **Mått som används**: `Revenue`
* **Exempel på rapporter**: Genomsnittlig avkastning på kundens livstid per kohort
   * **[!UICONTROL Metric]**: `Revenue`
   * **[!UICONTROL Cohort Date]**: `Customer's first order date`
   * **[!UICONTROL Time Interval]**: `Month`
   * **[!UICONTROL Time Period]**: Glidande kohorter i de senaste 8 kohorterna med minst 4 månaders data
   * **[!UICONTROL Duration]**: `12 Month(s)`
   * **[!UICONTROL Table]**: `Customer_entity`
   * **[!UICONTROL Perspective]**: Ackumulerat medelvärde per kohortmedlem

   ![Customer Lifetime Revenue by Cohort](../../assets/Avg_customer_lifetime_revenue_by_cohort.png)<!--{: width="929"}-->

### Kunder efter kuponganvändning

* **Beskrivning**: Antal köpta kunder som har använt en kupong/rabattkod. Detta kan hjälpa er att få en tydlig bild av era rabattsökande jämfört med fullprisköparna.
* **Mått som används**: `New Users`
* **Exempel på rapporter**: Kupong och icke-kupongkunder per månad
   * **[!UICONTROL Metric A]**: `Non coupon customers`
   * **[!UICONTROL Metric]**: `New Users`
   * **[!UICONTROL Filters]**: Kundens livstid Antal beställningar som är större än 0 och kundens livstid Antal kuponger som är lika med 0
   * **[!UICONTROL Metric B]**: `Coupon customers`
   * **[!UICONTROL Metric]**: `New Users`
   * **[!UICONTROL Filters]**: Kundernas livstid Antal beställningar som är större än 0 och kundens livstid Antal kuponger som är större än 0
   * **[!UICONTROL Time range]**: `All Time`
   * **[!UICONTROL Time interval]**: `By Month`

   ![Kunder efter kuponganvändning](../../assets/Customers_by_coupon_usage.png)<!--{: width="929"}-->

* **Exempel 2**: Procent av kupongkunder och icke-kupongkunder per månad
   * **[!UICONTROL Metric A]**: `Non coupon customers` (dölj mått)
      * **[!UICONTROL Metric]**: `New Users`
      * **[!UICONTROL Filters]**: `Customer's Lifetime Number of Orders Greater Than 0` och `Customer's Lifetime Number of Coupons Equal to 0`
   * **[!UICONTROL Metric B]**: `Coupon customers`
      * **[!UICONTROL Metric]**: `New Users`
      * **[!UICONTROL Filters]**: `Customers Lifetime Number of Orders Greater Than 0` och `Customer's Lifetime Number of Coupons Greater Than 0`
   * **[!UICONTROL Time Range]**: `All Time`
   * **[!UICONTROL Time Interval]**: `By Month`
   * **[!UICONTROL Formula]**: `B/(A+B)`

>[!NOTE]
>
> **Dölj alla mått**

![Kuponganvändning](../../assets/Customers_by_coupon_usage_formula.png)<!--{: width="929"}-->

### Genomsnittlig intäkt under de första 30 dagarna

* **Beskrivning**: Genomsnittligt intäktsbelopp som genererats av kunder som kund under de första 30 dagarna.
* **Måttbeskrivning**: Det här måttet utför en **Genomsnittlig** av `Customer's First 30 Day Revenue` från `customer_entity` tabell sorterad efter `created_at`.
* **Rapportbeskrivning**: Heltidsgenomsnitt av kundens första 30-dagars intäkter
* **[!UICONTROL Metric]**: `Average First 30 Day Revenue`
* **[!UICONTROL Time Range]**: `All Time`
* **[!UICONTROL Time Interval]**: `None`

![Genomsnittlig första 30-dagars intäkt](../../assets/Avg_first_30_day_revenue.png)<!--{: width="929"}-->

### Genomsnittlig omsättning för kundens livslängd

* **Beskrivning**: Det genomsnittliga intäktsbelopp som genereras av era kunder under deras livstid.
* **Måttbeskrivning**: Detta mått utför en **Genomsnittlig** i `Customer's Lifetime Revenue` kolumn på `customer_entity` tabell baserad på `created_at`.
* **Rapportbeskrivning**: Heltidsgenomsnitt av kundens livstidsintäkter
   * **[!UICONTROL Metric]**: `Average Customer Lifetime Revenue`
   * **[!UICONTROL Time Range]**: `All Time`
   * **[!UICONTROL Time Interval]**: `None`

![Kundens livstidsintäkt](../../assets/Avd_customer_lifetime_revenue_.png)<!--{: width="929"}-->

## Orderanalys {#orderanalytics}

### Intäkter

* **Beskrivning**: Inkomstmåttet visar den totala intäkten under en vald tidsperiod.
* Den här mätningen utför en **summa** av `grand_total` från `sales_flat_order` tabell sorterad efter `created_at`.
* **Rapportexempel**: Intäkter per månad, hittills i år
   * **[!UICONTROL Metric]**: `Revenue`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 1 Month Ago`
   * **Tidsintervall**: `By Month`

>[!TIP]
>
>Kontrollera att beräkningen av dina intäkter överensstämmer med definitionen som du diskuterar internt. Du kanske bara vill räkna av intäkter från order som har levererats, du kanske måste konvertera valutor från olika regioner och du kanske vill exkludera moms. Dessutom kan du använda [Filteruppsättningar](../../data-user/reports/ess-manage-data-filters.md) för att säkerställa enhetlighet i alla mätvärden som bygger på samma tabell.

![Intäkter](../../assets/revenue.png)<!--{: width="929"}-->

### Beställningar

* **Beskrivning**: Antal order under en viss tidsperiod. I en beställningsrapport spåras förändringar i ordervolym som orsakas av nya erbjudanden, kampanjer eller annat som kan öka (eller minska) transaktionsvolymen. Du kanske ofta vill segmentera detta mått med ett antal variabler för att besvara dina frågor.
* **Måttdefinition**: Detta mått utför en **Antal** av `entity_id` från `sales_flat_order` tabell sorterad efter `created_at`.
* **Exempel på rapporter**: Beställningar per månad, hittills i år
   * **[!UICONTROL Metric]**: `number of orders`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 1 Month Ago`
   * **[!UICONTROL Time Interval]**: `By Month`

>[!TIP]
>
>Precis som intäktsmätaren borde du ha [Filteruppsättningar](../../data-user/reports/ess-manage-data-filters.md) på plats för att exkludera ofullständiga, testade eller returnerade order.

![Beställningar](../../assets/orders_pic.png)<!--{: width="929"}-->

### Beställda produkter

* **Beskrivning**: De beställda produkterna anger hur många artiklar som sålts under en viss tidsperiod.
* **Måttdefinition**: Den här mätningen utför en **summa** av `qty_ordered` från `sales_flat_order_item` tabell sorterad efter `created_at`.
* **Exempel på rapporter**: Artiklar som säljs per månad, hittills i år
   * **[!UICONTROL Metric]**: `Products ordered`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 1 Month Ago`
   * **[!UICONTROL Time Interval]**: `By Month`

   ![Beställda produkter](../../assets/products_ordered_pic1.png)<!--{: width="929"}-->

* Kombinera det här måttet med antalet order för att beräkna antalet artiklar per order. Därefter lägger du till kupongkoder i rapporten för att avgöra hur era kampanjer påverkar kundvagnsstorlek eller segmentera efter nya eller upprepade order för att få en bättre förståelse för kundbeteendet.
* **Exempel på rapporter**: Produkter per beställning: Första ordern eller upprepade order
   * **[!UICONTROL Metric A]**: Beställda produkter: Första beställningen
      * **[!UICONTROL Metric]**: `Products ordered`
      * **[!UICONTROL Filter]**: `Customer's order number = 1`
   * **[!UICONTROL Metric B]**: Beställningar: Första beställningen
      * **[!UICONTROL Metric]**: `Orders`
      * **[!UICONTROL Filter]**: `Customer's order number = 1`
   * **[!UICONTROL Metric C]**: Beställda produkter: upprepa order
      * **[!UICONTROL Metric]**: `Products ordered`
      * **[!UICONTROL Filter]**: `Customer's order number > 1`
   * **[!UICONTROL Metric D]**: Beställningar: Upprepa order
      * **[!UICONTROL Metric]**: `Orders`
      * **[!UICONTROL Filter]**: `Customer's order number > 1`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 1 Month Ago`
   * **[!UICONTROL Time Interval]**: `By Week`
   * **[!UICONTROL Formula 1]**: `A/B`
   * **[!UICONTROL Formula 2]**: `C/D`

>[!NOTE]
>
>Avmarkera `Multiple Y-Axes box` och `Hide` alla mått

![Beställda produkter 2](../../assets/products_ordered_pic2.png)<!--{: width="929"}-->

### Genomsnittligt ordervärde

* **Beskrivning**: Spåra genomsnittsvärdet för beställningar som gjorts under en tidsperiod. Använd detta mätvärde för att snabbt avgöra hur ert genomsnittliga ordervärde (AOV) har fluktuerat till följd av era marknadsföringssatsningar, erbjudanden och/eller andra förändringar i ert företag.
* **Måttdefinition**: Det här måttet utför en **medel** av `grand_total` från `sales_flat_order` tabell sorterad efter `created_at`.
* **Exempel på rapporter**: AOV jämfört med föregående år, hittills i år
   * **[!UICONTROL Metric]**: `Average order value`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 1 Month Ago`
   * **[!UICONTROL Time Interval]**: `By Month`
   * **[!UICONTROL Perspective]**: `Amount Change vs Previous Year`

   ![AOV](../../assets/aov_pic.png)<!--{: width="929"}-->

### Produkter som köpts mest med kuponger

* **Beskrivning**: Den här rapporten innehåller information om vilka produkter som säljs när du erbjuder kampanjer eller kuponger.
* **Använda mått**: Beställda produkter
* **Exempel på rapporter**: Produkter som köpts mest med kuponger
   * **[!UICONTROL Metric]**: `Products ordered`
   * **[!UICONTROL Filter]**: `Order's coupon_code Is Not \[NULL\]`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By**]: `name` (eller `SKU`eller någon annan produkt-id)
   * **[!UICONTROL Show top/bottom]**: Top 25 sorted by Products ordered

   ![Produkter med kuponger](../../assets/prod_coupons_pic.png)<!--{: width="929"}-->

### Tid mellan order

* **Beskrivning**: Testa era antaganden och förväntningar om era kunders inköpscykler med en **tid mellan order** analys som tittar på medelvärdet (eller medianen!) tiden mellan köp. I tabellen nedan ser du att era bästa kunder - de som beställer mer än tre - gör sitt andra köp på mindre än sex månader. Kunder som inte gjort en fjärde beställning väntar 14 månader innan de gör ett andra köp.
* **Måttdefinition**: Det här måttet utför en **medel** av `Time since previous order` från `sales_flat_order` beställd av `created_at`.
* **Exempel på rapporter**:
   * **Mått 1**: ≤ 3 order
      * **[!UICONTROL Metric]**: `Average time between orders`
      * **[!UICONTROL Filter]**: `Customer's lifetime number of orders ≤ 3`
   * **Mått 2**: > 3 order
      * **[!UICONTROL Metric]**: `Average time between orders`
      * **[!UICONTROL Filter]**: `Customer's lifetime number of orders > 3`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By]**:` Customer's order number (previous-current)`

>[!NOTE]
>
>Avmarkera `Multiple Y-Axes` box.

![Tid mellan order](../../assets/time_bw_orders_pic.png)<!--{: width="929"}-->

## Analys av marknadsföringsutgifter {#mktgspendanalytics}

### Annonsutgift

* **Beskrivning**: Ni kan analysera era marknadsföringsutgifter över olika tidsperioder och intervall, med kampanjer, annonsuppsättningar eller andra segmenteringar.
* **Måttdefinition**: Det här måttet utför en summa på utgiftskolumnen i `Marketing Spend` tabellen sorterad efter `date` kolumn.
* **Rapportexempel**: Annonsutgift per kampanj
   * **[!UICONTROL Metric]**: `Ad spend`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By]**: `campaign`

![Annonskostnader](../../assets/ad_spend.png)<!--{: width="929"}-->

### Annonsvisningar och reklamklick

* **Beskrivning**: Förutom att analysera annonskostnaderna kan ni analysera annonsintrycket och annonsklickningarna.
* **Måttdefinition**: Det här måttet utför en summa på kolumnen för avtryck (eller klick) i `Marketing Spend` tabellen sorterad efter datumkolumnen.
* **Rapportexempel**: Lägg till intryck och annonsklickningar per dag
   * **[!UICONTROL Metric A]**: `Ad impressions`
   * **[!UICONTROL Metric B]**: `Ad clicks`
   * **[!UICONTROL Time Range]**: `1 Year Ago to 3 Months Ago`
   * **[!UICONTROL Time Interval]**: `By Day`

   ![Annonsexponeringar](../../assets/ad_impressions.png)<!--{: width="929"}-->

### Klickfrekvens (CTR)

* **Beskrivning**: Med hjälp av de annonsvisningar och reklamklickningar du har skapat ovan kan du analysera hur klickfrekvens du har valt mellan olika kampanjer över tiden.
* **Rapportexempel**: CTR per kampanj
   * **[!UICONTROL Metric A]**: `Ad impressions`
   * **[!UICONTROL Metric B]**: `Ad clicks`
   * **[!UICONTROL Time Range]**:`All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Formula]**: `B/A`
   * Välj `%` alternativ.
   * **[!UICONTROL Group By]**: `campaign`

>[!NOTE]
>
>Du kan **title** formeln som `CTR`och **hide** alla mätvärden.

![CTR](../../assets/CTR.png)<!--{: width="929"}-->

### Kostnad per klick (CPC)

* **Beskrivning**: Med hjälp av mätvärdena för annonskostnaderna och annonsklickningarna ovan kan ni analysera kostnaden per klick med olika kampanjer över tiden.
* **Rapportexempel**: CPC efter kampanj
   * **[!UICONTROL Metric A]**: `Ad spend`
   * **[!UICONTROL Metric B]**: `Ad clicks`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Formula]**: `A/B`
   * Välj `currency` option
   * **[!UICONTROL Group By]**: `campaign`

>[!NOTE]
>
>Du kan **title** formeln som `CPC`och **hide** alla mätvärden.

![CPC](../../assets/CPC.png)<!--{: width="929"}-->

### Kunder efter anskaffningskälla

* **Beskrivning**: Om du spårar källan, mediet och kampanjen för en order med [!DNL Google eCommerce]kan ni analysera kunderna utifrån deras anskaffningskälla. Detta hjälper er att identifiera vilka marknadsföringskällor som förvärvar kunder och svara på frågor som&quot;är de flesta av era kunder som gör sina första beställningar via [!DNL Google], [!DNL Facebook]eller någon annan källa?&quot;
* **Rapportexempel**: Kunder efter anskaffningskälla
   * **[!UICONTROL Metric Used]**: `New Customers`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `By Month`
   * **[!UICONTROL Group By]**: `Customer's first order's source`

>[!NOTE]
>
>Checka ut [den här artikeln](../analysis/most-value-source-channel.md) om du vill ha fler exempel på rapporter med hjälp av anskaffningskälla.

![Anskaffningskälla](../../assets/acquisition_source.png)<!--{: width="929"}-->

### Kunder per förvärvsmedium och förvärvskampanj

* **Beskrivning**: På samma sätt som när ni analyserar kunder via anskaffningskälla kan ni också analysera kunderna utifrån deras första beställningsmedium och kampanj. Detta kan hjälpa er att svara på frågor som&quot;vilka kampanjer lockar nya kunder?&quot;
* **Rapportexempel**: Kunder efter anskaffningskampanj med betalt medium
   * **[!UICONTROL Metric Used]**: `New customers`
   * **[!UICONTROL Filter]**: `Customer's first order's medium IN ppc`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By]**: `Customer's first order's campaign`

>[!NOTE]
>
>För filtret i `New Customers` kan du lägga till andra medier som betraktas som&quot;betalda&quot; medier för ditt företag, till exempel cpc eller betalsökningar.

![Medelvärvning](../../assets/acquisition_medium.png)<!--{: width="929"}-->

### Kundanskaffningskostnad (CAC) eller kostnad per förvärv (CPA)

* **Beskrivning**: Ett sätt att analysera kostnaden för en kampanj är att attribuera alla kostnader till enbart de kunder som ni förvärvat via kampanjen.
* **Rapportexempel**: CAC per kampanj
   * **[!UICONTROL Metric A]**: `New customers`
   * **[!UICONTROL Filter]**: `Customer's first order's medium IN ppc`
   * **[!UICONTROL Metric B]**: `Ad Spend`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Formula]**: `B/A`
   * Välj `currency` option
   * **[!UICONTROL Group By]**:
      * För mått `A`, markera `Customer's first order's campaign`
      * För mått `B`, markera `campaign`

   ![Nya användare.](../../assets/New_Users_Last_Month.png)

>[!NOTE]
>
>Du kan **title** formeln som `CTR`och **hide** alla mätvärden. Du kan även checka ut [den här artikeln](../analysis/roi-ad-camp.md) för mer information.

![CAC 1](../../assets/New_Users_Last_Month.png)

![CAC 2](../../assets/cac-2.png)

### Livstidsvärde per anskaffningskälla, medium och kampanj

* **Beskrivning**: Förutom att analysera antalet kunder som förvärvats av varje kampanj kan ni analysera dessa kunders genomsnittliga livstidsintäkter. Detta hjälper dig att identifiera:
   * Om vissa kampanjer lockar många kunder, men dessa kunder har en låg livstid.
   * Om vissa kampanjer lockar ett lågt antal kunder, men dessa kunder har ett högt livstidsvärde.
* **Rapportexempel**: Lägg först till `New customers` mätvärden. Lägg sedan till `Average lifetime revenue` mätvärden. Markera önskad tidsram och välj `interval` as `None`. Slutligen väljer du `group by` option as`Customer's first order's campaign`.
   * **[!UICONTROL Metric A]**: `New Customers`
   * **[!UICONTROL Filter A]**: `Customer's first order's source` LIKE &#39;%google%&#39;
   * **[!UICONTROL Filter B]**: `Customer's first order's medium IN ppc`
   * **[!UICONTROL Metric B]**: `Average lifetime revenue`
   * **[!UICONTROL Filter A]**: `Customer's first order's source` LIKE &#39;%google%&#39;
   * **[!UICONTROL Filter B]**: `Customer's first order's medium IN ppc`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Group By]**: `Customer's first order's campaign`

>[!NOTE]
>
>För de två filtren kan du lägga till andra medier som betraktas som&quot;betalda&quot; medier för ditt företag, till exempel cpc eller betalsökningar, och du kan lägga till andra källor som du vill analysera, till exempel Facebook. Du kan även checka ut [den här artikeln](../analysis/roi-ad-camp.md) för mer information om CAC, LTV och ROI.

![Livstidsvärde per anskaffningskälla, medium och kampanj](../../assets/LTV_2.png)<!--{: width="929"}-->

### Avkastning på investering

* **Beskrivning**: Ett sätt att beräkna avkastningen per kampanj är att analysera alla order som läggs genom kampanjen. Men en alternativ metod är att analysera livstidsvärdet för kunder som förvärvats via en kampanj. För att analysera avkastningen är det viktigt att kampanjnamnen är enhetliga i alla era utgiftsdata och transaktionsdata. Om du skapar följande rapport och det inte finns några ROI-värden på grund av felmatchade kampanjnamn kan du behöva titta i [UTM-taggning](../../best-practices/utm-tagging-google.md) du har implementerat.
* **Rapportexempel**: avkastning per kampanj
   * **[!UICONTROL Metric A]**: `New Customers`
   * **[!UICONTROL Filter A]**: `Customer's first order's source` LIKE &#39;%google%&#39;
   * **[!UICONTROL Filter B]**: `Customer's first order's medium IN ppc`
   * **[!UICONTROL Metric B]**: `Average lifetime revenue`
   * **[!UICONTROL Filter A]**: `Customer's first order's source` LIKE &#39;%google%&#39;
   * **[!UICONTROL Filter B]**: `Customer's first order's medium IN ppc`
   * **[!UICONTROL Metric C]**: `Ad spend`
   * **[!UICONTROL Time Range]**: `All-Time`
   * **[!UICONTROL Time Interval]**: `None`
   * **[!UICONTROL Formula]**: `(B-(C/A))/(C/A)`
   * Välj `% `option
   * **[!UICONTROL Group By]**:
      * För mått `A` och `B`, markera `Customer's first order's campaign`
      * För mått `C`, markera `campaign`

>[!NOTE]
>
>Du kan namnge formeln som&quot;ROI&quot; och dölja alla mått. Dessutom kan du justera filtren i mätvärdena för att analysera alternativa källor och medier. Du kan även checka ut [den här artikeln](../analysis/roi-ad-camp.md) för mer information om CAC, LTV och ROI.

![avkastning 1](../../assets/ROI_1.png)<!--{: width="929"}-->

![avkastning 2](../../assets/ROI_2.png)<!--{: width="929"}-->
