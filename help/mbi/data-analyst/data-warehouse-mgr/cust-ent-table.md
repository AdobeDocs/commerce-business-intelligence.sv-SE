---
title: customer_entity, tabell
description: Lär dig hur du får åtkomst till poster för alla registrerade konton.
exl-id: 24bf0e66-eea0-45ea-8ce6-4ff99b678201
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '601'
ht-degree: 0%

---

# customer_entity Table

The `customer_entity` tabellen innehåller poster för alla registrerade konton. Ett konto anses vara registrerat om de registrerar sig för ett konto, oavsett om de genomför ett köp eller inte. Varje rad motsvarar ett unikt registrerat konto, vilket framgår av kontots `entity_id`.

Det här registret innehåller inga poster med kunder som gör en beställning via gästutcheckning. Om din butik godkänner utcheckning av gäster, [läs hur du konto](../data-warehouse-mgr/guest-orders.md) för dessa kunder.

## Vanliga kolumner

| **Kolumnnamn** | **Beskrivning** |
|---|---|
| `created_at` | Tidsstämpel som motsvarar kontots registreringsdatum, lagras lokalt i UTC. Beroende på din konfiguration i [!DNL MBI]kan den här tidsstämpeln konverteras till en rapporttidszon i [!DNL MBI] som skiljer sig från databasens tidszon |
| `email` | E-postadress som är associerad med kontot |
| `entity_id` (PK) | Unik identifierare för tabellen och används ofta i kopplingar till `customer_id` i andra tabeller i instansen |
| `group_id` | Sekundärnyckel som är associerad med `customer_group` tabell. Gå med i `customer_group.customer_group_id` för att fastställa kundgruppen som är associerad med det registrerade kontot |
| `store_id` | Sekundärnyckel som är associerad med `store` tabell. Gå med i `store`.`store_id` för att avgöra vilken Commerce Store-vy som är associerad med det registrerade kontot |

{style="table-layout:auto"}

## Vanliga beräknade kolumner

| **Kolumnnamn** | **Beskrivning** |
|---|---|
| `Customer's first 30 day revenue` | Summan av alla intäkter för alla order som läggs av den här kunden inom 30 dagar från kundens första orderdatum. Beräknas av koppling `customer_entity.entity_id` till `sales_order.customer_id` och sammanfatta `base_grand_total` fält för alla order där `sales_order.Seconds between customer's first order date and this order` ≤ 2592000, vilket är antalet sekunder på 30 dagar |
| `Customer's first order date` | Tidsstämpel för den första ordern som lagts av den här kunden. Beräknas av koppling `customer_entity.entity_id` till `sales_order.customer_id` och returnera minimivärdet `sales_order`.`created_at` value |
| `Customer's first order's billing region` | Faktureringsområde som är associerat med kundens första order. Beräknas av koppling `customer_entity.entity_id` till `sales_order.customer_id` och returnera `Billing address region` där `sales_order.Customer's order number` = 1 |
| `Customer's first order's coupon_code` | Kupongkod som är kopplad till kundens första order. Beräknas av koppling `customer_entity.entity_id` till `sales_order.customer_id` och returnera `sales_order.coupon_code` där `sales_order.Customer's order number` = 1 |
| `Customer's group code` | Den registrerade kundens gruppnamn. Beräknas av koppling `customer_entity.group_id` till `customer_group`.`customer_group_id` och returnera `customer_group_code` fält |
| `Customer's lifetime number of coupons` | Totalt antal kuponger som tillämpas på alla order som den här kunden lägger. Beräknas av koppling `customer_entity.entity_id` till `sales_order.customer_id` och räkna antalet order där `sales_order.coupon_code` är inte `NULL` |
| `Customer's lifetime number of orders` | Totalt antal order som lagts av den här kunden. Beräknas av koppling `customer_entity.entity_id` till `sales_order.customer_id` och räkna antalet rader i `sales_order` table |
| `Customer's lifetime revenue` | Summan av intäkten för alla order som läggs av den här kunden. Beräknas av koppling `customer_entity.entity_id` till `sales_order.customer_id` och sammanfatta `base_grand_total` fält för alla order som läggs av den här kunden |
| `Seconds since customer's first order date` | Förfluten tid mellan kundens första orderdatum och nu. Beräknas genom subtraktion `Customer's first order date` från serverns tidsstämpel när frågan körs, returneras som ett heltal i sekunder |
| `Store name` | Namnet på Commerce Store som är associerad med det här registrerade kontot. Beräknas av koppling `customer_entity.store_id` till `store.store_id` och returnera `name` fält |

{style="table-layout:auto"}

## Vanliga mått

| **Måttnamn** | **Beskrivning** | **Konstruktion** |
|---|---|---|
| `Avg first 30 day revenue` | Genomsnittlig intäkt per kund för beställningar som gjorts inom 30 dagar efter kundens första beställning | Åtgärd: Genomsnittlig<br/>Operand: `Customer's first 30 day revenue`<br/>Tidsstämpel: `created_at`<br/>Filter:<br/><br/>- \[A\] `Seconds since customer's first order date` ≥ 2592000 (omfattar inte kunder som ännu inte har nått 30 dagar sedan sin första beställning) |
| `Avg lifetime coupons` | Genomsnittligt antal kuponger som tillämpas på order per kund under deras livstid | Åtgärd: Genomsnittlig<br/>Operand: `Customer's lifetime number of coupons`<br/>Tidsstämpel: `created_at` |
| `Avg lifetime orders` | Genomsnittligt antal beställningar per kund under deras livstid | Åtgärd: Genomsnittlig<br/>Operand: `Customer's lifetime number of orders`<br/>Tidsstämpel: `created_at` |
| `Avg lifetime revenue` | Genomsnittlig total intäkt per kund för alla beställningar som gjorts under deras livstid | Åtgärd: Genomsnittlig<br/>Operand: `Customer's lifetime revenue`<br/>Tidsstämpel: `created_at` |
| `New customers` | Antalet kunder med minst en order, räknat på datumet för deras första order. Exkluderar konton som registrerar men aldrig gör en beställning | Åtgärd: Antal<br/>Operand: `entity_id`<br/>Tidsstämpel: `Customer's first order date` |
| `Registered accounts` | Antalet registrerade konton. Inkluderar alla registrerade konton, oavsett om kontot någonsin beställt | Åtgärd: Antal<br/>Operand: `entity_id`<br/>Tidsstämpel: `created_at` |

{style="table-layout:auto"}

## Förena banor med sekundärnyckel

`customer_group`

* Gå med i `customer_group` för att skapa kolumner som returnerar kundgruppnamnet för det registrerade kontot.
   * Sökväg: `customer_entity.group_id` (många) => `customer_group.customer_group_id` (ett)

`store`

* Gå med i `store` för att skapa kolumner som returnerar information som är relaterad till butiken som är kopplad till det registrerade kontot.
   * Sökväg: `customer_entity.store_id` (många) => `store.store_id` (ett)
