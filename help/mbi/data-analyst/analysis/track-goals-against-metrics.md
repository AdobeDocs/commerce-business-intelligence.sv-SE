---
title: Spåra mål mot mätvärden
description: Lär dig hur du skapar en kontrollpanel som hjälper dig att spåra dina affärsmål mot dina faktiska data - inklusive intäkter, nya registrerade användare och beställningar över tid.
exl-id: 9d621f40-f9c2-4310-bd96-a46ab7159930
role: Admin, User
feature: Data Warehouse Manager, Reports, Dashboards, Reports
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%

---

# Spåra mål mot prestandamått

De flesta klienter vill spåra sina **affärsmål**, men inser inte att detta är möjligt i [!DNL Adobe Commerce Intelligence]. Det här avsnittet visar hur du konfigurerar en kontrollpanel som hjälper dig att spåra dina affärsmål mot dina faktiska data - inklusive intäkter, nya registrerade användare och beställningar över tid. Du får också lära dig hur du jämför års prestanda, allt på en kontrollpanel som den här:

![Kontrollpanelen visar målspårning mot faktiska mätresultat](../../assets/Goals-_dashboard_2.png)

Innan du börjar bör du granska [filöverföringen](../importing-data/connecting-data/using-file-uploader.md) och se till att du har definierat dina affärsmål för en viss period.

## Komma igång

Du måste först ladda upp en fil som innehåller specifika mål per dag, månad och kvartal för ditt företag.

Du kan använda [filöverföringen](../importing-data/connecting-data/using-file-uploader.md) och bilden nedan för att formatera filen. De vanligaste målen som klienter spårar i [!DNL Commerce Intelligence] är Beställningar, Intäkter och Nya registrerade konton.

![Excel-kalkylbladsmall för att spåra mål och mätvärden](../../assets/Goals-_Excel.png)

## Mått

Skapa ett nytt mått för varje mål. Om du till exempel överför månatliga intäkter och ordermål måste du skapa två nya mätvärden:

* **Månadsintäktsmål**
* I tabellen **`Monthly goals`**
* Detta mått utför en **summa**
* I kolumnen **`Revenue target`**
* Ordnad efter tidsstämpeln **`Month`**

* **Mål för månadsbeställningar**
* I tabellen **`Monthly goals`**
* Detta mått utför en **summa**
* I kolumnen **`Orders target`**
* Ordnad efter tidsstämpeln **`Month`**

* **Mål för nya registrerade konton** varje månad
* I tabellen **`Monthly goals`**
* Detta mått utför en **summa**
* I kolumnen **`New registered accounts target`**
* Ordnad efter tidsstämpeln **`Month`**

## Rapporter

Det är praktiskt att ha en blandning av statiska värden och visuella diagram när du analyserar dina mål. Nedan visas tre exempelrapporter som hjälper dig att komma igång med att följa upp dina intäkter.

* **Återstående intäkter för att uppnå målet**
* Mått `A`: `Revenue`
* &#x200B;
  [!UICONTROL -mått]: `Revenue`

* Mått `B`: `Target Revenue`
* [!UICONTROL Metric]: `Monthly Revenue Target`

* [!UICONTROL Formula]: `Revenue left to achieve target`
* &#x200B;
  [!UICONTROL -formel]: `(B-A)`
* &#x200B;
  [!UICONTROL Format]: `Number`

* [!UICONTROL Time period]: (oavsett vilken tidsperiod du vill ha)
* &#x200B;
  [!UICONTROL Interval]: `Month`
* &#x200B;
  [!UICONTROL -diagramtyp]: `Scalar`

* **Intäktsmål**
* Mått `A`: `Revenue`
* &#x200B;
  [!UICONTROL -mått]: `Revenue`

* Mått `B`: `Target Revenue`
* [!UICONTROL Metric]: `Monthly Revenue Target`

* Mått `C`: `Revenue (amount change since previous year)` (dölj)
* &#x200B;
  [!UICONTROL -mått]: `Revenue`
* [!UICONTROL Perspective]: `Amount change vs. Previous year`

* [!UICONTROL Formula]: (Den här månaden förra året)
* &#x200B;
  [!UICONTROL -formel]: `(A-C)`
* &#x200B;
  [!UICONTROL Format]: `Currency`

* Stäng av `Multiple Y-Axes`
* [!UICONTROL Time period]: (oavsett vilken tidsperiod du vill ha)*
* &#x200B;
  [!UICONTROL Interval]: `Month`
* [!UICONTROL Chart Type]: `Line Chart`

När du har slutfört rapporterna för intäktsmål kan du skapa identiska rapporter för mål runt order, registrerade konton eller andra värden som du har inkluderat i målfilöverföringen.

När du har kompilerat alla rapporter kan du ordna dem på kontrollpanelen som du vill. Resultatet kan se ut som bilden högst upp på den här sidan.
