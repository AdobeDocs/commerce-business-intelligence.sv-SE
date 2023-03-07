---
title: Importera Länkdelningsdata
description: Lär dig importera Länkdelning-data till [!DNL MBI].
exl-id: 1c2025a6-746c-4929-bbb1-62af1afcbc49
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---

# Importera `Linkshare` data

För att ta med `Linkshare` data till [!DNL MBI]måste du göra två saker:

1. [Exportera länkdelningsdata i ](#export)
1. [Överför kalkylbladet till [!DNL MBI]](../connecting-data/using-file-uploader.md)

## Exportera data från Länkshare {#export}

1. I `Linkshare` konto, gå till **[!UICONTROL Reports** > **Run Reports].**

1. I `Report` listruta, välja **[!UICONTROL Sales & Activity Report]**.

1. Låt alla andra alternativ i listrutan vara standardval.

1. I `Date Range` listruta, välj valfritt alternativ (`Sun - Sat`, `Mon - Sun`) matchar `Start of Week` inställningar i [!DNL MBI].

1. Rensa `Compare Year-Over-Year Data` kryssrutan.

1. Under `Data Type`, markera `Transaction Date`.

   ![importera\_linkshare\_data.png](../../../assets/importing_linkshare_data.png)

1. Klicka **[!UICONTROL View Report]**.

1. Klicka **[!UICONTROL Download]**.

   I det här skedet `.csv` och laddas ned.

När filen har laddats ned kan du överföra den till [!DNL MBI] med [`File Upload` funktion](../connecting-data/using-file-uploader.md).
