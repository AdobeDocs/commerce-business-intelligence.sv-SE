---
title: Anslut Google-lösenord
description: Lär dig mäta kampanjens avkastning genom att kombinera era era annonskostnader med kundens livstidsvärde (CLV) för användare som ni köpt från era kampanjer.
exl-id: db99f817-2a2e-4194-9dd2-ec2d6b27a118
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 0%

---

# Anslut [!DNL Google Adwords]

>[!NOTE]
>
>Kräver [Administratörsbehörigheter](../../../administrator/user-management/user-management.md).

![](../../../assets/Google_Adwords_logo.png)

Du gjorde din forskning, du skapade dina annonser, du lanserade dina [!DNL Google] kampanj. Nu är det dags att analysera era annonsutgiftsdata och se om era pengar används effektivt. Med hjälp av era annonsutgiftsdata kan ni [mäta kampanjens avkastning genom att analysera annonskostnaderna och kundens livstidsvärde (CLV)](../../analysis/roi-ad-camp.md) av de användare ni köpt från era kampanjer.

Kom igång genom att ange [!DNL Google Adwords] inloggningsuppgifter till [!DNL Commerce Intelligence].

1. Gå till `Connections` sida under **Hantera data > Integreringar**.
1. Klicka **Lägg till integrering**, som finns längst upp till höger på skärmen.
1. Klicka på **[!DNL Google Adwords]** -ikon. Då öppnas [!DNL Google Adwords] inloggningssida.
1. Ange [!DNL Google Analytics] autentiseringsuppgifter. När auktoriseringsprocessen är slutförd omdirigeras du tillbaka till [!DNL Commerce Intelligence].
1. En lista över profil-ID:n visas. Kontrollera de profiler som du vill ansluta till [!DNL Commerce Intelligence].

   ![](../../../assets/cnnct-profile.png)

1. Ändringarna sparas automatiskt, så klicka **[!UICONTROL Back to Connections]** när du är klar.

Om du har flera profiler och behöver hjälp med att identifiera vilket som är det, se `Connecting Multiple Google Analytics profiles` nedan.

## Ansluta flera [!DNL Google Analytics] profiler

Du kan ha flera webbplatser anslutna till en enda [!DNL Google Analytics] konto, som identifieras av deras egna [!DNL Google Analytics] Profil-ID. I det här fallet kan du välja att ta med alla dina profil-ID:n i [!DNL Commerce Intelligence]. Kontrollera de profil-ID som du vill inkludera under steget för profilval.

**Så här identifierar du en viss webbplats Google Analytics-profil-ID:**

1. Logga in [!DNL Google Analytics]
1. Gå till webbplatsens [!DNL Google Analytics] kontrollpanel
1. Titta på URL:en - profil-ID:t motsvarar de åtta siffror som följer `p` i slutet av raden:

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**`

## Kopplar från [!DNL Google Adwords]

1. Besök [!DNL Google] [kontoinställningar](https://www.google.com/account/about/?hl=en) sida.
1. Under `Security` avsnitt, klicka **[!UICONTROL edit]** nästa `Authorizing` program och webbplatser.
1. Klicka på **[!UICONTROL revoke access]**.

## Relaterad

* [Återautentisera integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Spåra hänvisningskälla för order via [!DNL Google ECommerce]](../integrations/google-ecommerce.md)
* [Spåra hänvisningskälla för användare i databasen](../../analysis/google-track-user-acq.md)
* [Upptäck era mest värdefulla förvärvskällor och kanaler](../../analysis/most-value-source-channel.md)
* [Öka avkastningen på era annonskampanjer](../../analysis/roi-ad-camp.md)
* [Hur [!DNL Google Analytics] UTM-attribueringsarbete?](../../analysis/utm-attributes.md)
