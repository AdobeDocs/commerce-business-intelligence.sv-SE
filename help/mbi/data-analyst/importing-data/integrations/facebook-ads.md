---
title: Connect Facebook Ads
description: Lär dig att analysera era annonsutgifter och se om era pengar används effektivt.
exl-id: 219a868b-f17c-4299-9e29-94db9156c9b6
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# Anslut [!DNL Facebook Ads]

>[!NOTE]
>
>Kräver [Administratörsbehörigheter](../../../administrator/user-management/user-management.md).

![](../../../assets/Facebook_Logo.png)

Du gjorde din undersökning, skapade dina annonser, lanserade din kampanj på [!DNL Facebook]. Nu är det dags att analysera era annonsutgiftsdata och se om era pengar används effektivt. Med hjälp av era annonsutgiftsdata kan ni [mäta kampanjens avkastning genom att analysera annonskostnaderna och kundens livstidsvärde (CLV)](../../../data-analyst/analysis/roi-ad-camp.md) av de användare ni köpt från era kampanjer.

Koppla era Facebook-annonser till [!DNL MBI] är en enkel process i tre steg:

1. [Lägg till [!DNL Facebook] som en datakälla i [!DNL MBI]](#stepone)
1. [Tillåt [!DNL MBI] åtkomst till [!DNL Facebook Ads] data](#steptwo)
1. [Välj [!DNL Facebook Ads] Konton för att hämta data](#stepthree)

## Lägg till [!DNL Facebook] som en datakälla i [!DNL MBI] {#stepone}

1. Lägg till [!DNL Facebook] integration till ditt konto, navigera till `Connections` sida under **[!UICONTROL Manage Data** > **Integrations]**.
1. Klicka **[!UICONTROL Add Integration]**, som finns till höger på skärmen ovanför Data `Sources` tabell.
1. Klicka på [!DNL Facebook] ikon. Det här visar [!DNL Facebook] auktoriseringssida.
1. Klicka **[!UICONTROL Authorize]**.

## Tillåt [!DNL MBI] åtkomst till [!DNL Facebook Ads] data {#steptwo}

Efter klickning **[!DNL Facebook Authorize]** visas ett litet popup-fönster:

![](../../../assets/Facebook_Access_Popup.png)

Du följer en serie steg för att tillåta [!DNL MBI] för att få tillgång till data från din offentliga profil, [!DNL Facebook Ads] och tillhörande statistik. Klicka **[!UICONTROL OK]** för att fortsätta.

## Välj [!DNL Facebook Ads] Konton för att hämta data {#stepthree}

1. När autentiseringen är klar uppmanas du att välja [!DNL Facebook Ads] Konton som du vill hämta data från. Markera önskade konton genom att klicka i kryssrutan i dialogrutan `Connect` kolumn.

   ![](../../../assets/Facebook_Ad_Accounts.png)

1. Klicka **[!UICONTROL Save Connections]**.

   Om anslutningen lyckas kan du *Anslutningen lyckades!* visas överst på sidan.

## vad kommer härnäst? {#next}

Se till att du spårar [!DNL Facebook] kampanjer i [!DNL Google Analytics]. Detta säkerställer att `utm\_campaign` fält i [!DNL Google Analytics] är korrekt ifylld för [!DNL Facebook] kampanjer.

## Relaterad

* [Återautentisera integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
* [Koppla samman [!DNL Google Adwords] konto](../integrations/google-ecommerce.md)
* [Spåra hänvisningskälla för order via [!DNL Google eCommerce]](../integrations/google-ecommerce.md)
* [Spåra hänvisningskälla för användare i databasen](../../analysis/google-track-user-acq.md)
* [Spåra användarenhets-, webbläsar- och operativsystemsdata i databasen](../../analysis/track-usr-dev-browser.md)
* [Upptäck era mest värdefulla förvärvskällor och kanaler](../../analysis/most-value-source-channel.md)
* [Öka avkastningen på era annonskampanjer](../../analysis/roi-ad-camp.md)
* [Hur [!DNL Google Analytics] UTM-attribueringsarbete?](../../analysis/utm-attributes.md)
