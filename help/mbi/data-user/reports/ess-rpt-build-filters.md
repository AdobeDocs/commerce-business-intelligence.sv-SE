---
title: Filter
description: Lär dig hur du använder filter.
exl-id: eb683dfe-9a90-400a-a0c0-3dc00d1f28b5
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '353'
ht-degree: 0%

---

# Filter

Ett eller flera filter kan läggas till för att begränsa vilka data som används för att skapa en rapport. Varje filter är ett uttryck som innehåller en kolumn från den associerade tabellen, en operator och ett värde. Om du t.ex. bara vill inkludera återkommande kunder kan du skapa ett filter som endast innehåller kunder som har gjort mer än en beställning. Flera filter kan användas med logiska `AND/OR` för att lägga till logik i rapporten.

>[!TIP]
>
>En rapport kan innehålla maximalt 3 500 datapunkter. Om du vill minska antalet datapunkter använder du ett filter för att minska mängden data som används för att generera rapporten.

MBI innehåller ett urval av filter som du kan använda &quot;i kartong&quot; eller ändra efter behov. Det finns ingen gräns för hur många filter du kan skapa.

## Så här lägger du till ett filter:

1. Håll markören över varje datapunkt i diagrammet.

   I den här rapporten visar varje datapunkt det totala antalet kunder för månaden.

1. Klicka på Filter (![](../../assets/magento-bi-btn-filter.png)).

   ![Lägg till filter](../../assets/magento-bi-report-builder-filter-add.png)

1. Klicka **[!UICONTROL Add Filter]**.

   Filtren numreras i bokstavsordning och det första är `[A]`. De första två delarna av filtret är listrutealternativ, och den tredje delen är ett värde.

   ![](../../assets/magento-bi-report-builder-filter-add-a.png)

   * Klicka på den första delen av filtret och välj den kolumn som du vill använda som ämne i uttrycket.

      ![Välj första delen av filtret](../../assets/magento-bi-report-builder-filter-part1.png)

   * Klicka på den andra delen av filtret och välj operatorn.

      ![Välj operator](../../assets/magento-bi-report-builder-filter-part2.png)

   * I den tredje delen av filtret anger du det värde som behövs för att slutföra uttrycket.

      ![Ange värdet](../../assets/magento-bi-report-builder-filter-part3.png)

   * När filtret är klart klickar du på **[!UICONTROL Apply]**.

      Rapporten innehåller nu bara återkommande kunder, och antalet kundposter som hämtats för rapporten har reducerats från 33 kB till 12 600 kB.

      ![Filtrerad rapport](../../assets/magento-bi-report-builder-filter-report.png)<!--{: .zoom}-->

1. Klicka på perspektivet ( ![](../../assets/magento-bi-btn-perspective.png)).

   ![Perspektiv](../../assets/magento-bi-report-builder-filter-perspective.png)<!--{: .zoom}-->

1. Välj `Cumulative`. Klicka sedan på **[!UICONTROL Apply]**.

   ![Kumulativt perspektiv](../../assets/magento-bi-report-builder-filter-perspective-cumulative.png)

   The `Cumulative` I perspektivet fördelas förändringen över tid i stället för att visa de ojämna upp- och nedgraderingarna för varje månad.

1. Ange `Title` för rapporten och klicka på **[!UICONTROL Save]** det som `Chart` till din instrumentpanel.

   ![Spara på instrumentpanelen](../../assets/magento-bi-report-builder-filter-perspective-cumulative-save.png)
