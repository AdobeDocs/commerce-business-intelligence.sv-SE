---
title: Analyserar kuponganvändning
description: Lär dig hur du analyserar kuponganvändning när du köper och behåller kunder.
exl-id: d4d1393f-1695-43f2-980a-84525f84031e
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1177'
ht-degree: 0%

---

# Kuponganvändning

Undrar du någonsin hur erbjudandet påverkar ditt företag? Vill du veta vilka kuponger som hjälper till eller skadar prestandan? I det här avsnittet behandlas analyser som ger en bra bild av dina kunders kuponganvändning genom att svara på följande frågor:

* Hur många kunder använder kuponger?
* Hur många kuponger används?
* Vad har du för intäkter före och efter kuponger?
* Vilket är det genomsnittliga ordervärdet före och efter kuponger?
* Vilken typ av kunder drar du till dig med kuponger?

## Rekommenderade mått {#metrics}

När du analyserar kuponganvändning bör du överväga att använda ([eller bygga](../../data-user/reports/ess-manage-data-metrics.md)) följande mått:

### Antal order

Den här mätningen visar antalet order med och utan kuponger över tiden. Detta visar om och hur ofta kunderna använder era kuponger och hur detta förändras över tid.

### Bruttointäkter

Det här måttet visar de bruttointäkter som du tjänar på order som innehåller en viss kupong. Bruttointäkten är en beräkning av hela priset för sålda artiklar, innan eventuella rabatter tillämpas. Detta kan hjälpa till att avgöra vilka kuponger som är kopplade till den högsta och den lägsta bruttointäkten.

### Rabatter från kuponger

Det här måttet kan visa det totala rabattbeloppet som tillämpas från kupongen. Det är viktigt att komma ihåg att dessa order kanske inte har gjorts utan kupongerna.

### Nettointäkter

Det här måttet visar den nettointäkt som du tjänar på order som innehåller en viss kupong. Nettointäkten är en beräkning av priset på de artiklar som säljs efter att alla rabatter har tillämpats. Detta kan hjälpa till att avgöra vilka kuponger som är kopplade till de högsta och lägsta nettointäkterna.

### Rabatterad procent

Här visas den del av bruttointäkten som motverkas av rabatter. För kuponger med rabatt är detta värde redan känt (till exempel 10 % rabatt). Trots detta ger denna åtgärd insikt i och en jämförelsemetod för kuponger som är en fast dollarrabatt.

### Genomsnittligt ordervärde netto

Detta mått visar det genomsnittliga ordervärdet när en kupong används. Du kan analysera om beställningar med kuponger konsekvent har ett lägre ordervärde än beställningar utan kuponger.

### Genomsnittlig orderrabatt

Här visas det genomsnittliga dollarvärdet som diskonterats från varje order där kuponger tillämpas. Här visas skillnaden mellan det genomsnittliga nettoordervärdet och det genomsnittliga bruttoordervärdet.

### Distinkta köpare

Det här måttet visar antalet distinkta köpare som använder en viss kupong.

### Genomsnittlig intäkt för livstid

Denna mätning hjälper till att utvärdera lojalitet och genomsnittliga intäkter som genereras av kunder som använder en viss kupong. När du utvärderar om kunder som använder kuponger har större värde än andra, måste du ta hänsyn till antalet olika köpare i varje kategori för att vara säker på att du har ett stort urval.

## Exempel {#example}

Nu när du vet vilka mätvärden du ska titta på kan du titta på ett exempel med tre olika kuponger - 10 % rabatt, 20 dollar på 100 eller mer och 10 dollar på.

| **Kupong** | **# order** | **Bruttointäkter** | **Bruttorabatter från kuponger** | **Nettointäkter** | **Procent rabatt** |
|-----|-----|-----|-----|-----|-----|
| **10 % rabatt** | 79 | 19 757 USD | 1 975,70 USD | 17 781,32 USD | 10,00 % |
| **$20 rabatt på $100+** | 101 | 13 928,91 USD | $2 020.00 | 11 908,91 USD | 14,50 % |
| **$10 rabatt** | 201 | 14 542,35 USD | $2 010.00 | 12 532,35 USD | 13,82 % |

{style="table-layout:auto"}


| **Kupong** | **Medel. nettoordervärde** | **Medel. orderrabatt** | **Distinkta köpare** | **Medel. livstidsintäkt** |
|-----|-----|-----|-----|-----|
| **10 % rabatt** | 225,08 USD | $25.01 | 79 | 361,50 USD |
| **$20 rabatt på $100+** | 117,91 USD | $20.00 | 95 | $218.76 |
| **$10 rabatt** | 62,35 USD | 10.00 USD | 199 | $84.27 |

