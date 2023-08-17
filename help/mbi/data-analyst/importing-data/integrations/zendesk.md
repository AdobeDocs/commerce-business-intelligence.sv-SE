---
title: Connect Zendesk
description: Lär dig hur du konsoliderar din helpdesk-rapportering i [!DNL Commerce Intelligence].
exl-id: 1c7f7c5c-4b1c-4bcf-8f1d-2b4cf9cdb0fb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 1%

---

# Anslut [!DNL Zendesk]

>[!NOTE]
>
>Kräver [Administratörsbehörigheter](../../../administrator/user-management/user-management.md).

![](../../../assets/Zendesk_logo.png)

Koppla samman [!DNL Zendesk] data gör att du kan konsolidera din helpdesk-rapportering i [!DNL Commerce Intelligence]. På så sätt kan ni optimera kundsupporten och övervaka helpdesk-prestanda tillsammans med era intäkter.

Koppla samman [!DNL Zendesk] data är en enkel trestegsprocess:

1. [Öppna [!DNL Zendesk] inloggningssida i [!DNL Commerce Intelligence]](#stepone)
1. [Hämta din [!DNL Zendesk] API-token](#steptwo)
1. [Ange [!DNL Zendesk] inloggningsinformation och token in [!DNL Commerce Intelligence]](#stepthree)

För att slutföra den här processen måste du öppna två webbläsarfönster eller -flikar - ett för [!DNL Commerce Intelligence], den andra för [!DNL Zendesk] konto.

## Öppna [!DNL Zendesk] inloggningssida i [!DNL Commerce Intelligence] {#stepone}

1. Gå till `Integrations` sida under **[!UICONTROL Manage Data** > ** Datakällor **> **Integrationer]**.
1. Klicka **[!UICONTROL Add Integration]**, som finns till höger på skärmen.
1. Klicka på [!DNL Zendesk] -ikon. Då öppnas [!DNL Zendesk] inloggningssida.

## Hämta din [!DNL Zendesk] API-token {#steptwo}

1. I fönstret/fliken där du är inloggad på [!DNL Zendesk] klickar du på inställningsikonen (kugghjulsikonen) längst ned till vänster på skärmen.
1. När `Settings` visas, leta upp `Channels` -avsnitt. Klicka **[!UICONTROL API]** i det här avsnittet.
1. I `Token Access` på den här sidan klickar du i kryssrutan intill `Enabled`. En lista över visning av Active API-token.
1. Klicka på **[!UICONTROL Add New Token]**.
1. Ange en etikett för token när du uppmanas till detta. Adobe rekommenderar att du använder `Commerce Intelligence`så att du snabbt vet vilket program som använder token.
1. Klicka på **[!UICONTROL Create]**.
1. En API-token skapas. Kopiera denna token. Den kommer att användas i nästa steg.

## Retur [!DNL Zendesk] inloggningsinformation och API-token i [!DNL Commerce Intelligence] {#stepthree}

1. Ange [!DNL Zendesk] webbplatsprefix och e-postinloggning i [!DNL Zendesk] inloggningssida i [!DNL Commerce Intelligence].
1. Ange din API-token.
1. Klicka på **[!UICONTROL Save & Connect]**. Om anslutningen lyckas kan du *Anslutningen lyckades!* visas högst upp på skärmen.

## Relaterat:

* [Förväntat [!DNL Zendesk] data](../integrations/exp-zendesk-data.md)
* [Återautentisera integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
