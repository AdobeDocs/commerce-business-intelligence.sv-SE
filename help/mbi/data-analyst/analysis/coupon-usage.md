---
title: Analyserar kuponganvändning
description: Lär dig hur du analyserar kuponganvändning för att förvärva och behålla kunder.
exl-id: d4d1393f-1695-43f2-980a-84525f84031e
source-git-commit: 4cad1e05502630e13f7a2d341f263140a02b3d82
workflow-type: tm+mt
source-wordcount: '1141'
ht-degree: 2%

---

# Kuponganvändning

Undrar du någonsin hur erbjudanden kuponger påverkar ditt företag? Vill du veta vilka kuponger som bidrar till sämre prestanda? Detta ämne utforskar analyser som ger dig en bra bild av dina kunders kuponganvändning genom att svara på dessa frågor:

* Hur många kunder använder kuponger?
* Hur många kuponger används?
* Vad har du för intäkter före och efter kuponger?
* Vilket är det genomsnittliga ordervärdet före och efter kuponger?
* Vilken typ av kunder drar du till dig med kuponger?

## Rekommenderade mått {#metrics}

När du analyserar kuponganvändning bör du använda ([eller byggnad](../../data-user/reports/ess-manage-data-metrics.md)) dessa mått:

### Antal order

Den här mätningen visar antalet order med och utan kuponger över tiden. Detta visar om och hur ofta kunderna använder era kuponger och hur detta förändras över tiden.

### Bruttointäkter

Detta mått visar bruttointäkten som du tjänar från beställningar som innehåller en viss kupong. Bruttointäkten är en beräkning av det fulla priset på de sålda objekten, före eventuella rabatter. Detta kan bidra till att fastställa vilka kuponger som är kopplade till den högsta och lägsta bruttointäkten.

### Rabatter på kuponger

Detta mått kan visa det totala rabattbeloppet som tillämpas från kupongerna. Det är viktigt att notera att dessa order inte kan ha inträffat utan kupongerna.

### Nettointäkter

Det här måttet visar de nettointäkter som du tjänar på order som innehåller en viss kupong. Nettointäkten är en beräkning av priset på de artiklar som säljs efter att alla rabatter har tillämpats. Detta kan hjälpa till att avgöra vilka kuponger som är kopplade till de högsta och lägsta nettointäkterna.

### Rabatterad procent

Här visas den andel av bruttointäkterna som uppvägs av rabatter. För kuponger som ger en procentuell rabatt är detta värde redan känt (till exempel 10 % rabatt). Trots detta ger denna åtgärd insikt och en metod för jämförelse av kuponger som är en fast dollarrabatt.

### Genomsnittligt nettoordervärde

Detta mått visar det genomsnittliga ordervärdet när en kupong används. Du kan analysera om beställningar med kuponger konsekvent har ett lägre ordervärde än beställningar utan kuponger.

### Genomsnittlig orderrabatt

Här visas det genomsnittliga dollarvärdet som diskonterats från varje order där kuponger tillämpas. Här visas skillnaden mellan det genomsnittliga nettoordervärdet och det genomsnittliga bruttoordervärdet.

### Distinkta köpare

Det här nyckeltalet visar antalet distinkta köpare som använder en viss kupong.

### Genomsnittlig livstidsintäkt

Denna mätning hjälper till att utvärdera lojalitet och genomsnittliga intäkter som genereras av kunder som använder en viss kupong. När du utvärderar om kunder som använder kuponger har större värde än andra, måste du ta hänsyn till antalet olika köpare i varje kategori för att vara säker på att du har ett stort urval.

## Exempel {#example}

Nu när du vet vilka mätvärden du ska titta på kan du titta på ett exempel med tre olika kuponger - 10 % rabatt, 20 dollar på 100 eller mer och 10 dollar på.

| **Kupong** | **Antal order** | **Bruttointäkter** | **Bruttorabatter från kuponger** | **Nettointäkter** | **Rabatterad procent** |
|-----|-----|-----|-----|-----|-----|
| **10 % rabatt** | 79 | $19,757.02 | $1,975.70 | $17,781.32 | 10.00% |
| **$20 rabatt $100+** | 101 | $13,928.91 | $2,020.00 | $11,908.91 | 14.50% |
| **10 dollar rabatt** | 201 | $14,542.35 | $2,010.00 | $12,532.35 | 13.82% |

{style="table-layout:auto"}


