---
title: Kohortanalys för livstidsintäkt
description: Utforska kraften i Commerce Intelligence-kohortanalyser.
exl-id: f2b55745-d364-4ba6-9857-ce9cee05c3ae
source-git-commit: 6b1bd96a0f9ae8bda3ae8db8ca78ad655079f2a4
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 0%

---

# [!DNL Lifetime Revenue Cohort] Analys

Det finns många sätt att se på data i [!DNL Adobe Commerce Intelligence]och du vet att tolkning och förståelse är lika viktiga som beräkning och visualisering. Det här avsnittet utforskar möjligheterna i [!DNL Commerce Intelligence] `cohort` analys.

## Vad gör `lifetime revenue cohort` betyder analys?

Tabellen nedan visar den ackumulerade utgiften per användare under en tidsperiod efter att de har förvärvats. `Cohorts` av användarna delas upp efter anskaffningsmånad.

Den orange raden ovan visar till exempel genomsnittet för användare som förvärvades i november 2011. Den första datapunkten innebär att de användare som förvärvades i november den första månaden i genomsnitt tillbringade cirka `$200`. Den andra datapunkten innebär att i slutet av den andra månaden hade dessa användare i genomsnitt spenderat cirka `$240`. De genomsnittliga utgifterna under månad två var ungefär `$40 (240 - 200)`. De olika linjerna representerar olika kohorter av användare. Den gröna linjen representerar de användare som förvärvades i december och den blå är de användare som förvärvades i oktober.

## Varför är detta viktigt?

Den här typen av `cohort` analys kan vara användbar för flera olika syften, men den mest omedelbara fördelen är ofta bättre beslut om kundförvärv. Många företag begränsar sina marknadsföringsutgifter till kanaler som ger lönsamhet på kundens första inköp. Dessa företag betalar för att förvärva kunder via en viss kanal så länge deras genomsnittliga första inköp ger mer `gross margin` mer än vad det kostar att förvärva dem.

Problemet med detta tillvägagångssätt är att det ofta leder till en underinvestering i tillväxt. Om era konkurrenter marknadsför baserat på en djupare förståelse för köpbeteenden så växer ni inte. The `lifetime revenue cohort` analyser hjälper er att förstå konsekvenserna av att utöka era kundvärvningsutgifter och är ett enkelt sätt att förmedla detta till resten av teamet. Om framtida kunder beter sig som befintliga kunder blir det en förutsägbar återbetalningsperiod om kunderna skaffar sig ett högre CPA. Beroende på företagets kassaställning kan du definiera vilken betalningsperiod du känner dig bekväm med, hitta rätt position i diagrammet och använda rätt belopp.

Du kan också använda den här analysen för att se om du blir bättre på att introducera, engagera och generera intäkter från de användare du köper. Den här `cohort` analys är ett bra sätt att se om en kostnadsfri leveranskampanj för nya användare resulterade i återkommande köpare eller engångsköpare som aldrig kommer tillbaka.

## Hur varierar detta för olika affärsmodeller?

För de flesta företag är `lifetime revenue cohort` Analysdiagram visar en stor del av utgifterna under den inledande perioden och ökar sedan långsammare över tiden. Den inledande ökningen beror på att kunderna är mer benägna att göra sina första inköp kort efter att de har förvärvats än vid något annat tillfälle. I de fall där köphändelsen i sig är ett inköp gör 100 % av kunderna ett köp under den första perioden. I de fall där registrering kan ske före köp är den här effekten mindre drastisk.

Som ett exempel [!DNL Groupon] skulle förmodligen ha ett mycket lägre initialhopp än [!DNL Amazon], eftersom många av de som anmäler sig till [!DNL Groupon] gör inte något köp direkt. Om det inte finns ett stort antal återbetalningar kommer det här diagrammet att sakta upp och till höger efter det första hoppet. Tillväxttakten tenderar att minska med tiden eftersom kunderna är mest aktiva när de registrerar sig för första gången. Detta gör att genomsnittet sjunker eftersom antalet personer i kohorten förblir konstant oavsett hur många som kommer tillbaka för att köpa mer. I prenumerationsföretag kommer avmattningen att minska mindre aggressivt än i företag där man gör engångsköp.

Det händer att en prenumerationsverksamhet faktiskt tar lång tid att växa. Det är ovanligt, men det är en bra signal för företaget när det händer. Detta innebär inte att det inte finns några som helst bortfallande kunder, utan att det snarare är uppgraderingar för kunder som behåller mer än att kompensera för kunder som lämnar oss.

## Hur beräknas detta?

Det finns två enkla indata i den här beräkningen: hur många medlemmar som finns i `cohort` (som aldrig ändras), och hur stora intäkter dessa medlemmar genererade under den angivna perioden. Bestämma medlemmarna i `cohort`, räknar du antalet användare som förvärvats under perioden i fråga. Ett förvärv kan vara ett första köp, ett första kontoköp, ett nyhetsbrev eller något annat evenemang. The `revenue` beräkningen är lite mer komplicerad. Du vill summera intäkt för order som lagts av medlemmar i detta `cohort` och ägde rum inom en fast tidsperiod från förvärvstidpunkten (t.ex. de tre första månaderna). Slutligen dividerar du intäkterna med antalet medlemmar i `cohort` för varje tidsperiod i diagrammet och lägg till det här värdet kumulativt över tiden.

## Vilka är variationerna i det här diagrammet?

Det finns många olika typer av användbara `cohort` analyserar. Den vanligaste variationen är [filtrera efter källa för kundvärvning](../analysis/most-value-source-channel.md). Du kanske vill titta på den här tabellen för kunder som kommer från `organic` sökning, `paid` sökning, eller ett närstående program. Detta hjälper er att förstå om kunderna från en förvärvskälla är mer lojala eller värdefulla än andra. Du kan också filtrera efter demografi eller andra användarattribut.

Ett annat sätt att se på data är med ett inkrementellt, snarare än kumulativt, dataperspektiv. Detta visar det stegvisa belopp som en genomsnittlig användare spenderar varje månad efter att de har förvärvats. Detta är användbart när du vill göra en prognos över antalet upprepade köp som du får från befintliga användare. Du kan även se det här med andra saker förutom intäkter. Några exempel inkluderar marginal- och icke-finansiella mätvärden som inbjudningar, röster eller meddelanden.
