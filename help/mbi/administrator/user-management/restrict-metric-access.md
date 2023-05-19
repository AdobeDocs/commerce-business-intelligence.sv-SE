---
title: Begränsa åtkomst till mätvärden
description: Lär dig hur du arbetar med tillgång till mätvärden och begränsningar.
exl-id: 88f5ca7a-8073-4968-9685-95f141b2a87f
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# Hantera mätningsanvändare

Förutom att ange behörighetsnivåer för användare kan du även begränsa åtkomsten till mätvärden per användare. Om du t.ex. vill att redovisningsavdelningen ska ha tillgång till intäktsrelaterade mått, men inte användaranhämtningsvärden, kan du begränsa åtkomsten till dessa värden.

I sådana fall rekommenderar Adobe att du anger att användarens konto ska vara **[[!UICONTROL Standard]](../../administrator/user-management/user-management.md)**. **[!UICONTROL Standard]** behörigheter bör ges till användare som inte behöver skapa eller ändra mått, beräknade kolumner, integreringar eller användare, men som behöver tillgång till data i Data warehouse. Om du vill begränsa åtkomsten till data fullständigt använder du **[!UICONTROL Read Only]** behörigheter i stället.

När du har angett behörighetsnivån kan du välja måtten på **[!UICONTROL Standard]** kan du få åtkomst genom att göra följande:

1. Gå till **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**.
1. Välj önskat användarkonto.
1. The **[!UICONTROL Metrics]** visas en lista med tillgängliga värden. Kontrollera de mätvärden som du vill att användaren ska ha tillgång till och avmarkera dem som användaren inte ska ha tillgång till.
1. [!DNL Adobe Commerce Intelligence] sparar ändringarna automatiskt. Om ändringen lyckas [!DNL Commerce Intelligence] visar **[!UICONTROL Saved!]** överst på sidan.

>[!NOTE]
>
>Alla användare med **[!UICONTROL Standard]** behörigheter kan komma åt alla data i Data warehouse via dataexport utöver alla mått från [!DNL Google Analytics].

Du kan också begränsa åtkomsten till ett mätresultat genom att redigera mätvärdena och **[!UICONTROL Standard]** välja användare i **[[!UICONTROL User Rights]](../../data-user/reports/ess-manage-data-metrics.md)** -avsnitt.

>[!NOTE]
>
>Om du duplicerar ett mätresultat [!DNL Commerce Intelligence] kopierar de användarbehörigheter som angetts i det ursprungliga måttet.
