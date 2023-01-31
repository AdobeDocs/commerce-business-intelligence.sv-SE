---
title: Ändra en mätnings driftstabell
description: Lär dig hur du ändrar datatabellen som ett mått använder för att utföra sin åtgärd.
exl-id: c7a074ca-31f4-43e5-85d9-b64dca95dc23
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# Ändra en mätnings driftstabell

I vissa fall kan du ändra datatabellen som ett mätvärde använder för att utföra åtgärden. Om du t.ex. har en ny användartabell, vill du migrera dina användarrelaterade mått från tabellen&quot;Användare\_Gammal&quot; för att använda tabellen&quot;Användare\_Nytt&quot; i stället.

1. Gå till **[!UICONTROL Data]** > **[!UICONTROL Metrics]**
1. Klicka **[!UICONTROL Edit]** bredvid måttet som du vill ändra `operational` tabell.
1. Klicka på **[!UICONTROL Change]**.

   ![](../../assets/change-metrics-1.png)
1. Välj nu den nya tabell som du vill basera måttet på.
1. Därefter måste du matcha befintliga datamått med motsvarande datamått i den nya tabellen. Om du till exempel har en kolumn som heter `User's registration date`väljer du bara vilken kolumn i den nya tabellen som ska innehålla samma datumdata. (Se nästa steg om du inte har matchande kolumner i den nya tabellen)

   ![](../../assets/change-metrics-2.png)

1. Om du inte har någon matchande kolumn i den nya tabellen kan du antingen **skapa den i din datatabell** eller [kontakta support](../../guide-overview.md) om det är en beräkningskolumn eller en dimension som har gjorts av [!DNL MBI]), eller enkelt **ta bort dimensionen från måttet**. Om du vill ta bort en dimension som du inte längre behöver går du tillbaka till måttets redigerare och väljer vilka dimensioner du vill ta bort under `Dimensions`.

   ![](../../assets/change-metrics-3.png)
