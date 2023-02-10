---
title: Förväntade stripe-data
description: Utforska de viktigaste datatabeller som du kan importera från Stripe till [!DNL MBI].
exl-id: 694577b2-48f9-4376-850d-acae1776afe3
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# Förväntat [!DNL Stripe] data

Efter [du har anslutit din [!DNL Stripe] konto](../integrations/stripe.md)kan du använda [data warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) för att enkelt spåra relevanta datafält för analys.

I den här artikeln utforskar vi de viktigaste datatabellerna som du kan importera från [!DNL Stripe] till [!DNL MBI]. När installationen är klar skapas följande tabeller i data warehouse. Klicka på länkarna i kolumnen Tabellnamn om du vill veta mer om attributen i varje tabell.

| **Tabellnamn** | **Beskrivning** |
|-----|-----|
| [`Customers`](https://stripe.com/docs/sources/customers) | Med kundobjekten kan du utföra återkommande avgifter och spåra flera avgifter som är kopplade till samma kund. |
| [`Charges`](https://stripe.com/docs/payments/payment-intents/migration/charges) | Det här registret innehåller information om avgifter för kredit- och debetkort, inklusive belopp, valuta, status, kund-ID med mera. |
| [`Coupons`](https://stripe.com/docs/api/coupons/object) | Tabellen innehåller information om en rabatt i procent eller belopp som du kanske vill tillämpa på en kund. Observera att kuponger endast gäller fakturor. de inte gäller engångsavgifter. |
| [`Invoices`](https://stripe.com/docs/billing/migration/invoice-states) | Det här registret innehåller information om fakturor, inklusive belopp som ska betalas, prenumerationer, fakturaartiklar, eventuella automatiska prospekteringsjusteringar och mycket annat. |
| [`Plans`](https://stripe.com/docs/api/plans/object) | Tabellen innehåller prisinformation för olika produkter och funktionsnivåer på din webbplats. Du kan till exempel ha en 10 USD/månad-plan för grundläggande funktioner och en 20 USD/månad-plan för premiumfunktioner. |
| [`Subscriptions`](https://stripe.com/docs/api/subscriptions/object) | Den här tabellen innehåller information om de prenumerationsplaner som dina kunder tillhör. Attributen omfattar kund-ID, status, datum för när programmet har avbrutits/avslutats, procent moms, testversionsinformation med mera. |
| [`Events`](https://stripe.com/docs/development/dashboard/events) | Händelser talar om något intressant som just har hänt på ett konto. [När en intressant händelse inträffar](https://stripe.com/docs/api/events/types)skapas ett nytt händelseobjekt. Om en avgift till exempel lyckas `charge.succeeded` Händelsen skapas; eller, när en faktura inte kan betalas `invoice.payment\_failed` -händelsen skapas. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Många API-begäranden kan leda till att flera händelser skapas. Om du till exempel skapar en ny prenumeration för en kund får du båda en `customer.subscription.created` -händelse och en  `charge.succeeded` -händelse.

## Relaterat:

* [Ansluter [!DNL Stripe]](../integrations/stripe.md)
* [Återautentisera integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
