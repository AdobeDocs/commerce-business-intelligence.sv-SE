---
title: Namnge rapporter och element i MBI
description: Lär dig de bästa sätten att namnge rapporter och element i [!DNL MBI].
exl-id: c662cedd-c779-4254-b04b-f3092a538c85
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 0%

---

# Namnge rapporter och element

Innan du börjar bygga in[!DNL MBI], vill Adobe dela med sig av några hemligheter till framgång. Det är viktigt att du vet hur man skapar mätvärden, filter och så vidare, men allt arbete kan vara bra om du inte hittar det du behöver eller om det är tvetydigt.

## Varför är nomenklatur viktigt? {#why}

Det sätt på vilket du namnger beräknade kolumner, mätvärden och rapporter avgör hur enkelt det är att navigera bland olika användare [!DNL MBI] konto. När du namnger de här funktionerna bör du tänka på de tre CSS-formaten:

* **TYDLIGHET** - Så att ni snabbt kan se vad en rapport visar, vad en mätare gör och så vidare.
* **ENHETLIGHET** - så att du (och Adobe supportteam) enkelt kan hitta och förstå element och rapporter i ditt konto.
* **KREDIGERBARHET** - För att ge inspiration och stärka andra datadrivna [!DNL MBI] -användare måste ni känna er säkra på hur de förstår och använder data!

Läs vidare för att få tips om hur du använder vår egen nomenklatur!

## Allmän bästa praxis {#general}

### Var meningsfull {#meaningful}

Var specifik när det är möjligt! Om det till exempel är landet, vet du om det är fraktlandet eller faktureringslandet? Är det användarens stad, eller så är det erbjudandets stad?

**Felaktigt exempel:**
Intäkter

Det här är vagt och berättar inte mycket för oss.

**Bra exempel:**
Intäkter (total bassumma + avgift) Användarens leveransland

Exemplen är specifika, vilket minskar risken för förvirring.

### Var konsekvent med versaler {#capitalize}

Adobe rekommenderar att stora bokstäver visas med de övriga gemena bokstäverna, såvida inte du har använt rätt skiftläge för inledande bokstäver. Till exempel: **Användarens ordernummer** i stället för **Användarens ordernummer.**

Det här är en fråga om att föredra, men det som är viktigt att komma ihåg är att vara konsekvent med vad du än väljer.

### Enhetskonsekvens {#entity}

Du har antagligen redan en nomenklatur på ditt företag. Se till att de mätvärden och dimensioner ni inför överensstämmer med vad som används i andra databaser och verktyg. Till exempel:

* Användare kontra kund kontra medlem konto
* Företag kontra organisation
* Registrering kontra skapande

### Stavning och grammatik {#spelling}

Kontrollera stavningen två gånger och glöm inte de där pesky-tillgångarna!

## Diagram {#charts}

Vid namngivning [diagram](../tutorials/using-visual-report-builder.md)är det mest användbart att följa den här formeln: **(dataperspektiv) + (mått) + (tidsperiod) + (tidsintervall)**

**Felaktigt exempel:**
Intäkter

Det här berättar ingenting om rapporten, som är dålig.

**Exempel:**
Ackumulerade intäkter de senaste 30 dagarna per månad

Det säger oss **exakt** vad som står i rapporten, som är fantastisk.

## Kontrollpaneler {#dashboards}

Kontrollpanelerna ska namnges på ett sätt som automatiskt representerar de rapporter som finns i dem. Om kontrollpanelen t.ex. bara innehåller information om intäkter och order kan du ge den ett namn som **Butiksnamn - intäkt och order.**

Om kontrollpanelen är en plats där du experimenterar med olika rapporter bör du överväga att ge den ett namn **Ditt namns sandlåda** så att du vet att rapporterna i dem är utkast.

## Dimensioner (beräknade kolumner) {#dimensions}

När ny namnges [dimensioner](../data-analyst/data-warehouse-mgr/creating-calculated-columns.md)är det mest användbart att följa den här formeln: **(Enhet) + (Nth) + (tidsram) + (beräkning) + (kommentarer)**. Till exempel:

Användarens första 30-dagars intäkt
* Användarens ordernummer
* Användarens ordernummer (väntar på granskning)

## Filteruppsättningar {#filterset}

[Filteruppsättningar](../data-user/reports/ess-manage-data-filters.md) är vanligtvis namngivna på ett sätt som förklarar den information de innehåller eller utesluter. Namnge t.ex. en filteruppsättning **Beställa artiklar vi räknar** gör att alla användare kan gå in, se logiken i filteruppsättningen och förstå vilken orderinformation som avgör vad som räknas i verksamheten. Kom ihåg att filteruppsättningar kan användas på både beräknade kolumner och mätvärden och bör vara enkla att förstå.

## Mått {#metrics}

[Mått](../data-user/reports/ess-manage-data-metrics.md) är i huvudsak frågor som du vill ha svar på regelbundet. Hur många beställningar har gjorts under den senaste månaden? Vilket är det genomsnittliga livstidsvärdet för era kunder? Det är bäst att namnge mätvärden så att de avspeglar svaret de ger användarna. Om du har samma mätvärden filtrerade för en viss butik eller avdelning bör de märkas som sådana. Till exempel:

Genomsnittlig kundservice (de första 30 dagarna) Butiksnamn - intäkt

Slutligen kan samma mätvärden ibland ordnas med olika tidsstämplar, beroende på hur enskilda användare beräknar dem. I så fall måste du se till att inkludera tidsstämpeln i namnet:

Intäkter (levererad\_at) Inkomster (skapad)

## Radbrytning {#wrapup}

Genom att etablera formaterings- och namnkonventioner tidigt får du hjälp med att skapa [!DNL MBI] konto. Kom ihåg de tre CS: tydlighet, konsekvens och trovärdighet.
