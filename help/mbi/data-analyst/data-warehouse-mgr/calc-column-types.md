---
title: Beräknade kolumntyper
description: Lär dig hur du skapar kolumner för att förbättra och optimera data för analys.
exl-id: 1af79b9e-77ff-4fc6-917a-4e6743b95035
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 0%

---

# Beräknade kolumntyper

* [Samma tabellberäkningar](#sametable)
* [En till många beräkningar](#onetomany)
* [Många till en beräkning](#manytoone)
* [Referenskarta](#map)
* [Avancerade beräknade kolumner](#advanced)

I [Data Warehouse Manager](../data-warehouse-mgr/tour-dwm.md) kan du skapa kolumner för att utöka och optimera data för analys. [Du kommer åt den här funktionen](../data-warehouse-mgr/creating-calculated-columns.md) genom att markera en tabell i Data Warehouse Manager och klicka på **[!UICONTROL Create New Column]**.

I det här avsnittet beskrivs de typer av kolumner som du kan skapa med Data Warehouse Manager. Den innehåller även beskrivningen, en visuell genomgång av den kolumnen och en [referenskarta](#map) av alla indata som krävs för att skapa en kolumn. Det finns tre sätt att skapa beräknade kolumner:

1. [Samma tabellberäknade kolumner](#sametable)
1. [En-till-många beräknade kolumner](#onetomany)
1. [Många-till-ett-beräknade kolumner](#manytoone)

## Samma tabellberäknade kolumner {#sametable}

Dessa kolumner skapas med indatakolumner från samma tabell.

### Ålder {#age}

En kolumn för beräkning av ålder returnerar antalet sekunder mellan den aktuella tiden och en viss indatatid.

I exemplet nedan skapas `Seconds since customer's most recent order` i tabellen `customers`. Detta kan användas för att skapa användarlistor för kunder som inte har gjort inköp (kallas ibland för att vinna) inom `X days`.

![](../../assets/age.gif)

### Valutakonverterare

En kolumn för valutakonvertering som beräknas konverterar den ursprungliga valutan i en kolumn till önskad ny valuta.

I exemplet nedan skapas `base\_grand\_total In AED` och `base\_grand\_total` konverteras från sin ursprungliga valuta till AED i tabellen `sales\_flat\_order`. Den här kolumnen fungerar bra för butiker med flera valutor som vill rapportera i sin lokala valuta.

För Commerce-klienter lagrar fältet `base\_currency\_code` vanligtvis inbyggda valutor. Fältet `Spot Time` ska matcha datumet som används i måtten.

![](../../assets/currency_converter.png)

## En-till-många beräknade kolumner {#onetomany}

`One-to-Many` kolumner [använder en sökväg mellan två tabeller](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md). Den här sökvägen innebär alltid en tabell, där ett attribut finns, och en många tabeller, där attributet flyttas ned till. Sökvägen kan beskrivas som en `foreign key--primary key`-relation.

### Kopplad kolumn {#joined}

En sammanfogad kolumn omlokaliserar ett attribut i den enda tabellen *till* i den många tabellen. Det klassiska exemplet på en/flera är kunder (en) och beställningar (många).

I exemplet nedan förenas dimensionen `Customer's group\_id` nedåt i tabellen `orders`.

![](../../assets/joined_column.gif)

## Många-till-ett-beräknade kolumner {#manytoone}

Dessa kolumner använder samma sökvägar som en-till-många-kolumner gör, men de pekar data i motsatt riktning. Kolumnen skapas på den ena sidan av banan, i motsats till många. På grund av den här relationen måste värdet i kolumnen vara en aggregering, det vill säga en matematisk åtgärd som utförs på datapunkterna på många sidor. Det finns många användningsfall för detta, och några av dem visas nedan.

### Antal {#count}

Den här typen av beräknad kolumn returnerar antalet värden i många tabeller *till* i en tabell.

I exemplet nedan skapas dimensionen `Customer's lifetime number of canceled orders` i tabellen `customers` (med ett filter för `orders.status`).

![](../../assets/many_to_one.gif){: width="699" height="351"}

### Summa {#sum}

En summerad beräknad kolumn är summan av värdena i tabellen `many` i tabellen.

Detta kan användas för att skapa kundnivådimensioner som `Customer's lifetime revenue`.

### Min eller Max {#minmax}

En minsta eller högsta beräknad kolumn returnerar den minsta eller största posten som finns på många sidor.

Detta kan användas för att skapa kundnivådimensioner som `Customer's first order date`.

### Finns {#exists}

En beräknad kolumn är ett binärt test som fastställer förekomsten av en post på många sidor. Den nya kolumnen returnerar med andra ord `1` om sökvägen ansluter minst en rad i varje tabell och `0` om ingen anslutning kan göras.

Den här typen av dimension kan till exempel avgöra om en kund någonsin köpt en viss produkt. Med hjälp av en koppling mellan en `customers`-tabell och en `orders`-tabell, ett filter för en viss produkt, kan en dimension `Customer has purchased Product X?` skapas.

## Referenskarta {#map}

Om du har problem med att komma ihåg vad alla indata är när du skapar en beräknad kolumn, bör du behålla referenskartan när du skapar:

![](../../assets/merged_reference_map.png)

## Avancerade beräknade kolumner {#advanced}

I din förfrågan om att analysera och besvara frågor om ditt företag kan du stöta på en situation där du inte kan skapa exakt den kolumn du vill ha.

För att få en snabb vändning rekommenderar Adobe att du tittar i guiden [Avancerade beräknade kolumntyper](../../data-analyst/data-warehouse-mgr/adv-calc-columns.md) för att se vilka typer av kolumner som Adobe supportteam kan skapa. Det avsnittet innehåller även information som du behöver för att skapa kolumnen. Ta med den tillsammans med din begäran.

## Relaterad dokumentation

* [Skapa beräknade kolumner](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md)
* [Skapa/ta bort banor för beräknade kolumner](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md)
* [Förstå och utvärdera tabellrelationer](../../data-analyst/data-warehouse-mgr/table-relationships.md)
