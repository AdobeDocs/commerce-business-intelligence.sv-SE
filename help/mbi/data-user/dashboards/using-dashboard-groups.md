---
title: Använd instrumentpanelsgrupper
description: Lär dig hur du kan ordna kontrollpaneler bättre.
exl-id: e48b7345-62d0-4898-997e-3c3c02040ad3
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# Använda panelgrupper

Instrumentpanelsgrupper ger bättre ordning på kontrollpanelerna. Det vanligaste användningsområdet är att gruppera liknande kontrollpaneler under samma&quot;grupp&quot;. Till exempel kan alla kontrollpaneler som är relaterade till marknadsföring grupperas under en kontrollpanelsgrupp&quot;Marknadsföring&quot;.

I listrutan för val av kontrollpanel visas kontrollpanelsgrupper i alfabetisk ordning med alla kontrollpaneler under Ingen grupp senast. Kontrollpaneler under samma grupp visas tillsammans och i alfabetisk ordning inom varje grupp.

## Gruppdelning på instrumentpanel

Instrumentpanelsgrupper kan inte delas direkt mellan användare. När en kontrollpanel delas med användare skapas den instrumentpanelsgrupp som den är underställd automatiskt för de användarna om den inte finns. Om instrumentpanelsgruppen finns läggs instrumentpanelen till i listan.

När en kontrollpanels grupp ändras av dess ägare återspeglas ändringen automatiskt för alla användare som kontrollpanelen har delats med. Användare kan inte ändra kontrollpanelsgruppen för kontrollpaneler som de inte äger.

## Skapa panelgrupper

Kontrollpanelsgrupper kan skapas på ett av två sätt:

1. När du skapar en kontrollpanel:

   ![skapa instrumentpanelsgrupp](../../assets/create-dashboard-groups-new-dashboard.png)

1. När du ändrar gruppen för en befintlig instrumentpanel från sidan `Manage Data > Dashboards`:

   1. Klicka på den kontrollpanel som du vill skapa gruppen för.

   1. Under `Dashboard Group (optional)` visas den aktuella instrumentpanelsgruppen.

   1. Om du vill skapa en grupp skriver du namnet på den nya gruppen och klickar sedan utanför rutan.

      ![skapa instrumentpanelsgrupp](../../assets/create-dashboard-groups-existing-dashboard.png)

## Lägg till befintliga instrumentpaneler i befintliga grupper

1. På sidan `Manage Data > Dashboards` väljer du den instrumentpanel som gruppen ska ändras för.

1. Texten under `Dashboard Group (optional)` visar den aktuella instrumentpanelsgruppen för instrumentpanelen.

1. Om du vill ändra gruppen på instrumentpanelen väljer du en annan grupp i listan - i det här fallet `PS`, `Campaigns`.

   ![ändra gruppkontrollpanel](../../assets/add-existing-dashboard-existing-group.png)

## Ta bort panelgrupper

När det inte finns några kontrollpaneler i en kontrollpanelgrupp tas den bort automatiskt.
