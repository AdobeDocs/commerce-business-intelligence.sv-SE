---
title: Importerar marknadsföringsdata för CJ-dotterbolag (Commission Junction)
description: Lär dig importera CJ-filialdata (Commission Junction) till [!DNL Commerce Intelligence].L Commerce Intelligence].
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---

# Importera [!DNL CJ Affiliate] data

Importera [!DNL CJ Affiliate (Commission Junction)] data till [!DNL Adobe Commerce Intelligence]följer du bara stegen nedan och bifogar den resulterande filen till en [supportanmälan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html). Adobe ställer in datatabellen för ditt konto och låter dig fortsätta överföra data oberoende av varandra.

## Exportera [!DNL CJ Affiliate] Data

1. I [!DNL CJ Affiliate] konto, gå till `Reports` -fliken.

1. I `Performance` flik, välja `Report Options`.

1. Ange `Performance By` lika med `Program`, `Trend` lika med `Daily`och `Date Range` är lika med det datumintervall som granskas.

   ![export-cj-affiliate-data](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. Välj `Run Report`.

1. I `File Format` listruta, välja `CSV`.  Klicka **[!UICONTROL Download]**.

   ![exportera cj-filialdata](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. När du har laddat ned filen kan du [ladda upp filen](../connecting-data/using-file-uploader.md) till [!DNL Commerce Intelligence] data warehouse.

   Då skapas en tabell i [!DNL Commerce Intelligence] data warehouse som du kan fortsätta att överföra färska data till regelbundet. När du överför filen följer du formateringskraven i [Använda filöverföringsprogrammet](../connecting-data/using-file-uploader.md).
