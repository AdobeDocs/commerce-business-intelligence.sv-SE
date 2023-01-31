---
title: Använd en rapport
description: Lär dig hur du använder rapportdata.
exl-id: 94d4db27-0e06-4066-9c03-036b109d2d9b
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 0%

---

# Använd en rapport

Använd rapporter i [!DNL MBI] för att hjälpa dig att besvara affärsfrågor - om du bara vill se månadens intäkter jämfört med förra året eller förstå dina anskaffningskostnader för den senaste [!DNL Google AdWords] kampanj.

Hur ser den vägen från fråga till svar ut, exakt?

Vi har kartlagt den vägen nedan för att hjälpa dig att visualisera processen. Det här avsnittet kommer att belysa både hur vi hanterar en analytisk fråga och den backend-logistik som krävs för att du ska få de data du behöver.

## Börja med frågan

Vi vet att ni hela tiden ställer frågor för att förbättra er verksamhet, från att öka kundnöjdheten till att minska leveranskostnaderna. Vi kommer att fokusera på hur du kan översätta dina frågor till analyser som hjälper dig att fatta beslut.

Vi antar till exempel att vi vill svara på följande fråga:

* Hur snabbt konverterar mina nya registranter?

## Identifiera ett mått

Med den fråga vi har till hands är det dags att identifiera en lista med möjliga analyser och mätningar för att besvara frågan. I det här exemplet fokuserar du på följande mått:

* Genomsnittlig tid från registrering till första inköpsdatum per användning.

Detta visar den genomsnittliga tiden mellan registreringsdatumet och användarens första inköpsdatum och ger en uppfattning om hur användarna beter sig i det sista steget i konverteringsprocessen.

## Söka efter data

Att förstå vad vi ska mäta är bara en del av vägen dit. För att utvärdera den genomsnittliga tiden från registrering till första inköpsdatum per användare måste vi identifiera alla datapunkter som vår åtgärd består av.

Dela upp vårt mått i dess kärnkomponenter: vi behöver veta antalet registrerade personer, eller antalet, antalet personer som har köpt något, och tiden mellan dessa två händelser.

På en högre nivå behöver vi veta var vi kan hitta dessa data i databasen, särskilt:

* Tabellen som registrerar en rad med data varje gång någon registrerar
* Tabellen som registrerar en datarad varje gång någon gör ett köp
* Kolumnen som kan användas för att förena eller referera till `purchase` tabellen till `customer` table - this will allow us know who made a purchase

På en mer detaljerad nivå måste vi identifiera de exakta datafält som kommer att användas för denna analys:

* Datatabellen och kolumnen som innehåller en kunds registreringsdatum: till exempel `user.created\_at`
* Datatabellen och kolumnen som innehåller ett inköpsdatum: till exempel `order.created\_at`

## Skapa datakolumner för analys

Utöver de inbyggda datakolumner som beskrivs ovan behöver vi även en uppsättning beräknade datafält för att kunna utföra den här analysen, som:

* `Customer's first purchase date` som returnerar en specifik användares `MIN(order.created_at`)

Den används sedan för att skapa:

* `Time between a customer's registration date and first purchase date`, som returnerar en viss användares tid mellan registreringsdatumet och det första inköpsdatumet. Detta kommer att bli grunden för våra mätvärden senare.

Båda dessa fält måste skapas på användarnivå (till exempel på `user` tabellen), så att genomsnittsanalysen kan normaliseras av användarna (dvs. nämnaren i den här genomsnittliga beräkningen är antalet användare).

Det är här [!DNL MBI] steg in! Du kan använda [!DNL MBI] data warehouse för att skapa kolumnerna ovan. Kontakta bara vårt analysteam och ge oss den specifika definitionen av dina nya kolumner så skapar vi dem. Du kan också utnyttja våra [Kolumnredigeraren](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md).

Det är en god vana att undvika att skapa dessa beräknade datafält direkt i databasen eftersom det medför en onödig börda för produktionsservrarna.

## Skapa måttet

Nu när vi har de datafält som krävs för vår analys är det dags att hitta eller skapa relevanta mätvärden för att skapa vår analys.

Här vet vi att vi matematiskt vill göra följande beräkning:


_[SUMMA `Time between a customer's registration date and first purchase date`] / [Totalt antal kunder som registrerat sig och köpt]_

Och vi vill att beräkningen ska ritas över tiden, eller trendas, enligt kundens registreringsdatum. Så här gör du [skapa det här måttet](../../data-user/reports/ess-manage-data-metrics.md) in [!DNL MBI]:

1. Gå till **[!UICONTROL Data]** och väljer `Metrics` -fliken.
1. Klicka **[!UICONTROL Add New Metric]** och väljer `user` tabell (där vi skapade dimensionerna ovan).
1. Välj `Average` på`Time between a customer's registration date and first purchase date` kolumn i `user` tabellen sorterad efter `Customer's registration date`  kolumn.
1. Lägg till relevanta filter eller filteruppsättningar.

Det här måttet är nu klart.

## Skapa rapporten

Med de nya måtten kan vi använda dem för att rapportera den genomsnittliga tiden mellan registrering och första inköpsdatum per registreringsdatum.

Gå bara till valfri kontrollpanel och [skapa en ny rapport](../../data-user/reports/ess-manage-data-metrics.md) med de mått som skapas ovan.

### `Visual Report Builder` {#visualrb}

[The `Visual Report Builder`](../../data-user/reports/ess-rpt-build-visual.md) är det enklaste sättet att visualisera data. Om du inte är bekant med SQL eller bara vill skapa en rapport snabbt, är Visual Report Builder ditt bästa val. Med bara några klick kan ni lägga till mätvärden, segmentera data och skapa rapporter i hela organisationen. Det här alternativet är perfekt för såväl nybörjare som experter, eftersom det inte kräver någon teknisk expertis.

|  |  |
|--- |--- |
| **Det här är perfekt för..** | **Det här är inte så bra för..** |
| - Alla nivåer av analys/teknikerfarenhet<br>- Skapa rapporter snabbt<br>- Skapa analyser att dela med andra användare | - Analyser som kräver SQL-specifika funktioner<br>- Testa nya kolumner - beräknade kolumner är beroende av uppdateringscykler för den inledande datapifieringen, medan de som skapas med SQL inte är |

{style=&quot;table-layout:auto&quot;}

### Rapportbeskrivningar och bilder

#### Lägga till beskrivningar i rapporter

När du skapar rapporter som ska delas med andra medlemmar i ditt team rekommenderar vi att du lägger till beskrivningar som gör att andra användare kan förstå din analys bättre.

1. Klicka **[!UICONTROL i]** överst i alla rapporter.
1. Ange en beskrivning i ordrutan.
1. Klicka **[!UICONTROL Save Description]**.

Låt oss ta en titt:

![Diagrambeskrivning](../../assets/Chart_Description.gif)

#### Exportera rapporter som bilder

Behöver du ta med en rapport i en presentation eller ett dokument? Alla rapporter kan sparas som en bild (i PNG-, PDF- eller SVG-format) med `Report Options` -menyn som finns i det övre högra hörnet i varje rapport.

1. Klicka på kugghjulsikonen i det övre högra hörnet i en rapport.
1. Välj `Enlarge`.
1. När rapporten förstoras klickar du på **[!UICONTROL Download]** i rapportens övre högra hörn.
1. Välj önskat bildformat i listrutan. Nedladdningen börjar omedelbart.

Ta en titt:

![](../../assets/exp-rep-as-image.gif)
