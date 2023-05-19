---
title: Bygge[!DNL Google ECommerce]dimensioner
description: Lär dig skapa dimensioner som länkar e-handelsdata till era order och kunddata.
exl-id: f8a557ae-01d7-4886-8a1c-c0f245c7bc49
source-git-commit: 6b1bd96a0f9ae8bda3ae8db8ca78ad655079f2a4
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 0%

---

# Bygge [!DNL Google ECommerce] Dimensioner

>[!NOTE]
>
>Kräver [Administratörsbehörigheter](../../administrator/user-management/user-management.md).

Nu när du är klar [ansluta[!DNL Google ECommerce] konto](../../data-analyst/importing-data/integrations/google-ecommerce.md), vad kan du göra med dessa data i [!DNL Commerce Intelligence]? I det här avsnittet går vi igenom hur du bygger upp dimensioner som länkar e-handelsdata till dina beställningar och kunddata.

Med de mått som omfattas kan du skapa analyser som [svara på viktiga frågor om era marknadsföringskanaler och kampanjer](../../data-analyst/analysis/most-value-source-channel.md). Hur stor procent av intäkterna kommer från varje källa? Hur påverkar livstidsvärdet [!DNL Facebook] förvärvade kunder jämfört med [!DNL Google]?

## Krav och översikt

För att skapa dimensionerna i det här avsnittet behöver du en [!DNL Google ECommerce] tabell, `orders` och en `customers` tabell. Tabellerna måste [synkad till Data warehouse](../../data-analyst/data-warehouse-mgr/tour-dwm.md) innan mått kan skapas. Tabeller som synkroniseras visas i `Synced Tables` i `Data Warehouse Manager`.

Här är en snabbtitt på synkronisering av tabeller och kolumner om du behöver en uppdaterare:

![](../../assets/Syncing_New_Columns.gif)

När du har skapat en koppling från `orders` tabellen till [!DNL Google eCommerce] skapar du de första tre dimensionerna i listan nedan. Därefter använder du de dimensionerna för att skapa tre användar-/kunddimensioner i `customers` tabell. För att avsluta kopplar du de kolumnerna till `orders` tabell.

Här följer de ingående dimensionerna:

* **Orderregister**

* Order [!DNL Google Analytics] källa
* Order [!DNL Google Analytics] medium
* Order [!DNL Google Analytics]En kampanj
* Kundens första order [!DNL Google Analytics] källa
* Kundens första order [!DNL Google Analytics] medium
* Kundens första order [!DNL Google Analytics] kampanj

* **Kundregister**

* Kundens första order [!DNL Google Analytics] källa
* Kundens första order [!DNL Google Analytics] medium
* Kundens första order [!DNL Google Analytics] kampanj

## Bygga dimensionerna

Om du vill skapa dimensioner öppnar du [data warehouse Manager](../data-warehouse-mgr/tour-dwm.md) genom att klicka **[!UICONTROL Data]** > **[!UICONTROL Data Warehouse]**.

### Ordertabell, rund 1

Det här exemplet bygger **Order [!DNL Google Analytics] Källa** dimension.

1. Klicka på tabellen i listan över tabeller i Data warehouse (i det här fallet `orders`) som innehåller din orderinformation.
1. Klicka **[!UICONTROL Create a Column]**.
1. Namnge kolumnen.
1. Välj `Joined Column` från [listruta för definition](../data-warehouse-mgr/calc-column-types.md). Det här exemplet fungerar med en [personlig relation](../data-warehouse-mgr/table-relationships.md), matchar `eCommerce.transactionID` till exakt en rad i `orders` tabell.
1. Därefter måste du definiera sökvägen eller hur tabellen och kolumnen som används ska kopplas. Klicka på `Select a table and column` listruta.
1. Sökvägen du behöver är inte tillgänglig, så du måste skapa en ny. Klicka **[!UICONTROL Create new Path]**.
1. I fönstret som visas anger du `Many` sida till `orders.order\_id`eller kolumnen i `orders` register som innehåller order-ID:t.
1. På `One` sida, hitta `Google ECommerce` tabellen och sedan ange kolumnen som `transactionID`.

   ![](../../assets/google-ecommerce-table.png)

1. Klicka **[!UICONTROL Save]** för att skapa banan.
1. När banan har lagts till klickar du på **[!UICONTROL Select table and column]** rullgardinsmeny igen.
1. Leta reda på `ECommerce` och klickar sedan på `Source` kolumn. Detta knyter ordningarna till källinformationen.
1. När du är tillbaka i tabellschemat klickar du på **[!UICONTROL Save]** igen för att skapa dimensionen.

Här är en titt på hela processen:

![](../../assets/help_center.gif)

