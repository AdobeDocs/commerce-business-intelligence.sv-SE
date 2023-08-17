---
title: Förväntade Salesforce-data
description: Lär dig mer om objekt som stöds och som inte stöds i Salesforce-data.
exl-id: 6625349f-2ec0-402d-8635-889a1f29811c
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '162'
ht-degree: 0%

---

# Förväntat [!DNL Salesforce] data

Efter [[!DNL Salesforce] konfiguration](../integrations/salesforce.md) är klar, en tabell för varje frågerbar [object](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_objects_concepts.htm) - namngivna `sf_/\{sobject-name}` - har skapats i din Data Warehouse.

>[!NOTE]
>
>Strukturen (kolumnerna) för varje tabell beror på fälten i objektet.

En lista över objekt som är tillgängliga för din organisation finns i [!DNL Salesforce] [Hämta en lista med objektdokumentation](https://developer.salesforce.com/docs/atlas.en-us.api_rest.meta/api_rest/dome_describeGlobal.htm). När du har en lista över objekt kan du titta på [Avsnittet Enhetsrelationsdiagram (ERD)](https://developer.salesforce.com/docs/atlas.en-us.object_reference.meta/object_reference/sforce_api_erd_knowledge.htm) av [!DNL Salesforce] dokumentation som visar hur enheter relaterar till varandra.

## Objekt som inte stöds

För närvarande [!DNL Salesforce] visar för närvarande inte följande objekt i deras API:

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

* [Ansluter [!DNL Salesforce]](../integrations/salesforce.md)
* [Återautentisera integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
