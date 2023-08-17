---
title: Formler
description: Lär dig hur du använder formler.
exl-id: b6432d93-739f-410c-b732-e09a278f8dae
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# Formler

En formel kombinerar flera mätvärden och matematisk logik för att besvara en fråga. Hur mycket av intäkterna per produkt under semestersäsongen genererades till exempel av nya kunder?

![Heldagsförsäljning på Dashboard](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-holiday-sales-dashboard.png)

## Steg 1: Skapa den grundläggande rapporten

1. Välj `Report Builder`.

1. Klicka **[!UICONTROL Add Metric]** och välj det första måttet för rapporten.

   I det här exemplet `Revenue by products ordered` mätvärden används.

1. Klicka **[!UICONTROL Add Metric]** igen och välj det andra måttet för rapporten.

   I det här exemplet `New Customers` mätvärden används.

1. Klicka på **[!UICONTROL Details]** för att visa information om varje mätvärde.

   ![Intäkter efter beställda produkter](../../assets/magento-bi-report-builder-revenue-by-products.png)

1. Klicka på namnet på varje mätvärde i sidofältet för att öppna inställningssidan på en ny webbläsarflik. Bläddra nedåt för att se alla komponenter i måttet, inklusive måttfrågan, filtret och dimensionerna.

   ![Måttinställningar](../../assets/magento-bi-report-builder-revenue-by-products-metric-detail.png)

1. Om du vill återgå till rapporten klickar du på fliken för föregående webbläsare.

1. Håll markören över ett fåtal datapunkter på varje rad för att se hur mycket varje mätvärde har.

## Steg 2: Lägg till en formel

1. Klicka på längst upp i sidlisten **[!UICONTROL Add Formula]**.

   Formelrutan visar mätvärden som tillgängliga indata `A` och `B`och innehåller en inmatningsruta där du kan ange formeln.

   Gör följande:

   * I `Enter your Formula` inmatningsruta, ange `A/B`.

     Detta dividerar intäkterna efter beställda produkter med antalet nya kunder.

   * Ange `Select format` till `123Number`.

   * Ersätt `Untitled` med ett namn för formeln.

   ![Formelinställningar](../../assets/magento-bi-report-builder-revenue-by-products-add-formula-detail.png)

1. När du är klar klickar du på **[!UICONTROL Apply]**.

   Rapporten har nu en ny rad för formeln, `New Customer Revenue`och i sidofältet visas de totala intäkterna för nya kunder.

   ![Rapport med formel](../../assets/magento-bi-report-builder-revenue-by-products-formula-report.png)

## Steg 3: Lägg till ett datumintervall

1. Klicka **[!UICONTROL Date Range]** längst upp till höger.

1. På `Fixed Date Range` gör du så här:

   * Välj datumintervall i kalendrarna.

     I det här exemplet kommer julsäsongen `November 1` via `December 31`.

   * Under `Select Time Interval`, välja `Day`.

     ![Fast datumintervall](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-fixed-date-range.png)

   * När du är klar klickar du på **[!UICONTROL Apply]**.

   Rapporten är nu begränsad till semestersäsongen, med en datapunkt för varje dag.

   ![Fast datumintervall](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-fixed-date-range-report.png)

## Steg 4: Spara rapporten

I det här steget sparar du rapporten som ett diagram och som en tabell.

1. Klicka `Untitled Report` överst på sidan och ange en beskrivande rubrik. I det här exemplet är rapporttiteln `2017 Holiday Sales`.

   Gör sedan följande:

   * Klicka på i det övre högra hörnet **[!UICONTROL Save]**.

   * För `Type`, acceptera standardinställningen `Chart` inställning.

   * Välj `Dashboard` om rapporten ska vara tillgänglig.

   * Klicka på **[!UICONTROL Save to Dashboard]**.

1. Klicka på rapporttiteln och ändra namnet. I det här exemplet ändras rapporttiteln till `2017 Holiday Sales Data`.

   Gör sedan följande:

   * Klicka på i det övre högra hörnet **[!UICONTROL Save a Copy]**.

   * Ange `Type` till `Table`.

   * Välj `Dashboard` om rapporten ska vara tillgänglig.

   * Klicka på **[!UICONTROL Save a Copy to Dashboard]**.

1. Gör något av följande om du vill visa rapporterna på kontrollpanelen:

   * Klicka **[!UICONTROL Go to Dashboard]** i meddelandet längst upp på sidan.

   * Välj **[!UICONTROL Dashboards]**. Klicka på namnet på den aktuella instrumentpanelen för att visa listan. Klicka sedan på namnet på kontrollpanelen där rapporten sparades.
