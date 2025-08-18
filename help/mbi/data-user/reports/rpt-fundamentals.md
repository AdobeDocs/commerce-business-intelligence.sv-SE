---
title: Använd en rapport
description: Lär dig hur du använder rapportdata.
exl-id: 94d4db27-0e06-4066-9c03-036b109d2d9b
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '985'
ht-degree: 0%

---

# Använd en rapport

Använd rapporter i [!DNL Adobe Commerce Intelligence] för att besvara affärsfrågor - vare sig du bara vill se månadens intäkter jämfört med förra året eller förstå dina anskaffningskostnader för din senaste [!DNL Google AdWords]-kampanj.

Hur ser den vägen från fråga till svar ut, exakt?

För att hjälpa dig att visualisera den här processen mappas den vägen nedan. I det här avsnittet beskrivs hur du arbetar med en analytisk fråga och hur backend-logistik som krävs för att få tillgång till de data du behöver.

## Börja med frågan

Ni vet att ni hela tiden ställer frågor för att förbättra er verksamhet, från att öka kundnöjdheten till att minska leveranskostnaderna. Ni fokuserar på hur ni kan översätta era frågor till analyser som hjälper er att fatta beslut.

I det här exemplet antar du att du vill svara på följande fråga:

* Hur snabbt konverterar mina nya registranter?

## Identifiera ett mått

Det är dags att identifiera en lista med möjliga analyser och mått för att besvara frågan. I det här exemplet fokuserar du på följande mått:

* Genomsnittlig tid från registrering till första inköpsdatum per användning.

Detta visar den genomsnittliga tiden som förfaller mellan registreringsdatumet och användarens första inköpsdatum och ger en uppfattning om hur användarna beter sig i det sista steget i konverteringsprocessen.

## Söka efter data

Att förstå vad vi ska mäta är bara en del av vägen dit. Om du vill utvärdera den genomsnittliga tiden från registrering till första inköpsdatum per användare måste du identifiera alla datapunkter som måttet består av.

Dela upp måttet i dess kärnkomponenter. Du måste känna till antalet, eller antalet, personer som har registrerat sig, antalet personer som har gjort ett köp och den tid som förflutit mellan dessa två händelser.

På en högre nivå behöver du veta var du kan hitta dessa data i databasen, speciellt:

* Tabellen som registrerar en rad med data varje gång någon registrerar
* Tabellen som registrerar en datarad som varje gång någon gör ett köp
* Kolumnen som kan användas för att ansluta till eller referera till tabellen `purchase` till tabellen `customer` - det gör att vi kan veta vem som gjorde ett köp

På en mer detaljerad nivå måste du identifiera de exakta datafält som används för den här analysen:

* Datatabellen och kolumnen som innehåller en kunds registreringsdatum, till exempel `user.created\_at`
* Datatabellen och kolumnen som innehåller ett inköpsdatum, till exempel `order.created\_at`

## Skapa datakolumner för analys

Utöver de inbyggda datakolumner som beskrivs ovan behöver du även en uppsättning beräknade datafält för att kunna utföra den här analysen, inklusive:

* `Customer's first purchase date` som returnerar en specifik användares `MIN(order.created_at`)

Det används sedan för att skapa:

* `Time between a customer's registration date and first purchase date`, vilket returnerar en viss användares tid som förflutit mellan registreringen och det första inköpsdatumet. Detta är grunden till mätvärdena senare.

Båda dessa fält måste skapas på användarnivå (till exempel i tabellen `user`). Detta gör att genomsnittsanalysen kan normaliseras av användarna (dvs. nämnaren i denna beräkning är antalet användare).

Det är här [!DNL Commerce Intelligence] steg in! Du kan använda din [!DNL Commerce Intelligence] Data Warehouse för att skapa kolumnerna ovan. Kontakta Adobe analysteam och ge oss en specifik definition av de nya kolumnerna som du ska skapa. Du kan också använda [kolumnredigeraren](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md).

Det är en god vana att undvika att skapa dessa beräknade datafält direkt i databasen eftersom det medför en onödig börda för produktionsservrarna.

## Skapa måttet

Nu när du har de datafält som krävs för analysen är det dags att hitta eller skapa relevanta mätvärden för att skapa din analys.

Här vill du utföra följande beräkning:


_[SUM av `Time between a customer's registration date and first purchase date`] / [Totalt antal kunder som registrerat sig och köpt]_

Och ni vill se den här beräkningen plottad över tid, eller trendmässigt, enligt kundens registreringsdatum. Så här [skapar du det här måttet](../../data-user/reports/ess-manage-data-metrics.md) i [!DNL Commerce Intelligence]:

1. Gå till **[!UICONTROL Data]** och välj fliken `Metrics`.
1. Klicka på **[!UICONTROL Add New Metric]** och markera tabellen `user` (där du skapade dimensionerna ovan).
1. I listrutan väljer du `Average` i kolumnen `Time between a customer's registration date and first purchase date` i tabellen `user` som ordnas av kolumnen `Customer's registration date`.
1. Lägg till relevanta filter eller filteruppsättningar.

Det här måttet är nu klart.

## Skapa rapporten

Med de nya måtten kan du använda dem för att rapportera den genomsnittliga tiden mellan registrering och första inköpsdatum per registreringsdatum.

Gå bara till en kontrollpanel och [skapa en rapport](../../data-user/reports/ess-manage-data-metrics.md) med måttet som skapas ovan.

### `Visual Report Builder` {#visualrb}

[Det `Visual Report Builder`](../../data-user/reports/ess-rpt-build-visual.md) är det enklaste sättet att visualisera dina data. Om du inte känner till SQL eller snabbt vill skapa en rapport är Visual Report Builder det bästa valet. Med bara några klick kan ni lägga till mätvärden, segmentera data och skapa rapporter i hela organisationen. Det här alternativet är perfekt för såväl nybörjare som experter, eftersom det inte kräver någon teknisk expertis.

|  |  |
|--- |--- |
| **Det här är perfekt för..** | **Det här är inte så bra för..** |
| - Alla nivåer av analys/teknisk erfarenhet<br> - Skapa rapporter snabbt<br> - Skapa analyser som kan delas med andra användare | - Analyser som kräver SQL-specifika funktioner <br> - Testar nya kolumner - beräknade kolumner är beroende av uppdateringscykler för den inledande datapifieringen, medan de som skapas med SQL inte är det. |

{style="table-layout:auto"}

### Rapportbeskrivningar och bilder

#### Lägga till beskrivningar i rapporter

När du skapar rapporter som delas med andra medlemmar i ditt team rekommenderar Adobe att du lägger till beskrivningar som ger andra användare en bättre förståelse för din analys.

1. Klicka på **[!UICONTROL i]** överst i en rapport.
1. Ange en beskrivning i ordrutan.
1. Klicka på **[!UICONTROL Save Description]**.

Se nedan:

![Diagrambeskrivning](../../assets/Chart_Description.gif)

#### Exportera rapporter som bilder

Behöver du ta med en rapport i en presentation eller ett dokument? Alla rapporter kan sparas som en bild (i PNG-, PDF- eller SVG-format) med menyn `Report Options` som finns i det övre högra hörnet i varje rapport.

1. Klicka på kugghjulsikonen i det övre högra hörnet i en rapport.
1. Välj `Enlarge` i listrutan.
1. När rapporten förstoras klickar du på **[!UICONTROL Download]** i rapportens övre högra hörn.
1. Välj önskat bildformat i listrutan. Nedladdningen startar omedelbart.

Se nedan:

![](../../assets/exp-rep-as-image.gif)