Försök sedan skapa **Order [!DNL Google Analytics] medium** och `campaign`. Det finns inte mycket att ändra för de här dimensionerna, så prova. Men om du fastnar kan du kolla [slutet av den här artikeln](#stuck) för att se vad som är annorlunda.

### Kundregister {#customers}

Det här exemplet bygger **Kundens första order [!DNL Google Analytics] källa** dimension.

1. Klicka på tabellen i listan över tabeller i Data warehouse (i det här fallet `customers`) som innehåller kundinformation.
1. Klicka **[!UICONTROL Create a Column]**.
1. Namnge kolumnen.
1. I det här exemplet väljer du `is MAX` definition från [listruta för definition](../../data-analyst/data-warehouse-mgr/calc-column-types.md). The `is MIN` kan även fungera om den används i en textkolumn med endast ett möjligt värde. Det viktiga är att se till att rätt filter ställs in, vilket du gör senare.
1. Klicka på **[!UICONTROL Select a table and column]** listrutan och välj `orders` tabellen, sedan `Order's [!DNL Google Analytics] source` kolumn.
1. Klicka **[!UICONTROL Save]**.
1. När du är tillbaka i tabellschemat klickar du på `Options` rullgardinsmeny `Filters`.
1. Klicka **[!UICONTROL Add Filter Set]** och sedan väljer `Orders we count` set. Du vill bara inkludera order i de order som du räknar filteruppsättningen för, så det är viktigt att den här filteruppsättningen är markerad.
1. Klicka **[!UICONTROL Add Filter]**. Du vill hitta kundens första order [!DNL Google Analytics] så du måste lägga till ett filter:

   _order.Kundens ordernummer = 1

   _
1. Klicka **[!UICONTROL Save]** för att skapa dimensionen.

Försök sedan skapa **Kundens första order [!DNL Google Analytics] medium** och `campaign`. Det finns inte mycket att ändra för de här dimensionerna, så prova. Men om du fastnar kan du kolla [slutet av den här artikeln](#stuck) för att se vad som är annorlunda.

### Bonus: Ordertabell, rund 2

Du kan stoppa här om du vill, men det här avsnittet aktiverar ytterligare analys genom att ta med **Kundens första order [!DNL Google Analytics] dimensioner** du skapade i [sista avsnittet](#customers) till `orders` tabell. Om du skapar dimensionerna i det här avsnittet kan du analysera alla mätvärden som bygger på `orders` tabell - `Revenue`, `Number of orders`, `Distinct buyers`och så vidare, med [!DNL Google Analytics] attribut för en kunds första order.

Det här exemplet förenar `Customer's first order's [!DNL Google Analytics] source` dimension till `orders` tabell.

1. Klicka på tabellen i listan över tabeller i Data warehouse (i det här fallet `orders`) som innehåller din orderinformation.
1. Klicka **[!UICONTROL Create a Column]**.
1. Namnge kolumnen.
1. Välj `Joined Column` i listrutan definition. Detta kopplar samman kunddimensionerna som du skapade i föregående avsnitt med `orders` tabell.
1. Klicka på **[!UICONTROL Select a table and column]** väljer du `customers` tabellen och `Customer's first order's [!DNL Google Analytics] source` kolumn.
1. Om en sökväg inte fylls i automatiskt väljer du den sökväg som bäst kopplar samman kund- och ordertabellerna.
1. Klicka **[!UICONTROL Save]** för att skapa dimensionen.

Här är en titt på hela processen:

![](../../assets/help_center2.gif)

Slutför genom att gå med i `Customer's first order's` medium och `campaign` dimensioner till `orders` tabell. Koppla ihop dimensionerna, och om det uppstår problem kan du kolla in [slutet av artikeln](#stuck) om du behöver hjälp.

### Radbrytning

Du är klar med att skapa dimensionerna, vilket betyder att du nu kan skapa kraftfulla analyser som spårar resultatet för olika kanaler och kampanjer. Kom ihåg att **nya kolumner är inte tillgängliga förrän nästa uppdatering har slutförts**.

Några av de populärare dimensionerna behandlas i det här avsnittet, men himlen är gränsen - prova att skapa din egen eller låt oss plocka oss om du vill ha hjälp med att utforska andra alternativ. 

### Ytterligare information

**`Orders`tabell 1**: När du skapar `Order's [!DNL Google Analytics]` medium och `campaign` mått är skillnaden de kolumner som är markerade i steg 12. I det här exemplet var kolumnen `Source`.

**`Customers`table**: När du skapar `Customer's first order's [!DNL Google Analytics]` medium och `campaign` dimensionerna är skillnaden de kolumner som är markerade i steg 5. I det här exemplet var kolumnen `Order's [!DNL Google Analytics]` källa.

**`Orders`tabell 2**: När du ansluter till `Customer's first order's [!DNL Google Analytics]` medium och `campaign` kolumner till `orders` tabellen är skillnaden de kolumner som är markerade i steg 5. I det här exemplet var kolumnen `Customer's first order's [!DNL Google Analytics]` källa.
