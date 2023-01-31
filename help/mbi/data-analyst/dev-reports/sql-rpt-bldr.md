---
title: Använda SQL Report Builder
description: Lär dig In och ut hur du använder SQL Report Builder.
exl-id: 3a485b00-c59d-4bc5-b78b-57e9e92dd9d6
source-git-commit: 09b6983c3e06a1f18035542dfa3b9de9ac3ceb38
workflow-type: tm+mt
source-wordcount: '1516'
ht-degree: 0%

---

# Använda `SQL Report Builder`

>[!NOTE]
>
>Kräver [Administratörsbehörigheter](../../administrator/user-management/user-management.md) för att skapa och redigera SQL-diagram. `Standard` kan användarna ordna om dessa diagram på kontrollpaneler, och `Read-only` användarna får samma upplevelse som de har med traditionella diagram. Dessutom `Read-only` -användare har inte åtkomst till frågetexten.

Se vår [utbildningsvideo](https://support.magento.com/hc/en-us/articles/360016730131) om du vill veta mer.

`SQL`, eller Structured Query Language, är ett programmeringsspråk som används för att kommunicera med databaser. I [!DNL MBI]används SQL för att hämta data från data warehouse. Ta en titt på rapporterna på din instrumentpanel - bakom kulisserna drivs var och en av dem av en SQL-fråga.

Du kan använda [`SQL Report Builder`](../dev-reports/sql-rpt-bldr.md) om du vill fråga data warehouse direkt, visa resultaten och omvandla dem till ett diagram. Du kan börja skapa en rapport med `SQL Report Builder` genom att navigera till **[!UICONTROL Report Builder** > **SQL Report Builder]**.

Se vår [utbildningsvideo](https://support.magento.com/hc/en-us/articles/360016730131-Training-Video-SQL-Report-Builder) om du vill veta mer.

The `SQL Report Builder` Med kan du ställa frågor direkt i data warehouse, visa resultaten och snabbt omvandla dem till ett diagram. Det bästa med att använda SQL för att skapa rapporter är att [du inte behöver vänta på uppdateringscykler för att iterera på kolumner](https://support.magento.com/hc/en-us/articles/360016506212) du skapar. Om resultatet inte blir som du vill kan du snabbt redigera och köra frågan igen tills det matchar dina förväntningar.

I den här artikeln visar vi hur du använder `SQL Report Builder`. När du vet hur du ska gå vidare kan du kolla in vår självstudiekurs om visualiseringar i SQL eller försöka optimera några av de frågor du har skrivit.

Här är en översikt över vad vi beskriver i den här artikeln:

1. [Skriva en fråga](#writing)

1. [Köra frågan och visa resultat](#runquery)

1. [Skapa en visualisering](#createviz)

1. [Sparar rapporten](#save)

## SQL Report Builder-integreringar

I det nuvarande skedet av världen [[!DNL Google Analytics]](../importing-data/integrations/google-analytics.md) är den enda integreringen som inte går att använda med [`SQL Report Builder`](../dev-reports/sql-rpt-bldr.md). Vi arbetar på att ta med den här funktionen i en senare version.

Om du vill börja skapa en ny SQL-rapport klickar du på **[!UICONTROL Report Builder]** eller **[!UICONTROL Add Report]** överst på en kontrollpanel. I `Report Picker` skärm, klicka **[!UICONTROL SQL Report Builder]** för att öppna SQL-redigeraren.

## Kom igång

Om du vill redigera en rapport klickar du på kugghjulet (![](../../assets/gear-icon.png)) i det övre högra hörnet av ett SQL-baserat diagram och klicka på **[!UICONTROL Edit]**.

## Skriva en fråga {#writing}

>[!NOTE]
>
>`SQL Report Builder` frågor är skiftlägeskänsliga. Kontrollera att du använder rätt skiftläge när du skriver frågor, annars kan oväntade resultat eller fel uppstå.

Efter [riktlinjer för frågeoptimering](../../best-practices/optimizing-your-sql-queries.md)skriver du en fråga i SQL-redigeraren.

>[!IMPORTANT]
>
>**Mätvärden i SQL-rapporter** - När du infogar ett mätvärde i en SQL-rapport `current definition` av mätvärdena används.

Om mätvärdena uppdateras i framtiden kommer SQL-rapporten *inte* återspeglar ändringarna. Du måste redigera rapporten manuellt för att ändringarna ska börja gälla.

Med knapparna överst i sidlisten kan du växla mellan listor med tabeller och mätvärden som är tillgängliga för användning i `SQL Report Builder`. Om du inte ser vad du söker i listan kan du söka efter den med hjälp av sökfältet högst upp i sidlisten.

Du kan också använda sidofältet i SQL-redigeraren för att infoga mått, tabeller och kolumner direkt i dina frågor genom att hålla markören över dem och klicka **[!UICONTROL Insert]**:

![Infoga en tabell i SQL-redigeraren.](../../assets/SQL_RB_Insert_Table.png)

>[!NOTE]
>
>Alla [Funktionen SELECT](https://www.postgresql.org/docs/9.5/sql-select.html#SQL-SELECT-LIST), eller en funktion som inte muterar data, som stöds av PostgreSQL, stöds i SQL Report Builder. Detta omfattar, men är inte begränsat till, AVG, COUNT, COUNT DISTINCT, MIN/MAX och SUM.

Dessutom stöds alla JOIN-typer, men vi rekommenderar att du bara använder INNER JOIN eftersom det är den billigaste typen av JOIN.

## Köra frågan och visa resultat {#runquery}

När du är klar med din fråga klickar du på **[!UICONTROL Run Query]**. Resultatet visas i en tabell under SQL-redigeraren:

![Kör frågan och visa resultat.](../../assets/SQL_Run_Query.gif)

Om något verkar saknas i resultatet kan du redigera frågan och köra den igen tills du är nöjd.

Ibland ser du [meddelanden under redigeraren med EXPLAIN i dem](../../best-practices/optimizing-your-sql-queries.md). Om du ser något av detta innebär det att frågan inte har körts och att du behöver finjustera något.

När du är klar med redigeringen av frågan kan du gå vidare till att antingen skapa en visualisering eller spara ditt arbete på en kontrollpanel.

## Skapa en visualisering {#createviz}

Om du vill skapa en visualisering med dina frågeresultat klickar du på **[!UICONTROL Chart]** i `Results` fönster. På den här fliken väljer du:

* The `Series`eller den kolumn som du vill mäta, till exempel **Sålda artiklar**.
* The `Category`eller den kolumn som du vill använda för att segmentera data, till exempel **förvärvskälla**.
* The `Labels`eller X-axelvärden.

Här är en snabb titt på hur visualiseringsprocessen ser ut:

![](../../assets/SQL_RB_viz_overview.gif)

En detaljerad genomgång av hur du skapar en visualisering finns i [Skapa visualiseringar från SQL-frågor, genomgång](../../tutorials/create-visuals-from-sql.md){: target=&quot;_blank&quot;}.

## Sparar rapporten {#save}

Innan du kan spara ditt arbete måste du ge rapporten ett namn. Kom ihåg att följa [riktlinjer för att namnge](../../best-practices/naming-elements.md){: target=&quot;_blank&quot;} och välj något som tydligt anger vad rapporten är!

Klicka **[!UICONTROL Save]** längst upp till höger i SQL-redigeraren och välj rapporten `Type` (`Chart` eller `Table`). Om du vill slå ihop allt markerar du kontrollpanelen för att spara rapporten och klickar på **[!UICONTROL Save to Dashboard]**.

![](../../assets/SQL_Save_Report.gif)

### Analysera dina data

#### `SQL Report Builder`

[`The SQL Report Builder`](../dev-reports/sql-rpt-bldr.md) ger er möjlighet att ställa frågor direkt till data warehouse, se resultaten och snabbt omvandla dem till en rapport. Om du använder SQL kan du [för att använda SQL-funktioner som inte är tillgängliga](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html) i `Visual` eller `Cohort` Report Builder, vilket ger er större kontroll över era data.

Vi vill nämna att beräknade kolumner som skapats med SQL inte är beroende av uppdateringscykler, vilket innebär att du kan upprepa dem som du vill och omedelbart se resultaten.

>[!NOTE]
>
>Detta gäller endast kolumnstrukturen, inte datans aktualitet. Uppdateringsdata är fortfarande beroende av slutförda uppdateringscykler.

| **Det här är perfekt för..** | **Det här är inte så bra för..** |
|---|---|
| Intermediala/avancerade analytiker | Nybörjare - du måste kunna SQL. |
| SQL-kunnighet | Enkla analyser - att skriva en fråga kan vara mer användbart än att bara använda Visual Report Builder. |
| Skapa engångskalkylerade kolumner | Dela med andra - tänk på er målgrupp: Förstår de SQL? Om de inte gör det kan de bli förvirrade av hur rapporten byggs. |
| Data med `one-to-many` relationer |  |
| Testa en ny kolumn eller analys |  |

#### Resultat för databas jämfört med SQL Editor

Större delen av tiden kan skillnader i resultat tillskrivas uppdateringscykler. If [!DNL MBI] är på väg att replikera data från databasen till Data warehouse, kan du se olika resultat även om du använder samma fråga.

Anslutningsproblem kan också leda till avvikelser. Navigera till `Connections` sida genom att klicka **[!DNL Manage Data** > **Connections]**) för att ta reda på det - finns det ett fel för databasintegreringen i fråga? I så fall kan du behöva [autentisera integreringen igen](https://support.magento.com/hc/en-us/articles/360016733151-Reauthenticating-integrations) för att få igång saker och ting igen.

Om alla integreringar har anslutits och du inte befinner dig mitt i en uppdateringscykel kan något annat vara fel. Prova att använda [felsökningsguider för diskrepans](https://support.magento.com/hc/en-us/sections/360003074492) på vår supportwebbplats för att identifiera problemet.

#### Om du tar bort en SQL-rapport tas även de underliggande kolumnerna bort från Data warehouse?

Nej, du kommer inte att förlora några kolumner från Data warehouse, oavsett hur du har skapat dem.

Kolumner som skapats med `Data Warehouse Manager` påverkas inte om du tar bort en rapport eller fråga som använder dem.

Kolumner som skapats med `SQL Report Builder` sparas inte i Data warehouse.


#### `Report Builder` kontra `SQL Report Builder`

The `SQL Report Builder` ger dig större flexibilitet när du skapar och strukturerar diagram - du kan till exempel välja vilka värden som ska visas på `X` och `Y` axlar. Mer information om att skapa diagram finns i `SQL Report Builder`, se vår [Skapa visualiseringar från SQL-frågor](../../tutorials/create-visuals-from-sql.md) självstudiekurs.

#### `Cohort Report Builder` {#cohortrb}

Till skillnad från `Visual Report Builder`, [`Cohort Report Builder`](../dev-reports/cohort-rpt-bldr.md) är avsett för ett enda ändamål - att analysera och identifiera beteendetrender för liknande användargrupper över tiden. Om du använder Kohort Report Builder behöver du inte vara SQL-kunnig, så du kan dyka rakt in utan tvekan om du precis har börjat.

| **Det här är perfekt för..** | **Det här är inte så bra för..** |
|---|---|
| Intermediala/avancerade analytiker | Nybörjare - du behöver träna att definiera kohorter. |
| Identifiera beteendetrender över tid | Kvalitativ analys - den kan [klart](../dev-reports/create-qual-cohort-analysis.md), men behöver vår hjälp. |

## Återskapa frågor efter uppdateringscykeln

Du behöver inte återskapa dina frågor. Rapporter skapade med [`SQL Report Builder`](../dev-reports/sql-rpt-bldr.md) sparas på samma sätt som i traditionell `Report Builder`. Uppdateringsprocessen för SQL-diagram är exakt densamma - när data har uppdaterats beräknas och visas värdena i diagrammen på nytt.

>[!NOTE]
>
>När du tar bort en SQL-rapport eller -fråga tas de underliggande kolumnerna inte bort från Data warehouse. Du kommer inte att förlora några kolumner, oavsett hur du har skapat dem.

* Kolumner som skapas med hjälp av Data warehouse Manager påverkas inte om du tar bort en rapport eller fråga som använder dem.

* Kolumner som skapas med SQL Report Builder sparas inte i Data warehouse.

## Radbrytning {#wrapup}

Om du vill prova något mer utmanande, varför inte skriva en fråga som är optimerad för visualisering? Kolla in vår [Skapa visualiseringar från SQL-frågor, genomgång](../../tutorials/create-visuals-from-sql.md){: target=&quot;_blank&quot;} för att komma igång.
