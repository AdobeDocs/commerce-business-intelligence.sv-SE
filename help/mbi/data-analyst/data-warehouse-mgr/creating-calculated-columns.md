---
title: Skapa beräknade kolumner
description: Lär dig hur du konsoliderar data från olika källor.
exl-id: 668cbc77-6a96-4687-9f40-3635b1be5c66
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 0%

---

# Skapa beräknade kolumner

När du analyserar data är det praktiskt att konsolidera data från olika källor. vill gruppera intäkterna genom att hämta in data och länka data från `orders` tabell och [!DNL Google Analytics] data? Kanske vill ni gruppera intäkterna efter kundkön eller koppla ett kundattribut till transaktionsdata för segmentering. Det här avsnittet handlar om hur man gör just det.

Innan du börjar rekommenderar Adobe att du granskar [Guide för beräknade kolumntyper](../../data-analyst/data-warehouse-mgr/calc-column-types.md) om du vill ha information om vilka typer av kolumner du kan skapa i Data warehouse Manager, tillsammans med definitioner och exempel.

1. Kom igång genom att klicka **[!DNL Manage Data > Data Warehouse]**.

1. Klicka på den tabell där du vill skapa en kolumn. Om du till exempel vill skapa en `Customer Gender` kolumn för intäktssegmentering väljer du `sales_flat_order` tabell.

1. Tabellschemat visas. Klicka **[!UICONTROL Create New Column]**.

1. Ge kolumnen ett namn. Till exempel: `Customer Gender`.

1. Markera kolumndefinitionen. Det är här [Guide för beräknade kolumntyper](../data-warehouse-mgr/calc-column-types.md) kommer väl till pass!

1. För vissa typer av kolumner krävs lite mer information för att kolumnen ska kunna skapas:

   * För `One to Many` (förenad) och `Many to One` (aggregerade) kolumner måste du markera tabellerna och kolumnerna.

   * För `Same Table calculation`måste du välja önskat datumfält i listrutan.

Om du skapar en `One to Many` (förenad) eller `Many to One` (sammanställd) kolumn måste du välja en sökväg för att koppla ihop de två tabellerna. I det här steget kan du antingen använda en befintlig bana eller skapa en.

>[!NOTE]
>
>Kom ihåg att definiera tabellen som antingen många eller ett.

* Om du vill kan du använda [filter](../../data-user/reports/ess-manage-data-filters.md) till den nya kolumnen.

* När du är klar klickar du på **[!UICONTROL Save]**.

Din nya kolumn visas i den aktuella tabellen med en `Pending` status. När nästa uppdatering är klar är kolumnen tillgänglig för användning i mätvärden och rapporter.

## Referenskarta {#map}

Om du har problem med att komma ihåg vad alla indata är när du skapar en beräknad kolumn, kan du försöka behålla referenskartan när du skapar:

![](../../assets/Calculated_Columns_Example.png)

## Relaterad dokumentation

* [Beräknade kolumntyper](../data-warehouse-mgr/calc-column-types.md)
* [Avancerade beräknade kolumntyper](../data-warehouse-mgr/adv-calc-columns.md)
* [Byggnad [!DNL Google ECommerce] dimensioner med beställnings- och kunddata](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
