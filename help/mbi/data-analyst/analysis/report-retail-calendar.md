---
title: Rapportering i en butikskalender
description: Lär dig hur du konfigurerar strukturen så att du kan använda en 4-5-4-kalender i din [!DNL Commerce Intelligence] konto.
exl-id: 3754151c-4b0f-4238-87f2-134b8409e32b
source-git-commit: 4cad1e05502630e13f7a2d341f263140a02b3d82
workflow-type: tm+mt
source-wordcount: '627'
ht-degree: 0%

---

# Rapportering i en butikskalender

I det här avsnittet visas hur du konfigurerar strukturen för att använda en [4-5-4 butikskalender](https://nrf.com/resources/4-5-4-calendar) inom [!DNL Adobe Commerce Intelligence] konto. Den visuella rapportbyggaren tillhandahåller otroligt flexibla tidsintervall, intervall och oberoende inställningar. Alla dessa inställningar fungerar dock med den traditionella månadskalendern.

Eftersom många kunder ändrar sin kalender så att den använder återförsäljnings- eller redovisningsdatum visar stegen nedan hur de arbetar med data och skapar rapporter med hjälp av återförsäljningsdatum. Instruktionerna nedan hänvisar till butikskalendern för 4-5-4, men du kan ändra dem för alla specifika kalendrar som teamet använder, oavsett om det är ekonomiska eller bara en anpassad tidsram.

Innan du börjar bör du granska [filöverföringen](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) och se till att du har förlängt `.csv` -fil. Detta garanterar att datumen täcker alla dina historiska data och för in datumen i framtiden.

Denna analys innehåller [avancerade beräknade kolumner](../data-warehouse-mgr/adv-calc-columns.md).

## Komma igång

Du kan [ladda ned](../../assets/454-calendar.csv) a `.csv` version av 4-5-4-kalendern för detaljhandelsår 2014 till 2017. Du kan behöva justera den här filen i enlighet med din interna butikskalender och utöka datumintervallet för att stödja din historiska och aktuella tidsram. När du har hämtat filen använder du filöverföringsprogrammet för att skapa en tabell för butikskalender i [!DNL Commerce Intelligence] data warehouse. Om du använder en oförändrad version av 4-5-4-kalendern för återförsäljning måste du se till att strukturen och datatyperna för fälten i den här tabellen matchar följande:

| Kolumnnamn | Kolumndatatyp | Primär nyckel |
| --- | --- | --- |
| `Date Retail` | `Date & Time` | `Yes` |
| `Year Retail` | `Whole Number` | `No` |
| `Quarter Retail` | `Whole Number` | `No` |
| `Month Number Retail` | `Whole Number` | `No` |
| `Week Retail` | `Whole Number` | `No` |
| `Month Name Retail` | `Text` (Upp till 255 tecken) | `No` |
| `Week Number of Month Retail` | `Whole Number` | `No` |

{style="table-layout:auto"}

## Kolumner att skapa

* **sales\_order** table
   * `INPUT` `created\_at` (åååå-mm-dd 00:00:00)
      * [!UICONTROL Column type]: – `Same table > Calculation`
      * [!UICONTROL Inputs]: – `created\_at`
      * [!UICONTROL Datatype]: – `Datetime`
      * [!UICONTROL Calculation]: - ` case when A is null then null else to\_char(A, 'YYYY-MM-DD 00:00:00') end`

* **Butikskalender** filöverföringsregister
   * **Aktuellt datum**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]: `Date Retail`
      * 
         [!UICONTROL-datatyp]: `Datetime`
      * [!UICONTROL Calculation]: `case when A is null then null else to\_char(now(), 'YYYY-MM-DD 00:00:00') end`

         >[!NOTE]
         >
         >The `now()` funktionen ovan är specifik för PostgreSQL. Fast de [!DNL Commerce Intelligence] data warehouse ligger på PostgreSQL, vissa kan ligga på Redshift. Om beräkningen ovan returnerar ett fel kan du behöva använda funktionen för omflyttning `getdate()` i stället för `now()`.
   * **Aktuellt år** (Måste skapas av supportanalytiker)
      * [!UICONTROL Column type]: E`vent Counter`
      * [!UICONTROL Local Key]: `Current date`
      * [!UICONTROL Remote Key]: `Retail calendar.Date Retail`
      * 
         [!UICONTROL Operation]: `Max`
      * [!UICONTROL Operation value]: `Year Retail`
   * **Ingår i aktuellt år? (Ja/Nej)**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * 
         [!UICONTROL-datatyp]: `String`
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when A = B then 'Yes' else 'No' end`
   * **Ingår i föregående år? (Ja/Nej)**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * 
         [!UICONTROL-datatyp]: String
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when (A = (B-1)) then 'Yes' else 'No' end`


