---
title: Importerar marknadsföringsdata för CJ-dotterbolag (Commission Junction)
description: Lär dig importera CJ-filialdata (Commission Junction) till [!DNL MBI].L MBI].
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---

# Importera `CJ Affiliate` data

Importera `CJ Affiliate` (kommissionens knutpunkt) data till [!DNL MBI]följer du bara stegen nedan och bifogar den resulterande filen till en supportanmälan. Vi skapar datatabellen för ditt konto och låter dig fortsätta överföra data oberoende av varandra.

## Exportera `CJ Affiliate` Data

1. I `CJ Affiliate` konto, gå till `Reports` -fliken.

1. I `Performance` flik, välja `Report Options`.

1. Ange `Performance By` lika med `Program`, `Trend` lika med `Daily`och `Date Range` är lika med det datumintervall som granskas.

   ![export-cj-affiliate-data](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. Välj `Run Report`.

1. I `File Format` listruta, välja `CSV`.  Klicka **[!UICONTROL Download]**.

   ![exportera cj-filialdata](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. När du har laddat ned filen kan du [ladda upp filen](../connecting-data/using-file-uploader.md) till [!DNL MBI] data warehouse.

   Då skapas en ny tabell i [!DNL MBI] data warehouse som du kan fortsätta att överföra färska data till regelbundet. När du överför filen måste du följa formateringskraven som anges i [Använda filöverföringsprogrammet](../connecting-data/using-file-uploader.md).