| **Kupong** | **Medel nettoordervärde** | **Medel orderrabatt** | **Distinkta köpare** | **Medel. omsättning** |
|-----|-----|-----|-----|-----|
| **10 % rabatt** | $225.08 | $25.01 | 79 | $361.50 |
| **$20 rabatt på $100+** | $117.91 | $20.00 | 95 | $218.76 |
| **10 dollar rabatt** | $62.35 | $10.00 | 199 | $84.27 |

{style="table-layout:auto"}

## Vad kan du ta ifrån det här?

Cirka 80 beställningar gjordes med &quot;10% off&quot; kupong, 100 beställningar med &quot;$20 av $ 100 eller mer&quot; kupong, och 200 beställningar med &quot;$10 off&quot; kupong. Den **antal order** i samband med varje kupong kan variera beroende på flera faktorer, inklusive:

* den tidsperiod för vilken kupongerna erbjöds.
* den tidpunkt på dagen/veckan/månaden/året som kupongerna erbjöds.
* den säsong då kupongen erbjöds, beroende på verksamheten. Till exempel:
* Kupongen&quot;10 % rabatt&quot; erbjöds under sommarmånaderna, men företaget säljer kläder för vintertid.

* begränsningar för kupongerna. Till exempel:
* Kupongen &quot;$10 rabatt&quot; erbjuds endast nya kunder.
* Kupongen &quot;10% off&quot; erbjuds endast till kunder som köper en vinterrock i samma ordning.

* den typiska kundens köpbeteende.

Med **bruttorabatter** för alla tre kuponger är lika (ca 2 000 dollar), antalet beställningar för varje kupong är olika. Genom att analysera rabatterna per order kan du förklara orsaken till kontrastsiffrorna. Kupongen&quot;10 % rabatt&quot; har minst antal order, men en **genomsnittlig orderrabatt** cirka 25 dollar. Även om den här kupongen har ett lågt antal order ger det höga genomsnittliga rabattvärdet bruttorabatten på cirka 2 000 dollar.

**Brutto- och nettointäkter** ge en övergripande uppfattning om det fulla värdet av de order som är kopplade till varje kupong. Den övergripande bilden ger dock ingen förståelse för de olika beteenden som är kopplade till varje kupong. När du tittar på en per order basis, kan du se att den &quot;10% off&quot; kupongen har en hög **genomsnittlig nettoorder** värde, vilket i sin tur leder till en hög **nettointäkter**.

Å andra sidan har kupongen&quot;10 % rabatt&quot; ett högt genomsnittligt rabattvärde ($25,01), men det lägsta **procent rabatt**. Detta är praktiskt när du tar hänsyn till det genomsnittliga nettoordervärdet 225,08 USD. Rabatten på&quot;10 % rabatt&quot; har en liten procentuell rabatt på ett stort genomsnittligt nettoordervärde, vilket innebär att den genomsnittliga orderrabatten är ett stort belopp.

Titta på **distinkta köpare** och **genomsnittlig intäkt för livstid** för varje kupong. Kupongen &quot;10% off&quot; har samma antal order som olika köpare. Detta kan bero på att varje kund begränsas till en kupong. Å andra sidan har kupongerna &quot;$20 av $100 eller mer&quot; och &quot;$10 av&quot; färre distinkta köpare än antalet beställningar, vilket innebär att vissa kunder använde dessa kuponger flera gånger.

För genomsnittliga livstidsintäkter, kan du se att den genomsnittliga livstidsintäkten för varje kupong är större än respektive **genomsnittlig nettoorder** värde. Detta innebär att kunderna gjorde upprepade inköp och/eller att deras ordervärde var mycket högre än det genomsnittliga nettoordervärdet.

## Vad mer kan jag analysera? {#otheranalyses}

Analyserna som nämns i det här avsnittet kan ge er värdefulla insikter om hur era kunder använder era kuponger, men det finns en mängd andra analyser som gör att ni kan fördjupa er lite mer.

**Ni kan analysera era kundförvärv utifrån kuponger.**

Vilka kuponger uppmuntrar kunderna att lägga order? attraherar de här kupongen engångsköpare eller uppmuntrar de kundlojalitet (med andra ord kunder som gör upprepade köp)?

**Ni kan analysera hur lång tid det tar för era kunder att använda era kuponger.**

Används era kuponger samma dag som de släpps eller går det en vecka eller två innan de flesta av era kunder använder dem?

**Ni kan hitta det optimala rabattbeloppet som ökar kundlojaliteten och det totala värdet.**

Vilket rabattbelopp uppmuntrar återkommande köpare, högre genomsnittligt ordervärde och högre livstidsintäkter?

Genom att svara på dessa frågor får ni insikter om era kunder, deras beteende och vilka kuponger som ger ert företag mest värde.
