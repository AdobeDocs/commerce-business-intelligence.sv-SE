---
title: Analys av senaste, frekvenser, monetära tillgångar (RFM)
description: Lär dig hur du skapar en kontrollpanel där du kan segmentera kunderna utifrån deras senaste, frekventa och monetära rankningar.
exl-id: 8f0f08fd-710b-4810-9faf-3d0c3cc0a25d
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 0%

---

# RFM-analys

I den här artikeln beskrivs hur du skapar en instrumentpanel där du kan segmentera kunderna utifrån deras senaste, frekventa och monetära rankningar. RFM-analys är en marknadsföringsteknik som tar hänsyn till kundbeteenden för att hjälpa er att bestämma segmentering för utåtriktad marknadsföring. Den omfattar tre aspekter:

* Hur nyligen en kund har köpt från din butik
* Hur ofta de köper från dig
* Pengar in hur mycket kunden spenderar

![](../../assets/blobid0.png)

RFM-analysen kan bara konfigureras om du har [!DNL MBI] Pro-plan för den nya arkitekturen (om du till exempel har alternativet &quot;Vyer i Data warehouse&quot; på menyn &quot;Hantera data&quot;). Dessa kolumner kan skapas från sidan Hantera data > Data warehouse. Detaljerade instruktioner finns nedan.

## Komma igång

Du måste först överföra en fil som bara innehåller en primärnyckel med värdet 1. Detta gör att du kan skapa vissa nödvändiga beräknade kolumner för analysen.

Du kan använda den här [hjälpcenterartikel](../importing-data/connecting-data/using-file-uploader.md) och bilden nedan för att formatera filen.

## Beräknade kolumner

Ytterligare en skillnad görs om ditt företag tillåter gästbeställningar. I så fall kan du ignorera alla steg för `customer_entity` tabell. Om gästorder inte tillåts, ignorera alla steg för `sales_flat_order` tabell.

Kolumner att skapa

* **`Sales_flat_order/customer_entity`** table
* `Customer's last order date`
* [!UICONTROL Column type]: `Many to one > Max`
* [!UICONTROL Pat]: `sales_flat_order.customer_id > customer_entity.entity_id`
* Markerad [!UICONTROL column]: `created_at`
* [!UICONTROL Filter]: `Orders we count`

* 

       Sekunder sedan kundens senaste orderdatum
   * [!UICONTROL Column type]: - &quot;Samma tabell > Ålder
* Markerad [!UICONTROL column]: `Customer's last order date`

* (input) Count reference reference
* [!UICONTROL Column type]: `Same table > Calculation`
* 
   [!UICONTROL-indata]: `entity_id`
* [!UICONTROL Calculation]: `**case when A is null then null else 1 end**`
* 

   [!UICONTROL-datatyp]: `Integer`

* **Räkningsreferens** table (this is the file you uploaded with the number &quot;1&quot;)
* Antal kunder
* [!UICONTROL Column type]: `Many to One > Count Distinct`
* [!UICONTROL Path]: `ales_flat_order.(input) reference > Count reference.Primary Key` ELLER `customer_entity.(input)reference > Count Reference`. `Primary Key`
* Markerad [!UICONTROL column]: `sales_flat_order.customer_email` ELLER `customer_entity.entity_id`

* **Customer_entity** table
* Antal kunder
* [!UICONTROL Column type]: `One to Many > JOINED_COLUMN`
* [!UICONTROL Path]: `customer_entity`.(input) reference > Customer Concentration. `Primary Key`
* Markerad [!UICONTROL column]: `Number of customers`

* (indata) `Ranking by customer lifetime revenue`
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Customer's lifetime revenue`

* Rankning efter kundens livstidsintäkt
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: `case when A is null then null else (B-(A-1)) end`
* 

   [!UICONTROL-datatyp]: `Integer`

* Kundens monetära poäng (i procent)
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: `Case when round((B-A+1)*100/B,0) <= 20 then 5 when round((B-A+1)*100/B,0) <= 40 then 4 when round((B-A+1)*100/B,0) <= 60 then 3 when round((B-A+1)*100/B,0) <= 80 then 2 when round((B-A+1)*100/B,0) <= 100 then 1 else 0 end`
* 

   [!UICONTROL-datatyp]: `Integer`

* (input) Rankning per kundens livstid antal order
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Customer's lifetime number of orders`

* Rankning efter kundens livstidsantal order
* 
   [!UICONTROL-kolumntyp]: – "Samma tabell > Beräkning"
* [!UICONTROL Inputs]: - **(input) Rankning per kundens livstid antal order**, **Antal kunder**
* [!UICONTROL Calculation]: - **case when A is null then null else (B-(A-1)) end**
* [!UICONTROL Datatype]: - heltal

* Kundens frekvenspoäng (per percentiler)
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime number of orders`, `Number of customers`
* [!UICONTROL Calculation]: `Case when round((B-A+1)*100/B,0) <= 20 then 5 when round((B-A+1)*100/B,0) <= 40 then 4 when round((B-A+1)*100/B,0) <= 60 then 3 when round((B-A+1)*100/B,0) <= 80 then 2 when round((B-A+1)*100/B,0) <= 100 then 1 else 0 end`
* 

   [!UICONTROL-datatyp]: `Integer`

* Ordna efter sekunder sedan kundens senaste orderdatum
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Seconds since customer's last order date`

