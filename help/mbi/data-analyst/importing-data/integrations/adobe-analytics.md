---
title: Connect Adobe Analytics
description: Lär dig att sätta samman hela kundresan med fokus på [!DNL Adobe Analytics] och e-handelns fokus kan du lita på [!DNL Commerce Intelligence].
exl-id: 824e1ee4-6b88-42f7-b265-29330dbc4407
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 0%

---

# Anslut [!DNL Adobe Analytics]

>[!NOTE]
>
>Kräver [Administratörsbehörigheter](../../../administrator/user-management/user-management.md).

![](../../../assets/adobe-analytic-slogo.png)

The [!DNL Adobe Analytics] integration för [!DNL Adobe Commerce Intelligence] gör att ni kan sätta samman hela kundresan med fokus på [!DNL Adobe Analytics] och e-handelns fokus kan du lita på [!DNL Commerce Intelligence]. Detta ger en fullständig bild av butikens totala prestanda.

Mer specifikt finns i [!DNL Adobe Analytics] integration för [!DNL Commerce Intelligence] ger säljarna möjlighet att börja kombinera [!DNL Adobe Commerce] och [!DNL Adobe Analytics] datauppsättningar.

- Skapa en anslutning från din befintliga [!DNL Adobe Analytics] konto till [!DNL Commerce Intelligence].

- Välj upp till 25 mätvärden och dimensioner från en och samma rapportsvit för att återge dem i Data warehouse.

- Använd all standard [!DNL Commerce Intelligence] funktioner för att omvandla, förena och rapportera om replikerade [!DNL Adobe Analytics] data.

## Anslutningskrav

Följande information krävs för att ansluta:

- [!DNL Adobe Analytics] inloggningsuppgifter

- `Name` och/eller `ID` av [!DNL Adobe Analytics] rapportsvit för att replikera data från

- Lista med mätvärden och mått som ska replikeras till [!DNL Commerce Intelligence]

## Ansluta [!DNL Adobe Analytics] Integration för [!DNL Commerce Intelligence]

1. Gå till `Integrations` sida under **[!DNL Manage Data** > **Integrations]**.

1. Klicka **[!UICONTROL Add an Integration]**.

1. Klicka på **[!UICONTROL Adobe Analytics]** -ikonen för att komma åt sidan där du kan godkänna [!DNL Adobe Analytics] kontoanslutning.

1. Klicka **[!UICONTROL Authorize with Adobe Analytics]**.

1. Ange [!DNL Adobe Analytics] autentiseringsuppgifter. När auktoriseringen är klar omdirigeras du tillbaka till [!DNL Commerce Intelligence].

1. En lista över tillgängliga rapportsviter visas. Välj den rapportsvit som du vill importera data från och klicka sedan på **[!UICONTROL Continue]**.

1. Skärmen för att välja mått och mått visas. Välj minst ett mätvärde och minst en dimension, upp till en sammanlagd summa på 25 mätvärden och dimensioner. Sök efter namn eller bläddra för att hitta dina komponenter och klicka sedan på kryssrutorna för att markera dem. Klicka **[!UICONTROL Continue]**.

1. Den valda rapportsviten visas i en tabell. Klicka **[!UICONTROL Save]** för att bekräfta ditt val.

1. Informera [!DNL Commerce Intelligence] [supportteam](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) att integreringen är auktoriserad och de kör den inledande anslutningsprocessen åt dig.

När den inledande anslutningsprocessen har körts är tabellen tillgänglig på Data warehouse-sidan under `All Tables` -fliken. Markera de kolumner som du vill replikera, så visas data efter nästa fullständiga uppdatering.
