---
title: Förväntade Zendesk-data
description: Lär dig de viktigaste datatabeller du kan importera från Zendesk till Commerce Intelligence, inklusive länkar till ytterligare dokumentation om Zendesk-data.
exl-id: 838d8d13-e2e1-44c2-a416-f1792200ee6f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 0%

---

# [!DNL Zendesk] data förväntades

När [du har anslutit ditt [!DNL Zendesk] konto](../integrations/zendesk.md) kan du använda [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) för att enkelt spåra relevanta datafält för analys.

I det här avsnittet utforskas huvuddatatabellerna som du kan importera från [!DNL Zendesk] till [!DNL Adobe Commerce Intelligence], inklusive länkar till ytterligare dokumentation om [!DNL Zendesk]-data.

| Tabellnamn | Beskrivning |
|-----|-----|
| [`Audits`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits) | Registeraktiviteten `Audits` som är associerad med en biljett, inklusive statusändringar och både kund- och agentsvar. Det här registret innehåller ett biljett-ID som länkar tillbaka till tabellen `Tickets`, som gör att du kan analysera tiden för första svar och tiden till lösning för varje biljett. |
| [`Audit_~\_Events`](https://developer.zendesk.com/rest_api/docs/core/ticket_audits#audit-events) | Tabellen `audit_~\_events` är underordnad tabellen `audits` och registrerar ytterligare information om en biljetthändelse. |
| [`Organizations`](https://developer.zendesk.com/rest_api/docs/core/organizations) | Registret `Organizations` lagrar företagsinformation om dina slutanvändare, till exempel namn, ID, associerade domännamn, taggar och anpassade fält. |
| [`Tickets`](https://developer.zendesk.com/rest_api/docs/core/tickets) | Tabellen `Tickets` registrerar all biljettinformation, inklusive tidsstämpeln `created_at` och `requester\_id` och `assignee\_id` som gör att du kan länka en biljett till en slutanvändare och agent i tabellen `Users`. |
| [`Ticket_~\_Fields`](https://developer.zendesk.com/rest_api/docs/core/ticket_fields) | Tabellen `ticket fields` innehåller information om grundläggande textfält och anpassade biljettfält i ditt konto. Attribut för den här tabellen omfattar fältet `ID`, `URL`, `type`, `title`, `description`, `position`, `requirement setting`, agent- och slutanvändarspecifik information samt information om att skapa och uppdatera. |
| [`Users`](https://developer.zendesk.com/rest_api/docs/core/users) | Tabellen `Users` innehåller all information om slutanvändare och agenter, inklusive personens namn och e-postadress. På så sätt kan ni analysera både slutanvändarnas engagemang och hur agenterna fungerar. |
| [`Zendesk\_Groups`](https://developer.zendesk.com/rest_api/docs/core/groups) | Grupper är hur agenter är organiserade i ditt Zendesk-konto. Tabellen `Groups` registrerar information som `group ID`, `URL`, `name` samt information om att skapa och uppdatera. |
| [`Zendesk\_Macro`](https://developer.zendesk.com/rest_api/docs/core/macros) | Makron är åtgärder som definieras av dig och som ändrar värdena i en biljettens fält. Den här tabellen innehåller attribut som makrots titel, ID, åtgärder, begränsningar samt information om skapande och uppdatering. |
| [`Zendesk\_Tags`](https://developer.zendesk.com/rest_api/docs/core/tags) | Tabellen `Tags` innehåller en lista med alla taggar i ditt konto. |
| [`Zendesk\_Ticket\_Metrics`](https://developer.zendesk.com/rest_api/docs/core/ticket_metrics#ticket-metrics) | Det här registret innehåller data om biljettmått. Fälten innehåller information om `ticket ID`, `URL` och antalet grupper, tilldelningar, återöppningar, svar, svarstid (i minuter), fullständig matchningstid och senaste uppdatering (till exempel status, tilldelad eller begärande). |

{style="table-layout:auto"}

## Relaterad

* [Ansluter Zendesk](../integrations/zendesk.md)
* [Återautentiserar integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
