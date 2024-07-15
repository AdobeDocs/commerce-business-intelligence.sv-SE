---
title: Avancerade beräknade kolumntyper
description: Lär dig grunderna för de flesta användningsfall för kolumner - men du kanske vill ha en beräknad kolumn som är lite mer komplex än vad Data Warehouse Manager kan skapa.
exl-id: 9871fa19-95b3-46e4-ae2d-bd7c524d12db
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 2%

---

# Avancerade beräknade kolumntyper

Många analyser som du kanske vill skapa innehåller en **ny kolumn** som du vill `group by` eller `filter by`. Självstudiekursen [Skapa beräknade kolumner](../data-warehouse-mgr/creating-calculated-columns.md) beskriver grunderna för de flesta användningsfall, men du kanske vill ha en beräknad kolumn som är lite mer komplex än vad Data Warehouse Manager kan skapa.
{: #top}

Den här typen av Data Warehouse kan skapas av Adobe-teamet hos analytiker. Ange följande information om du vill definiera en ny beräknad kolumn:

1. **`definition`** i den här kolumnen (inklusive indata, formler eller formatering)
1. Den **`table`** som du vill skapa kolumnen på
1. Alla **`example data points`** som beskriver vad kolumnen ska innehålla

Här är några vanliga exempel på avancerade beräknade kolumner som användarna ofta tycker är användbara:

* [Ordna (eller rangordna) händelse sekventiellt](#compareevents)
* [Hitta tiden mellan två händelser](#twoevents)
* [Jämför sekventiella händelsevärden](#sequence)
* [Konvertera valuta](#currency)
* [Konvertera tidszoner](#timezone)
* [Någonting annat](#else)

## Jag försöker beställa händelser sekventiellt {#compareevents}

Detta kallas en beräknad kolumn för **händelsenummer**. Det innebär att du försöker hitta den sekvens i vilken händelser inträffade för en viss händelseägare, som en kund eller användare.

Här är ett exempel:

| **`event\_id`** | **`owner\_id`** | **`timestamp`** | **`Owner's event number`** |
|-----|-----|-----|-----|
| 1 | `A` | 2015-01-01 00:00:00 | 1 |
| 2 | `B` | 2015-01-01 00:30:00 | 1 |
| 3 | `A` | 2015-01-01 02:00:00 | 2 |
| 4 | `A` | 2015-01-02 13:00:00 | 3 |
| 5 | `B` | 2015-01-03 13:00:00 | 2 |

{style="table-layout:auto"}

En kolumn för beräkning av händelsenummer kan användas för att observera skillnader i beteende mellan förstagångshändelser, upprepningshändelser och nth-händelser i dina data.

Vill du se hur kundens kolumn med ordernummer fungerar? Klicka på bilden för att se den användas som en grupp efter dimension i en rapport.

![Använder en kolumn med ett händelsenummer som beräknas för att gruppera efter kundens ordernummer.](../../assets/EventNumber.gif)<!--{: style="max-width: 500px;"}-->

Om du vill skapa den här typen av beräknad kolumn måste du känna till:

* Tabellen som du vill skapa den här kolumnen för
* Det fält som identifierar händelsens ägare (`owner\_id` i det här exemplet)
* Det fält som du vill beställa händelserna med (`timestamp` i det här exemplet)

[Tillbaka till början](#top)

## Jag försöker hitta tiden mellan två händelser. {#twoevents}

Detta kallas en `date difference` beräknad kolumn. Det innebär att du försöker hitta tiden mellan två händelser som tillhör en enda post, baserat på händelsens tidsstämplar.

Här är ett exempel:

| `id` | `timestamp\_1` | `timestamp\_2` | `Seconds between timestamp\_2 and timestamp\_1` |
|-----|-----|-----|-----|
| `A` | 2015-01-01 00:00:00 | 2015-01-01 12:30:00 | 45000 |
| `B` | 2015-01-01 08:00:00 | 2015-01-01 10:00:00 | 7200 |

{style="table-layout:auto"}

En beräknad datumdifferenskolumn kan användas för att skapa ett mått som beräknar medeltiden eller mediantiden mellan två händelser. Klicka på bilden nedan för att se hur måttet `Average time to first order` används i en rapport.

![Använder en beräknad datumdifferenskolumn för att beräkna genomsnittlig tid till första ordern.](../../assets/DateDifference.gif)<!--{: style="max-width: 500px;"}-->

Om du vill skapa den här typen av beräknad kolumn måste du känna till:

* Tabellen som du vill skapa den här kolumnen för
* De två tidsstämplar mellan vilka du vill veta skillnaden

[Tillbaka till början](#top)

## Jag försöker jämföra värden för sekventiella händelser. {#sequence}

Detta kallas en **sekventiell händelsejämförelse**. Det innebär att du försöker hitta delta mellan ett värde (valuta, nummer, tidsstämpel) och motsvarande värde för ägarens föregående händelse.

Här är ett exempel:

| **`event\_id`** | **`owner\_id`** | **`timestamp`** | **`Seconds since owner's previous event`** |
|-----|-----|-----|-----|
| 1 | `A` | 2015-01-01 00:00:00 | NULL |
| 2 | `B` | 2015-01-01 00:30:00 | NULL |
| 3 | `A` | 2015-01-01 02:00:00 | 7720 |
| 4 | `A` | 2015-01-02 13:00:00 | 126000 |
| 5 | `B` | 2015-01-03 13:00:00 | 217800 |

{style="table-layout:auto"}

En sekventiell händelsejämförelse kan användas för att hitta den genomsnittliga tiden eller mediantiden mellan varje sekventiell händelse. Klicka på bilden nedan för att se hur **medel- och mediantiden mellan order**-mätvärdena fungerar.

=![Använder en beräknad kolumn för sekventiell händelsejämförelse för att beräkna genomsnittlig och mediantid mellan order.](../../assets/SeqEventComp.gif)<!--{: style="max-width: 500px;"}-->

Om du vill skapa den här typen av beräknad kolumn måste du känna till:

* Tabellen som du vill skapa den här kolumnen för
* Det fält som identifierar ägaren till händelserna (`owner\_id` i exemplet)
* Det värdefält som du vill se skillnaden mellan för varje sekventiell händelse (`timestamp` i det här exemplet)

[Tillbaka till början](#top)

## Jag försöker konvertera valuta. {#currency}

En beräknad kolumn för **valutakonvertering** konverterar transaktionsbelopp från en registrerad valuta till en rapporteringsvaluta, baserat på valutakursen vid händelseläget.

Här är ett exempel:

| **`id`** | **`timestamp`** | **`transaction\_value\_EUR`** | **`transaction\_value\_USD`** |
|-----|-----|-----|-----|
| `1` | 2015-01-01 00:00:00 | 30 | 33,57 |
| `2` | 2015-01-02 00:00:00 | 50 | 55,93 |

{style="table-layout:auto"}

Om du vill skapa den här typen av beräknad kolumn måste du känna till:

* Tabellen som du vill skapa den här kolumnen för
* Den kolumn med transaktionsbelopp som du vill konvertera
* Kolumnen som anger valutan som data spelades in i (vanligtvis en ISO-kod)
* Den föredragna rapporteringsvalutan

[Tillbaka till början](#top)

## Jag försöker konvertera tidszoner. {#timezone}

En beräknad kolumn för **tidszonskonvertering** konverterar tidsstämplarna för en viss datakälla från den inspelade tidszonen till en rapporttidszon.

Här är ett exempel:

| **`id`** | **`timestamp\_UTC`** | **`timestamp\_ET`** |
|-----|-----|-----|
| `1` | 2015-01-01 00:00:00 | 2014-12-31 19:00:00 |
| `2` | 2015-01-01 12:00:00 | 2015-01-01 07:00:00 |

{style="table-layout:auto"}

Om du vill skapa den här typen av beräknad kolumn måste du känna till:

* Tabellen som du vill skapa den här kolumnen för
* Den tidsstämpelkolumn som du vill konvertera
* Tidszonen där data spelades in
* Rekommenderad tidszon för rapportering

[Tillbaka till början](#top)

## Jag försöker göra något som inte finns med här. {#else}

Oroa dig inte. Bara för att det inte finns med här betyder det inte att det inte är möjligt. Adobe-teamet hos Data Warehouse Analysts kan hjälpa till.

Om du vill definiera en ny beräknad kolumn, [skickar du en supportanmälan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) med information om exakt vad du vill skapa.

## Relaterad dokumentation

* [Skapa beräknade kolumner](../data-warehouse-mgr/creating-calculated-columns.md)
* [Beräknade kolumntyper](../data-warehouse-mgr/calc-column-types.md)
* [Bygger [!DNL Google ECommerce] dimensioner med order- och kunddata](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
