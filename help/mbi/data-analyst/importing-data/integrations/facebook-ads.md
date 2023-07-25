---
title: Connect Facebook Ads
description: Lär dig hur ni analyserar era annonsutgiftsdata och ser om era pengar används effektivt.
exl-id: 219a868b-f17c-4299-9e29-94db9156c9b6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '304'
ht-degree: 0%

---

# Anslut [!DNL Facebook Ads]

>[!NOTE]
>
>Kräver [Administratörsbehörigheter](../../../administrator/user-management/user-management.md).

![](../../../assets/facebook-ads-logo.png)

Du gjorde din undersökning, skapade dina annonser, lanserade din kampanj på [!DNL Facebook]. Nu är det dags att analysera era annonsutgiftsdata och se om era pengar används effektivt. Med hjälp av era annonsutgiftsdata kan ni [mäta kampanjens avkastning genom att analysera annonskostnaderna och kundens livstidsvärde (CLV)](../../../data-analyst/analysis/roi-ad-camp.md) av de användare ni köpt från era kampanjer.

Koppla samman [!DNL Facebook Ad] data till [!DNL Commerce Intelligence] är en enkel process i tre steg:

1. [Lägg till [!DNL Facebook] som en datakälla i [!DNL Commerce Intelligence]](#stepone)
1. [Tillåt [!DNL Commerce Intelligence] åtkomst till [!DNL Facebook Ads] data](#steptwo)
1. [Välj [!DNL Facebook Ads] Konton för att hämta data](#stepthree)

## Lägg till [!DNL Facebook] som en datakälla i [!DNL Commerce Intelligence] {#stepone}

1. Lägg till [!DNL Facebook] integrering med [!DNL Commerce Intelligence]konto, navigera till `Connections` sida under **[!UICONTROL Manage Data** > **Integrations]**.
1. Klicka **[!UICONTROL Add Integration]**, till höger.
1. Klicka på [!DNL Facebook] ikon. Här visas [!DNL Facebook] auktoriseringssida.
1. Klicka **[!UICONTROL Authorize]**.

## Tillåt [!DNL Commerce Intelligence] åtkomst till [!DNL Facebook Ads] data {#steptwo}

Efter klickning **[!DNL Facebook Authorize]** visas ett litet popup-fönster:

![](../../../assets/Facebook_Access_Popup.png)

Följ en serie steg för att tillåta [!DNL Commerce Intelligence] för att få tillgång till data från din offentliga profil, [!DNL Facebook Ads] och relaterade statistik. Klicka **[!UICONTROL OK]** för att fortsätta.

## Välj [!DNL Facebook Ads] Konton för att hämta data {#stepthree}

1. När autentiseringen är klar uppmanas du att välja [!DNL Facebook Ads] Konton som du vill hämta data från. Markera önskade konton genom att klicka i kryssrutan i dialogrutan `Connect` kolumn.

   ![](../../../assets/Facebook_Ad_Accounts.png)

1. Klicka **[!UICONTROL Save Connections]**.

   Om anslutningen lyckas kan du *Anslutningen lyckades!* visas högst upp på sidan.

## Vad kommer härnäst? {#next}

Se till att du spårar [!DNL Facebook] kampanjer i [!DNL Google Analytics]. Detta säkerställer att `utm\_campaign` fält i [!DNL Google Analytics] är korrekt ifylld för [!DNL Facebook] kampanjer.

## Relaterad

* [Återautentisera integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Koppla samman [!DNL Google Adwords] konto](../integrations/google-ecommerce.md)
* [Spåra hänvisningskälla för order via [!DNL Google eCommerce]](../integrations/google-ecommerce.md)
* [Spåra hänvisningskälla för användare i databasen](../../analysis/google-track-user-acq.md)
* [Spåra användarenhetsdata, webbläsardata och operativsystemsdata i databasen](../../analysis/track-usr-dev-browser.md)
* [Upptäck era mest värdefulla förvärvskällor och kanaler](../../analysis/most-value-source-channel.md)
* [Öka avkastningen på era annonskampanjer](../../analysis/roi-ad-camp.md)
* [Hur [!DNL Google Analytics] UTM-attribueringsarbete?](../../analysis/utm-attributes.md)