* Kundens senaste poäng (i procent)
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime number of orders`, `Number of customers`
* [!UICONTROL Calculation]: `Case when (A * 100/B,0) <= 20 then 5 when (A * 100/B,0) <= 40 then 4 when (A * 100/B,0) <= 60 then 3 when (A * 100/B,0) <= 80 then 2 when (A * 100/B,0) <= 100 then 1 else 0 end`
* 

   [!UICONTROL-datatyp]: `Integer`

* Kundens senaste poäng (i procent)
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `Customer's recency score (by percentiles)`, `Customer's frequency score (by percentiles)`, `Customer's monetary score (by percentiles)`
* [!UICONTROL Calculation]: `case when (A IS NULL or B IS NULL or C IS NULL) then null else concat(A,B,C) end`
* 

   [!UICONTROL-datatyp]: String

* **Räkningsreferens** table
* [!UICONTROL Number of customers]: `(RFM > 0)`
* [!UICONTROL Column type]: `Many to One > Count Distinct`
* [!UICONTROL Path]: `sales_flat_order.(input) reference > Customer Concentration. Primary Key` ELLER `customer_entity.(input)reference > Customer Concentration.Primary Key`
* Markerad [!UICONTROL column]: `sales_flat_order.customer_email` ELLER `customer_entity.entity_id`
* [!UICONTROL Filter]: `Customer's RFM score (by percentile)` Inte lika med 000

* **Customer_entity** table
* [!UICONTROL Number of customers]: `(RFM > 0)`
* [!UICONTROL Column type]: `One to Many > JOINED_COLUMN`
* [!UICONTROL Path]: `customer_entity.(input) reference > Customer Concentration.Primary Key`
* Markerad [!UICONTROL column]: - `Number of customers`

* Kundens senaste poäng `(R+F+M)`
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: – `Customer's recency score (by percentiles)`, `Customer's frequency score (by percentiles)`, `Customer's monetary score (by percentiles)`
* [!UICONTROL Calculation]: `case when (A IS NULL or B IS NULL or C IS NULL) then null else A+B+C end`
* 

   [!UICONTROL-datatyp]: `Integer`

* (input) Rankning by customer&#39;s overall RFM score
* [!UICONTROL Column type]: `Same table > Event Number`
* [!UICONTROL Event owner]: `(input) reference for count`
* [!UICONTROL Event rank]: `Customer's recency score (R+F+M)`
* [!UICONTROL Filter]: `Customer's RFM score (by percentile)` Inte lika med 000

* Rankning efter kundens totala RFM-poäng
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer's overall RFM score`, `Number of customers (RFM > 0)`
* [!UICONTROL Calculation]: `case when A is null then null else (B-(A-1)) end`
* 

   [!UICONTROL-datatyp]: `Integer`

* Kundens RFM-grupp
* [!UICONTROL Column type]: `Same table > Calculation`
* [!UICONTROL Inputs]: `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: `Case when round(A * 100/B,0) <= 20 then '5. copper' when round(A * 100/B,0) <= 40 then '4. bronze' when round(A * 100/B,0) <= 60 then '3. silver' when round(A * 100/B,0)<= 80 then '2. gold' else '1. Platinum' end`
* 

   [!UICONTROL-datatyp]: `Integer`

>[!NOTE]
>
>De percentiler som används är till och med delar av kunderna (till exempel 20 % för att returnera 1-5). Om du har ett anpassat sätt att väga dessa kan du meddela analytikern när du skickar in biljetten.

## Mått

Inga nya mätvärden!

**Anteckning**: Se till att [lägga till alla nya kolumner som dimensioner till mått](../data-warehouse-mgr/manage-data-dimensions-metrics.md) innan du skapar nya rapporter.

## Rapporter

* **Kunder efter RFM-gruppering**
* Mått `A`: `New customers`
* [!UICONTROL Metric]: `New customers`
* [!UICONTROL Filter]: `Customer's RFM score (by percentiles) Not Equal to 000`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* Dölj diagram
* [!UICONTROL Group by]: `Customer's RFM group`
* 
   [!UICONTROL Group by]: `Email`
* 

   [!UICONTROL Chart type]: `Table`

* **Kunder med fem senaste poäng**
* Mått `A`: `New customers`
* [!UICONTROL Metric]: `New customers`
* [!UICONTROL Filter]: `Customer's recency score (by percentiles) Equal to 5`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 
   [!UICONTROL Chart Type]: `Scalar`
* Dölj diagram
* 
   [!UICONTROL Group by]: `Email`
* [!UICONTROL Group by]: `Customer's RFM score (R+F+M)`
* 

   [!UICONTROL Chart type]: `Table`

* **Kunder med en senaste poäng**
* Mått `A`: `New customers`
* [!UICONTROL Metric]: `New customers`
* [!UICONTROL Filter]: `Customer's recency score (by percentiles) Equal to 1`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 
   [!UICONTROL Chart Type]: `Scalar`
* Dölj diagram
* 
   [!UICONTROL Group by]: `Email`
* [!UICONTROL Group by]: `Customer's RFM score (R+F+M)`
* 

   [!UICONTROL Chart type]: `Table`

När du har kompilerat alla rapporter kan du ordna dem på kontrollpanelen som du vill. Resultatet kan se ut som exempelinstrumentpanelen ovan, men de tre genererade tabellerna är bara exempel på den typ av kundsegmentering du kan utföra.
