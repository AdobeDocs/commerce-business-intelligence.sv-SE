---
title: Connect Mixpanel
description: Lär dig hur du analyserar hur användare navigerar och använder dina webbplatser och appar.
exl-id: e6a9f08f-1063-4d92-93e6-971280239fdb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# Anslut [!DNL Mixpanel]

>[!NOTE]
>
>Kräver [Administratörsbehörigheter](../../../administrator/user-management/user-management.md).

![](../../../assets/Mixpanel_logo.png)

Med [!DNL Mixpanel]kan du analysera hur användare navigerar och använder dina webbplatser och appar. Om man tittar närmare på användarbeteendedata leder det till smartare design- och utvecklingsbeslut, vilket innebär en bättre produkt totalt sett. Ansluter [!DNL Mixpanel] till [!DNL Commerce Intelligence] gör att du kan analysera hur användarna beter sig och hur det beteendet innebär intäkter.

Koppla samman [!DNL Mixpanel] data till [!DNL Commerce Intelligence] en enkel trestegsprocess:

1. [Öppna [!DNL Mixpanel] inloggningssida i [!DNL Commerce Intelligence]](#stepone)
1. [Hämta din [!DNL Mixpanel] API-autentiseringsuppgifter](#steptwo)
1. [Ange [!DNL Mixpanel] API-autentiseringsuppgifter i [!DNL Commerce Intelligence]](#stepthree)

För att slutföra den här processen måste du öppna två webbläsarfönster eller -flikar, ett för [!DNL Commerce Intelligence] och den andra för [!DNL Mixpanel] konto.

## Öppna [!DNL Mixpanel] inloggningssida {#stepone}

Kom igång:

1. Gå till `Connections` sida under **[!DNL Manage Data** > **Connections]**.

1. Klicka **[!UICONTROL Add a New Source]**, som finns till höger på skärmen ovanför `Data Sources` tabell.

1. Klicka på [!DNL Mixpanel] och inloggningssidan öppnas.

Lämna den här sidan öppen och växla till webbläsarfönstret med [!DNL Mixpanel] konto.

## Hämtar [!DNL Mixpanel] API-autentiseringsuppgifter {#steptwo}

Om du inte har loggat in på [!DNL Mixpanel] gör du det och gör sedan följande:

1. Klicka **[!UICONTROL Account]** i det övre högra hörnet.

1. Klicka på **[!UICONTROL Projects]**.

1. Din API-inloggningsinformation visas:

![Hämtar API-autentiseringsuppgifter för Mixpanel](../../../assets/Mixpanel_API_creds.png)

Håll den här öppen, du behöver den för att slå ihop det här.

## Ange [!DNL Mixpanel] API-autentiseringsuppgifter i [!DNL Commerce Intelligence] {#stepthree}

1. Kopiera `API Key` och `Secret` till [!DNL Mixpanel] inloggningssida i [!DNL Commerce Intelligence].
1. Klicka **[!UICONTROL Connect to Mixpanel]** för att slutföra installationen.

Om anslutningen lyckas kan du _Klart!_ visas högst upp på sidan.

### Relaterad

* [Förväntat [!DNL Mixpanel] data](../integrations/mixpanel-data.md)
* [Återautentisera integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
