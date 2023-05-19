---
title: QuickBooks-data förväntades
description: Lär dig att enkelt spåra relevanta datafält för analys.
exl-id: a60996bd-e3d1-497d-abce-f02ef1444f1a
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '1053'
ht-degree: 0%

---

# Förväntat [!DNL QuickBooks] data

Efter [du har anslutit din [!DNL QuickBooks] konto](../../../data-analyst/importing-data/integrations/quickbooks.md)kan du använda [data warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) för att enkelt spåra relevanta datafält för analys. Följande tabeller skapas i Data warehouse:

Om du vill visa alla fält som är tillgängliga för spårning klickar du på länkarna i tabellnamnskolumnen.

## Transaktionsenheter {#transactionentities}

| **Tabellnamn** | **Beskrivning** |
|-----|-----|
| [`bill`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Bill) | The `bills` tabellen innehåller information om AP-transaktioner eller en betalningsförfrågan från en tredje part. Attribut omfattar valutatyp, valutakurs, totalt belopp, förfallodatum, saldo med mera. |
| [`billpayments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/BillPayment) | `BillPayment` företag är den slutliga transaktionen för betalning av räkningar som mottagits från en leverantör. Det här registret innehåller leverantörsinformation, betalningstyp, totalt belopp, transaktionsdatum med mera. |
| [`creditmemos`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/CreditMemo) | The `creditmemos` register registrerar transaktioner som är återbetalningar eller krediter för både fullständiga och partiella betalningar. Vissa attribut inkluderar kundens namn, kundens fakturerings- och leveransinformation, belopp och datum. |
| [`deposits`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Deposit) | `Deposits` inkludera direkt inlåning och kundbetalningar som flyttats till tillgångskontot efter att ha hållits i `Undeposited Funds` konto. Attributen innehåller belopp, insättnings-ID och datum. |
| [`estimates`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Estimate) | `Estimates` är transaktioner som ges till kunder som inkluderar föreslagna priser för en vara eller tjänst. Det här registret visar belopp, rabattinformation, kundinformation och datum. |
| [`invoices`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Invoice) | `Invoices` är försäljningsformulär som en kund betalar senare. Fakturaregistret registrerar insättningsinformation, datum, radobjekt, skatteinformation och kundinformation. |
| [`journalentries`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/JournalEntry) | The `journalentries` registerposter AR- och AP-kontoinformation, inklusive journalpost-ID, transaktionsdatum och radartikelinformation. |
| [`payments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Payment) | A `payment` posten innehåller attribut som betalnings-ID, tillämpade och ej tillämpade belopp, transaktionsdatum, transaktionstyp och bearbetningsstatus. |
| [`purchases`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Purchase) | The `purchases` tabellen visar dina utgifter och innehåller information om inköps-ID, betalningstyp, belopp och radartikel. |
| [`purchaseorders`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/PurchaseOrder) | The `purchaseorders` register innehåller begäranden om varor som skickas till leverantörer. Det här registret innehåller information om leverantör, inköpsordernummer, transaktionsdatum, radobjektsinformation, totalt belopp och information om AP-konto. |
| [`refundreceipts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/RefundReceipt) | The `refundreceipts` registerposter återbetalningar till kunder. Attribut är bl.a. inbetalnings-ID, radobjektsinformation, totalbelopp, kundinformation och saldo. |
| [`salesreceipts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/SalesReceipt) | The `salesreceipts` register registrerar information i de kvitton som skickas till kunderna, inklusive försäljningskvitto-ID, radobjektsinformation, totalt belopp, kundinformation, transaktionsdatum och eventuella insättningar. |
| [`timeactivities`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TimeActivity) | The `timeactivities` register innehåller tidsposter för leverantörer och/eller anställda och innehåller information om tidsaktivitet, medarbetare/leverantör, loggad tid, aktivitetsbeskrivning och inspelat datum. |
| [`transfers`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Transfer) | The `transfers` register registrerar information om medel som flyttats mellan konton. Attribut inkluderar överförings-ID, belopp, kontoinformation och datum. |
| [`vendorcredits`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/VendorCredit) | Leverantörskrediter är AP-transaktioner som är återbetalningar eller krediter som ges till leverantörer. The `vendorcredits` registret innehåller leverantörens kredit-ID, radobjektsinformation, leverantörsinformation, AP-konto, totalt belopp och datum. |

{style="table-layout:auto"}

## Namnlisteentiteter {#namelistentities}

| **Tabellnamn** | **Beskrivning** |
|-----|-----|
| [`accounts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Account) | Det här registret innehåller konto-ID, namn, status, typ, saldo, valuta och skapandetid. |
| [`budgets`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Budget) | Det här registret registrerar all information som rör företagsbudgetar, inklusive budget-ID, namn, start- och slutdatum, typ, status och detaljer. |
| [`classes`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Class) | Med klasser, som tillämpas på detaljrader med transaktioner, kan du spåra segment som inte är kopplade till en klient eller ett projekt. Det här registret registrerar klass-ID, namn, underklass och status. |
| [`customers`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Customer) | The `customers` tabellen innehåller all information om dina kunder, inklusive kundens ID, namn, fakturerings- och leveransadress, telefonnummer och e-postadress. |
| [`departments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Department) | The `departments` tabellen innehåller avdelnings-ID, namn och typ (underavdelning respektive avdelning på den översta nivån). |
| [`employees`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Employee) | The `employees` register registrerar information om de personer som arbetar för ditt företag. Attributen omfattar medarbetarens ID, namn, adress, telefonnummer och fakturerbar information, om företaget har löneaktiverat. |
| [`items`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Item) | The `items` tabellen innehåller information om produkter eller tjänster som ditt företag säljer. Det här registret innehåller information om artikel-ID, namn, beskrivning, pris per enhet, typ, inköpsinformation, lagerbehållning samt information om intäkter och tillgångskonto. |
| [`paymentmethods`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/PaymentMethod) | The `paymentmethods` register registrerar den betalningsmetod som mottagits för varor och tjänster. Den innehåller betalnings-ID, typ och namn. |
| [`taxagencies`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxAgency) | I det här registret registreras information om skattemyndigheter, inklusive skattemyndighets-ID, och spårningsinformation om skatter för inköp och försäljning. |
| [`taxcodes`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxCode) | Skattekoder används för att spåra skattestatus (skattepliktig kontra icke-beskattningsbar) för produkter, tjänster och kunder. The `taxcodes` tabellen innehåller momskod-ID, namn, beskrivning, status, skattestatus, skattesats och momsgrupp. |
| [`taxrates`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxRate) | Skattesatser används för att beräkna skatteskulder. Det här registret innehåller momsregistreringsnummer, namn, beskrivning, skattesats, skattemyndighet med mera. |
| [`terms`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Term) | Den här enheten representerar villkoren för försäljning. Termtabellen innehåller termen ID, namn, typ, rabattprocent och förfallodagar. |
| [`vendors`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Vendor) | Registret Leverantörer innehåller information om de leverantörer du köper från. Registerattributen innehåller leverantörs-ID, företagsnamn, kontonummer, kontosaldo, 1099-status, faktureringsadress, telefonnummer, e-postadress och webbadress. |

{style="table-layout:auto"}

## Relaterat:

* [Ansluter [!DNL QuickBooks]](../integrations/quickbooks.md)
* [Återautentisera integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
