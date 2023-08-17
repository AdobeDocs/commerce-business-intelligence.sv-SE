---
title: enterprise_rma-tabell
description: Lär dig hur du analyserar information om en viss returbegäran.
exl-id: a19cbc9a-e34f-4f4e-820f-9e413d1a552d
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# enterprise_rma-tabell

Varje rad i `enterprise_rma` tabell (anropas ofta `magento_rma` i Adobe Commerce 2.x, men namnet kan anpassas) innehåller information om en viss returbegäran.

>[!NOTE]
>
>Tabellen levereras som standard med ditt Adobe Commerce-konto om du är en `Enterprise Edition` eller `Enterprise Cloud Edition` kund.

## Vanliga inbyggda kolumner

| **Kolumnnamn** | **Beskrivning** |
|---|---|
| `entity\_id` | Unik identifierare för registret. Varje `entity\_id` representerar en returbegäran. |
| `date\_requested` | Datumet då returen begärdes. |
| `status` | Status för returen. Värdena är bland annat&quot;mottagen&quot;,&quot;väntande&quot; och&quot;auktoriserad&quot;. |
| `order\_id` | Sekundärnyckel associerad med `sales\_flat\_order` tabell. |
| `customer\_id` | Sekundärnyckel associerad med `customer\_entity` tabell. |

{style="table-layout:auto"}

## Vanliga beräknade kolumner

| **Kolumnnamn** | **Beskrivning** |
|---|---|
| `Order's created\_at` | Detta är datumet för den ursprungliga ordern. Detta kan användas för att få fram tiden mellan beställnings- och returbegäran. |
| `Customer's order number` | Detta är kundens ordernummer som är kopplat till den ursprungliga ordern. |
| `Seconds between order's created\_at and return's date\_requested` | Antalet sekunder från orderdatumet till returbegäran. |
| `Return's total value` | Detta är det totala monetära beloppet som returneras. Detta är summan av varje returobjekts enskilda returbelopp. |

{style="table-layout:auto"}

## Vanliga mått

| **Måttnamn** | **Beskrivning** | **Konstruktion** |
|---|---|---|
| `Number of returns` | Antalet begärda returer. | `Operation` kolumn: `entity id`<br>`Operation`: `Count`<br>`Timestamp` Kolumn: `date requested` |
| `Total returned amount` | Det totala penningbelopp som returneras. | `Operation `Kolumn: `Return's total value`<br>`Operation`: Summa<br>`Timestamp` Kolumn: begärt datum |
| `Average returned amount` | Det genomsnittliga penningbelopp som returneras. | `Operation`` Column: Return's total value`<br>`Operation`: `Average`<br>`Timestamp` Kolumn: `date requested` |
| `Average time to return` | Genomsnittlig tid från order till retur. | `Operation` Kolumn: Sekunder mellan order som skapas vid och returdatum som begärts<br>`Operation`: `Average`<br>`Timestamp` Kolumn: `date requested` |

{style="table-layout:auto"}

## Anslutningar till andra tabeller

`sale_flat_order`

* Skapa kopplade kolumner för att segmentera och filtrera efter attribut på ordningsnivå på `enterprise_rma` tabellen via följande join:
   * Commerce 1.x: `enterprise_rma.order_id` (många) => `sales_flat_order.entity_id` (ett)
   * Commerce 2.x: `magento_rma.order_id` (många) => `sales_order.entity_id` (ett)

`enterprise_rma_item_entity`

* Skapa flera-till-en-kolumner som `Return's total value` på `enterprise_rma` tabellen via följande join:
   * Commerce 1.x: `enterprise_rma_item_entity.rma_entity_id` (många) => `enterprise_rma.entity_id` (ett)
   * Commerce 2.x: `magento_rma_item_entity.rma_entity_id ` (många) => `magento_rma.entity_id` (ett)
