---
title: Connect Google Analytics
description: Lär dig ansluta Google Analytics med  [!DNL Commerce Intelligence].
exl-id: 10e813f1-0306-4bdd-8222-e6364ac624de
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 0%

---

# Anslut [!DNL Google Analytics]

>[!NOTE]
>
>Kräver [administratörsbehörighet](../../../administrator/user-management/user-management.md).

![Google Analytics-logotyp](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] är den mest använda webbanalystjänsten på Internet. Genom att implementera [!DNL Google Analytics] på din webbplats kan du spåra hur besökarna använder din webbplats, vilket innehåll som är attraktivt, var besökarna lämnar webbplatsen och mycket annat. Om du analyserar dessa mått i [!DNL Commerce Intelligence], tillsammans med andra datadelar, förbättras webbplatsens övergripande hälsa och användbarhet.

Kom igång genom att ange dina [!DNL Google Analytics]-autentiseringsuppgifter i [!DNL Commerce Intelligence]:

1. Gå till **[!UICONTROL Manage Data** > **Integrations]**.

1. Klicka på **[!UICONTROL Add Integration]** till höger på skärmen.

1. Klicka på ikonen [!DNL Google Analytics]. Då öppnas sidan med [!DNL Google Analytics] inloggningsuppgifter.

1. Ange dina [!DNL Google Analytics]-autentiseringsuppgifter. När auktoriseringsprocessen har slutförts omdirigeras du tillbaka till [!DNL Commerce Intelligence].

1. En lista över profil-ID:n visas. Kontrollera de profiler som du vill ansluta till [!DNL Commerce Intelligence]. Om du har flera profiler och behöver hjälp med att identifiera vilka som är vilka, se avsnittet Ansluter flera [!DNL Google Analytics]-profiler nedan.

   ![Google Analytics Admin-sida med profil-ID i URL](../../../assets/list-profile-id.png)<!--{: width="600px"}-->

1. Ändringarna sparas automatiskt, så klicka på **Tillbaka till anslutningar** när du är klar.

## Ansluter flera [!DNL Google Analytics]-profiler

Du kan ha flera webbplatser anslutna till ett enda [!DNL Google Analytics]-konto, som identifieras av deras eget profil-ID för [!DNL Google Analytics]. I det här fallet kan du välja att ta med alla dina profil-ID:n i [!DNL Commerce Intelligence]. Kontrollera de profil-ID som du vill inkludera under steget för profilval.

Så här identifierar du en viss webbplats profil-ID [!DNL Google Analytics]:

1. Logga in på [!DNL Google Analytics]
1. Gå till den aktuella webbplatsens [!DNL Google Analytics]-instrumentpanel
1. Titta på URL:en - profil-ID:t motsvarar de åtta siffrorna efter `p` i slutet av raden:

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Kopplar från [!DNL Google Analytics] från [!DNL Commerce Intelligence] {#disconnect}

1. Gå till sidan med [!DNL Google Analytics] [kontoinställningar](https://accounts.google.com/).
1. Under avsnittet `Security` klickar du på **[!UICONTROL edit]** bredvid `Authorizing` program och webbplatser.
1. Klicka på **[!UICONTROL revoke access]** bredvid [!DNL Commerce Intelligence].

## Relaterat:

* [Återautentiserar integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=sv-SE)
* [Ansluter  [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Analysera webbplatsaktivitet och kundkonverteringsgrader](../../analysis/web-act-cust-conversion.md)
* [Spåra kundvärvningsdata med hjälp av  [!DNL Google Analytics] cookies](../../analysis/google-track-user-acq.md)
