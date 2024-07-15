---
title: Översätta SQL-frågor till Commerce Intelligence-rapporter
description: Lär dig hur SQL-frågor översätts till beräknade kolumner, mätvärden som du använder i Commerce Intelligence.
exl-id: b3e3905f-6952-4f15-a582-bf892a971fae
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '933'
ht-degree: 0%

---

# Översätta SQL-frågor i Commerce Intelligence

Har du någonsin undrat hur SQL-frågor översätts till de [beräknade kolumnerna](../data-warehouse-mgr/creating-calculated-columns.md), [metrics](../../data-user/reports/ess-manage-data-metrics.md) och [reports](../../tutorials/using-visual-report-builder.md) som du använder i [!DNL Commerce Intelligence]? Om du är en tung SQL-användare kan du arbeta smartare i [Data Warehouse Manager](../data-warehouse-mgr/tour-dwm.md) och få ut det mesta av [!DNL Commerce Intelligence]-plattformen genom att förstå hur SQL översätts i [!DNL Commerce Intelligence].

I slutet av det här avsnittet finns en **översättningsmatris** för SQL-frågesatser och [!DNL Commerce Intelligence] -element.

Börja med en allmän fråga:

| | |
|--- |--- |
| `SELECT` |  |
| `a,` | Rapport `group by` |
| `SUM(b)` | `Aggregate function` (kolumn) |
| `FROM c` | `Source`-tabell |
| `WHERE` |  |
| `d IS NOT NULL` | `Filter` |
| `AND time < X`<br><br> `AND time >= Y` | Rapport `time frame` |
| `GROUP BY a` | Rapport `group by` |

Det här exemplet omfattar de flesta översättningsfall, men det finns några undantag. Gör en djupdykning, med början från hur funktionen `aggregate` översätts.

## Sammanställningsfunktioner

Sammanställningsfunktioner (till exempel `count`, `sum`, `average`, `max`, `min`) i frågor har antingen formen **metriska aggregeringar** eller **kolumnaggregeringar** i [!DNL Commerce Intelligence]. Den differentierande faktorn är om en join krävs för att utföra aggregeringen.

Titta på ett exempel för vart och ett av de ovanstående.

## Måttaggregat {#aggregate}

Ett mått krävs vid aggregering av `within a single table`. Exempelvis skulle mängdfunktionen `SUM(b)` från frågan ovan sannolikt representeras av ett mått som summerar kolumnen `B`. 

Titta på ett specifikt exempel på hur ett `Total Revenue`-mått kan definieras i [!DNL Commerce Intelligence]. Titta på frågan nedan som du försöker översätta:

| | |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | `Metric operation` (kolumn) |
| `FROM orders` | `Metric source`-tabell |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Mått `filter` |
| `AND created_at < X`<br><br>`AND created_at >= Y` | Mått `timestamp` (och rapportering `time range`) |

Navigera till måttverktyget genom att klicka på **[!UICONTROL Manage Data** > ** Metrisk **> **Skapa nytt mätresultat]**. Du måste först markera rätt `source`-tabell, som i det här fallet är `orders`-tabellen. Därefter ställs måtten in enligt nedan:

![Måttaggregering](../../assets/Metric_aggregation.png)

## Kolumnaggregeringar

En beräknad kolumn krävs vid sammanställning av en kolumn som är kopplad från en annan tabell. Du kan till exempel ha en kolumn som är inbyggd i din `customer`-tabell som heter `Customer LTV` och som summerar det totala värdet för alla order som är kopplade till den kunden i tabellen `orders`.

Frågan för den här aggregeringen kan se ut ungefär som nedan:

|  |  |
|--- |--- |
| `Select` | |
| `c.customer_id` | Ägare av sammanställd |
| `SUM(o.order_total) as "Customer LTV"` | Sammanställningsåtgärd (kolumn) |
| `FROM customers c` | Sammanställd ägarregister |
| `JOIN orders o` | Källregister för aggregering |
| `ON c.customer_id = o.customer_id` | Bana |
| `WHERE o.status = 'success'` | Aggregera, filter |

Om du konfigurerar detta i [!DNL Commerce Intelligence] måste du använda din kundhanterare, där du skapar en sökväg mellan din `orders`- och `customers`-Data Warehouse och sedan skapar en  med namnet `Customer LTV` i kundens tabell.

Titta på hur du skapar en ny sökväg mellan `customers` och `orders`. Slutmålet är att skapa en ny aggregerad kolumn i tabellen `customers`, så navigera först till tabellen `customers` i Datan Warehouse och klicka sedan på **[!UICONTROL Create a Column** > ** Markera en definition **> **SUM]**.

Sedan måste du välja källtabellen. Om det finns en sökväg till din `orders`-tabell väljer du den i listrutan. Om du skapar en ny sökväg klickar du på **[!UICONTROL Create new path]** så visas skärmen nedan:

![Skapa ny sökväg](../../assets/Create_new_path.png)

Här bör du noga tänka på relationen mellan de två tabeller som du försöker ansluta till. I det här fallet finns det eventuellt `Many` order som är kopplade till `One`-kunden, och därför visas tabellen `orders` på `Many`-sidan, medan tabellen `customers` är markerad på `One`-sidan.

