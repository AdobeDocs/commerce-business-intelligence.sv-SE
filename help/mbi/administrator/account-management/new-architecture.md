---
title: Ny arkitektur
description: Läs om fördelarna med att byta till ny arkitektur.
exl-id: cbb10673-5704-4a90-9574-5ac114f389b9
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---

# Ny arkitektur

Våra produkts- och ingenjörsteam har fokuserat på att göra de mest svepande, efterfrågade förbättringarna möjliga under det senaste året. Vi är stolta över att kunna meddela att det finns en ny [!DNL MBI] produktarkitektur som gör dessa förbättringar till verklighet.

## Fördelar med den nya arkitekturen

* Skapa nya typer av kolumner i data warehouse, inklusive beräknade kolumner med SQL.
* Nya kolumner är omedelbart tillgängliga.
* Datalatens har förbättrats dramatiskt.

## Tekniska fördelar

De viktigaste skillnaderna listas ovan, men det som tekniskt sett har ändrats är hur vi utför beräkningar under uppdateringscykeln. Beräkningar körs inte längre på varje kolumn under varje uppdatering. körs i stället on demand från Visual Report Builder.

### Byt till ny arkitektur

Eftersom kontona har skapats på ett helt annat sätt finns det ingen automatisk process som vi kan använda för att migrera data warehouse eller rapporter till ett nytt arkitekturkonto, så om vi går över till den nya arkitekturen krävs en omimplementering av ditt befintliga konto.

### Kostnad för att uppgradera till den nya arkitekturen

Ingen extra kostnad! Vi kommer att skapa ett nytt konto som du kan använda för att börja implementera på nytt, vilket är kostnadsfritt i minst en månad. På så sätt får ni tid att ha båda kontona öppna så att ni enklare kan genomföra omimplementeringen och se till att teamet inte har någon lucka i tjänsten.

### Den tid som behövs för att återimplementera kontot i den nya arkitekturen

Tidpunkterna för omimplementering varierar beroende på vad du vill återskapa. Vi rekommenderar att du utför följande steg i ditt befintliga konto för att få en uppfattning om vad som skulle ingå i din omimplementering:

* Identifiera en kärnuppsättning rapporter/kontrollpaneler.
* Identifiera mätvärden och dimensioner som krävs för att skapa rapporterna.
* Identifiera de kolumner som krävs för att återskapa dessa mått och mått.

När detta är klart vet ni vilka data ni behöver synkronisera till den nya arkitekturen data warehouse för att kunna återskapa dessa kärnrapporter.

### Få hjälp

The [!DNL MBI] Tjänsteteamet kan genomföra omimplementeringen till en extra kostnad. Kontakta oss [Customer Success Team](../../guide-overview.md) och vara redo att tillhandahålla en lista med instrumentpaneler/rapporter som du vill prioritera när du skapar i det nya kontot

### Statistik med befintlig arkitektur

Om dessa funktioner inte är viktiga för dig kan du hålla dig till ditt befintliga konto. Det finns ingen extra kostnad för att behålla ditt befintliga konto, och vi kommer att fortsätta stödja dessa konton utan ändringar.
