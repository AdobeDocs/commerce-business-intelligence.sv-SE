---
title: Help desk-rapportering för Zendesk
description: Läs om era mest värdefulla hänvisningskanaler.
exl-id: b6142ef2-2be8-401f-ac35-f86fc68d204e
source-git-commit: 6b1bd96a0f9ae8bda3ae8db8ca78ad655079f2a4
workflow-type: tm+mt
source-wordcount: '392'
ht-degree: 0%

---

# Help desk-rapportering för [!DNL Zendesk]

>[!NOTE]
>
>Detta är bara tillgängligt för klienter som finns på `Pro` planera och använda den nya arkitekturen. Du har den nya arkitekturen om du har `Data Warehouse Views` avsnitt som är tillgängliga efter markering `Manage Data` i huvudverktygsfältet.

Konsoliderar [!DNL Zendesk] data med transaktionsdatabasen är ett utmärkt sätt att bättre förstå hur kunderna interagerar med era sälj- eller kundframgångsgrupper. Det hjälper er också att veta vilken typ av kunder som använder er supportplattform. I det här avsnittet visas hur du konfigurerar en kontrollpanel för att få detaljerade rapporter om din [!DNL Zendesk] prestanda och band till era transaktionskunder.

Innan du börjar vill du ansluta [[!DNL Zendesk]](../integrations/zendesk.md). Denna analys innehåller [avancerade beräknade kolumner](../../data-warehouse-mgr/adv-calc-columns.md).

<!-- Getting Started -->

## Komma igång

### Kolumner att spåra

* `audits` table
* `_id`
* `created_at`
* `id`
* `ticket_id`
* `_updated_at`

* `audits_~_events` table
* `_sub_id`
* `_id_of_parent`
* `author_id`
* `field_name`
* `public`
* `type`
* `value`

* `tickets` table
* `_id`
* `assignee_id`
* `created_at`
* `id`
* `requester_id`
* `status`
* `updated_at`
* `via_~_source_~_from_~_address`
* `_updated_at`

* `users` table
* `_id`
* `created_at`
* `emails`
* `id`
* `role`
* `updated_at`
* `_updated_at`

### Filteruppsättningar att skapa

* `[!DNL Zendesk] Tickets` table
   * `status != deleted`

* `Filter set name`: `Tickets we count`
* `Filter set logic`:

## Beräknade kolumner

### Kolumner att skapa

* **`[!DNL Zendesk] user's`** table
   * `User is agent? (Yes/No) `
   * 
      * `Column type` - `Same Table > Calculation`

      * `Input columns` - `role`, `email`

      * `SQL Calculation` `- case when `A` is not `null` and `A!=`end-user` sedan `Yes` när `B` är inte `null` och `B` gilla `%@magento.com` sedan `Yes` else `No` end

      * Ersätt `@magento.com` med din domän

      * `Datatype` - `String`

* **`[!DNL Zendesk] audits_~_events`** table
   * Välj en definition: `Joined Column`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] audits_~_events.author_id8`
   * [!UICONTROL One]: `[!DNL Zendesk] users.id`

   * Välj en [!UICONTROL table]: `[!DNL Zendesk] users`
   * Välj en [!UICONTROL column]: `User is agent? (Yes/No)`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits_~_events.author_id = [!DNL Zendesk] users.id`

* **`Author is agent? (Yes/No)`**

