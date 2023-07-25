---
title: Connect Google Analytics Warehouse
description: Lär dig att spåra hur besökarna använder er webbplats, vilket innehåll som är attraktivt, var besökarna lämnar webbplatsen och mycket annat.
exl-id: b9879399-9e1a-4f36-b510-8426ebc83aeb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 0%

---

# Anslut [!DNL Google Analytics Warehoused]

>[!NOTE]
>
>Kräver [Administratörsbehörigheter](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] är den vanligaste webbanalystjänsten på Internet. Implementering [!DNL Google Analytics] på er webbplats kan ni spåra hur besökarna använder er webbplats, vilket innehåll som är attraktivt, var besökarna lämnar webbplatsen och mycket annat. [!DNL Google Analytics Warehoused] är en separat integrering från din befintliga [!DNL Google Analytics] integrering. Det ger bättre analys tack vare att [!DNL Google Analytics] data i Data warehouse, som skiljer sig från den befintliga livematningen [!DNL Google Analytics] integrering. Analysera mätvärdena i [!DNL Commerce Intelligence], tillsammans med andra data, förbättrar webbplatsens övergripande hälsa och användbarhet.

## Skillnaden mellan GA Warehouse och Live Integration

Den viktigaste skillnaden är att en integrering sparas ([!DNL Google Analytics Warehoused]) och den andra inte ([!DNL Google Analytics Live]). Om [!DNL Google Analytics Warehoused]kan du manipulera [!DNL Google Analytics] data och ger er möjlighet att kombinera [!DNL Google Analytics] och andra datakällor för att skapa insiktsfull rapportering.

Titta på [!DNL Google Analytics] annonskampanjer för ett exempel på vad som kan göras från en manipulation. Anta att ni hade flera annonskampanjer för fjärde kvartalet med olika namn. Kampanjerna var ett resultat av ett specifikt marknadsföringsinitiativ. Med lagrade data kan du skapa en kolumn som hittar kampanjnamnen i fråga och returnerar det fjärde kvartalets initialnamn för `Operation Dumbo`.

Kombinationsaspekten tillåter [!DNL Google Analytics] Uppgifter som ska sammanfogas med andra uppgifter för att utföra analyser. Ta till exempel `Total Time On Site By Ad Campaign` data från [!DNL Google Analytics] och förena dem mot `Total Spent Per Campaign` data från [!DNL Facebook Ads] för att få en fullständig bild av hur mycket engagemang kostar er.

Med [!DNL Google Analytics Live] integrering, å andra sidan, [!DNL Google Analytics] diagram är som en liten silo som inte är lagrad i Data warehouse.

## Ansluter [!DNL Google Analytics Warehoused]

>[!INFO]
>
>[!DNL Google Analytics Warehoused] är en `Premium` Integrering. [Kontakta support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) om du vill lägga till den här integreringen i din prenumeration.

1. Gå till `Connections` sida under **[!UICONTROL Admin** > **Integrations]**.
1. Klicka **[!UICONTROL Add an Integration]**, till höger.
1. Klicka på [!DNL Google Analytics Warehoused] ikon. Då öppnas [!DNL Google Analytics] inloggningssida.
1. Ange [!DNL Google Analytics] autentiseringsuppgifter. När auktoriseringsprocessen är slutförd omdirigeras du tillbaka till [!DNL Commerce Intelligence].
1. En lista över profil-ID:n visas. Kontrollera de profiler som du vill ansluta till [!DNL Commerce Intelligence]. Om du har flera profiler och behöver hjälp med att identifiera vilket som är det, se Ansluter flera [!DNL Google Analytics] profilavsnittet nedan.

## Ansluta flera [!DNL Google Analytics] profiler

Du kan ha flera webbplatser anslutna till en enda [!DNL Google Analytics] konto, som identifieras av deras egna [!DNL Google Analytics] profil-ID. I det här fallet kan du välja att ta med alla dina profil-ID:n i [!DNL Commerce Intelligence]. Kontrollera de profil-ID som du vill inkludera under steget för profilval.

Identifiera en viss webbplats [!DNL Google Analytics] Profil-ID:

1. Logga in [!DNL Google Analytics]
1. Gå till webbplatsens [!DNL Google Analytics] kontrollpanel
1. Titta på URL:en - profil-ID:t motsvarar de åtta siffror som följer `p` i slutet av raden

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Kopplar från [!DNL Google Analytics Warehoused] från [!DNL Commerce Intelligence] {#disconnect}

1. Besök [!DNL Google Analytics] [kontoinställningar](https://myaccount.google.com/intro) sida.
1. Under `Security` och klicka **[!UICONTROL edit]** nästa `Authorizing` program och webbplatser.
1. Klicka **[!UICONTROL revoke access]** nästa [!DNL Commerce Intelligence].

## Relaterad dokumentation

* [Återautentisera integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Ansluter [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Analysera webbplatsaktivitet och kundkonverteringsgrader](../../analysis/web-act-cust-conversion.md)
* [Spåra kundvärvningsdata med [!DNL Google Analytics] cookies](../../analysis/google-track-user-acq.md)
