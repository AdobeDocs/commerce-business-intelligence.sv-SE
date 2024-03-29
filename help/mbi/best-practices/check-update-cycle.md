---
title: Kontrollera statusen för uppdateringscykeln
description: Lär dig hur du kontrollerar statusen för uppdateringscykeln.
exl-id: bd65f2bb-86c1-4e83-a132-797694ddb086
role: Admin, Data Architect, Data Engineer, User
feature: Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# Uppdatera förlopp för cykel

När du loggar in på [!DNL Adobe Commerce Intelligence] på kontrollpanelen finns det flera sätt att kontrollera status för den senaste uppdateringscykeln. Allt beror på typen av [användarbehörigheter](../administrator/user-management/user-management.md) som du har.

## Varför ska jag kontrollera statusen för uppdateringscykeln?

Att kontrollera statusuppdateringscykeln är användbart när du granskar data i [!DNL Commerce Intelligence] konto. Om du ser [resultat som inte uppfyller dina förväntningar](../data-analyst/data-warehouse-mgr/data-and-updates-faq.md)till exempel daglig försäljning i [!DNL Commerce Intelligence] matchar inte det du ser i e-handelsplattformen eller i [[!DNL Google] e-handelsintäkter](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html) Du kan kontrollera den sista datapunkten för att se om problemet är löst när en uppdatering har slutförts.

## [!UICONTROL Read-Only] och [!UICONTROL Standard] Användare

`Read-only` användare kan logga in på sin kontrollpanel och se hur nyligen data har uppdaterats genom att hålla markören över ikonen längst upp till höger på sidan. Detta visar när den sista datapunkten hämtades.

![](../../mbi/assets/last-success-data.png)

## [!UICONTROL Admin] Användare

`Admin` -användare kan logga in på kontrollpanelen och se den sista datapunkten ovan, tillsammans med en kort statusikon för sina kontointegreringar.

Mer information får du av administratörer som kan klicka **[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]**.

![](../../mbi/assets/detail-manage-data-integrations.png)

På den här sidan visas aktuell uppdateringsstatus och tidpunkten för den senaste slutförda uppdateringen.

Om en uppdatering pågår visas en länk för att begära ett e-postmeddelande när uppdateringen har slutförts.

Om en uppdatering inte pågår visas en länk som tvingar en uppdatering att starta.

>[!NOTE]
>
>Om du har öppethållande timmar (tid när du inte vill ha det [!DNL Commerce Intelligence] för att uppdatera dina data) startas en uppdateringscykel som inte respekterar begränsningarna för dessa öppningstider.