* **`[!DNL Zendesk] audits`** table
   * Välj en definition: `Exists`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] audits_~_events._id_of_parent`
   * [!UICONTROL One]: `[!DNL Zendesk] audits._id`

   * Välj en [!UICONTROL table]: `[!DNL Zendesk] audits_~_events`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits_~_events._id_of_parent = [!DNL Zendesk] audits._id`
   * [!UICONTROL Filter]:
   * `field_name` = `status`
   * `type` = `Change`
   * `value` = `solved`

   * Välj en definition: `Exists`
   * Välj en [!UICONTROL table]: `[!DNL Zendesk] audits_~_events`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits_~_events._id_of_parent = [!DNL Zendesk] audits._id`
   * [!UICONTROL Filter]: `Author is agent? (Yes/No)`
   * `type` = `Comment`
   * `public` = `1`

* **`Status changes to solved? (1/0)`**
* **`Is agent comment? (1/0)`**

* **`[!DNL Zendesk] Tickets`** table
   * Välj en definition: `Joined Column`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] tickets.requester_id`
   * [!UICONTROL One]: `[!DNL Zendesk] users.id`

   * Välj en [!UICONTROL table]: `[!DNL Zendesk] users`
   * Välj en [!UICONTROL column]: `email`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.requester_id = [!DNL Zendesk] users.id`

   * Välj en definition: `Joined Column`
   * Välj en [!UICONTROL table]: `[!DNL Zendesk] users`
   * Välj en [!UICONTROL column]: `role`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.requester_id = [!DNL Zendesk] users.id`

   * Välj en definition: `Max`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] audits.ticket_id`
   * [!UICONTROL One]: `[!DNL Zendesk] tickets.id`

   * Välj en [!UICONTROL table]: `[!DNL Zendesk] audits`
   * Välj en [!UICONTROL column]: `created_at`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits.ticket_id = [!DNL Zendesk] tickets.id`
   * [!UICONTROL Filter]:
   * `status` ändrat till `solved = 1`

   * Välj en definition: `Min`
   * Välj en [!UICONTROL table]: `[!DNL Zendesk] audits`
   * Välj en [!UICONTROL column]: `created_at`
   * [!UICONTROL Path]: `[!DNL Zendesk] audits.ticket_id = [!DNL Zendesk] tickets.id`
   * [!UICONTROL Filter]:
   * `Is agent comment? = 1`

* `Requester's email`
* `Requester's role`
* `Ticket's latest solved date`
* `First agent response date`
* `Seconds to resolution`
   * 
      * `Column type` - `Same Table > Date Difference`

      * `Ticket's latest solved date` minus `created_at`

* **`Seconds to first response`**
   * 
      * `Column type` - `Same Table > Date Difference`

      * `First agent response date` minus `created_at`

* **`Requester's ticket number`**
   * 
      * `Column type` - `Same Table > Event Number`

      * `Event Owner` - `requester_id`

      * `Event Rank` - `created_at`

* **`Ticket created_at (hour of day)`**
   * 
      * `Column type` - &quot;Samma tabell > Beräkning&quot;

      * `Input columns` - `created_at`

      * `SQL Calculation` - `to_char(A,'HH24')::int`

      * `Datatype` - heltal

* **`Ticket created_at (day of week)`**
   * 
      * `Column type` - &quot;Samma tabell > Beräkning&quot;

      * `Input columns` - `created_at`

      * `Calculation` - `to_char(A,'D')||'. '||to_char(A,'Day')`

      *`Datatype` – `String`


* **`customer_entity`** table
   * Välj en definition: `Count`
   * [!UICONTROL Create Path]:
   * [!UICONTROL Many]: `[!DNL Zendesk] tickets.email`
   * 

      [!UICONTROL One]: `customer_entity.email`

   * Välj en [!UICONTROL table]: `[!DNL Zendesk] tickets`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.email = customer_entity.email`
   * [!UICONTROL Filter]:
   * `Tickets we count`

* **`User's lifetime number of support tickets requested`**
* **`Has user filed a support ticket? (Yes/No)`**
   * 
      * `Column type` - &quot;Samma tabell > Beräkning&quot;

      * `Input columns` - `User's lifetime number of support tickets requested`

      * `Calculation` - `case when A>0 then 'Yes' else 'No' end`

      * `Datatype` – `String`

* **`[!DNL Zendesk] Tickets`** table
   * Välj en definition: `Joined Column`
   * Välj en [!UICONTROL table]: `customer_entity`
   * Välj en [!UICONTROL column]: `User's lifetime number of support tickets requested`
   * [!UICONTROL Path]: `[!DNL Zendesk] tickets.email = customer_entity.email`

* **`Requester's lifetime number of support tickets`**

## Mått

* **[!DNL Zendesk]Nya biljetter**
   * `Tickets we count`

* I **`[!DNL Zendesk] tickets`** table
* Detta mått utför en **Antal**
* På **`id`** kolumn
* Beställd av **`created_at`** tidsstämpel
* [!UICONTROL Filter]:

* **[!DNL Zendesk]Lösta biljetter**
   * `Tickets we count`
   * status IN `closed, solved`

* I **`[!DNL Zendesk] tickets`** table
* Detta mått utför en **Antal**
* På **`id`** kolumn
* Beställd av **`created_at`** tidsstämpel
* [!UICONTROL Filter]:

