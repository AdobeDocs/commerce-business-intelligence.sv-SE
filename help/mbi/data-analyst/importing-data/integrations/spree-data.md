---
title: Förväntade uppslagsdata
description: Upptäck de viktigaste datatabellerna som du kan importera från Spree till [!DNL Commerce Intelligence] konto.
exl-id: 203a2d4b-e7ad-4704-a3c1-8e22ff0bf2d6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# Förväntat [!DNL Spree] data

Efter att du har [ansluten till din [!DNL Spree] store](../../../data-analyst/importing-data/integrations/spree.md)kan du använda [Data Warehouse Manager](../../data-warehouse-mgr/tour-dwm.md) för att enkelt spåra relevanta datafält från [!DNL Spree] plattform för analys.

I det här avsnittet beskrivs de huvuddatatabeller som du kan importera från [!DNL Spree] i [!DNL Commerce Intelligence] konto, inklusive länkar till [ytterligare dokumentation](https://guides.spreecommerce.org/developer/addresses.html#address) om [!DNL Spree] data.

| **Tabellnamn** | **Beskrivning** |
|-----|-----|
| `Users` | The `users` tabellen innehåller kontoinformation för registrerade kunder, inklusive personens e-postadress, namn och registreringsdatum. På så sätt kan ni analysera olika kundsegment och deras köpbeteenden. |
| [`Orders`](https://guides.spreecommerce.org/developer/orders.html#overview) | The `orders` tabellen är grunden för all er statistik på ordernivå. Här registreras all orderinformation från din [!DNL Spree] butik, inklusive `completed\_at` (orderns tidsstämpel), `user\_id` (ID för den registrerade användare som lade ordern). Om beställningen gjordes av en registrerad användare `user\_id` länkar tillbaka till `users` tabell som gör det möjligt att analysera användarbeteenden. |
| `Line items` | The `line\_items` tabellen är underordnad någon av `orders` tabell eller `subscriptions`. Den registrerar information om en order eller en prenumerations radobjekt. För beställningar med flera produkter har varje produkt en egen datarad i tabellen, inklusive en `product\_id` så att du kan knyta det till `Products` tabell. |
| `Products` | The `products` register registrerar all produktinformation för en säljbar artikel i uppslagskatalogen. På så sätt kan ni segmentera era produktattribut på artikelnivå. |
| `Subscriptions` | Om du har en [!DNL Spree] prenumerationstillägg, `subscriptions` tabellen innehåller information om varje enskild prenumeration, inklusive `created\_at` (startdatum), `cancelled\_at` (det datum då en prenumeration annullerades) och `interval` av prenumerationen. |

{style="table-layout:auto"}

## Relaterat:

* [Ansluter [!DNL Spree]](../integrations/spree.md)
* [Återautentisera integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
