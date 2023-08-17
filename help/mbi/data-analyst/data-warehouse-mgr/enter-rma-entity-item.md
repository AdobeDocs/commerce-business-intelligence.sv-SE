---
title: Enterprise_RMA_Item_Entity Table
description: Lär dig hur du analyserar information om ett visst objekt från en begärd retur.
exl-id: aa71cb3f-3e0b-4b6b-b4cc-dad103f79c51
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '275'
ht-degree: 0%

---

# enterprise_rma_item_entity, tabell

Varje rad i `enterprise_rma_item_entity` tabell (anropas ofta `magento_rma_item_entity` i Commerce 2.x, men namnet kan anpassas) innehåller information om en viss artikel från en begärd retur.

>[!NOTE]
>
>Det här registret levereras endast som standard med ditt Commerce-konto om du är en `Enterprise Edition` eller `Enterprise Cloud Edition` kund.

## Vanliga inbyggda kolumner

| **Kolumnnamn** | **Beskrivning** |
|---|---|
| `entity\_id` | Unik identifierare för registret. Varje `entity\_id` representerar ett objekt som har begärts för retur. |
| `rma\_entity\_id` | Sekundärnyckel associerad med `enterprise\_rma` tabell. |
| `status` | Status för artikelns retur. Värdena är bland annat&quot;mottagen&quot;,&quot;väntande&quot; och&quot;auktoriserad&quot;. Värdena i den här statusen kanske inte matchar värdet för den totala returens status. |
| `qty\_requested` | Kvantiteten som kunden begär för retur. |
| `qty\_approved` | Den kvantitet som godkänts för retur. |
| `qty\_returned` | Returnerad kvantitet. |
| `order\_item\_id` | Sekundärnyckel associerad med `sales\_flat\_order\_item` tabell. |
| `product\_sku` | Den sku som returneras. |

{style="table-layout:auto"}

## Vanliga beräknade kolumner

| **Kolumnnamn** | **Beskrivning** |
|---|---|
| `Return date\_requested` | Detta är det datum då kunden begärde returen. |
| `Item price` | Artikelns pris. |
| `Return item's total value (qty\_returned * price)` | Detta är det totala monetära värdet för de artiklar som returneras. Detta används för att beräkna det totala returbeloppet på `enterprise\_rma` tabell. |

{style="table-layout:auto"}

## Vanliga mått

| **Måttnamn** | **Beskrivning** | **Konstruktion** |
|---|---|---|
| `Number of items returned` | Antalet artiklar som returneras. | Åtgärdskolumn: returnerad kvantitet<br>Åtgärd: Summa<br>Tidsstämpelkolumn: Begärt returdatum |
| `Returned items' total value` | Det returnerade penningbeloppet. | Åtgärdskolumn: Returartikelns totala värde (returnerat antal * pris)<br>Åtgärd: Summa<br>Tidsstämpelkolumn: Begärt returdatum |

{style="table-layout:auto"}

## Anslutningar till andra tabeller

`enterprise_rma`

* Skapa kopplade kolumner som `Return date\_requested` på `enterprise_rma_item_entity` tabellen via följande join:
* Commerce 1.x: `enterprise_rma_item_entity.rma_entity_id ` (många) => `enterprise_rma.entity_id` (ett)
* Commerce 2.x: `magento_rma_item_entity.rma_entity_id ` (många) => `magento_rma.entity_id` (ett)

`sales_flat_order_item`

* Skapa kopplade kolumner på  `enterprise_rma_item_entity` tabellen via följande join:

* Commerce 1.x: `enterprise_rma_item_entity.order_item_id ` (många) => `sales_flat_order_item.item_id` (ett)
* Commerce 2.x: `magento_rma_item_entity.order_item_id ` (många) => `sales_order_item.item_id` (ett)
