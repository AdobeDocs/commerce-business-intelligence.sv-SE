---
title: Förväntade Zendesk-data
description: Lär dig de viktigaste datatabellerna som du kan importera från Zendesk till Commerce Intelligence, inklusive länkar till ytterligare dokumentation om Zendesk-data.
exl-id: 838d8d13-e2e1-44c2-a416-f1792200ee6f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---

# Förväntat [!DNL Zendesk] data

Efter [du har anslutit din [!DNL Zendesk] konto](../integrations/zendesk.md)kan du använda [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) för att enkelt spåra relevanta datafält för analys.

I det här avsnittet beskrivs de huvuddatatabeller som du kan importera från [!DNL Zendesk] till [!DNL Adobe Commerce Intelligence], inklusive länkar till ytterligare dokumentation om [!DNL Zendesk] data.

| Tabellnamn | Beskrivning |
|-----|-----|
| [`Audits`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits) | The `Audits` registerposter aktivitet som är kopplad till en biljett, inklusive statusändringar och både kund- och agentsvar. Tabellen innehåller ett biljett-ID som länkar tillbaka till `Tickets` tabell, som gör att du kan analysera tiden till första svar och tiden till lösning för varje biljett. |
| [`Audit_~\_Events`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits#audit-events) | The `audit_~\_events` tabellen är underordnad `audits` register och registrerar ytterligare information om en biljetthändelse. |
| [`Organizations`](https://developer.zendesk.com/rest_api/docs/core/organizations) | The `Organizations` register registrerar företagsinformation om slutanvändarna, t.ex. namn, ID, associerade domännamn, taggar och anpassade fält. |
| [`Tickets`](https://developer.zendesk.com/rest_api/docs/core/tickets) | The `Tickets` register registrerar all biljettinformation, inklusive `created_at` tidsstämpel och `requester\_id` och `assignee\_id`som gör att du kan länka en biljett till en slutanvändare och agent i `Users` tabell. |
| [`Ticket_~\_Fields`](https://developer.zendesk.com/rest_api/docs/core/ticket_fields) | The `ticket fields` tabellen innehåller information om grundläggande textfält och anpassade biljettfält i ditt konto. Attribut för den här tabellen inkluderar fältet `ID`, `URL`, `type`, `title`, `description`, `position`, `requirement setting`, agent- och slutanvändarspecifik information samt information om att skapa och uppdatera. |
| [`Users`](https://developer.zendesk.com/rest_api/docs/core/users) | The `Users` tabellen innehåller all information om slutanvändare och agenter, inklusive personens namn och e-postadress. På så sätt kan ni analysera både slutanvändarnas engagemang och hur agenterna fungerar. |
| [`Zendesk\_Groups`](https://developer.zendesk.com/rest_api/docs/core/groups) | Grupper är hur agenter är organiserade i ditt Zendesk-konto. The `Groups` registerposter information som `group ID`, `URL`, `name`samt skapa och uppdatera information. |
| [`Zendesk\_Macro`](https://developer.zendesk.com/rest_api/docs/core/macros) | Makron är åtgärder som definieras av dig och som ändrar värdena i en biljettens fält. Den här tabellen innehåller attribut som makrots titel, ID, åtgärder, begränsningar samt information om skapande och uppdatering. |
| [`Zendesk\_Tags`](https://developer.zendesk.com/rest_api/docs/core/tags) | The `Tags` tabellen innehåller en lista med alla taggar i ditt konto. |
| [`Zendesk\_Ticket\_Metrics`](https://developer.zendesk.com/rest_api/docs/core/ticket_metrics#ticket-metrics) | Det här registret innehåller data om biljettmått. Fälten innehåller `ticket ID`, `URL`och antalet grupper, tilldelningar, återöppningar, svar, svarstid (i minuter), full lösningstid och senaste uppdateringsinformation (till exempel status, tilldelad eller begärande). |

{style="table-layout:auto"}

## Relaterad

* [Ansluter Zendesk](../integrations/zendesk.md)
* [Återautentisera integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
