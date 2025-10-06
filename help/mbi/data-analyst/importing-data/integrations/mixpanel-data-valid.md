---
title: Dataverifiering i blandpanelen
description: Lär dig hur du bekräftar att du har synkroniserat alla data som är tillgängliga för dig direkt i Mixpanel.
exl-id: d18ce954-26fe-4440-ad8b-4f266c007b2f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '134'
ht-degree: 0%

---

# Dataverifiering i [!DNL Mixpanel]

När [!DNL Adobe Commerce Intelligence] först ansluter till dina [!DNL Mixpanel]-data kan din kontohanterare eller analytiker begära att du anger dataexport från [!DNL Mixpanel] i valideringssyfte. På så sätt kan du bekräfta att du har synkroniserat alla data som är tillgängliga direkt i [!DNL Mixpanel].

## Dataexportprocess: `Events`

1. Besök ditt `Segmentation`-avsnitt och visa `Your Top Events`.

   ![Kontrollpanel med blandade paneler som visar de vanligaste händelserna](../../../assets/your-top-events.png)

1. Välj `Past 96 Hours` för tidsintervallet

   ![Intervallväljare för blandpanel med alternativ för de senaste 96 timmarna](../../../assets/past-96-hours.png)

1. Bläddra till den nedre högra delen av rapporten och exportera en `.csv`-fil:

   ![Alternativet Exportera från en blandpanel till CSV på menyn](../../../assets/export-csv-mixpanel.png)

1. Skicka filen `.csv` till kontohanteraren eller analytikern som du arbetar med i den här valideringsprocessen.
