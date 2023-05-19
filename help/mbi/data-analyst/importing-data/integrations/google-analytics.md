---
title: Connect Google Analytics
description: Lär dig koppla Google Analytics med [!DNL Commerce Intelligence].
exl-id: 10e813f1-0306-4bdd-8222-e6364ac624de
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# Anslut [!DNL Google Analytics]

>[!NOTE]
>
>Kräver [Administratörsbehörigheter](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] är den vanligaste webbanalystjänsten på Internet. Implementering [!DNL Google Analytics] på er webbplats kan ni spåra hur besökarna använder er webbplats, vilket innehåll som är attraktivt, var besökarna lämnar webbplatsen och mycket annat. Analysera mätvärdena i [!DNL Commerce Intelligence], tillsammans med andra data, förbättrar webbplatsens övergripande hälsa och användbarhet.

Kom igång genom att ange [!DNL Google Analytics] inloggningsuppgifter till [!DNL Commerce Intelligence]:

1. Gå till **[!UICONTROL Manage Data** > **Integrations]**.

1. Klicka **[!UICONTROL Add Integration]**, som finns till höger på skärmen.

1. Klicka på [!DNL Google Analytics] ikon. Då öppnas [!DNL Google Analytics] inloggningssida.

1. Ange [!DNL Google Analytics] autentiseringsuppgifter. När auktoriseringsprocessen är slutförd omdirigeras du tillbaka till [!DNL Commerce Intelligence].

1. En lista över profil-ID:n visas. Kontrollera de profiler som du vill ansluta till [!DNL Commerce Intelligence]. Om du har flera profiler och behöver hjälp med att identifiera vilket som är det, se Ansluter flera [!DNL Google Analytics] profilavsnittet nedan.

   ![](../../../assets/list-profile-id.png)<!--{: width="600px"}-->

1. Ändringarna sparas automatiskt, så klicka **Tillbaka till anslutningar** när du är klar.

## Ansluta flera [!DNL Google Analytics] profiler

Du kan ha flera webbplatser anslutna till en enda [!DNL Google Analytics] konto, som identifieras av deras egna [!DNL Google Analytics] profil-ID. I det här fallet kan du välja att ta med alla dina profil-ID:n i [!DNL Commerce Intelligence]. Kontrollera de profil-ID som du vill inkludera under steget för profilval.

Identifiera en viss webbplats [!DNL Google Analytics] Profil-ID:

1. Logga in [!DNL Google Analytics]
1. Gå till webbplatsens [!DNL Google Analytics] kontrollpanel
1. Titta på URL:en - profil-ID:t motsvarar de åtta siffror som följer `p` i slutet av raden:

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Kopplar från [!DNL Google Analytics] från [!DNL Commerce Intelligence] {#disconnect}

1. Besök [!DNL Google Analytics] [kontoinställningar](https://accounts.google.com/) sida.
1. Under `Security` och klicka **[!UICONTROL edit]** nästa `Authorizing` program och webbplatser.
1. Klicka **[!UICONTROL revoke access]** nästa [!DNL Commerce Intelligence].

## Relaterat:

* [Återautentisera integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Ansluter [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Analysera webbplatsaktivitet och kundkonverteringsgrader](../../analysis/web-act-cust-conversion.md)
* [Spåra kundvärvningsdata med [!DNL Google Analytics] cookies](../../analysis/google-track-user-acq.md)
