---
title: Spåra mål mot mätvärden
description: Lär dig hur du skapar en kontrollpanel som hjälper dig att spåra dina affärsmål mot dina faktiska data - inklusive intäkter, nya registrerade användare och beställningar över tid.
exl-id: 9d621f40-f9c2-4310-bd96-a46ab7159930
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 0%

---

# Spåra mål mot prestandamått

De flesta kunder vill spåra sina **verksamhetsmål**, men inser inte att detta är möjligt i [!DNL Adobe Commerce Intelligence]. Det här avsnittet visar hur du konfigurerar en kontrollpanel som hjälper dig att spåra dina affärsmål mot dina faktiska data - inklusive intäkter, nya registrerade användare och beställningar över tid. Du får också lära dig hur du jämför års prestanda, allt på en kontrollpanel som den här:

![](../../assets/Goals-_dashboard_2.png)

Innan du börjar bör du granska [filöverföring](../importing-data/connecting-data/using-file-uploader.md) och se till att du har definierat dina affärsmål för en viss period.

## Komma igång

Du måste först överföra en fil som innehåller specifika mål per dag, månad och kvartal för ditt företag.

Du kan använda [filöverföring](../importing-data/connecting-data/using-file-uploader.md) och bilden nedan för att formatera filen. De vanligaste målen som kunderna spårar in [!DNL Commerce Intelligence] innehåller beställningar, intäkter och nya registrerade konton.

![](../../assets/Goals-_Excel.png)

## Mått

Skapa ett nytt mått för varje mål. Om du till exempel överför månatliga intäkter och ordermål måste du skapa två nya mätvärden:

* **Månadsintäktsmål**
* I **`Monthly goals`** table
* Detta mått utför en **Summa**
* På **`Revenue target`** kolumn
* Beställd av **`Month`** tidsstämpel

* **Mål för månadsorder**
* I **`Monthly goals`** table
* Detta mått utför en **Summa**
* På **`Orders target`** kolumn
* Beställd av **`Month`** tidsstämpel

* **Mål för nya registrerade konton varje månad**
* I **`Monthly goals`** table
* Detta mått utför en **Summa**
* På **`New registered accounts target`** kolumn
* Beställd av **`Month`** tidsstämpel

## Rapporter

Det är praktiskt att ha en blandning av statiska värden och visuella diagram när du analyserar dina mål. Nedan visas tre exempelrapporter som hjälper dig att komma igång med att följa upp dina intäkter.

* **Återstående intäkter för att uppnå målet**
* Mått `A`: `Revenue`
* 
  [!UICONTROL-mått]: `Revenue`

* Mått `B`: `Target Revenue`
* [!UICONTROL Metric]: `Monthly Revenue Target`

* [!UICONTROL Formula]: `Revenue left to achieve target`
* 
  [!UICONTROL-formel]: `(B-A)`
* 
  [!UICONTROL Format]: `Number`

* [!UICONTROL Time period]: (Vilken tidsperiod du vill ha)
* 
  [!UICONTROL Interval]: `Month`
* 
  [!UICONTROL-diagramtyp]: `Scalar`

* **Intäktsmål**
* Mått `A`: `Revenue`
* 
  [!UICONTROL-mått]: `Revenue`

* Mått `B`: `Target Revenue`
* [!UICONTROL Metric]: `Monthly Revenue Target`

* Mått `C`: `Revenue (amount change since previous year)` (dölj)
* 
  [!UICONTROL-mått]: `Revenue`
* [!UICONTROL Perspective]: `Amount change vs. Previous year`

* [!UICONTROL Formula]: (Den här månaden förra året)
* 
  [!UICONTROL-formel]: `(A-C)`
* 
  [!UICONTROL Format]: `Currency`

* Stäng av `Multiple Y-Axes`
* [!UICONTROL Time period]: (Vilken tidsperiod du vill ha)*
* 
  [!UICONTROL Interval]: `Month`
* [!UICONTROL Chart Type]: `Line Chart`

När du har slutfört rapporterna för intäktsmål kan du skapa identiska rapporter för mål runt order, registrerade konton eller andra värden som du har inkluderat i målfilöverföringen.

När du har kompilerat alla rapporter kan du ordna dem på kontrollpanelen som du vill. Resultatet kan se ut som bilden högst upp på den här sidan.
