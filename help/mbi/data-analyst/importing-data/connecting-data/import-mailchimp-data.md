---
title: Importera MailChimp-data
description: Lär dig att importera MailChimp-data till  [!DNL Commerce Intelligence].
exl-id: 5595c6a6-5476-4a0e-a493-ddc32161894e
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# Importera [!DNL Mailchimp]-data

Om du vill få en heltäckande bild av dina kampanjsatsningar kan du importera dina [!DNL Mailchimp]-e-postkampanjdata till [!DNL Commerce Intelligence]. För att kunna slutföra importen måste du göra följande för varje [!DNL Mailchimp]-kampanj du har:

## Exportera Öppnar data {#opens}

1. Gå till fliken [!DNL Mailchimp] när du har loggat in på `Campaigns`.

   ![importera mailchimp 1](../../../assets/import-mailchimp-1.png)

1. Klicka på **[!UICONTROL View Report]** bredvid kampanjnamnet.

   ![importera mailchimp 2](../../../assets/import-mailchimp-2.png)

1. Klicka på **[!UICONTROL Opened]**-numret.

   ![importera mailchimp 3](../../../assets/import-mailchimp-3.png)

1. Klicka på **[!UICONTROL Export]** och spara filen `.csv`.

   Du måste lägga till `primary key`-, `date (mm/dd/yyyy)`- och `campaign name`-kolumner i den här filen. Kontrollera att `primary keys` är unik för varje rad.

   ![importera mailchimp 4](../../../assets/import-mailchimp-4.png)

## Exportera klickdata {#clicks}

1. Gå tillbaka till skärmen `View Report` för kampanjen.

1. Klicka på numret som `Clicked`.

   ![importera mailchimp 5](../../../assets/import-mailchimp-5.png)

1. Klicka på siffran under kolumnen `Total Clicks` ELLER `Unique Clicks`.

   ![importera mailchimp 6](../../../assets/import-mailchimp-6.png)

1. Klicka på **[!UICONTROL Export]** och spara filen `.csv`.

   Du måste lägga till `Primary Key`, `date (mm/dd/yyyy)`, `campaign name` och `URL` kolumner i den här filen. Du behöver inte lägga till den fullständiga URL:en, bara något som talar om vad du klickade på.

   ![importera mailchimp 7](../../../assets/import-mailchimp-7.png)

1. Upprepa steg 3 och 4 för varje URL som du klickar på i ditt e-postmeddelande och kombinera alla data i samma `.csv`-fil när du är klar.

## Exportera skickade data {#sent}

1. Gå till fliken `Campaigns` i [!DNL Mailchimp].

1. Klicka på **[!UICONTROL View Report]** bredvid kampanjnamnet.

1. Klicka på siffran bredvid `Recipients`.

   ![importera mailchimp 8](../../../assets/import-mailchimp-8.png)

1. Klicka på **[!UICONTROL Export]** och spara filen `.csv`.

   Du måste lägga till `Primary Key`-, `date (mm/dd/yyyy)`- och `campaign name`-kolumner i den här filen.

   ![importera mailchimp 9](../../../assets/import-mailchimp-9.png)

## Förbered filer för överföring till [!DNL Commerce Intelligence] {#upload}

Varje fil - `Opens`, `Clicks` och `Sent` - ska överföras till [!DNL Commerce Intelligence] som en separat fil. Adobe rekommenderar att du namnger filerna med följande namnkonvention: `MailChimp\_ACTION\_DATE`. Ersätt `ACTION` med `Open`, `Click` eller `Sent` och ersätt `DATE` med exportdatumet.

När du är redo att överföra filerna använder du [`File Upload`-funktionen &#x200B;](../connecting-data/using-file-uploader.md) för att hämta data till din Data Warehouse.
