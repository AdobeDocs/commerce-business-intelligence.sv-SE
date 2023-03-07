---
title: tabell för försäljning_order
description: Lär dig hur du arbetar med tabellen sales_order.
exl-id: 19a8ab88-de51-48f8-af39-ae4897834afe
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 0%

---

# `sales_order` Tabell

The `sales_order` tabell (`sales_flat_order` på M1) är där varje order hämtas. Vanligtvis representerar varje rad en unik order, även om det finns några anpassade implementeringar av Commerce som leder till att en order delas upp i separata rader.

Det här registret innehåller alla kundorder, oavsett om beställningen har bearbetats via gästutcheckning. Om din butik accepterar utcheckning av gäster kan du få mer information om detta [användningsfall](../data-warehouse-mgr/guest-orders.md).

## Vanliga kolumner

| **Kolumnnamn** | **Beskrivning** |
|---|---|
| `base_currency_code` | Valuta för alla värden som hämtas i `base_*` fält (det vill säga `base_grand_total`, `base_subtotal`och så vidare). Detta återspeglar vanligtvis Commerce Stores standardvaluta |
| `base_discount_amount` | Rabattvärde som tillämpas på ordern |
| `base_grand_total` | Slutpris som kunden betalar på ordern, efter att moms, frakt och rabatter har lagts på. Även om det går att anpassa den exakta beräkningen så är det i allmänhet `base_grand_total` beräknas som `base_subtotal` + `base_tax_amount` + `base_shipping_amount` `+` `base_discount_amount` `-` `base_gift_cards_amount` `-` `base_customer_balance_amount` |
| `base_subtotal` | Bruttovaruvärde för alla artiklar som ingår i ordern. Skatter, frakt, rabatter o.s.v. ingår inte |
| `base_shipping_amount` | Leveransvärde som lagts på ordern |
| `base_tax_amount` | Momsvärde som tillämpas på ordern |
| `billing_address_id` | `Foreign key` som är kopplade till `sales_order_address` tabell. Gå med i `sales_order_address.entity_id` för att fastställa faktureringsadressuppgifter som är kopplade till ordern |
| `coupon_code` | Kupongen tillämpas på ordern. Om ingen kupong används är detta fält `NULL` |
| `created_at` | Tidsstämpel för att skapa ordern, som lagras lokalt i UTC. Beroende på din konfiguration i [!DNL MBI]kan den här tidsstämpeln konverteras till en rapporttidszon i [!DNL MBI] som skiljer sig från databasens tidszon |
| `customer_email` | E-postadress till den kund som beställer. Detta fylls i i alla situationer, inklusive order som bearbetas via gästutcheckning |
| `customer_group_id` | Sekundärnyckel som är associerad med `customer_group` tabell. Gå med i `customer_group.customer_group_id` för att fastställa kundgruppen som är kopplad till ordern |
| `customer_id` | `Foreign key` som är kopplade till `customer_entity` om kunden är registrerad. Gå med i `customer_entity.entity_id` för att avgöra vilka kundattribut som är kopplade till ordern. Om beställningen gjordes via gästutcheckning är det här fältet `NULL` |
| `entity_id` (PK) | Unik identifierare för tabellen och används ofta i kopplingar till andra tabeller i Commerce-instansen |
| `increment_id` | Unik identifierare för en order och kallas ofta `order_id` inom Adobe Commerce. The `increment_id` används oftast för kopplingar till externa källor, som [!DNL Google Ecommerce] |
| `shipping_address_id` | Sekundärnyckel som är associerad med `sales_order_address` tabell. Gå med i `sales_order_address.entity_id` för att fastställa leveransadressuppgifter för ordern |
| `status` | Orderstatus. Kan returnera värden som &#39;complete&#39;, &#39;processing&#39;, &#39;canceled&#39;, &#39;repaid&#39; och alla anpassade statusvärden som implementerats i Commerce-instansen. Reservation för ändringar när ordern behandlas |
| `store_id` | `Foreign key` som är kopplade till `store` tabell. Gå med i `store`.`store_id` för att avgöra vilken Commerce Store-vy som är associerad med ordern |

{style="table-layout:auto"}

