---
title: Skapa och använda en SQL-beräknad kolumn
description: Lär dig hur avancerade kolumner kan skapas i form av SQL Calculation-kolumner i den nya Adobe Commerce Intelligence-arkitekturen.
exl-id: f16e4ee4-ed73-4ddb-b701-1fe3db14346a
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, SQL Report Builder, Commerce Tables
source-git-commit: 8090c2e0f17f0e8d3bdec668ce546206bf024691
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 0%

---

# Skapa en SQL-beräknad kolumn

I det här avsnittet beskrivs syftet med och användningsområdena för `Calculation` kolumntyp, som kan läggas till i tabeller med [Data Warehouse Manager](../data-warehouse-mgr/tour-dwm.md). Nedan förklaras vad SQL-beräkningar gör, varför de används, processen för att skapa en SQL-beräkning och innehåller två exempel.

**Förklaring**

Tidigare bedömdes kolumner `advanced` kan bara utföras av en analytiker i Customer Success Team här på [!DNL Adobe Commerce Intelligence]. Nu har slutanvändaren allt som behövs och avancerade kolumner kan skapas i form av `SQL Calculation` kolumner på nya [!DNL Commerce Intelligence] arkitektur.

The `Calculation` kolumntypen, som nu finns som ett alternativ i Data Warehouse Manager, är samma tabellåtgärd som gör att du kan omforma kolumnerna i en tabell med hjälp av PostgreSQL-logik. Dokumentation om funktioner och operatorer som kan användas i `Calculation` kolumntypen finns på PostgreSQL-webbplatsen [här](https://www.postgresql.org/docs/9.6/functions.html).

De olika kolumner som kan skapas med `Calculation` -kolumnen är nästan obegränsad, men de flesta kolumner kan skapas med IF-THEN-programsatser och grundläggande aritmetik, som används i exemplen nedan.

**Exempel 1: Är kundens senaste order?**

De flesta konton har en kolumn som kallas `Is customer's last order?` på sina `orders` tabell för att utföra analyser av upprepade inköpspriser och kunder. Om ditt konto är baserat på den nya arkitekturen skapas den här kolumnen med en `Calculation` och kan visas på skärmbilden nedan:

![](../../assets/Is_customer_s_last_order.png)

The `Is customer's last order?` kolumnen använder indata `Customer's lifetime number of orders` och `Customer's order number` kantutjämnad som `A` och `B` respektive.

Line by line, the Innehåll of the PostgreSQL is:

* case: Detta startar en serie av If - then-programsatser
* när `A` är null eller `B` är null och null: Om någon av inmatningarna är tom ska utdata också vara tomma. Detta förhindrar SQL-fel
* när `A=B` sedan `Yes`: If `Customer's lifetime number of orders` är lika med `Customer's order number` för den här raden, returnera `Yes`. Så om kunden har lagt fyra order skulle raden för den fjärde ordern returnera `Yes` for `Is customer's last order?`
* else `No`: Om inget av de andra programsatserna är uppfyllda returneras `No`
* end: Detta avslutar programsatserna If - then

Möjliga värden som kan returneras av den här kolumnen (`NULL`, `Yes`, `No`) innehåller tecken som inte är siffror, så datatypen här är String.

**Exempel 2: Totalt orderartikelvärde (kvantitet * pris)**

Många kunder gillar att analysera intäkterna på artikelnivå och segmentera dem med fält som `product name` eller `category`. De flesta databaser ger dig i själva verket inte intäkter från en produkt i en beställning, utan de anger i stället den kvantitet som sålts i beställningen och artikelns pris.

För att möjliggöra produktintäktsanalyser har de flesta konton en kolumn som kallas `Order item total value (quantity * price)` på sina `Orders Items` tabell. Om ditt konto är baserat på den nya arkitekturen skapas den här kolumnen även med en `Calculation` och kan visas på skärmbilden nedan:

![](../../assets/Order_item_total_value.png)

I handelsschemat `Order item total value (quantity * price)` kolumnen använder indata `qty ordered` och `base price` kantutjämnad som `A` och `B` respektive.

Värdena som returneras av den här nya kolumnen är i dollar och cent, så den korrekta datatypen är `Decimal(10,2)`.

**Mekanik**

En ny `Calculation` kan läggas till i en tabell genom att navigera till **[!DNL Manage Data > Data Warehouse]** enligt nedan:

![](../../assets/blobid2.png)

Här kan du skapa en `Calculation` kolumn genom att följa stegen nedan:

1. Markera tabellen som du vill lägga till `Calculation` kolumn.
1. När du är i rätt tabell klickar du på **[!UICONTROL Create New Column]** längst upp till höger på skärmen.
1. Från `Select a definition` listruta, välja `Same Table`.
1. Välj `Calculation` som `column definition equation`.
1. Ange kolumnnamnet.
1. Välj `input` kolumner från tabellen som används i logiken för den nya kolumnen. Varje kolumn som du lägger till får ett alias, så den första kolumnen är `A`, den andra är `B` och så vidare.
1. I fönstret anger du PostgreSQL-logiken för den nya kolumnen med hjälp av bokstavsalias för dina indata. SQL-beräkningen ska begränsas till en enda kolumndefinition, inklusive all logik mellan SELECT- och FROM-satserna i en SQL-fråga. SQL-nyckelord som använder någon av indatabokstäverna ska skrivas med gemener. Om du till exempel använder `CASE` -programsats, ska skrivas med gemener - `case`. Systemet förutsätter att det finns ett versalt `A` är en av inmatningarna.
1. Välj lämplig datatyp.
   * `Integer` - Hela numret
   * `Decimal(10,2)` - ett decimaltal med 10 siffror totalt, varav 2 är till höger om decimalkommat
   * `String` - Alla typer av text eller teckenserier som använder icke-siffror
   * `Datetime` - `yyyy-MM-dd hh:mm:ss` format

1. Klicka på **[!UICONTROL test column]**. Detta genererar en lista med fem testvärden för var och en av dina indata och visar resultatet av logiken från steg 6 för varje uppsättning med testvärden. Om någon del av SQL genererar ett fel returneras felmeddelandet. Exempelresultat kan bara genereras om alla indatakolumner är inbyggda fält. Om någon av indatakolumnerna är beräknade kolumner måste du validera resultatet genom att lägga till kolumnen i ett mätresultat och visa den i Report Builder

1. När du är nöjd med resultatet klickar du på **[!UICONTROL Save]**. Kolumnen kan användas.
