---
title: Optimera databasen för analys
description: Lär dig hur du optimerar databasen för analys.
exl-id: e73e1a1e-c933-476d-97bc-bd8f52bb2fa1
role: Admin, Data Architect, Data Engineer, User
feature: Business Performance, Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 0%

---

# Optimera databasen

Den främsta fördelen med att använda en operativ databas för [!DNL Adobe Commerce Intelligence] är att inget behöver skapas eller ändras för att samla in data. Värdefull information finns redan - du behöver bara låsa upp den.

Det här avsnittet innehåller några rekommendationer som hjälper dig att optimera databasen för analys och hämta åtgärdbara insikter från rådata.

## Ta inte bort data

>[!TIP]
>
>De lokala och internationella lagar som påverkar din verksamhet (och dina egna användarvillkor) kan påverka vilka typer av data du kan behålla och hur länge du kan behålla dem. Efterlevnad av dessa lagar bör vara din första prioritet.

När en order annulleras, en användare inaktiverar sitt konto eller en produkt avbryts är det frestande att ta bort den associerade informationen i databasen. Tabeller växer och det verkar som en klok idé att eliminera rörighet. Om du tar bort rader innebär det dock att informationen går förlorad för alltid eller att du måste leta igenom gamla säkerhetskopior för att hitta den.

I stället kan du lägga till en statuskolumn i tabellen som anger när raden inte längre är aktiv eller relevant. Vi rekommenderar även att du lägger till en kolumn som lagrar datumet då ändringen utfördes eller skapar en logg för historiska ändringar. Om tabellerna blir så stora att prestandan börjar bli lidande bör du arkivera gamla data i en tabell som används för analys.

## Sällan överskrivna data

Överskrivande data bör göras sparsamt och med försiktighet.

Många företag använder till exempel inloggningsdatum för att lagra det senaste inloggningsdatumet i stället för en tabell med historiska inloggningar. Även om du kanske bara behöver det senaste inloggningsdatumet för funktionella syften, är överskrivna data en enorm förlust ur analysperspektiv. Genom att inte ha en komplett logg över dessa åtgärder elimineras möjligheten att se hur många användare som varit borta under långa perioder och sedan återaktiveras. Det gör det också omöjligt att bygga saker som användarinteraktionskohortanalyser som baseras på inloggningar.

Om du uppdaterar en post på grund av någon typ av användaråtgärd bör du vanligtvis inte skriva över information om en tidigare eller separat användaråtgärd.

## Inkludera `Updated_at` kolumner för data som uppdaterats över tid

Om en tabells rader kommer att ha ändrade värden över tiden, till exempel **order\_status** ändringar från `processing` till `complete`, inkluderar du en **uppdaterad\_at** -kolumn som registreras när den senaste ändringen inträffar. Kontrollera att ett **uppdaterat\_at**-värde är tillgängligt när den nya dataraden infogas första gången, när datumet **uppdaterad\_at** motsvarar datumet **skapad\_at**.

Förutom optimering för analys kan du även använda [metoder för inkrementell replikering](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md) i **uppdaterade\_at** -kolumner, vilket kan korta uppdateringscyklernas längd.

## Store User Acquisition Source

En av de vanligaste felen är att [användarens inhämtningskälla](../data-analyst/analysis/google-track-user-acq.md) (UAS) inte lagras i den operativa databasen. I de flesta fall när detta är ett problem spåras bara UAS via [!DNL Google Analytics] eller något annat webbanalysverktyg. Dessa verktyg kan vara värdefulla, men det finns vissa nackdelar med att enbart lagra UAS i dem. Du kan t.ex. inte extrahera data på användarnivå från dessa verktyg. När det är möjligt är det oftast en svår process. Det bör vara enkelt att få fram den här informationen och kombinera den med data från andra källor, t.ex. beteendeinformation och transaktionsinformation som också lagras i databasen.

Att lagra UAS i din egen databas är ofta den största förbättring som onlineföretag kan göra av sina analysfunktioner. Detta gör det möjligt för UAS att analysera försäljning, användarinteraktion, betalningsperioder, kundens livstidsvärde, bortfall och andra kritiska mätvärden. [Den här informationen är viktig när du ska bestämma var marknadsföringsresurser ska investeras ](../data-analyst/analysis/most-value-source-channel.md).

Alltför många företag fokuserar enbart på att hitta kanaler som ger nya användare till lägsta möjliga kostnad. Om ni inte håller på att hålla reda på kvaliteten hos de användare ni skaffat från varje kanal riskerar ni att locka till er användare som inte genererar något affärsvärde.

## Inställningar för datatabell

### Ange en primärnyckel

En [primärnyckel](https://en.wikipedia.org/wiki/Unique_key) är en oföränderlig kolumn (eller en uppsättning kolumner) som skapar unika värden i en tabell. Primära nycklar är oerhört viktiga eftersom de ser till att dina tabeller replikeras korrekt i [!DNL Commerce Intelligence].

När du skapar primärnycklar ska du använda en heltalsdatatyp för kolumnen som ökar automatiskt. Adobe rekommenderar att du undviker att använda flera kolumnprimärnycklar där det är möjligt.

Om tabellen är en SQL-vy lägger du till en kolumn som kan fungera som primärnyckel. [!DNL Commerce Intelligence] kan automatiskt identifiera den här kolumnen som en primärnyckel.

### Tilldela en datatyp till din datakolumn

Om en datakolumn inte har en tilldelad [datatyp](https://en.wikipedia.org/wiki/Data_type), [!DNL Commerce Intelligence] gissar vilken datatyp som ska användas. Om systemet gissar fel kanske du inte kan utföra de relevanta analyserna förrän supportteamet på Adobe justerar kolumnen till rätt datatyp. Om till exempel en datumkolumn tolkas som en numerisk datatyp kan du använda den datumdimensionen för att skapa en trend över tiden.

### Lägg till prefix i datatabellerna om du har flera databaser

Om du har fler än en databas ansluten till [!DNL Commerce Intelligence] rekommenderar Adobe att du lägger till prefix i tabellerna för att undvika förvirring. Prefix hjälper dig att komma ihåg varifrån mätvärden eller datamängder kommer.
