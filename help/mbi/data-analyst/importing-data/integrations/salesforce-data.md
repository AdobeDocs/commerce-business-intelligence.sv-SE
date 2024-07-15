---
title: Förväntade Salesforce-data
description: Lär dig mer om objekt som stöds och som inte stöds i Salesforce-data.
exl-id: 6625349f-2ec0-402d-8635-889a1f29811c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 0%

---

# [!DNL Salesforce] data förväntades

När [[!DNL Salesforce] setup](../integrations/salesforce.md) har slutförts skapas en tabell för varje frågningsbart [objekt](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_concepts.htm) - med namnet `sf_/\{sobject-name}` - i Datan Warehouse.

>[!NOTE]
>
>Strukturen (kolumnerna) för varje tabell beror på fälten i objektet.

En lista över objekt som är tillgängliga för din organisation finns i [!DNL Salesforce] [Hämta en lista med objekt-dokumentation](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_describeGlobal.htm). När du har en lista över objekt kan du läsa igenom [enhetsrelationsdiagrammet (ERD)](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_erd_knowledge.htm) i [!DNL Salesforce] -dokumentationen för att se hur entiteter relaterar till varandra.

## Objekt som inte stöds

[!DNL Salesforce] visar för närvarande inte följande objekt i sin API:

* `Announcement`
* `Attachment`
* `ContentDocumentLink`
* `External objects` - [Vad är ett externt objekt?](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_external_objects.htm)
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

* [Ansluter  [!DNL Salesforce]](../integrations/salesforce.md)
* [Återautentiserar integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
