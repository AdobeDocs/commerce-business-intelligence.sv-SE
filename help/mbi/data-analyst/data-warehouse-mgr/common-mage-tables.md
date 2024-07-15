---
title: Vanliga Commerce-tabeller
description: Läs mer om några av de vanligaste tabellerna som  [!DNL Commerce Intelligence] kunder använder.
exl-id: 8b316130-55c6-4771-ae6e-97ac605fc6cc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '461'
ht-degree: 0%

---

# Vanliga Commerce-tabeller

När du ansluter en [!DNL Adobe Commerce]-instans till [[!DNL Adobe Commerce Intelligence]](../importing-data/integrations/magento.md) replikerar [!DNL Commerce Intelligence] automatiskt data från vissa av dina handelstabeller (vanligtvis 4-6 tabeller) för att konfigurera den första uppsättningen instrumentpaneler och rapporter. Även om detta är en bra startpunkt genererar de flesta butiksinstanser tiotals eller till och med hundratals ytterligare tabeller som kan ge viktiga insikter i verksamhetens prestanda.

Nedan finns en lista över några av de vanligaste tabellerna som [!DNL Commerce Intelligence]-kunder använder. När du har [anslutit din Commerce-instans till Commerce Intelligence](../../data-analyst/importing-data/integrations/magento.md) kan du använda [Data Warehouse Manager](../../data-analyst/data-warehouse-mgr/tour-dwm.md) för att spåra relevanta datafält.

| Tabellnamn | Beskrivning |
|---|---|
| `catalog_category_entity` | Varje rad i tabellen `catalog_category_entity` beskriver en specifik kategori. Med den associerade tabellen `catalog_category_entity_varchar` och mappningstabellen `catalog_category_product` kan du hämta kategoriinformation för varje produkt. |
| `catalog_category_product` | Varje rad i tabellen `catalog_category_product` visar en kombination av en produkt och en kategori. Därför kan en viss produkt finnas i det här registret flera gånger med olika kategorier, och en viss kategori kan finnas i det här registret flera gånger som är kopplade till olika produkter. Den här tabellen indexerar tabellen `catalog_category_entity` (som innehåller information på kategorinivå) och tabellen `catalog_product_entity` (som innehåller information på produktnivå). |
| `catalog_product_entity` | Varje rad i tabellen `catalog_product_entity` representerar en specifik produkt. Detta gäller även när produkten skapades i ditt Commerce-konto och dess SKU. |
| `customer_entity` | Varje rad i tabellen [`customer_entity`](../data-warehouse-mgr/cust-ent-table.md) representerar en registrerad användare på webbplatsen. Grundläggande kundnivåinformation som registreringsdatum och e-postadress live i det här registret. |
| `quote` | Varje rad i tabellen [`quote`](../data-warehouse-mgr/sales-flat-quote-table.md) representerar en vagn som skapades i utcheckningsprocessen, oavsett om vagnen till slut konverterades till en order. På grund av tabellens potentiella storlek rekommenderar Adobe att du regelbundet tar bort poster om vissa villkor uppfylls, t.ex. om det finns några okonverterade kort som är äldre än 60 dagar. |
| `quote_item` | Varje rad i tabellen [`quote_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) representerar ett objekt som lagts till i en kundvagn, oavsett om vagnen konverterades till en order eller inte. På grund av tabellens potentiella storlek rekommenderar Adobe att du regelbundet tar bort poster om vissa villkor uppfylls, t.ex. om det finns några okonverterade kort som är äldre än 60 dagar. |
| `sales_order` | Varje rad i tabellen [`sales_order`](../data-warehouse-mgr/sales-flat-order-table.md) representerar en ordning som har placerats på din plats. Det här registret innehåller information på ordernivå, t.ex. orderdatum, den kund som beställde ordern, ordersumma samt rabattanvändning och kupongkod. |
| `sales_order_address` | Varje rad i tabellen `sales_order_address` innehåller leverans- och faktureringsinformation för en viss order. I tabellen `sales_order` refererar `billing_address_id` och `shipping_address_id` för en viss ordning till en viss rad (identifieras av `entity_id`) i tabellen `sales_order_address`. |
| `sales_order_item` | Varje rad i tabellen [`sales_order_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) identifierar ett specifikt objekt från en viss ordning. Varje rad innehåller information om t.ex. produkt, inköpskvantitet och den ordning som den angivna artikeln är kopplad till. |

{style="table-layout:auto"}

## Relaterad dokumentation

[Entitetsrelationsdiagram](../data-warehouse-mgr/entity-rel-diag.md)
