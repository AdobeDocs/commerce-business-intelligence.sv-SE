---
title: register_quote_item
description: Lär dig hur du arbetar med tabellen quote_item.
exl-id: dad36e88-5986-4b52-8a0e-ac084fabb275
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---

# quote_item Table

The `quote_item` tabell (`sales_flat_quote_item` på M1) innehåller uppgifter om varje artikel som lagts till i en kundvagn, oavsett om vagnen övergavs eller konverterades till ett inköp. Varje rad representerar en vagnsartikel. På grund av tabellens potentiella storlek rekommenderar Adobe att du regelbundet tar bort poster om vissa villkor uppfylls, t.ex. om det finns några okonverterade kort som är äldre än 60 dagar.

>[!NOTE]
>
>Det går bara att analysera historiska, övergivna varukorgar om du inte tar bort poster från `quote` och `quote_item` tabell. Om du tar bort poster kan du bara se varukorgarna som ännu inte tagits bort från databasen.

## Vanliga inbyggda kolumner

| **Kolumnnamn** | **Beskrivning** |
|---|---|
| `base_price` | Priset för en enskild enhet av en produkt vid den tidpunkt då artikeln lades till i en kundvagn, efter [katalogprisregler, nivårabatter och specialpriser](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) och innan moms, frakt eller kundvagnsrabatt ges. Detta representeras i butikens basvaluta. |
| `created_at` | Tidsstämpel för att skapa varukorgen, som lagras lokalt i UTC. Beroende på din konfiguration i [!DNL Commerce Intelligence]kan den här tidsstämpeln konverteras till en rapporttidszon i [!DNL Commerce Intelligence] som skiljer sig från databasens tidszon |
| `item_id` (PK) | Unik identifierare för registret |
| `name` | Orderartikelns textnamn |
| `parent_item_id` | `Foreign key` som relaterar en enkel produkt till dess överordnade paket eller konfigurerbara produkt. Gå med i `quote_item.item_id` för att fastställa överordnade produktattribut som är kopplade till en enkel produkt. För artiklar i överordnad kundvagn (dvs. paket eller konfigurerbara produkttyper), `parent_item_id` är `NULL` |
| `product_id` | `Foreign key` som är kopplade till `catalog_product_entity` tabell. Gå med i `catalog_product_entity.entity_id` för att fastställa produktattribut som är kopplade till orderartikeln |
| `product_type` | Typ av produkt som lagts till i vagnen. Potentiell [produkttyper](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/product-create.html#product-types) inkludera: enkel, konfigurerbar, grupperad, virtuell, paketerad och nedladdningsbar |
| `qty` | Antal enheter som ingår i vagnen för den aktuella varukorgen |
| `quote_id` | `Foreign key` som är kopplade till `quote` tabell. Gå med i `quote.entity_id` för att fastställa varukorgsattribut som är kopplade till varukorgen |
| `sku` | Unik identifierare för kundvagnsartikeln |
| `store_id` | Sekundärnyckel associerad med `store` tabell. Gå med i `store.store_id` för att avgöra vilken Commerce Store-vy som är associerad med kundvagnsartikeln |

{style="table-layout:auto"}

## Vanliga beräknade kolumner

| **Kolumnnamn** | **Beskrivning** |
|---|---|
| `Cart creation date` | Tidsstämpel som är associerad med datumet då vagnen skapades. Beräknat av koppling `quote_item.quote_id` till `quote.entity_id` och returnera `created_at` tidsstämpel |
| `Cart is active? (1/0)` | Booleskt fält som returnerar &quot;1&quot; om kundvagnen har skapats och ännu inte konverterats till en order. Returnerar &quot;0&quot; för konverterade varukorgar eller varukorgar som skapats med administratören. Beräknat av koppling `quote_item.quote_id` till `quote.entity_id` och returnera `is_active` fält |
| `Cart item total value (qty * base_price)` | Totalt värde för en artikel när artikeln lades till i en kundvagn, efter [katalogprisregler, nivårabatter och specialpriser](https://experienceleague.adobe.com/docs/commerce-admin/catalog/products/pricing/pricing-advanced.html) och innan moms, frakt eller kundvagnsrabatt ges. Beräknas genom att multiplicera `qty` av `base_price` |
| `Seconds since cart creation` | Förfluten tid mellan kundvagnens datum och nu. Beräknat av koppling `quote_item.quote_id` till `quote.entity_id` och returnera `Seconds since cart creation` fält |
| `Store name` | Namn på Commerce Store som är associerad med orderartikeln. Beräknat av koppling `sales_order_item.store_id` till `store.store_id` och returnera `name` fält |

{style="table-layout:auto"}

## Vanliga mått

| **Måttnamn** | **Beskrivning** | **Konstruktion** |
|---|---|---|
| `Number of abandoned cart items` | Total kvantitet artiklar som lagts till i varukorgar som uppfyller specifika villkor för att&quot;kunden överger&quot; | `Operation: Sum`<br/>`Operand: qty`<br/>`Timestamp: Cart creation date`<br>Filter:<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x, där &quot;x&quot; motsvarar förfluten tid (i sekunder) sedan vagnen skapades efter vilken en vagn betraktas som övergiven |
| `Abandoned cart item value` | Summan av de totala intäkterna från varukorgar som uppfyller specifika villkor för att&quot;kunden överger&quot; | `Operation: Sum`<br>`Operand: Cart item total value (qty * base_price)`<br>`Timestamp:` `Cart creation date`<br>Filter:<br><br>- \[`A`\] `Cart is active? (1/0)` = 1<br>- \[`B`\] `Seconds since cart creation` > x, där &quot;x&quot; motsvarar förfluten tid (i sekunder) sedan vagnen skapades efter vilken en vagn betraktas som övergiven |

{style="table-layout:auto"}

## Förena banor med sekundärnyckel

`catalog_product_entity`

* Gå med i `catalog_product_entity` för att skapa kolumner som returnerar produktattribut som är kopplade till kundvagnsartikeln.
   * Sökväg: `quote_item.product_id` (många) => `catalog_product_entity.entity_id` (ett)

`quote`

* Gå med i `quote` för att skapa nya varukorg på kundvagnsnivå som är associerade med varukorgsobjektet.
   * Sökväg: `quote_item.quote_id` (många) => `quote.entity_id` (ett)

`quote_item`

* Gå med i `quote_item` om du vill skapa kolumner som associerar information om den överordnade konfigurerbara eller paketerade SKU:n med den enkla produkten. [Kontakta support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) om du behöver hjälp med att konfigurera dessa beräkningar, om du bygger i Data Warehouse Manager.
   * Sökväg: `quote_item.parent_item_id` (många) => `quote_item.item_id` (ett)

`store`

* Gå med i `store` för att skapa kolumner som returnerar information som är relaterad till Commerce Store som är kopplad till kundvagnsartikeln.
   * Sökväg: `quote_item.store_id` (många) => `store.store_id` (ett)
