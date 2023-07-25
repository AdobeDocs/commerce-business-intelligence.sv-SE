---
title: Dela instrumentpaneler med andra användare
description: Lär dig hur du delar kontrollpaneler med andra användare.
exl-id: 6279b049-d1b2-4d40-b30b-ee8772e990f4
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 0%

---

# Dela instrumentpaneler med andra användare

Att dela instrumentpaneler är ett bra sätt att se till att teamet är med och uppmuntra till samarbete. Genom att skapa och dela en central kontrollpanel kan du ge teamet den information de behöver samtidigt som ni behåller kontrollen. [[!DNL Adobe] rekommenderas](../../best-practices/share-dashboard-best-practice.md){: target=&quot;_blank&quot;} som du beviljar `Edit` behörighet till ett fåtal för att minimera oavsiktliga ändringar.

>[!NOTE]
>
>Om instrumentpanelen som du delar innehåller rapporter som skapats med mått som en viss användare inte har tillgång till, visas ett `Error Loading Data` meddelande. Om du vill att data ska visas för den specifika användaren, [admin-användare](../../administrator/user-management/user-management.md) måste ge tillgång till alla mätvärden som används i dessa rapporter.

## Dela en kontrollpanel

1. Klicka **[!UICONTROL Share Dashboard]** längst upp på skärmen.

   En lista över alla användare i din [!DNL Commerce Intelligence] kontot visas.

1. Om du vill välja en användare att dela kontrollpanelen med markerar du kryssrutan till vänster om namnet.

   Om du vill markera/avmarkera alla användare klickar du på **[!UICONTROL Select]** och markera `Everyone` eller `None`, respektive.

1. Behörigheter kan anges per användare eller en kombination.

   *Ange individuella behörigheter*, klicka **[!UICONTROL None]** till höger om användarens namn. I den här listrutan väljer du vilken typ av behörigheter användaren ska ha.

   *Så här anger du behörigheter vid masser*, klicka **[!UICONTROL Set Permissions]**. I den här listrutan väljer du vilken typ av behörigheter de markerade användarna ska ha.

   >[!NOTE]
   >
   >Du kan också använda den här funktionen för att uppdatera tidigare angivna behörigheter. Om du till exempel inte längre vill dela instrumentpanelen med någon anger du deras behörigheter till `None`.

1. Om du vill dela kontrollpanelen klickar du på **[!UICONTROL Save Changes]**. De valda användarna får ett e-postmeddelande med en inbjudan om att visa kontrollpanelen.

Exempel:

![kontrollpanel för resurs](../../assets/Share_Dashboards.gif)
