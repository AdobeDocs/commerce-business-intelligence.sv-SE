---
title: Citattabell
description: Lär dig hur du arbetar med offerttabellen.
exl-id: 3a1e9239-33a7-429e-bfc8-628c68701710
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 0%

---

# Citattabell

Tabellen `quote` (`sales_flat_quote` på M1) innehåller poster i varje kundvagn som skapats i din butik, oavsett om de övergivits eller konverterats till ett inköp. Varje rad representerar en vagn. På grund av tabellens potentiella storlek rekommenderar Adobe att du regelbundet tar bort poster om vissa villkor uppfylls, t.ex. om det finns några okonverterade kort som är äldre än 60 dagar.

>[!NOTE]
>
>Det går bara att analysera historiska, övergivna kundvagnar om du inte tar bort poster från tabellen `quote`. Om du tar bort poster kan du bara se varukorgarna som ännu inte tagits bort från databasen.

## Vanliga inbyggda kolumner

| **Kolumnnamn** | **Beskrivning** |
|---|---|
| `base_currency_code` | Valuta för alla värden som har hämtats i `base_*` fält (det vill säga `base_grand_total`, `base_subtotal` och så vidare). Detta återspeglar vanligtvis Commerce butiks standardvaluta |
| `base_grand_total` | Slutligt pris som anges till kunden för vagnen, efter att alla skatter, frakt och rabatter har tillämpats. Även om den exakta beräkningen är anpassningsbar, beräknas `base_grand_total` i allmänhet som `base_subtotal` + `base_tax_amount` + `base_shipping_amount` + `base_discount_amount` - `base_gift_cards_amount` - `base_customer_balance_amount` |
| `base_subtotal` | Bruttovaruvärde för alla artiklar i vagnen. Skatter, frakt, rabatter o.s.v. ingår inte |
| `created_at` | Tidsstämpel för att skapa kundvagnen, som lagras lokalt i UTC. Beroende på din konfiguration i [!DNL Commerce Intelligence] kan den här tidsstämpeln konverteras till en annan tidszon för rapportering i [!DNL Commerce Intelligence] än databasens tidszon |
| `customer_email` | E-postadress till den kund som skapade vagnen |
| `customer_id` | `Foreign key` som är associerad med tabellen `customer_entity`, om kunden är registrerad. Anslut till `customer_entity.entity_id` för att fastställa vilka kundattribut som är kopplade till användaren som skapade kundvagnen. Om vagnen skapades via gästutcheckning är det här fältet `NULL` |
| `entity_id` (PK) | Unik identifierare för tabellen och används ofta i kopplingar till andra tabeller i Commerce-instansen |
| `is_active` | Booleskt fält som returnerar &quot;1&quot; om kundvagnen har skapats och ännu inte konverterats till en order. Returnerar &quot;0&quot; för konverterade varukorgar eller varukorgar som skapats av administratören |
| `items_qty` | Summan av den totala kvantiteten av alla artiklar som ingår i vagnen |
| `reserved_order_id` | `Foreign key` associerad med tabellen `sales_order`. Anslut till `sales_order.increment_id` för att fastställa orderdetaljer som är kopplade till en konverterad kundvagn. För varukorgar som inte är associerade med en konverterad order återstår `reserved_order_id` `NULL` |
| `store_id` | `Foreign key` associerad med tabellen `store`. Anslut till `store`.`store_id` för att avgöra vilken Commerce Store-vy som är associerad med kundvagnen |

{style="table-layout:auto"}

## Vanliga beräknade kolumner

| **Kolumnnamn** | **Beskrivning** |
|---|---|
| `Order date` | Tidsstämpel som visar orderskapandedatum för konverterade kundvagnar. Beräknas genom att koppla `quote.reserved_order_id` till `sales_order.increment_id` och returnera fältet `sales_order.created_at` |
| `Seconds between cart creation and order` | Förfluten tid mellan att skapa kundvagn och att skapa order. Beräknat genom subtraktion av `created_at` från `Order date`, returnerat som ett heltal i sekunder |
| `Seconds since cart creation` | Förfluten tid mellan kundvagnens datum och nu. Beräknas genom att subtrahera `created_at` från serverns tidsstämpel när frågan körs och returneras som ett heltal i sekunder. De vanligaste för att identifiera en kundvagns ålder |
| `Store name` | Namnet på den Commerce-butik som är associerad med den här ordern. Beräknas genom att koppla `quote.store_id` till `store.store_id` och returnera fältet `name` |

{style="table-layout:auto"}

## Vanliga mått

| **Måttnamn** | **Beskrivning** | **Konstruktion** |
|---|---|---|
| `Number of abandoned carts` | Antal kundvagnar som uppfyller specifika villkor för att&quot;kunden överger&quot; | `Operation: Count`<br/>`Operand:` `entity_id`<br/>`Timestamp:` `created_at`<br/>Filter:<br><br>- \[`A`\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x, där &quot;x&quot; motsvarar förfluten tid (i sekunder) sedan vagnen skapades och en vagn anses övergiven |
| `Avg time to cart conversion` | Genomsnittlig tid mellan att skapa kundvagn och att skapa order för konverterade kundvagnar | `Operation: Average`<br>`Operand:` `Seconds between cart creation and order`<br>`Timestamp:` `created_at` |
| `Abandoned cart value` | Summan av den totala övergivna potentiella intäkten i kundvagnen, där intäkten definieras som fältet `base_grand_total` | `Operation: Sum`<br>`Operand:` `base_grand_total`<br>`Timestamp:` `created_at`<br>Filter:<br><br>- \[A\] `is_active` = 1<br>- \[`B`\] `items_count` > 0<br>- \[`C`\] `Seconds since cart creation` > x, där &quot;x&quot; motsvarar förfluten tid (i sekunder) sedan vagnen skapades efter vilken en vagn anses övergiven |

{style="table-layout:auto"}

## Förena banor med sekundärnyckel

`customer_entity`

* Anslut till tabellen `customer_entity` om du vill skapa nya kundnivåkolumner som är kopplade till kunden som skapade kundvagnen.
   * Sökväg: `quote.customer_id` (många) => `customer_entity.entity_id` (en)

`sales_order`

* Koppla till tabellen `sales_order` om du vill skapa kolumner som returnerar orderinformation som är kopplad till en konverterad kundvagn.
   * Sökväg:`quote.reserved_order_id` (många) => `sales_order.increment_id` (en)

`store`

* Anslut till tabellen `store` om du vill skapa kolumner som returnerar information som är relaterad till den Commerce-butik som är kopplad till kundvagnen.
   * Sökväg: `quote.store_id` (många) => `store.store_id` (en)
