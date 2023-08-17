---
title: Konsolidera dina tabeller
description: Lär dig hur du konsoliderar tabeller och databaser.
exl-id: 6065bed3-fb84-4147-a223-92dc3e1b15a5
role: Admin, User
feature: Commerce Tables, Data Integration
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 0%

---

# Konsolidera dina tabeller

Om du har flera butiker eller flera marknader kan liknande databaser lagras separat. I [!DNL Adobe Commerce Intelligence]är det enkelt att sammanfoga liknande tabeller från olika databaser.

Du kan till exempel ha en `orders` tabell för `Market A`och liknande `orders` tabell för `Market B`. [!DNL Commerce Intelligence] kan konsolidera båda tabellerna och göra det möjligt för dig att titta på sammanställda orderdata från båda `Market A` och `B`, förutom att segmentera den efter en viss marknad.

Indatatabeller måste vara **liknande strukturerad**. Alla indatatabeller måste alltså innehålla de datakolumner som krävs i den konsoliderade tabellen.

I det här avsnittet beskrivs några av de vanligaste användningsområdena för konsoliderade tabeller och nästa steg som krävs för att skapa egna.

## Recommendations för när konsoliderade tabeller ska användas

Nedan beskrivs när det kan vara lämpligt att använda konsoliderade tabeller i systemet.

### Integrera data från flera webbplatser

Om du säljer produkter under olika varumärken och webbplatser är det troligt att tabellerna för varje varumärke eller webbplats är strukturerade på liknande sätt.

Du kan till exempel ha en `orders` tabell för webbplats `A` och en separat, men liknande, `orders` tabell för webbplats `B`. I den här situationen kan det vara användbart att konsolidera `orders` tabeller från webbplats `A` och `B`. På så sätt kan du se de samlade intäkterna och antalet beställningar från webbplatsen `A` och `B`, förutom att kunna segmentera mätvärden på dessa två webbplatser.

### Integrera äldre data

Många företag har omarbetat sina databaser vid ett eller annat tillfälle, och data från den gamla databasen konverteras inte alltid till det nya systemet. Du kan använda konsoliderade tabeller för att koppla nyckelkolumnerna från äldre tabeller till de som finns i det aktiva systemet. På så sätt kan ni utföra en enhetlig analys av era data genom hela historiken.

### Kombinera händelser för aktiv användaranalys

Föreställ dig en webbplats där användarna kan göra flera saker: ta en undersökning, spela ett spel, göra ett köp, hänvisa till en vän och så vidare. Vanligtvis lagras var och en av dessa händelser i en egen tabell. Detta gör det svårt att göra en analys av hur många distinkta användare som har vidtagit minst en åtgärd av något slag under en given tidsperiod.

Du kan använda konsoliderade tabeller för att skapa en enhetlig lista över alla användare och när någon av dessa händelser ägde rum. Du kan sedan köra frågor i den konsoliderade tabellen för att enkelt utföra en sådan analys.

Precis som med alla andra tabeller i Datan Warehouse kan du lägga till ytterligare kolumner för att driva olika typer av diagram och analyser.

## Skapa, visa eller uppdatera en konsoliderad tabell

Om du vill lägga till en konsoliderad tabell i Datan Warehouse kontaktar du [!DNL Commerce Intelligence] [support](../guide-overview.md#Submitting-a-Support-Ticket).

>[!NOTE]
>
>Eftersom konsoliderade tabeller inte kan visas i `Data Warehouse Manager`kan du bara visa och uppdatera de här tabellerna genom att [!DNL Commerce Intelligence] support.
