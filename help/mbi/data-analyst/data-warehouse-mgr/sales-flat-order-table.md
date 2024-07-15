---
title: tabell för försäljning_order
description: Lär dig hur du arbetar med tabellen sales_order.
exl-id: 19a8ab88-de51-48f8-af39-ae4897834afe
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1200'
ht-degree: 0%

---

# `sales_order`-tabell

Tabellen `sales_order` (`sales_flat_order` på M1) är där varje order hämtas. Vanligtvis representerar varje rad en unik ordning, även om det finns några anpassade implementeringar av Commerce som leder till att en ordning delas upp i separata rader.

Det här registret innehåller alla kundorder, oavsett om beställningen har bearbetats via gästutcheckning. Om din butik godkänner gästutcheckning kan du hitta mer information om [användningsfallet](../data-warehouse-mgr/guest-orders.md).

## Vanliga kolumner

| **Kolumnnamn** | **Beskrivning** |
|---|---|
| `base_currency_code` | Valuta för alla värden som har hämtats i `base_*` fält (det vill säga `base_grand_total`, `base_subtotal` och så vidare). Detta återspeglar vanligtvis Commerce butiks standardvaluta |
| `base_discount_amount` | Rabattvärde som tillämpas på ordern |
| `base_grand_total` | Slutpris som kunden betalar på ordern, efter att moms, frakt och rabatter har lagts på. Även om den exakta beräkningen är anpassningsbar, beräknas `base_grand_total` i allmänhet som `base_subtotal` + `base_tax_amount` + `base_shipping_amount` `+` `base_discount_amount` `-` `base_gift_cards_amount` `-` `base_customer_balance_amount` |
| `base_subtotal` | Bruttovaruvärde för alla artiklar som ingår i ordern. Skatter, frakt, rabatter o.s.v. ingår inte |
| `base_shipping_amount` | Leveransvärde som lagts på ordern |
| `base_tax_amount` | Momsvärde som tillämpas på ordern |
| `billing_address_id` | `Foreign key` associerad med tabellen `sales_order_address`. Anslut till `sales_order_address.entity_id` för att fastställa faktureringsadressuppgifter som är associerade med ordern |
| `coupon_code` | Kupongen tillämpas på ordern. Om ingen kupong används är fältet `NULL` |
| `created_at` | Tidsstämpel för att skapa ordern, som lagras lokalt i UTC. Beroende på din konfiguration i [!DNL Commerce Intelligence] kan den här tidsstämpeln konverteras till en annan tidszon för rapportering i [!DNL Commerce Intelligence] än databasens tidszon |
| `customer_email` | E-postadress till den kund som beställer. Detta fylls i i alla situationer, inklusive order som bearbetas via gästutcheckning |
| `customer_group_id` | Sekundärnyckel associerad med tabellen `customer_group`. Anslut till `customer_group.customer_group_id` för att fastställa kundgruppen som är associerad med ordern |
| `customer_id` | `Foreign key` som är associerad med tabellen `customer_entity`, om kunden är registrerad. Anslut till `customer_entity.entity_id` för att fastställa vilka kundattribut som är kopplade till ordern. Om beställningen placerades via gästutcheckning är det här fältet `NULL` |
| `entity_id` (PK) | Unik identifierare för tabellen och används ofta i kopplingar till andra tabeller i Commerce-instansen |
| `increment_id` | Unik identifierare för en order och kallas ofta `order_id` i Adobe Commerce. `increment_id` används oftast för kopplingar till externa källor, till exempel [!DNL Google Ecommerce] |
| `shipping_address_id` | Sekundärnyckel associerad med tabellen `sales_order_address`. Anslut till `sales_order_address.entity_id` för att fastställa leveransadressuppgifterna som är kopplade till ordern |
| `status` | Orderstatus. Kan returnera värden som &#39;complete&#39;, &#39;processing&#39;, &#39;canceled&#39;, &#39;repaid&#39; och alla anpassade statusvärden som implementerats på Commerce-instansen. Reservation för ändringar när ordern behandlas |
| `store_id` | `Foreign key` associerad med tabellen `store`. Anslut till `store`.`store_id` för att avgöra vilken Commerce Store-vy som är associerad med ordern |

