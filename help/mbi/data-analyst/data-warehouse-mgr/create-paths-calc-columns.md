---
title: Skapa eller ta bort banor för beräknade kolumner
description: Lär dig hur du definierar en sökväg som beskriver hur tabellen du skapar en kolumn i är relaterad till tabellen som du hämtar information från.
exl-id: 734a8046-8058-4f03-93a2-8d59b9be6d2d
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---

# Skapa eller ta bort banor för beräknade kolumner

## Uppdatera beräknade kolumner

När du [skapar beräknade kolumner](../data-warehouse-mgr/creating-calculated-columns.md) i Datan Warehouse uppmanas du att definiera en sökväg som beskriver hur tabellen du skapar en kolumn i är relaterad till tabellen som du hämtar information från. För att kunna skapa en bana måste du känna till två saker:

1. Hur tabellerna i databaserna relaterar till varandra
1. Primära och utländska nycklar som definierar relationen

Om du känner till den här informationen kan du enkelt skapa en sökväg enligt instruktionerna i det här avsnittet. Du kan fråga en teknisk expert i din organisation eller kontakta [Professional Services-teamet](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=sv-SE).

## Uppdateringar om tabellrelationer och nyckeltyper {#refresher}

### Tabellrelationer {#relationships}

Det här konceptet beskrivs i artikeln [Förstå och utvärdera tabellrelationer](../../data-analyst/data-warehouse-mgr/table-relationships.md), men en snabb sammanfattning skadar aldrig någon, eller hur?

Tabeller kan relateras till varandra på ett av tre sätt:

| **`Relationship Type`** | **`Example`** |
|-----|-----|
| **`one-to-one`** | Förhållandet mellan människor och förarens körkortsnummer. En person kan bara ha ett körkortsnummer och ett körkortsnummer tillhör endast en person. |
| **`one-to-many`** | Relationen mellan order och artiklar - en order kan innehålla många artiklar, men en artikel tillhör en enda order. I det här fallet är ordertabellen den ena sidan och artikeltabellen den andra sidan. |
| **`many-to-many`** | Relationen mellan produkter och kategorier: en produkt kan tillhöra många kategorier, och en kategori kan innehålla många produkter. |

{style="table-layout:auto"}

När en relation mellan två tabeller tolkas kan den användas för att bestämma vilken sökväg som ska skapas för att hämta information från en tabell till en annan. I nästa steg måste du känna till de primära och externa nycklarna som underlättar en tabellrelation.

### Primära och utländska nycklar {#keys}

En `Primary Key` är en oföränderlig kolumn eller en uppsättning kolumner som skapar unika värden i en tabell. När en kund t.ex. gör en beställning på en webbplats läggs en ny rad till i tabellen `orders` i kundvagnen, med en ny `order_id`. Med denna/detta `order_id` kan både kunden och företaget spåra förloppet för den specifika beställningen. Eftersom order-ID är unikt är det vanligtvis `Primary Key` i en `orders`-tabell.

En `Foreign Key` är en kolumn som skapats inuti en tabell som länkar till kolumnen `Primary Key` i en annan tabell. Sekundära nycklar skapar referenser mellan tabeller så att analytikerna enkelt kan söka efter och länka ihop poster. Säg att ni ville veta vilka order som tillhör var och en av era kunder. `customer id`-kolumnen (`Primary Key` i tabellen `customers`) och `order_id`-kolumnen (`Foreign Key` i tabellen `customers`, som refererar till `Primary Key` i tabellen `orders`) gör att vi kan länka och analysera den här informationen. När du skapar en sökväg ombeds du definiera både `Primary Key` och `Foreign Key`.

## Skapa en bana {#createpath}

När du skapar en kolumn i Datan Warehouse måste du definiera sökvägen som hämtar information från en tabell till en annan. Ibland fylls banor i i förväg eftersom det finns en sökväg mellan tabeller, men om detta inte inträffar måste du skapa en.

Använd relationen mellan **kunder** och **order** för att visa hur det går till. Nedbruten:

