---
title: Visualiseringsalternativ i Visual Report Builder
description: Lär dig hur du använder visualiseringsalternativen i Report Builder.
exl-id: e42a004e-28e3-4484-bb5a-b58c810b23e0
source-git-commit: df81d2b036d00cd53274ec1ae22031dbf06cc948
workflow-type: tm+mt
source-wordcount: '1533'
ht-degree: 0%

---

# Visualiseringsalternativ

Att välja rätt visualisering för en viss datauppsättning är en viktig del av analysprocessen. Alla datauppsättningar har en historia att berätta, men effekten av den berättelsen framhävs av dess visuella påverkan och läsbarhet.

The [!DNL Commerce Intelligence] [!DNL Visual Report Builder] har 12 olika visualiseringsalternativ, vart och ett med sina egna fördelar och användningsfall. I det här avsnittet beskrivs de olika visualiseringsalternativen i [!DNL Commerce Intelligence], inklusive nödvändiga rapportkonfigurationer när det är tillämpligt, och ett exempel på ett användningsfall. Följande visualiseringar är tillgängliga i [!DNL Commerce Intelligence]:

* `Scalar`
* `Table`
* `Line`
* `Bar`
* `Stacked Bar`
* `Column`
* `Stacked Column`
* `Pie`
* `Area`
* `Funnel`
* `Scatter plot`
* `Bubble`
* `Heatmap`

## `Scalar`

`Scalar` -rapporter visas som ett numeriskt värde. Oftast används detta för att visa&quot;heltidsvärdet&quot; för ett nyckeltal som intäkt eller order, eller för att jämföra intäkt hittills jämfört med budget med två separata skalära rapporter. I exemplet nedan visar detta helt enkelt det totala antalet order för det angivna rapporteringsintervallet:

![](../../assets/blobid0.png)

Om du vill spara en rapport som en skalär konfigurerar du dina filter och tidsinställningar och klickar sedan på **[!UICONTROL Save]** eller **[!UICONTROL Update]** i rapportens övre högra del. Under `Type` väljer du Nummer: Måttnamn för att spara rapporten som det värde som visas på vänster sida.

![](../../assets/blobid1.png)

**Krav**:

* `Time interval`: `None`
* `Group by`: `None`
* Endast ett mått

## `Table`

Som namnet antyder, `table` -rapporter passar bra för att visa tabelldetaljer. När det finns ett behov av att visa många grupper utifrån värden eller mätvärden i en enda rapport är en tabell ofta det bästa sättet att gå. Nedan finns en tabell med&quot;Kundinformation&quot; som visar order och intäkter grupperade efter kundens e-postadress:

![](../../assets/blobid2.png)

Precis som för skalära rapporter kan du spara en rapport som en tabell genom att klicka på **[!UICONTROL Save]** eller **[!UICONTROL Update]** i Report Builder och sedan väljer du alternativet Table under `Type` listruta.

![](../../assets/blobid3.png)

**Krav:**

* Även om det inte finns några krav på rapportkonfiguration är det viktigt att tänka på att tabeller är begränsade till 3 500 rader. Om datauppsättningen innehåller fler än 3 500 rader måste du antingen filtrera resultaten för att begränsa omfånget eller exportera resultaten till `.csv` eller `Excel` för att se hela datauppsättningen.

## `Line`

`Line` diagram är det perfekta valet för att jämföra prestanda hos liknande metriska kohorter. Analysera till exempel intäkterna för två regioner under samma tidsperiod eller jämföra årstillväxt för fullgjorda order enligt nedan:

![](../../assets/blobid0.png)

Varje mätvärde och formel som läggs till i rapporten representeras av en egen rad. När du jämför mätvärden med liknande enheter och skalor ska du inte glömma bort att avmarkera kryssrutan för `Multiple Y-Axes` om du vill visa alla mätvärden på samma skala.

Om du vill spara en rapport som ett linjediagram justerar du rapporten `Type` till `Chart`och välj lämplig visualisering i Report Builder enligt nedan:

![](../../assets/blobid1.png)

**Krav:**

* Ingen

## `Bar`

`Bar` diagram visar dina data som en serie vågräta staplar och är bäst för att visa övergripande prestanda för ett begränsat antal mätvärden eller gruppera efter värden. Ett stapeldiagram kan till exempel användas för att jämföra intäkten per butik:

