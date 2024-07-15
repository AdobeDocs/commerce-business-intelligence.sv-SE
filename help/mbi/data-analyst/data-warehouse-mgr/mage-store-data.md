---
title: Lagra data i Adobe Commerce
description: Lär dig hur data genereras, vad som gör att en ny rad infogas och hur åtgärder registreras i Adobe Commerce-databasen.
exl-id: 436ecdc1-7112-4dec-9db7-1f3757a2a938
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '964'
ht-degree: 2%

---

# Lagrar data i [!DNL Adobe Commerce]

Plattformen [!DNL Adobe Commerce] spelar in och organiserar en mängd värdefulla handelsdata i hundratals tabeller. I det här avsnittet beskrivs:

* hur dessa data genereras
* vad gör att en ny rad infogas i en av [Core Commerce Tables](../data-warehouse-mgr/common-mage-tables.md)
* hur åtgärder som att göra ett köp eller skapa ett konto registreras i databasen [!DNL Adobe Commerce]

Om du vill diskutera dessa begrepp kan du läsa följande exempel:

`Clothes4U` är en klädåterförsäljare med både en online- och en tegelsten- och murbruk. Den använder [!DNL Magento Open Source] bakom sin webbplats för att samla in och organisera data.

## `catalog\_product\_entity`

Den är den 22 september och `Clothes4U` rullar ut tre nya objekt på sin höstrad: `Throwback Bellbottoms`, `Straight Leg Jeans` och `V-Neck T-Shirts`. En `Clothes4U`-anställd öppnar sin Commerce-administratör, klickar på **[!UICONTROL Add Product]** och anger all information för `Throwback Bellbottoms`.

Medarbetaren är nöjd med alla inställningar för `Throwback Bellbottoms` och klickar på **[!UICONTROL Save]**, vilket infogar den första raden nedanför i tabellen `catalog_product_entity`. Medarbetaren upprepar processen, skapar en annan Commerce-produkt för `Straight Leg Jeans` och sedan en tredje för `V-Neck T-Shirt` och infogar den andra och tredje raden nedan i tabellen `catalog_product_entity`:

| **`entity\_id`** | **`entity\_type\_id`** | **`attribute\_set\_id`** | **`sku`** | **`created\_at`** |
|---|---|---|---|---|
| 205 | 4 | 8 | Pants10 | 2016/09/22 09:15:43 |
| 206 | 4 | 8 | Pants11 | 2016/09/22 09:18:17 |
| 207 | 4 | 12 | Shirts6 | 2016/09/22 09:24:02 |

* `entity_id` - Det här är primärnyckeln för tabellen `catalog_product_entity`, vilket innebär att alla rader i tabellen måste ha olika `entity_id`. Varje `entity_id` i den här tabellen kan bara associeras med en produkt, och varje produkt kan bara associeras med en `entity_id`
   * Tabellens översta rad, `entity_id` = 205, är den nya raden som skapats för&quot;Throwback Bellbottoms&quot;. Var `entity_id` = 205 än visas på Commerce-plattformen avser den produkten &quot;Throwback Bellbottoms&quot;
* `entity_type_id` - Commerce har flera kategorier av objekt (som kunder, adresser och produkter för att nämna några), och den här kolumnen används för att ange kategorin som den här raden tillhör.
   * Detta är tabellen `catalog_product_entity`, och varje rad har samma entitetstyp: product. I Adobe Commerce är `entity_type_id` för produkten 4, vilket är anledningen till att alla tre nya produkter som skapats returnerar 4 för den här kolumnen.
* `attribute_set_id` - Attributuppsättningar används för att identifiera produkter som har samma typ av beskrivningar.
   * De två översta raderna i tabellen är produkterna `Throwback Bellbottoms` och `Straight Leg Jeans`, som båda är byxor. Dessa produkter skulle ha samma beskrivningar (till exempel name, inseam, wastline) och därför ha samma `attribute_set_id`. Det tredje objektet, `V-Neck T-Shirt`, har en annan `attribute_set_id` eftersom det inte skulle ha samma beskrivningar som byxorna. Skjortor har inte eftersläpningar eller insömmar.
* `sku` - Det här är unika värden som tilldelas till varje produkt av användaren när en produkt skapas i Adobe Commerce.
* `created_at` - Den här kolumnen returnerar tidsstämpeln för när varje produkt skapades

## `customer\_entity`

Kort efter att de tre nya produkterna lagts till besöker en ny kund, `Sammy Customer`, `Clothes4U`s webbplats för första gången. Eftersom `Clothes4U` inte tillåter gästbeställningar måste `Sammy Customer` först skapa ett konto på webbplatsen. Kunden anger obligatoriska autentiseringsuppgifter och klickar på Skicka, vilket resulterar i följande nya post på [`customer\_entity table`](../data-warehouse-mgr/cust-ent-table.md):

