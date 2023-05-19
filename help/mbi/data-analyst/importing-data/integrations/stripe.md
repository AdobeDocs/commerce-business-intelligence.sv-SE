---
title: Koppla rand
description: Lär dig hur du hanterar och spårar företagets betalningar och fakturadata.
exl-id: c038f2a9-b2bd-4e45-93f9-12d2e5077b31
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 0%

---

# Anslut [!DNL Stripe]

>[!NOTE]
>
>Kräver [Administratörsbehörigheter](../../../administrator/user-management/user-management.md).

![](../../../assets/stripe-logo.png)

[!DNL Stripe] gör att du kan hantera och spåra företagets betalningar och fakturadata. Koppla samman [!DNL Stripe] konto till [!DNL Commerce Intelligence] är en enkel tvåstegsprocess:

1. [Lägg till [!DNL Stripe] som en datakälla i [!DNL Commerce Intelligence]](#stepone)
1. [Tillåt [!DNL Commerce Intelligence] åtkomst till [!DNL Stripe] Data](#steptwo)

## Lägg till [!DNL Stripe] som en datakälla {#stepone}

1. Gå till `Connections` sida under **[!UICONTROL Admin** > **Connections]**.
1. Klicka **[!UICONTROL Add a Data Source]**, som finns till höger på skärmen ovanför `Data Sources` tabell.
1. Klicka på [!DNL Stripe] ikon. Här visas `[!DNL Stripe] authorization` sida.
1. Klicka **[!UICONTROL Connect with Stripe]**.

## Tillåt [!DNL Commerce Intelligence] åtkomst till [!DNL Stripe] data {#steptwo}

Efter klickning **[!UICONTROL Connect with Stripe]** visas en sida för åtkomstbegäran.

1. Klicka **[!UICONTROL Sign in with Stripe to Continue]**.

1. Ange dina uppgifter och klicka på **[!UICONTROL Sign in to your account]**.

1. Dina autentiseringsuppgifter valideras och du omdirigeras tillbaka till [!DNL Commerce Intelligence].

1. Om anslutningen lyckas kan du *Anslutningen lyckades!* visas högst upp på skärmen.

## Relaterat:

The [[!DNL Stripe] API-dokumentation](https://stripe.com/docs/api) kan vara en användbar resurs för att lära dig mer om hur [!DNL Stripe] är integrerat med [!DNL Commerce Intelligence].

* [Förväntat [!DNL Stripe] data](../integrations/stripe-data.md)
* [Återautentisera integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
