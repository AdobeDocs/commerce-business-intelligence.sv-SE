---
title: register_quote_item
description: Lär dig hur du arbetar med tabellen quote_item.
exl-id: dad36e88-5986-4b52-8a0e-ac084fabb275
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 0%

---

# quote_item Table

Tabellen `quote_item` (`sales_flat_quote_item` på M1) innehåller poster för varje artikel som lagts till i en kundvagn, oavsett om vagnen övergavs eller konverterades till ett inköp. Varje rad representerar en vagnsartikel. På grund av tabellens potentiella storlek rekommenderar Adobe att du regelbundet tar bort poster om vissa villkor uppfylls, t.ex. om det finns några okonverterade kort som är äldre än 60 dagar.

>[!NOTE]
>
>Det går bara att analysera historiska, övergivna kundvagnar om du inte tar bort poster från tabellen `quote` och `quote_item`. Om du tar bort poster kan du bara se varukorgarna som ännu inte tagits bort från databasen.

## Vanliga inbyggda kolumner

| **Kolumnnamn** | **Beskrivning** |
|---|---|
| `base_price` | Priset för en enskild enhet av en produkt när artikeln lades till i en kundvagn, efter att [katalogprisregler, nivåindelade rabatter och specialpriser](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) har tillämpats och innan moms, frakt eller kundrabatter har tillämpats. Detta representeras i butikens basvaluta. |
| `created_at` | Tidsstämpel för att skapa varukorgen, som lagras lokalt i UTC. Beroende på din konfiguration i [!DNL Commerce Intelligence] kan den här tidsstämpeln konverteras till en annan tidszon för rapportering i [!DNL Commerce Intelligence] än databasens tidszon |
| `item_id` (PK) | Unik identifierare för registret |
| `name` | Orderartikelns textnamn |
| `parent_item_id` | `Foreign key` som relaterar en enkel produkt till dess överordnade paket eller konfigurerbara produkt. Anslut till `quote_item.item_id` för att fastställa överordnade produktattribut som är kopplade till en enkel produkt. För överordnade kundvagnsartiklar (dvs. paket eller konfigurerbara produkttyper) är `parent_item_id` `NULL` |
| `product_id` | `Foreign key` associerad med tabellen `catalog_product_entity`. Anslut till `catalog_product_entity.entity_id` för att fastställa produktattribut som är kopplade till orderartikeln |
| `product_type` | Typ av produkt som lagts till i vagnen. Potentiella [produkttyper](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) omfattar: enkla, konfigurerbara, grupperade, virtuella, paketbaserade och hämtningsbara |
| `qty` | Antal enheter som ingår i vagnen för den aktuella varukorgen |
| `quote_id` | `Foreign key` associerad med tabellen `quote`. Koppla till `quote.entity_id` för att fastställa varukorgsattribut som är associerade med varukorgsobjektet |
| `sku` | Unik identifierare för kundvagnsartikeln |
| `store_id` | Sekundärnyckel associerad med tabellen `store`. Anslut till `store.store_id` för att fastställa vilken Commerce Store-vy som är associerad med kundvagnsobjektet |

{style="table-layout:auto"}

## Vanliga beräknade kolumner

| **Kolumnnamn** | **Beskrivning** |
|---|---|
| `Cart creation date` | Tidsstämpel som är associerad med datumet då vagnen skapades. Beräknas genom att `quote_item.quote_id` kopplas till `quote.entity_id` och tidsstämpeln `created_at` returneras |
| `Cart is active? (1/0)` | Booleskt fält som returnerar &quot;1&quot; om kundvagnen har skapats och ännu inte konverterats till en order. Returnerar &quot;0&quot; för konverterade varukorgar eller varukorgar som skapats med administratören. Beräknas genom att koppla `quote_item.quote_id` till `quote.entity_id` och returnera fältet `is_active` |
| `Cart item total value (qty * base_price)` | Totalt värde för en artikel när artikeln lades till i en kundvagn, efter att [katalogprisregler, nivåindelade rabatter och specialpriser](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) har tillämpats och innan moms, frakt eller kundrabatter har tillämpats. Beräknas genom att multiplicera `qty` med `base_price` |
| `Seconds since cart creation` | Förfluten tid mellan kundvagnens datum och nu. Beräknas genom att koppla `quote_item.quote_id` till `quote.entity_id` och returnera fältet `Seconds since cart creation` |
| `Store name` | Namn på den Commerce-butik som är associerad med orderartikeln. Beräknas genom att koppla `sales_order_item.store_id` till `store.store_id` och returnera fältet `name` |

{style="table-layout:auto"}

## Vanliga mått

| **Måttnamn** | **Beskrivning** | **Konstruktion** |
|---|---|---|
| `Number of abandoned cart items` | Total kvantitet artiklar som lagts till i varukorgar som uppfyller specifika villkor för att&quot;kunden överger&quot; | `Operation: Sum`<br/>`Operand: qty`<br/>`Timestamp: Cart creation date`<br>Filter:<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x, där &quot;x&quot; motsvarar förfluten tid (i sekunder) sedan vagnen skapades efter vilken en vagn betraktas som övergiven |
| `Abandoned cart item value` | Summan av de totala intäkterna från varukorgar som uppfyller specifika villkor för att&quot;kunden överger&quot; | `Operation: Sum`<br>`Operand: Cart item total value (qty * base_price)`<br>`Timestamp:` `Cart creation date`<br>Filter:<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x, där &quot;x&quot; motsvarar förfluten tid (i sekunder) sedan vagnen skapades efter vilken en vagn betraktas som övergiven |

{style="table-layout:auto"}

## Förena banor med sekundärnyckel

`catalog_product_entity`

* Anslut till tabellen `catalog_product_entity` om du vill skapa kolumner som returnerar produktattribut som är kopplade till kundvagnsobjektet.
   * Sökväg: `quote_item.product_id` (många) => `catalog_product_entity.entity_id` (en)

`quote`

* Anslut till tabellen `quote` om du vill skapa nya kundvagnsnivåkolumner som är associerade med kundvagnsobjektet.
   * Sökväg: `quote_item.quote_id` (många) => `quote.entity_id` (en)

`quote_item`

* Anslut till `quote_item` om du vill skapa kolumner som associerar information om den överordnade konfigurerbara eller paketerade SKU:n med den enkla produkten. [Kontakta support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) om du behöver hjälp med att konfigurera de här beräkningarna, om du bygger i Data Warehouse Manager.
   * Sökväg: `quote_item.parent_item_id` (många) => `quote_item.item_id` (en)

`store`

* Anslut till tabellen `store` om du vill skapa kolumner som returnerar information som är relaterad till den Commerce-butik som är kopplad till kundvagnsobjektet.
   * Sökväg: `quote_item.store_id` (många) => `store.store_id` (en)
