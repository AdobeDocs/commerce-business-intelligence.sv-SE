---
title: Citattabell
description: Lär dig hur du arbetar med offerttabellen.
exl-id: 3a1e9239-33a7-429e-bfc8-628c68701710
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '605'
ht-degree: 0%

---

# Citattabell

The `quote` tabell (`sales_flat_quote` på M1) innehåller uppgifter om varje kundvagn som du har skapat i din butik, oavsett om den har övergivits eller konverterats till ett inköp. Varje rad representerar en vagn. På grund av tabellens potentiella storlek rekommenderar Adobe att du regelbundet tar bort poster om vissa villkor uppfylls, t.ex. om det finns några okonverterade kort som är äldre än 60 dagar.

>[!NOTE]
>
>Det går bara att analysera historiska, övergivna varukorgar om du inte tar bort poster från `quote` tabell. Om du tar bort poster kan du bara se varukorgarna som ännu inte tagits bort från databasen.

## Vanliga inbyggda kolumner

| **Kolumnnamn** | **Beskrivning** |
|---|---|
| `base_currency_code` | Valuta för alla värden som hämtas i `base_*` fält (det vill säga `base_grand_total`, `base_subtotal`och så vidare). Detta återspeglar vanligtvis Commerce Stores standardvaluta |
| `base_grand_total` | Slutligt pris som anges till kunden för vagnen, efter att alla skatter, frakt och rabatter har tillämpats. Även om det går att anpassa den exakta beräkningen så är det i allmänhet `base_grand_total` beräknas som `base_subtotal` + `base_tax_amount` + `base_shipping_amount` + `base_discount_amount` - `base_gift_cards_amount` - `base_customer_balance_amount` |
| `base_subtotal` | Bruttovaruvärde för alla artiklar i vagnen. Skatter, frakt, rabatter o.s.v. ingår inte |
| `created_at` | Tidsstämpel för att skapa kundvagnen, som lagras lokalt i UTC. Beroende på din konfiguration i [!DNL Commerce Intelligence]kan den här tidsstämpeln konverteras till en rapporttidszon i [!DNL Commerce Intelligence] som skiljer sig från databasens tidszon |
| `customer_email` | E-postadress till den kund som skapade vagnen |
| `customer_id` | `Foreign key` som är kopplade till `customer_entity` om kunden är registrerad. Gå med i `customer_entity.entity_id` för att avgöra vilka kundattribut som är kopplade till användaren som skapade kundvagnen. Om vagnen skapades via gästutcheckning är det här fältet `NULL` |
| `entity_id` (PK) | Unik identifierare för tabellen och används ofta i kopplingar till andra tabeller i Commerce-instansen |
| `is_active` | Booleskt fält som returnerar &quot;1&quot; om kundvagnen har skapats och ännu inte konverterats till en order. Returnerar &quot;0&quot; för konverterade varukorgar eller varukorgar som skapats av administratören |
| `items_qty` | Summan av den totala kvantiteten av alla artiklar som ingår i vagnen |
| `reserved_order_id` | `Foreign key` som är kopplade till `sales_order` tabell. Gå med i `sales_order.increment_id` för att fastställa orderdetaljer som är kopplade till en konverterad kundvagn. För varukorgar som inte är kopplade till en konverterad order visas `reserved_order_id` återstår `NULL` |
| `store_id` | `Foreign key` som är kopplade till `store` tabell. Gå med i `store`.`store_id` för att avgöra vilken Commerce Store-vy som är associerad med kundvagnen |

{style="table-layout:auto"}

## Vanliga beräknade kolumner

| **Kolumnnamn** | **Beskrivning** |
|---|---|
| `Order date` | Tidsstämpel som visar orderskapandedatum för konverterade kundvagnar. Beräknat av koppling `quote.reserved_order_id` till `sales_order.increment_id` och returnera `sales_order.created_at` fält |
| `Seconds between cart creation and order` | Förfluten tid mellan att skapa kundvagn och att skapa order. Beräknas genom subtraktion `created_at` från `Order date`, returneras som ett heltal i antal sekunder |
| `Seconds since cart creation` | Förfluten tid mellan kundvagnens datum och nu. Beräknas genom subtraktion `created_at` från serverns tidsstämpel när frågan körs, returneras som ett heltal i sekunder. De vanligaste för att identifiera en kundvagns ålder |
| `Store name` | Namnet på det Commerce Store som är associerat med den här ordern. Beräknat av koppling `quote.store_id` till `store.store_id` och returnera `name` fält |

{style="table-layout:auto"}

## Vanliga mått

| **Måttnamn** | **Beskrivning** | **Konstruktion** |
|---|---|---|
| `Number of abandoned carts` | Antal kundvagnar som uppfyller specifika villkor för att&quot;kunden överger&quot; | `Operation: Count`<br/>`Operand:` `entity_id`<br/>`Timestamp:` `created_at`<br/>Filter:<br><br>- \[`A`\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x, där &quot;x&quot; motsvarar förfluten tid (i sekunder) sedan vagnen skapades efter vilken en vagn betraktas som övergiven |
| `Avg time to cart conversion` | Genomsnittlig tid mellan att skapa kundvagn och att skapa order för konverterade kundvagnar | `Operation: Average`<br>`Operand:` `Seconds between cart creation and order`<br>`Timestamp:` `created_at` |
| `Abandoned cart value` | Summan av de totala intäkterna från övergiven varukorgen, där intäkten definieras som `base_grand_total` fält | `Operation: Sum`<br>`Operand:` `base_grand_total`<br>`Timestamp:` `created_at`<br>Filter:<br><br>- \[A\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x, där &quot;x&quot; motsvarar förfluten tid (i sekunder) sedan vagnen skapades efter vilken en vagn betraktas som övergiven |

{style="table-layout:auto"}

## Förena banor med sekundärnyckel

`customer_entity`

* Gå med i `customer_entity` för att skapa nya kundnivåkolumner som är kopplade till kunden som skapade kundvagnen.
   * Sökväg: `quote.customer_id` (många) => `customer_entity.entity_id` (ett)

`sales_order`

* Gå med i `sales_order` för att skapa kolumner som returnerar orderinformation som är kopplad till en konverterad kundvagn.
   * Sökväg:`quote.reserved_order_id` (många) => `sales_order.increment_id` (ett)

`store`

* Gå med i `store` för att skapa kolumner som returnerar information som är relaterad till Commerce Store som är kopplad till kundvagnen.
   * Sökväg: `quote.store_id` (många) => `store.store_id` (ett)
