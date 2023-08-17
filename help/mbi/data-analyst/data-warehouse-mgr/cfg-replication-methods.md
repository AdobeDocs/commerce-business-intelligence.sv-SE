---
title: Konfigurerar replikeringsmetoder
description: Lär dig hur tabeller är ordnade och hur tabelldata fungerar gör att du kan välja den bästa replikeringsmetoden för tabellerna.
exl-id: 83895c48-a6ec-4b01-9890-164e0b21dcbc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Data Import/Export
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1414'
ht-degree: 0%

---

# Konfigurerar replikeringsmetoder

`Replication` metoder och [omkontroller](../data-warehouse-mgr/cfg-data-rechecks.md) används för att identifiera nya eller uppdaterade data i dina databastabeller. Att ställa in dem på rätt sätt är avgörande för att både datakvaliteten och optimerade uppdateringstider ska kunna garanteras. Det här avsnittet fokuserar på replikeringsmetoder.

När nya tabeller synkroniseras i [Data Warehouse Manager](../data-warehouse-mgr/tour-dwm.md)väljs automatiskt en replikeringsmetod för tabellen. Om du förstår de olika replikeringsmetoderna, hur tabeller är ordnade och hur tabelldata fungerar kan du välja den bästa replikeringsmetoden för tabellerna.

## Vilka är replikeringsmetoderna?

`Replication` metoder kan delas in i tre grupper - `Incremental`, `Full Table`och `Paused`.

