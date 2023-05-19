---
title: Lagra data i Adobe Commerce
description: Lär dig hur data genereras, vad som gör att en ny rad infogas och hur åtgärder registreras i Adobe Commerce-databasen.
exl-id: 436ecdc1-7112-4dec-9db7-1f3757a2a938
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 3%

---

# Lagra data i [!DNL Adobe Commerce]

The [!DNL Adobe Commerce] registrerar och organiserar ett stort antal värdefulla affärsdata i hundratals tabeller. I det här avsnittet beskrivs:

* hur dessa data genereras
* vad gör att en ny rad infogas i en av [Core Commerce Tables](../data-warehouse-mgr/common-mage-tables.md)
* hur åtgärder som att göra ett köp eller skapa ett konto registreras i [!DNL Adobe Commerce] databas

Om du vill diskutera dessa begrepp kan du läsa följande exempel:

`Clothes4U` är en klädhandlare med både online- och murbruk. Den använder [!DNL Magento Open Source] bakom sin webbplats för att samla in och organisera data.

## `catalog\_product\_entity`

den 22 september, och `Clothes4U` distribuerar tre nya objekt till sin höstlinje: `Throwback Bellbottoms`, `Straight Leg Jeans`och `V-Neck T-Shirts`. A `Clothes4U` employee öppnar sin Commerce Admin, klicka **[!UICONTROL Add Product]** och anger all information för `Throwback Bellbottoms`.

Uppfyrad med alla inställningar för `Throwback Bellbottoms`klickar medarbetaren **[!UICONTROL Save]** som infogar den första raden nedanför i `catalog_product_entity` tabell. Medarbetaren upprepar processen och skapar en annan Commerce-produkt för `Straight Leg Jeans`och sedan en tredje för `V-Neck T-Shirt`, infogar den andra och tredje raden nedanför i `catalog_product_entity` tabell:

| **`entity\_id`** | **`entity\_type\_id`** | **`attribute\_set\_id`** | **`sku`** | **`created\_at`** |
|---|---|---|---|---|
| 205 | 4 | 8 | Pants10 | 2016/09/22 09:15:43 |
| 206 | 4 | 8 | Pants11 | 2016/09/22 09:18:17 |
| 207 | 4 | 12 | Shirts6 | 2016/09/22 09:24:02 |

* `entity_id` - Detta är primärnyckeln till `catalog_product_entity` tabell, vilket innebär att alla rader i tabellen måste ha olika `entity_id`. Varje `entity_id` i det här registret kan bara associeras med en produkt, och varje produkt kan bara associeras med en `entity_id`
   * Tabellens övre rad ovan, `entity_id` = 205, är den nya raden som skapats för&quot;Throwback Bellbottoms&quot;. Var `entity_id` = 205 i Commerce-plattformen avser produkten &quot;Throwback Bellbottoms&quot;
* `entity_type_id` - Handeln har flera kategorier av objekt (som kunder, adresser och produkter, för att nämna några), och den här kolumnen används för att ange kategorin som den här raden tillhör.
   * Detta är `catalog_product_entity` tabell har varje rad samma enhetstyp: produkt. I Adobe Commerce `entity_type_id` för produkten är 4, vilket är anledningen till att alla tre nya produkter skapade retur 4 för denna kolumn.
* `attribute_set_id` - Attributuppsättningar används för att identifiera produkter som har samma beskrivning.
   * De två översta raderna i tabellen är `Throwback Bellbottoms` och `Straight Leg Jeans` produkter, som båda är byxor. Dessa produkter skulle ha samma beskrivningar (till exempel namn, inseam, midline) och därför ha samma `attribute_set_id`. Den tredje posten `V-Neck T-Shirt` har en annan `attribute_set_id` eftersom den inte skulle ha samma beskrivningar som byxorna, Skjortor har inte dammar eller insömmar.
* `sku` - Detta är unika värden som användaren tilldelar varje produkt när han/hon skapar en produkt i Adobe Commerce.
* `created_at` - Den här kolumnen returnerar tidsstämpeln för när varje produkt skapades

## `customer\_entity`

Kort efter de tre nya produkterna, en ny kund, `Sammy Customer`, besök `Clothes4U`för första gången. Sedan `Clothes4U` tillåter inte gästorder, `Sammy Customer` måste först skapa ett konto på webbplatsen. Kunden anger obligatoriska inloggningsuppgifter och klickar på Skicka, vilket resulterar i följande nya post på [`customer\_entity table`](../data-warehouse-mgr/cust-ent-table.md):

