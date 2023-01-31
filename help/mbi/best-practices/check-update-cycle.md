---
title: Kontrollera statusen för uppdateringscykeln
description: Lär dig hur du kontrollerar statusen för uppdateringscykeln.
exl-id: bd65f2bb-86c1-4e83-a132-797694ddb086
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---

# Uppdatera förlopp för cykel

När du loggar in på [!DNL MBI] på kontrollpanelen finns det flera sätt att kontrollera status för den senaste uppdateringscykeln. Det beror helt på vilken typ av [användarbehörigheter](../administrator/user-management/user-management.md) det har du.

## Varför ska jag kontrollera statusen för uppdateringscykeln?

Att kontrollera statusuppdateringscykeln är användbart när du granskar data i [!DNL MBI] konto. Om du ser [resultat som inte uppfyller dina förväntningar](../data-analyst/data-warehouse-mgr/data-and-updates-faq.md)t.ex. daglig försäljning [!DNL MBI] matchar inte det du ser i din e-handelsplattform eller i din [[!DNL Google] e-handelsintäkter](https://support.magento.com/hc/en-us/articles/360016505232) Du kan kontrollera den sista datapunkten för att se om problemet kommer att lösas när en uppdatering har slutförts.

## [!UICONTROL Read-Only] och [!UICONTROL Standard]** Användare

`Read-only` användare kan logga in på sin kontrollpanel och se hur nyligen data har uppdaterats genom att hålla markören över ikonen längst upp till höger på sidan. Detta visas när den sista datapunkten har dragits.

![](../../mbi/assets/last-success-data.png)

## [!UICONTROL Admin] Användare

`Admin` -användare kan logga in på kontrollpanelen och se den sista datapunkten ovan, tillsammans med en kort statusikon för sina kontointegreringar.

Mer information får du av administratörer som kan klicka **[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]**.

![](../../mbi/assets/detail-manage-data-integrations.png)

På den här sidan visas aktuell uppdateringsstatus och tidpunkten för den senaste slutförda uppdateringen.

Om en uppdatering pågår ser du en länk för att begära ett e-postmeddelande när uppdateringen har slutförts.

Om en uppdatering inte pågår visas en länk som tvingar en uppdatering att starta.

>[!NOTE]
>
>Om du har öppethållande timmar (tid när du inte vill ha det) [!DNL MBI] om du vill uppdatera dina data) kommer en uppdatering att starta en uppdateringscykel som inte respekterar begränsningarna för dessa öppningstider.
