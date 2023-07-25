---
title: Importera Länkdelningsdata
description: Lär dig importera Länkdelning-data till [!DNL Commerce Intelligence].
exl-id: 1c2025a6-746c-4929-bbb1-62af1afcbc49
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '94'
ht-degree: 0%

---

# Importera [!DNL Linkshare] data

För att ta med [!DNL Linkshare] data till [!DNL Adobe Commerce Intelligence]måste du göra två saker:

1. [Exportera länkdelningsdata i ](#export)
1. [Överför kalkylbladet till [!DNL Commerce Intelligence]](../connecting-data/using-file-uploader.md)

## Exportera data från Länkshare {#export}

1. I [!DNL Linkshare] konto, gå till **[!UICONTROL Reports** > **Run Reports].**

1. I `Report` listruta, välja **[!UICONTROL Sales & Activity Report]**.

1. Låt alla andra alternativ i listrutan vara standardval.

1. I `Date Range` listruta, välj valfritt alternativ (`Sun - Sat`, `Mon - Sun`) matchar `Start of Week` inställningar i [!DNL Commerce Intelligence].

1. Rensa `Compare Year-Over-Year Data` kryssrutan.

1. Under `Data Type`, markera `Transaction Date`.

   ![importera\_linkshare\_data.png](../../../assets/importing_linkshare_data.png)

1. Klicka **[!UICONTROL View Report]**.

1. Klicka **[!UICONTROL Download]**.

   I det här skedet `.csv` och laddas ned.

När filen har laddats ned kan du överföra den till [!DNL Commerce Intelligence] med [`File Upload` funktion](../connecting-data/using-file-uploader.md).
