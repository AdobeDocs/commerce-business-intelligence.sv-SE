---
title: Använda Visual Report Builder
description: Lär dig att analysera data i rapporten under en viss tidsperiod.
exl-id: da97b63d-63f0-4fd6-87e3-4cac49a42acc
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 0%

---

# Använd [!DNL Visual Report Builder]

The [[!DNL Visual Report Builder]](../data-user/reports/ess-rpt-build-visual.md) gör att ni kan utforska era data visuellt för att få insikter och fatta affärsbeslut. I den här självstudiekursen får du hjälp med att skapa en grundläggande rapport.

>[!NOTE]
>
>Om du vill lägga till en rapport på en kontrollpanel måste du `Standard` [användarbehörigheter](../administrator/user-management/user-management.md) och `Edit` åtkomst till kontrollpanelen.

## Steg 1: Skapa en rapport

Om du vill börja skapa en rapport klickar du på **[!UICONTROL Report Builder]** på sidlisten eller **[!UICONTROL Add Report]** överst på en kontrollpanel. När `Report Builder` visas klickar du på **[!UICONTROL Visual Report Builder]** alternativ.

Redigera en rapport som skapats i [!DNL Visual Report Builder], klicka på kugghjulsikonen (Alternativ) i det övre högra hörnet av ett diagram och klicka sedan på **[!UICONTROL Edit]**.

## Steg 2: Lägga till mått

Det första steget för att skapa en analys är att välja [måttet](../data-user/reports/ess-manage-data-metrics.md) att analysera. Även om mätvärdena listas i bokstavsordning som standard kan du också gruppera dem efter tabellen som styr mätvärdena.

Du kan lägga till ytterligare mått när det inledande måttet har valts och täcka över alla mätvärden i en enskild rapport eller utföra multimetriska beräkningar genom att lägga till formler.

## Steg 3: Lägga till `Formulas`

`Formulas` läggs till i rapporter genom att klicka **[!UICONTROL Add Formula]**, placerad alldeles ovanför listan med mätvärden i rapporten. I [formelredigerare](../data-analyst/dev-reports/formulas-in-rpt-bldr.md), kan alla mätvärden som ingår i rapporten användas som indata. Grundläggande matematiska operatorer används för att ändra de olika mätvärdena.

Säg att du vill skapa en rapport som visar de genomsnittliga intäkterna per order. I det här fallet delar du upp `Revenue` mått efter `Number of orders` mätvärden.

![](../assets/ave-rev-per-order.png)

## Steg 4: Ange `Time Period` och `Interval of Analysis` {#time}

Om du vill nollställa en viss tidsrymd kan du ange tidsperioden för analysen. Du kan också välja tidsintervall för att segmentera data (till exempel efter år, kvartal eller månad). Använd menyerna i diagrammets övre högra hörn för att ange tidsperioden och intervallet.

![](../assets/Time_Options_Report_Builder.png)

När du anger ett visst datumintervall för tidsperioden måste du se till att startdatumet är i början av intervallet och att slutdatumet är i slutet av intervallet.

Du kan till exempel ange en tidsperiod från `January 1st` till `March 1st` och välja `monthly` intervallvisning `March` som en datapunkt, men ignorera varje dag i `March` utom `March 1`. I så fall bör du `Time Period` från `January 1 to March 31`.

## Steg 5: `Group by` / `Segmenting the Analysis` {#groupby}

[Segmentera mätvärden efter datamängd](../best-practices/segment-filter.md)klickar du på **[!UICONTROL Group by]** längst upp till vänster i diagrammet. Då visas en listruta med alla tillgängliga mått för det första mätvärdet som finns i listan.

Du kan `None` för att förhindra att ett mätvärde segmenteras. Du kanske vill ha ett mått som returnerar totala intäkter utan att segmenteras, samtidigt som ett annat intäktsmått segmenteras efter region.

Gå tillbaka till exempel med genomsnittliga intäkter per order och ställ in Group by för att få kampanjkoden. Här visas den genomsnittliga intäkten per order både med och utan kampanjkod.

![](../assets/Group_By_Report_Builder.png)

Om mätvärdena som ingår i analysen bygger på olika datatabeller kan du välja matchande datamått i varje tabell i ett popup-fönster. Målet här är att hitta dimensioner som delar värdetyper för segmentering:

![](../assets/Dimension_Editor.png)

## Steg 6: Inställning `Metric Filters`, `Perspective`och `Time Interval` {#metric-specific}

För varje mätvärde som läggs till i analysen kan du lägga till filter, välja det relevanta dataperspektivet och ange `time interval` alternativ. Klicka på tratten (`Filter`), öga (`Perspective`), och klocka (`Time`) ikoner som finns bredvid mätvärdena i rapporten.

![](../assets/Filters_Perspective_Interval_Report_builder.png)

### `Filters`

`Filters` begränsa den datamängd som ingår i analysen. Filter är till exempel användbara när du utvärderar enskilda förvärvskanaler och tar bort avvikande värden.

