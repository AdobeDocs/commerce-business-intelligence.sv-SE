---
title: QuickBooks-data förväntades
description: Lär dig att enkelt spåra relevanta datafält för analys.
exl-id: a60996bd-e3d1-497d-abce-f02ef1444f1a
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '796'
ht-degree: 0%

---

# [!DNL QuickBooks] data förväntades

När [du har anslutit ditt [!DNL QuickBooks] konto](../../../data-analyst/importing-data/integrations/quickbooks.md) kan du använda [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) för att enkelt spåra relevanta datafält för analys. Följande tabeller skapas i din Data Warehouse:

Om du vill visa alla fält som är tillgängliga för spårning klickar du på länkarna i tabellnamnskolumnen.

## Transaktionsenheter {#transactionentities}

| **Tabellnamn** | **Beskrivning** |
|-----|-----|
| [`bill`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Bill) | Registret `bills` innehåller information om AP-transaktioner eller en betalningsförfrågan från en tredje part. Attribut omfattar valutatyp, valutakurs, totalt belopp, förfallodatum, saldo med mera. |
| [`billpayments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/BillPayment) | `BillPayment` enheter är den slutliga transaktionen för betalning av räkningar som tagits emot från en leverantör. Det här registret innehåller leverantörsinformation, betalningstyp, totalt belopp, transaktionsdatum med mera. |
| [`creditmemos`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/CreditMemo) | Registret `creditmemos` registrerar transaktioner som är återbetalningar eller krediter för både fullständiga och partiella betalningar. Vissa attribut inkluderar kundens namn, kundens fakturerings- och leveransinformation, belopp och datum. |
| [`deposits`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Deposit) | `Deposits` inkluderar direkta insättningar och kundbetalningar som flyttats till tillgångskontot efter att ha hållits i `Undeposited Funds`-kontot. Attributen innehåller belopp, insättnings-ID och datum. |
| [`estimates`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Estimate) | `Estimates` är transaktioner som ges till kunder som inkluderar föreslagna priser för en vara eller tjänst. Det här registret visar belopp, rabattinformation, kundinformation och datum. |
| [`invoices`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Invoice) | `Invoices` är försäljningsformulär som en kund betalar senare. Fakturaregistret registrerar insättningsinformation, datum, radobjekt, skatteinformation och kundinformation. |
| [`journalentries`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/JournalEntry) | Registret `journalentries` registrerar AR- och AP-kontoinformation, inklusive journalpost-ID, transaktionsdatum och radartikelinformation. |
| [`payments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Payment) | En `payment`-post innehåller attribut som betalnings-ID, tillämpade och ej tillämpade belopp, transaktionsdatum, transaktionstyp och bearbetningsstatus. |
| [`purchases`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Purchase) | Tabellen `purchases` representerar dina utgifter och innehåller information om inköp-ID, betalningstyp, belopp och radartiklar. |
| [`purchaseorders`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/PurchaseOrder) | Registret `purchaseorders` innehåller begäranden om varor som skickas till leverantörer. Det här registret innehåller information om leverantör, inköpsordernummer, transaktionsdatum, radobjektsinformation, totalt belopp och information om AP-konto. |
| [`refundreceipts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/RefundReceipt) | Registret `refundreceipts` registrerar återbetalningar som ges till kunder. Attribut är bl.a. inbetalnings-ID, radobjektsinformation, totalbelopp, kundinformation och saldo. |
| [`salesreceipts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/SalesReceipt) | Registret `salesreceipts` registrerar information i de kvitton som skickas till kunder, inklusive försäljningskvitto-ID, radobjektsinformation, totalt belopp, kundinformation, transaktionsdatum och eventuella insättningar. |
| [`timeactivities`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TimeActivity) | Registret `timeactivities` innehåller tidsposter för leverantörer och/eller anställda och innehåller information om tidsaktivitet, personal/leverantör, loggad tid, aktivitetsbeskrivning och inspelat datum. |
| [`transfers`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Transfer) | Registret `transfers` registrerar information om medel som flyttats mellan konton. Attribut inkluderar överförings-ID, belopp, kontoinformation och datum. |
| [`vendorcredits`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/VendorCredit) | Leverantörskrediter är AP-transaktioner som är återbetalningar eller krediter som ges till leverantörer. Registret `vendorcredits` innehåller leverantörskreditid, radobjektsinformation, leverantörsinformation, AP-konto, totalt belopp och datum. |

{style="table-layout:auto"}

## Namnlisteentiteter {#namelistentities}

| **Tabellnamn** | **Beskrivning** |
|-----|-----|
| [`accounts`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Account) | Det här registret innehåller konto-ID, namn, status, typ, saldo, valuta och skapandetid. |
| [`budgets`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Budget) | Det här registret registrerar all information som rör företagsbudgetar, inklusive budget-ID, namn, start- och slutdatum, typ, status och detaljer. |
| [`classes`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Class) | Med klasser, som tillämpas på detaljrader med transaktioner, kan du spåra segment som inte är kopplade till en klient eller ett projekt. Det här registret registrerar klass-ID, namn, underklass och status. |
| [`customers`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Customer) | Tabellen `customers` innehåller all information som rör dina kunder, inklusive kundens ID, namn, fakturerings- och leveransadress, telefonnummer och e-postadress. |
| [`departments`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Department) | Tabellen `departments` innehåller avdelnings-ID, namn och typ (underavdelning respektive översta avdelning). |
| [`employees`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Employee) | Registret `employees` registrerar information om de personer som arbetar för ditt företag. Attributen omfattar medarbetarens ID, namn, adress, telefonnummer och fakturerbar information, om företaget har löneaktiverat. |
| [`items`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Item) | Tabellen `items` innehåller information om produkter eller tjänster som ditt företag säljer. Det här registret innehåller information om artikel-ID, namn, beskrivning, pris per enhet, typ, inköpsinformation, lagerbehållning samt information om intäkter och tillgångskonto. |
| [`paymentmethods`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/PaymentMethod) | Registret `paymentmethods` registrerar betalningsmetoden som tagits emot för varor och tjänster. Den innehåller betalnings-ID, typ och namn. |
| [`taxagencies`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxAgency) | I det här registret registreras information om skattemyndigheter, inklusive skattemyndighets-ID, och spårningsinformation om skatter för inköp och försäljning. |
| [`taxcodes`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxCode) | Skattekoder används för att spåra skattestatus (skattepliktig kontra icke-beskattningsbar) för produkter, tjänster och kunder. Registret `taxcodes` innehåller momskod-ID, namn, beskrivning, status, skattestatus, skattesats och momsgrupp. |
| [`taxrates`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/TaxRate) | Skattesatser används för att beräkna skatteskulder. Det här registret innehåller momsregistreringsnummer, namn, beskrivning, skattesats, skattemyndighet med mera. |
| [`terms`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Term) | Den här enheten representerar villkoren för försäljning. Termtabellen innehåller termen ID, namn, typ, rabattprocent och förfallodagar. |
| [`vendors`](https://developer.intuit.com/app/developer/qbo/docs/api/accounting/all-entities/Vendor) | Registret Leverantörer innehåller information om de leverantörer du köper från. Registerattributen innehåller leverantörs-ID, företagsnamn, kontonummer, kontosaldo, 1099-status, faktureringsadress, telefonnummer, e-postadress och webbadress. |

{style="table-layout:auto"}

## Relaterat:

* [Ansluter  [!DNL QuickBooks]](../integrations/quickbooks.md)
* [Återautentiserar integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
