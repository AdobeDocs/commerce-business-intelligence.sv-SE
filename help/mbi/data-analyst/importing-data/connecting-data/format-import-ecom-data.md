---
title: Formatera och importera e-handelsdata
description: Lär dig de idealiska dataformaten som ska användas för att överföra e-handelsdata.
exl-id: 7b910f78-9a5a-4d5d-a8b7-1b0b76304afe
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '459'
ht-degree: 0%

---

# Formatera och importera data

Om du använder en integrering som för närvarande inte stöds av [!DNL Adobe Commerce Intelligence] kan du fortfarande använda [filöverföringsfunktionen](using-file-uploader.md) för att hämta data till Datan Warehouse. I det här avsnittet beskrivs de idealiska dataformat som ska användas för att överföra e-handelsdata.

## `Orders`-tabell

Tabellen `orders` ska innehålla en rad för varje transaktion som företaget har utfört. Potentiella kolumner är:

| Kolumnnamn | Beskrivning |
|----|----|
| `Order ID` | Orderns ID ska vara unikt för varje rad i tabellen. Detta är vanligtvis tabellens primärnyckel. |
| `Customer` | Kunden som gjorde beställningen. |
| `Order total` | Summan av ordern. Detta kan vara en beräkningsbaserad kolumn där värden i andra kolumner - t.ex. delsumma och frakt - utgör summan för den här kolumnen. |
| `Currency` | Valutan som ordern har betalats i. Inkludera om relevant. |
| ` Order status` | Orderns status, till exempel `In Progress`, `Refunded` eller `Complete`. Värdet för den här kolumnen ändras (om den inte är fullständig). Nya och uppdaterade data kan importeras med funktionen [Lägg till data](../../../data-analyst/importing-data/connecting-data/using-file-uploader.md) på sidan `File Uploads`. |
| `Acquisition/marketing channel` | Förvärvs- eller marknadsföringskanalen som kunden som beställde refererades till. |
| `Order datetime` | Datum och tid då ordern skapades. |
| `Order updated at` | Datum och tid då den senaste ändringen av orderposten gjordes. |

{style="table-layout:auto"}

## `Order detail/items`-tabell {#itemstable}

Tabellen `order_detail / items` ska innehålla en rad för varje distinkt objekt i varje ordning. Potentiella kolumner är:

| Kolumnnamn | Beskrivning |
|----|----|
| `Order item ID` | Orderartikel-ID ska vara unikt för varje rad i tabellen. Detta är vanligtvis `primary key` för tabellen. |
| `Order ID` | Orderns ID. |
| `Product ID` | Produktens ID. |
| `Product name` | Produktens namn. |
| `Product's unit price` | Priset för en enda enhet av produkten. |
| `Quantity` | Kvantiteten av produkten i ordern. |

## `Customers`-tabell {#customerstable}

Tabellen `customers` ska innehålla en rad för varje kundkonto. Potentiella kolumner är:

| Kolumnnamn | Beskrivning |
|----|----|
| `Customer ID` | Kund-ID ska vara unikt för varje rad i tabellen. Detta är vanligtvis tabellens primärnyckel. |
| `Customer created at` | Datum och tid då kundens konto skapades. |
| `Customer modified at` | Datum och tid då kundens konto senast ändrades. |
| `Acquisition/marketing channel source` | Förvärvs- eller marknadsföringskanalen som kunden refererades till. |
| `Demographic info` | Demografisk information som åldersintervall och kön kan användas för att segmentera dina rapporter. |
| `Acquisition/marketing channel` | Förvärvs- eller marknadsföringskanalen som kunden som beställde refererades till. |

## `Subscription payments`-tabell

Tabellen `subscriptions` ska innehålla en rad för varje prenumerationsbetalning. Potentiella kolumner är:

| Kolumnnamn | Beskrivning |
|----|----|
| `Subscription ID` | Prenumerations-ID ska vara unikt för varje rad i tabellen. Detta är vanligtvis tabellens primärnyckel. |
| `Customer ID` | ID för den kund som gjorde betalningen. |
| `Payment amount` | Beloppet för prenumerationsbetalningen. |
| `Start date` | Startdatum/tid för perioden som betalningen täcker. |
| `End date` | Slutdatum/tid för perioden som betalningen täcker. |
