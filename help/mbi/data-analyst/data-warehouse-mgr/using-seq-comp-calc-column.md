---
title: Beräknad kolumn för sekventiell jämförelse
description: Lär dig syftet med och användningsområdena för kolumnen Beräknad sekventiell jämförelse.
exl-id: 625062b4-f05d-42aa-94c3-729b39c7d728
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: 2433a614e9858684842804a0ae29fb67f0d41ead
workflow-type: tm+mt
source-wordcount: '413'
ht-degree: 0%

---

# Beräknad kolumn för sekventiell jämförelse

I det här avsnittet beskrivs syftet med och användningsområdena för `Sequential Comparison` beräknad kolumn tillgänglig i **[!DNL Manage Data > Data Warehouse]** sida. Nedan visas en förklaring av vad det gör, följt av ett exempel och hur det fungerar.

**Förklaring**

The `Sequential Comparison` kolumntyp: söker efter skillnaden mellan efterföljande händelser. Den vanligaste typen av `Sequential Comparison` kolumnen är `Seconds since previous order` kolumn. Det finns tre indata som behövs för den här kolumnen:

1. `Event Owner`: Den här inmatningen avgör för vilken enhet rader grupperas. I `Seconds since previous order` -kolumnen är händelseägaren kunden eftersom du vill hitta antalet sekunder sedan den föregående ordern från samma kund.
1. `Event Date`: Den här inmatningen framtvingar händelsesekvensen. I de fall `Seconds since previous order`, ska kolumnen som innehåller tidsstämpeln för ordern vara `Event Date`. Den här inmatningen är alltid en tidsstämpel.
1. `Value to Compare`: Detta är det faktiska värde som ska jämföras. Den subtraherar föregående rads värde från den aktuella radens värde. Därför anropas en kolumn som visar tidsskillnaden mellan på varandra följande order från en kund `Seconds since previous order`. Den här inmatningen behöver inte vara en tidsstämpel. Ett exempel på icke-tidsstämpel är att hitta skillnaden i ordervärde mellan på varandra följande order från en kund.

**Exempel**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Seconds since owner's previous event`** |
|--- |--- |--- |--- |
| **`1`** | A | 2015-01-01 00:00:00 | NULL |
| **`2`** | B | 2015-01-01 00:30:00 | NULL |
| **`3`** | A | 2015-01-01 02:00:00 | 7200 |
| **`4`** | A | 2015-01-02 13:00:00 | 126000 |
| **`5`** | B | 2015-01-03 13:00:00 | 217800 |

I exemplet ovan `Seconds since owner's previous event` är `Sequential Comparison` beräknad kolumn. För `owner_id = A`identifierar den först en sekvens som baseras på `timestamp` och sedan subtraherar föregående händelses `timestamp` från den aktuella händelsens tidsstämpel. I den tredje raden i tabellen - den andra raden i `owner_id A` - värdet av `Seconds since owner's previous event` är antalet sekunder mellan 2015-01-01 02:00 och 2015-01-01 00:00:00. Skillnaden är lika med två timmar = 7 200 sekunder.

För den här beräknade kolumntypen har raden som motsvarar ägarens första händelse en `NULL` värde.

**Mekanik**

Skapa en **Händelsenummer** kolumn:

1. Navigera till **[!DNL Manage Data > Data Warehouse]** sida.

1. Navigera till tabellen som du vill skapa den här kolumnen för.

1. Klicka **[!UICONTROL Create New Column]** längst upp till höger.

1. Välj `Same Table` som `Definition Type` (om kolumnerna som du vill jämföra inte finns i samma tabell kan du behöva flytta dem).

1. Välj `SEQUENTIAL_COMPARISON` som `Column Definition Equation`.

1. Välj indata enligt ovan:
   - `Event Owner`
   - `Event Date`
   - `Value to Compare`

1. Du kan också lägga till filter för att utesluta rader från övervägandet. Undantagna rader har en `NULL` värdet för den här kolumnen.

1. Ange ett namn för kolumnen högst upp på sidan och klicka på **[!UICONTROL Save]**.

1. Kolumnen är tillgänglig att använda *omedelbart*.

![SEK](../../assets/SEC_new.png)
