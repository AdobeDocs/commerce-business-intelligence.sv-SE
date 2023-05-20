---
title: Import av marknadsdata från CJ Affiliate (Commission Junction)
description: Lär dig importera CJ Affiliate-data (Commission Junction) till [!DNL Commerce Intelligence].l Commerce Intelligence].
exl-id: 1db83f34-15a1-4599-ab0a-65d527ccae01
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 0%

---

# Importera [!DNL CJ Affiliate] data

Importera [!DNL CJ Affiliate (Commission Junction)] data till [!DNL Adobe Commerce Intelligence], följ bara stegen nedan och bifoga den resulterande filen till en [supportärende](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html). Adobe kommer att ställa in datatabellen ditt konto och tillåter dig att fortsätta överföra data oberoende av varandra.

## Exportera [!DNL CJ Affiliate] Data

1. I din [!DNL CJ Affiliate] konto går du till `Reports` -fliken.

1. I dialogrutan `Performance` -fliken väljer du `Report Options`.

1. Uppsättning `Performance By` lika med `Program`, `Trend` lika med `Daily`och `Date Range` är lika med det datumintervall som granskas.

   ![export-cj-affiliate-data](../../../assets/export-cj-affiliate-data-1.png)<!--{:.zoom}-->

1. Välj `Run Report`.

1. I dialogrutan `File Format` väljer du `CSV`.  Klicka **[!UICONTROL Download]**.

   ![exportera cj-affiliatedata](../../../assets/export-an-individual-order-2.jpg)<!--{:.zoom}-->

1. När du har hämtat filen kan du [överföra filen](../connecting-data/using-file-uploader.md) till din [!DNL Commerce Intelligence] Data Warehouse.

   Då skapas en tabell i [!DNL Commerce Intelligence] Data Warehouse som du kan fortsätta att överföra nya data till med jämna mellanrum. När du överför filen följer du formateringskraven i [Använda filöverföraren](../connecting-data/using-file-uploader.md).
