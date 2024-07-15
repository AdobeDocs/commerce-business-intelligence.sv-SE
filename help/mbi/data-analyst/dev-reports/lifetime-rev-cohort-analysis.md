---
title: Kohortanalys för livstidsintäkt
description: Utforska kraften i Commerce Intelligence kohortanalys.
exl-id: f2b55745-d364-4ba6-9857-ce9cee05c3ae
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 0%

---

# [!DNL Lifetime Revenue Cohort]-analys

Det finns flera sätt att titta på dina data i [!DNL Adobe Commerce Intelligence], och du vet att tolkning och förståelse är lika viktiga som beräkning och visualisering. Det här avsnittet utforskar kraften i [!DNL Commerce Intelligence] `cohort`-analysen.

## Vad betyder `lifetime revenue cohort`-analys?

Tabellen nedan visar den ackumulerade utgiften per användare under en tidsperiod efter att de har förvärvats. `Cohorts` användare har delats upp efter förvärvsmånad.

Den orange raden ovan visar till exempel genomsnittet för användare som förvärvades i november 2011. Den första datapunkten innebär att de användare som förvärvades i november i genomsnitt tillbringade cirka `$200` den första månaden. Den andra datapunkten innebär att dessa användare i slutet av den andra månaden i genomsnitt hade tillbringat cirka `$240`. Deras genomsnittliga utgifter i månad två var ungefär `$40 (240 - 200)`. De olika linjerna representerar olika kohorter av användare. Den gröna linjen representerar de användare som förvärvades i december och den blå är de användare som förvärvades i oktober.

## Varför är detta viktigt?

Den här typen av `cohort`-analys kan vara användbar för flera olika syften, men den mest omedelbara fördelen är ofta bättre kundvärvningsbeslut. Många företag begränsar sina marknadsföringsutgifter till kanaler som ger lönsamhet på kundens första inköp. Dessa företag betalar för att förvärva kunder via en viss kanal så länge deras genomsnittliga första inköp ger mer `gross margin` än vad de behöver för att förvärva dem.

Problemet med detta tillvägagångssätt är att det ofta leder till en underinvestering i tillväxt. Om era konkurrenter marknadsför baserat på en djupare förståelse för köpbeteenden så växer ni inte. Analysen av `lifetime revenue cohort` hjälper dig att förstå konsekvenserna av att utöka kundförvärvsutgifterna och är ett enkelt sätt att förmedla detta till resten av teamet. Om framtida kunder beter sig som befintliga kunder blir det en förutsägbar återbetalningsperiod om kunderna skaffar sig ett högre CPA. Beroende på företagets kassaställning kan du definiera vilken betalningsperiod du känner dig bekväm med, hitta den relevanta positionen i diagrammet och använda i enlighet med detta.

Du kan också använda den här analysen för att se om du blir bättre på att introducera, engagera och generera intäkter från de användare du köper. Den här `cohort`-analysen är till exempel ett bra sätt att se om en kostnadsfri frakthöjning för nya användare resulterade i upprepade köpare eller engångsköpare som aldrig kommer tillbaka.

## Hur varierar detta för olika affärsmodeller?

För de flesta företag kommer analysdiagrammet `lifetime revenue cohort` att visa en stor utgift under den inledande perioden och sedan öka långsammare över tiden. Den inledande ökningen beror på att kunderna är mer benägna att göra sina första inköp kort efter att de har förvärvats än vid något annat tillfälle. I de fall där köphändelsen i sig är ett inköp gör 100 % av kunderna ett köp under den första perioden. I de fall där registrering kan ske före köp är den här effekten mindre drastisk.

Som ett exempel har [!DNL Groupon] troligtvis ett mycket lägre initialt hopp än [!DNL Amazon], eftersom många av de som registrerar sig för [!DNL Groupon] inte gör något köp direkt. Om det inte finns ett stort antal återbetalningar kommer det här diagrammet att ta ett steg uppåt och åt höger efter det första hoppet. Tillväxttakten tenderar att minska med tiden eftersom kunderna är mest aktiva när de registrerar sig för första gången. Detta gör att genomsnittet sjunker eftersom antalet personer i kohorten förblir konstant oavsett hur många som kommer tillbaka för att köpa mer. I prenumerationsföretag kommer avmattningen att minska mindre aggressivt än i företag där man gör engångsköp.

Det händer att en prenumerationsverksamhet faktiskt tar lång tid att växa. Det är ovanligt, men det är en bra signal för företaget när det händer. Detta innebär inte att det inte finns några som helst bortfallande kunder, utan att det snarare är uppgraderingar för kunder som behåller mer än att kompensera för kunder som lämnar oss.

## Hur beräknas detta?

Det finns två enkla indata i den här beräkningen: hur många medlemmar som finns i `cohort` (som aldrig ändras) och hur mycket intäkter dessa medlemmar genererade under den angivna perioden. Om du vill fastställa medlemmarna i `cohort` räknar du antalet användare som har förvärvats under perioden i fråga. Ett förvärv kan vara ett första köp, ett första kontoköp, ett nyhetsbrev eller något annat evenemang. `revenue`-beräkningen är lite mer komplicerad. Du vill summera intäkten för order som placerats av medlemmar i `cohort` och som ägde rum inom en fast tidsperiod från anskaffningsdatumet (till exempel de första tre månaderna). Slutligen dividerar du intäkten med antalet medlemmar i `cohort` för varje tidsperiod i diagrammet och lägger till det här värdet kumulativt över tiden.

## Vilka är variationerna i det här diagrammet?

Det finns många olika typer av användbara `cohort`-analyser. Den vanligaste variationen är [filtrering efter källa för användarförvärv](../analysis/most-value-source-channel.md). Du kanske vill titta i det här diagrammet efter kunder som kom från `organic`-sökningen, `paid`-sökningen eller ett koncernbolag. Detta hjälper er att förstå om kunderna från en förvärvskälla är mer lojala eller värdefulla än andra. Du kan också filtrera efter demografi eller andra användarattribut.

Ett annat sätt att se på data är med ett inkrementellt, snarare än kumulativt, dataperspektiv. Detta visar det stegvisa belopp som en genomsnittlig användare spenderar varje månad efter att de har förvärvats. Detta är användbart när du vill göra en prognos över antalet upprepade köp som du får från befintliga användare. Du kan även se det här med andra saker förutom intäkter. Några exempel inkluderar marginal- och icke-finansiella mätvärden som inbjudningar, röster eller meddelanden.
