---
title: Begränsa åtkomst till mätvärden
description: Lär dig hur du arbetar med tillgång till mätvärden och begränsningar.
exl-id: 88f5ca7a-8073-4968-9685-95f141b2a87f
role: Admin, User
feature: User Management
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 0%

---

# Hantera mätningsanvändare

Förutom att ange behörighetsnivåer för användare kan du även begränsa åtkomsten till mätvärden per användare. Om du t.ex. vill att redovisningsavdelningen ska ha tillgång till intäktsrelaterade mått, men inte användaranhämtningsvärden, kan du begränsa åtkomsten till dessa värden.

I sådana fall rekommenderar Adobe att du anger användarens konto till **[[!UICONTROL Standard]](../../administrator/user-management/user-management.md)**. **[!UICONTROL Standard]**-behörigheter bör ges till användare som inte behöver skapa eller ändra mått, beräknade kolumner, integreringar eller användare, men som behöver åtkomst till data i Data Warehouse. Om du vill begränsa åtkomsten till data fullständigt ska du använda behörigheterna **[!UICONTROL Read Only]** i stället.

När du har angett behörighetsnivån kan du välja de mått som en **[!UICONTROL Standard]**-användare har åtkomst till genom att göra följande:

1. Gå till **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**.
1. Välj önskat användarkonto.
1. Fliken **[!UICONTROL Metrics]** visar en lista med tillgängliga mått. Kontrollera de mätvärden som du vill att användaren ska ha tillgång till och avmarkera dem som användaren inte ska ha tillgång till.
1. [!DNL Adobe Commerce Intelligence] sparar ändringarna automatiskt. Om ändringen lyckas visas [!DNL Commerce Intelligence] högst upp på sidan.**[!UICONTROL Saved!]**

>[!NOTE]
>
>Alla användare med **[!UICONTROL Standard]**-behörighet har åtkomst till alla data i Data Warehouse via dataexport utöver alla mått från [!DNL Google Analytics].

Du kan också begränsa åtkomsten till ett mätresultat genom att redigera mätvärdena och **[!UICONTROL Standard]** välja användare i avsnittet **[[!UICONTROL User Rights]](../../data-user/reports/ess-manage-data-metrics.md)**.

>[!NOTE]
>
>Om du duplicerar ett mätvärde kopierar [!DNL Commerce Intelligence] de användarbehörigheter som angetts i det ursprungliga måttet.
