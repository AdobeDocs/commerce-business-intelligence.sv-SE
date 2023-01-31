---
title: Förväntade lagrade data för Google Analytics
description: Lär dig interagera med lagerdata från Google Analytics.
exl-id: 2b1305cd-5f34-43d9-b77f-a4f5b1d82c66
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '383'
ht-degree: 0%

---

# Förväntat [!DNL Google Analytics] Lagrade data

>[!NOTE]
>
>Kräver [Administratörsbehörigheter](../../../administrator/user-management/user-management.md).

>[!NOTE]
>
>Viss information används med tillstånd från våra vänner på [[!DNL Stitch]](https://www.stitchdata.com/docs/integrations/saas/google-analytics).

[!DNL Google Analytics Warehoused] integration i [!DNL MBI] använder [!DNL Google Analytics] [API för huvudrapportering](https://developers.google.com/analytics/devguides/reporting/core/v3/).

>[!NOTE]
>
>För att undvika oväntade eller okänsliga resultat bör du kontrollera att de dimensioner du använder är [kompatibel med måtten](https://developers.google.com/analytics/devguides/reporting/core/dimsmets) du använder i `Report Builder`.

En enda tabell - anropad `report` - kommer att skapas i Data warehouse.

Schemat för den här tabellen består av de mått och Dimensioner som du valde under konfigurationsprocessen och två andra kolumner: `start-date` och `end-date`.

Om du till exempel valde följande mått och Dimensioner under installationen:

* `Metrics`: `ga:users`
* `Dimensions`: `ga:month`

Tabellen skulle se ut som exemplet nedan.

| **Kolumnnamn** | **Beskrivning** |
|-----|-----|
| `\_id` | Den här kolumnen är `primary key`. |
| `\_rjm\_record\_hash` | [!DNL MBI] unik identifierare. Den här kolumnen skapas av [!DNL MBI]. |
| `\_updated\_at` | Den här kolumnen innehåller den senaste gången dataraden uppdaterades. Den här kolumnen skapas av [!DNL MBI]. |
| `start-date` | Identifiering av vilken dag raden är avsedd för. |
| `end-date` | Identifiering av vilken dag raden är avsedd för. |
| `month` | Vald dimension: Månad i sessionen, ett tvåsiffrigt heltal mellan 01 och 12. |
| `users` | Markerat mätvärde: Det totala antalet användare för den begärda tidsperioden. |

{style=&quot;table-layout:auto&quot;}

## Påminnelse: Skillnaden mellan Google Analytics Warehouse och Live Integration

Den viktigaste skillnaden är att en integrering sparas ([!DNL Google Analytics Warehoused]) och den andra inte ([!DNL Google Analytics Live]). Om [!DNL Google Analytics Warehoused]kan du manipulera [!DNL Google Analytics] data och ger er möjlighet att kombinera [!DNL Google Analytics] och andra datakällor för att skapa insiktsfull rapportering.

Låt oss titta på [!DNL Google Analytics] annonskampanjer för ett exempel på vad som kan göras från en manipulation. Anta att ni har haft flera annonskampanjer för Q4 med olika namn. Kampanjerna var ett resultat av ett specifikt marknadsföringsinitiativ. Med lagrade data kan vi skapa en ny kolumn som hittar kampanjnamnen i fråga och returnerar Q4-initialnamnet för `Operation Dumbo`.

Kombinationsaspekten tillåter [!DNL Google Analytics] Uppgifter som ska sammanfogas med andra uppgifter för att utföra analyser. Ta till exempel `Total Time On Site By Ad Campaign` data från [!DNL Google Analytics] och förena dem mot `Total Spent Per Campaign` data från [!DNL Facebook Ads] för att få en fullständig bild av hur mycket engagemang kostar er.

Med [!DNL Google Analytics Live] integrering, å andra sidan, [!DNL Google Analytics] diagram är som en liten silo som inte lagras i [!DNL MBI] data warehouse.

## Relaterat:

* [Ansluter [!DNL Google Analytics Warehoused]](../integrations/google-analytics-warehoused.md)
