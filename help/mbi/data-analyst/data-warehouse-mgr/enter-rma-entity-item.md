---
title: Enterprise_RMA_Item_Entity Table
description: Lär dig hur du analyserar information om ett visst objekt från en begärd retur.
exl-id: aa71cb3f-3e0b-4b6b-b4cc-dad103f79c51
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '269'
ht-degree: 0%

---

# enterprise_rma_item_entity, tabell

Varje rad i tabellen `enterprise_rma_item_entity` (kallas ofta `magento_rma_item_entity` i Commerce 2.x, men namnet kan anpassas) innehåller information om ett specifikt objekt från en begärd retur.

>[!NOTE]
>
>Den här tabellen levereras endast som standard med ditt Commerce-konto om du är `Enterprise Edition`- eller `Enterprise Cloud Edition`-kund.

## Vanliga inbyggda kolumner

| **Kolumnnamn** | **Beskrivning** |
|---|---|
| `entity\_id` | Unik identifierare för registret. Varje `entity\_id` representerar ett objekt som har begärts för retur. |
| `rma\_entity\_id` | Sekundärnyckel associerad med tabellen `enterprise\_rma`. |
| `status` | Status för artikelns retur. Värdena är bland annat&quot;mottagen&quot;,&quot;väntande&quot; och&quot;auktoriserad&quot;. Värdena i den här statusen kanske inte matchar värdet för den totala returens status. |
| `qty\_requested` | Kvantiteten som kunden begär för retur. |
| `qty\_approved` | Den kvantitet som godkänts för retur. |
| `qty\_returned` | Returnerad kvantitet. |
| `order\_item\_id` | Sekundärnyckel associerad med tabellen `sales\_flat\_order\_item`. |
| `product\_sku` | Den sku som returneras. |

{style="table-layout:auto"}

## Vanliga beräknade kolumner

| **Kolumnnamn** | **Beskrivning** |
|---|---|
| `Return date\_requested` | Detta är det datum då kunden begärde returen. |
| `Item price` | Artikelns pris. |
| `Return item's total value (qty\_returned * price)` | Detta är det totala monetära värdet för de artiklar som returneras. Detta används för att beräkna det totala returbeloppet i tabellen `enterprise\_rma`. |

{style="table-layout:auto"}

## Vanliga mått

| **Måttnamn** | **Beskrivning** | **Konstruktion** |
|---|---|---|
| `Number of items returned` | Antalet artiklar som returneras. | Åtgärdskolumn: returnerad<br>Åtgärd: Summa<br>Tidsstämpelkolumn: Begärt returdatum |
| `Returned items' total value` | Det returnerade penningbeloppet. | Åtgärdskolumn: Returobjektets totala värde (returnerat * pris)<br>Åtgärd: Summa<br>Tidsstämpelkolumn: Begärt returdatum |

{style="table-layout:auto"}

## Anslutningar till andra tabeller

`enterprise_rma`

* Skapa kopplade kolumner som `Return date\_requested` i tabellen `enterprise_rma_item_entity` via följande koppling:
* Commerce 1.x: `enterprise_rma_item_entity.rma_entity_id ` (många) => `enterprise_rma.entity_id` (en)
* Commerce 2.x: `magento_rma_item_entity.rma_entity_id ` (många) => `magento_rma.entity_id` (en)

`sales_flat_order_item`

* Skapa kopplade kolumner på  `enterprise_rma_item_entity`-tabell via följande join:

* Commerce 1.x: `enterprise_rma_item_entity.order_item_id ` (många) => `sales_flat_order_item.item_id` (en)
* Commerce 2.x: `magento_rma_item_entity.order_item_id ` (många) => `sales_order_item.item_id` (en)