[**[!UICONTROL Incremental Replication]**](#incremental) innebär att [!DNL Commerce Intelligence] replikerar endast nya eller uppdaterade data vid varje replikeringsförsök. Eftersom dessa metoder minskar fördröjningen avsevärt rekommenderar Adobe att du använder den där det är möjligt.

[**[!UICONTROL Full Table Replication]**](#fulltable) innebär att [!DNL Commerce Intelligence] replikerar hela tabellinnehållet vid varje replikeringsförsök. På grund av den potentiellt stora mängd data som kan replikeras kan dessa metoder öka fördröjningen och uppdateringstiden. Om en tabell innehåller tidstämpling- eller datetime-kolumner rekommenderar Adobe att du använder en Stegvis metod i stället.

**[!UICONTROL Paused]** anger att replikeringen för tabellen har stoppats eller pausats. [!DNL Commerce Intelligence] söker inte efter nya eller uppdaterade data under en uppdateringscykel, vilket innebär att inga data replikeras från en tabell som har detta som replikeringsmetod.

## Stegvisa replikeringsmetoder {#incremental}

### Ändrad vid (mest idealisk)

The `Modified At` replikeringsmetoden använder en datetime-kolumn, som fylls i när en rad skapas och sedan uppdateras när data ändras, för att hitta data som ska replikeras. Den här metoden är utformad för att fungera med tabeller som uppfyller följande kriterier:

* innehåller en `datetime` kolumn som fylls i från början när en rad skapas och uppdateras när raden ändras,
* den `datetime` kolumnen är aldrig null,
* rader tas inte bort från tabellen

Utöver dessa kriterier rekommenderar Adobe att **indexering** den `datetime` kolumn som används för `Modified At` replikering, eftersom detta bidrar till att optimera replikeringshastigheten.

När uppdateringen körs identifieras nya eller ändrade data genom sökning efter rader som har ett värde i `datetime` -kolumn som inträffade efter den senaste uppdateringen. När nya rader identifieras replikeras de till Datan Warehouse. Om det finns några rader i [Data Warehouse Manager](../data-warehouse-mgr/tour-dwm.md), skrivs de över med de aktuella databasvärdena.

En tabell kan till exempel ha en kolumn som kallas `modified\_at` som anger senaste gången data ändrades. Om den senaste uppdateringen kördes tisdag klockan 12.00 söker uppdateringen efter alla rader som har en `modified\_at` större än tisdag klockan tolv. Alla identifierade rader som antingen har skapats eller ändrats sedan klockan 12.00 på tisdagen replikeras till Datan Warehouse.

**Visste du det?**
Även om din databas för närvarande inte stöder `Incremental` Replikeringsmetod kan eventuellt användas [gör ändringar i databasen](../../best-practices/mod-db-inc-replication.md) som skulle göra det möjligt att `Modified At` eller `Single Auto Incrementing PK`.

`Modified At` är inte bara den mest idealiska replikeringsmetoden, utan också den snabbaste. Den här metoden ger inte bara märkbara hastighetsökningar med stora datauppsättningar, den kräver inte heller att du konfigurerar ett alternativ för omkontroll. Andra metoder måste iterera genom en hel tabell för att identifiera ändringar, även om en liten delmängd av data har ändrats. `Modified At` itererar bara genom den lilla delmängden.

### Enkel autoökning primärnyckel

`Auto Incrementing` är ett beteende som i angiven ordning tilldelar primärnycklar till rader. Om en tabell `Auto Incrementing` och den högsta primärnyckeln i tabellen är 1 000 och nästa primärvärde är 1 001 eller högre. En tabell som inte använder `Auto Incrementing` beteendet kan tilldela ett primärnyckelvärde som är mindre än 1 000 eller hoppa till ett mycket större tal, men det är inte vanligt.

Den här metoden är utformad för att replikera nya data från tabeller som uppfyller följande kriterier:

* `single-column primary key`; och
* `primary key` datatypen är `integer`; och
* `auto incrementing` primärnyckelvärden.

När en tabell används `Single Auto Incrementing Primary Key` nya data identifieras genom att du söker efter primärnyckelvärden som är högre än det högsta värdet i Datan Warehouse. Om det högsta primärnyckelvärdet i Datan Warehouse till exempel är 500, söker nästa uppdatering efter rader med primärnyckelvärden på 501 eller högre.

### Lägg till datum

The `Add Date` metodfunktioner som liknar `Single Auto Incrementing Primary Key` -metod. I stället för att använda ett heltal som primärnyckel för tabellen använder den här metoden ett `timestamped` för att söka efter nya rader.

När en tabell använder `Add Date` nya data upptäcks genom att söka efter tidsstämplade värden som är större än det senaste datumet som synkroniseras med Datan Warehouse. Exempel: om en uppdatering senast kördes 2015-02-12:00:00, alla rader med en större tidsstämpel markeras som nya data och replikeras.

>[!NOTE]
>
>Till skillnad från `Modified At` metod, `Add Date` söker inte efter uppdaterad information på befintliga rader - den ser bara fram emot nya rader.

## Fullständiga replikeringsmetoder för tabeller {#fulltable}

### Fullständig tabell

`Full table` hela tabellen uppdateras när nya rader upptäcks. Detta är den i särklass minst effektiva replikeringsmetoden eftersom alla data måste bearbetas om under varje uppdatering, förutsatt att det finns nya rader.

Nya rader upptäcks genom att du skickar en fråga till databasen i början av synkroniseringsprocessen och räknar antalet rader. Om den lokala databasen innehåller fler rader än [!DNL Commerce Intelligence], uppdateras tabellen. Om antalet rader är identiskt, eller om [!DNL Commerce Intelligence] innehåller *mer* rader än din lokala databas, hoppas tabellen över.

Detta leder till den viktiga punkten att **`Full Table`replikeringen är inte kompatibel när:**

* fler rader tas bort än vad som har skapats i den lokala databastabellen mellan efterföljande uppdateringscykler, eller
* kolumnvärden ändras, men inga ytterligare rader skapas

I något av de ovanstående scenarierna `Full Table` inga ändringar upptäcks vid replikeringen och dina data blir inaktuella. På grund av ineffektiviteten hos denna replikeringsmetod och de krav som nämns ovan, `Full Table` replikering rekommenderas endast som en sista utväg.

### Primärnyckelgrupp

När en tabell använder `Primary Key Batch` (PK Batch) upptäcks nya data genom att rader i primärnyckelvärden, eller grupper, räknas. Även om du vanligtvis tänker att detta används med heltal kan även textvärden ordnas på ett sätt som gör att systemet kan definiera konstanta intervall.

Anta till exempel att en uppdatering körs och utför en radräkning för intervallet mellan 1 och 100. I den här uppdateringen hittar och loggar systemet 37 rader. I nästa uppdatering utförs radantalet igen i intervallet 1-100 och 41 rader hittas. Eftersom antalet rader är olika jämfört med den senaste uppdateringen undersöker systemet det intervallet (eller gruppen) mer i detalj.

Den här metoden är avsedd att replikera data från tabeller som uppfyller följande kriterier:

* icke-heltal med en kolumn, eller
* sammansatta nycklar (flera kolumner som innehåller primärnyckeln) - observera att kolumner som används i en sammansatt primärnyckel aldrig kan ha null-värden, eller
* primärnyckelvärden med en kolumn, ett heltal och utan autostegning.

Den här metoden är inte perfekt eftersom den är oerhört långsam på grund av den mängd bearbetning som måste utföras för att undersöka grupper och hitta ändringar. Adobe rekommenderar att du inte använder den här metoden såvida det inte är omöjligt att göra nödvändiga ändringar för att stödja de andra replikeringsmetoderna. Förväntade att uppdateringstiderna ska öka om den här metoden måste användas.

## Ställa in replikeringsmetoder

Replikeringsmetoderna anges tabell för tabell. Om du vill ange en replikeringsmetod för en tabell måste du [`Admin`](../../administrator/user-management/user-management.md) behörigheter så att du kan komma åt Data Warehouse Manager.

1. I Data Warehouse Manager väljer du tabellen i `Synced Tables` lista för att visa tabellens schema.
1. Den aktuella replikeringsmetoden visas under tabellnamnet. Klicka på länken om du vill ändra den.
1. I popup-fönstret som visas klickar du på alternativknappen bredvid antingen `Incremental` eller `Full Table` för att välja en replikeringstyp.
1. Klicka sedan på **[!UICONTROL Replication Method]** för att välja en metod. Till exempel: `Paused` eller `Modified At`.

   >[!NOTE]
   >
   >**Vissa inkrementella metoder kräver att du anger en`Replication Key`**. [!DNL Commerce Intelligence] använder den här nyckeln för att bestämma var nästa uppdateringscykel ska börja.
   >
   >Om du till exempel vill använda `modified at` metod för `orders` måste du ange en `date column` som replikeringsnyckeln. Det kan finnas flera alternativ för replikeringsnycklar, men du väljer `created at`eller när ordern skapades. Om den senaste uppdateringscykeln stoppades 12/1/2015 00:10:00, nästa cykel börjar replikera data med en `created at` datum större än detta.

1. När du är klar klickar du **[!UICONTROL Save]**.

Se hela processen:

![](../../assets/replication_method.gif)<!--{: width="801" height="341"}-->

## Radbrytning

För att avsluta har du sammanställt den här tabellen som jämför de olika replikeringsmetoderna. Det är otroligt praktiskt när du väljer en metod för tabellerna i Datan Warehouse.

| **`Method`** | **`Syncing New Data`** | **`Processing Rechecks on Large Data Sets`** | **`Handle Composite Keys?`** | **`Handle Non-Integer PKs?`** | **`Handle Non-Sequential PK Population?`** | **`Handle Row Deletion?`** |
|-----|-----|-----|-----|-----|-----|-----|
| `Auto-Incrementing Primary Key` | Snabbare | Långsam | Nej | Nej | Nej | Ja |
| `Primary Key Batch Monitoring` | Långsam | Långsam | Ja | Ja | Ja | Ja |
| `Modified At` | Snabbare | Snabbare | Ja | Ja | Ja | Nej |

{style="table-layout:auto"}

## Relaterad dokumentation

* [Förstå omkontroller av data](../data-warehouse-mgr/cfg-data-rechecks.md)
* [Ändra databasen som stöds ](../../best-practices/mod-db-inc-replication.md)
* [Optimera databasen för analys](../../best-practices/opt-db-analysis.md)
* [Minskar uppdateringstiderna](../../best-practices/reduce-update-cycle-time.md)
