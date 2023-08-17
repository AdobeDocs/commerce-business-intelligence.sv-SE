---
title: Exportera rådata
description: Lär dig exportera poster från [!DNL Commerce Intelligence] Data Warehouse för att få en närmare titt på vad som ligger bakom instrumentpanelen.
exl-id: 26decdaf-2b2c-4ca2-b3d5-0386892662e8
role: Admin, Data Architect, Data Engineer, Leader, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '477'
ht-degree: 0%

---

# Exportera rådata

Med export av rådata kan du exportera poster från Datan Warehouse för att få en närmare bild av vad som ligger bakom instrumentpanelen. Export av rådata kan också hjälpa dig [identifiera datamatchningsavvikelser](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html).

Export av rådata ger tillgång till ytterligare kolumner och dimensioner som genereras genom avnormalisering och föraggning av relevanta mått. Till exempel: `User's first order date` är en dimension som du kan exportera för varje användare i [!DNL Commerce Intelligence], även om den inte är tillgänglig i din databas.

Den här självstudien handlar om följande:

* [Markera data som ska exporteras](#select)
* [Laddar ned export (](#download)
* [Få tillgång till historikexport](#historical)

## Steg 1: Markera data som ska exporteras {#select}

Det finns två sätt att exportera rådata på [!DNL Commerce Intelligence]:

1. på diagramnivå
1. på tabellnivå

### Exportera på tabellnivå i [!UICONTROL Manage Data] Tabb

Om du vill exportera tabellen från [!UICONTROL Manage Data] -flik, du behöver [Administratör](../administrator/user-management/user-management.md) behörigheter.

1. Klicka **[!UICONTROL Manage Data** > ** Exportera data **> **Raw-dataexport]**.
1. Du ser en `Export List` av nyligen skapade dataexporter, om sådana finns. Klicka **[!UICONTROL Add Export]** för att skapa en export.
1. The `New Raw Data Export` visas. Här kan du anpassa exporten genom att markera eller avmarkera kolumner och filter:

   * `Table` - `Table` markerar den tabell som data exporteras från. Som standard visas den tabell som du navigerade till.
   * `Export Name` - I det här fältet anger du namnet på exporten. Exempel: `Philadelphia - Daily Revenue`.
   * `Available Columns` - I det här fältet listas de kolumner (dimensioner) i databasen som är tillgängliga för export. Om du vill lägga till en kolumn klickar du på dess namn.
   * `Selected Columns` - I det här fältet listas de kolumner (dimensioner) som för närvarande ingår i exporten. Om du vill ta bort en kolumn klickar du på dess namn.
   * `Filter` - I det här avsnittet visas de filter som för närvarande används för exporten. Dessa filter kan ändras. Du kan också lägga till nya filter om du vill exportera en viss datauppsättning.
   * När du är klar klickar du **[!UICONTROL Export Data]**.

### Exportera på diagramnivå från kontrollpanelen

1. Klicka på kugghjulsikonen i det övre högra hörnet av ett diagram.

1. Välj `Raw Export` från listrutan för att visa `Raw Export` -dialogrutan.

1. Anpassa exporten genom att välja `table`, `columns`och `filters` att inkludera eller exkludera. Mer information om fälten i den här modulen finns i föregående avsnitt.

   >[!NOTE]
   >
   >Tabellen som visas i `Table` -fältet är som standard tabellen som styr diagrammet.

1. När du är klar klickar du **[!UICONTROL Export Data]**.

Se hela processen på diagramnivå.

![](../assets/Chart-level_export.gif)

## Steg 2: Hämta exporten {#download}

Exporten börjar bearbetas omedelbart efter att du har slutfört dina val i dialogrutan `Raw Data Export` -dialogrutan. Eftersom vissa exporter kan vara stora är de begränsade till 10 miljoner rader och kan ta lite tid att genomföra.

Om du vill kontrollera om exporten är klar klickar du på **[!UICONTROL Raw Data Exports]** i skärmens övre högra hörn. Klicka **[!UICONTROL Download]** för att ladda ned en zippad `.csv` exportfil.

![](../assets/Downloading_export.gif)

## Steg 3: Få tillgång till historisk export {#historical}

Om du vill visa tidigare exporter klickar du på **[!UICONTROL Raw Data Export]** i skärmens övre högra hörn. Väntande och slutförda rapporter kan användas i upp till sju dagar.
