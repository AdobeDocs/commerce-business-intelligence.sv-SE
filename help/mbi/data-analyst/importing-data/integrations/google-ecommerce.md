---
title: Connect Google ECommerce
description: Läs om era mest värdefulla hänvisningskanaler.
exl-id: c80f52f3-894a-4084-8c0e-aee618ed77f5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Anslut [!DNL Google ECommerce]

>[!NOTE]
>
>Kräver [Administratörsbehörigheter](../../../administrator/user-management/user-management.md).

![](../../../assets/google-ecommerce-logo.png)

Ni har ett stadigt flöde av trafik och beställningar, vilket innebär att ni effektivt når och värvar kunder. Men vilka är era mest värdefulla hänvisningskanaler? Vilket är det genomsnittliga livstidsvärdet för kunder som förvärvats från en källa jämfört med en annan? Genom att ansluta källdata för orderreferenser från [!DNL Google ECommerce] till [!DNL Commerce Intelligence]kan du skapa analyser som hjälper dig att identifiera [mest värdefulla marknadsföringskanaler](../../../data-analyst/analysis/most-value-source-channel.md).

Kom igång genom att ange [!DNL Google ECommerce] inloggningsuppgifter till [!DNL Commerce Intelligence]:

1. Gå till `Connections` sida under **[!UICONTROL Admin** > **Connections]**.

1. Klicka **[!UICONTROL Add a New Source]**, som finns till höger på skärmen ovanför `Data Sources` tabell.

1. Klicka på [!DNL Google ECommerce] ikon. Då öppnas [!DNL Google ECommerce] inloggningssida.

1. Ange [!DNL Google Analytics] autentiseringsuppgifter. När auktoriseringsprocessen är slutförd omdirigeras du tillbaka till [!DNL Commerce Intelligence].

1. En lista över profil-ID:n visas. Kontrollera de profiler som du vill ansluta till [!DNL Commerce Intelligence].

   Om du har flera profiler och behöver hjälp med att identifiera vilket som är vilket, se **Ansluter flera [!DNL Google Analytics] profilavsnittet nedan.

   ![](../../../assets/conn-mult-ga-profiles.png)<!--{: width="500"}-->

1. Ändringarna sparas automatiskt, så klicka **[!UICONTROL Back to Connections]** när du är klar.

## Ansluta flera [!DNL Google Analytics] profiler till [!DNL Commerce Intelligence]

Du kan ha flera webbplatser anslutna till en enda [!DNL Google Analytics] konto, som identifieras av deras egna [!DNL Google Analytics] profil-ID. I det här fallet kan du välja att ta med alla dina profil-ID:n i [!DNL Commerce Intelligence]. Kontrollera de profil-ID som du vill inkludera under steget för profilval.

Identifiera en viss webbplats [!DNL Google Analytics] Profil-ID:

1. Logga in [!DNL Google Analytics].
1. Gå till webbplatsens [!DNL Google Analytics] kontrollpanel.
1. Titta på URL:en - profil-ID:t motsvarar de åtta siffror som följer `p` i slutet av raden.

   `www.google.com/analytics/web/#home/a11345062w43527078p**XXXXXXXX**/`

## Kopplar från [!DNL Google ECommerce] från [!DNL Commerce Intelligence] {#disconnect}

1. Besök [!DNL Google Analytics] [kontoinställningar](https://www.google.com/account/about/?hl=en) sida.
1. Under `Security` avsnitt, klicka **[!UICONTROL edit]** nästa `Authorizing` program och webbplatser.
1. Klicka **[!UICONTROL revoke access]** nästa [!DNL Commerce Intelligence].

## Relaterat:

* [Förväntat [!DNL Google ECommerce] data](../integrations/google-ecommerce-data.md)
* [Återautentisera integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
* [Konfigurera [!DNL Google ECommerce] spårning](https://support.google.com/analytics/answer/1009612?hl=en)
* [Upptäck era mest värdefulla förvärvskällor och kanaler](../../analysis/most-value-source-channel.md)
* [Öka avkastningen på era annonskampanjer](../../analysis/roi-ad-camp.md)
