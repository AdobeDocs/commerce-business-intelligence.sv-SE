---
title: Connect Google Analytics
description: Lär dig koppla Google Analytics med [!DNL MBI].
exl-id: 10e813f1-0306-4bdd-8222-e6364ac624de
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 0%

---

# Anslut [!DNL Google Analytics]

>[!NOTE]
>
>Kräver [Administratörsbehörigheter](../../../administrator/user-management/user-management.md).

![](../../../assets/google-analytics-logo.png)

[!DNL Google Analytics] är den vanligaste webbanalystjänsten på Internet. Implementering [!DNL Google Analytics] på er webbplats kan ni spåra hur besökarna använder er webbplats, vilket innehåll som är attraktivt, var besökarna lämnar webbplatsen och mycket annat. Analysera mätvärdena i [!DNL MBI], tillsammans med andra datadelar, förbättrar webbplatsens övergripande hälsa och användbarhet.

Låt oss komma igång med våra [!DNL Google Analytics] inloggningsuppgifter till [!DNL MBI]:

1. Gå till **[!UICONTROL Manage Data** > **Integrations]** sida.
1. Klicka **[!UICONTROL Add Integration]**, som finns till höger på skärmen.
1. Klicka på [!DNL Google Analytics] ikon. Detta öppnar [!DNL Google Analytics] inloggningssida.
1. Ange [!DNL Google Analytics] autentiseringsuppgifter. När auktoriseringsprocessen är slutförd omdirigeras du tillbaka till [!DNL MBI].
1. En lista med profil-ID:n visas. Markera de profiler som du vill ansluta till [!DNL MBI]. Om du har flera profiler och behöver hjälp med att identifiera vilket som är det, se Ansluter flera [!DNL Google Analytics] profilavsnittet nedan.

   ![](../../../assets/list-profile-id.png)<!--{: width="600px"}-->

1. Ändringarna sparas automatiskt, så klicka **Tillbaka till anslutningar** när du är klar.

## Ansluta flera [!DNL Google Analytics] profiler

Du kan ha flera webbplatser anslutna till en enda [!DNL Google Analytics] konto, som identifieras av deras egna [!DNL Google Analytics] profil-ID. I det här fallet kan du välja att ta med alla dina profil-ID:n i [!DNL MBI]. Kontrollera bara de profil-ID som du vill inkludera under steget för profilval.

Identifiera en viss webbplats [!DNL Google Analytics] Profil-ID:

1. Logga in [!DNL Google Analytics]
1. Gå till webbplatsens [!DNL Google Analytics] kontrollpanel
1. Titta på URL:en - profil-ID:t motsvarar de åtta siffrorna efter `p` i slutet av raden:

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Kopplar från [!DNL Google Analytics] från [!DNL MBI] {#disconnect}

1. Besök [!DNL Google Analytics] [kontoinställningar](https://www.google.com/accounts/) sida.
1. Under `Security` och klicka **[!UICONTROL edit]** nästa `Authorizing` program och webbplatser.
1. Klicka **[!UICONTROL revoke access]** nästa [!DNL MBI].

## Relaterat:

* [Återautentisera integreringar](https://support.magento.com/hc/en-us/articles/360016733151)
* [Ansluter [!DNL Google Adwords]](../integrations/google-adwords.md)
* [Analysera webbplatsaktivitet och kundkonverteringsgrader](../../analysis/web-act-cust-conversion.md)
* [Spåra kundvärvningsdata med [!DNL Google Analytics] cookies](../../analysis/google-track-user-acq.md)
* [Spåra användarenhets- och webbläsardata med [!DNL Google Analytics] cookies](https://support.magento.com/hc/en-us/articles/360016732911)
