---
title: customer_entity, tabell
description: Lär dig hur du får åtkomst till poster för alla registrerade konton.
exl-id: 24bf0e66-eea0-45ea-8ce6-4ff99b678201
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '610'
ht-degree: 0%

---

# customer_entity-tabell

Registret `customer_entity` innehåller poster för alla registrerade konton. Ett konto anses vara registrerat om de registrerar sig för ett konto, oavsett om de genomför ett köp eller inte. Varje rad motsvarar ett unikt registrerat konto, vilket identifieras av kontots `entity_id`.

Det här registret innehåller inga poster med kunder som gör en beställning via gästutcheckning. Om din butik godkänner gästutcheckning kan du läsa [hur du kontoför gästbeställningar](../data-warehouse-mgr/guest-orders.md) för dessa beställningar.

## Vanliga kolumner

| **Kolumnnamn** | **Beskrivning** |
|---|---|
| `created_at` | Tidsstämpel som motsvarar kontots registreringsdatum, lagras lokalt i UTC. Beroende på din konfiguration i [!DNL Commerce Intelligence] kan den här tidsstämpeln konverteras till en annan tidszon för rapportering i [!DNL Commerce Intelligence] än databasens tidszon |
| `email` | E-postadress som är associerad med kontot |
| `entity_id` (PK) | Unik identifierare för tabellen och används ofta i kopplingar till `customer_id` i andra tabeller i instansen |
| `group_id` | Sekundärnyckel associerad med tabellen `customer_group`. Anslut till `customer_group.customer_group_id` för att fastställa kundgruppen som är associerad med det registrerade kontot |
| `store_id` | Sekundärnyckel associerad med tabellen `store`. Anslut till `store`.`store_id` för att avgöra vilken Commerce Store-vy som är associerad med det registrerade kontot |

{style="table-layout:auto"}

## Vanliga beräknade kolumner

| **Kolumnnamn** | **Beskrivning** |
|---|---|
| `Customer's first 30 day revenue` | Summan av alla intäkter för alla order som läggs av den här kunden inom 30 dagar efter kundens första orderdatum. Beräknas genom att koppla `customer_entity.entity_id` till `sales_order.customer_id` och summera fältet `base_grand_total` för alla order där `sales_order.Seconds between customer's first order date and this order` ≤ 2592000, vilket är antalet sekunder på 30 dagar |
| `Customer's first order date` | Tidsstämpel för den första ordern som lagts av den här kunden. Beräknas genom att koppla `customer_entity.entity_id` till `sales_order.customer_id` och returnera miniminivån `sales_order`.`created_at` värde |
| `Customer's first order's billing region` | Faktureringsområde som är associerat med kundens första order. Beräknas genom att koppla `customer_entity.entity_id` till `sales_order.customer_id` och returnera `Billing address region` där `sales_order.Customer's order number` = 1 |
| `Customer's first order's coupon_code` | Kupongkod som är kopplad till kundens första order. Beräknas genom att koppla `customer_entity.entity_id` till `sales_order.customer_id` och returnera `sales_order.coupon_code` där `sales_order.Customer's order number` = 1 |
| `Customer's group code` | Den registrerade kundens gruppnamn. Beräknas genom att `customer_entity.group_id` kopplas till `customer_group`.`customer_group_id` och returnerar fältet `customer_group_code` |
| `Customer's lifetime number of coupons` | Totalt antal kuponger som tillämpas på alla order som läggs av den här kunden. Beräknas genom att koppla `customer_entity.entity_id` till `sales_order.customer_id` och räkna antalet order där `sales_order.coupon_code` inte är `NULL` |
| `Customer's lifetime number of orders` | Totalt antal order som lagts av den här kunden. Beräknas genom att koppla `customer_entity.entity_id` till `sales_order.customer_id` och räkna antalet rader i tabellen `sales_order` |
| `Customer's lifetime revenue` | Summan av intäkten för alla order som läggs av den här kunden. Beräknas genom att koppla `customer_entity.entity_id` till `sales_order.customer_id` och summera fältet `base_grand_total` för alla order som den här kunden har placerat |
| `Seconds since customer's first order date` | Förfluten tid mellan kundens första orderdatum och nu. Beräknas genom att subtrahera `Customer's first order date` från serverns tidsstämpel när frågan körs, som returneras som ett heltal i sekunder |
| `Store name` | Namnet på den Commerce-butik som är associerad med det här registrerade kontot. Beräknas genom att koppla `customer_entity.store_id` till `store.store_id` och returnera fältet `name` |

{style="table-layout:auto"}

## Vanliga mått

| **Måttnamn** | **Beskrivning** | **Konstruktion** |
|---|---|---|
| `Avg first 30 day revenue` | Genomsnittlig intäkt per kund för beställningar som gjorts inom 30 dagar efter kundens första beställning | Åtgärd: Genomsnitt<br/>operand: `Customer's first 30 day revenue`<br/>Tidsstämpel: `created_at`<br/>Filter:<br/><br/>- \[A\] `Seconds since customer's first order date` ≥ 2592000 (exkluderar kunder som ännu inte har nått 30 dagar sedan den första beställningen) |
| `Avg lifetime coupons` | Genomsnittligt antal kuponger som tillämpas på order per kund under deras livstid | Åtgärd: Genomsnitt<br/>operand: `Customer's lifetime number of coupons`<br/>Tidsstämpel: `created_at` |
| `Avg lifetime orders` | Genomsnittligt antal beställningar per kund under deras livstid | Åtgärd: Genomsnitt<br/>operand: `Customer's lifetime number of orders`<br/>Tidsstämpel: `created_at` |
| `Avg lifetime revenue` | Genomsnittlig total intäkt per kund för alla beställningar som gjorts under deras livstid | Åtgärd: Genomsnitt<br/>operand: `Customer's lifetime revenue`<br/>Tidsstämpel: `created_at` |
| `New customers` | Antalet kunder med minst en order, räknat på datumet för deras första order. Exkluderar konton som registrerar men aldrig gör en beställning | Åtgärd: Antal<br/>operand: `entity_id`<br/>Tidsstämpel: `Customer's first order date` |
| `Registered accounts` | Antalet registrerade konton. Inkluderar alla registrerade konton, oavsett om kontot någonsin beställt | Åtgärd: Antal<br/>operand: `entity_id`<br/>Tidsstämpel: `created_at` |

{style="table-layout:auto"}

## Förena banor med sekundärnyckel

`customer_group`

* Anslut till tabellen `customer_group` om du vill skapa kolumner som returnerar kundgruppnamnet för det registrerade kontot.
   * Sökväg: `customer_entity.group_id` (många) => `customer_group.customer_group_id` (en)

`store`

* Anslut till tabellen `store` om du vill skapa kolumner som returnerar information som är relaterad till butiken som är kopplad till det registrerade kontot.
   * Sökväg: `customer_entity.store_id` (många) => `store.store_id` (en)