![](../../assets/blobid2.png)

Alla distinkta mått, grupperade efter och tidsintervallkombinationer visas som en egen stapel. Om du har två mätvärden med en `group by`, med tre distinkta `group by` värden visar rapporten sex separata fält.

Om du vill spara en rapport som ett stapeldiagram justerar du rapporten `Type` till `Chart` och väljer `Bar` enligt nedan:

![](../../assets/blobid3.png)

**Krav:**

* Ingen

## `Stacked Bar`

`Stacked bar` diagrammen liknar stapeldiagrammets bröder, med möjlighet att visa den proportionella uppdelningen av varje stapel. Oftast skapas staplade stapeldiagram med två eller flera mätvärden och en grupp per, så att varje stapel representerar en unik grupp efter värde som delas mellan de olika måtten.

Rapporten nedan innehåller till exempel två identiska intäktsmått med en filtrerad order för första gången och den andra filtrerad för upprepade order. När du har grupperat efter butik kan du se både det totala intäktsbidraget för varje butik (som representeras av den totala bredden på stapeln) och första gången, jämfört med en upprepad intäktsfördelning för varje butik.

![](../../assets/blobid4.png)

Se till att `Multiple Y-Axes` är avmarkerad när du skapar en rapport som den ovan.

Om du vill spara en rapport som ett staplat stapeldiagram justerar du rapporten `Type` till `Chart` och välj alternativet för staplade fält i Report Builder:

![](../../assets/blobid5.png)

**Krav:**

* Ingen

## `Column`

`Column` diagram representerar varje datapunkt som en lodrät kolumn, och är bättre för att visa tidsstyrda data än för det vågräta stapeldiagrammet. Varje unik mätmetod och gruppera efter kombination representeras i en egen serie med staplar. En kolumnrapport är bäst för rapporter med tre eller färre värden eller ett mått med en enda grupp genom att innehålla 1-3 grupper med värden.

I exemplet nedan ser du två intäktsmått, en filtrerad för första gången och den andra för upprepade intäkter, som trendar över tid per månad:

![](../../assets/blobid6.png)

Du kan spara kolumnrapporter genom att ändra rapporten `Type` till `Chart`och välja alternativet för kolumnvisualisering:

![](../../assets/blobid7.png)

**Krav:**

* Ingen

## `Stacked Column`

`Stacked column` -rapporter är nästan identiska med kolumndiagram, förutom att liknande kolumner staplas ovanpå varandra så att den totala höjden representerar summan av värdena. Staplade kolumner är ännu bättre visualiserade med ett begränsat antal mätvärden eller gruppbyte.

Använda samma rapportkonfiguration som beskrivs i `Column` ovan skulle en rapport med två intäktsmått (filtrerad för första gången och upprepad) se ut som nedan med en staplad kolumnvisualisering:

![](../../assets/blobid8.png)

Det är viktigt att `Multiple Y-Axes` kryssrutan är avmarkerad när flera mätvärden visas med den staplade kolumnvisualiseringen.

Om du vill spara en rapport som en staplad kolumn anger du rapporten `Type` till `Chart` och väljer `stacked column` alternativ:

![](../../assets/blobid9.png)

**Krav:**

* Ingen

## `Pie`

`Pie` diagram är bäst för att visa ett enskilt mått med en eller flera gruppbyte, eller flera mått utan gruppbyte. I båda fallen måste tidsintervallet anges till ingen för att data ska kunna visas i ett cirkeldiagram. I exemplet nedan är ett enskilt ordermått en grupp efter butiksnamn för att visa uppdelningen av order efter butik:

![](../../assets/blobid10.png)

Om du vill spara en rapport som ett cirkeldiagram anger du rapporten `Type` till `Chart` och väljer `pie` enligt nedan:

![](../../assets/blobid11.png)

**Krav:**

* `Time interval`: `None`
* Något av följande:
   * `Single metric with one or more group bys`
   * `Multiple metrics with no group bys`

## `Area`

`Area` diagram är nästan identiska med staplade stapeldiagram, förutom att kolumnerna visas kontinuerligt. Precis som staplade kolumner är ytdiagram bäst att visualisera med ett begränsat antal gruppbyte eller mätvärden.

Ta samma exempel från `stacked column` i rapporten nedan visas första gången jämfört med upprepade intäkter med hjälp av ytdiagramsvisualisering:

