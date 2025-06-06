---
title: Anslut Google-lösenord
description: Lär dig mäta kampanjens avkastning genom att kombinera era era annonskostnader med kundens livstidsvärde (CLV) för användare som ni köpt från era kampanjer.
exl-id: db99f817-2a2e-4194-9dd2-ec2d6b27a118
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Anslut [!DNL Google Adwords]

>[!NOTE]
>
>Kräver [administratörsbehörighet](../../../administrator/user-management/user-management.md).

![](../../../assets/Google_Adwords_logo.png)

Du har gjort din undersökning, du har skapat dina annonser och du har startat din [!DNL Google]-kampanj. Nu är det dags att analysera era annonsutgiftsdata och se om era pengar används effektivt. Med hjälp av dina annonsutgiftsdata kan du [mäta kampanjens avkastning genom att omvandla annonskostnaden och kundens livstidsvärde (CLV)](../../analysis/roi-ad-camp.md) för användare som ni köpt från era kampanjer.

Kom igång genom att ange dina [!DNL Google Adwords]-autentiseringsuppgifter i [!DNL Commerce Intelligence].

1. Gå till sidan `Connections` under **Hantera data > Integreringar**.
1. Klicka på **Lägg till integrering** som finns i skärmens övre högra hörn.
1. Klicka på ikonen **[!DNL Google Adwords]**. Då öppnas sidan med [!DNL Google Adwords] inloggningsuppgifter.
1. Ange dina [!DNL Google Analytics]-autentiseringsuppgifter. När auktoriseringsprocessen har slutförts omdirigeras du tillbaka till [!DNL Commerce Intelligence].
1. En lista över profil-ID:n visas. Kontrollera de profiler som du vill ansluta till [!DNL Commerce Intelligence].

   ![](../../../assets/cnnct-profile.png)

1. Ändringarna sparas automatiskt, så klicka på **[!UICONTROL Back to Connections]** när du är klar.

Om du har flera profiler och behöver hjälp med att identifiera vilka som är vilka, se avsnittet `Connecting Multiple Google Analytics profiles` nedan.

## Ansluter flera [!DNL Google Analytics]-profiler

Du kan ha flera webbplatser anslutna till ett enda [!DNL Google Analytics]-konto, som identifieras av deras egna [!DNL Google Analytics]-profil-ID. I det här fallet kan du välja att ta med alla dina profil-ID:n i [!DNL Commerce Intelligence]. Kontrollera de profil-ID som du vill inkludera under steget för profilval.

**Så här identifierar du Google Analytics-profil-ID för en viss webbplats:**

1. Logga in på [!DNL Google Analytics]
1. Gå till den aktuella webbplatsens [!DNL Google Analytics]-instrumentpanel
1. Titta på URL:en - profil-ID:t motsvarar de åtta siffrorna efter `p` i slutet av raden:

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**`

## Kopplar från [!DNL Google Adwords]

1. Gå till sidan med [!DNL Google] [kontoinställningar](https://www.google.com/account/about/?hl=en).
1. Klicka på **[!UICONTROL edit]** bredvid `Authorizing` program och webbplatser under avsnittet `Security`.
1. Klicka på **[!UICONTROL revoke access]**.

## Relaterad

* [Återautentiserar integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=sv-SE)
* [Spåra referenskälla för order via  [!DNL Google ECommerce]](../integrations/google-ecommerce.md)
* [Spåra hänvisningskälla för användare i databasen](../../analysis/google-track-user-acq.md)
* [Upptäck era mest värdefulla förvärvskällor och kanaler](../../analysis/most-value-source-channel.md)
* [Öka avkastningen på era annonskampanjer](../../analysis/roi-ad-camp.md)
* [Hur fungerar  [!DNL Google Analytics] UTM-attribuering?](../../analysis/utm-attributes.md)
