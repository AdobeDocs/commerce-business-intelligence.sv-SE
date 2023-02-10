---
title: Förväntade Salesforce-data
description: Lär dig mer om objekt som stöds och som inte stöds i Salesforce-data.
exl-id: 6625349f-2ec0-402d-8635-889a1f29811c
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%

---

# Förväntat [!DNL Salesforce] data

[Efter [!DNL Salesforce] installationen är klar](../integrations/salesforce.md), en tabell för varje frågningsbar [object](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_objects_concepts.htm) - namngivna `sf_/\{sobject-name}` - kommer att skapas i data warehouse.

>[!NOTE]
>
>Strukturen (kolumnerna) för varje tabell är beroende av fälten i objektet.

En lista över objekt som är tillgängliga för din organisation finns i [!DNL Salesforce] [Hämta en lista med objektdokumentation](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_describeGlobal.htm). När du har en lista över objekt kan du titta på [Avsnittet Enhetsrelationsdiagram (ERD)](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_erd_knowledge.htm) av [!DNL Salesforce] dokumentation som visar hur enheter relaterar till varandra.

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
* [Återautentisera integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
