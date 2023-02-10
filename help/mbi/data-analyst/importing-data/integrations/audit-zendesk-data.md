---
title: Granska Zendesk-data
description: Lär dig hur du exporterar dina Zendesk-data.
exl-id: 3c8dcc72-3623-4c4e-a941-f431a97571e0
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# Granska Zendesk-data

Hittade något konstigt i [[!DNL Zendesk] data](../integrations/exp-zendesk-data.md)? För att identifiera problemet måste vi utforska dina data. Detta kan du göra genom att exportera [!DNL Zendesk] till en nedladdningsbar fil.

## Aktivera dataexport

Dataexport är för närvarande inte aktiverad för alla [!DNL Zendesk] konton. Om du vill aktivera den här funktionen [skicka en supportanmälan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en), som talar om [!DNL Zendesk] underdomännamn.

>[!NOTE]
>
>Endast `Enterprise` och `Plus` planer har för närvarande tillgång till den här funktionen.

När dataexporten är aktiverad kan bara administratörer i en viss e-postdomän exportera data från [!DNL Zendesk] konto. Den här e-postdomänen är vanligtvis samma e-postdomän som din [!DNL Zendesk]. Kontoägarens e-postdomän används som standard, men du kan ändra domänen om det behövs.

## Exportera till en hämtningsbar fil

1. Klicka på ikonen Admin (kugghjulslogotyp) i sidlisten och välj **[!UICONTROL Manage** > **Reports]**.
1. Klicka på **[!UICONTROL Export]** -fliken.
1. Klicka **[!UICONTROL Request file]** bredvid Fullständig XML-export enligt bilden nedan.

   Nu börjar en byggprocess; du får ett mejl när det är klart.
   ![reports_export_new.png](../../../assets/reports_export_new.png)

1. Klicka på länken i e-postmeddelandet för att ladda ned en ZIP-fil som innehåller rapporten.

   Den här nedladdningslänken gäller i minst tre dagar.

Den här processen skapar en XML-fil som innehåller all information som finns lagrad i den aktuella [!DNL Zendesk] konto, inklusive biljettdata (med kommentarer), användardata och kontodata. Nu kan du [skicka en supportanmälan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) (bifoga den här filen!) så att vi kan ta en närmare titt på era data. Om filen är för stor kan du dela den med [!DNL MBI] team via [!DNL Dropbox] eller [!DNL Google Drive].

Mer information om [!DNL Zendesk] filexport, se den officiella [[!DNL Zendesk] exportdokumentation](https://support.zendesk.com/hc/en-us/articles/4408886165402-Exporting-data-to-a-JSON-CSV-or-XML-file).