* **sales\_order** table
   * **Skapad\_at (år för återförsäljning)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Sökväg -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * Välj en [!UICONTROL table]: `Retail Calendar`
      * Välj en [!UICONTROL column]: `Year Retail`
   * **Skapad\_at (återförsäljningsvecka)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Sökväg -
         * [!UICONTROL Many]: sales\_order.\[INPUT\] skapad (åååå-mm-dd 00):00:00
         * [!UICONTROL One]: Butikskalender.Datum Detaljhandel
      * Välj en [!UICONTROL table]: `Retail Calendar`
      * Välj en [!UICONTROL column]: `Week Retail`
   * **Skapad\_at (återförsäljningsmånad)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Bana
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: `Retail Calendar.Date Retail`
      * Välj en [!UICONTROL table]: `Retail Calendar`
      * Välj en [!UICONTROL column]: `Month Number Retail`
   * **Vill du inkludera i föregående år? (Ja/Nej)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Sökväg -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: Detaljhandel `Calendar.Date Retail`
      * Välj en [!UICONTROL table]: `Retail Calendar`
      * Välj en [!UICONTROL column]: `Include in previous retail year? (Yes/No)`
   * **Vill du inkludera i aktuellt år? (Ja/Nej)**
      * [!UICONTROL Column type]: `One to Many > JOINED\_COLUMN`
      * Sökväg -
         * [!UICONTROL Many]: `sales\_order.\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)`
         * [!UICONTROL One]: Detaljhandel `Calendar.Date Retail`
      * Välj en [!UICONTROL table]: `Retail Calendar`
      * Välj en [!UICONTROL column]: `Include in current retail year? (Yes/No)`

## Mått

Obs! Inga nya mätvärden behövs för den här analysen. Se dock till att [lägg till de nya kolumnerna som du har skapat i tabellen sales\_order som dimensioner](../data-warehouse-mgr/manage-data-dimensions-metrics.md) för alla mått i tabellen sales\_order innan du fortsätter med rapporterna.

## Rapporter

* **Veckobeställningar - detaljhandelskalender (ÅÅÅ)**
   * Mått `A`: `2017`
      * [!UICONTROL Metric]: Antal order
      * [!UICONTROL Filter]:
         * Skapad\_at (återförsäljningsår) = 2017
   * Mått `B`: `2016`
      * [!UICONTROL Metric]: Antal order
      * [!UICONTROL Filter]:
         * Skapad\_at (återförsäljningsår) = 2016
   * Mått `C`: `2015`
      * [!UICONTROL Metric]: `Number of orders`
      * [!UICONTROL Filter]:
         * `Created\_at (retail Year) = 2015`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL Interval]: `None`
   * 
      [!UICONTROL Group by]: `Created\_at` (retail week)
   * 
      [!UICONTROL Chart type]: `Line`
      * Stäng av `multiple Y-axes`

* **Översikt över butikskalender (aktuellt år per månad)**
   * Mått `A`: `Revenue`
      * 
         [!UICONTROL-mått]: `Revenue`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * Mått `B`: `Orders`
      * [!UICONTROL Metric]: `Number of orders`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * Mått `C`: `Avg order value`
      * [!UICONTROL Metric]: `Avg order value`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL Interval]: `None`
   * 
      [!UICONTROL Group by]: `Created\_at` (retail month)
   * 

      [!UICONTROL Chart type]: `Line`

* **Översikt över butikskalender (föregående år per månad)**
   * Mått `A`: `Revenue`
      * 
         [!UICONTROL-mått]: `Revenue`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * Mått `B`: `Orders`
      * [!UICONTROL Metric]: Antal order
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * Mått `C`: `Avg order value`
      * [!UICONTROL Metric]: `Avg order value`
      * [!UICONTROL Filter]:
         * 
            [!UICONTROL Include current retail year?]: `Yes`
   * [!UICONTROL Time period]: `All time`
   * 
      [!UICONTROL Interval]: `None`
   * 
      [!UICONTROL Group by]: `Created\_at` (retail month)
   * 

      [!UICONTROL Chart type]: `Line`

## Nästa steg

Ovanstående beskriver hur du konfigurerar en butikskalender så att den är kompatibel med alla mätvärden som bygger på din `sales\_order` tabell (som `Revenue` eller `Orders`). Du kan även utöka den för att stödja butikskalendern för mätvärden som bygger på valfri tabell. Det enda kravet är att det här registret har ett giltigt datetime-fält som kan användas för att ansluta till butikskalendertabellen.

Om du till exempel vill visa kundnivåstatistik i en 4-5-4-kalender skapar du en `Same Table` beräkning i `customer\_entity` tabell, liknar `\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)` som beskrivs ovan. Du kan sedan använda den här kolumnen för att återskapa `One to Many` JOINED\_COLUMN-beräkningar (som `Created_at (retail year)`) och `Include in previous retail year? (Yes/No)` genom att ansluta `customer\_entity` tabellen till `Retail Calendar` tabell.

Glöm inte att [lägga till alla nya kolumner som dimensioner till mått](../data-warehouse-mgr/manage-data-dimensions-metrics.md) innan du skapar nya rapporter.
