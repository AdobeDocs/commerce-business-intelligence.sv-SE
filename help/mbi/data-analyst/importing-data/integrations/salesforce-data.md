---
title: Förväntade Salesforce-data
description: Lär dig mer om objekt som stöds och som inte stöds i Salesforce-data.
exl-id: 6625349f-2ec0-402d-8635-889a1f29811c
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---

# Förväntat [!DNL Salesforce] data

[Efter [!DNL Salesforce] installationen är klar](../integrations/salesforce.md), en tabell för varje frågningsbar [object](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_objects_concepts.htm) - namngivna `sf_/\{sobject-name}` - kommer att skapas i data warehouse.

>[!NOTE]
>
>Strukturen (kolumnerna) för varje tabell är beroende av fälten i objektet.

En lista över objekt som är tillgängliga för din organisation finns i [!DNL Salesforce] [Hämta en lista med objektdokumentation](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_describeGlobal.htm). När du har en lista över objekt kan du titta på [Avsnittet Enhetsrelationsdiagram (ERD)](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_erd_majors.htm) av [!DNL Salesforce] dokumentation som visar hur enheter relaterar till varandra.

## Objekt som inte stöds

För närvarande [!DNL Salesforce] visar för närvarande inte följande objekt i deras API:

* `Announcement`
* `Attachment`
* `ContentDocumentLink`
* `External objects` - [Vad är ett externt objekt?](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_objects_external_objects.htm)
* `CollaborationGroupRecord`
* `ContentDocument`
* `ContentDocumentLink`
* `FeedItem`
* `FieldDefinition`
* `IdeaComment`
* `ListViewChartInstance`
* `Order`
* `PlatformAction`

* `KnowledgeArticleVersion`
* `NewsFeed`
* `RecentlyViewed`
* `TopicAssignment`
* `UserRecordAccess`
* `UserProfileFeed`
* `Vote`

## Relaterat:

* [Ansluter [!DNL Salesforce]](../integrations/salesforce.md)
* [Återautentisera integreringar](https://support.magento.com/hc/en-us/articles/360016733151)
