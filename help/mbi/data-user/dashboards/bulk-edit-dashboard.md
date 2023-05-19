---
title: Massredigeringsdiagram i kontrollpaneler
description: Läs om hur du använder gruppredigeringsfunktionen i [!DNL Commerce Intelligence].
exl-id: 576ffabb-5e5d-4251-9662-951e2cd30f31
source-git-commit: 3bf4829543579d939d959753eb3017364c6465bd
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# Massredigera diagram i kontrollpaneler

Gruppredigeringsfunktionen gör det enkelt att ändra diagramnamn och datum på kontrollpanelerna. Du vill till exempel att alla diagram på en specifik kontrollpanel ska hänvisa till en enskild butik och rapportera månadsvis i stället för kvartalsvis. I stället för att ändra allt manuellt kan du `bulk-editing` funktionen gör jobbet. I det här avsnittet får du lära dig hur du använder:

* [The [!DNL Find/Replace] Funktion](#findreplace)

* [The [!DNL Prepend Name] Funktion](#prepend)

* [The [!DNL Change Dates] Funktion](#dates)

Men tänk på det här, trots allt.. *Måste dessa förändringar vara permanenta?* Om inte, överväg att klona kontrollpanelen och sedan ändra datumen i den nya kontrollpanelen. På så sätt kan du behålla den ursprungliga kontrollpanelen samtidigt som du gör de ändringar du behöver.

>[!NOTE]
>
>Om du ändrar många rapporter kan uppdateringsprocessen ta en liten stund.

## Använda [!DNL Find/Replace] {#findreplace}

1. Klicka på kugghjulet (![](../../assets/gear-icon.png)) bredvid instrumentpanelens namn och sedan [!UICONTROL Bulk Edit Reports] -fönstret.

1. Klicka **[!UICONTROL Chart Title Find and Replace]** på popup-menyn.

1. I `Chart Title Find` skriver du de ord eller tecken du vill söka efter.

1. I `Replace With` skriver du in de ord eller tecken som ska ersätta det som finns i `Find` fält.

1. Klicka **[!UICONTROL Update Reports]**.

Exempel:

![massredigering](../../assets/bulk_edit.gif)

## Förväntande `Chart Names` {#prepend}

1. Klicka på kugghjulet (![](../../assets/gear-icon.png)) bredvid instrumentpanelens namn och sedan [!UICONTROL Bulk Edit Reports] -fönstret.

1. Klicka **[!UICONTROL Prepend Report Names]** på popup-menyn.

1. Skriv de ord eller tecken som du vill lägga till i diagrammen.

1. Klicka **[!UICONTROL Update Reports]**.

Exempel:

![prepend](../../assets/prepend.gif)

## Ändrar `Dates` {#dates}

1. Klicka på kugghjulet (![](../../assets/gear-icon.png)) bredvid instrumentpanelens namn och välj sedan [!UICONTROL Bulk Edit Reports] -fönstret.

1. Klicka **[!UICONTROL Change Dates]** i popup-fönstret.

1. Ange den nya `Start/End Date` och `Time Interval`. Du kan också lämna dessa fält oförändrade.

1. Klicka **[!UICONTROL Update Reports]**.

Exempel:

![ändringsdatum](../../assets/dates.gif)
