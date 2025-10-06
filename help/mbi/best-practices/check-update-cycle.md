---
title: Kontrollera statusen för uppdateringscykeln
description: Lär dig hur du kontrollerar statusen för uppdateringscykeln.
exl-id: bd65f2bb-86c1-4e83-a132-797694ddb086
role: Admin, Data Architect, Data Engineer, User
feature: Dashboards
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# Uppdatera förlopp för cykel

När du loggar in på din [!DNL Adobe Commerce Intelligence]-instrumentpanel finns det flera sätt att kontrollera status för din senaste uppdateringscykel. Allt beror på vilken typ av [användarbehörigheter](../administrator/user-management/user-management.md) du har.

## Varför ska jag kontrollera statusen för uppdateringscykeln?

Att kontrollera statusuppdateringscykeln är användbart när du granskar data i ditt [!DNL Commerce Intelligence]-konto. Om du ser [resultat som inte uppfyller dina förväntningar](../data-analyst/data-warehouse-mgr/data-and-updates-faq.md), till exempel, matchar inte daglig försäljning i [!DNL Commerce Intelligence] det du ser i din e-handelsplattform eller i dina [[!DNL Google] e-handelsintäkter](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html), kan du kontrollera den sista datapunkten för att se om problemet har lösts när en uppdatering är klar.

## [!UICONTROL Read-Only] och [!UICONTROL Standard] användare

`Read-only` användare kan logga in på sin instrumentpanel och se hur nyligen data har uppdaterats genom att hålla markören över ikonen längst upp till höger på sidan. Detta visar när den sista datapunkten hämtades.

![Senaste lyckade tidsstämpel för datauppdatering visas i gränssnittet](../../mbi/assets/last-success-data.png)

## [!UICONTROL Admin] användare

`Admin` användare kan logga in på instrumentpanelen och se den sista datapunkten ovan, tillsammans med en kort statusikon för sina kontointegreringar.

Administratörsanvändare kan klicka **[!UICONTROL Manage Data]** > **[!UICONTROL Integrations]** för mer information.

![Sidan Hantera dataintegreringar med anslutningsinformation och uppdateringsstatus](../../mbi/assets/detail-manage-data-integrations.png)

På den här sidan visas aktuell uppdateringsstatus och tidpunkten för den senaste slutförda uppdateringen.

Om en uppdatering pågår visas en länk för att begära ett e-postmeddelande när uppdateringen har slutförts.

Om en uppdatering inte pågår visas en länk som tvingar en uppdatering att starta.

>[!NOTE]
>
>Om du har öppethållande timmar (tid när du inte vill att [!DNL Commerce Intelligence] ska uppdatera dina data) anges, startar en uppdateringscykel som inte uppfyller begränsningarna för dessa öppningstider.
