---
title: Dataverifiering i blandpanelen
description: Lär dig hur du bekräftar att du har synkroniserat alla data som är tillgängliga för dig direkt i Mixpanel.
exl-id: d18ce954-26fe-4440-ad8b-4f266c007b2f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '112'
ht-degree: 0%

---

# Dataverifiering i [!DNL Mixpanel]

När [!DNL Adobe Commerce Intelligence] först ansluter till [!DNL Mixpanel] data kan din kontohanterare eller analytiker begära att du exporterar data från [!DNL Mixpanel] för valideringsändamål. På så sätt kan du bekräfta att du har synkroniserat alla data som är tillgängliga direkt i [!DNL Mixpanel].

## Dataexportprocess: `Events`

1. Besök `Segmentation` avsnitt och vy `Your Top Events`.

   ![](../../../assets/your-top-events.png)

1. Välj `Past 96 Hours` för tidsintervallet

   ![](../../../assets/past-96-hours.png)

1. Bläddra till den nedre högra delen av rapporten och exportera en `.csv` fil:

   ![](../../../assets/export-csv-mixpanel.png)

1. Skicka `.csv` till kontohanteraren eller analytikern som du arbetar med i den här valideringsprocessen.