{style="table-layout:auto"}

## Vanliga beräknade kolumner

| **Kolumnnamn** | **Beskrivning** |
|---|---|
| `Billing address city` | Faktureringsort för ordern. Beräknat av koppling till `sales_order`.`billing_address_id` till `sales_order_address`.`entity_id` och returnerar fältet `city` |
| `Billing address country` | Landskod för fakturering för ordern. Beräknat av koppling till `sales_order`.`billing_address_id` till `sales_order_address`.`entity_id` och returnerar `country_id` |
| `Billing address region` | Faktureringsområde (oftast stat eller provins) för ordern. Beräknat av koppling till `sales_order`.`billing_address_id` till `sales_order_address`.`entity_id` och returnerar fältet `region` |
| `Customer's first order date` | Tidsstämpel för den första ordern som lagts av den här kunden. Anses ofta vara&quot;förvärvstidpunkten&quot; för en kund. Beräknas genom att returnera det minsta `sales_order`.`created_at`-värde för varje unik kund |
| `Customer's first order's billing region` | Faktureringsområde för värvning för kunden som lade ordern. Beräknas genom att returnera `Billing address region` som är associerad med kundens första order |
| `Customer's first order's coupon_code` | Kupongkod för den kund som lade ordern. Beräknas genom att returnera `coupon_code` som är associerad med kundens första order |
| `Customer's group code` | Gruppnamn för den kund som lade ordern. Beräknat av koppling till `sales_order`.`customer_group_id` till `customer_group`.`customer_group_id` och returnerar fältet `customer_group_code` |
| `Customer's lifetime number of coupons` | Totalt antal kuponger som tillämpas på alla order som läggs av den här kunden. Beräknas genom att räkna antalet order där `coupon_code` inte är `NULL` för varje unik kund |
| `Customer's lifetime number of orders` | Totalt antal order som lagts av den här kunden. Beräknas genom att räkna antalet rader i tabellen `sales_order` för varje unik kund |
| `Customer's lifetime revenue` | Summan av intäkten för alla order som läggs av den här kunden. Beräknas genom att summera fältet `base_grand_total` för alla order för varje unik kund |
| `Customer's order number` | Sekventiell orderrankning för den här kundens order. Beräknas genom att identifiera alla order som lagts av en kund, sortera dem i stigande ordning med tidsstämpeln `created_at` och tilldela varje order ett stegvis heltalsvärde. Till exempel returnerar kundens första order `Customer's order number` av 1, kundens andra order `Customer's order number` av 2 och så vidare. |
| `Customer's order number (previous-current)` | Rankning av kundens tidigare order sammanfogad med rangordningen för den här ordern, avgränsad med ett `-`-tecken. Beräknas genom sammanfogning (`Customer's order number` - 1) med `-` följt av `Customer's order number`. För den order som är associerad med kundens andra inköp returnerar den här kolumnen värdet `1-2`. Används oftast för att representera tiden mellan två orderhändelser (d.v.s. i tabellen&quot;Tid mellan order&quot;) |
| `Is customer's last order?` | Avgör om ordern motsvarar kundens senaste, eller senaste, order. Beräknas genom att jämföra värdet `Customer's order number` med `Customer's lifetime number of orders`. När dessa två fält är lika för den angivna ordningen returnerar kolumnen `Yes`, annars returneras `No` |
| `Number of items in order` | Total kvantitet artiklar som ingår i ordern. Beräknat av koppling till `sales_order`.`entity_id` till `sales_order_item`.`order_id` och summerar `sales_order_item`.Fältet `qty_ordered` |
| `Seconds between customer's first order date and this order` | Förfluten tid mellan denna beställning och kundens första beställning. Beräknas genom att subtrahera `Customer's first order date` från `created_at` för varje order, returneras som ett heltal i sekunder |
| `Seconds since previous order` | Förfluten tid mellan denna beställning och kundens närmast föregående order. Beräknas genom att subtrahera `created_at` för föregående order från `created_at` för den här ordern, som returneras som ett heltal i sekunder. För orderposten som motsvarar en kunds tredje order returnerar den här kolumnen antalet sekunder mellan kundens andra order och tredje order. För kundens första order returnerar det här fältet `NULL` |
| `Shipping address city` | Orderns leveransort. Beräknat av koppling till `sales_order`.`shipping_address_id` till `sales_order_address`.`entity_id` och returnerar fältet `city` |
| `Shipping address country` | Leveranslandskod för ordern. Beräknat av koppling till `sales_order`.`Shipping_address_id` till `sales_order_address`.`entity_id` och returnerar `country_id` |
| `Shipping address region` | Leveransregion (oftast stat eller provins) för ordern. Beräknat av koppling till `sales_order`.`shipping_address_id` till `sales_order_address`.`entity_id` och returnerar fältet `region` |
| `Store name` | Namnet på den Commerce-butik som är associerad med den här ordern. Beräknat av koppling till `sales_order`.`store_id` till `store`.`store_id` och returnerar fältet `name` |

