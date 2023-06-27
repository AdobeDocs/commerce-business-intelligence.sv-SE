---
title: Översätta SQL-frågor i Commerce Intelligence-rapporter
description: Lär dig hur SQL-frågor översätts till beräknade kolumner, mätvärden som du använder i Commerce Intelligence.
exl-id: b3e3905f-6952-4f15-a582-bf892a971fae
source-git-commit: fa65bd909495d4d73cabbc264e9a47b3e0a0da3b
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 0%

---

# Översätta SQL-frågor i Commerce Intelligence

Har någonsin undrat hur SQL-frågor översätts till [beräknade kolumner](../data-warehouse-mgr/creating-calculated-columns.md), [mått](../../data-user/reports/ess-manage-data-metrics.md)och [rapporter](../../tutorials/using-visual-report-builder.md) du använder i [!DNL Commerce Intelligence]? Om du är en tung SQL-användare kan du förstå hur SQL översätts i [!DNL Commerce Intelligence] kan du arbeta smartare i [data warehouse Manager](../data-warehouse-mgr/tour-dwm.md) och få ut så mycket som möjligt av [!DNL Commerce Intelligence] plattform.

I slutet av det här avsnittet finns en **översättningsmatris** för SQL-frågesatser och [!DNL Commerce Intelligence] -element.

Börja med att titta på en allmän fråga:

| | |
|--- |--- |
| `SELECT` |  |
| `a,` | Rapport `group by` |
| `SUM(b)` | `Aggregate function` (kolumn) |
| `FROM c` | `Source` table |
| `WHERE` |  |
| `d IS NOT NULL` | `Filter` |
| `AND time < X`<br><br> `AND time >= Y` | Rapport `time frame` |
| `GROUP BY a` | Rapport `group by` |

Det här exemplet omfattar de flesta översättningsfall, men det finns några undantag. Gör en djupdykning, och börja med hur `aggregate` funktionen är översatt.

## Sammanställningsfunktioner

Sammanställningsfunktioner (till exempel `count`, `sum`, `average`, `max`, `min`) i frågor antingen i form av **metrisk aggregering** eller **kolumnaggregeringar** in [!DNL Commerce Intelligence]. Den differentierande faktorn är om en join krävs för att utföra aggregeringen.

Titta på ett exempel för vart och ett av de ovanstående.

## Måttaggregat {#aggregate}

Ett mått krävs vid aggregering `within a single table`. Till exempel `SUM(b)` sammanställningsfunktionen från frågan ovan skulle troligtvis representeras av ett mått som summerar kolumnen `B`. 

Titta på ett specifikt exempel på hur en `Total Revenue` kan definieras i [!DNL Commerce Intelligence]. Titta på frågan nedan som du försöker översätta:

| | |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | `Metric operation` (kolumn) |
| `FROM orders` | `Metric source` table |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Mått `filter` |
| `AND created_at < X`<br><br>`AND created_at >= Y` | Mått `timestamp` (och rapportering) `time range`) |

Navigera till måttverktyget genom att klicka **[!UICONTROL Manage Data** > ** Mått **> **Skapa nytt mått]** måste du först välja rätt `source` tabellen, som i detta fall är `orders` tabell. Därefter ställs måtten in enligt nedan:

![Måttaggregering](../../assets/Metric_aggregation.png)

## Kolumnaggregeringar

En beräknad kolumn krävs vid sammanställning av en kolumn som är kopplad från en annan tabell. Du kan till exempel ha en kolumn inbyggd i `customer` tabell anropad `Customer LTV`som summerar det totala värdet av alla order som är kopplade till den kunden i `orders` tabell.

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

Konfigurera detta i [!DNL Commerce Intelligence] kräver att du använder din Data warehouse-hanterare, där du bygger en väg mellan `orders` och `customers` skapa sedan en kolumn som kallas `Customer LTV` i kundens register.

Se hur man skapar en ny bana mellan `customers` och `orders`. Slutmålet är att skapa en ny aggregerad kolumn i `customers` tabell, så navigera först till `customers` bord i Data warehouse och klicka sedan på **[!UICONTROL Create a Column** > ** Välj en definition **> **SUM]**.

Sedan måste du välja källtabellen. Om det finns en sökväg till `orders` markerar du den i listrutan. Om du skapar en ny bana klickar du **[!UICONTROL Create new path]** och skärmen nedan visas:

![Skapa ny bana](../../assets/Create_new_path.png)

Här bör du noga tänka på relationen mellan de två tabeller som du försöker ansluta till. I det här fallet finns det `Many` order som är kopplade till `One` kunden `orders` tabellen visas på `Many` sidan, `customers` tabellen markerad på `One` sida.

>[!NOTE]
>
>I [!DNL Commerce Intelligence], a `path` motsvarar en `Join` i SQL.

När banan har sparats kan du skapa `Customer LTV` kolumn! Se nedan:

![](../../assets/Customer_LTV.gif)

