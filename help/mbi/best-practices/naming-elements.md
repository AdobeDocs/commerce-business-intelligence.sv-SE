---
title: Namnge rapporter och element i Commerce Intelligence
description: Lär dig de bästa sätten att namnge rapporter och element i  [!DNL Commerce Intelligence].
exl-id: c662cedd-c779-4254-b04b-f3092a538c85
role: Admin, User
feature: Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 0%

---

# Namnge rapporter och element

Innan du börjar bygga i [!DNL Adobe Commerce Intelligence] vill Adobe dela några hemligheter med framgång. Det är viktigt att du vet hur man skapar mätvärden, filter och så vidare, men allt arbete kan vara bra om du inte hittar det du behöver eller om det är tvetydigt.

## Varför är nomenklatur viktigt? {#why}

Det sätt du namnger beräknade kolumner, mätvärden och rapporter på avgör i vilken ordning olika användare kan navigera i ditt [!DNL Commerce Intelligence]-konto. När du namnger de här funktionerna bör du tänka på de tre CSS-formaten:

* **CLARITY** - så att du snabbt kan se vad en rapport visar, vad ett mätvärde gör och så vidare.
* **ENHETLIGHET** - så att du (och Adobe supportteam) enkelt kan hitta och förstå element och rapporter i ditt konto.
* **CREDIBILITY** - För att kunna inspirera och ge andra datadrivna [!DNL Commerce Intelligence]-användare ökade möjligheter måste du känna dig säker på hur de förstår och använder data!

Läs vidare för att få tips om hur du använder vår egen nomenklatur!

## Allmän bästa praxis {#general}

### Var meningsfull {#meaningful}

Var specifik när det är möjligt! Om det till exempel är landet, vet du om det är fraktlandet eller faktureringslandet? Är det användarens stad, eller så är det erbjudandets stad?

**Felaktigt exempel:**
Intäkter

Det här är vagt och berättar inte mycket för oss.

**Bra exempel:**
Intäkter (total bassumma + avgift)
Användarens leveransland

Exemplen är specifika, vilket minskar risken för förvirring.

### Var konsekvent med versaler {#capitalize}

[!DNL Adobe] rekommenderar inledande versal med resten av tecknen i gemener, om inte rätt noun-stil används. Till exempel **Användarens ordernummer** i stället för **Användarens ordernummer.**

Det här är en fråga om att föredra, men det som är viktigt att komma ihåg är att vara konsekvent med vad du än väljer.

### Enhetskonsekvens {#entity}

Du har antagligen redan en nomenklatur på ditt företag. Se till att de mätvärden och dimensioner ni inför överensstämmer med vad som används i andra databaser och verktyg. Exempel:

* Användare kontra kund kontra medlem konto
* Företag kontra organisation
* Registrering kontra skapande

### Språkkontroll {#spelling}

Kontrollera stavningen två gånger och glöm inte de där pesky-tillgångarna!

## Diagram {#charts}

När du namnger [diagram](../tutorials/using-visual-report-builder.md) är det mest användbart att följa den här formeln: **(Dataperspektiv) + (mått) + (tidsperiod) + (tidsintervall)**

**Felaktigt exempel:**
Intäkter

Det här berättar ingenting om rapporten, som är dålig.

**Exempel:**
Ackumulerade intäkter de senaste 30 dagarna per månad

Detta visar **exakt** vad som finns i rapporten, vilket är fantastiskt.

## Kontrollpaneler {#dashboards}

Kontrollpanelerna ska namnges på ett sätt som automatiskt representerar de rapporter som finns i dem. Om din instrumentpanel till exempel bara innehåller information om intäkter och order kan du ge den ett namn som **Butiksnamn - Inkomster och order.**

Om instrumentpanelen däremot är en plats där du experimenterar med olika rapporter kan du ge den namnet **Sandbox** för ditt namn så att du vet att rapporterna i den är utkast.

## Dimensioner (beräknade kolumner) {#dimensions}

När du namnger nya [dimensioner](../data-analyst/data-warehouse-mgr/creating-calculated-columns.md) är det mest användbart att följa den här formeln: **(Enhet) + (Nth) + (tidsram) + (beräkning) + (kommentarer)**. Exempel:

Användarens första 30-dagars intäkt
* Användarens ordernummer
* Användarens ordernummer (väntar på granskning)

## Filteruppsättning {#filterset}

[Filteruppsättningar](../data-user/reports/ess-manage-data-filters.md) namnges vanligtvis på sätt som förklarar vilken information de inkluderar eller utesluter. Om du till exempel namnger en filteruppsättning **Beställningsobjekt som vi räknar** kan alla användare gå in, visa logiken i filteruppsättningen och förstå vilken orderinformation som avgör vad som räknas i verksamheten. Kom ihåg att filteruppsättningar kan användas på både beräknade kolumner och mätvärden och bör vara enkla att förstå.

## Mått {#metrics}

[Mätvärden](../data-user/reports/ess-manage-data-metrics.md) är i huvudsak frågor som du vill ha svar på regelbundet. Hur många beställningar har gjorts under den senaste månaden? Vilket är det genomsnittliga livstidsvärdet för era kunder? Det är bäst att namnge mätvärden så att de avspeglar svaret de ger användarna. Om du har samma mätvärden filtrerade för en viss butik eller avdelning bör de märkas som sådana. Exempel:

Normal kundservice (de första 30 dagarna)
Butiksnamn - intäkt

Slutligen kan samma mätvärden ibland ordnas med olika tidsstämplar, beroende på hur enskilda användare beräknar dem. I så fall måste du se till att inkludera tidsstämpeln i namnet:

Intäkter (levererat\_at)
Intäkter (skapade\_at)

## Radbrytning {#wrapup}

Om du upprättar formaterings- och namnkonventioner i förtid blir du bättre konfigurerad för ditt [!DNL Commerce Intelligence]-konto. Kom ihåg de tre CS: klarhet, konsekvens och trovärdighet.
