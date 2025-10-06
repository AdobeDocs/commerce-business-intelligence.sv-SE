---
title: Skapa och använda en SQL-beräknad kolumn
description: Lär dig hur avancerade kolumner kan skapas i form av SQL Calculation-kolumner i den nya Adobe Commerce Intelligence-arkitekturen.
exl-id: f16e4ee4-ed73-4ddb-b701-1fe3db14346a
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, SQL Report Builder, Commerce Tables
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '839'
ht-degree: 0%

---

# Skapa en SQL-beräknad kolumn

I det här avsnittet beskrivs syftet med och användningsområdena för kolumntypen `Calculation` som kan läggas till i tabeller med [Data Warehouse Manager](../data-warehouse-mgr/tour-dwm.md). Nedan förklaras vad SQL-beräkningar gör, varför de används, processen för att skapa en SQL-beräkning och innehåller två exempel.

**Förklaring**

Tidigare kunde kolumner som ansågs vara `advanced` bara utföras av en analytiker i Customer Success Team här på [!DNL Adobe Commerce Intelligence]. Nu är alla funktioner i slutanvändarens händer och avancerade kolumner kan skapas i form av `SQL Calculation` kolumner i den nya [!DNL Commerce Intelligence]-arkitekturen.

Kolumntypen `Calculation`, som nu finns som ett alternativ i Data Warehouse Manager, är samma tabellåtgärd som gör att du kan omforma kolumnerna i en tabell med hjälp av PostgreSQL-logik. Dokumentation om funktioner och operatorer som kan användas i kolumntypen `Calculation` finns på PostgreSQL-webbplatsen [här](https://www.postgresql.org/docs/9.6/functions.html).

De olika kolumner som kan skapas med kolumnen `Calculation` är nästan obegränsade, men de flesta kolumner kan skapas med IF-THEN-satser och grundläggande aritmetik, som används i exemplen nedan.

**Exempel 1: Är kundens senaste order?**

De flesta konton har en kolumn med namnet `Is customer's last order?` i sin `orders`-tabell för att utföra analyser på upprepade inköpspriser och skadade kunder. Om ditt konto finns i den nya arkitekturen skapas den här kolumnen med en `Calculation`-kolumn och kan visas på skärmbilden nedan:

![SQL beräknad kolumndefinition för identifiering av kundens senaste order](../../assets/Is_customer_s_last_order.png)

Kolumnen `Is customer's last order?` använder indata `Customer's lifetime number of orders` och `Customer's order number` med alias `A` respektive `B`.

Line by line, the Innehåll of the PostgreSQL is:

* case: Detta startar en serie av If - then-programsatser
* när `A` är null eller `B` är null: Om någon av inmatningarna är tom ska även utdata vara tomma. Detta förhindrar SQL-fel
* när `A=B` sedan `Yes`: Om `Customer's lifetime number of orders` är lika med `Customer's order number` för den här raden returnerar du `Yes`. Om en kund har lagt fyra order returnerar raden för den fjärde ordern `Yes` för `Is customer's last order?`
* else `No`: Om ingen av de andra när -programsatserna uppfylls returnerar du `No`
* end: Detta avslutar programsatserna If - then

Möjliga värden som kan returneras av den här kolumnen (`NULL`, `Yes`, `No`) innehåller tecken som inte är siffror, så datatypen här är String.

**Exempel 2: Totalt orderartikelvärde (kvantitet * pris)**

Många kunder gillar att analysera intäkter på objektnivå och dela upp dem i fält som `product name` eller `category`. De flesta databaser ger dig i själva verket inte intäkter från en produkt i en beställning, utan de anger i stället den kvantitet som sålts i beställningen och artikelns pris.

För att aktivera produktintäktsanalyser har de flesta konton en kolumn med namnet `Order item total value (quantity * price)` i sin `Orders Items`-tabell. Om ditt konto finns i den nya arkitekturen skapas den här kolumnen också med en `Calculation`-kolumn och kan visas på skärmbilden nedan:

![SQL beräknad kolumndefinition för orderartikelns totalvärde](../../assets/Order_item_total_value.png)

I Commerce-schemat använder kolumnen `Order item total value (quantity * price)` indata `qty ordered` och `base price` med alias `A` respektive `B`.

Värdena som returneras av den här nya kolumnen är i dollar och cent, så den korrekta datatypen är `Decimal(10,2)`.

**Mekanik**

En ny `Calculation`-kolumn kan läggas till i en tabell genom att navigera till **[!DNL Manage Data > Data Warehouse]** enligt nedan:

![Tabellvy som visar beräknade kolumnresultat](../../assets/blobid2.png)

Härifrån kan du skapa en `Calculation`-kolumn genom att följa stegen nedan:

1. Markera den tabell som du vill lägga till kolumnen `Calculation` i.
1. Klicka på **[!UICONTROL Create New Column]** längst upp till höger på skärmen när du är i rätt tabell.
1. Välj `Select a definition` i listrutan `Same Table`.
1. Välj `Calculation` som `column definition equation`.
1. Ange kolumnnamnet.
1. Välj de `input` kolumner från tabellen som används i logiken för den nya kolumnen. Varje kolumn som du lägger till får ett bokstavsalias, så den första kolumnen är `A`, den andra är `B` och så vidare.
1. I fönstret anger du PostgreSQL-logiken för den nya kolumnen med hjälp av bokstavsalias för dina indata. SQL-beräkningen ska begränsas till en enda kolumndefinition, inklusive all logik mellan SELECT- och FROM-satserna i en SQL-fråga. SQL-nyckelord som använder någon av indatabokstäverna ska skrivas med gemener. Om du till exempel använder programsatsen `CASE` ska den skrivas med gemener - `case`. Systemet antar att ett versalt `A` refererar till en av indatavärdena.
1. Välj lämplig datatyp.
   * `Integer` - Hela numret
   * `Decimal(10,2)` - ett decimaltal med totalt 10 siffror, varav 2 är till höger om decimalkommat
   * `String` - Alla typer av text eller teckenserier som använder icke-siffror
   * `Datetime` - `yyyy-MM-dd hh:mm:ss`-format

1. Klicka på **[!UICONTROL test column]**. Detta genererar en lista med fem testvärden för var och en av dina indata och visar resultatet av logiken från steg 6 för varje uppsättning med testvärden. Om någon del av SQL genererar ett fel returneras felmeddelandet. Exempelresultat kan bara genereras om alla indatakolumner är inbyggda fält. Om någon av indatakolumnerna är beräknade kolumner måste du validera resultatet genom att lägga till kolumnen i ett mätresultat och visa den i Visual Report Builder

1. När du är nöjd med resultatet klickar du på **[!UICONTROL Save]**. Kolumnen kan användas.
