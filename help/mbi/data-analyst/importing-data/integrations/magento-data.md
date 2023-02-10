---
title: Förväntade handelsdata
description: Utforska huvuddatatabellerna som Commerce-användare importerar till MBI
exl-id: b481c8fc-41b6-4094-8901-17d57f26bfc0
source-git-commit: 9974cc5c5cf89829ca522ba620b8c0c2d509610c
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# Förväntade handelsdata

Efter att du har [har anslutit din Commerce Store](../../../data-analyst/importing-data/integrations/magento.md)kan du använda Data warehouse Manager för att enkelt spåra relevanta datafält från din Commerce-databas för analys.

I den här artikeln utforskar vi de viktigaste datatabellerna som Commerce-användare importerar till [!DNL MBI].

| **Tabellnamn** | **Beskrivning** |
|-----|-----|
| `Customers` | The `customer\_entity` och relaterade tabeller beskriver informationen som hör till varje *registrerad kund* i din databas, som deras e-postadress och registreringsdatum. Med den här informationen kan ni börja segmentera efter kundattribut och kohorter. |
| `Orders` | The `sales\_flat\_order` register registrerar alla order, inklusive `created\_at` tidsstämpel som beställningen placerades på och `base\_grand\_total` fält som summerar intäkter. Dessa fält kommer att utgöra grunden för dina ordernivåvärden. Om ordern gjordes av en *registrerad kund*, `customer\_id` fältet kommer att länka tillbaka till  `customer\_entity` en tabell som gör det möjligt att analysera kundernas köpbeteende. |
| `Order items` | The `sales\_flat\_order\_item` register registrerar alla artiklar som tillhör en order. Detta inkluderar `price` och `qty\_ordered` fält, samt `order\_id` fält som ansluter till `sales\_flat\_order` tabell. Det här bordet är grunden för mätvärden som `Item sold`och du kan segmentera efter `product` och `product type`. |
| `Products` | The `catalog\_product\_entity` I tabellen lagras information om produktnivåattribut, som kategori, storlek och färg. |
| `Categories` | Dina produkter tillhör en eller flera olika `product categories`, beroende på hur ditt Commerce-bygge är konfigurerat. The `catalog\_category\_entity` I -tabellen lagras hierarkin för dessa kategorier (Appsällan > Tops > T-Shirts, till exempel) och `catalog\_category\_product` tabellen loggar anslutningarna mellan produkterna och dessa kategorier. |

{style=&quot;table-layout:auto&quot;}

## Relaterad

* [Ansluter [!DNL Adobe Commerce]](../integrations/magento.md)
* [Återautentisera integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
