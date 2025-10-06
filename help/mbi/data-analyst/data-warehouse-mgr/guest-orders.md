---
title: Gästorder
description: Lär dig mer om hur gästbeställningarna påverkar dina data och vilka alternativ du måste ha för att kunna hantera gästbeställningar i din [!DNL Commerce Intelligence] Data Warehouse.
exl-id: cd5120ca-454c-4cf4-acb4-3aebe06cdc9a
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '566'
ht-degree: 0%

---

# Gästorder

När du granskar dina beställningar och märker att många `customer\_id`-värden är null eller inte har något värde att koppla tillbaka till tabellen `customers`, indikerar detta att din butik tillåter gästbeställningar. Det innebär att tabellen `customers` troligen inte omfattar alla dina kunder.

I det här avsnittet diskuteras hur gästbeställningarna påverkar dina data och vilka alternativ du måste använda för att hantera gästbeställningar i din [!DNL Commerce Intelligence] Data Warehouse.

## Påverkan av gästorder på data

I den typiska e-handelsdatabasen finns det en `orders`-tabell som ansluter till en `customers`-tabell. Varje rad i tabellen `orders` har en `customer\_id`-kolumn som är unik för en rad i tabellen `customers`.

* **Om alla kunder är registrerade** och gästorder inte tillåts innebär det att alla poster i tabellen `orders` har ett värde i kolumnen `customer\_id`. Därför kopplas varje order tillbaka till tabellen `customers`.

  ![Datatabell för gästorder som visar kundinformation](../../assets/guest-orders-4.png)

* **Om gästorder tillåts** innebär det att vissa order inte har något värde i kolumnen `customer\_id`. Endast registrerade kunder får ett värde för kolumnen `customer\_id` i tabellen `orders`. Kunder som inte är registrerade får ett `NULL`-värde (eller tomt) för den här kolumnen. Därför har inte alla orderposter matchande poster i tabellen `customers`.

  >[!NOTE]
  >
  >För att identifiera den unika individ som gjorde ordern måste det finnas ett annat unikt användarattribut bredvid `customer\_id` som är kopplat till en order. Normalt används kundens e-postadress.

## Så här tar du med gästbeställningar i Data Warehouse-inställningarna i beräkningen

Vanligtvis tar den säljtekniker som implementerar ditt konto hänsyn till gästbeställningar när du bygger grunden för din Data Warehouse.

Det bästa sättet att ta med gästbeställningar är att basera alla kundnivåvärden på tabellen `orders`. Den här konfigurationen använder ett unikt kund-ID som alla kunder har, inklusive gäster (vanligtvis används kundens e-post). Registreringsdata från tabellen `customers` ignoreras. Med det här alternativet inkluderas endast kunder som har gjort minst ett köp i kundnivårapporter. Registrerade användare som ännu inte har gjort ett inköp inkluderas inte. Med det här alternativet baseras ditt `New customer`-mått på kundens första orderdatum i tabellen `orders`.

Du kan lägga märke till att filtret `Customers we count` som har angetts i den här typen av inställningar har ett filter för `Customer's order number = 1`.

![Filteruppsättningskonfiguration för att exkludera gästorder](../../assets/guest-orders-filter-set.png)

I en situation utan gästorder finns varje kund som en unik rad i kundtabellen (se bild 1). Ett mätvärde som `New customers` kan bara räkna ID:t för den här tabellen baserat på `created\_at`-datumet för att förstå nya kunder baserat på registreringsdatumet.

I en gästorderkonfiguration där alla kundvärden är baserade på tabellen `orders` för att kunna hantera gästorder måste du se till att du är `not counting customers twice`. Om du räknar ID:t för ordertabellen, räknar du varje order. Om du i stället räknar ID:t i tabellen `orders` och använder ett filter, `Customer's order number = 1`, kommer du att räkna varje unik kund `only one time`. Detta gäller för alla kundnivåmått som `Customer's lifetime revenue` eller `Customer's lifetime number of orders`.

Ovanför kan du se att det finns null `customer\_ids` i tabellen `orders`. Om du använder `customer\_email` för att identifiera unika kunder ser du att `erin@test.com` har placerat tre (3) order. Därför kan du skapa ett `New customers`-mått i din `orders`-tabell baserat på följande villkor:

* `Operation table = orders`
* `Operation column = id`
* `Operation = count`
* `Timestamp = Customer's first order date`
* `Filter = Customer's we count (where Customer's order number = 1)`
