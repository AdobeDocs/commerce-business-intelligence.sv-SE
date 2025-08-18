---
title: Förväntade Stripe-data
description: Utforska de viktigaste datatabellerna som du kan importera från Stripe till Commerce Intelligence.
exl-id: 694577b2-48f9-4376-850d-acae1776afe3
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# [!DNL Stripe] data förväntades

När [du har anslutit ditt [!DNL Stripe] konto](../integrations/stripe.md) kan du använda [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) för att enkelt spåra relevanta datafält för analys.

I det här avsnittet utforskas huvuddatatabellerna som du kan importera från [!DNL Stripe] till [!DNL Commerce Intelligence]. När installationen är klar skapas följande tabeller i din Data Warehouse. Klicka på länkarna i kolumnen Tabellnamn om du vill veta mer om attributen i varje tabell.

| **Tabellnamn** | **Beskrivning** |
|-----|-----|
| [`Customers`](https://stripe.com/docs/sources/customers) | Med kundobjekten kan du utföra återkommande avgifter och spåra flera avgifter som är kopplade till samma kund. |
| [`Charges`](https://stripe.com/docs/payments/payment-intents/migration/charges) | Det här registret innehåller information om avgifter för kredit- och debetkort, inklusive belopp, valuta, status, kund-ID med mera. |
| [`Coupons`](https://stripe.com/docs/api/coupons/object) | Det här registret innehåller information om en procent- eller avdragsrabatt som du kanske vill tillämpa på en kund. Kuponger gäller endast fakturor. De gäller inte engångsavgifter. |
| [`Invoices`](https://stripe.com/docs/billing/migration/invoice-states) | Det här registret innehåller information om fakturor, inklusive belopp som ska betalas, prenumerationer, fakturaartiklar, eventuella automatiska prospekteringsjusteringar och mycket annat. |
| [`Plans`](https://stripe.com/docs/api/plans/object) | Tabellen innehåller prisinformation för olika produkter och funktionsnivåer på din webbplats. Du kan till exempel ha en 10 USD/månad-plan för grundläggande funktioner och en 20 USD/månad-plan för premiumfunktioner. |
| [`Subscriptions`](https://stripe.com/docs/api/subscriptions/object) | Den här tabellen innehåller information om de prenumerationsplaner som dina kunder tillhör. Attributen omfattar kund-ID, status, datum för när programmet har avbrutits/avslutats, procent moms, testversionsinformation med mera. |
| [`Events`](https://stripe.com/docs/development/dashboard/events) | Händelser talar om något intressant som har hänt på ett konto. [När en intressant händelse inträffar](https://stripe.com/docs/api/events/types) skapas ett nytt händelseobjekt. Om till exempel händelsen `charge.succeeded` har skapats med en avgift, eller om en faktura inte kan betalas, skapas en `invoice.payment\_failed`-händelse. |

{style="table-layout:auto"}

>[!NOTE]
>
>Många API-begäranden kan leda till att flera händelser skapas. Om du till exempel skapar en prenumeration för en kund får du både en `customer.subscription.created`-händelse och en `charge.succeeded`-händelse.

## Relaterat:

* [Ansluter  [!DNL Stripe]](../integrations/stripe.md)
* [Återautentiserar integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=sv-SE)