>[!NOTE]
>
>I [!DNL Commerce Intelligence] är en `path` ekvivalent med en `Join` i SQL.

När sökvägen har sparats kan du skapa kolumnen `Customer LTV`! Se nedan:

![](../../assets/Customer_LTV.gif)

Nu när du har skapat den nya `Customer LTV`-kolumnen i din `customers`-tabell kan du skapa en [måttaggregering](#aggregate) med den här kolumnen (till exempel för att hitta den genomsnittliga LTV-nivån per kund). Du kan också `group by` eller `filter` med den beräknade kolumnen i en rapport med hjälp av befintliga mått som bygger på tabellen `customers`.

>[!NOTE]
>
>För det senare måste du [lägga till dimensionen i befintliga mått](../data-warehouse-mgr/manage-data-dimensions-metrics.md) innan den är tillgänglig som `filter` eller `group by` när du skapar en ny beräknad kolumn.

Se [skapa beräknade kolumner](../data-warehouse-mgr/creating-calculated-columns.md) med Data Warehouse Manager.

## `Group By`-satser

`Group By`-funktioner i frågor representeras ofta i [!DNL Commerce Intelligence] som en kolumn som används för att segmentera eller filtrera en visuell rapport. Låt oss till exempel gå tillbaka till `Total Revenue`-frågan som du utforskade tidigare, men den här gången segmenterar intäkterna av `coupon\_code` för att få en bättre förståelse för vilka kuponger som genererar störst intäkter.

Börja med frågan nedan:

| | |
|--- |--- |
| `SELECT coupon_code,` | Rapport `group by` |
| `SUM(order_total) as "Total Revenue"` | `Metric operation`(kolumn) |
| `FROM orders` | `Metric source`-tabell |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Mått `filter` |
| `AND created_at < '2016-12-01'` <br><br>`AND created_at >= '2016-09-01'` | Mått `timestamp` (och rapportering `time range`) |
| `GROUP BY coupon_code` | Rapport `group by` |

>[!NOTE]
>
>Den enda skillnaden från den fråga du började med tidigare är att&quot;kupongen\_code&quot; har lagts till som grupp efter._

Med samma `Total Revenue`-mått som du skapade tidigare är du nu redo att skapa en intäktsrapport segmenterad med kupongkod! Titta på bilden nedan som visar hur du konfigurerar den här visuella rapporten med information från september till november:

![Intäkter per kupongkod](../../assets/Revenue_by_coupon_code.gif)

## Formler

Ibland kan en fråga innehålla flera aggregeringar för att beräkna relationen mellan olika kolumner. Du kan till exempel beräkna det genomsnittliga ordervärdet i en fråga på ett av två sätt:

* `AVG('order\_total')` ELLER
* `SUM('order\_total')/COUNT('order\_id')`

Den tidigare metoden skulle innebära att ett nytt mätvärde skapas som utför ett genomsnitt i kolumnen `order\_total`. Den senare metoden kan dock skapas direkt i rapportverktyget, förutsatt att du redan har angett värden för att beräkna `Total Revenue` och `Number of orders`.

Ta ett steg tillbaka och titta på den övergripande frågan för `Average order value`:

| | |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | Mått `operation` (kolumn) |
| `COUNT(order_id) as "Number of orders"` | Mått `operation` (kolumn) |
| `SUM(order_total)/COUNT(order_id) as "Average order value"` | Mått `operation` (kolumn) / Måttåtgärd (kolumn) |
| `FROM orders` | Måtttabell `source` |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Mått `filter` |
| `AND created_at < '2016-12-01'`<br><br>`AND created_at >= '2016-09-01'` | Måttets tidsstämpel (och tidsintervall för rapportering) |

Anta nu att du redan har ställt in mätvärden för att beräkna `Total Revenue` och `Number of orders`. Eftersom dessa mått finns kan du öppna `Report Builder` och skapa en on demand-beräkning med funktionen `Formula`:

![AOV-format](../../assets/AOV_forumula.gif)

## Radbrytning

Om du är en tung SQL-användare kan du skapa beräknade kolumner, mätvärden och rapporter med hjälp av frågor som översätts i [!DNL Commerce Intelligence].

Se matrisen nedan för snabb referens. Detta visar SQL-satsens motsvarande [!DNL Commerce Intelligence]-element och hur det kan mappas till mer än ett element, beroende på hur det används i frågan.

## Commerce Intelligence Elements

| **`SQL Clause`** | **`Metric`** | **`Filter`** | **`Report group by`** | **`Report time frame`** | **`Path`** | **`Calculated column inputs`** | **`Source table`** |
|---|---|---|---|---|---|---|---|
| `SELECT` | X | - | X | - | - | X | - |
| `FROM` | - | - | - | - | - | - | X |
| `WHERE` | - | X | - | - | - | - | - |
| `WHERE` (med tidselement) | - | - | - | X | - | - | - |
| `JOIN...ON` | - | X | - | - | X | X | - |
| `GROUP BY` | - | - | X | - | - | - | - |
