---
title: Ny arkitektur
description: Läs om fördelarna med att byta till ny arkitektur.
exl-id: cbb10673-5704-4a90-9574-5ac114f389b9
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Ny arkitektur

MBI Product and Engineering teams har fokuserat på att göra de mest svepande, efterfrågade förbättringarna möjliga under det senaste året. Adobe har nöjet att meddela att det finns en ny [!DNL MBI] produktarkitektur som gör dessa förbättringar till verklighet.

## Fördelar med den nya arkitekturen

* Skapa typer av kolumner i Data warehouse, inklusive beräknade kolumner med SQL.
* Nya kolumner är omedelbart tillgängliga.
* Datalatens har förbättrats dramatiskt.

## Tekniska fördelar

De viktigaste skillnaderna listas ovan, men den största förändringen är hur beräkningar utförs under uppdateringscykeln. Beräkningar körs inte längre på varje kolumn under varje uppdatering. körs i stället on demand från Visual Report Builder.

### Byt till ny arkitektur

Eftersom kontona är uppbyggda på olika sätt finns det ingen automatisk process för att migrera Data warehouse eller rapporter till ett nytt arkitekturkonto. Att gå över till den nya arkitekturen kräver att ditt befintliga konto implementeras på nytt.

### Kostnad för att uppgradera till den nya arkitekturen

Ingen extra kostnad! Adobe skapar det här nya kontot så att du kan börja återimplementera det, vilket är kostnadsfritt i minst en månad. På så sätt får ni tid att ha båda kontona öppna så att ni enklare kan genomföra omimplementeringen och se till att teamet inte har någon lucka i tjänsten.

### Den tid som behövs för att återimplementera kontot i den nya arkitekturen

Tidpunkterna för återimplementering varierar beroende på vad du vill återskapa. Adobe rekommenderar att du utför följande steg i ditt befintliga konto för att få en uppfattning om vad som skulle ingå i din implementering:

* Identifiera en kärnuppsättning rapporter/kontrollpaneler.
* Identifiera mätvärden och dimensioner som krävs för att skapa rapporterna.
* Identifiera de kolumner som krävs för att återskapa dessa mått och mått.

När detta är klart vet ni vilka data ni behöver synkronisera till den nya arkitekturen Data warehouse för att kunna återskapa dessa kärnrapporter.

### Få hjälp

The [!DNL MBI] Tjänsteteamet kan genomföra omimplementeringen till en extra kostnad. Kontakta [Adobe Account Team](../../guide-overview.md) och vara redo att tillhandahålla en lista med instrumentpaneler/rapporter som du vill prioritera när du skapar i det nya kontot

### Statistik med befintlig arkitektur

Om dessa funktioner inte är viktiga för dig kan du hålla dig till ditt befintliga konto. Det kostar inget att behålla det befintliga kontot. Adobe fortsätter att stödja dessa konton utan ändringar.