* Relationen är `one-to-many` - en kund kan ha många order, men en order kan bara ha en kund. Detta anger relationens riktning eller var den beräknade kolumnen ska skapas. I det här fallet betyder det att information från tabellen `orders` kan hämtas till tabellen `customers`.
* `primary key` som du vill använda är `customers.customerid` eller kolumnen `customer ID` i tabellen `customers`.
* `foreign key` som du vill använda är `orders.customerid` eller kolumnen `customer ID` i tabellen `orders`.

Nu kan du skapa banan.

1. Klicka på **[!UICONTROL Data > Data Warehouse]**.
1. Klicka på den tabell i vilken du vill skapa kolumnen i tabelllistan. I det här exemplet är det tabellen `customers`.
1. Tabellschemat visas. Klicka på **[!UICONTROL Create New Column]**.
1. Ge din kolumn ett namn, till exempel `Customer's orders`.
1. Markera definitionen för kolumnen. Ta en titt på [den beräknade kolumnguiden](../data-warehouse-mgr/creating-calculated-columns.md) om du vill ha ett praktiskt kalkylblad.
1. Klicka på alternativet **[!UICONTROL Create new path]** i listrutan [!UICONTROL Select table and column].

   ![Skapar sökvägar för beräknade kolumner modal](../../assets/Creating_Paths_modal.png)

1. Använd listrutorna för att välja primär- och sekundärnycklar för varje tabell.

   På `Many`-sidan väljer du `orders.customerid` - kom ihåg att kunderna kan ha många order.

   På `One`-sidan väljer du `customers.customerid` - en order kan bara ha en kund.

1. Klicka på **[!UICONTROL Save]** om du vill spara sökvägen och slutföra skapandet av kolumnen.

### Begränsningar för att skapa banor {#limits}

* **[!DNL Commerce Intelligence]kan inte gissa primära/externa nyckelrelationer**. Du vill inte infoga felaktiga data i ditt konto, så du måste skapa sökvägar manuellt.

* **För närvarande kan sökvägar bara anges mellan två olika tabeller**. Innebär logiken som du försöker återskapa fler än två tabeller? Det kan sedan vara bra att (1) koppla kolumnerna till en mellanliggande tabell först, sedan till den&quot;slutliga destinationstabellen&quot; eller (2) rådfråga [Professional Services-teamet](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=sv-SE) för att hitta det bästa sättet att uppnå dina mål.

* **En kolumn kan bara vara sekundärnyckelreferens för EN sökväg åt gången**. Om `order_items.order_id` till exempel pekar på `orders.id` kan `order_items.order_id` inte peka på något annat.

* **`Many-to-many`sökvägar kan skapas tekniskt, men ofta skapas felaktiga data eftersom ingen sida är en `one-to-many` sekundärnyckel** . Det bästa sättet att närma sig dessa banor beror alltid på den önskade analysen. Kontakta RJ:s analysteam för att hitta den bästa lösningen.

Om du inte kan skapa en beräknad kolumn på grund av en eller flera av begränsningarna ovan kontaktar du supporten med en beskrivning av kolumnen som du är

## Ta bort en beräknad kolumnsökväg {#delete}

Har du skapat en felaktig sökväg i Datan Warehouse? Eller kanske du ska göra lite vårrengöring och vill städa upp? Om du behöver ta bort en sökväg från ditt konto kan du [skicka en biljett till Adobe supportanalytiker](../../guide-overview.md#Submitting-a-Support-Ticket). **Ange namnet på sökvägen!**

## Radbrytning {#wrapup}

Nu kan du skapa banor för beräknade kolumner i Datan Warehouse. Om du fortfarande är osäker på en viss sökväg kan du alltid klicka på **[!UICONTROL Support]** i ditt [!DNL Commerce Intelligence]-konto för att få hjälp.

## Relaterad

* [Förstå och utvärdera tabellrelationer](../data-warehouse-mgr/table-relationships.md)
* [Skapa banor för beräknade kolumner](../data-warehouse-mgr/create-paths-calc-columns.md)
* [Beräknade kolumntyper](../data-warehouse-mgr/calc-column-types.md) försöker skapa.
