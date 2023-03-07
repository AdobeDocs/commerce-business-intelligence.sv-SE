---
title: Ordna data med funktionen Visa överkant/nederkant
description: Lär dig hur du beställer data med funktionen Visa överkant/underkant.
exl-id: d47119f4-cdc5-4fa7-a606-d4b8555a8843
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---

# Beställa data med `Show Top/Bottom` funktion

Du kan göra mer i `Visual Report Builder` än att skapa analyser som trendar över tid. Du kan t.ex. skapa en rapport som visar hur värdefulla era förvärv- och marknadsföringskanaler är, men du kan också skapa en rapport som bara visar de fem främsta prestationerna. På samma sätt kan ni fokusera om era marknadsföringssatsningar genom att skapa en rapport som visar vilka lägen som genererar störst intäkter.

Den här sorteringen och sorteringen av data kan göras i rapporter där både en `Group By` och `Time Interval of None`. När båda dessa element finns i en rapport `Show Top/Bottom` visas ovanför förhandsvisningen av diagrammet. Med den här funktionen kan du se de översta (högsta till lägsta) och understa (lägsta till högsta) datapunkterna baserat på de parametrar som du anger.

![Visa över-/underkant-funktionen i Visual Report Builder.](../../assets/Show_Top_Bottom.png)

## Hur använder jag den här? {#how}

När du klickat på **[!UICONTROL Show Top/Bottom link]** visas ett fönster där du kan ange parametrarna för visning och sortering. Talet i textrutan kan vara ett heltal (som `5`) eller `ALL`. Därefter kan du välja att sortera rapporten antingen efter måttet ELLER efter grupperingen.

Om du till exempel vill visa de fem hänvisningskällorna som gav störst intäkter är det så här du gör:

1. Lägg till `Revenue` mätvärden till rapporten.

1. Lägg till en `Group By` för att segmentera mätvärdena efter hänvisningskälla.

1. Ange `Time Interval` till `None`.

1. I `Show Top/Bottom` inställningar, ange att visningen ska `5` så att endast hänvisningskällor med de fem högsta totala intäktsbeloppen inkluderas i rapporten.

>[!NOTE]
>
>Eftersom rapporten inte har en `Time Interval`kan värdena - i det här fallet de fem viktigaste hänvisningskällorna - ändras över tiden. Om en hänvisningskälla överstiger en annan vad gäller intäkter, ändras den ordning i vilken källorna visas.

## Hur är det med att använda flera mätvärden? {#multiplemetrics}

Det blir komplicerat att använda den här funktionen när det finns mer än ett mått i en rapport, eftersom varje mätvärde bara kan sorteras för sig själv eller av en av grupperingarna.

Säg att du har skapat en rapport med båda `Revenue` och `Number of orders` mätvärden, grupperade efter hänvisningskälla. `Revenue` kan bara sorteras efter `Revenue` eller hänvisningskälla och `Number of orders` kan bara sorteras efter `Number of orders` eller hänvisningskälla.

Det innebär att du kan visa `Revenue` endast uppifrån `5` inkomstgenererande hänvisningskällor, du kan inte visa antalet order också efter den översta `5` inkomstgenererande hänvisningskällor. Enkelt uttryckt: när det finns flera mätvärden är det bästa valet att sortera varje mätvärde efter grupperingen.

Nedan visas ett exempel på ett diagram som sorterade `Revenue` själva måttet i stället för av grupperingen. Som du ser har ingen sortering av måtten efter grupperingen skapat en märklig (och i slutändan oanvändbar) rapport:

![Konstiga och ohjälpsamma rapportresultat.](../../assets/strange-report-results.png)

Om du hade sorterat båda måtten efter grupperingen skulle diagrammet se ut så här:

![Sortera båda måtten efter grupperingen.](../../assets/sort-metrics-by-grouping.png)

## Hur sorteras värden som standard? {#defaultsorting}

När endast ett mått ingår i en rapport med en `Group by` och `Time Interval` av `None`, standardordningen i `Visual Report Builder` ska visa de översta värdena baserat på måttet. I den här instansen `Show Top/Bottom` -funktionen är kanske inte nödvändig om det passar dina behov.

I det här exemplet visas hur många möjligheter som säljarna har stängt. Tabellen sorteras automatiskt från högsta till lägsta baserat på måttet, i det här fallet `Won Opportunities`.

![Beställning efter måttet.](../../assets/Ordered_by_metric.png)

När ett andra mätvärde läggs till är standardinställningen att ordningen för det översta baseras på grupperingen. När mätvärden och grupperingar läggs till, baseras standardsorteringen på den första grupperingen, den andra grupperingen och så vidare.

![Sortering efter gruppering.](../../assets/Ordered_by_grouping.png)

## Radbrytning {#wrapup}

Vissa grundläggande funktioner beskrivs här, men den här funktionen har många intressanta användningsområden.

Fundera på föregående säljare och exempel på affärsmöjligheter. Tar bort `Time Interval`, använda `Group By`och sorteringen av data baserat på grupperingen gjorde att vi kunde få en detaljerad bild av varje enskild personals antal vunna möjligheter. Med `Show Top/Bottom` kan vi identifiera vilka som är de främsta prestationerna.
