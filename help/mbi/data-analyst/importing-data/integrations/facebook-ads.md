---
title: Anslut Facebook-annonser
description: Lär dig hur ni analyserar era annonsutgiftsdata och ser om era pengar används effektivt.
exl-id: 219a868b-f17c-4299-9e29-94db9156c9b6
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# Anslut [!DNL Facebook Ads]

>[!NOTE]
>
>Kräver [administratörsbehörighet](../../../administrator/user-management/user-management.md).

![Facebook Ads-logotyp](../../../assets/facebook-ads-logo.png)

Du gjorde din undersökning, du skapade dina annonser, du lanserade din kampanj [!DNL Facebook]. Nu är det dags att analysera era annonsutgiftsdata och se om era pengar används effektivt. Med hjälp av dina annonsutgiftsdata kan du [mäta kampanjens avkastning genom att omvandla annonskostnaden och kundens livstidsvärde (CLV)](../../../data-analyst/analysis/roi-ad-camp.md) för användare som ni köpt från era kampanjer.

Att ansluta dina [!DNL Facebook Ad]-data till [!DNL Commerce Intelligence] är en enkel process i tre steg:

1. [Lägg till [!DNL Facebook] som en datakälla i [!DNL Commerce Intelligence]](#stepone)
1. [Tillåt [!DNL Commerce Intelligence] åtkomst till dina [!DNL Facebook Ads] data](#steptwo)
1. [Välj [!DNL Facebook Ads] Konton för att hämta data](#stepthree)

## Lägg till [!DNL Facebook] som en datakälla i [!DNL Commerce Intelligence] {#stepone}

1. Om du vill lägga till integreringen [!DNL Facebook] i ditt [!DNL Commerce Intelligence]konto går du till sidan `Connections` under **[!UICONTROL Manage Data** > **Integrations]**.
1. Klicka på **[!UICONTROL Add Integration]** till höger.
1. Klicka på ikonen [!DNL Facebook]. Detta visar auktoriseringssidan för [!DNL Facebook].
1. Klicka på **[!UICONTROL Authorize]**.

## Ge [!DNL Commerce Intelligence] åtkomst till dina [!DNL Facebook Ads]-data {#steptwo}

När du har klickat på **[!DNL Facebook Authorize]** visas ett litet popup-fönster:

![Dialogrutan för behörighet till Facebook för Commerce Intelligence](../../../assets/Facebook_Access_Popup.png)

Du följer en serie steg för att tillåta [!DNL Commerce Intelligence] att få åtkomst till data från din offentliga profil, [!DNL Facebook Ads] och relaterad statistik. Klicka på **[!UICONTROL OK]** på de här stegen för att fortsätta.

## Välj [!DNL Facebook Ads] konton för att dra in data {#stepthree}

1. När autentiseringen är klar uppmanas du att välja de [!DNL Facebook Ads]-konton som du vill hämta data från. Markera önskade konton genom att klicka i kryssrutan i kolumnen `Connect`.

   ![Gränssnitt för val av Facebook-annonskonton](../../../assets/Facebook_Ad_Accounts.png)

1. Klicka på **[!UICONTROL Save Connections]**.

   Om anslutningen lyckas har en *anslutning lyckades!*-meddelandet visas högst upp på sidan.

## Vad kommer härnäst? {#next}

Kontrollera att du spårar [!DNL Facebook] kampanjer i [!DNL Google Analytics]. Detta garanterar att fältet `utm\_campaign` i [!DNL Google Analytics] fylls i korrekt för dina [!DNL Facebook]-kampanjer.

## Relaterad

* [Återautentiserar integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Anslut ditt [!DNL Google Adwords] konto](../integrations/google-ecommerce.md)
* [Spåra referenskälla för order via  [!DNL Google eCommerce]](../integrations/google-ecommerce.md)
* [Spåra hänvisningskälla för användare i databasen](../../analysis/google-track-user-acq.md)
* [Spåra användarenhetsdata, webbläsardata och operativsystemsdata i databasen](../../analysis/track-usr-dev-browser.md)
* [Upptäck era mest värdefulla förvärvskällor och kanaler](../../analysis/most-value-source-channel.md)
* [Öka avkastningen på era annonskampanjer](../../analysis/roi-ad-camp.md)
* [Hur fungerar  [!DNL Google Analytics] UTM-attribuering?](../../analysis/utm-attributes.md)