Nu när du har byggt nya `Customer LTV` i din `customers` kan du skapa en [metrisk aggregering](#aggregate) med hjälp av den här kolumnen (till exempel för att hitta genomsnittligt antal TV-apparater per kund). Du kan också `group by` eller `filter` efter den beräknade kolumnen i en rapport med befintliga mätvärden som bygger på `customers` tabell.

>[!NOTE]
>
>När du skapar en ny beräknad kolumn måste du [lägga till dimensionen i befintliga mätvärden](../data-warehouse-mgr/manage-data-dimensions-metrics.md) innan det blir tillgängligt som `filter` eller `group by`.

Se [skapa beräknade kolumner](../data-warehouse-mgr/creating-calculated-columns.md) med Data warehouse Manager.

## `Group By` klausuler

`Group By` funktioner i frågor representeras ofta i [!DNL Commerce Intelligence] som en kolumn som används för att segmentera eller filtrera en visuell rapport. Låt oss till exempel gå igenom `Total Revenue` fråga som du utforskat tidigare, men den här gången segmenteras intäkterna av `coupon\_code` för att få en bättre förståelse för vilka kuponger som genererar störst intäkter.

Börja med frågan nedan:

| | |
|--- |--- |
| `SELECT coupon_code,` | Rapport `group by` |
| `SUM(order_total) as "Total Revenue"` | `Metric operation`(kolumn) |
| `FROM orders` | `Metric source` table |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Mått `filter` |
| `AND created_at < '2016-12-01'` <br><br>`AND created_at >= '2016-09-01'` | Mått `timestamp` (och rapportering) `time range`) |
| `GROUP BY coupon_code` | Rapport `group by` |

>[!NOTE]
>
>Den enda skillnaden från den fråga du började med tidigare är att&quot;kupongen\_code&quot; har lagts till som grupp efter._

Använda samma `Total Revenue` mätvärden som du har skapat tidigare, är du nu redo att skapa en intäktsrapport segmenterad efter kupongkod! Titta på bilden nedan som visar hur du konfigurerar den här visuella rapporten med information från september till november:

![Intäkter per kupongkod](../../assets/Revenue_by_coupon_code.gif)

## Formler

Ibland kan en fråga innehålla flera aggregeringar för att beräkna relationen mellan olika kolumner. Du kan till exempel beräkna det genomsnittliga ordervärdet i en fråga på ett av två sätt:

* `AVG('order\_total')` ELLER
* `SUM('order\_total')/COUNT('order\_id')`

Den första metoden skulle innebära att ett nytt mätvärde skapas som utför ett genomsnitt på `order\_total` kolumn. Den senare metoden kan dock skapas direkt i rapportbyggaren förutsatt att du redan har ställt in mätvärden för att beräkna `Total Revenue` och `Number of orders`.

Ta ett steg tillbaka och se den övergripande frågan för `Average order value`:

| | |
|--- |--- |
| `SELECT` |  |
| `SUM(order_total) as "Total Revenue"` | Mått `operation` (kolumn) |
| `COUNT(order_id) as "Number of orders"` | Mått `operation` (kolumn) |
| `SUM(order_total)/COUNT(order_id) as "Average order value"` | Mått `operation` (kolumn) / Måttåtgärd (kolumn) |
| `FROM orders` | Mått `source` table |
| `WHERE` |  |
| `email NOT LIKE '%@magento.com'` | Mått `filter` |
| `AND created_at < '2016-12-01'`<br><br>`AND created_at >= '2016-09-01'` | Mättidsstämpel (och tidsintervall för rapportering) |

Anta nu att du redan har ställt in mätvärden för att beräkna `Total Revenue` och `Number of orders`. Eftersom dessa mätvärden finns kan du bara öppna `Report Builder` och skapa en behovsstyrd beräkning med `Formula` funktion:

![AOV-forumen](../../assets/AOV_forumula.gif)

## Radbrytning

Om du är en tung SQL-användare kan du tänka på hur frågor översätts i [!DNL Commerce Intelligence] Med kan du skapa beräknade kolumner, mätvärden och rapporter.

Se matrisen nedan för snabb referens. Detta visar SQL-satsens motsvarighet [!DNL Commerce Intelligence] -element och hur det kan mappas till mer än ett element, beroende på hur det används i frågan.

## Commerce Intelligence Elements

| **`SQL Clause`** | **`Metric`** | **`Filter`** | **`Report group by`** | **`Report time frame`** | **`Path`** | **`Calculated column inputs`** | **`Source table`** |
|---|---|---|---|---|---|---|---|
| `SELECT` | X | - | X | - | - | X | - |
| `FROM` | - | - | - | - | - | - | X |
| `WHERE` | - | X | - | - | - | - | - |
| `WHERE` (med tidselement) | - | - | - | X | - | - | - |
| `JOIN...ON` | - | X | - | - | X | X | - |
| `GROUP BY` | - | - | X | - | - | - | - |
