---
title: Använda SQL Report Builder
description: Lär dig In och ut hur du använder SQL Report Builder.
exl-id: 3a485b00-c59d-4bc5-b78b-57e9e92dd9d6
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '1413'
ht-degree: 0%

---

# Använda [!DNL SQL Report Builder]

>[!NOTE]
>
>Kräver [Administratörsbehörigheter](../../administrator/user-management/user-management.md) för att skapa och redigera SQL-diagram. `Standard` kan användarna ordna om dessa diagram på kontrollpaneler, och `Read-only` användarna har samma upplevelse som de har av traditionella diagram. Dessutom `Read-only` -användare har inte åtkomst till frågetexten.

Se [utbildningsvideo](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html) om du vill veta mer.

[!DNL SQL], eller Structured Query Language, är ett programmeringsspråk som används för att kommunicera med databaser. I [!DNL Commerce Intelligence], [!DNL SQL] används för att fråga efter eller hämta data från Data warehouse. Titta på rapporterna på din instrumentpanel - bakom kulisserna drivs var och en av dem av en [!DNL SQL] fråga.

Du kan använda [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) om du vill fråga Data warehouse direkt, visa resultaten och omvandla dem till ett diagram. Du kan börja skapa en rapport med [!DNL SQL Report Builder] genom att klicka **[!UICONTROL Report Builder** > **[!DNL SQL Report Builder]]**.

Se [utbildningsvideo](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html) om du vill veta mer.

The [!DNL SQL Report Builder] Med kan du ställa frågor direkt i Data warehouse, visa resultaten och snabbt omvandla dem till ett diagram. Det bästa med att använda [!DNL SQL] att skapa rapporter är att du inte behöver vänta på uppdateringscykler för att iterera på kolumner som du skapar. Om resultatet inte ser bra ut kan du snabbt redigera och köra frågan igen tills det matchar dina förväntningar.

I det här avsnittet får du hjälp med att använda [!DNL SQL Report Builder]. När du vet hur du ska gå, se [!DNL SQL] för visualiseringar, självstudiekurs eller prova att optimera några av de frågor du har skrivit.

I den här artikeln:

1. [Skriva en fråga](#writing)

1. [Köra frågan och visa resultat](#runquery)

1. [Skapa en visualisering](#createviz)

1. [Sparar rapporten](#save)

## [!DNL SQL Report Builder] Integreringar

[[!DNL Google Analytics]](../importing-data/integrations/google-analytics.md) är den enda integreringen som inte går att använda med [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md). Den här funktionen är under utveckling.

Så här kommer du igång med att skapa en [!DNL SQL] rapport, klicka på **[!UICONTROL Report Builder]** eller **[!UICONTROL Add Report]** överst på en kontrollpanel. I [!DNL Report Picker] skärm, klicka **[!UICONTROL SQL Report Builder]** för att öppna [!DNL SQL] redigerare.

## Kom igång

Om du vill redigera en rapport klickar du på kugghjulet (![](../../assets/gear-icon.png)) i det övre högra hörnet av ett [!DNL SQL]-baserat diagram och klicka **[!UICONTROL Edit]**.

## Skriva en fråga {#writing}

>[!NOTE]
>
>[!DNL SQL Report Builder] frågor är skiftlägeskänsliga. Kontrollera att du använder rätt skiftläge när du skriver frågor, annars kan oväntade resultat eller fel uppstå.

Efter [riktlinjer för frågeoptimering](../../best-practices/optimizing-your-sql-queries.md), skriver du en fråga i [!DNL SQL] redigerare.

>[!IMPORTANT]
>
>**Mätvärden i [!DNL SQL] rapporter** - När du infogar ett mätvärde i en SQL-rapport `current definition` av måttet används.

Om mätvärdena uppdateras i framtiden kommer SQL-rapporten *inte* återspeglar ändringarna. Du måste redigera rapporten manuellt för att ändringarna ska börja gälla.

Med knapparna överst i sidlisten kan du växla mellan listor med tabeller och mätvärden som är tillgängliga för användning i [!DNL SQL Report Builder]. Om du inte ser vad du söker i listan kan du söka efter den med hjälp av sökfältet högst upp i sidlisten.

Du kan också använda sidlisten i dialogrutan [!DNL SQL] redigerare som infogar mått, tabeller och kolumner direkt i frågorna genom att hålla markören över dem och klicka **[!UICONTROL Insert]**:

![Infoga en tabell i [!DNL SQL] redigerare.](../../assets/SQL_RB_Insert_Table.png)

>[!NOTE]
>
>Alla [Funktionen SELECT](https://www.postgresql.org/docs/9.5/sql-select.html#SQL-SELECT-LIST), eller en funktion som inte muterar data, som stöds av PostgreSQL, stöds i SQL Report Builder. Detta omfattar, men är inte begränsat till, AVG, COUNT, COUNT DISTINCT, MIN/MAX och SUM.

Dessutom kan `JOIN` type stöds, men Adobe rekommenderar endast att INER JOIN används eftersom det är det billigaste av `JOIN` typer.

## Köra frågan och visa resultat {#runquery}

När du är klar med din fråga klickar du på **[!UICONTROL Run Query]**. Resultatet visas i en tabell under SQL-redigeraren:

![Kör frågan och visa resultat.](../../assets/SQL_Run_Query.gif)

Om något verkar vara fel i resultatet kan du redigera frågan och köra den igen tills du är nöjd.

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

Klicka **[!UICONTROL Save]** längst upp till höger i [!DNL SQL] och väljer rapport `Type` (`Chart` eller `Table`). Om du vill slå ihop allt markerar du kontrollpanelen för att spara rapporten och klickar på **[!UICONTROL Save to Dashboard]**.

![](../../assets/SQL_Save_Report.gif)

### Analysera dina data

#### [!DNL SQL Report Builder]

[[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) ger er möjlighet att ställa frågor direkt till Data warehouse, se resultaten och snabbt omvandla dem till en rapport. Använda [!DNL SQL] ger dig även möjlighet att [att använda [!DNL SQL] funktioner som inte är tillgängliga](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html) i `Visual` eller `Cohort` Report Builder, vilket ger er större kontroll över era data.

Beräknade kolumner som skapats med [!DNL SQL] är inte beroende av uppdateringscykler, vilket innebär att du kan upprepa dem som du vill och omedelbart se resultaten.

>[!NOTE]
>
>Detta gäller endast kolumnstrukturen, inte datans aktualitet. Uppdateringsdata är fortfarande beroende av slutförda uppdateringscykler.

| **Det här är perfekt för..** | **Det här är inte så bra för..** |
|---|---|
| Intermediala/avancerade analytiker | Nybörjare - du måste veta [!DNL SQL]. |
| The [!DNL SQL] ohyfsad | Enkla analyser - att skriva en fråga kan vara mer praktiskt än att bara använda [!UICONTROL Visual Report Builder]. |
| Skapa engångskalkylerade kolumner | Dela med andra - tänk på er målgrupp: förstår de [!DNL SQL]? Om de inte gör det kan de bli förvirrade av hur rapporten byggs. |
| Data med `one-to-many` relationer |  |
| Testa en ny kolumn eller analys |  |

#### Resultat för databas jämfört med SQL Editor

Olika resultat beror oftast på uppdateringscykler. If [!DNL Commerce Intelligence] är på väg att replikera data från databasen till Data warehouse, kan du se olika resultat även om du använder samma fråga.

Anslutningsproblem kan också leda till avvikelser. Navigera till `Connections` sida genom att klicka **[!DNL Manage Data** > **Connections]** för att ta reda på det - finns det ett fel för databasintegreringen i fråga? I så fall kan du behöva [autentisera integreringen igen](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html) för att få igång saker och ting igen.

Om alla integreringar har anslutits och du inte befinner dig mitt i en uppdateringscykel kan något annat vara fel.

#### Tar bort en [!DNL SQL] Vill du även ta bort de underliggande kolumnerna från Data warehouse?

Nej, du förlorar inga spalter från Data warehouse, oavsett hur du har skapat dem.

Kolumner som skapats med `Data Warehouse Manager` påverkas inte om du tar bort en rapport eller fråga som använder dem.

Kolumner som skapats med [!DNL SQL Report Builder] sparas inte i Data warehouse.


#### `Report Builder` kontra `SQL Report Builder`

The [!DNL SQL Report Builder] ger dig större flexibilitet när du skapar och strukturerar diagram - du kan till exempel välja vilka värden som ska visas på `X` och `Y` axlar. Mer information om hur du skapar diagram finns i [!DNL SQL Report Builder], kolla in [Skapa visualiseringar från [!DNL SQL] frågor](../../tutorials/create-visuals-from-sql.md) självstudiekurs.

#### `Cohort Report Builder` {#cohortrb}

Till skillnad från [!DNL Visual Report Builder], [[!DNL Cohort Report Builder]](../dev-reports/cohort-rpt-bldr.md) är avsett för ett enda ändamål - att analysera och identifiera beteendetrender för liknande användargrupper över tiden. Använda [!DNL Cohort Report Builder] kräver inga [!DNL SQL] så att du kan dyka rakt in utan tvekan om du just börjar.

| **Det här är perfekt för..** | **Det här är inte så bra för..** |
|---|---|
| Intermediala/avancerade analytiker | Nybörjare - du behöver praktiska kohorter. |
| Identifiera beteendetrender över tid | Kvalitativ analys - den kan [klart](../dev-reports/create-qual-cohort-analysis.md), men behöver hjälp av Adobe. |

## Återskapa frågor efter uppdateringscykeln

Du behöver inte återskapa dina frågor. Rapporter skapade med [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) sparas på samma sätt som i traditionell `Report Builder`. Uppdateringsprocessen för [!DNL SQL] är desamma - när data har uppdaterats beräknas och visas värdena i diagrammen på nytt.

>[!NOTE]
>
>När en [!DNL SQL] rapport/fråga, den tar inte bort de underliggande kolumnerna från Data warehouse. Du förlorar inga kolumner, oavsett hur du har skapat dem.

* Kolumner som skapats med Data warehouse Manager påverkas inte om du tar bort en rapport eller fråga som använder dem.

* Kolumner som skapas med SQL Report Builder sparas inte i Data warehouse.

## Radbrytning {#wrapup}

Om du vill prova något mer utmanande, varför inte skriva en fråga som är optimerad för visualisering? Kolla in [Skapa visualiseringar från [!DNL SQL] frågor, genomgång](../../tutorials/create-visuals-from-sql.md){: target=&quot;_blank&quot;} för att komma igång.