## Vanliga beräknade kolumner

| **Kolumnnamn** | **Beskrivning** |
|---|---|
| `Billing address city` | Faktureringsort för ordern. Beräknas av koppling `sales_order`.`billing_address_id` till `sales_order_address`.`entity_id` och returnera `city` fält |
| `Billing address country` | Landskod för fakturering för ordern. Beräknas av koppling `sales_order`.`billing_address_id` till `sales_order_address`.`entity_id` och returnera `country_id` |
| `Billing address region` | Faktureringsområde (oftast stat eller provins) för ordern. Beräknas av koppling `sales_order`.`billing_address_id` till `sales_order_address`.`entity_id` och returnera `region` fält |
| `Customer's first order date` | Tidsstämpel för den första ordern som lagts av den här kunden. Anses ofta vara&quot;förvärvstidpunkten&quot; för en kund. Beräknas genom att returnera miniminivån `sales_order`.`created_at` värde för varje unik kund |
| `Customer's first order's billing region` | Faktureringsområde för värvning för kunden som lade ordern. Beräknas genom att returnera `Billing address region` som är kopplad till kundens första order |
| `Customer's first order's coupon_code` | Kupongkod för den kund som lade ordern. Beräknas genom att returnera `coupon_code` som är kopplad till kundens första order |
| `Customer's group code` | Gruppnamn för den kund som lade ordern. Beräknas av koppling `sales_order`.`customer_group_id` till `customer_group`.`customer_group_id` och returnera `customer_group_code` fält |
| `Customer's lifetime number of coupons` | Totalt antal kuponger som tillämpas på alla order som läggs av den här kunden. Beräknas genom att räkna antalet order där `coupon_code` är inte `NULL` för varje unik kund |
| `Customer's lifetime number of orders` | Totalt antal order som lagts av den här kunden. Beräknas genom att räkna antalet rader i `sales_order` tabell för varje unik kund |
| `Customer's lifetime revenue` | Summan av intäkten för alla order som läggs av den här kunden. Beräknas genom att summera `base_grand_total` fält för alla order för varje unik kund |
| `Customer's order number` | Sekventiell orderrankning för den här kundens order. Beräknas genom att identifiera alla order som lagts av en kund och sortera dem i stigande ordning efter `created_at` tidsstämpla och tilldela varje order ett stegvis ökande heltalsvärde. Till exempel returnerar kundens första order en `Customer's order number` av 1 returnerar kundens andra order `Customer's order number` av 2 och så vidare. |
| `Customer's order number (previous-current)` | Rankning av kundens tidigare order sammanfogad med rangordningen för den här ordern, åtskild med en `-` tecken. Beräknas genom sammanfogning (&quot;`Customer's order number` - 1&quot;) med &quot;`-`&quot; följt av &quot;`Customer's order number`&quot;. För den order som är associerad med kundens andra inköp returnerar den här kolumnen till exempel värdet `1-2`. Används oftast för att representera tiden mellan två orderhändelser (d.v.s. i tabellen&quot;Tid mellan order&quot;) |
| `Is customer's last order?` | Avgör om ordern motsvarar kundens senaste, eller senaste, order. Beräknas genom att jämföra `Customer's order number` värde med `Customer's lifetime number of orders`. När dessa två fält är lika för den angivna ordningen returnerar kolumnen &quot;Ja&quot;; annars returneras&quot;Nej&quot; |
| `Number of items in order` | Total kvantitet artiklar som ingår i ordern. Beräknas av koppling `sales_order`.`entity_id` till `sales_order_item`.`order_id` och sammanfatta `sales_order_item`.`qty_ordered` fält |
| `Seconds between customer's first order date and this order` | Förfluten tid mellan denna beställning och kundens första beställning. Beräknas genom subtraktion `Customer's first order date` från `created_at` för varje order, returneras som ett heltal i sekunder |
| `Seconds since previous order` | Förfluten tid mellan denna beställning och kundens närmast föregående order. Beräknas genom att subtrahera `created_at` för föregående order från `created_at` i den här ordningen, returneras som ett heltal i sekunder. För orderposten som motsvarar en kunds tredje order returnerar den här kolumnen antalet sekunder mellan kundens andra order och tredje order. För kundens första order returnerar det här fältet `NULL` |
| `Shipping address city` | Orderns leveransort. Beräknas av koppling `sales_order`.`shipping_address_id` till `sales_order_address`.`entity_id` och returnera `city` fält |
| `Shipping address country` | Leveranslandskod för ordern. Beräknas av koppling `sales_order`.`Shipping_address_id` till `sales_order_address`.`entity_id` och returnera `country_id` |
| `Shipping address region` | Leveransregion (oftast stat eller provins) för ordern. Beräknas av koppling `sales_order`.`shipping_address_id` till `sales_order_address`.`entity_id` och returnera `region` fält |
| `Store name` | Namnet på det Commerce Store som är associerat med den här ordern. Beräknas av koppling `sales_order`.`store_id` till `store`.`store_id` och returnera `name` fält |

