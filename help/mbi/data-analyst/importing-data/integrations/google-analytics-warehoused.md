---
title: Connect Google Analytics Warehouse
description: Lär dig att spåra hur besökarna använder er webbplats, vilket innehåll som är attraktivt, var besökarna lämnar webbplatsen och mycket annat.
exl-id: b9879399-9e1a-4f36-b510-8426ebc83aeb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# Anslut [!DNL Google Analytics Warehoused]

>[!NOTE]
>
>Kräver [administratörsbehörighet](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] är den mest använda webbanalystjänsten på Internet. Genom att implementera [!DNL Google Analytics] på din webbplats kan du spåra hur besökarna använder din webbplats, vilket innehåll som är attraktivt, var besökarna lämnar webbplatsen och mycket annat. [!DNL Google Analytics Warehoused] är en separat integrering med din befintliga [!DNL Google Analytics]-integrering. Det ger en bättre analys eftersom [!DNL Google Analytics]-data finns i Datan Warehouse, vilket skiljer sig från liveflödet i den befintliga [!DNL Google Analytics]-integreringen. Om du analyserar dessa mått i [!DNL Commerce Intelligence], tillsammans med andra datadelar, förbättras webbplatsens övergripande hälsa och användbarhet.

## Skillnaden mellan GA Warehouse och Live Integration

Den huvudsakliga differentiatorn är att en integrering lagras ([!DNL Google Analytics Warehoused]) och den andra inte är ([!DNL Google Analytics Live]). I fallet [!DNL Google Analytics Warehoused] tillåter detta att dina [!DNL Google Analytics]-data ändras och ger dig möjlighet att kombinera [!DNL Google Analytics] och andra datakällor för att skapa insikter om rapportering.

Titta på [!DNL Google Analytics] annonskampanjer för att få ett exempel på vad som kan göras från en manipuleringssynpunkt. Anta att ni hade flera annonskampanjer för fjärde kvartalet med olika namn. Kampanjerna var ett resultat av ett specifikt marknadsföringsinitiativ. Med lagrade data kan du skapa en kolumn som hittar kampanjnamnen i fråga och returnerar det fjärde kvartalets initialnamn `Operation Dumbo`.

Kombinationsaspekten tillåter att [!DNL Google Analytics] data kopplas till andra data för att utföra analyser. Ta t.ex. `Total Time On Site By Ad Campaign` data från [!DNL Google Analytics] och anslut dem till `Total Spent Per Campaign` data från [!DNL Facebook Ads] för att få en fullständig bild av hur mycket engagemang som kostar er.

Med integreringen av [!DNL Google Analytics Live] å andra sidan är varje [!DNL Google Analytics]-diagram som en liten silo som inte lagras i Datan Warehouse.

## Ansluter [!DNL Google Analytics Warehoused]

>[!INFO]
>
>[!DNL Google Analytics Warehoused] är en `Premium`-integrering. [Kontakta support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) om du vill lägga till den här integreringen i din prenumeration.

1. Gå till sidan `Connections` under **[!UICONTROL Admin** > **Integrations]**.
1. Klicka på **[!UICONTROL Add an Integration]**, som finns till höger.
1. Klicka på ikonen [!DNL Google Analytics Warehoused]. Då öppnas sidan med [!DNL Google Analytics] inloggningsuppgifter.
1. Ange dina [!DNL Google Analytics]-autentiseringsuppgifter. När auktoriseringsprocessen har slutförts omdirigeras du tillbaka till [!DNL Commerce Intelligence].
1. En lista över profil-ID:n visas. Kontrollera de profiler som du vill ansluta till [!DNL Commerce Intelligence]. Om du har flera profiler och behöver hjälp med att identifiera vilka som är vilka, se avsnittet Ansluter flera [!DNL Google Analytics]-profiler nedan.

## Ansluter flera [!DNL Google Analytics]-profiler

Du kan ha flera webbplatser anslutna till ett enda [!DNL Google Analytics]-konto, som identifieras av deras eget profil-ID för [!DNL Google Analytics]. I det här fallet kan du välja att ta med alla dina profil-ID:n i [!DNL Commerce Intelligence]. Kontrollera de profil-ID som du vill inkludera under steget för profilval.

Så här identifierar du en viss webbplats profil-ID [!DNL Google Analytics]:

1. Logga in på [!DNL Google Analytics]
1. Gå till den aktuella webbplatsens [!DNL Google Analytics]-instrumentpanel
1. Titta på URL:en - profil-ID:t motsvarar de åtta siffrorna efter `p` i slutet av raden

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Kopplar från [!DNL Google Analytics Warehoused] från [!DNL Commerce Intelligence] {#disconnect}

1. Gå till sidan med [!DNL Google Analytics] [kontoinställningar](https://myaccount.google.com/intro).
1. Under avsnittet `Security` klickar du på **[!UICONTROL edit]** bredvid `Authorizing` program och webbplatser.
1. Klicka på **[!UICONTROL revoke access]** bredvid [!DNL Commerce Intelligence].

## Relaterad dokumentation

* [Återautentiserar integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Ansluter  [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Analysera webbplatsaktivitet och kundkonverteringsgrader](../../analysis/web-act-cust-conversion.md)
* [Spåra kundvärvningsdata med hjälp av  [!DNL Google Analytics] cookies](../../analysis/google-track-user-acq.md)
