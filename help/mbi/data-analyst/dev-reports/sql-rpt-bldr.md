---
title: Använda SQL Report Builder
description: Lär dig allt om hur du använder SQL Report Builder.
exl-id: 3a485b00-c59d-4bc5-b78b-57e9e92dd9d6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '1397'
ht-degree: 0%

---

# Använder [!DNL SQL Report Builder]

>[!NOTE]
>
>Kräver [administratörsbehörighet](../../administrator/user-management/user-management.md) för att skapa och redigera SQL-diagram. `Standard` användare kan ordna om dessa diagram på kontrollpaneler, och `Read-only` användare har samma upplevelse som de har av traditionella diagram. Dessutom har `Read-only` användare inte åtkomst till frågetexten.

Mer information finns i [utbildningsvideon](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html).

[!DNL SQL], eller Structured Query Language, är ett programmeringsspråk som används för att kommunicera med databaser. I [!DNL Commerce Intelligence] används [!DNL SQL] för att fråga efter eller hämta data från din Data Warehouse. Titta på rapporterna på din instrumentpanel - bakom kulisserna drivs var och en av dem av en [!DNL SQL]-fråga.

Du kan använda [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) för att direkt fråga din Data Warehouse, visa resultaten och omvandla dem till ett diagram. Du kan börja skapa en rapport med [!DNL SQL Report Builder] genom att klicka på **[!UICONTROL Report Builder** > **[!DNL SQL Report Builder]]**.

Mer information finns i [utbildningsvideon](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-sql-report-builder.html).

Med [!DNL SQL Report Builder] kan du ställa frågor direkt till din Data Warehouse, visa resultaten och snabbt omvandla dem till ett diagram. Det bästa med att använda [!DNL SQL] för att skapa rapporter är att du inte behöver vänta på uppdateringscykler för att iterera i kolumner som du skapar. Om resultatet inte ser bra ut kan du snabbt redigera och köra frågan igen tills det matchar dina förväntningar.

I det här avsnittet får du hjälp med att använda [!DNL SQL Report Builder]. När du känner till din väg kan du kolla in självstudiekursen [!DNL SQL] för visualiseringar eller försöka optimera några av frågorna som du har skrivit.

I den här artikeln:

