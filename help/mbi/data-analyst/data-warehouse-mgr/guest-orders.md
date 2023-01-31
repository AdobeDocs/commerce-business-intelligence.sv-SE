---
title: Gästorder
description: Lär dig mer om hur gästbeställningarna påverkar dina data och vilka alternativ du måste ha för att hantera gästbeställningar på rätt sätt i dina [!DNL MBI] data warehouse.
exl-id: cd5120ca-454c-4cf4-acb4-3aebe06cdc9a
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# Gästorder

När du granskar dina beställningar, om du märker att så många `customer\_id` är null eller har inget värde att koppla tillbaka till `customers` tabellen, är det oftast en indikation på att din butik tillåter gästbeställningar. Det innebär att `customers` tabellen är antagligen inte omfattande för alla era kunder.

I det här avsnittet diskuterar vi vilken inverkan gästbeställningar har på dina data och vilka alternativ du måste ha för att hantera gästbeställningar i din [!DNL MBI] data warehouse.

## Påverkan av gästorder på data

I den typiska e-handelsdatabasen finns en `orders` tabell som sammanfogas med en `customers` tabell. Varje rad på `orders` tabellen har en `customer\_id` kolumn som är unik för en rad på `customers` tabell.

* **Om alla kunder är registrerade** och gästorder är inte tillåtna, vilket innebär att alla poster i `orders` tabellen har ett värde i `customer\_id` kolumn. Därför går varje order tillbaka till `customers` tabell. Det visas i bilden nedan.

   ![](../../assets/guest-orders-4.png)

* **Om gästorder tillåts** betyder det att vissa order inte har något värde i `customer\_id` kolumn. Endast registrerade kunder får ett värde för `customer\_id` kolumn på `orders` tabell. Kunder som inte är registrerade får en `NULL` (eller tomt) värde för den här kolumnen. Därför kommer inte alla orderposter att ha matchande poster i `customers` tabell.

   >[!NOTE]
   >
   >För att identifiera den unika personen som gjorde ordern måste det finnas ett annat unikt användarattribut bredvid `customer\_id` kopplade till en order. Normalt används kundens e-postadress.

## Så här tar du med gästbeställningar i data warehouse

Vanligtvis kommer den säljtekniker som implementerar ditt konto att ta hänsyn till gästbeställningar när du bygger grunden för din data warehouse.

Det bästa sättet att ta hänsyn till gästbeställningar är att basera alla kundnivåvärden på `orders` tabell. Den här konfigurationen använder ett unikt kund-ID som alla kunder har, inklusive gäster (vanligtvis används kundens e-post). Detta ignorerar registreringsdata från `customers` tabell. Med det här alternativet inkluderas endast kunder som har gjort minst ett köp i kundnivårapporter. Registrerade användare som ännu inte har gjort ett inköp inkluderas inte. Med det här alternativet kan du `New customer` mätvärdet baseras på kundens första orderdatum i `orders` tabell.

Du kan lägga märke till att `Customers we count` filteruppsättningar i den här typen av inställningar har ett filter för `Customer's order number = 1`. Låt oss tänka på varför det här är.

![](../../assets/guest-orders-filter-set.png)

I en situation utan gästorder finns varje kund som en unik rad i kundtabellen (se bild 1). Ett mått som `New customers` kan bara räkna ID:t för den här tabellen baserat på `created\_at` datum för att förstå nya kunder baserat på registreringsdatum.

I en gästorderinställning där alla kundvärden baseras på `orders` register för att ta hänsyn till gästbeställningar måste du se till att du `not counting customers twice`. Om du räknar ID:t i ordertabellen kommer du att räkna varje order. Om du i stället räknar ID:t på `orders` tabell och använda ett filter, `Customer's order number = 1`, kommer ni att räkna med varje unik kund `only one time`. Detta gäller alla kundnivåvärden som `Customer's lifetime revenue` eller `Customer's lifetime number of orders`.

I bild 2 ovan ser du att det finns null `customer\_ids` i `orders` tabell. Om vi använder `customer\_email` för att identifiera unika kunder ser du att `erin@test.com` har gjort tre (3) beställningar. Därför kan vi bygga en `New customers` mätvärden på `orders` tabell baserad på följande villkor:

* `Operation table = orders`
* `Operation column = id`
* `Operation = count`
* `Timestamp = Customer's first order date`
* `Filter = Customer's we count (where Customer's order number = 1)`