## Vanliga mått

| **Måttnamn** | **Beskrivning** | **Konstruktion** |
|---|---|---|
| `Avg order value` | Den genomsnittliga intäkten per order, där intäkten definieras som `base_grand_total` | `Operation: Average`<br/>`Operand: base_grand_total`<br/>`Timestamp: created_at` |
| `Avg time between orders` | Genomsnittlig tid mellan en kunds (n-1) order och n:e order, för alla kunder och beställningar | `Operation: Average`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `GMV` | Summan av bruttovaruvärdet för alla order, där GMV definieras som delsumman, innan alla skatter och rabatter tillämpas | `Operation: Sum`<br/>`Operand: base_subtotal`<br/>`Timestamp: created_at` |
| `Median time between orders` | Mediantiden mellan en kunds (n-1) order och n:e order, för alla kunder och beställningar | `Operation: Median`<br/>`Operand: Seconds since previous order`<br/>`Timestamp:` `created_at` |
| `Orders` | Det totala antalet beställningar som har placerats | `Operation: Count`<br/>`Operand: entity_id`<br/>`Timestamp:` `created_at` |
| `Revenue` | Summan av intäkten för alla order, där intäkten definieras som det slutliga pris som kunden betalar, efter att alla skatter, rabatter, frakt osv. har tillämpats | `Operation: Sum`<br/>`Operand: base_grand_total`<br/>`Timestamp:` `created_at` |
| `Shipping` | Summan av fraktbeloppet för alla order | `Operation: Sum`<br/>`Operand: base_shipping_amount`<br/>`Timestamp:` `created_at` |
| `Tax` | Summan av moms på alla order | `Operation: Sum`<br/>`Operand:` `base_tax_amount`<br/>`Timestamp:` `created_at` |
| `Unique Customers` | Antalet unika kunder som gör en beställning inom det angivna rapporttidsintervallet. Om rapportens intervall till exempel var en vecka räknas varje kund som gör minst en beställning under en viss vecka exakt en gång, oavsett hur många beställningar de gjorde den veckan | `Operation: Count Distinct`<br/>`Operand:` `customer_email`<br/>`Timestamp:` `created_at` |

## `Foreign Key` förena banor

`customer_entity`

* Anslut till tabellen `customer_entity` om du vill skapa nya kundnivåkolumner som är kopplade till kunden som gjorde beställningen.
   * Sökväg: `sales_order.customer_id` (många) => `customer_entity.entity_id` (en)

`customer_group`

* Anslut till tabellen `customer_group` om du vill skapa kolumner som returnerar kundgruppnamnet för kunden som lade ordern.
   * Sökväg: `sales_order.customer_group_id` (många) => `customer_group.customer_group_id` (en)

`sales_order_address`

* Anslut till tabellen `sales_order_address` om du vill skapa kolumner som returnerar fakturerings- och leveransplatser som är associerade med ordern. Det går att ansluta två sökvägar beroende på om fakturerings- eller leveransinformation krävs.
   * Banor:
      * Leverans: `sales_order.shipping_address_id`(många) => `sales_order_address.entity_id` (en)
      * Fakturering: `sales_order.billing_address_id`(många) => `sales_order_address.entity_id` (en)

`store`

* Anslut till tabellen `store` om du vill skapa kolumner som returnerar information som är relaterad till den Commerce-butik som är kopplad till ordern.
   * Sökväg: `sales_order.store_id` (många) => `store.store_id` (en)
