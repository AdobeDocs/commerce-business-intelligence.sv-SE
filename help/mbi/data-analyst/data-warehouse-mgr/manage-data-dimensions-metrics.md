---
title: Hantera datamängder
description: Lär dig vad en dimension är och den kan användas för att filtrera eller segmentera diagram baserat på ett mätvärde.
exl-id: 143a4b1e-2e6f-438a-90e6-bdda13b39cb9
source-git-commit: 2db58f4b612fda9bdb2570e582fcde89ddc18154
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# Hantera datamängder

>[!NOTE]
>
>Kräver [Administratörsbehörigheter](../../administrator/user-management/user-management.md).

En dimension är ett fält i samma tabell som ett mått som kan användas för att filtrera eller segmentera diagram baserat på det måttet. Ett intäktsmått kan t.ex. innehålla ort, delstat, land, orderstatus, kupongkod och andra typer av dimensioner.

## Lägg till dimensioner till flera mätvärden

Så här lägger du till en eller flera dimensioner till flera mått samtidigt:

1. Gå till **[!UICONTROL Manage Data > Metrics]**.

1. Klicka **[!UICONTROL Add Dimensions To Metric(s)]**.

1. Välj den tabell som innehåller dimensionerna.

1. I `Choose Metric(s) to Add Dimensions` markerar du de mätvärden du vill lägga till dimensioner i. När du har valt `Choose Dimensions to Add` visas till höger. Markera de dimensioner som du vill lägga till i det valda måttet.

   ![](../../assets/Add_Dimensions.png)

1. Om du vill segmentera eller gruppera efter någon av rapportens datamått måste du ange att de är _Grupperbar_.

1. Klicka **[!UICONTROL Add]**.

## Ta bort dimensioner från flera mått

Så här tar du bort en eller flera dimensioner från flera mått:

1. Gå till **[!UICONTROL Data > Metrics]**.

1. Klicka **[!UICONTROL Remove Dimensions From Metric(s)]**.

1. Välj den tabell som innehåller dimensionerna.

1. Välj de mått som du vill ta bort från vänster och de dimensioner som du vill ta bort till höger.

1. Klicka **[!UICONTROL Remove]**.

1. Om dimensionerna används för rapporter visas en varning med listan över diagram som använder dimensionerna. Klicka **[!UICONTROL Delete]** om du vill ta bort de markerade dimensionerna och alla deras underordnade, inklusive rapporter.

## Hantera mått i mätvärden

**Så här lägger du till dimensioner i ett mått:**

1. Gå till **[!UICONTROL Data > Metrics]**.

1. Klicka **[!UICONTROL Edit]** på mätvärdena vill du ha en ny dimension.

1. I `Dimensions` -avsnittet använder du `Add a dimension` för att välja en dimension att lägga till.

>[!NOTE]
>
>Alla dimensioner som du vill filtrera eller gruppera efter måste redan spåras i [!DNL Commerce Intelligence]. Om du inte hittar den önskade dimensionen kan du behöva börja spåra en ny datakolumn i databasen via [data warehouse](../data-warehouse-mgr/tour-dwm.md) sida.


**Så här tar du bort dimensioner från ett mått:**

1. Gå till **[!UICONTROL Manage Data > Metrics]**.

1. Klicka **[!UICONTROL Edit]** på mätvärdena vill du ha en ny dimension.

1. Under `Dimensions` markerar du kryssrutan i borttagningskolumnen bredvid de dimensioner som du vill ta bort.

>[!NOTE]
>
>Även efter att du har tagit bort en dimension finns den fortfarande som en kolumn i tabellen i Data warehouse. Du kan lägga tillbaka det i alla mätvärden och skapa nya mätvärden med dessa mått. Ta bort den datakolumn som en dimension motsvarar från [!DNL Commerce Intelligence]tar du bara bort spåret från datakolumnen via [data warehouse](../data-warehouse-mgr/tour-dwm.md) sida.

## Relaterad dokumentation

* [Metodtips för segmentering och filtrering](../../best-practices/segment-filter.md)
