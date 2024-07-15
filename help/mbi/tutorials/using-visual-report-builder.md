---
title: Använda Visual Report Builder
description: Lär dig att analysera data i rapporten under en viss tidsperiod.
exl-id: da97b63d-63f0-4fd6-87e3-4cac49a42acc
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1199'
ht-degree: 0%

---

# Använd [!DNL Visual Report Builder]

Med [[!DNL Visual Report Builder]](../data-user/reports/ess-rpt-build-visual.md) kan du visuellt utforska dina data för att få insikter och hjälpa till att fatta affärsbeslut. I den här självstudiekursen får du hjälp med att skapa en grundläggande rapport.

>[!NOTE]
>
>Om du vill lägga till en rapport på en instrumentpanel behöver du `Standard` [användarbehörigheter](../administrator/user-management/user-management.md) och `Edit` åtkomst till instrumentpanelen.

## Steg 1: Skapa en rapport

Om du vill börja skapa en rapport klickar du på **[!UICONTROL Report Builder]** i sidofältet eller **[!UICONTROL Add Report]** högst upp på en kontrollpanel. Klicka på alternativet **[!UICONTROL Visual Report Builder]** när sidan `Report Builder` visas.

Om du vill redigera en rapport som skapats i [!DNL Visual Report Builder] klickar du på kugghjulsikonen (Alternativ) i det övre högra hörnet av ett diagram och klickar sedan på **[!UICONTROL Edit]**.

## Steg 2: Lägga till mått

Det första steget i att skapa en analys är att välja [måttet ](../data-user/reports/ess-manage-data-metrics.md) som ska analyseras. Även om mätvärdena listas i bokstavsordning som standard kan du också gruppera dem efter tabellen som styr mätvärdena.

Du kan lägga till ytterligare mått när det inledande måttet har valts och täcka över alla mätvärden i en enskild rapport eller utföra multimetriska beräkningar genom att lägga till formler.

## Steg 3: Lägger till `Formulas`

`Formulas` läggs till i rapporter genom att klicka på **[!UICONTROL Add Formula]**, som finns precis ovanför listan med mätvärden i rapporten. I [formelredigeraren](../data-analyst/dev-reports/formulas-in-rpt-bldr.md) kan alla mätvärden som ingår i rapporten användas som indata. Grundläggande matematiska operatorer används för att ändra de olika mätvärdena.

Säg att du vill skapa en rapport som visar de genomsnittliga intäkterna per order. I det här fallet dividerar du `Revenue`-måttet med `Number of orders`-måttet.

![](../assets/ave-rev-per-order.png)

## Steg 4: Ange `Time Period` och `Interval of Analysis` {#time}

Om du vill nollställa en viss tidsrymd kan du ange tidsperioden för analysen. Du kan också välja tidsintervall för att segmentera data (till exempel efter år, kvartal eller månad). Använd menyerna i diagrammets övre högra hörn för att ange tidsperioden och intervallet.

![](../assets/Time_Options_Report_Builder.png)

När du anger ett visst datumintervall för tidsperioden måste du se till att startdatumet är i början av intervallet och att slutdatumet är i slutet av intervallet.

Om du till exempel anger en tidsperiod från `January 1st` till `March 1st` och väljer ett `monthly` intervall visas `March` som en datapunkt, men ignorerar varje dag i `March` förutom `March 1`. I så fall bör du skapa din `Time Period` från `January 1 to March 31`.

## Steg 5: `Group by` / `Segmenting the Analysis` {#groupby}

[Klicka på menyn **[!UICONTROL Group by]** längst upp till vänster i diagrammet om du vill segmentera dina mått med datamått](../best-practices/segment-filter.md). Då visas en listruta med alla tillgängliga mått för det första mätvärdet som finns i listan.

Du kan välja `None` för att förhindra att ett mätvärde segmenteras. Du kanske vill ha ett mått som returnerar totala intäkter utan att segmenteras, samtidigt som ett annat intäktsmått segmenteras efter region.

Gå tillbaka till exempel med genomsnittliga intäkter per order och ställ in Group by för att få kampanjkoden. Här visas den genomsnittliga intäkten per order både med och utan kampanjkod.

![](../assets/Group_By_Report_Builder.png)

Om mätvärdena som ingår i analysen bygger på olika datatabeller kan du välja matchande datamått i varje tabell i ett popup-fönster. Målet här är att hitta dimensioner som delar värdetyper för segmentering:

![](../assets/Dimension_Editor.png)

## Steg 6: Ange `Metric Filters`, `Perspective` och `Time Interval` {#metric-specific}

För varje mätvärde som läggs till i analysen kan du lägga till filter, välja det relevanta dataperspektivet och ange `time interval` alternativ. Klicka på ikonerna för tratt (`Filter`), öga (`Perspective`) och klocka (`Time`) bredvid mätvärdena som ingår i rapporten för att få tillgång till de här funktionerna.

![](../assets/Filters_Perspective_Interval_Report_builder.png)

### `Filters`

`Filters` begränsar datamängden som ingår i analysen. Filter är till exempel användbara när du utvärderar enskilda förvärvskanaler och tar bort avvikande värden.

