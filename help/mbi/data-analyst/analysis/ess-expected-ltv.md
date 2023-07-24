---
title: Förväntad analys av livstidsvärde (LTV) (grundläggande)
description: Lär dig hur ni skapar analyser för att förstå era nuvarande kunders livstidsvärde och förutse hur livstidsvärdet ökar med fler order.
exl-id: e6f02cf6-f542-4768-969c-3ec998a7caa9
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---

# Förväntad analys av livstidsvärde

Att förutse kundernas livstidsvärde när de gör fler beställningar är en av de viktigaste aspekterna i alla typer av företag av alla storlekar.

Nedan följer stegen för att skapa analyser för att förstå era nuvarande kunders livstidsvärde och förutse hur livstidsvärdet ökar med fler order.

![förväntat livstid](../../assets/expected_ltv_720.png)

## Bygga ett mått

Det första steget är att skapa ett nytt mått med följande steg:
* Navigera till **[!UICONTROL Manage Data > Metrics]**
   * Visa befintlig **[!UICONTROL Avg lifetime revenue]**.

  >[!NOTE]
  >
  >Tabellen som måttet är uppbyggt på (troligen `customer_entity` eller `sales_order` beroende på butikens förmåga att acceptera utcheckning av gäster.)

   * Klicka **[!UICONTROL Create New Metric]** och markera tabellen ovan.
   * Detta mått utför en **Median** på `Customer's lifetime revenue` kolumn, sorterad efter `created_at`.
      * [!UICONTROL Filters]:
         * Lägg till `Customers we count (Saved Filter Set)` (eller `Registered accounts we count`)

   * Ge måttet ett namn, till exempel `Median lifetime revenue`.

## Skapa en instrumentpanel

När mätvärdena har skapats kan du **skapa en kontrollpanel** genom att göra detta:
* Navigera till **[!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**.
* Ge instrumentpanelen ett namn som `Expected LTV`.

* Här skapar du och lägger till alla rapporter.

## Skapar rapporter

>[!NOTE]
>
>På **[!UICONTROL Time Period:]**, anges tidsperioden för varje rapport som `All-time`. Du kan ändra detta efter dina analysbehov. Adobe rekommenderar att alla rapporter på kontrollpanelen täcker samma tidsperiod, till exempel `All time`, `Year-to-date`, eller `Last 365 days`.

* **[!UICONTROL Average LTV (all)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL-intervall]: `None`
   * [!UICONTROL Chart Type]: `Number (scalar)`

* **[!UICONTROL Average LTV (customers / non-guest checkout)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Lägg till [!UICONTROL filters]:
         * [`A`] `Customer's group code` **Inte lika med** `Not Logged In`
         * [`B`] `Customer's lifetime number of orders` **Större än**`0`

   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL-intervall]: `None`
   * [!UICONTROL Chart Type]: `Number (scalar)`

* **[!UICONTROL Average and Median LTV]**
   * Mått `1`: `Avg lifetime revenue`
   * Mått `2`: `Median lifetime revenue`
   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `By Month`
   * 
     [!UICONTROL-diagramtyp]: `Line`
   * Avmarkera `Multiple Y-Axes`

* **LTV efter antal beställningar under hela livstiden**
   * Mått `1`: `Avg lifetime revenue`
   * Mått `2`: `New customers`
   * [!UICONTROL Time period]: `All time`
   * 
     [!UICONTROL-intervall]: `None`
   * [!UICONTROL Group by]: `Customer's lifetime number of orders`
   * 
     [!UICONTROL-diagramtyp]: `Line`

  >[!NOTE]
  >
  >Lägg inte till alla värden för `Customer's lifetime number of orders`. Titta istället på en punkt där antalet nya kunder når ett litet antal och manuellt lägga till varje kunds antal beställningsvärden för hela livstiden till den punkten. Om det till exempel finns 200 kunder på en order, 75 på två, 15 på tre och 3 på fyra lägger du till *1, 2 och 3*.

* Lägg till befintlig [!UICONTROL Avg customer lifetime revenue by cohort] rapport.

När du har skapat rapporterna kan du se bilden högst upp i det här avsnittet för att se hur du kan ordna rapporterna på din kontrollpanel.
