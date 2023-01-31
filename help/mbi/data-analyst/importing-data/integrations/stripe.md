---
title: Koppla rand
description: Lär dig hur du hanterar och håller reda på företagets betalningar och fakturadata.
exl-id: c038f2a9-b2bd-4e45-93f9-12d2e5077b31
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---

# Koppla rand

>[!NOTE]
>
>Kräver [Administratörsbehörigheter](../../../administrator/user-management/user-management.md).

![](../../../assets/stripe-logo.png)

[!DNL Stripe] gör att du kan hantera och hålla reda på företagets betalningar och fakturadata. Koppla samman [!DNL Stripe] konto till [!DNL MBI] är en enkel tvåstegsprocess:

1. [Lägg till [!DNL Stripe] som en datakälla i [!DNL MBI]](#stepone)
1. [Tillåt [!DNL MBI] åtkomst till [!DNL Stripe] Data](#steptwo)

## Lägg till [!DNL Stripe] som en datakälla {#stepone}

1. Gå till `Connections` sida under **[!UICONTROL Admin** > **Connections]**.
1. Klicka **[!UICONTROL Add a Data Source]**, som finns till höger på skärmen ovanför `Data Sources` tabell.
1. Klicka på [!DNL Stripe] ikon. Det här visar `[!DNL Stripe] authorization` sida.
1. Klicka **[!UICONTROL Connect with Stripe]**.

## Tillåt [!DNL MBI] åtkomst till [!DNL Stripe] data {#steptwo}

Efter klickning **[!UICONTROL Connect with Stripe]** visas en sida för åtkomstbegäran.

1. Klicka **[!UICONTROL Sign in with Stripe to Continue]**.

1. Ange dina uppgifter och klicka på **[!UICONTROL Sign in to your account]**.

1. När du har klickat valideras dina inloggningsuppgifter och du omdirigeras tillbaka till [!DNL MBI].

1. Om anslutningen lyckas kan du *Anslutningen lyckades!* visas högst upp på skärmen.

## Relaterat:

Om du är lite mer teknikkunnig, [[!DNL Stripe] API-dokumentation](https://stripe.com/docs/api) kan vara en användbar resurs för att lära dig mer om hur [!DNL Stripe] är integrerat med [!DNL MBI].

* [Förväntat [!DNL Stripe] data](../integrations/stripe-data.md)
* [Återautentisera integreringar](https://support.magento.com/hc/en-us/articles/360016733151)
