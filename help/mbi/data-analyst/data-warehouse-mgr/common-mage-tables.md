---
title: Vanliga handelstabeller
description: Läs om några av de vanligaste tabellerna som [!DNL Commerce Intelligence] kunderna använder.
exl-id: 8b316130-55c6-4771-ae6e-97ac605fc6cc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---

# Vanliga handelstabeller

När du ansluter en [!DNL Adobe Commerce] instans till [[!DNL Adobe Commerce Intelligence]](../importing-data/integrations/magento.md), [!DNL Commerce Intelligence] replikerar automatiskt data från vissa av dina handelstabeller (vanligen 4-6 tabeller) för att konfigurera den första uppsättningen instrumentpaneler och rapporter. Även om detta är en bra startpunkt genererar de flesta butiksinstanser tiotals eller till och med hundratals ytterligare tabeller som kan ge viktiga insikter i verksamhetens prestanda.

Nedan finns en lista över några av de vanligaste tabellerna som [!DNL Commerce Intelligence] kunderna använder. Efter dig [koppla din Commerce-instans till Commerce Intelligence](../../data-analyst/importing-data/integrations/magento.md)kan du använda [Data Warehouse Manager](../../data-analyst/data-warehouse-mgr/tour-dwm.md) för att spåra relevanta datafält.

| Tabellnamn | Beskrivning |
|---|---|
| `catalog_category_entity` | Varje rad i `catalog_category_entity` tabellen beskriver en viss kategori. Med associerade `catalog_category_entity_varchar` tabellen och `catalog_category_product` mappningstabell kan du hämta kategoriinformation för varje produkt. |
| `catalog_category_product` | Varje rad i `catalog_category_product` en kombination av en produkt och en kategori. Därför kan en viss produkt finnas i det här registret flera gånger med olika kategorier, och en viss kategori kan finnas i det här registret flera gånger som är kopplade till olika produkter. Den här tabellen indexerar `catalog_category_entity` tabell (som innehåller information på kategorinivå) och `catalog_product_entity` tabell (som innehåller produktnivåinformation). |
| `catalog_product_entity` | Varje rad i `catalog_product_entity` tabellen representerar en specifik produkt. Detta inkluderar när produkten skapades i ditt Commerce-konto och dess SKU. |
| `customer_entity` | Varje rad i [`customer_entity`](../data-warehouse-mgr/cust-ent-table.md) tabellen representerar en registrerad användare på webbplatsen. Grundläggande kundnivåinformation som registreringsdatum och e-postadress live i det här registret. |
| `quote` | Varje rad i [`quote`](../data-warehouse-mgr/sales-flat-quote-table.md) tabellen representerar en kundvagn som skapades i utcheckningsprocessen, oavsett om vagnen konverterades till en order eller inte. På grund av tabellens potentiella storlek rekommenderar Adobe att du regelbundet tar bort poster om vissa villkor uppfylls, t.ex. om det finns några okonverterade kort som är äldre än 60 dagar. |
| `quote_item` | Varje rad i [`quote_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) tabellen representerar en artikel som lagts till i en kundvagn, oavsett om vagnen så småningom konverterats till en order. På grund av tabellens potentiella storlek rekommenderar Adobe att du regelbundet tar bort poster om vissa villkor uppfylls, t.ex. om det finns några okonverterade kort som är äldre än 60 dagar. |
| `sales_order` | Varje rad i [`sales_order`](../data-warehouse-mgr/sales-flat-order-table.md) tabellen representerar en order som lagts på din plats. Det här registret innehåller information på ordernivå, t.ex. orderdatum, den kund som beställde ordern, ordersumma samt rabattanvändning och kupongkod. |
| `sales_order_address` | Varje rad på `sales_order_address` tabellen innehåller information om frakt och fakturering för en viss order. På `sales_order` tabellen, `billing_address_id` och `shipping_address_id` för en viss order hänvisar till en viss rad (identifieras med `entity_id`) på `sales_order_address` tabell. |
| `sales_order_item` | Varje rad i [`sales_order_item`](../data-warehouse-mgr/sales-flat-quote-item-table.md) tabell identifierar ett specifikt objekt från en viss ordning. Varje rad innehåller information om t.ex. produkt, inköpskvantitet och den ordning som den angivna artikeln är kopplad till. |

{style="table-layout:auto"}

## Relaterad dokumentation

[Entitetsrelationsdiagram](../data-warehouse-mgr/entity-rel-diag.md)