1. [Skriva en fråga](#writing)

1. [Köra frågan och visa resultat](#runquery)

1. [Skapa en visualisering](#createviz)

1. [Sparar rapporten](#save)

## [!DNL SQL Report Builder] integreringar

[[!DNL Google Analytics]](../importing-data/integrations/google-analytics.md) är den enda integreringen som inte är tillgänglig för användning med [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md). Den här funktionen är under utveckling.

Om du vill komma igång med att skapa en [!DNL SQL]-rapport klickar du på **[!UICONTROL Report Builder]** eller **[!UICONTROL Add Report]** överst på en kontrollpanel. Öppna [!DNL Report Picker]-redigeraren genom att klicka på **[!UICONTROL SQL Report Builder]** på skärmen [!DNL SQL].

## Kom igång

Om du vill redigera en rapport klickar du på kugghjulsikonen (![Kugghjulsikonen](../../assets/gear-icon.png)) i det övre högra hörnet av ett [!DNL SQL]-baserat diagram och klickar på **[!UICONTROL Edit]**.

## Skriva en fråga {#writing}

>[!NOTE]
>
>[!DNL SQL Report Builder] frågor är skiftlägeskänsliga. Kontrollera att du använder rätt skiftläge när du skriver frågor, annars kan oväntade resultat eller fel uppstå.

Följ [riktlinjerna för frågeoptimering](../../best-practices/optimizing-your-sql-queries.md) och skriv en fråga i [!DNL SQL]-redigeraren.

>[!IMPORTANT]
>
>**Mätvärden i [!DNL SQL] rapporter** - När du infogar ett mätvärde i en SQL-rapport används måttets `current definition`.

Om måttet uppdateras i framtiden återspeglar SQL-rapporten *inte* ändringarna. Du måste redigera rapporten manuellt för att ändringarna ska börja gälla.

Med knapparna högst upp i sidofältet kan du växla mellan listor med tabeller och mätvärden som är tillgängliga för användning i [!DNL SQL Report Builder]. Om du inte ser vad du söker i listan kan du söka efter den med hjälp av sökfältet högst upp i sidlisten.

Du kan också använda sidofältet i [!DNL SQL]-redigeraren för att infoga mått, tabeller och kolumner direkt i dina frågor genom att hålla markören över dem och klicka på **[!UICONTROL Insert]**:

![Infoga en tabell i [!DNL SQL]-redigeraren.](../../assets/SQL_RB_Insert_Table.png)

>[!NOTE]
>
>Alla [SELECT-funktioner](https://www.postgresql.org/docs/9.5/sql-select.html#SQL-SELECT-LIST), eller funktioner som inte muterar data, som stöds av PostgreSQL, stöds i SQL Report Builder. Detta omfattar, men är inte begränsat till, AVG, COUNT, COUNT DISTINCT, MIN/MAX och SUM.

Dessutom stöds alla `JOIN`-typer, men Adobe rekommenderar endast att du använder INNER JOIN eftersom det är det billigaste av `JOIN`-typerna.

## Köra frågan och visa resultat {#runquery}

När du är klar med att skriva din fråga klickar du på **[!UICONTROL Run Query]**. Resultatet visas i en tabell under SQL-redigeraren:

![Kör frågan och visa resultat.](../../assets/SQL_Run_Query.gif)

Om något verkar vara fel i resultatet kan du redigera frågan och köra den igen tills du är nöjd.

Du kan ibland se [meddelanden under redigeraren med EXPLAIN i dem](../../best-practices/optimizing-your-sql-queries.md). Om du ser något av detta innebär det att frågan inte har körts och att du behöver finjustera något.

När du är klar med redigeringen av frågan kan du gå vidare till att antingen skapa en visualisering eller spara ditt arbete på en kontrollpanel.

## Skapa en visualisering {#createviz}

Om du vill skapa en visualisering med dina frågeresultat klickar du på fliken **[!UICONTROL Chart]** i rutan `Results`. På den här fliken väljer du:

* `Series`, eller den kolumn som du vill mäta, till exempel **Artiklar som sålts**.
* `Category`, eller den kolumn som du vill använda för att segmentera dina data, till exempel **hämtningskälla**.
* Värdena `Labels` eller X-axel.

Här är en snabb titt på hur visualiseringsprocessen ser ut:

![Animerad demonstration av SQL Report Builder-visualisering - översikt](../../assets/SQL_RB_viz_overview.gif)

En detaljerad genomgång av hur du skapar en visualisering finns i självstudiekursen [Skapa visualiseringar från SQL-frågor](../../tutorials/create-visuals-from-sql.md){: target="_blank"}.

## Sparar rapporten {#save}

Innan du kan spara ditt arbete måste du ge rapporten ett namn. Kom ihåg att följa riktlinjerna för [bästa praxis för namngivning](../../best-practices/naming-elements.md){: target="_blank"} och välj något som tydligt anger vad rapporten är!

Klicka på **[!UICONTROL Save]** i det övre högra hörnet av [!DNL SQL]-redigeraren och markera rapporten `Type` (`Chart` eller `Table`). Om du vill slå ihop allt markerar du instrumentpanelen för att spara rapporten och klickar på **[!UICONTROL Save to Dashboard]**.

![Animerad demonstration av hur du sparar en SQL-rapport på instrumentpanelen](../../assets/SQL_Save_Report.gif)

### Analysera dina data

#### [!DNL SQL Report Builder]

[[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) ger dig möjlighet att direkt fråga din Data Warehouse, visa resultaten och snabbt omvandla dem till en rapport. Om du använder [!DNL SQL] kan du även använda [funktioner som inte är tillgängliga [!DNL SQL]  i &#x200B;](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html)- eller `Visual` Report Builders, vilket ger dig större kontroll över dina data.`Cohort`

Beräknade kolumner som skapats med [!DNL SQL] är inte beroende av uppdateringscykler, vilket innebär att du kan iterera på dem som du vill och omedelbart se resultaten.

>[!NOTE]
>
>Detta gäller endast kolumnstrukturen, inte datans aktualitet. Uppdateringsdata är fortfarande beroende av slutförda uppdateringscykler.

| **Det här är perfekt för..** | **Det här är inte så bra för..** |
|---|---|
| Intermediala/avancerade analytiker | Nybörjare - du måste känna till [!DNL SQL]. |
| [!DNL SQL]-kunnig | Enkla analyser - att skriva en fråga kan vara mer användbart än att bara använda [!UICONTROL Visual Report Builder]. |
| Skapa engångskalkylerade kolumner | Dela med andra - tänk på din målgrupp: Förstår de [!DNL SQL]? Om de inte gör det kan de bli förvirrade av hur rapporten byggs. |
| Data med `one-to-many`-relationer |  |
| Testa en ny kolumn eller analys |  |

#### Resultat för databas jämfört med SQL Editor

Olika resultat beror oftast på uppdateringscykler. Om [!DNL Commerce Intelligence] håller på att replikera data från din databas till din Data Warehouse, kan du se olika resultat även om du använder samma fråga.

Anslutningsproblem kan också leda till avvikelser. Navigera till sidan `Connections` genom att klicka på **[!DNL Manage Data** > **Connections]** för att checka ut den - finns det ett fel för databasintegrationen i fråga? I så fall kan du behöva [autentisera integreringen](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html) igen för att få igång saker igen.

Om alla integreringar har anslutits och du inte befinner dig mitt i en uppdateringscykel kan något annat vara fel.

#### Om du tar bort en [!DNL SQL]-rapport tas även de underliggande kolumnerna bort från min Data Warehouse?

Nej, du förlorar inga kolumner från din Data Warehouse, oavsett hur du har skapat dem.

Kolumner som skapats med `Data Warehouse Manager` påverkas inte om du tar bort en rapport eller fråga som använder dem.

Kolumner som skapats med [!DNL SQL Report Builder] sparas inte i din Data Warehouse.


#### `Report Builder` jämfört med `SQL Report Builder`

[!DNL SQL Report Builder] ger dig större flexibilitet när du skapar och strukturerar diagram - du kan till exempel välja vilka värden som ska visas på axlarna `X` och `Y`. Mer information om hur du skapar diagram i [!DNL SQL Report Builder] finns i självstudiekursen [Skapa visualiseringar från  [!DNL SQL] frågor](../../tutorials/create-visuals-from-sql.md).

#### `Cohort Report Builder` {#cohortrb}

Till skillnad från [!DNL Visual Report Builder] är [[!DNL Cohort Report Builder]](../dev-reports/cohort-rpt-bldr.md) avsedd för ett enda syfte - att analysera och identifiera beteendetrender för liknande användargrupper över tiden. Om du använder [!DNL Cohort Report Builder] krävs ingen [!DNL SQL]-kunnighet, så du kan dyka rakt in utan tveksamhet om du just har börjat.

| **Det här är perfekt för..** | **Det här är inte så bra för..** |
|---|---|
| Intermediala/avancerade analytiker | Nybörjare - du behöver praktiska kohorter. |
| Identifiera beteendetrender över tid | Kvalitativ analys - den kan vara [klar](../dev-reports/create-qual-cohort-analysis.md), men kräver Adobe-hjälp. |

## Återskapa frågor efter uppdateringscykeln

Du behöver inte återskapa dina frågor. Rapporter som skapats med [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) sparas på samma sätt som de som skapats i det traditionella `Report Builder`. Uppdateringsprocessen för [!DNL SQL] diagram är densamma. När data har uppdaterats beräknas och visas värdena i diagrammen på nytt.

>[!NOTE]
>
>När du tar bort en [!DNL SQL]-rapport/fråga tas de underliggande kolumnerna inte bort från din Data Warehouse. Du förlorar inga kolumner, oavsett hur du har skapat dem.

* Kolumner som skapas med Data Warehouse Manager påverkas inte om du tar bort en rapport eller fråga som använder dem.

* Kolumner som skapas med SQL Report Builder sparas inte i din Data Warehouse.

## Radbrytning {#wrapup}

Om du vill prova något mer utmanande, varför inte skriva en fråga som är optimerad för visualisering? Kolla in [Skapa visualiseringar från [!DNL SQL] frågesjälvstudiekursen](../../tutorials/create-visuals-from-sql.md){: target="_blank"} för att komma igång.