![](../../assets/blobid12.png)

Om du vill spara en rapport som ett ytdiagram justerar du `Type` till `Chart` och välj områdesalternativ:

![](../../assets/blobid13.png)

**Krav:**

* Ingen

## `Funnel`

`Funnel` diagram är perfekta för att visualisera konverteringar i en förväntad händelsesekvens. Ett par exempel är att analysera de potentiella intäkterna i säljprocessen från lead till sluten affär eller mäta nedgången i kunder mellan första och andra ordern, andra och tredje ordern osv. Ett exempel på det senare visas nedan:

![](../../assets/blobid4.png)

I en trattrapport återspeglas det relativa värdet för ett visst steg i tratten av stegets höjd. Rapportkonfigurationen avgör i vilken ordning stegen visas. Det finns två sätt att konfigurera en trattrapport:

* `Single metric with one group by`: - Stegen bestäms av inställningen &quot;Visa överkant/underkant&quot; för gruppen efter. Som standard visas trattsteg i ordning från det största till det minsta värdet, men du kan också sortera dem i bokstavsordning efter gruppens namn.

* `Multiple metrics with no group by`: - Stegen i den ordning som måtten läggs till i rapporten.

Om du vill spara en rapport som ett trattdiagram justerar du rapporten `Type` till `Chart` och välj lämplig visualisering i Report Builder.

![](../../assets/blobid5.png)

**Krav:**

* `Time interval`: `None`
* Något av följande:
   * `Single metric with one group by`
   * `Multiple metrics with no group by`

## `Scatter plot`

A `scatter plot` används för att undersöka en metods relation till två olika variabler så att du enkelt kan identifiera relationer och avvikelser. Den här typen av visualisering används bäst med numeriska dimensioner - prova den med ordermåttet och `Customer's lifetime number of coupons` och `Customer's lifetime revenue` dimensioner för att se hur kuponganvändningen är relaterad till intäkten. Du kan välja mellan en punktdiagram med och utan trendlinje:

![](../../assets/scatter-plot-1.png)

![utan trendlinje](../../assets/scatter-plot-2.png)

![](../../assets/scatter-plot-3.png)

![Med trendlinje](../../assets/scatter-plot-4.png)

**Krav:**

Alternativ 1:

* Två `metrics`
* Ett `group by`
* `Time interval`: `None`

Alternativ 2:

* Två `metrics`
* Nej `group by`
* Ange `time interval`

## `Bubble` diagram

A `bubble` kan visa upp till fyra dimensioner av data där `X` och `Y` axlarna anger placeringen av bubblorna. The `Z` är storleken på bubblorna, och genom att ta med två grupper kan du lägga till färg i bubblorna. Den här typen av visualisering används bäst när du vill rita upp flera datamängder i ett enda diagram.

I följande diagram visas antalet kunder (bubbelstorlek) grupperade efter en specifik anskaffningskälla (bubbelfärg) och tillstånd (olika bubblor i en viss färg), plottade mot total intäkt och genomsnittlig livstid.

![](../../assets/bubble-1.png)

Följande diagram visar antalet kunder (bubbelstorlek) grupperade efter anskaffningskälla (bubbelfärg) och tillstånd (olika bubblor i en viss färg), plottade mot genomsnittligt livstidsvärde och totala intäkter.

![](../../assets/bubble-2.png)

**Krav för bubbeldiagram i en serie:**

Alternativ 1

* Tre `metrics`
* Ett `group by`
* `Time interval`: `None`

Alternativ 2

* Tre `metrics`
* Nej `group by`
* Ange `time interval`

**Krav för bubbeldiagram i flera serier:**

* Tre `metrics`
* Två `group by`
* `Time interval`: `None`

## `Heatmap`

Använd `heatmaps` för att visualisera aktiveringspunkter i dina data. En heatmap kan t.ex. visa var du regelbundet får högre volym. Genom att visualisera dessa data kan du justera lagernivåerna så att du kan tillgodose efterfrågan under dessa toppfönster.

Följande värmekarta visar order per veckodag per timma av dagen i aggregat, över flera veckor.

![](../../assets/heat-map.png)<!--{: width="650"}-->

**Krav:**

Alternativ 1

* Ett `metric`
* Två `group by`
* `Time interval`: `None`

Alternativ 2

* Ett `metric`
* Ett `group by`
* Ange `time interval`