* **[!DNL Zendesk]Distinkta användare som arkiverar biljetter**
   * `Tickets we count`

* I **`[!DNL Zendesk] tickets`** table
* Detta mått utför en **Distinkt antal**
* På **`requester_id`** kolumn
* Beställd av **`created_at`** tidsstämpel
* [!UICONTROL Filter]:

* **[!DNL Zendesk]Genomsnittlig matchningstid för biljetter**
   * `Tickets we count`
   * status IN `closed, solved`

* I **`[!DNL Zendesk] tickets`** table
* Det här måttet utför en **Medel (eller Median)**
* På **`Seconds to resolution`** kolumn
* Beställd av **`created_at`** tidsstämpel
* [!UICONTROL Filter]:

* **[!DNL Zendesk]Genomsnittlig/mediantid till första svar**
   * Biljetter som räknas
   * status IN closed, resolved

* I **`[!DNL Zendesk] tickets`** table
* Det här måttet utför en **Medel (eller Median)**
* På **`Seconds to first response`** kolumn
* Beställd av **`created_at`** tidsstämpel
* [!UICONTROL Filter]:

>[!NOTE]
>
>Se till att [lägga till alla nya kolumner som dimensioner till mått](../../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) innan du skapar nya rapporter.

### Rapporter

* **[!UICONTROL New/Open/Pending tickets]**
   * [!UICONTROL Metric]: `New Tickets`
   * [!UICONTROL Filter]:
   * status IN `new, open, pending`

* Mått `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Closed/Solved tickets]**
   * [!UICONTROL Metric]: `New Tickets`
   * [!UICONTROL Filter]:
   * status IN `solved, closed`

* Mått `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Average time to first response]**
   * [!UICONTROL Metric]: `Average time to first response`

* Mått `A`: `Average time to first response`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Average time to resolution]**
   * [!UICONTROL Metric]: `Average time to resolution`
   * [!UICONTROL Filter]:
   * status IN `solved, closed`

* Mått `A`: `Average time to resolution`
* `Time period`: `All time`
* `Interval`: `None`
* `Chart Type`: `Scalar`

* **[!UICONTROL Tickets by status]**
   * [!UICONTROL Metric]: `New Tickets`

* Mått `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `status`
* `Chart Type`: `Stacked Column`

* **[!UICONTROL Number of new and solved tickets]**
   * [!UICONTROL Metric]: `New Tickets`

   * [!UICONTROL Metric]: `New Tickets`

* Mått `A`: `New tickets`
* Mått `B`: `Solved tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Line`

* **[!UICONTROL Time to first response]**
   * [!UICONTROL Metric]: `Average time to first response`

* Mått `A`: `Average time to first response`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Time to resolution]**
   * [!UICONTROL Metric]: `Average time to resolution`
   * [!UICONTROL Filter]:
   * status IN `solved, closed`

* Mått `A`: `Average time to resolution`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Distinct users filing tickets]**
   * [!UICONTROL Metric]: `Distinct users filing tickets`

* Mått `A`: `Distinct users filing tickets`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Chart Type`: `Column`

* **[!UICONTROL Peak ticket days]**
   * [!UICONTROL Metric]: `New Tickets`

* Mått `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Group by`: `Ticket created_at (day of week)`
* `Chart Type`: `Pie`

* **[!UICONTROL Peak ticket hours]**
   * [!UICONTROL Metric]:`New Tickets`

   * `Show top/bottom`: `Top 100% sorted by created_at (hour of the day)`

* Mått `A`: `New tickets`
* `Time period`: `All time`
* `Interval`: `None`
* `Group by`: `Ticket created_at (hour of the day)`
* `Chart Type`: `Pie`

* **[!UICONTROL Avg LTV of users who have and have not filed tickets]**
   * [!UICONTROL Metric]: `Average lifetime revenue`

* Mått `A`: `Average lifetime revenue`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `User has filed a support ticket?`
* `Chart Type`: `Column`

* **[!UICONTROL Number of new users who have and have not filed tickets]**
   * 

      [!UICONTROL-mått]: Users

* Mått `A`: `New users`
* `Time period`: `All time`
* `Interval`: `Monthly`
* `Group by`: `User has filed a support ticket?`
* `Chart Type`: `Column`
