---
title: Definiera kundkoncentration
description: Lär dig hur du skapar en kontrollpanel som hjälper dig att mäta hur de totala intäkterna fördelas mellan era kunder.
exl-id: 6242019f-a6a5-48d3-b214-94acd7842e00
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# Kundkoncentration

I det här avsnittet beskrivs hur du skapar en kontrollpanel som hjälper dig att mäta hur de totala intäkterna fördelas bland kunderna. Förstå vilken procentandel av kunderna som bidrar med vilken procentandel av intäkterna och skapar segmenterade listor på bästa möjliga marknad för och behåller era högkvalitativa kunder.

Den här analysen innehåller [avancerade beräknade kolumner](../data-warehouse-mgr/adv-calc-columns.md).

## Komma igång

Du måste först överföra en fil som bara innehåller en primärnyckel med värdet 1. Detta gör att du kan skapa vissa nödvändiga beräknade kolumner för analysen.

Du kan använda [filöverföringen](../importing-data/connecting-data/using-file-uploader.md) och bilden nedan för att formatera filen.

## Beräknade kolumner

Om du använder den ursprungliga arkitekturen (om du t.ex. inte har alternativet `Data Warehouse Views` på menyn `Manage Data`) vill du kontakta supportteamet för att bygga ut kolumnerna nedan. På den nya arkitekturen kan dessa kolumner skapas från sidan `Manage Data > Data Warehouse`. Detaljerade instruktioner finns nedan.

Ytterligare en skillnad görs om ditt företag tillåter gästbeställningar. I så fall kan du ignorera alla steg för tabellen `customer_entity`. Om gästorder inte tillåts, ignorera alla steg för tabellen `sales_flat_order`.

Kolumner att skapa

* `Sales_flat_order/customer_entity`-tabell
* (indata) `reference`
* [!UICONTROL Column type]: - `Same table > Calculation`
* [!UICONTROL Inputs]: - `entity_id`
* [!UICONTROL Calculation]: - **case when A is null then null else 1 end**
* [!UICONTROL Datatype]: - `Integer`

* tabellen `Customer concentration` (det här är filen som du överförde med numret `1`)
* Antal kunder
* [!UICONTROL Column type]: - `Many to One > Count Distinct`
* Sökväg - `sales_flat_order.(input) reference > Customer Concentration.Primary Key` ELLER `customer_entity.(input)reference > Customer Concentration.Primary Key`
* Markerad kolumn - `sales_flat_order.customer_email` ELLER `customer_entity.entity_id`

* `customer_entity`-tabell
* Antal kunder
* [!UICONTROL Column type]: - `One to Many > JOINED_COLUMN`
* Sökväg - `customer_entity.(input) reference > Customer Concentration. Primary Key`
* Markerad kolumn - `Number of customers`

* (indata) `Ranking by customer lifetime revenue`
* [!UICONTROL Column type]: - `Same table > Event Number`
* Händelseägare - `Number of customers`
* Händelserangordning - `Customer's lifetime revenue`

* Kundens intäktspunkt
* [!UICONTROL Column type]: - `Same table > Calculation`
* [!UICONTROL Inputs]: - `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: - **case when A is null then null else (A/B)* 100 end &#x200B;**
* [!UICONTROL Datatype]: - `Decimal`

* `Sales_flat_order`-tabell
* Antal kunder
* [!UICONTROL Column type]: - `One to Many > JOINED_COLUMN`
* Sökväg - `sales_flat_order.(input) reference > Customer Concentration.Primary Key`
* Markerad kolumn - `Number of customers`

* (input) Rankning per kundens livstid
* [!UICONTROL Column type]: - `Same table > Event Number`
* Händelseägare - `Number of customers`
* Händelserangordning - `Customer's lifetime revenue`
* Filter - `Customer's order number = 1`

* Kundens intäktspunkt
* [!UICONTROL Column type]: - `Same table > Calculation`
* [!UICONTROL Inputs]: - `(input) Ranking by customer lifetime revenue`, `Number of customers`
* [!UICONTROL Calculation]: - **case when A is null then null else (A/B)* 100 end &#x200B;**
* [!UICONTROL Datatype]: - `Decimal`

>[!NOTE]
>
>De percentiler som används är till och med delar av kunder, vilket representerar den sjätte percentilen av er kundbas. Varje kund är associerad med ett heltal mellan 1 och 100, som kan ses som en livstidsintäkt på *rankning*. Om kundens intäktspolicy för en viss kund till exempel är **5** är den här kunden i den ***femte percentilen*** av alla kunder i termer av livstidsintäkter.

## Mått

* **Totalt kundlivstidsvärde**
* I tabellen `customer_entity`
* Detta mått utför en **summa**
* I kolumnen `Customer's lifetime revenue`
* Ordnad efter tidsstämpeln `Customer's first order date`

## Rapporter

* **Kundkoncentration**
* [!UICONTROL Metric]: `Total customer lifetime value`
* [!UICONTROL Filter]: `Customer's revenue percentile IS NOT NULL`

* [!UICONTROL Metric]: `Total customer lifetime value`
* [!UICONTROL Filter]: `Customer's revenue percentile IS NOT NULL`

* &#x200B;
  [!UICONTROL Group by]: `Independent`
* Mått `A`: `Total customer lifetime revenue by percentile`
* Mått `B`: `Total customer lifetime revenue (ungrouped)`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Customer's revenue percentile`
* Visa över/under: `100% of Customer's revenue percentile Name`
* &#x200B;
  [!UICONTROL Chart type]: `Line`

* **Högsta koncentrationen 10 %**
* [!UICONTROL Filter]: `Customer's revenue percentile <= 10`

* Mått `A`: `Total customer lifetime revenue`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* Dölj diagram
* &#x200B;
  [!UICONTROL Group by]: `Email`
* &#x200B;
  [!UICONTROL Chart type]: `Table`

* **50 % nedersta koncentration med endast ett inköp**

* Mått `A`: `Total customer lifetime revenue`
* `Customer's revenue percentile <= 50`
* `Customer's lifetime number of orders = 1`
* [!UICONTROL Filter]:

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* Dölj diagram
* &#x200B;
  [!UICONTROL Group by]: `Email`
* &#x200B;
  [!UICONTROL Chart type]: `Table`

* **10 % nedersta koncentration**
* [!UICONTROL Filter]: `Customer's revenue percentile > 90`

* Mått `A`: `Total customer lifetime revenue`
* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* Dölj diagram
* &#x200B;
  [!UICONTROL Group by]: `Email`
* &#x200B;
  [!UICONTROL Chart type]: `Table`

När du har kompilerat alla rapporter kan du ordna dem på kontrollpanelen som du vill. Resultatet kan se ut som kontrollpanelen ovan.

[Kontakta support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=sv-SE) om du får frågor under arbetet med att skapa den här analysen, eller om du bara vill engagera Professional Services-teamet.
