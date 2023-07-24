---
title: data warehouse Manager
description: Lär dig hur du hanterar tabell- och kolumnsynkroniseringsinställningar, fördjupar dig i ett tabellschema och skapar beräknade kolumner som kan användas i rapporter.
exl-id: b9577919-0db0-47f1-a426-1abe48443ac0
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1240'
ht-degree: 0%

---

# data warehouse Manager

>[!NOTE]
>
>Kräver [Administratörsbehörigheter](../../administrator/user-management/user-management.md)

Data warehouse Manager som du kommer åt genom att klicka **[!UICONTROL Manage Data > Data Warehouse]**, är portalen för [!DNL Adobe Commerce Intelligence] data warehouse. Med hjälp av Data warehouse Manager kan du hantera tabell- och kolumnsynkroniseringsinställningar, gå nedåt i en tabells schema och skapa beräknade kolumner som kan användas i rapporter.

Det här ämnet handlar om:

* [Lära dig vägen runt](#learning)
* [Synkronisera tabeller och kolumner](#syncing)
* [Skapa beräknade kolumner](#calculated)
* [Släppa tabeller och ta bort kolumner](#delete)
* [Synkronisera nya tabeller i bakgrunden](#syncnew)
* [När kan jag använda mina nya kolumner?](#when)

## Lära dig vägen runt {#learning}

Den vänstra sidan av `Data Warehouse Manager` sidan innehåller tabelllistan, så att du enkelt kan växla mellan tabeller. När du väljer en tabell från listan fylls tabellhanteringsområdet i med tabellens schema där du kan ändra den markerade tabellen.

I tabelllistan grupperas tabellerna efter anslutningskälla. De här källorna läggs till under [!UICONTROL Manage Data > Integrations] och kan vara antingen en databas, en [API](https://developer.adobe.com/commerce/services/reporting/)eller en anslutning från tredje part. Överst i tabelllistan finns det en sökruta där du enkelt kan hitta de tabeller du söker.

Under sökrutan visas två alternativ: `All Tables` och `Synced Tables`. The `All Tables` anger alla tabeller som du har gjort tillgängliga för Data warehouse, inklusive både synkroniserade och osynkroniserade tabeller.

The `Synced Tables` visar alla tabeller som redan har lagts till i Data warehouse och som har data som replikeras från de markerade kolumnerna.

Visa inte tabellen som du letar efter i `All Tables` lista? Det finns några möjliga orsaker till detta:

* Datakällan har inte lagts till än
* Datakällan är en databas och [!DNL Commerce Intelligence] användare som du har skapat saknar åtkomst. I så fall måste du eller databasadministratören bevilja åtkomst.
* Datakällan eller tabellen har nyligen lagts till och har inte synkroniserats än

## Synkronisera tabeller och kolumner {#syncing}

### Synkroniserar nya tabeller och inbyggda kolumner

Med Data warehouse Manager kan du inte bara visa och hantera datakällor, du kan också välja de enskilda tabeller och kolumner som du vill synkronisera.

1. Klicka på `All Tables` och leta reda på tabellen som du vill synkronisera.
1. Klicka på namnet på tabellen för att förhandsgranska schemat. Om tabellen är ny visas alla kolumner som `Unsynced`.
1. Markera de kolumner som du vill synkronisera.

   >[!NOTE]
   >
   >Kolumner som är inbyggda i en tabell har Från databasen i `Location` kolumn.

1. Kontrollera att `Primary Key` kolumner - de här kolumnerna har en nyckelsymbol bredvid kolumnnamnet. A `Primary Key` krävs för att kunna synkronisera data korrekt till Data warehouse.

   Om du synkroniserar en tabell som kommer direkt från databasen är det möjligt att `Primary Keys` får inte betecknas. I så fall kontaktar du databasadministratören och begär att en eller flera primärnycklar läggs till i tabellen.
1. När du är klar klickar du på ![knapp](../../assets/button.png) -knappen.

A *Klart!* visas meddelandet och statusen ändras till `Pending` för de markerade kolumnerna. När nästa fullständiga uppdatering är klar är de nya synkroniserade tabellerna och kolumnerna tillgängliga för användning i rapporter. Du kan också ange nya [replikeringsmetoder](./cfg-replication-methods.md) efter den inledande synkroniseringen.

Här är en kort titt på hela processen:

![Lägga till kolumner i data warehouse](../../assets/DW_sync.gif)

### Synkronisera nya tabeller i bakgrunden {#syncnew}

När du synkroniserar en stor tabell för första gången måste Data warehouse hämta in alla datapunkter i tabellen retroaktivt innan nya data hämtas kontinuerligt. Om tabellen är stor kanske du inte vill att den inledande synkroniseringen ska köras i sekvens med **uppdateringscykel**. I det här fallet vill du att den inledande synkroniseringen ska ske i bakgrunden, i *parallell* med alla uppdateringar som körs.

Om du vill vara säker på att det sker bör du markera `Save and Sync Data Immediately` för att synkronisera tabellen för första gången.

### Söker efter nya tabeller och kolumner {#forceupdate}

Data warehouse identifierar inte automatiskt nya källor, tabeller eller kolumner så fort de läggs till. En synkroniseringsprocess pågår under hela veckan för att hitta nya tillägg och göra dem tillgängliga, men du kan tvinga fram en struktursynkronisering om du vill komma åt nyligen tillagda tabeller och kolumner innan processen körs.

Under sökfältet i tabelllistan finns en `Check for new tables and columns` länk. Om du klickar på den här länken framtvingas struktursynkroniseringsprocessen. nya tillägg är vanligtvis tillgängliga efter 10 minuter. Uppdatera sidan för att se den nya källan, tabellen eller kolumnen.

## Skapar beräknade kolumner {#calculated}

Att bara kunna se och hantera data från alla era källor gör det mycket enklare att få insikter i verksamheten. Men i Data warehouse Manager kan du gå ett steg längre genom att skapa beräknade kolumner i dina tabeller. `Calculated` kolumner hämtar ny information från dina befintliga data.

Säg att du vill lägga till `user's lifetime revenue` till `users` för att hitta värdefulla användare. Om du vill segmentera intäkterna efter kön kan du lägga till `customer's gender` till `orders` tabell.

Mer information finns här [självstudiekurs](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md).

## Släpp tabeller och ta bort kolumner {#delete}

På samma sätt som du kan markera tabeller och kolumner som ska synkroniseras med Data warehouse kan du även ta bort eller släppa dem.

>[!NOTE]
>
>När du släpper en tabell eller tar bort kolumner tas alla beroende rapporter, mätvärden, filteruppsättningar och kolumner bort när du har bekräftat borttagningen. Var säker på att du vill göra det här - **den här åtgärden kan inte ångras.**

Var inte orolig om du klickar **[!UICONTROL Delete]** av misstag. En beroendekontroll körs innan något tas bort, så du har möjlighet att granska allt innan du bekräftar.

Om du vill ta bort kolumner klickar du på tabellen som kolumnen tillhör. Markera kolumnerna som du vill ta bort och klicka på ![button\_1.png](../../assets/button_1.png) -knappen.

Om du vill ta bort en synkroniserad tabell markerar du alla kolumner i tabellen och klickar på knappen ![knapp](../../assets/button_1.png) -knappen. Då tas alla inbyggda och beräknade kolumner som använder den här tabellen bort från Data warehouse.

### Bekräfta ändringar

Oavsett om du släpper en tabell eller tar bort kolumner, körs en beroendekontroll innan borttagningsprocessen slutförs. Beroenden är beräknade kolumner, mått, filteruppsättningar och rapporter som använder tabellen eller kolumnerna som tas bort. Alla identifierade beroenden visas - i det här läget kan du antingen avbryta processen eller klicka på **[!UICONTROL Confirm Changes]** för att släppa tabellen/ta bort kolumnerna.

Det går inte att återställa borttagna beroenden, men tabellerna och kolumnerna är fortfarande tillgängliga om du behöver synkronisera om inbyggda kolumner i framtiden.

Här följer en snabbtitt på hur du tar bort en kolumn:

![Ta bort en kolumn från data warehouse](../../assets/DW_delete.gif)

## När kan jag använda mina nya kolumner? {#when}

Nya synkroniserade kolumner och nya/uppdaterade beräknade kolumner kan användas när nästa fullständiga uppdatering har slutförts. Om en uppdatering inte redan pågår kan du framtvinga en uppdatering genom att klicka på **[!UICONTROL Force update]** visas högst upp i `Data Warehouse` eller `Integrations` sida. Du kan också schemalägga ett e-postmeddelande när uppdateringen har slutförts genom att klicka på **[!UICONTROL Email me when complete]**.

När du är redo att använda dina nya kolumner i rapporter, [du måste lägga till dem i mätvärden först](../data-warehouse-mgr/manage-data-dimensions-metrics.md). Även om data inte är tillgängliga förrän en uppdatering har slutförts kan du fortfarande använda nya kolumner i rapporter. Data i rapporten visas när uppdateringen är klar.

## Radbrytning

Den här artikeln omfattade mycket material. Vid det här laget bör du ha en god förståelse för vad en databas är, hur data är ordnade, hur tabeller relaterar till varandra och vad du kan göra med Data warehouse Manager.

Testa dina kunskaper med [skapa en beräknad kolumn](../data-warehouse-mgr/creating-calculated-columns.md) eller [skapa intressanta rapporter](../../tutorials/using-visual-report-builder.md).
