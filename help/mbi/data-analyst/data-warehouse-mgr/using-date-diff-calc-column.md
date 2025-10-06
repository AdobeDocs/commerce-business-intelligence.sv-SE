---
title: Använda kolumnen Beräknad datumdifferens
description: Lär dig syftet med och användningsområdena för den beräknade kolumnen Datumdifferens.
exl-id: 6ecab794-3466-4b3a-a929-3e56287522aa
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# Datumdifferens beräknad kolumn

I det här avsnittet beskrivs syftet med och användningsområdena för den beräknade kolumnen `Date Difference` som är tillgänglig på sidan **[!DNL Manage Data > Data Warehouse]**. Nedan visas en förklaring av vad det gör, följt av ett exempel, och hur det fungerar.

**Förklaring**

Kolumntypen `Date Difference` beräknar tiden mellan två händelser som tillhör en enskild post, baserat på händelsens tidsstämplar. Det råvärde som beräknas i den här kolumnen är i sekunder, men konverteras automatiskt till minuter, timmar, dagar och så vidare, för visning i rapporter. När det används som ett filter/en grupp av vill du dock använda värdet i sekunder.

En `date difference` beräknad kolumn kan användas för att skapa ett mått som beräknar den genomsnittliga tiden eller mediantiden mellan två händelser, till exempel den genomsnittliga tiden mellan kundregistrering och deras första order.

**Exempel**

| **`id`** | **`timestamp_1`** | **`timestamp_2`** | **`Seconds between timestamp_2 and timestamp_1`** |
|--- |--- |--- |--- |
| `A` | 2015-01-01 00:00:00 | 2015-01-01 12:30:00 | 45000 |
| `B` | 2015-01-01 08:00:00 | 2015-01-01 10:00:00 | 7200 |

{style="table-layout:auto"}


I ovanstående exempel är kolumnen `Date Difference` kolumnen `Seconds between timestamp_2 and timestamp_1`. Beräkningen `timestamp_2 minus timestamp_1` utförs.

**Mekanik**

I följande steg beskrivs hur du skapar en `Date Difference`-kolumn.

1. Navigera till sidan **[!DNL Manage Data > Data Warehouse]**.
1. Navigera till tabellen som du vill skapa den här kolumnen för.
1. Klicka på **[!UICONTROL Create a Column]** och konfigurera kolumnen så här:
   * Välj `Column Definition Type` > `Same Table`
   * Välj `Column Definition Equation` > `DATE_DIFF = (Ending DATETIME - Starting DATETIME)`
   * Välj kolumnen `Ending DATETIME` > Välj det sista datetime-fältet, vilket vanligtvis är den händelse som inträffar senare
   * Välj `Starting DATETIME` kolumn** > Välj startdatum/tid-fält, vilket vanligtvis är den händelse som inträffar tidigare

1. Ange ett namn för kolumnen och klicka på **[!UICONTROL Save]**.
1. Kolumnen kan användas *omedelbart*.

Följande exempel har konfigurerats för att beräkna `Seconds between order date and customer's creation date`:

![Beräkningskonfiguration för datumdifferens som visar kolumnval för datum/tid](../../assets/date_diff.png)
