---
title: Connect Mixpanel
description: Lär dig hur du analyserar hur användare navigerar och använder dina webbplatser och appar.
exl-id: e6a9f08f-1063-4d92-93e6-971280239fdb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 0%

---

# Anslut [!DNL Mixpanel]

>[!NOTE]
>
>Kräver [administratörsbehörighet](../../../administrator/user-management/user-management.md).

![](../../../assets/Mixpanel_logo.png)

Med [!DNL Mixpanel] kan du analysera hur användare navigerar och använder dina webbplatser och appar. Om man tittar närmare på användarbeteendedata leder det till smartare design- och utvecklingsbeslut, vilket innebär en bättre produkt totalt sett. Om du ansluter [!DNL Mixpanel] till [!DNL Commerce Intelligence] kan du analysera hur dina användare beter sig och hur det beteendet innebär intäkter.

Ansluta dina [!DNL Mixpanel]-data till [!DNL Commerce Intelligence] i en enkel trestegsprocess:

1. [Öppna sidan för  [!DNL Mixpanel] autentiseringsuppgifter i [!DNL Commerce Intelligence]](#stepone)
1. [Hämta dina  [!DNL Mixpanel] API-autentiseringsuppgifter](#steptwo)
1. [Ange dina [!DNL Mixpanel] API-autentiseringsuppgifter i [!DNL Commerce Intelligence]](#stepthree)

Du måste öppna två webbläsarfönster eller flikar, ett för [!DNL Commerce Intelligence] och ett för ditt [!DNL Mixpanel]-konto, för att kunna slutföra den här processen.

## Öppnar sidan med [!DNL Mixpanel] inloggningsuppgifter {#stepone}

Kom igång:

1. Gå till sidan `Connections` under **[!DNL Manage Data** > **Connections]**.

1. Klicka på **[!UICONTROL Add a New Source]**, som finns till höger på skärmen ovanför tabellen `Data Sources`.

1. Klicka på ikonen [!DNL Mixpanel] så öppnas inloggningssidan.

Lämna den här sidan öppen och växla till webbläsarfönstret med ditt [!DNL Mixpanel]-konto.

## Hämtar dina [!DNL Mixpanel] API-autentiseringsuppgifter {#steptwo}

Om du inte har loggat in på ditt [!DNL Mixpanel]-konto än gör du det och gör sedan följande:

1. Klicka på **[!UICONTROL Account]** i det övre högra hörnet.

1. Klicka på **[!UICONTROL Projects]** i den dialogruta som visas.

1. Din API-inloggningsinformation visas:

![Hämtar API-autentiseringsuppgifter för Mixpanel](../../../assets/Mixpanel_API_creds.png)

Håll den här öppen, du behöver den för att slå ihop det här.

## Ange dina [!DNL Mixpanel] API-autentiseringsuppgifter i [!DNL Commerce Intelligence] {#stepthree}

1. Kopiera `API Key` och `Secret` till inloggningssidan för [!DNL Mixpanel] i [!DNL Commerce Intelligence].
1. Klicka på **[!UICONTROL Connect to Mixpanel]** för att slutföra konfigurationen.

Om anslutningen lyckas, _lyckades!_-meddelandet visas högst upp på sidan.

### Relaterad

* [ [!DNL Mixpanel] data förväntades](../integrations/mixpanel-data.md)
* [Återautentiserar integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
