---
title: Ändra en mätnings användningstabell
description: Lär dig hur du ändrar datatabellen som ett mått använder för att utföra sin åtgärd.
exl-id: c7a074ca-31f4-43e5-85d9-b64dca95dc23
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '213'
ht-degree: 0%

---

# Ändra en mätnings användningstabell

I vissa fall kan du ändra datatabellen som ett mätvärde använder för att utföra åtgärden. Om du till exempel har en ny användartabell vill du migrera dina användarrelaterade mått från tabellen `Users\_Old` så att tabellen `Users\_New` används i stället.

1. Gå till **[!UICONTROL Data]** > **[!UICONTROL Metrics]**
1. Klicka på **[!UICONTROL Edit]** bredvid måttet som du vill ändra tabellen `operational` för.
1. Klicka på **[!UICONTROL Change]** i redigeraren.

   ![](../../assets/change-metrics-1.png)
1. Välj den nya tabell som du vill basera måttet på.
1. Matcha befintliga datamått med motsvarande i den nya tabellen. Om du t.ex. har en kolumn med namnet `User's registration date` väljer du bara vilken kolumn i den nya tabellen som ska registrera samma datumdata. (Se nästa steg om du inte har matchande kolumner i den nya tabellen)

   ![](../../assets/change-metrics-2.png)

1. Om du inte har någon matchande kolumn i den nya tabellen kan du antingen **skapa den i datatabellen** eller [kontakta support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) om det är en beräkningskolumn eller en dimension som har skapats av [!DNL Commerce Intelligence]. Du kan också **ta bort dimensionen från måttet**. Om du vill ta bort en dimension som du inte längre behöver går du tillbaka till måttets redigerare och väljer vilka dimensioner som ska tas bort under `Dimensions`.

   ![](../../assets/change-metrics-3.png)
