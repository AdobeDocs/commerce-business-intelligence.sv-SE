---
title: Förväntade Facebook Ads-data
description: Lär dig en kort översikt över de tabeller som rekommenderas när du synkroniserar med din Data Warehouse
exl-id: 0c8b907b-1a98-470b-bb2c-55327e88e502
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '303'
ht-degree: 0%

---

# [!DNL Facebook Ads] data förväntades

När du har [anslutit ditt [!DNL Facebook Ads] konto](../integrations/facebook-ads.md) kan du använda [Data Warehouse Manager](../../../data-analyst/data-warehouse-mgr/tour-dwm.md) för att enkelt spåra relevanta datafält för analys.

I det här avsnittet finns en kort översikt över de tabeller som Adobe rekommenderar att du synkroniserar med din Data Warehouse. Det här visar bara huvudtabellerna, eftersom det finns några deltabeller.

## Huvudtabeller för annonskampanjer

Dessa tabeller innehåller data om viktiga komponenter i annonskampanjer.

### [`facebook _campaigns_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign-group)

Det här registret är huvudtabellen för kampanjer i ett [!DNL Facebook Ads]-konto. Kolumnerna är `campaign id`, `name`, `status (active/paused)`, `objective`.

### [`facebook _adsets_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-campaign)

Den här tabellposten är huvudtabellen för [!DNL Facebook Ads] uppsättningar i ett [!DNL Facebook Ads]-konto. Kolumnerna innehåller annonsen `Campaign id/name` som annonsuppsättningen tillhör, information om budgetering, budtyp, planering och målgruppsanpassning.

### [`facebook _ads_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/adgroup)

Den här tabellen registrerar alla annonser i ett [!DNL Facebook Ads]-konto. Kolumnerna innehåller annonsinformation, inklusive annonsuppsättningen och annonskampanjen som den tillhör, annonsinbjudanden, annonsinriktning och referens till specifik kreativ (bild/text) som annonsen använder.

### [`facebook _adcreative_ (account-id)`](https://developers.facebook.com/docs/marketing-api/reference/ad-creative)

Den här tabellen registrerar kreatörer som används i [!DNL Facebook Ads]. Creative Cloud innehåller kreativa namn, beskrivning och relevanta bild-URL:er där det är lämpligt.

## Segmenterade kampanjtabeller

Följande tabeller innehåller en post för varje kampanj/uppsättning/annonskombination för varje dag, segmenterad efter dimensioner som ålder, kön och land.

### `facebook _ads insights_ (account-id)`

Tabellen innehåller ett tävlingsbidrag för varje kampanj/uppsättning/annonskombination för varje dag, tillsammans med statistik, inklusive visningar, klickningar, kostnad, cpc, cpm, cpp, ctr, räckvidd, social räckvidd och utgifter.

### `facebook _ads insights_ (account-id)_~\_actions`

Det här är en deltabell av tabellen `facebook_ads_insights_{account_id}`. Det innehåller konverteringsdata för åtgärder som utförs baserat på olika kampanjer.

### `facebook _ads insights country_ (account-id)`

Tabellen innehåller samma information som tabellen `facebook_ads_insights_{account_id}` och segmenterar den per land.

### `facebook ads insights age and gender (account-id)`

Tabellen innehåller samma information som tabellen `facebook_ads_insights_{account_id}` och segmenterar den efter ålder och kön.

## Relaterad

* [Ansluter  [!DNL Facebook Ads]](../integrations/facebook-ads.md)
* [Återautentiserar integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=sv-SE)
