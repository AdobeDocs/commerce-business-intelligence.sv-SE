---
title: Instrumentpanelsövergripande filtrering
description: Lär dig göra massredigeringar av alla rapporter på en specifik kontrollpanel.
exl-id: 379d0027-8a7a-4062-a66a-4f06c37b806c
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# Instrumentpanelsövergripande filtrering

Med filtrering på hela kontrollpanelen kan du göra massredigeringar av alla rapporter på en specifik kontrollpanel. Du kan snabbt visa samma analys över olika tidsperioder eller för olika butiker. Du kan enkelt jämföra prestanda för ett föregående år, en månad eller en vecka per butik. Du kan uppdatera en hel instrumentpanel för att passa en nyligen lanserad kampanj.

## Datumfilter

Om du vill ändra datumintervallet eller intervallet för rapporter på en kontrollpanel klickar du på kalenderikonen i det övre högra hörnet (![kalender](../../assets/calendar-button.png)).

Du kan välja att visa data med en `Fixed Date Range` eller olika förberäknade `Moving Date Ranges`:

![rörliga datumintervall](../../assets/moving_date_ranges.png)

Alternativen för `Last Full...` rörligt intervall representerar det senast slutförda intervallet, medan `This...` är det aktuella pågående intervallet. Om det till exempel är juni är `Last Full Month` _maj 1 - 31 maj_, medan `This Month` är _juni 1 - nu_.

Eller skapa en egen `Custom Moving Range`\:

![anpassat rörligt område](../../assets/custom-moving-range.png)

Välj att ändra intervallet också. Om du väljer standardknappen (![standardtidsintervall](../../assets/time_interval_default.png)) innebär det att endast datumintervallet ändras:

![tidsintervall](../../assets/time_interval.png)

Om du vill återställa alla rapporter till det ursprungliga datumintervallet och intervallet klickar du på **[!UICONTROL Restore Defaults]** eller **[!UICONTROL Cancel]**.

När du anger ett datumfilter för en kontrollpanel tillämpas det filtret endast på den instrumentpanelen. Det används inte när du navigerar till andra instrumentpaneler.

>[!NOTE]
>
>För närvarande ingår inte `Cohort Reports` och `SQL Reports` när ändringar tillämpas på en instrumentpanelsnivå.

## Butiksfilter

Om du vill analysera hur en viss butik fungerar klickar du på butiksikonen i det övre högra hörnet (![Butiksfilter](../../assets/store-filter.png)). Som standard är `Store Filter` inställd på `All Stores`, vilket visar data från alla [butiksvyer](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/store-views.html) som är tillgängliga på din Commerce-webbplats.

>[!NOTE]
>
>Ett arkivfilter är aktiverat eller inaktiverat för ett helt [!DNL Commerce Intelligence]-konto. Om en instrumentpanel innehåller rapporter som inte påverkas av filtret (till exempel rapporter som inte är byggda på [!DNL Adobe Commerce]-data) uppdateras inte dessa rapporter när arkivfiltret används. Du kan [kontakta support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) om du anser att en rapport ska uppdateras baserat på arkivval eller om du tror att kontoarkivfiltret har inaktiverats av misstag.

När du väljer en butik i `Store Filter` behåller filtret markeringen när du navigerar mellan instrumentpaneler. Om du behåller din markering kan du visa data för den valda butiken överallt tills du väljer `All Stores`.

## Filter för delade instrumentpaneler

Om en användare konfigurerar datumfiltret för delade instrumentpaneler ser andra användare med åtkomst till kontrollpanelen att samma filter tillämpas. Butiksfiltret gäller dock inte i det här fallet. Om instrumentpanelens ägare konfigurerar arkivfiltret och delar instrumentpanelen, kommer det konfigurerade arkivfiltret inte att finnas kvar för en annan användare. En användare måste ha [redigeringsåtkomst](../../data-user/dashboards/share-dashboard-with-users.md) till en instrumentpanel för att kunna justera kontrollpanelsfiltren.
