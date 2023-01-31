---
title: Anslut Google-lösenord
description: Lär dig mäta kampanjens avkastning genom att kombinera era era annonskostnader med kundens livstidsvärde (CLV) för användare som ni köpt från era kampanjer.
exl-id: db99f817-2a2e-4194-9dd2-ec2d6b27a118
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '339'
ht-degree: 0%

---

# Anslut [!DNL Google Adwords]

>[!NOTE]
>
>Kräver [Administratörsbehörigheter](../../../administrator/user-management/user-management.md).

![](../../../assets/Google_Adwords_logo.png)

Ni forskade, skapade era annonser och lanserade era kampanjer. Nu är det dags att analysera era annonsutgiftsdata och se om era pengar används effektivt. Med hjälp av era annonsutgiftsdata kan ni [mäta kampanjens avkastning genom att analysera annonskostnaderna och kundens livstidsvärde (CLV)](../../analysis/roi-ad-camp.md) av de användare ni köpt från era kampanjer.

Låt oss komma igång med våra [!DNL Google Adwords] inloggningsuppgifter till [!DNL MBI]:

1. Gå till sidan Anslutningar under **Hantera data > Integreringar**.
1. Klicka **Lägg till integrering**, som finns längst upp till höger på skärmen.
1. Klicka på **[!DNL Google Adwords]** ikon. Detta öppnar [!DNL Google Adwords] inloggningssida.
1. Ange [!DNL Google Analytics] autentiseringsuppgifter. När auktoriseringsprocessen är slutförd omdirigeras du tillbaka till [!DNL MBI].
1. En lista med profil-ID:n visas. Markera de profiler som du vill ansluta till [!DNL MBI].

   ![](../../../assets/cnnct-profile.png)

1. Ändringarna sparas automatiskt, så klicka **[!UICONTROL Back to Connections]** när du är klar.

Om du har flera profiler och behöver hjälp med att identifiera vilket som är det, se `Connecting Multiple Google Analytics profiles` nedan.

## `Connecting multiple Google Analytics profiles`

Du kan ha flera webbplatser anslutna till en enda [!DNL Google Analytics] konto, som identifieras av deras egna [!DNL Google Analytics] Profil-ID. I det här fallet kan du välja att inkludera alla dina profil-ID:n i [!DNL MBI]. Kontrollera bara de profil-ID som du vill inkludera under steget för val av profil.

**Så här identifierar du en viss webbplats Google Analytics-profil-ID:**

1. Logga in [!DNL Google Analytics]
1. Gå till webbplatsens [!DNL Google Analytics] kontrollpanel
1. Titta på URL:en - profil-ID:t motsvarar de åtta siffrorna efter `p` i slutet av raden:

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**`

## Kopplar från [!DNL Google Adwords]

1. Besök [!DNL Google] [kontoinställningar](https://www.google.com/accounts/) sida.
1. Under `Security` och klicka **[!UICONTROL edit]** nästa `Authorizing` program och webbplatser.
1. Klicka **[!UICONTROL revoke access]** nästa [!DNL MBI].

## Relaterad

* [Återautentisera integreringar](https://support.magento.com/hc/en-us/articles/360016733151)
* [Spåra hänvisningskälla för order via [!DNL Google ECommerce]](../integrations/google-ecommerce.md)
* [Spåra hänvisningskälla för användare i databasen](../../analysis/google-track-user-acq.md)
* [Spåra användarenhets-, webbläsar- och operativsystemsdata i databasen](https://support.magento.com/hc/en-us/articles/360016732911)
* [Upptäck era mest värdefulla förvärvskällor och kanaler](../../analysis/most-value-source-channel.md)
* [Öka avkastningen på era annonskampanjer](../../analysis/roi-ad-camp.md)
* [Hur [!DNL Google Analytics] UTM-attribueringsarbete?](../../analysis/utm-attributes.md)
