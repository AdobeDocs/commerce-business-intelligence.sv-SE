---
title: Rapportering i en butikskalender
description: Lär dig hur du konfigurerar strukturen så att den använder en 4-5-4-kalender för återförsäljning inom ditt [!DNL Commerce Intelligence] konto.
exl-id: 3754151c-4b0f-4238-87f2-134b8409e32b
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '651'
ht-degree: 0%

---

# Rapportering i en butikskalender

I det här avsnittet visas hur du konfigurerar strukturen så att den använder en [4-5-4-butikskalender](https://nrf.com/resources/4-5-4-calendar) i ditt [!DNL Adobe Commerce Intelligence]-konto. Den visuella rapportbyggaren tillhandahåller otroligt flexibla tidsintervall, intervall och oberoende inställningar. Alla dessa inställningar fungerar dock med den traditionella månadskalendern.

Eftersom många kunder ändrar sin kalender så att den använder återförsäljnings- eller redovisningsdatum visar stegen nedan hur de arbetar med data och skapar rapporter med hjälp av återförsäljningsdatum. Instruktionerna nedan hänvisar till butikskalendern för 4-5-4, men du kan ändra dem för alla specifika kalendrar som teamet använder, oavsett om det är ekonomiska eller bara en anpassad tidsram.

Innan du börjar bör du granska [filöverföringsprogrammet](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) och se till att du har förlängt filen `.csv`. Detta garanterar att datumen täcker alla dina historiska data och för in datumen i framtiden.

Den här analysen innehåller [avancerade beräknade kolumner](../data-warehouse-mgr/adv-calc-columns.md).

## Komma igång

Du kan [hämta](../../assets/454-calendar.csv) en `.csv`-version av 4-5-4-butikskalendern för 2014 till 2017. Du kan behöva justera den här filen i enlighet med din interna butikskalender och utöka datumintervallet för att stödja din historiska och aktuella tidsram. När du har hämtat filen kan du använda filöverföringsprogrammet för att skapa en butikskalendertabell i Datan Warehouse [!DNL Commerce Intelligence]. Om du använder en oförändrad version av 4-5-4-kalendern för återförsäljning måste du se till att strukturen och datatyperna för fälten i den här tabellen matchar följande:

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

* tabellen **sales\_order**
   * `INPUT` `created\_at` (åååå-mm-dd 00:00:00)
      * [!UICONTROL Column type]: - `Same table > Calculation`
      * [!UICONTROL Inputs]: - `created\_at`
      * [!UICONTROL Datatype]: - `Datetime`
      * [!UICONTROL Calculation]: - ` case when A is null then null else to\_char(A, 'YYYY-MM-DD 00:00:00') end`

* **Butikskalender** filöverföringsregister
   * **Aktuellt datum**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]: `Date Retail`
      * &#x200B;

        [!UICONTROL -datatyp]: `Datetime`
      * [!UICONTROL Calculation]: `case when A is null then null else to\_char(now(), 'YYYY-MM-DD 00:00:00') end`

        >[!NOTE]
        >
        >Funktionen `now()` ovan är specifik för PostgreSQL. Även om de flesta [!DNL Commerce Intelligence] datalagerställen finns på PostgreSQL kan vissa finnas på Redshift. Om beräkningen ovan returnerar ett fel kan du behöva använda funktionen `getdate()` för omflyttning i stället för `now()`.

   * **Aktuellt återförsäljningsår** (måste skapas av supportanalytiker)
      * [!UICONTROL Column type]: E`vent Counter`
      * [!UICONTROL Local Key]: `Current date`
      * [!UICONTROL Remote Key]: `Retail calendar.Date Retail`
      * &#x200B;

        [!UICONTROL Operation]: `Max`
      * [!UICONTROL Operation value]: `Year Retail`
   * **Ingår i aktuellt år? (Ja/Nej)**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * &#x200B;

        [!UICONTROL -datatyp]: `String`
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when A = B then 'Yes' else 'No' end`
   * **Ingår i föregående år? (Ja/Nej)**
      * [!UICONTROL Column type]: `Same table > Calculation`
      * [!UICONTROL Inputs]:
         * `A` - `Year Retail`
         * `B` - `Current retail year`
      * &#x200B;

        [!UICONTROL -datatyp]: String
      * [!UICONTROL Calculation]: `case when A is null or B is null then null when (A = (B-1)) then 'Yes' else 'No' end`

* tabellen **sales\_order**
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
         * [!UICONTROL Many]: sales\_order.\[INPUT\] skapad (åååå-mm-dd 00:00:00
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

Obs! Inga nya mätvärden behövs för den här analysen. Se dock till att [lägga till de nya kolumnerna som du har skapat i tabellen sales\_order som dimensioner](../data-warehouse-mgr/manage-data-dimensions-metrics.md) för alla mått i tabellen sales\_order innan du fortsätter med rapporterna.

## Rapporter

* **Veckobeställningar - butikskalender (YearY)**
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
   * &#x200B;

     [!UICONTROL Interval]: `None`
   * &#x200B;

     [!UICONTROL Group by]: `Created\_at` (retail week)
   * &#x200B;

     [!UICONTROL Chart type]: `Line`
      * Stäng av `multiple Y-axes`

* **Översikt över butikskalender (aktuellt år per månad)**
   * Mått `A`: `Revenue`
      * &#x200B;

        [!UICONTROL -mått]: `Revenue`
      * [!UICONTROL Filter]:
         * &#x200B;

           [!UICONTROL Include current retail year?]: `Yes`
   * Mått `B`: `Orders`
      * [!UICONTROL Metric]: `Number of orders`
      * [!UICONTROL Filter]:
         * &#x200B;

           [!UICONTROL Include current retail year?]: `Yes`
   * Mått `C`: `Avg order value`
      * [!UICONTROL Metric]: `Avg order value`
      * [!UICONTROL Filter]:
         * &#x200B;

           [!UICONTROL Include current retail year?]: `Yes`
   * [!UICONTROL Time period]: `All time`
   * &#x200B;

     [!UICONTROL Interval]: `None`
   * &#x200B;

     [!UICONTROL Group by]: `Created\_at` (retail month)
   * &#x200B;

     [!UICONTROL Chart type]: `Line`

* **Översikt över butikskalender (föregående år per månad)**
   * Mått `A`: `Revenue`
      * &#x200B;

        [!UICONTROL -mått]: `Revenue`
      * [!UICONTROL Filter]:
         * &#x200B;

           [!UICONTROL Include current retail year?]: `Yes`
   * Mått `B`: `Orders`
      * [!UICONTROL Metric]: Antal order
      * [!UICONTROL Filter]:
         * &#x200B;

           [!UICONTROL Include current retail year?]: `Yes`
   * Mått `C`: `Avg order value`
      * [!UICONTROL Metric]: `Avg order value`
      * [!UICONTROL Filter]:
         * &#x200B;

           [!UICONTROL Include current retail year?]: `Yes`
   * [!UICONTROL Time period]: `All time`
   * &#x200B;

     [!UICONTROL Interval]: `None`
   * &#x200B;

     [!UICONTROL Group by]: `Created\_at` (retail month)
   * &#x200B;

     [!UICONTROL Chart type]: `Line`

## Nästa steg

Ovanstående beskriver hur du konfigurerar en butikskalender så att den är kompatibel med alla mått som är inbyggda i din `sales\_order`-tabell (till exempel `Revenue` eller `Orders`). Du kan även utöka den för att stödja butikskalendern för mätvärden som bygger på valfri tabell. Det enda kravet är att det här registret har ett giltigt datetime-fält som kan användas för att ansluta till butikskalendertabellen.

Om du till exempel vill visa kundnivåstatistik för en 4-5-4-kalender för återförsäljning skapar du en `Same Table`-beräkning i tabellen `customer\_entity` som liknar `\[INPUT\] created\_at (yyyy-mm-dd 00:00:00)` som beskrivs ovan. Du kan sedan använda den här kolumnen för att reproducera beräkningarna `One to Many` JOINED\_COLUMN (som `Created_at (retail year)`) och `Include in previous retail year? (Yes/No)` genom att koppla tabellen `customer\_entity` till tabellen `Retail Calendar`.

Glöm inte att [lägga till alla nya kolumner som dimensioner till mätvärden](../data-warehouse-mgr/manage-data-dimensions-metrics.md) innan du skapar nya rapporter.