| **`entity id`** | **`entity type id`** | **`email`** | **`created at`** |
|---|---|---|---|
| `214` | `1` | `sammy.customer@gmail.com` | `2016/09/23 15:27:12` |

* `entity_id` - Precis som föregående tabell, `entity_id` är primärnyckeln till `customer_entity` tabell.
   * När `Sammy Customer` skapade ett konto och raden ovan skrevs till `customer_entity` register, kund tilldelades `entity_id` = 214. I alla tabeller identifierades kunden som `entity_id` = 214 avser alltid användaren Sammy Customer
* `entity_type_id` - Den här kolumnen identifierar vilken typ av entitet som listas i den här tabellen och fungerar på samma sätt som i `catalog_product_entity` table
   * Varje rad på `customer_entity` tabellen är en kund och Commerce definierar kunder som `entity_type_id` 1 som standard
* `email` - det här fältet fylls i av det e-postmeddelande som en ny kund anger när han/hon skapar sitt konto
* `created_at` - Den här kolumnen returnerar tidsstämpeln för när varje användare ansluter

## `sales\_flat\_order (or Sales\_order` om du har [!DNL Adobe Commerce 2.x]

När kontot har skapats är `Sammy Customer` är redo att börja göra ett köp. På webbplatsen lägger kunden till två par av `Throwback Bellbottoms` och en `V-Neck T-Shirt` till varukorgen. Kunden är nöjd med valen och övergår till kassan och skickar ordern, vilket skapar följande post på [plan ordertabell för försäljning](../data-warehouse-mgr/sales-flat-order-table.md):

| **`entity id`** | **`customer id**`**`subtotal`****`created at`** |
|---|---|---|---|
| 227 | 214 | 94.85 | 2016/09/23 15:41:39 |

* `entity_id` - det här är primärnyckeln till `sales_flat_order` tabell.
   * När Sammy Customer lade denna order och raden ovan skrevs till `sales_flat_order` register, ordern har tilldelats `entity_id` = 227.
* `customer_id` - Den här kolumnen är den unika identifieraren för kunden som lade den här särskilda ordern
   * The `customer_id` som är kopplad till denna beställning är 214, vilket är Sammy Customer&#39;s `entity_id` på `customer_entity` tabell.
* `subtotal` - Den här kolumnen är det totala beloppet som debiteras en kund för ordern
   * De två paren&quot;Throwback Bellbottoms&quot; och&quot;V-Neck T-Shirt&quot; kostar totalt 94,85 dollar
* `created_at` - Den här kolumnen returnerar tidsstämpeln för när varje order skapades

## `sales\_flat\_order\_item ( or Sales\_order\_item`

(om du har Commerce 2.0 eller senare)

Förutom den enstaka raden på `Sales\_flat\_order` tabell, när `Sammy Customer` skickar ordern, en rad för varje unik artikel i den ordningen infogas i [`sales\_flat\_order\_item` table](../data-warehouse-mgr/sales-flat-order-item-table.md):

| **`item\_id`** | **`name`** | **`product\_id`** | **`order\_id`** | **`qty\_ordered`** | **`price`** |
|---|---|---|---|---|---|
| 822 | `Throwback Bellbottoms` | 205 | 227 | 2 | 39.95 |
| 823 | `V-Neck T-Shirt` | 207 | 227 | 1 | 14.95 |

* `item_id` - Den här kolumnen är primärnyckeln för `sales_flat_order_item` table
   * `Sammy Customer`Ordern har skapat två rader i det här registret eftersom ordern innehöll två distinkta produkter
* `name` - Den här kolumnen är namnet på produkten
* `product_id` - Den här kolumnen är den unika identifieraren för den produkt som raden refererar till
   * Den första raden ovan har `product_id` = 205 eftersom `Throwback Bellbottoms` har `entity_id` av 205 på `catalog_product_entity` table
* `order_id` - Den här kolumnen är `entity_id` av den order som innehåller dessa specifika orderartiklar
   * Båda raderna ovan har `order_id` = 227 eftersom de båda är en del av den beställning som `Sammy Customer`som har `entity_id` = 227 på `sales_flat_order` table
* `qty_ordered` - Denna kolumn är antalet enheter av produkten som ingår i denna specifika order
   * `Sammy Customer`Ordningen innehöll två par `Throwback Bellbottoms`
* `price` - Den här kolumnen är priset för en enda enhet i orderartikeln
   * The `subtotal` från `Sammy Customer`i `sales_flat_order` tabellen var 94,85, vilket är summan av två par av `Throwback Bellbottoms` på 39,95 USD vardera och 1 `V-Neck T-Shirt` 14,95 USD.