{style="table-layout:auto"}

## Vad kan du ta ifrån det här?

Cirka 80 beställningar gjordes med kupongen &quot;10 % rabatt&quot;, 100 beställningar med kupongen &quot;$20&quot; på minst 100 dollar och 200 beställningar med kupongen &quot;$10&quot;. Antalet **order** som är associerade med varje kupong kan variera beroende på flera faktorer, bland annat:

* hur länge kupongen erbjuds.
* den tidpunkt på dag/vecka/månad/år då kupongen erbjöds.
* den säsong då kupongen erbjöds, beroende på verksamheten. Exempel:
* Kupongen&quot;10 % rabatt&quot; erbjöds under sommarmånaderna, men företaget säljer kläder för vintertid.

* begränsningar för kupongerna. Exempel:
* Kupongen &quot;$10 rabatt&quot; erbjuds endast nya kunder.
* Kupongen&quot;10 % rabatt&quot; erbjuds endast kunder som köper en vinterjacka i samma ordning.

* den typiska kundens köpbeteende.

Även om de **bruttorabatterna** för alla tre kuponger är lika (ca 2 000 USD), är antalet order för varje kupong olika. Genom att analysera rabatterna per order kan du förklara orsaken till kontrastsiffrorna. Kupongen&quot;10 % rabatt&quot; har minst antal order, men en **genomsnittlig orderrabatt** på cirka 25 USD. Även om den här kupongen har ett lågt antal order ger det höga genomsnittliga rabattvärdet bruttorabatten på cirka 2 000 dollar.

**Brutto- och nettointäkt** ger en övergripande uppfattning om det fullständiga värdet av de order som är kopplade till varje kupong. Den övergripande bilden ger dock ingen förståelse för de olika beteenden som är kopplade till varje kupong. När du tittar på en orderbas ser du att kupongen&quot;10 % rabatt&quot; har ett högt **genomsnittligt nettoordervärde**, vilket i sin tur leder till en hög **nettointäkt**.

Å andra sidan har kupongen&quot;10 % rabatt&quot; ett högt genomsnittligt rabattvärde ($25,01), men det lägsta **procentvärdet**. Detta är praktiskt när du tar hänsyn till det genomsnittliga nettoordervärdet 225,08 USD. Rabatten på&quot;10 % rabatt&quot; har en liten procentuell rabatt på ett stort genomsnittligt nettoordervärde, vilket innebär att den genomsnittliga orderrabatten är ett stort belopp.

Titta på de **distinkta köparna** och **genomsnittliga livstidsintäkterna** för varje kupong. &quot;10 % rabatt&quot; har samma antal order som distinkta köpare. Detta kan bero på att varje kund har en rabattkupong. Å andra sidan har rabattkupongen &quot;$20 på $100 eller mer&quot; och &quot;$10 av&quot; färre distinkta köpare än antalet order, vilket innebär att vissa kunder använde dessa kuponger flera gånger.

För genomsnittliga intäkter för livstid ser du att den genomsnittliga livstidsintäkten för varje kupong är större än respektive **genomsnittliga nettoordervärde**. Detta innebär att kunderna antingen gjorde upprepade inköp och/eller att deras ordervärde var mycket högre än det genomsnittliga nettoordervärdet.

## Vad mer kan jag analysera? {#otheranalyses}

Analyserna som nämns i det här avsnittet kan ge er värdefulla insikter om hur era kunder använder era kuponger, men det finns en mängd andra analyser som gör att ni kan fördjupa er lite mer.

**Du kan analysera dina kundförvärv från kuponger.**

Vilka kuponger uppmuntrar kunderna att lägga order? attraherar de här kupongen engångsköpare eller uppmuntrar de kundlojalitet (med andra ord kunder som gör upprepade köp)?

**Du kan analysera hur lång tid det tar för dina kunder att använda dina kuponger.**

Används era kuponger samma dag som de släpps eller går det en vecka eller två innan de flesta av era kunder använder dem?

**Du kan hitta det optimala rabattbeloppet som ökar kundlojaliteten och det totala värdet.**

Vilket rabattbelopp uppmuntrar återkommande köpare, högre genomsnittligt ordervärde och högre livstidsintäkter?

Genom att svara på dessa frågor får ni insikter om era kunder, deras beteende och vilka kuponger som ger ert företag mest värde.