## Vanliga mått

| **Måttnamn** | **Beskrivning** | **Konstruktion** |
|---|---|---|
| `Avg order value` | Genomsnittlig intäkt per order, där intäkten definieras som `base_grand_total` | `Operation: Average`<br/>`Operand: base_grand_total`<br/>`Timestamp: created_at` |
| `Avg time between orders` | Genomsnittlig tid mellan en kunds (n-1) order och n:e order, för alla kunder och beställningar | `Operation: Average`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `GMV` | Summan av bruttovaruvärdet för alla order, där GMV definieras som delsumman, innan alla skatter och rabatter tillämpas | `Operation: Sum`<br/>`Operand: base_subtotal`<br/>`Timestamp: created_at` |
| `Median time between orders` | Mediantiden mellan en kunds (n-1) order och n:e order, för alla kunder och beställningar | `Operation: Median`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `Orders` | Det totala antalet beställningar som har placerats | `Operation: Count`<br/>`Operand: entity_id`<br/>`Timestamp:` `created_at` |
| `Revenue` | Summan av intäkten för alla order, där intäkten definieras som det slutliga pris som kunden betalar, efter att alla skatter, rabatter, frakt osv. har tillämpats | `Operation: Sum`<br/>`Operand: base_grand_total`<br/>`Timestamp:` `created_at` |
| `Shipping` | Summan av fraktbeloppet för alla order | `Operation: Sum`<br/>`Operand: base_shipping_amount`<br/>`Timestamp:` `created_at` |
| `Tax` | Summan av moms på alla order | `Operation: Sum`<br/>`Operand:` `base_tax_amount`<br/>`Timestamp:` `created_at` |
| `Unique Customers` | Antalet unika kunder som gör en beställning inom det angivna rapporttidsintervallet. Om rapportens intervall till exempel var en vecka räknas varje kund som gör minst en beställning under en viss vecka exakt en gång, oavsett hur många beställningar de gjorde den veckan | `Operation: Count Distinct`<br/>`Operand:` `customer_email`<br/>`Timestamp:` `created_at` |

## `Foreign Key` Förena banor

`customer_entity`

* Gå med i `customer_entity` för att skapa nya kundnivåkolumner som är kopplade till kunden som gjorde beställningen.
   * Sökväg: `sales_order.customer_id` (många) => `customer_entity.entity_id` (ett)

`customer_group`

* Gå med i `customer_group` för att skapa kolumner som returnerar kundgruppnamnet för den kund som lade ordern.
   * Sökväg: `sales_order.customer_group_id` (många) => `customer_group.customer_group_id` (ett)

`sales_order_address`

* Gå med i `sales_order_address` för att skapa kolumner som returnerar fakturerings- och leveransplatser som är associerade med ordern. Det går att ansluta två sökvägar beroende på om fakturerings- eller leveransinformation krävs.
   * Banor:
      * Leverans: `sales_order.shipping_address_id`(många) => `sales_order_address.entity_id` (ett)
      * Fakturering: `sales_order.billing_address_id`(många) => `sales_order_address.entity_id` (ett)

`store`

* Gå med i `store` för att skapa kolumner som returnerar information som är relaterad till det Commerce Store som är associerad med ordern.
   * Sökväg: `sales_order.store_id` (många) => `store.store_id` (ett)
