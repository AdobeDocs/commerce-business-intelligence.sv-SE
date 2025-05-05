---
title: Connect Stripe
description: Lär dig hur du hanterar och spårar företagets betalningar och fakturadata.
exl-id: c038f2a9-b2bd-4e45-93f9-12d2e5077b31
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 1%

---

# Anslut [!DNL Stripe]

>[!NOTE]
>
>Kräver [administratörsbehörighet](../../../administrator/user-management/user-management.md).

![](../../../assets/stripe-logo.png)

Med [!DNL Stripe] kan du hantera och spåra ditt företags betalningar och fakturadata. Att ansluta ditt [!DNL Stripe]-konto till [!DNL Commerce Intelligence] är en enkel tvåstegsprocess:

1. [Lägg till [!DNL Stripe] som en datakälla i [!DNL Commerce Intelligence]](#stepone)
1. [Tillåt [!DNL Commerce Intelligence] åtkomst till dina [!DNL Stripe] data](#steptwo)

## Lägg till [!DNL Stripe] som datakälla {#stepone}

1. Gå till sidan `Connections` under **[!UICONTROL Admin** > **Connections]**.
1. Klicka på **[!UICONTROL Add a Data Source]**, som finns till höger på skärmen ovanför tabellen `Data Sources`.
1. Klicka på ikonen [!DNL Stripe]. Sidan `[!DNL Stripe] authorization` visas.
1. Klicka på **[!UICONTROL Connect with Stripe]**.

## Ge [!DNL Commerce Intelligence] åtkomst till dina [!DNL Stripe]-data {#steptwo}

När du har klickat på **[!UICONTROL Connect with Stripe]** visas en sida för åtkomstbegäran.

1. Klicka på **[!UICONTROL Sign in with Stripe to Continue]**.

1. Ange dina autentiseringsuppgifter och klicka på **[!UICONTROL Sign in to your account]**.

1. Dina autentiseringsuppgifter valideras och du dirigeras tillbaka till [!DNL Commerce Intelligence].

1. Om anslutningen lyckas har en *anslutning lyckades!*-meddelandet visas högst upp på skärmen.

## Relaterat:

[[!DNL Stripe] API-dokumentationen ](https://stripe.com/docs/api) kan vara användbar när du vill veta mer om hur [!DNL Stripe] integreras med [!DNL Commerce Intelligence].

* [ [!DNL Stripe] data förväntades](../integrations/stripe-data.md)
* [Återautentiserar integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=sv-SE)
