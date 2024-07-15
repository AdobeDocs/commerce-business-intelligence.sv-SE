---
title: Konfigurerar replikeringsmetoder
description: Lär dig hur tabeller är ordnade och hur tabelldata fungerar gör att du kan välja den bästa replikeringsmetoden för tabellerna.
exl-id: 83895c48-a6ec-4b01-9890-164e0b21dcbc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Data Import/Export
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1433'
ht-degree: 0%

---

# Konfigurerar replikeringsmetoder

`Replication`-metoder och [omkontroller](../data-warehouse-mgr/cfg-data-rechecks.md) används för att identifiera nya eller uppdaterade data i databastabellerna. Att ställa in dem på rätt sätt är avgörande för att både datakvaliteten och optimerade uppdateringstider ska kunna garanteras. Det här avsnittet fokuserar på replikeringsmetoder.

När nya tabeller synkroniseras i [Data Warehouse Manager](../data-warehouse-mgr/tour-dwm.md) väljs automatiskt en replikeringsmetod för tabellen. Om du förstår de olika replikeringsmetoderna, hur tabeller är ordnade och hur tabelldata fungerar kan du välja den bästa replikeringsmetoden för tabellerna.

## Vilka är replikeringsmetoderna?

`Replication` metoder kan delas in i tre grupper - `Incremental`, `Full Table` och `Paused`.

