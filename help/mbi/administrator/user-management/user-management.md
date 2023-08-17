---
title: Hantera Adobe Commerce-användare och behörigheter
description: Lär dig hur du hanterar dina Commerce Intelligence-användare.
exl-id: 2a5eeabb-3c13-4ca1-b845-ed255b389c9f
role: Admin, User
feature: User Management
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# Hantera användarbehörigheter

[!DNL Adobe Commerce Intelligence] ska vara en enda källa till sanning i hela organisationen. Varje användare har en egen uppsättning kontrollpaneler som de kan [dela med andra användare](../../data-user/dashboards/share-dashboard-with-users.md).

## Behörighetsnivåer

I [!DNL Commerce Intelligence], finns det tre allmänna behörighetsnivåer som gäller för användare, som väljs när ett konto skapas:

* `Admin`
* `Standard`
* `Read-Only`

Dessa behörigheter gör att användare kan utföra vissa åtgärder eller komma åt specifika delar av [!DNL Commerce Intelligence]. Här följer en tabell över vad varje behörighetsnivå kan göra i [!DNL Commerce Intelligence]:

|   | `Admin` | `Standard` | `Read Only` |
| -----|-----|-----|----|
| **Skapa/hantera användare** | ✔ |   |   |
| **Skapa e-postsammanfattningar** | ✔ | ✔ |   |
| **Skapa/redigera/dela kontrollpaneler** | ✔ | ✔ |   |
| **Visa instrumentpaneler** | ✔ | ✔ | ✔ |
| **Skapa/redigera/ta bort visuella rapporter** | ✔ | ✔* |   |
| **Skapa/redigera/ta bort SQL-rapporter** | ✔ |  |   |
| **Klonpaneler** | ✔ |   |   |
| **Lägg till/hantera integreringar** | ✔ |   |   |
| **Öppna Data Warehouse Manager** | ✔ |   |   |
| **Synkronisera/avsynkronisera tabeller och kolumner** | ✔ |   |   |
| **Skapa/redigera mätvärden** | ✔ |   |   |
| **Skapa/redigera filteruppsättningar** | ✔ |   |   |
| **Skapa/redigera beräknade kolumner** | ✔ |   |   |
| **Skapa en lista med beroende rapporter** | ✔ |   |   |
| **Översikt över Access System** | ✔ |   |   |
| **Åtkomstinställningar för tidszon** | ✔ |   |   |
| **Åtkomstfakturering** | ✔ | ✔** |   |
| **Kontakta supporten** | ✔ | ✔ | ✔ |

{style="table-layout:auto"}

>[!NOTE]
>
>_Du kan begränsa **[!UICONTROL Standard]**användarens [tillgång till specifika mätvärden](../../administrator/user-management/restrict-metric-access.md)._
>
>**[!UICONTROL Standard] _-användare har åtkomst till Fakturering med en extra behörighetsinställning._
>
>**[!UICONTROL Read-Only]** kan bara _visa_ instrumentpaneler som har delats med dem; de kan inte skapa eller redigera någonting i [!DNL Commerce Intelligence]och de kan inte heller söka efter och lägga till nya instrumentpaneler på sitt konto. Adobe rekommenderar att du delar en specifik uppsättning kontrollpaneler med **[!UICONTROL Read-Only]** användare som du eller någon annan medlem i ditt team underhåller. Klona inte en uppsättning instrumentpaneler åt dem.

## Ytterligare behörigheter: Fakturering och teknik {#billingtech}

Förutom de allmänna behörighetsnivåerna finns det två andra användarbeteckningar - `Billing` och `Technical`. Dessa beteckningar bör användas tillsammans med de allmänna behörighetsnivåerna.

### Fakturering

`Billing` användare har tillgång till faktureringssidan och kan ändra betalningsinformation. Adobe kan också kontakta dem för faktureringsfrågor.

`Admin` användare har åtkomst till `Billing` som standard, men `Standard` kan även få åtkomst om de har `Billing` markerad kryssruta på sin profil.

![fakturering](../../assets/billing.png)<!--{: width="550" height="363"}-->

### Teknisk

`Technical` -användare har inte någon behörighet som är specifik för dem - den här inställningen markerar bara en teknisk kontakt inom organisationen. Adobe kan kontakta dessa användare för tekniska frågor.

`Admin` användare kan lägga till nya användare i sina konton genom att klicka på **[!UICONTROL Account Settings]** > **[!UICONTROL Create Users]** och följer anvisningarna. När användaren har skapats i [!DNL Commerce Intelligence], får den person du bjuder in e-postinstruktioner om hur du slutför kontokonfigurationsprocessen.

När som helst, `Admins` kan visa alla användare på deras konto genom att klicka på **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**. På den här sidan visas användarens behörigheter och vilka mått och instrumentpaneler som användaren kan komma åt.
