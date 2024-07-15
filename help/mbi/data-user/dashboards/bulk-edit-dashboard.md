---
title: Massredigeringsdiagram i kontrollpaneler
description: Lär dig hur du använder gruppredigeringsfunktionen i  [!DNL Commerce Intelligence].
exl-id: 576ffabb-5e5d-4251-9662-951e2cd30f31
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 1%

---

# Massredigera diagram i kontrollpaneler

Gruppredigeringsfunktionen gör det enkelt att ändra diagramnamn och datum på kontrollpanelerna. Du vill till exempel att alla diagram på en specifik kontrollpanel ska hänvisa till en enskild butik och rapportera månadsvis i stället för kvartalsvis. Låt funktionen `bulk-editing` utföra arbetet i stället för att ändra allt manuellt. I det här avsnittet får du lära dig hur du använder:

* [Funktionen  [!DNL Find/Replace] ](#findreplace)

* [Funktionen  [!DNL Prepend Name] ](#prepend)

* [Funktionen  [!DNL Change Dates] ](#dates)

Tänk på det här med tanke på det: *Måste de här ändringarna vara permanenta?* Om inte, överväg att klona instrumentpanelen och sedan ändra datumen på den nya instrumentpanelen. På så sätt kan du behålla den ursprungliga kontrollpanelen samtidigt som du gör de ändringar du behöver.

>[!NOTE]
>
>Om du ändrar många rapporter kan uppdateringsprocessen ta en liten stund.

## Använder [!DNL Find/Replace] {#findreplace}

1. Klicka på kugghjulsikonen (![](../../assets/gear-icon.png)) bredvid instrumentpanelens namn och sedan på [!UICONTROL Bulk Edit Reports]-fönstret.

1. Klicka på **[!UICONTROL Chart Title Find and Replace]** i popup-fönstret.

1. Skriv de ord eller tecken som du vill hitta i fältet `Chart Title Find`.

1. I fältet `Replace With` skriver du de ord eller tecken som ska ersätta det som finns i fältet `Find`.

1. Klicka på **[!UICONTROL Update Reports]**.

Exempel:

![massredigering](../../assets/bulk_edit.gif)

## Förväntar `Chart Names` {#prepend}

1. Klicka på kugghjulsikonen (![](../../assets/gear-icon.png)) bredvid instrumentpanelens namn och sedan på [!UICONTROL Bulk Edit Reports]-fönstret.

1. Klicka på **[!UICONTROL Prepend Report Names]** i popup-fönstret.

1. Skriv de ord eller tecken som du vill lägga till i diagrammen.

1. Klicka på **[!UICONTROL Update Reports]**.

Exempel:

![prepend](../../assets/prepend.gif)

## Ändrar `Dates` {#dates}

1. Klicka på kugghjulsikonen (![](../../assets/gear-icon.png)) bredvid instrumentpanelens namn och välj sedan fönstret [!UICONTROL Bulk Edit Reports].

1. Klicka på **[!UICONTROL Change Dates]** i popup-fönstret.

1. Ange nya `Start/End Date` och `Time Interval`. Du kan också lämna dessa fält oförändrade.

1. Klicka på **[!UICONTROL Update Reports]**.

Exempel:

![ändrar datum](../../assets/dates.gif)
