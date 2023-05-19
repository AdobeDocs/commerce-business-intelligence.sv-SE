---
title: Skapa eller ta bort banor för beräknade kolumner
description: Lär dig hur du definierar en sökväg som beskriver hur tabellen du skapar en kolumn i är relaterad till tabellen som du hämtar information från.
exl-id: 734a8046-8058-4f03-93a2-8d59b9be6d2d
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '1019'
ht-degree: 0%

---

# Skapa eller ta bort banor för beräknade kolumner

## Uppdatera beräknade kolumner

När [skapa beräknade kolumner](../data-warehouse-mgr/creating-calculated-columns.md) i Data warehouse uppmanas du att definiera en sökväg som beskriver hur tabellen du skapar en kolumn i är relaterad till tabellen som du hämtar information från. För att kunna skapa en bana måste du känna till två saker:

1. Hur tabellerna i databaserna relaterar till varandra
1. Primära och utländska nycklar som definierar relationen

Om du känner till den här informationen kan du enkelt skapa en sökväg enligt instruktionerna i det här avsnittet. Du kan fråga en teknisk expert i din organisation eller kontakta [Professional Services Team](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

## Uppdaterar tabellrelationer och nyckeltyper {#refresher}

### Tabellrelationer {#relationships}

Detta begrepp beskrivs i [Artikel om att förstå och utvärdera tabellrelationer](../../data-analyst/data-warehouse-mgr/table-relationships.md)Men en snabb sammanfattning skadar ingen, eller hur?

Tabeller kan relateras till varandra på ett av tre sätt:

| **`Relationship Type`** | **`Example`** |
|-----|-----|
| **`one-to-one`** | Förhållandet mellan människor och körkortsnummer. En person kan bara ha ett körkortsnummer och ett körkortsnummer tillhör endast en person. |
| **`one-to-many`** | Relationen mellan order och artiklar - en order kan innehålla många artiklar, men en artikel tillhör en enda order. I det här fallet är ordertabellen den ena sidan och artikeltabellen den andra sidan. |
| **`many-to-many`** | Förhållandet mellan produkter och kategorier: en produkt kan tillhöra många kategorier och en kategori kan innehålla många produkter. |

{style="table-layout:auto"}

När en relation mellan två tabeller tolkas kan den användas för att bestämma vilken sökväg som ska skapas för att hämta information från en tabell till en annan. I nästa steg måste du känna till de primära och externa nycklarna som underlättar en tabellrelation.

### Primära och utländska nycklar {#keys}

A `Primary Key` är en oföränderlig kolumn eller en uppsättning kolumner som skapar unika värden i en tabell. När en kund t.ex. gör en beställning på en webbplats läggs en ny rad till i `orders` i kundvagnen med en ny `order_id`. Detta `order_id` låter både kunden och företaget följa utvecklingen av den specifika beställningen. Eftersom order-ID är unikt är det vanligtvis `Primary Key` av `orders` tabell.

A `Foreign Key` är en kolumn som skapats inuti en tabell som länkar till `Primary Key` kolumn i en annan tabell. Sekundära nycklar skapar referenser mellan tabeller så att analytikerna enkelt kan söka efter och länka ihop poster. Säg att ni ville veta vilka order som tillhör var och en av era kunder. The `customer id` kolumn (`Primary Key` i `customers` tabellen) och `order_id` kolumn (`Foreign Key` i `customers` tabell, referera till `Primary Key` i `orders` table) kan vi länka och analysera den här informationen. När du skapar en bana ombeds du definiera båda `Primary Key` och `Foreign Key`.

## Skapa en bana {#createpath}

När du skapar en kolumn i Data warehouse måste du definiera sökvägen som hämtar information från en tabell till en annan. Ibland fylls banor i i förväg eftersom det finns en sökväg mellan tabeller, men om detta inte inträffar måste du skapa en.

Använd relationen mellan **kunder** och **order** för att visa hur man gör. Nedbruten:

* Relationen är `one-to-many` - en kund kan ha många order, men en order kan bara ha en kund. Detta anger relationens riktning eller var den beräknade kolumnen ska skapas. I det här fallet betyder det information från `orders` kan läggas in i `customers` tabell.
* The `primary key` du vill använda är `customers.customerid`eller `customer ID` kolumn i `customers` tabell.
* The `foreign key` du vill använda är `orders.customerid`eller `customer ID` kolumn i `orders` tabell.

Nu kan du skapa banan.

1. Klicka **[!UICONTROL Data > Data Warehouse]**.
1. Klicka på den tabell i vilken du vill skapa kolumnen i tabelllistan. I det här exemplet är det `customers` tabell.
1. Tabellschemat visas. Klicka **[!UICONTROL Create New Column]**.
1. Ge kolumnen ett namn, till exempel `Customer's orders`.
1. Markera kolumndefinitionen. Kolla in [Beräknad kolumnstödlinje](../data-warehouse-mgr/creating-calculated-columns.md) för ett praktiskt kalkylblad.
1. I [!UICONTROL Select table and column] listrutan, klicka på **[!UICONTROL Create new path]** alternativ.

   ![Skapa banor för beräknade kolumner modal](../../assets/Creating_Paths_modal.png)

1. Använd listrutorna för att välja primär- och sekundärnycklar för varje tabell.

   På `Many` sida, du väljer `orders.customerid` - Kom ihåg att kunderna kan ha många order.

   På `One` sida, du väljer `customers.customerid` - en order kan bara ha en kund.

1. Klicka **[!UICONTROL Save]** för att spara banan och slutföra kolumnskapandet.

### Begränsningar för att skapa banor {#limits}

* **[!DNL Commerce Intelligence]kan inte gissa relationer för primär-/sekundärnyckel**. Du vill inte infoga felaktiga data i ditt konto, så du måste skapa sökvägar manuellt.

* **För närvarande kan sökvägar bara anges mellan två olika tabeller**. Innebär logiken du försöker återskapa fler än två tabeller? Det kan sedan vara bra att (1) koppla kolumnerna till en mellanliggande tabell först, sedan till tabellen&quot;Slutdestination&quot; eller (2) läsa med [Professional Services Team](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) för att hitta det bästa sättet att se på era mål.

* **En kolumn kan bara vara sekundärnyckelreferens för en bana åt gången**. Om `order_items.order_id` pekar på `orders.id`sedan `order_items.order_id` kan inte peka på något annat.

* **`Many-to-many`banor kan tekniskt sett skapas, men ofta skapas felaktiga data eftersom ingen sida är sann `one-to-many` sekundärnyckel**. Det bästa sättet att närma sig dessa banor beror alltid på den önskade analysen. Kontakta RJ:s analysteam för att hitta den bästa lösningen.

Om du inte kan skapa en beräknad kolumn på grund av en eller flera av begränsningarna ovan kontaktar du supporten med en beskrivning av kolumnen som du är

## Ta bort en beräknad kolumnsökväg {#delete}

Har du skapat en felaktig sökväg i Data warehouse? Eller kanske du ska göra lite vårrengöring och vill städa upp? Om du behöver ta bort en sökväg från ditt konto kan du [skicka över en biljett till Adobe supportanalytiker](../../guide-overview.md#Submitting-a-Support-Ticket). **Var noga med att ta med namnet på sökvägen!**

## Radbrytning {#wrapup}

Nu när du är bekväm med att skapa banor för beräknade kolumner i Data warehouse. Om du fortfarande är osäker på en viss bana kan du alltid klicka **[!UICONTROL Support]** i [!DNL Commerce Intelligence] för att få hjälp.

## Relaterad

* [Förstå och utvärdera tabellrelationer](../data-warehouse-mgr/table-relationships.md)
* [Skapa banor för beräknade kolumner](../data-warehouse-mgr/create-paths-calc-columns.md)
* [Beräknade kolumntyper](../data-warehouse-mgr/calc-column-types.md) försöker skapa.
