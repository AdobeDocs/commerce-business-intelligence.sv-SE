---
title: Ny arkitektur
description: Läs om fördelarna med att byta till ny arkitektur.
exl-id: cbb10673-5704-4a90-9574-5ac114f389b9
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Import/Export
source-git-commit: ddda796c9f32d22b1d679fc245eb11b92cd491cf
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 0%

---

# Ny arkitektur

[!DNL Adobe Commerce Intelligence] Produktteam och ingenjörsteam har fokuserat på att göra de mest svepande och efterfrågade förbättringarna möjliga under det senaste året. Adobe har stor glädje av att kunna meddela att det finns en ny [!DNL Commerce Intelligence]-produktarkitektur som gör dessa förbättringar till verklighet.

## Fördelar med den nya arkitekturen

* Skapa typer av kolumner i Datan Warehouse, inklusive beräknade kolumner med SQL.
* Nya kolumner är omedelbart tillgängliga.
* Datalatens har förbättrats dramatiskt.

## Tekniska fördelar

De viktigaste skillnaderna listas ovan, men den största förändringen är hur beräkningar utförs under uppdateringscykeln. Beräkningar körs inte längre på alla kolumner under varje uppdatering, utan körs på begäran från Visual Report Builder.

### Byt till ny arkitektur

Eftersom kontona är uppbyggda på olika sätt finns det ingen automatisk process för att migrera Datan Warehouse eller rapporterna till ett nytt arkitekturkonto. Att gå över till den nya arkitekturen kräver en omimplementering av ditt befintliga konto.

### Kostnad för att uppgradera till den nya arkitekturen

Ingen extra kostnad! Adobe skapar det här nya kontot så att du kan börja implementera om, vilket är kostnadsfritt i minst en månad. På så sätt får ni tid att ha båda kontona öppna så att ni enklare kan genomföra omimplementeringen och se till att teamet inte har någon lucka i tjänsten.

### Den tid som behövs för att återimplementera kontot i den nya arkitekturen

Tidpunkterna för omimplementering varierar beroende på vad du vill återskapa. Adobe rekommenderar att du utför följande steg i ditt befintliga konto för att få en uppfattning om vad som skulle ingå i din omimplementering:

* Identifiera en kärnuppsättning rapporter/kontrollpaneler.
* Identifiera mätvärden och dimensioner som krävs för att skapa rapporterna.
* Identifiera de kolumner som krävs för att återskapa dessa mått och mått.

När detta är klart vet du vilka data du behöver synkronisera med den nya Datan Warehouse för arkitektur för att kunna återskapa dessa kärnrapporter.

### Få hjälp

[!DNL Adobe Commerce Intelligence] [Services-teamet](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=sv-SE) kan utföra din omimplementering till en extra kostnad. Kontakta ditt [Adobe-kontoteam](../../guide-overview.md#Submitting-a-Support-Ticket) och förbered dig för att tillhandahålla en lista med instrumentpaneler/rapporter som du vill prioritera när du skapar i det nya kontot

### Statistik med befintlig arkitektur

Om dessa funktioner inte är viktiga för dig kan du hålla dig till ditt befintliga konto. Det kostar inget att behålla det befintliga kontot. Adobe fortsätter att stödja dessa konton utan ändringar.
