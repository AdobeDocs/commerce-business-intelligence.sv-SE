---
title: Förväntade Commerce-data
description: Utforska de viktigaste datatabeller som Commerce-användare importerar till Commerce Intelligence
exl-id: b481c8fc-41b6-4094-8901-17d57f26bfc0
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 0%

---

# [!DNL Adobe Commerce] data förväntades

När du har [anslutit din [!DNL Adobe Commerce] butik](../../../data-analyst/importing-data/integrations/magento.md) kan du använda Data Warehouse Manager för att enkelt spåra relevanta datafält från din Commerce-databas för analys.

I det här avsnittet beskrivs huvuddatatabellerna som Commerce-användare importerar till [!DNL Commerce Intelligence].

| **Tabellnamn** | **Beskrivning** |
|-----|-----|
| `Customers` | Registren `customer\_entity` och relaterade tabeller beskriver informationen som är associerad med varje *registrerad kund* i din databas, t.ex. e-postadress och registreringsdatum. Med den här informationen kan ni börja segmentera efter kundattribut och kohorter. |
| `Orders` | Tabellen `sales\_flat\_order` registrerar alla order, inklusive tidsstämpeln `created\_at` som ordern placerades i och fältet `base\_grand\_total` som summerar intäkten. Dessa fält är grunden för dina ordernivåvärden. Om beställningen gjordes av en *registrerad kund* länkar fältet `customer\_id` tillbaka till tabellen `customer\_entity` för att göra det möjligt att analysera kundens beteende. |
| `Order items` | Registret `sales\_flat\_order\_item` registrerar alla objekt som tillhör en order. Detta inkluderar fälten `price` och `qty\_ordered` samt fältet `order\_id` som ansluter till tabellen `sales\_flat\_order`. Den här tabellen är grunden för mätvärden som `Item sold`, och gör att du kan segmentera efter `product` och `product type`. |
| `Products` | I tabellen `catalog\_product\_entity` lagras information om produktnivåattribut, som kategori, storlek och färg. |
| `Categories` | Dina produkter tillhör en eller flera olika `product categories`, beroende på hur din Commerce-version är konfigurerad. Tabellen `catalog\_category\_entity` lagrar hierarkin för dessa kategorier (Klar > Tops > T-Shirts, till exempel) och tabellen `catalog\_category\_product` loggar anslutningarna mellan dina produkter och dessa kategorier. |

{style="table-layout:auto"}

## Relaterad

* [Ansluter  [!DNL Adobe Commerce]](../integrations/magento.md)
* [Återautentiserar integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
