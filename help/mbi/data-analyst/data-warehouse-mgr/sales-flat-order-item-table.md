---
title: register_för försäljningsorder_artikel
description: Lär dig hur du arbetar med tabellen sales_order_item.
exl-id: 5c48e985-3ba2-414b-bd1f-555b3da763bd
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 0%

---

# `sales_order_item` Tabell

The `sales_order_item` tabell (`sales_flat_order_item` på M1) innehåller uppgifter om alla produkter som köpts i en beställning. Varje rad representerar en unik `sku` ingår i en beställning. Kvantiteten enheter som köpts för en viss `sku` representeras oftast av `qty_ordered` fält.

## Produkttyper

The `sales_order_item` hämtar information om alla [produkttyper](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) som köptes. En vanlig vana inom [!DNL Adobe Commerce] är att erbjuda konfigurerbara produkter, med andra ord en produkt som kan anpassas efter storlek, färg och andra produktattribut. Även om en konfigurerbar produkt har sin egen `sku`kan den gälla flera enkla produkter, där varje enskild produkt representerar en unik produktkonfiguration. Se [konfigurera produkter](https://developer.adobe.com/commerce/webapi/rest/tutorials/configurable-product/) för mer information.

Ta till exempel en konfigurerbar produkt som t-shirt. När en kund checkar ut väljer han/hon alternativ för att ändra färg och storlek. Om kunden väljer en färg på `blue`och en storlek på `small`och till slut köpa en enkel produkt som `t-shirt-blue-small` som avser tillbaka till huvudprodukten i `t-shirt`.

När en konfigurerbar produkt ingår i en beställning genereras två rader i `sales_order_item` tabell: en för [enkel](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-simple.html) `sku` och en för [konfigurerbar](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-configurable.html) överordnad. De här två posterna i `sales_order_item` tabellen kan kopplas till varandra genom följande join:

* (enkelt) `sales_order_item.parent_item_id` => (konfigurerbar) `sales_order_item.item_id`

Det är därför möjligt att rapportera om försäljning av produkter antingen på enkel nivå eller på konfigureringsbar nivå. Som standard är alla `order-item-level` mätvärden i [!DNL Commerce Intelligence] är konfigurerade att exkludera de enkla produkterna, och *endast* rapportera om de konfigurerbara versionerna. Detta uppnås genom `Ordered products we count` filteruppsättning, som filtrerar på villkor där `parent_item_id` är `NULL`.

## Vanliga kolumner

| **Kolumnnamn** | **Beskrivning** |
|----|----|
| `base_price` | Priset för en enskild enhet av en produkt vid tidpunkten för försäljningen efter [katalogprisregler, nivårabatter och specialpriser](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) och innan moms, frakt eller kundvagnsrabatt ges. Detta representeras i butikens basvaluta. |
| `created_at` | Tidsstämpel för att skapa orderobjektet, som lagras lokalt i UTC. Beroende på din konfiguration i [!DNL Commerce Intelligence]kan den här tidsstämpeln konverteras till en rapporttidszon i [!DNL Commerce Intelligence] som skiljer sig från databasens tidszon. |
| `item_id` (PK) | Unik identifierare för registret. |
| `name` | Orderartikelns textnamn. |
| `order_id` | `Foreign key` som är kopplade till `sales_order` tabell. Gå med i `sales_order.entity_id` för att fastställa orderattribut som är kopplade till orderartikeln. |
| `parent_item_id` | `Foreign key` som relaterar en enkel produkt till dess överordnade paket eller konfigurerbara produkt. Gå med i `sales_order_item.item_id` för att fastställa överordnade produktattribut som är kopplade till en enkel produkt. För överordnade orderartiklar (dvs. paket eller konfigurerbara produkttyper), `parent_item_id` är `NULL`. |
| `product_id` | `Foreign key` som är kopplade till `catalog_product_entity` tabell. Gå med i `catalog_product_entity.entity_id` för att fastställa produktattribut som är kopplade till orderartikeln. |
| `product_type` | Typ av produkt som sålts. Potentiell [produkttyper](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) inkludera: enkel, konfigurerbar, grupperad, virtuell, paketerad och nedladdningsbar. |
| `qty_ordered` | Antal enheter som ingår i vagnen för den specifika orderartikeln vid tidpunkten för försäljningen. |
| `sku` | Unik identifierare för orderartikeln som köptes. |
| `store_id` | `Foreign key` som är kopplade till `store` tabell. Gå med i `store.store_id` för att avgöra vilken Commerce Store-vy som är kopplad till orderartikeln. |

{style="table-layout:auto"}

## Vanliga beräknade kolumner

| **Kolumnnamn** | **Beskrivning** |
|---|---|
| `Customer's email` | E-postadress till den kund som beställer. Beräknas av koppling `sales_order_item.order_id` till `sales_order.entity_id` och returnera `customer_email` fält. |
| `Customer's lifetime number of orders` | Totalt antal order som lagts av den här kunden. Beräknas av koppling `sales_order_item.order_id` till `sales_order.entity_id` och returnera `Customer's lifetime number of orders` fält. |
| `Customer's lifetime revenue` | Summan av intäkten för alla order som läggs av den här kunden. Beräknas av koppling `sales_order_item.order_id` till `sales_order.entity_id` och returnera `Customer's lifetime revenue` fält. |
| `Customer's order number` | Sekventiell orderrankning för den här kundens order. Beräknas av koppling `sales_order_item.order_id` till `sales_order.entity_id` och returnera `Customer's order number` fält. |
| `Order item total value (quantity * price)` | Totalt värde för en orderartikel vid tidpunkten för försäljningen efter [katalogprisregler, nivårabatter och specialpriser](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) och innan moms, frakt eller kundvagnsrabatt ges. Beräknas genom att multiplicera `qty_ordered` av `base_price`. |
| `Order's coupon_code` | Kupongen tillämpas på ordern. Beräknas av koppling `sales_order_item.order_id` till `sales_order.entity_id` och returnera `coupon_code` fält. |
| `Order's increment_id` | Unik identifierare för ordern. Beräknas av koppling `sales_order_item.order_id` till `sales_order.entity_id` och returnera `increment_id` fält. |
| `Order's status` | Orderns status. Beräknas av koppling `sales_order_item.order_id` till `sales_order.entity_id` och returnera `status` fält. |
| `Store name` | Namn på Commerce Store som är associerad med orderartikeln. Beräknas av koppling `sales_order_item.store_id` till `store.store_id` och returnera `name` fält. |

{style="table-layout:auto"}

## Vanliga mått

| **Måttnamn** | **Beskrivning** | **Konstruktion** |
|---|---|---|
| `Products ordered` | Den totala produktkvantitet som ingår i varukorgar vid försäljningstillfället | `Operation: Sum`<br>`Operand: qty_ordered`<br>`Timestamp: created_at` |
| `Revenue by products ordered` | Totalt värde av produkter som ingår i varukorgar vid tidpunkten för försäljningen efter att regler för katalogpriser, rabattnivåer och specialpriser har tillämpats och innan moms, frakt eller kundrabatt har tillämpats | `Operation: Sum`<br>`Operand: Order item total value (quantity * price)`<br>`Timestamp: created_at` |

{style="table-layout:auto"}

## `Foreign Key` Förena banor

`catalog_product_entity`

* Gå med i `catalog_product_entity` för att skapa kolumner som returnerar produktattribut som är kopplade till orderartikeln.
   * Sökväg: `sales_order_item.product_id` (många) => `catalog_product_entity.entity_id` (ett)

`sales_order`

* Gå med i `sales_order` om du vill skapa nya kolumner på ordningsnivå som är associerade med orderobjektet.
   * Sökväg: `sales_order_item.order_id` (många) => `sales_order.entity_id` (ett)

`sales_order_item`

* Gå med i `sales_order_item` om du vill skapa kolumner som associerar information om den överordnade konfigurerbara eller paketerade SKU:n med den enkla produkten. [Kontakta support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) om du behöver hjälp med att konfigurera dessa beräkningar, om du bygger i Data warehouse.
   * Sökväg: `sales_order_item.parent_item_id` (många) => `sales_order_item.item_id` (ett)

`store`

* Gå med i `store` för att skapa kolumner som returnerar information som är relaterad till Commerce Store som är kopplad till orderartikeln.
   * Sökväg: `sales_order_item.store_id` (många) => `store.store_id` (ett)
