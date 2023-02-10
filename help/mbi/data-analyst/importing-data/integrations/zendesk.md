---
title: Connect Zendesk
description: Lär dig hur du konsoliderar din helpdesk-rapportering i [!DNL MBI].
exl-id: 1c7f7c5c-4b1c-4bcf-8f1d-2b4cf9cdb0fb
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 0%

---

# Anslut [!DNL Zendesk]

>[!NOTE]
>
>Kräver [Administratörsbehörigheter](../../../administrator/user-management/user-management.md).

![](../../../assets/Zendesk_logo.png)

Koppla samman [!DNL Zendesk] data gör att du kan konsolidera din helpdesk-rapportering i [!DNL MBI]. På så sätt kan ni optimera kundsupporten och övervaka helpdesk-prestanda tillsammans med era intäkter.

Koppla samman [!DNL Zendesk] data är en enkel trestegsprocess:

1. [Öppna [!DNL Zendesk] inloggningssida i [!DNL MBI]](#stepone)
1. [Hämta din [!DNL Zendesk] API-token](#steptwo)
1. [Ange [!DNL Zendesk] inloggningsinformation och token in [!DNL MBI]](#stepthree)

För att slutföra den här processen måste du öppna två webbläsarfönster eller flikar - ett för [!DNL MBI], den andra för [!DNL Zendesk] konto.

## Öppna [!DNL Zendesk] inloggningssida i [!DNL MBI] {#stepone}

1. Gå till `Integrations` sida under **[!UICONTROL Manage Data** > ** Datakällor **> **Integrationer]**.
1. Klicka **[!UICONTROL Add Integration]**, som finns till höger på skärmen.
1. Klicka på [!DNL Zendesk] ikon. Detta öppnar [!DNL Zendesk] inloggningssida.

## Hämta din [!DNL Zendesk] API-token {#steptwo}

1. I fönstret/fliken där du är inloggad på [!DNL Zendesk] klickar du på inställningsikonen (kugghjulsikonen) längst ned till vänster på skärmen.
1. När `Settings` visas, leta upp `Channels` -avsnitt. Klicka **[!UICONTROL API]** i det här avsnittet.
1. I `Token Access` på den här sidan klickar du i kryssrutan bredvid `Enabled`. En lista över Active API-token visas.
1. Klicka **[!UICONTROL Add New Token]**.
1. Ange en etikett för token när du uppmanas till detta. Vi rekommenderar att du använder `MBI`så att du snabbt vet vilket program som använder token.
1. Klicka **[!UICONTROL Create]**.
1. En API-token skapas. Kopiera denna token; den kommer att användas i nästa steg.

## Retur [!DNL Zendesk] inloggningsinformation och API-token i [!DNL MBI] {#stepthree}

1. Ange [!DNL Zendesk] webbplatsprefix och e-postinloggning i [!DNL Zendesk] inloggningssida i [!DNL MBI].
1. Ange din API-token.
1. Klicka **[!UICONTROL Save & Connect]**. Om anslutningen lyckas kan du *Anslutningen lyckades!* visas högst upp på skärmen.

## Relaterat:

* [Förväntat [!DNL Zendesk] data](../integrations/exp-zendesk-data.md)
* [Återautentisera integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
