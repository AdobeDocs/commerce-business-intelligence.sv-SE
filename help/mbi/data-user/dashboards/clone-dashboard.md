---
title: Klonpaneler
description: Lär dig hur du klonar kontrollpaneler.
exl-id: f0bfa786-ab01-4c55-9d8a-ed002c2321b6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '196'
ht-degree: 0%

---

# Klona en instrumentpanel

Om du klonar en kontrollpanel kan du kopiera alla rapporter i en kontrollpanel till en ny kontrollpanel.

Detta är användbart om du vill återskapa en befintlig uppsättning diagram men ändra perspektivet (till exempel en annan datavy, en annan marknad, en annan webbplats eller en annan butik). När du har duplicerat kontrollpanelen kan du redigera alla nya diagram för att ändra måtten, datavyn, filtret eller gruppvis.

1. Om du vill klona en instrumentpanel klickar du på **[!UICONTROL Options]** högst upp på skärmen.

1. Klicka på **[!UICONTROL Save As]** i listrutan.

1. Ange `New Dashboard Name` när du uppmanas till detta. Adobe rekommenderar att du ger dig en överblick över vilken information som finns på kontrollpanelen.

   Du klonar till exempel en instrumentpanel med namnet `Customer Activity`. Den här instrumentpanelen innehöll information om kundaktivitet för din Philadelphia-plats, men nu vill du skapa en instrumentpanel för din nya New York-ort. Den här instrumentpanelen kan heta `New York City - Customer Activity`.

1. Använd fälten `Chart Title Find` och `Chart Title Replace` för att hitta alla diagram med `Philadelphia` i titeln och ersätt den med `New York City`.

   Om du inte anger några värden i de här fälten läggs `(2)` automatiskt till i slutet av alla diagramrubriker på den nya instrumentpanelen.

1. Klicka på **[!UICONTROL Save]** för att klona instrumentpanelen.

Exempel:

![kloninstrumentpanel](../../assets/datgif.gif)
