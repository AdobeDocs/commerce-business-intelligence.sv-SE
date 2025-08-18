---
title: Förväntade uppslagsdata
description: Utforska de huvuddatatabeller som du kan importera från Spry till ditt [!DNL Commerce Intelligence] konto.
exl-id: 203a2d4b-e7ad-4704-a3c1-8e22ff0bf2d6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# [!DNL Spree] data förväntades

När du har [anslutit din [!DNL Spree] butik](../../../data-analyst/importing-data/integrations/spree.md) kan du använda [Data Warehouse Manager](../../data-warehouse-mgr/tour-dwm.md) för att enkelt spåra relevanta datafält från din [!DNL Spree]-plattform för analys.

I det här avsnittet utforskas de huvuddatatabeller som du kan importera från [!DNL Spree] till ditt [!DNL Commerce Intelligence]-konto, inklusive länkar till [ytterligare dokumentation](https://guides.spreecommerce.org/developer/addresses.html#address) om [!DNL Spree]-data.

| **Tabellnamn** | **Beskrivning** |
|-----|-----|
| `Users` | Tabellen `users` innehåller kontoinformation för registrerade kunder, inklusive personens e-postadress, namn och registreringsdatum. På så sätt kan ni analysera olika kundsegment och deras köpbeteenden. |
| [`Orders`](https://guides.spreecommerce.org/developer/orders.html#overview) | Tabellen `orders` fungerar som grund för alla dina ordernivåvärden. Här registreras all orderinformation för inköp från din [!DNL Spree]-butik, inklusive `completed\_at` (orderns tidsstämpel), `user\_id` (ID för den registrerade användaren som lade ordern). Om beställningen gjordes av en registrerad användare länkar `user\_id` tillbaka till tabellen `users` för att göra det möjligt att analysera användarbeteenden. |
| `Line items` | Tabellen `line\_items` är underordnad tabellen `orders` eller `subscriptions`. Den registrerar information om en order eller en prenumerations radobjekt. För order med flera produkter har varje produkt en egen datarad i den här tabellen, inklusive en `product\_id` som gör att du kan koppla den till tabellen `Products`. |
| `Products` | Registret `products` registrerar all produktinformation för ett säljbart objekt i uppslagskatalogen. På så sätt kan ni segmentera era produktattribut på artikelnivå. |
| `Subscriptions` | Om du har ett [!DNL Spree]-prenumerationstillägg innehåller tabellen `subscriptions` information om varje enskild prenumeration, inklusive `created\_at` (startdatum), `cancelled\_at` (det datum då en prenumeration avbröts) och `interval` för prenumerationen. |

{style="table-layout:auto"}

## Relaterat:

* [Ansluter  [!DNL Spree]](../integrations/spree.md)
* [Återautentiserar integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=sv-SE)
