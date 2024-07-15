---
title: Förväntade lagrade data för Google Analytics
description: Lär dig interagera med lagerdata från Google Analytics.
exl-id: 2b1305cd-5f34-43d9-b77f-a4f5b1d82c66
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 0%

---

# [!DNL Google Analytics Warehoused] data förväntades

>[!NOTE]
>
>Kräver [administratörsbehörighet](../../../administrator/user-management/user-management.md).

>[!NOTE]
>
>Viss information användes med tillstånd från dina vänner på [[!DNL Stitch]](https://www.stitchdata.com/docs/integrations/saas/google-analytics).

Integrationen [!DNL Google Analytics Warehoused] i [!DNL Commerce Intelligence] använder [!DNL Google Analytics] [Core Reporting API](https://developers.google.com/analytics/devguides/reporting/core/v3/).

>[!NOTE]
>
>För att undvika oväntade eller okänsliga resultat bör du kontrollera att de dimensioner du använder är [kompatibla med ett eller flera mått](https://ga-dev-tools.google/dimensions-metrics-explorer/) som du använder i `Report Builder`.

En enda tabell med namnet `report` skapas i Datan Warehouse.

Schemat för den här tabellen består av de mått och Dimensioner som du valde under konfigurationsprocessen och två andra kolumner: `start-date` och `end-date`.

Om du till exempel valde följande mått och Dimensioner under installationen:

* `Metrics`: `ga:users`
* `Dimensions`: `ga:month`

Tabellen skulle se ut som exemplet nedan.

| **Kolumnnamn** | **Beskrivning** |
|-----|-----|
| `\_id` | Den här kolumnen är `primary key`. |
| `\_rjm\_record\_hash` | [!DNL Commerce Intelligence] unik identifierare. Den här kolumnen skapas av [!DNL Commerce Intelligence]. |
| `\_updated\_at` | Den här kolumnen innehåller den senaste gången dataraden uppdaterades. Den här kolumnen skapas av [!DNL Commerce Intelligence]. |
| `start-date` | Identifiering av vilken dag raden är avsedd för. |
| `end-date` | Identifiering av vilken dag raden är avsedd för. |
| `month` | Vald dimension: Månad i sessionen, ett tvåsiffrigt heltal mellan 01 och 12. |
| `users` | Markerat mätvärde: Det totala antalet användare för den begärda tidsperioden. |

{style="table-layout:auto"}

## Vad är skillnaden mellan [!DNL Google Analytics Warehoused] och [!DNL Live Integration]?

Den huvudsakliga differentiatorn är att en integrering lagras ([!DNL Google Analytics Warehoused]) och den andra inte är ([!DNL Google Analytics Live]). I fall med [!DNL Google Analytics Warehoused] tillåter detta att dina [!DNL Google Analytics]-data ändras och ger dig möjlighet att kombinera [!DNL Google Analytics] och andra datakällor för att skapa insikter om rapportering.

Titta på [!DNL Google Analytics] annonskampanjer för att få ett exempel på vad som kan göras från en manipuleringssynpunkt. Anta att ni har haft flera annonskampanjer för Q4 med olika namn. Kampanjerna var ett resultat av ett specifikt marknadsföringsinitiativ. Med lagrade data kan du skapa en kolumn som hittar kampanjnamnen i fråga och returnerar Q4-initialnamnet för `Operation Dumbo`.

Kombinationsaspekten tillåter att [!DNL Google Analytics] data kopplas till andra data för att utföra analyser. Ta t.ex. `Total Time On Site By Ad Campaign` data från [!DNL Google Analytics] och anslut dem till `Total Spent Per Campaign` data från [!DNL Facebook Ads] för att få en fullständig bild av hur mycket engagemang som kostar er.

Med integreringen av [!DNL Google Analytics Live] å andra sidan är varje [!DNL Google Analytics]-diagram som en liten silo som inte lagras i din [!DNL Commerce Intelligence]-Data Warehouse.

## Relaterat:

* [Ansluter  [!DNL Google Analytics Warehoused]](../integrations/google-analytics-warehoused.md)