Förutom listrutorna och textrutan kan du även använda speciella filteroperatorer som `LIKE` eller `IN` för att skapa filter.

Användning av jokertecken (`%` eller `_`) med `LIKE` -programsatser stöds. The `%` jokertecknet matchar flera tecken, medan `_` matchar endast ett tecken. Exempel:

- `affiliate's name Like B%` endast tillåter data från kunder vars namn börjar med `B`.

- `affiliate's name Like _ake` tillåter bara data från kunder vars namn är något som `Jake`, `Rake`, eller `Bake` men inte `Drake` eller `Blake`.

Genom att lägga till flera filter får du noggrann kontroll över diagrammets data. Som standard måste alla filtervillkor vara true för att en datadel ska kunna inkluderas, men du kan skapa ELLER-relationer genom att redigera textrutan Filterregler.

![](../assets/edit-filter-rules.png)

### `Perspectives`

`Perspectives` Gör att du enkelt kan växla mellan olika vyer av dina data. Se vad som finns:

- `Standard perspective`: I standardperspektivet visas resultatet för matchningsdatumet på x-axeln (till exempel intäkter i januari). Det här perspektivet använder du i exemplet med genomsnittlig intäkt per order.

![](../assets/Standard.png)

- `Amount` ELLER `Percent Change` kontra `Previous Period` perspektiv: Det här perspektivet visar hur mycket eller hur många procent som ändras från ett intervall till nästa och är användbart för att mäta förändringshastigheten i snabbföränderliga mätvärden. Det finns också ett perspektiv för att jämföra intervallet med samma tidsperiod förra året för att visa tillväxten år över år.

![](../assets/Amt_or_Percent_Change.png)

- `Cumulative perspective`: `cumulative perspective` visar det pågående eller ackumulerade summeringsbeloppet för mätningen under tidsperioden. Detta används ofta för att analysera totala kunder och planera för framtida kapacitet.

![](../assets/Cumulative_Perspective.png)

- `Percent of First Value perspective`: Detta perspektiv visar data i procent av det första intervallet som ingår i analysen. Detta är användbart vid mätning av effekten av specifika åtgärder i förhållande till den första periodens resultat.

![](../assets/Percent_of_First_Value.png)

- `Rolling averages window perspective`: Fönsterperspektivet för rullande medelvärden visar det rullande medelvärdet för ett mätvärde över det angivna tidsintervallet. Intervallet måste vara detsamma som det intervall som anges på rapportnivån. Om rapporten t.ex. visar det sista hela kvartalet av Intäkter per vecka, kan du ställa in det rullande genomsnittliga tidsintervallet till fyra veckor. Detta gör att de första tre värdena är null och det fjärde värdet representerar genomsnittet för de fyra första veckorna av intäkt. Se till att du stänger av `Multiple Y-Axes` om du visar samma mätvärde med ett rullande medelvärde, som i exemplet nedan.

![](../assets/rolling_avg_window.png)

### Mätningsspecifika tidsalternativ

Det finns två alternativ för mätvärden som används i rapporter: de kan trender över tiden enligt globala tidsalternativ, eller inte, vilket visar dem som ett skalärtal.

Ändra ett tidsintervall för mätning till `None` returnerar `scalar` tal, vilket är användbart när du skapar formler som innebär att ett tidstrendningsmått delas med ett `scalar` tal. Du kan också ändra tidsintervallet för `scalar` mätvärden till ett tidsintervall som är oberoende av rapportens tidsintervall.

Exempel: 2019 års månadsinkomst uttryckt i procent av de totala intäkterna 2019. Du kan lägga till två `Revenue` mätvärden till en rapport med ett globalt tidsintervall från 1 januari 2019 till 31 december 2019, segmenterade efter månadsintervall.

>[!NOTE]
>
>Om du lägger till `group by` mått, välj en ny visualisering eller justera tidsintervallet och spara sedan bara talet (`scalar`). Dessa justeringar behålls inte nästa gång du öppnar rapporten från en kontrollpanel - bara tidsintervallet behålls.

Om du vill veta mer om hur du använder tidsalternativ i dina rapporter kan du läsa detta [självstudiekurs](../tutorials/time-options-visual-rpt-bldr.md).

## Steg 7: Spara rapporten

När du skapar ett diagram kan du spara det genom att klicka på **[!UICONTROL Save]** i det övre högra hörnet av `Visual Report Builder`.

Du kan välja att spara ett diagram, en tabell eller en siffra (`scalar`) med `Type` listrutan och kontrollpanelen som rapporten ska sparas på med `Location` nedrullningsbar meny.

Du kan sedan spara rapporten genom att klicka på **[!UICONTROL Save to Dashboard]**.

![](../assets/save-to-dashboard.png)

## Rapportutdata

Här följer information om vilka rapportutdata du ska välja:

### Diagram

![](../assets/RB_Chart.png)

### Tabell

![](../assets/RB_Table.png)

### Tal (`scalar`)

![](../assets/RB_Scalar.png)

Grattis! Du är färdig.