[**[!UICONTROL Incremental Replication]**](#incremental) betyder att [!DNL Commerce Intelligence] endast replikerar nya eller uppdaterade data för varje replikeringsförsök. Eftersom dessa metoder minskar fördröjningen avsevärt rekommenderar Adobe att du använder den där det är möjligt.

[**[!UICONTROL Full Table Replication]**](#fulltable) betyder att [!DNL Commerce Intelligence] replikerar hela innehållet i en tabell vid varje replikeringsförsök. På grund av den potentiellt stora mängd data som kan replikeras kan dessa metoder öka fördröjningen och uppdateringstiden. Om en tabell innehåller tidstämpling- eller datetime-kolumner rekommenderar Adobe att du använder en Stegvis metod i stället.

**[!UICONTROL Paused]** anger att replikeringen för tabellen har stoppats eller pausats. [!DNL Commerce Intelligence] söker inte efter nya eller uppdaterade data under en uppdateringscykel. Det innebär att inga data replikeras från en tabell som har detta som replikeringsmetod.

## Stegvisa replikeringsmetoder {#incremental}

### Ändrad vid (mest idealisk)

Replikeringsmetoden `Modified At` använder en datetime-kolumn, som fylls i när en rad skapas och sedan uppdateras när data ändras, för att hitta data som ska replikeras. Den här metoden är utformad för att fungera med tabeller som uppfyller följande kriterier:

* innehåller en `datetime`-kolumn som fylls i från början när en rad skapas och uppdateras när raden ändras,
* `datetime`-kolumnen är aldrig null;
* rader tas inte bort från tabellen

Utöver dessa villkor rekommenderar Adobe **indexering** den `datetime`-kolumn som används för `Modified At`-replikering, eftersom detta bidrar till att optimera replikeringshastigheten.

När uppdateringen körs identifieras nya eller ändrade data genom sökning efter rader som har ett värde i kolumnen `datetime` som inträffade efter den senaste uppdateringen. När nya rader identifieras replikeras de till Datan Warehouse. Om det finns rader i [Data Warehouse Manager](../data-warehouse-mgr/tour-dwm.md) skrivs de över med de aktuella databasvärdena.

En tabell kan till exempel ha en kolumn med namnet `modified\_at` som anger att data senast ändrades. Om den senaste uppdateringen kördes tisdag klockan 12.00 söker uppdateringen efter alla rader med ett `modified\_at`-värde som är större än tisdag klockan 12.00. Alla identifierade rader som antingen har skapats eller ändrats sedan klockan 12.00 på tisdagen replikeras till Datan Warehouse.

**Visste du det?**
Även om din databas inte har stöd för en `Incremental` replikeringsmetod kan du [göra ändringar i din databas](../../best-practices/mod-db-inc-replication.md) som skulle kunna användas av `Modified At` eller `Single Auto Incrementing PK`.

`Modified At` är inte bara den mest idealiska replikeringsmetoden, utan även den snabbaste. Den här metoden ger inte bara märkbara hastighetsökningar med stora datauppsättningar, den kräver inte heller att du konfigurerar ett alternativ för omkontroll. Andra metoder måste iterera genom en hel tabell för att identifiera ändringar, även om en liten delmängd av data har ändrats. `Modified At` itererar bara genom den lilla delmängden.

### Enkel autoökning primärnyckel

`Auto Incrementing` är ett beteende som sekventiellt tilldelar primärnycklar till rader. Om en tabell är `Auto Incrementing` och den högsta primärnyckeln i tabellen är 1 000 är nästa primära värde 1 001 eller högre. En tabell som inte använder beteendet `Auto Incrementing` kan tilldela ett primärnyckelvärde som är mindre än 1 000 eller hoppa till ett mycket större tal, men det är inte vanligt.

Den här metoden är utformad för att replikera nya data från tabeller som uppfyller följande kriterier:

* `single-column primary key`; och
* datatypen `primary key` är `integer`; och
* `auto incrementing` primärnyckelvärden.

När en tabell använder `Single Auto Incrementing Primary Key`-replikering upptäcks nya data genom sökning efter primärnyckelvärden som är högre än det högsta värdet i Datan Warehouse. Om det högsta primärnyckelvärdet i Datan Warehouse till exempel är 500, söker nästa uppdatering efter rader med primärnyckelvärden på 501 eller högre.

### Lägg till datum

Metoden `Add Date` fungerar ungefär som metoden `Single Auto Incrementing Primary Key`. I stället för att använda ett heltal för tabellens primärnyckel använder den här metoden en `timestamped`-kolumn för att söka efter nya rader.

När en tabell använder `Add Date`-replikering upptäcks nya data genom att söka efter tidsstämplade värden som är större än det senaste datumet som synkroniseras med Datan Warehouse. Om en uppdatering senast kördes 20/12/2015 09:00:00 markeras alla rader med en tidsstämpel som är större än denna som nya data och replikeras.

>[!NOTE]
>
>Till skillnad från metoden `Modified At` söker `Add Date` inte efter uppdaterad information på befintliga rader, utan bara fram till nya rader.

## Fullständiga replikeringsmetoder för tabeller {#fulltable}

### Fullständig tabell

`Full table`-replikeringen uppdaterar hela tabellen när nya rader upptäcks. Detta är den i särklass minst effektiva replikeringsmetoden eftersom alla data måste bearbetas om under varje uppdatering, förutsatt att det finns nya rader.

Nya rader upptäcks genom att du skickar en fråga till databasen i början av synkroniseringsprocessen och räknar antalet rader. Om din lokala databas innehåller fler rader än [!DNL Commerce Intelligence] uppdateras tabellen. Om antalet rader är identiska, eller om [!DNL Commerce Intelligence] innehåller *fler* rader än din lokala databas, hoppas tabellen över.

Detta leder till den viktiga punkten att **`Full Table`-replikering är inkompatibel när:**

* fler rader tas bort än vad som har skapats i den lokala databastabellen mellan efterföljande uppdateringscykler, eller
* kolumnvärden ändras, men inga ytterligare rader skapas

I något av de ovanstående scenarierna identifierar `Full Table`-replikeringen inga ändringar och dina data blir inaktuella. På grund av den här replikeringsmetodens ineffektivitet, och de krav som anges ovan, rekommenderas `Full Table`-replikering endast som en sista utväg.

### Primärnyckelgrupp

När en tabell använder `Primary Key Batch` (PK Batch) identifieras nya data genom att rader i primärnyckelvärden, eller grupper, räknas. Även om du vanligtvis tänker att detta används med heltal kan även textvärden ordnas på ett sätt som gör att systemet kan definiera konstanta intervall.

Anta till exempel att en uppdatering körs och utför en radräkning för intervallet mellan 1 och 100. I den här uppdateringen hittar och loggar systemet 37 rader. I nästa uppdatering utförs radantalet igen i intervallet 1-100 och 41 rader hittas. Eftersom antalet rader är olika jämfört med den senaste uppdateringen undersöker systemet det intervallet (eller gruppen) mer i detalj.

Den här metoden är avsedd att replikera data från tabeller som uppfyller följande kriterier:

* icke-heltal med en kolumn, eller
* sammansatta nycklar (flera kolumner som innehåller primärnyckeln) - observera att kolumner som används i en sammansatt primärnyckel aldrig kan ha null-värden, eller
* primärnyckelvärden med en kolumn, ett heltal och utan autostegning.

Den här metoden är inte perfekt eftersom den är oerhört långsam på grund av den mängd bearbetning som måste utföras för att undersöka grupper och hitta ändringar. Adobe rekommenderar att du inte använder den här metoden såvida det inte är omöjligt att göra nödvändiga ändringar för att stödja de andra replikeringsmetoderna. Förväntade att uppdateringstiderna ska öka om den här metoden måste användas.

## Ställa in replikeringsmetoder

Replikeringsmetoderna anges tabell för tabell. Om du vill ange en replikeringsmetod för en tabell behöver du [`Admin`](../../administrator/user-management/user-management.md) behörigheter så att du kan komma åt Data Warehouse Manager.

1. I tabellhanteraren markerar du Datan Warehouse i listan `Synced Tables` för att visa tabellens schema.
1. Den aktuella replikeringsmetoden visas under tabellnamnet. Klicka på länken om du vill ändra den.
1. Klicka på alternativknappen bredvid `Incremental` eller `Full Table`-replikering i popup-fönstret som visas för att välja en replikeringstyp.
1. Klicka sedan på listrutan **[!UICONTROL Replication Method]** för att välja en metod. Till exempel `Paused` eller `Modified At`.

   >[!NOTE]
   >
   >**Vissa inkrementella metoder kräver att du anger`Replication Key`**. [!DNL Commerce Intelligence] använder den här nyckeln för att avgöra var nästa uppdateringscykel ska börja.
   >
   >Om du till exempel vill använda metoden `modified at` för tabellen `orders` måste du ange en `date column` som replikeringsnyckel. Det kan finnas flera alternativ för replikeringsnycklar, men du väljer `created at` eller den tidpunkt då ordern skapades. Om den senaste uppdateringscykeln stoppades 12/1/2015 00:10:00 börjar nästa cykel replikera data med ett `created at` -datum som är större än detta.

1. När du är klar klickar du på **[!UICONTROL Save]**.

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
