---
title: Exportera rådata
description: Lär dig exportera poster från din [!DNL Commerce Intelligence] Data Warehouse för att få en närmare titt på vad som ligger bakom instrumentpanelen.
exl-id: 26decdaf-2b2c-4ca2-b3d5-0386892662e8
role: Admin, Data Architect, Data Engineer, Leader, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---

# Exportera rådata

Med export av rådata kan du exportera poster från Datan Warehouse för att få en närmare bild av vad som ligger bakom instrumentpanelen. Dessutom kan export av rådata hjälpa dig att [identifiera datameddelanden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html).

Export av rådata ger tillgång till ytterligare kolumner och dimensioner som genereras genom avnormalisering och föraggning av relevanta mått. `User's first order date` är till exempel en dimension som du kan exportera för varje användare i [!DNL Commerce Intelligence], men som kanske inte är tillgänglig i din databas.

Den här självstudien handlar om följande:

* [Markera data som ska exporteras](#select)
* [Laddar ned export (](#download)
* [Få tillgång till historikexport](#historical)

## Steg 1: Markera data som ska exporteras {#select}

Det finns två sätt att exportera rådata i [!DNL Commerce Intelligence]:

1. på diagramnivå
1. på tabellnivå

### Exportera på tabellnivå på fliken [!UICONTROL Manage Data]

Om du vill exportera tabellen från fliken [!UICONTROL Manage Data] behöver du [administratörsbehörighet](../administrator/user-management/user-management.md).

1. Klicka på **[!UICONTROL Manage Data** > ** Exportera data **> **Raw-dataexport]**.
1. Du ser `Export List` av nyligen skapade dataexporter, om det finns några. Klicka på **[!UICONTROL Add Export]** om du vill skapa en export.
1. Dialogrutan `New Raw Data Export` visas. Här kan du anpassa exporten genom att markera eller avmarkera kolumner och filter:

   * `Table` - Fältet `Table` markerar tabellen som data exporteras från. Som standard visas den tabell som du navigerade till.
   * `Export Name` - I det här fältet anger du namnet på exporten. Till exempel: `Philadelphia - Daily Revenue`.
   * `Available Columns` - Det här fältet visar de kolumner (dimensioner) i databasen som är tillgängliga för export. Om du vill lägga till en kolumn klickar du på dess namn.
   * `Selected Columns` - Det här fältet visar de kolumner (dimensioner) som för närvarande ingår i exporten. Om du vill ta bort en kolumn klickar du på dess namn.
   * `Filter` - I det här avsnittet visas de filter som för närvarande används för exporten. Dessa filter kan ändras. Du kan också lägga till nya filter om du vill exportera en viss datauppsättning.
   * När du är klar klickar du på **[!UICONTROL Export Data]**.

### Exportera på diagramnivå från kontrollpanelen

1. Klicka på kugghjulsikonen i det övre högra hörnet av ett diagram.

1. Välj `Raw Export` i listrutan för att visa dialogrutan `Raw Export`.

1. Anpassa exporten genom att välja `table`, `columns` och `filters` för att inkludera eller exkludera. Mer information om fälten i den här modulen finns i föregående avsnitt.

   >[!NOTE]
   >
   >Tabellen som visas i fältet `Table` är som standard tabellen som styr diagrammet.

1. När du är klar klickar du på **[!UICONTROL Export Data]**.

Se hela processen på diagramnivå.

![](../assets/Chart-level_export.gif)

## Steg 2: Hämta exporten {#download}

Exporten börjar bearbetas omedelbart efter att du har slutfört dina val i dialogrutan `Raw Data Export`. Eftersom vissa exporter kan vara stora är de begränsade till 10 miljoner rader och kan ta lite tid att genomföra.

Om du vill kontrollera om exporten är klar klickar du på **[!UICONTROL Raw Data Exports]** i skärmens övre högra hörn. Klicka på **[!UICONTROL Download]** om du vill hämta en zippad `.csv`-fil av exporten.

![](../assets/Downloading_export.gif)

## Steg 3: Få tillgång till historisk export {#historical}

Om du vill visa tidigare exporter klickar du på **[!UICONTROL Raw Data Export]** i skärmens övre högra hörn. Väntande och slutförda rapporter kan användas i upp till sju dagar.
