---
title: register_för försäljningsorder_artikel
description: Lär dig hur du arbetar med tabellen sales_order_item.
exl-id: 5c48e985-3ba2-414b-bd1f-555b3da763bd
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 0%

---

# `sales_order_item`-tabell

Tabellen `sales_order_item` (`sales_flat_order_item` på M1) innehåller poster för alla produkter som köpts i en beställning. Varje rad representerar en unik `sku` som ingår i en order. Antalet enheter som köptes för en viss `sku` representeras oftast av fältet `qty_ordered`.

## Produkttyper

`sales_order_item` innehåller information om alla [produkttyper](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) som köpts. Ett vanligt tillvägagångssätt i [!DNL Adobe Commerce] är att erbjuda konfigurerbara produkter, eller med andra ord en produkt som kan anpassas efter storlek, färg och andra produktattribut. Även om en konfigurerbar produkt har en egen `sku` kan den relatera till flera enkla produkter, där varje enskild produkt representerar en unik produktkonfiguration. Mer information finns i [konfigurera produkter](https://developer.adobe.com/commerce/webapi/rest/tutorials/configurable-product/).

Ta till exempel en konfigurerbar produkt som t-shirt. När en kund checkar ut väljer han/hon alternativ för att ändra färg och storlek. Om kunden väljer färgen `blue` och storleken `small`, köper de en enkel produkt som `t-shirt-blue-small` som relaterar tillbaka till den överordnade produkten `t-shirt`.

När en konfigurerbar produkt ingår i en ordning genereras två rader i tabellen `sales_order_item`: en för [simple](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-simple.html) `sku` och en för den överordnade [configurable](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/types/product-create-configurable.html) . Dessa två poster i tabellen `sales_order_item` kan relateras till varandra via följande join:

* (enkelt) `sales_order_item.parent_item_id` => (konfigurerbart) `sales_order_item.item_id`

Det är därför möjligt att rapportera om försäljning av produkter antingen på enkel nivå eller på konfigureringsbar nivå. Som standard är alla `order-item-level`-standardvärden i [!DNL Commerce Intelligence] konfigurerade att exkludera de enkla produkterna och *endast*-rapporten för de konfigurerbara versionerna. Detta uppnås med filteruppsättningen `Ordered products we count`, som filtrerar på villkoret där `parent_item_id` är `NULL`.

## Vanliga kolumner

| **Kolumnnamn** | **Beskrivning** |
|----|----|
| `base_price` | Priset för en enskild enhet av en produkt vid tidpunkten för försäljningen efter att [katalogprisregler, nivårabatter och specialpriser](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) har tillämpats och innan moms, frakt eller kundvagnsrabatter har tillämpats. Detta representeras i butikens basvaluta. |
| `created_at` | Tidsstämpel för att skapa orderobjektet, som lagras lokalt i UTC. Beroende på din konfiguration i [!DNL Commerce Intelligence] kan den här tidsstämpeln konverteras till en tidszon för rapportering i [!DNL Commerce Intelligence] som skiljer sig från databasens tidszon. |
| `item_id` (PK) | Unik identifierare för registret. |
| `name` | Orderartikelns textnamn. |
| `order_id` | `Foreign key` associerad med tabellen `sales_order`. Anslut till `sales_order.entity_id` för att fastställa orderattribut som är kopplade till orderobjektet. |
| `parent_item_id` | `Foreign key` som relaterar en enkel produkt till dess överordnade paket eller konfigurerbara produkt. Anslut till `sales_order_item.item_id` för att fastställa överordnade produktattribut som är kopplade till en enkel produkt. För överordnade orderartiklar (dvs. paket eller konfigurerbara produkttyper) är `parent_item_id` `NULL`. |
| `product_id` | `Foreign key` associerad med tabellen `catalog_product_entity`. Anslut till `catalog_product_entity.entity_id` för att fastställa produktattribut som är associerade med orderartikeln. |
| `product_type` | Typ av produkt som sålts. Möjliga [produkttyper](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) är: enkla, konfigurerbara, grupperade, virtuella, paketbaserade och hämtningsbara. |
| `qty_ordered` | Antal enheter som ingår i vagnen för den specifika orderartikeln vid tidpunkten för försäljningen. |
| `sku` | Unik identifierare för orderartikeln som köptes. |
| `store_id` | `Foreign key` associerad med tabellen `store`. Anslut till `store.store_id` för att ta reda på vilken Commerce Store-vy som är associerad med orderobjektet. |

{style="table-layout:auto"}

## Vanliga beräknade kolumner

| **Kolumnnamn** | **Beskrivning** |
|---|---|
| `Customer's email` | E-postadress till den kund som beställer. Beräknas genom att koppla `sales_order_item.order_id` till `sales_order.entity_id` och returnera fältet `customer_email`. |
| `Customer's lifetime number of orders` | Totalt antal order som lagts av den här kunden. Beräknas genom att koppla `sales_order_item.order_id` till `sales_order.entity_id` och returnera fältet `Customer's lifetime number of orders`. |
| `Customer's lifetime revenue` | Summan av intäkten för alla order som läggs av den här kunden. Beräknas genom att koppla `sales_order_item.order_id` till `sales_order.entity_id` och returnera fältet `Customer's lifetime revenue`. |
| `Customer's order number` | Sekventiell orderrankning för den här kundens order. Beräknas genom att koppla `sales_order_item.order_id` till `sales_order.entity_id` och returnera fältet `Customer's order number`. |
| `Order item total value (quantity * price)` | Totalt värde för en orderartikel vid försäljningstillfället efter att [katalogprisregler, nivårabatter och specialpriser](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) har tillämpats och innan moms, frakt eller kundrabatt har tillämpats. Beräknas genom att multiplicera `qty_ordered` med `base_price`. |
| `Order's coupon_code` | Kupongen tillämpas på ordern. Beräknas genom att koppla `sales_order_item.order_id` till `sales_order.entity_id` och returnera fältet `coupon_code`. |
| `Order's increment_id` | Unik identifierare för ordern. Beräknas genom att koppla `sales_order_item.order_id` till `sales_order.entity_id` och returnera fältet `increment_id`. |
| `Order's status` | Orderns status. Beräknas genom att koppla `sales_order_item.order_id` till `sales_order.entity_id` och returnera fältet `status`. |
| `Store name` | Namn på den Commerce-butik som är associerad med orderartikeln. Beräknas genom att koppla `sales_order_item.store_id` till `store.store_id` och returnera fältet `name`. |

{style="table-layout:auto"}

## Vanliga mått

| **Måttnamn** | **Beskrivning** | **Konstruktion** |
|---|---|---|
| `Products ordered` | Den totala produktkvantitet som ingår i varukorgar vid försäljningstillfället | `Operation: Sum`<br>`Operand: qty_ordered`<br>`Timestamp: created_at` |
| `Revenue by products ordered` | Totalt värde av produkter som ingår i varukorgar vid tidpunkten för försäljningen efter att regler för katalogpriser, rabattnivåer och specialpriser har tillämpats och innan moms, frakt eller kundrabatt har tillämpats | `Operation: Sum`<br>`Operand: Order item total value (quantity * price)`<br>`Timestamp: created_at` |

{style="table-layout:auto"}

## `Foreign Key` förena banor

`catalog_product_entity`

* Anslut till tabellen `catalog_product_entity` om du vill skapa kolumner som returnerar produktattribut som är kopplade till orderobjektet.
   * Sökväg: `sales_order_item.product_id` (många) => `catalog_product_entity.entity_id` (en)

`sales_order`

* Koppla till tabellen `sales_order` om du vill skapa nya kolumner på ordningsnivå som är associerade med orderobjektet.
   * Sökväg: `sales_order_item.order_id` (många) => `sales_order.entity_id` (en)

`sales_order_item`

* Anslut till `sales_order_item` om du vill skapa kolumner som associerar information om den överordnade konfigurerbara eller paketerade SKU:n med den enkla produkten. [Kontakta support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) om du behöver hjälp med att konfigurera de här beräkningarna, om du bygger i Data Warehouse Manager.
   * Sökväg: `sales_order_item.parent_item_id` (många) => `sales_order_item.item_id` (en)

`store`

* Anslut till tabellen `store` om du vill skapa kolumner som returnerar information som är relaterad till Commerce Store som är kopplad till orderobjektet.
   * Sökväg: `sales_order_item.store_id` (många) => `store.store_id` (en)
