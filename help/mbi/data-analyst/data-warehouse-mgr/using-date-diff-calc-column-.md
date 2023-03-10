---
title: Använda kolumnen Beräknad datumdifferens
description: Lär dig syftet med och användningsområdena för den beräknade kolumnen Datumdifferens.
exl-id: 6ecab794-3466-4b3a-a929-3e56287522aa
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 2%

---

# Datumdifferens beräknad kolumn

I det här avsnittet beskrivs syftet med och användningsområdena för `Date Difference` beräknad kolumn tillgänglig i **[!DNL Manage Data > Data Warehouse]** sida. Nedan visas en förklaring av vad det gör, följt av ett exempel, och hur det går till att skapa det.

**Förklaring**

The `Date Difference` kolumntyp: söker efter tiden mellan två händelser som tillhör en enskild post, baserat på händelsens tidsstämplar. Det råvärde som beräknas i den här kolumnen är i sekunder, men konverteras automatiskt till minuter, timmar, dagar och så vidare, för visning i rapporter. När det används som ett filter/en grupp av vill du dock använda värdet i sekunder.

A `date difference` Beräknad kolumn kan användas för att skapa ett mått som beräknar den genomsnittliga tiden eller mediantiden mellan två händelser, till exempel den genomsnittliga tiden mellan kundregistrering och deras första order.

**Exempel**

| **`id`** | **`timestamp_1`** | **`timestamp_2`** | **`Seconds between timestamp_2 and timestamp_1`** |
|--- |--- |--- |--- |
| `A` | 2015-01-01 00:00:00 | 2015-01-01 12:30:00 | 45000 |
| `B` | 2015-01-01 08:00:00 | 2015-01-01 10:00:00 | 7200 |

{style="table-layout:auto"}


I exemplet ovan är `Date Difference` kolumnen är `Seconds between timestamp_2 and timestamp_1` kolumn. Beräkningen utförs `timestamp_2 minus timestamp_1`.

**Mekanik**

Följande steg beskriver hur du skapar en `Date Difference` kolumn.

1. Navigera till **[!DNL Manage Data > Data Warehouse]** sida.
1. Navigera till tabellen som du vill skapa den här kolumnen för.
1. Klicka **[!UICONTROL Create a Column]** och konfigurera din kolumn enligt följande:
   * Välj `Column Definition Type` > `Same Table`
   * Välj `Column Definition Equation` > `DATE_DIFF = (Ending DATETIME - Starting DATETIME)`
   * Välj `Ending DATETIME` kolumn > Välj det sista datetime-fältet, vilket vanligtvis är den händelse som inträffar senare
   * Välj `Starting DATETIME` kolumn** > Välj startdatum/tid-fält, vilket vanligtvis är händelsen som inträffar tidigare

1. Ange ett namn för kolumnen och klicka på **[!UICONTROL Save]**.
1. Kolumnen är tillgänglig att använda *omedelbart*.

Följande exempel är konfigurerat för att beräkna `Seconds between order date and customer's creation date`:

![](../../assets/date_diff.png)