| **`entity id`** | **`entity type id`** | **`email`** | **`created at`** |
|---|---|---|---|
| `214` | `1` | `sammy.customer@gmail.com` | `2016/09/23 15:27:12` |

* `entity_id` - Precis som den föregående tabellen är `entity_id` primärnyckeln för tabellen `customer_entity`.
   * När `Sammy Customer` skapade ett konto och raden ovan skrevs till tabellen `customer_entity` tilldelades kunden `entity_id` = 214. I alla tabeller avser kunden som identifieras som `entity_id` = 214 alltid användaren Sammy Customer
* `entity_type_id` - Den här kolumnen identifierar vilken typ av entitet som listas i den här tabellen och fungerar på samma sätt som i tabellen `catalog_product_entity`
   * Varje rad i tabellen `customer_entity` är en kund och Commerce definierar kunder som `entity_type_id` som standard
* `email` - det här fältet fylls i av e-postmeddelandet som en ny kund anger när han/hon skapar sitt konto
* `created_at` - Den här kolumnen returnerar tidsstämpeln för varje användare som är ansluten

## `sales\_flat\_order (or Sales\_order` om du har [!DNL Adobe Commerce 2.x]

När kontot har skapats är `Sammy Customer` redo att börja göra ett köp. På webbplatsen lägger kunden till två par av `Throwback Bellbottoms` och en `V-Neck T-Shirt` i kundvagnen. Kunden är nöjd med valen och övergår till kassan och skickar ordern, vilket skapar följande post i tabellen [försäljning av plan order](../data-warehouse-mgr/sales-flat-order-table.md):

| **`entity id`** | **`customer id**` | **`subtotal`** | **`created at`** |
|---|---|---|---|
| 227 | 214 | 94,85 | 2016/09/23 15:41:39 |

* `entity_id` - det här är primärnyckeln för tabellen `sales_flat_order`.
   * När Sammy Customer lade den här ordern och raden ovan skrevs till tabellen `sales_flat_order` tilldelades ordern `entity_id` = 227.
* `customer_id` - Den här kolumnen är den unika identifieraren för kunden som placerade den här ordern
   * `customer_id` som är associerad med den här beställningen är 214, vilket är Sammy-kundens `entity_id` i tabellen `customer_entity`.
* `subtotal` - Den här kolumnen är det totala beloppet som debiteras en kund för ordern
   * De två paren&quot;Throwback Bellbottoms&quot; och&quot;V-Neck T-Shirt&quot; kostar totalt 94,85 dollar
* `created_at` - Den här kolumnen returnerar tidsstämpeln för när varje order skapades

## `sales\_flat\_order\_item ( or Sales\_order\_item`

(om du har Commerce 2.0 eller senare)

Förutom den enskilda raden i tabellen `Sales\_flat\_order` infogas en rad för varje unikt objekt i ordningen i tabellen [`sales\_flat\_order\_item` när ](../data-warehouse-mgr/sales-flat-order-item-table.md) skickar ordningen:`Sammy Customer`

| **`item\_id`** | **`name`** | **`product\_id`** | **`order\_id`** | **`qty\_ordered`** | **`price`** |
|---|---|---|---|---|---|
| 822 | `Throwback Bellbottoms` | 205 | 227 | 2 | 39,95 |
| 823 | `V-Neck T-Shirt` | 207 | 227 | 1 | 14,95 |

* `item_id` - Den här kolumnen är primärnyckeln för tabellen `sales_flat_order_item`
   * `Sammy Customer`s order har skapat två rader i den här tabellen eftersom ordern innehöll två distinkta produkter
* `name` - Den här kolumnen är namnet på produkten
* `product_id` - Den här kolumnen är den unika identifieraren för den produkt som den här raden refererar till
   * Den första raden ovan har `product_id` = 205 eftersom `Throwback Bellbottoms` har `entity_id` 205 i tabellen `catalog_product_entity`
* `order_id` - Den här kolumnen är `entity_id` i ordningen som innehåller dessa speciella orderobjekt
   * Båda raderna ovan har `order_id` = 227 eftersom de båda är en del av ordningen som placeras av `Sammy Customer`, som har `entity_id` = 227 i tabellen `sales_flat_order`
* `qty_ordered` - Den här kolumnen är antalet enheter i produkten som ingår i den här specifika ordern
   * Ordningen för `Sammy Customer` innehöll två par `Throwback Bellbottoms`
* `price` - Den här kolumnen är priset för en enda enhet i orderartikeln
   * `subtotal` från `Sammy Customer` i tabellen `sales_flat_order` var 94,85, vilket är summan av två par med `Throwback Bellbottoms` på 39,95 USD vardera och 1 `V-Neck T-Shirt` på 14,95 USD.
