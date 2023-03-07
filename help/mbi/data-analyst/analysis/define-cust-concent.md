---
title: Definiera kundkoncentration
description: Lär dig hur du skapar en kontrollpanel som hjälper dig att mäta hur de totala intäkterna fördelas mellan era kunder.
exl-id: 6242019f-a6a5-48d3-b214-94acd7842e00
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# Kundkoncentration

I den här artikeln beskrivs hur du ställer in en kontrollpanel som hjälper dig att mäta hur de totala intäkterna fördelas bland kunderna. Förstå vilken procentandel av kunderna som bidrar med vilken procentandel av intäkterna och skapar segmenterade listor på bästa möjliga marknad för och behåller era högkvalitativa kunder.

Denna analys innehåller [avancerade beräknade kolumner](../data-warehouse-mgr/adv-calc-columns.md).

## Komma igång

Du måste först överföra en fil som bara innehåller en primärnyckel med värdet 1. Detta gör att du kan skapa vissa nödvändiga beräknade kolumner för analysen.

Du kan använda [filöverföringen](../importing-data/connecting-data/using-file-uploader.md) och bilden nedan för att formatera filen.

## Beräknade kolumner

Om du använder den ursprungliga arkitekturen (till exempel om du inte har `Data Warehouse Views` alternativ under `Manage Data` ska du kontakta supportteamet för att bygga ut kolumnerna nedan. På den nya arkitekturen kan dessa kolumner skapas från `Manage Data > Data Warehouse` sida. Detaljerade instruktioner finns nedan.

Ytterligare en skillnad görs om ditt företag tillåter gästbeställningar. I så fall kan du ignorera alla steg för `customer_entity` tabell. Om gästorder inte tillåts, ignorera alla steg för `sales_flat_order` tabell.

Kolumner att skapa

* `Sales_flat_order/customer_entity` table
* (indata) `reference`
* [!UICONTROL Column type]: – `Same table > Calculation`
* [!UICONTROL Inputs]: – `entity_id`
* [!UICONTROL Calculation]: - **case when A is null then null else 1 end**
* [!UICONTROL Datatype]: – `Integer`

* `Customer concentration` tabell (det här är filen som du överförde med numret) `1`)
* Antal kunder
* [!UICONTROL Column type]: – `Many to One > Count Distinct`
* Sökväg - `sales_flat_order.(input) reference > Customer Concentration.Primary Key` ELLER `customer_entity.(input)reference > Customer Concentration.Primary Key`
* Markerad kolumn - `sales_flat_order.customer_email` ELLER `customer_entity.entity_id`

* `customer_entity` table
* Antal kunder
* [!UICONTROL Column type]: – `One to Many > JOINED_COLUMN`
* Sökväg - `customer_entity.(input) reference > Customer Concentration. Primary Key`
* Markerad kolumn - `Number of customers`

* (indata) `Ranking by customer lifetime revenue`
* [!UICONTROL Column type]: – `Same table > Event Number`
* Ägare till händelse - `Number of customers`
* Händelserangordning - `Customer's lifetime revenue`

* Kundens intäktspunkt
* [!UICONTROL Column type]: – `Same table > Calculation`
* [!UICONTROL Inputs]: – `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: - **om A är null är null else (A/B)* 100 slut **
* [!UICONTROL Datatype]: – `Decimal`

* `Sales_flat_order` table
* Antal kunder
* [!UICONTROL Column type]: – `One to Many > JOINED_COLUMN`
* Sökväg - `sales_flat_order.(input) reference > Customer Concentration.Primary Key`
* Markerad kolumn - `Number of customers`

* (input) Rankning per kundens livstidsintäkt
* [!UICONTROL Column type]: – `Same table > Event Number`
* Ägare till händelse - `Number of customers`
* Händelserangordning - `Customer's lifetime revenue`
* Filter - `Customer's order number = 1`

* Kundens intäktspunkt
* [!UICONTROL Column type]: – `Same table > Calculation`
* [!UICONTROL Inputs]: – `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: - **om A är null är null else (A/B)* 100 slut **
* [!UICONTROL Datatype]: - `Decimal`

>[!NOTE]
>
>De percentiler som används är till och med delar av kunder, vilket representerar den sjätte percentilen av er kundbas. Varje kund är associerad med ett heltal mellan 1 och 100, som kan ses som en livstidsinkomst *rankning*. Om kundens intäktspolicy för en viss kund till exempel är **5**, den här kunden finns i ***femte percentilen*** av alla kunder i termer av livstidsintäkter.

## Mått

* **Totalt kundlivstidsvärde**
* I `customer_entity` table
* Detta mått utför en **Summa**
* På `Customer's lifetime revenue` kolumn
* Beställd av `Customer's first order date` tidsstämpel

## Rapporter

* **Kundkoncentration**
* [!UICONTROL Metric]: `Total customer lifetime value`
* [!UICONTROL Filter]: `Customer's revenue percentile IS NOT NULL`

* [!UICONTROL Metric]: `Total customer lifetime value`
* [!UICONTROL Filter]: `Customer's revenue percentile IS NOT NULL`

* 
   [!UICONTROL Group by]: `Independent`
* Mått `A`: `Total customer lifetime revenue by percentile`
* Mått `B`: `Total customer lifetime revenue (ungrouped)`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Customer's revenue percentile`
* Visa över/under: `100% of Customer's revenue percentile Name`
* 

   [!UICONTROL Chart type]: `Line`

* **Högsta koncentration på 10 %**
* [!UICONTROL Filter]: `Customer's revenue percentile <= 10`

* Mått `A`: `Total customer lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* Dölj diagram
* 
   [!UICONTROL Group by]: `Email`
* 

   [!UICONTROL Chart type]: `Table`

* **Lägsta 50 % koncentration med endast ett köp**

* Mått `A`: `Total customer lifetime revenue`
* `Customer's revenue percentile <= 50`
* `Customer's lifetime number of orders = 1`
* [!UICONTROL Filter]:

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* Dölj diagram
* 
   [!UICONTROL Group by]: `Email`
* 

   [!UICONTROL Chart type]: `Table`

* **Lägsta koncentration 10 %**
* [!UICONTROL Filter]: `Customer's revenue percentile > 90`

* Mått `A`: `Total customer lifetime revenue`
* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* Dölj diagram
* 
   [!UICONTROL Group by]: `Email`
* 

   [!UICONTROL Chart type]: `Table`

När du har kompilerat alla rapporter kan du ordna dem på kontrollpanelen som du vill. Resultatet kan se ut som kontrollpanelen ovan.

Om du stöter på några frågor när du skapar den här analysen eller bara vill engagera Professional Services-teamet, [kontakta support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
