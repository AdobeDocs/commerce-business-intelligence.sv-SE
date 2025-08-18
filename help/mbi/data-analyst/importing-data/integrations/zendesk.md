---
title: Connect Zendesk
description: Lär dig hur du konsoliderar din helpdesk-rapportering i  [!DNL Commerce Intelligence].
exl-id: 1c7f7c5c-4b1c-4bcf-8f1d-2b4cf9cdb0fb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 1%

---

# Anslut [!DNL Zendesk]

>[!NOTE]
>
>Kräver [administratörsbehörighet](../../../administrator/user-management/user-management.md).

![](../../../assets/Zendesk_logo.png)

Om du ansluter dina [!DNL Zendesk]-data kan du konsolidera din helpdesk-rapportering i [!DNL Commerce Intelligence]. På så sätt kan ni optimera kundsupporten och övervaka helpdesk-prestanda tillsammans med era intäkter.

Att ansluta dina [!DNL Zendesk]-data är en enkel trestegsprocess:

1. [Öppna sidan för  [!DNL Zendesk] autentiseringsuppgifter i [!DNL Commerce Intelligence]](#stepone)
1. [Hämta din  [!DNL Zendesk] API-token](#steptwo)
1. [Ange din  [!DNL Zendesk] inloggningsinformation och token i [!DNL Commerce Intelligence]](#stepthree)

Du måste öppna två webbläsarfönster eller flikar för att kunna slutföra den här processen - ett för [!DNL Commerce Intelligence] och ett för ditt [!DNL Zendesk]-konto.

## Öppna sidan [!DNL Zendesk] med autentiseringsuppgifter i [!DNL Commerce Intelligence] {#stepone}

1. Gå till sidan `Integrations` under **[!UICONTROL Manage Data** > **&#x200B; Datakällor &#x200B;**> **Integrationer]**.
1. Klicka på **[!UICONTROL Add Integration]** till höger på skärmen.
1. Klicka på ikonen [!DNL Zendesk]. Då öppnas sidan med [!DNL Zendesk] inloggningsuppgifter.

## Hämta din [!DNL Zendesk] API-token {#steptwo}

1. Klicka på inställningsikonen (kugghjulsikonen) längst ned till vänster på skärmen i fönstret/fliken där du är inloggad på ditt [!DNL Zendesk]-konto.
1. Leta reda på avsnittet `Settings` när menyn `Channels` visas. Klicka på **[!UICONTROL API]** i det här avsnittet.
1. Klicka i kryssrutan bredvid `Token Access` i avsnittet `Enabled` på den här sidan. En lista över visning av Active API-token.
1. Klicka på **[!UICONTROL Add New Token]**.
1. Ange en etikett för token när du uppmanas till detta. Adobe rekommenderar att du använder `Commerce Intelligence` så att du snabbt vet vilket program som använder token.
1. Klicka på **[!UICONTROL Create]**.
1. En API-token skapas. Kopiera denna token. Den kommer att användas i nästa steg.

## Ange inloggningsinformation för [!DNL Zendesk] och API-token i [!DNL Commerce Intelligence] {#stepthree}

1. Ange ditt [!DNL Zendesk]-webbplatsprefix och e-postadressen för inloggning på sidan [!DNL Zendesk] för inloggningsuppgifter i [!DNL Commerce Intelligence].
1. Ange din API-token.
1. Klicka på **[!UICONTROL Save & Connect]**. Om anslutningen lyckas har en *anslutning lyckades!*-meddelandet visas högst upp på skärmen.

## Relaterat:

* [ [!DNL Zendesk] data förväntades](../integrations/exp-zendesk-data.md)
* [Återautentiserar integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
