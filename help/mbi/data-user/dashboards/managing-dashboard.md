---
title: Hantera instrumentpaneler
description: Lär dig hur du hanterar användarbehörigheter för kontrollpaneler som du äger, tar bort kontrollpaneler som du inte längre behöver och anger en standardkontrollpanel.
exl-id: 32c21093-2a7d-4d8e-afc0-19bd702f9b36
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# Hantera en instrumentpanel

>[!NOTE]
>
>Kräver [administratörsbehörighet](../../administrator/user-management/user-management.md).

I **[!DNL Manage Data** > **Dashboards]** kan du hantera användarbehörigheter för instrumentpaneler som du äger, ta bort instrumentpaneler som du inte längre behöver och ange en standardinstrumentpanel. Det här ämnet handlar om:

1. [Byta namn på instrumentpaneler](#rename)

1. [Hantera behörigheter för kontrollpanelen](#userperm)

1. [Ändra standardinstrumentpanelen](#default)

1. [Ta bort instrumentpaneler](#delete)

## Byta namn på en instrumentpanel {#rename}

Så här byter du namn på en kontrollpanel:

1. Klicka på namnet på kontrollpanelen som du vill ändra.

2. Ange det nya namnet i fältet `Dashboard Name`.

## Hantera användarbehörigheter {#userperm}

Det finns tre åtkomstnivåer i [!DNL Commerce Intelligence] för instrumentpaneler - `View`, `Edit` och `None`.

* `View` tillåter valda användare att visa instrumentpanelen men inte redigera den. Användarna kan också ändra storlek på diagram, exportera data och kopiera diagram till sina egna kontrollpaneler med funktionen Spara som om de har behörighet som Standard eller Admin.

* `Edit` tillåter att valda användare kan redigera och spara diagram på den här instrumentpanelen om de har standard- eller administratörsbehörighet. Dessutom kan användare med redigeringsbehörighet även dela kontrollpaneler med andra användare.

* `None` betyder att de valda användarna inte kan visa eller redigera den här instrumentpanelen.

Användarbehörigheter kan ändras på ett av två sätt - för alla användare eller för en enskild användare.

1. *Om du vill ändra alla användares behörigheter* använder du listrutan bredvid etiketten `Set all users' permissions to…`.

1. *Om du vill ändra en enskild användares behörigheter* använder du listrutan bredvid användarens namn för att ange önskad åtkomstnivå.

## Ändra standardinstrumentpanelen {#default}

Så här ändrar du standardinstrumentpanelen för kontot:

1. Klicka på namnet på den kontrollpanel som du vill använda som standard.

1. Klicka på **[!UICONTROL Make Default]**.

## Ta bort instrumentpaneler {#delete}

Så här tar du bort en kontrollpanel:

1. Klicka på namnet på den kontrollpanel som du vill ta bort.

1. Klicka på **[!UICONTROL Delete Dashboard]**.