Förutom listrutemenyer och textrutor kan du även använda speciella filteroperatorer som `LIKE` eller `IN` för att skapa filter.

Användning av jokertecken (`%` eller `_`) med `LIKE`-satser stöds. Jokertecknet `%` matchar flera tecken, medan `_` endast matchar ett tecken. Exempel:

- `affiliate's name Like B%` tillåter bara data från kunder vars namn börjar med `B`.

- `affiliate's name Like _ake` tillåter bara data från kunder vars namn är något som `Jake`, `Rake` eller `Bake`, men inte `Drake` eller `Blake`.

Genom att lägga till flera filter får du noggrann kontroll över diagrammets data. Som standard måste alla filtervillkor vara true för att en datadel ska kunna inkluderas, men du kan skapa ELLER-relationer genom att redigera textrutan Filterregler.

![](../assets/edit-filter-rules.png)

### `Perspectives`

`Perspectives` Gör att du enkelt kan växla mellan olika vyer av dina data. Se vad som finns:

- `Standard perspective`: I standardperspektivet visas resultatet för matchningsdatumet på x-axeln (till exempel intäkten i januari). Det här perspektivet använder du i exemplet med genomsnittlig intäkt per order.

![](../assets/Standard.png)

- `Amount` OR `Percent Change` kontra `Previous Period`-perspektiv: Det här perspektivet visar mängden eller procentförändringen från ett intervall till nästa och är användbart för att mäta ändringshastigheten i snabbföränderliga mått. Det finns också ett perspektiv för att jämföra intervallet med samma tidsperiod förra året för att visa tillväxten år över år.

![](../assets/Amt_or_Percent_Change.png)

- `Cumulative perspective`: `cumulative perspective` visar det pågående eller ackumulerade summeringsbeloppet för mätningen under tidsperioden. Detta används ofta för att analysera totala kunder och planera för framtida kapacitet.

![](../assets/Cumulative_Perspective.png)

- `Percent of First Value perspective`: Det här perspektivet visar data i procent av det första intervallet som ingår i analysen. Detta är användbart vid mätning av effekten av specifika åtgärder i förhållande till den första periodens resultat.

![](../assets/Percent_of_First_Value.png)

- `Rolling averages window perspective`: Fönsterperspektivet för rullande medelvärde visar det rullande medelvärdet för ett mätvärde över det angivna tidsintervallet. Intervallet måste vara detsamma som det intervall som anges på rapportnivån. Om rapporten t.ex. visar det sista hela kvartalet av Intäkter per vecka, kan du ställa in det rullande genomsnittliga tidsintervallet till fyra veckor. Detta gör att de första tre värdena är null och det fjärde värdet representerar genomsnittet för de fyra första veckorna av intäkt. Se till att du stänger av kryssrutan `Multiple Y-Axes` om du visar samma mätvärde med ett rullande medelvärde, som i exemplet nedan.

![](../assets/rolling_avg_window.png)

### Mätningsspecifika tidsalternativ

Det finns två alternativ för mätvärden som används i rapporter: de kan trender över tiden enligt globala tidsalternativ, eller inte, vilket visar dem som ett skalärtal.

Om du ändrar ett tidsintervall för måttet till `None` returneras ett `scalar`-tal, vilket är användbart när du skapar formler som inbegriper att dela ett tidsstyrningsmått med ett `scalar`-tal. Du kan också ändra tidsintervallet för `scalar`-måttet till ett tidsintervall som är oberoende av tidsintervallet för rapporten.

Exempel: 2019 års månadsinkomst uttryckt i procent av de totala intäkterna 2019. Du kan lägga till två `Revenue`-mått i en rapport med det globala tidsintervallet 1 januari 2019 till 31 december 2019, segmenterat efter månadsintervall.

>[!NOTE]
>
>Om du lägger till `group by` dimensioner väljer du en ny visualisering eller justerar tidsintervallet och sparar sedan bara talet (`scalar`). Dessa justeringar behålls inte nästa gång du öppnar rapporten från en kontrollpanel - bara tidsintervallet behålls.

Mer information om hur du använder tidsalternativ i dina rapporter finns i den här [självstudiekursen](../tutorials/time-options-visual-rpt-bldr.md).

## Steg 7: Spara rapporten

När du skapar ett diagram kan du spara det genom att klicka på **[!UICONTROL Save]** i det övre högra hörnet av `Visual Report Builder`.

Du kan välja att spara ett diagram, en tabell eller ett nummer (`scalar`) med listrutan `Type` och kontrollpanelen som rapporten ska sparas på med listrutan `Location`.

Du kan sedan spara rapporten genom att klicka på **[!UICONTROL Save to Dashboard]**.

![](../assets/save-to-dashboard.png)

## Rapportutdata

Här följer information om vilka rapportutdata du ska välja:

### Diagram

![](../assets/RB_Chart.png)

### Tabell

![](../assets/RB_Table.png)

### Nummer (`scalar`)

![](../assets/RB_Scalar.png)

Grattis! Du är färdig.
