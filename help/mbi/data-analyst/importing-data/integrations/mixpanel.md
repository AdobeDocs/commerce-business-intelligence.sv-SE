---
title: Connect Mixpanel
description: Lär dig hur du analyserar hur användare navigerar och använder dina webbplatser och appar.
exl-id: e6a9f08f-1063-4d92-93e6-971280239fdb
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 0%

---

# Anslut [!DNL Mixpanel]

>[!NOTE]
>
>Kräver [Administratörsbehörigheter](../../../administrator/user-management/user-management.md).

![](../../../assets/Mixpanel_logo.png)

Med [!DNL Mixpanel]kan du analysera hur användare navigerar och använder dina webbplatser och appar. Om man tittar närmare på användarbeteendedata leder det till smartare design- och utvecklingsbeslut, vilket innebär en bättre produkt totalt sett. Ansluter [!DNL Mixpanel] till [!DNL MBI] gör att du kan analysera hur användarna beter sig och hur det beteendet innebär intäkter.

Koppla samman [!DNL Mixpanel] data till [!DNL MBI] en enkel trestegsprocess:

1. [Öppna [!DNL Mixpanel] inloggningssida i [!DNL MBI]](#stepone)
1. [Hämta din [!DNL Mixpanel] API-autentiseringsuppgifter](#steptwo)
1. [Ange [!DNL Mixpanel] API-autentiseringsuppgifter i MBI](#stepthree)

För att slutföra den här processen måste du öppna två webbläsarfönster eller flikar - ett för [!DNL MBI], den andra för [!DNL Mixpanel] konto.

## Öppna [!DNL Mixpanel] inloggningssida {#stepone}

Låt oss komma igång:

1. Gå till `Connections` sida under **[!DNL Manage Data** > **Connections]**.
1. Klicka **[!UICONTROL Add a New Source]**, som finns till höger på skärmen ovanför `Data Sources` tabell.
1. Klicka på [!DNL Mixpanel] och inloggningssidan öppnas.

Lämna den här sidan öppen och växla till webbläsarfönstret med [!DNL Mixpanel] konto.

## Hämtar [!DNL Mixpanel] API-autentiseringsuppgifter {#steptwo}

Om du inte har loggat in på [!DNL Mixpanel] gör du det och gör sedan följande:

1. Klicka **[!UICONTROL Account]** i det övre högra hörnet.
1. Klicka på **[!UICONTROL Projects]**.
1. API-autentiseringsuppgifterna visas:

![Hämtar API-autentiseringsuppgifter för Mixpanel](../../../assets/Mixpanel_API_creds.png)

Håll det här öppet - vi behöver det för att slå ihop det här.

## Ange [!DNL Mixpanel] API-autentiseringsuppgifter i [!DNL MBI] {#stepthree}

1. Kopiera `API Key` och `Secret` till [!DNL Mixpanel] inloggningssida i [!DNL MBI].
1. Klicka **[!UICONTROL Connect to Mixpanel]** för att slutföra installationen.

Så ja! Om anslutningen lyckas kan du _Klart!_ visas överst på sidan.

### Relaterad

* [Förväntat [!DNL Mixpanel] data](../integrations/mixpanel-data.md)
* [Återautentisera integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
