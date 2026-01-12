---
title: Skapa automatiska e-postsammanfattningar
description: Lär dig skapa automatiska e-postsammanfattningar.
exl-id: a9aea4fc-9193-467f-8554-3ad77ac3fa73
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: a65ededb203b7551fdfcb31cff130ef85b01fbe3
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 0%

---

# Skapa automatiska e-postsammanfattningar

E-postsammanfattningar är ett kraftfullt kommunikationsverktyg som du kan använda för att dela status och trender i din verksamhet med viktiga intressenter. Med e-postsammanfattningar kan du:

* E-posta grafiska sammanfattningar som innehåller rapporter
* Inkludera eller exkludera e-postsammanfattningens författare från att ta emot e-postmeddelandet
* Schemalägg när e-postmeddelandet skickas
* Redigera, ta bort och pausa befintliga schemalagda e-postsammanfattningar

## Skapa ny e-postsammanfattning

1. Klicka på **[!DNL Manage Data]** och sedan på **[!UICONTROL Email Summary]** i sidofältet.

   Om det här är första gången du skapar en e-postsammanfattning visas inga sparade sammanfattningar på den här sidan.

1. Klicka på **[!UICONTROL Create New Email Summary]** längst upp till höger.

1. Ange ett namn för sammanfattningen.

   Välj ett namn som visar vad som ingår i sammanfattningen. Exempel: `AOV Comparison`.

1. I avsnittet `Choose Content` markerar du de rapporter som du vill ta med i sammanfattningen.

   Det finns två alternativ för att lägga till innehåll:

   * **Välj enskilda rapporter** - Välj specifika rapporter från dina instrumentpaneler
   * **Markera hela instrumentpanelen** - Inkludera alla rapporter från en instrumentpanel så som de visas i instrumentpanelslayouten

   Du kan välja upp till tio rapporter som du äger. När du har valt en rapport använder du de ikoner som visas för att välja om du vill att rapporten ska skickas som en tabell eller ett diagram. Om du sparade rapporten som ett nummer kan du bara skicka den som ett nummer. Mer information om hur du skickar en e-postsammanfattning som innehåller en rapport med inaktuella data finns i [Hantera dina kontoinställningar](../../administrator/account-management/managing-account-settings.md).

   Om du vill lägga till hela kontrollpaneler har du följande format- och borttagningsalternativ:

   * Ändra rapportens format till ett diagram eller en tabell
   * Ta bort rapporter från att inkluderas i e-postmeddelandet
   * Välj det här alternativet om du vill inkludera en CSV-fil för tabellrapporter. På så sätt kan mottagarna få åtkomst till rådata som kan exporteras direkt från sin inkorg.

   >[!NOTE]
   >
   >`Cohort` rapporter är bara tillgängliga om du använder den nya arkitekturen.

   >[!NOTE]
   >
   >Stora CSV-bilagor stöds upp till totalt 25 MB per e-post.

1. (Valfritt) Välj `Send Email To Me` om du vill få e-postmeddelandet.

1. Om du vill inkludera andra användare i e-postmeddelandet anger du deras e-postadresser i fältet `Add Email Recipients`, avgränsade med kommatecken, blanksteg, tabbar eller semikolon.

## Schemalägg e-postsammanfattning

I fältet `Set when to send the Email Summary` kan du ange när e-postsammanfattningarna ska skickas. Alternativ:

* `Manual`
* `Once`
* `Repeating`

### Spara e-postsammanfattning som ska skickas vid ett senare datum

1. Välj `Manual` i fältet `Set when to send the Email Summary`.

1. Klicka på **[!UICONTROL Save]**.

   Sammanfattningen sparas då i listan med e-postsammanfattningar.

1. När du är redo att skicka sammanfattningen klickar du på kugghjulsikonen och väljer `Send Now`.

### Skicka e-postsammanfattning en gång

1. Välj `Once` i fältet `Set when to send the Email Summary`.

1. Ange startdatumet i kalendern `Select Start Date`.

1. Ange den tid det tar att skicka e-postmeddelandet i fältet `Select time to send`.

### Skapa upprepande schema

1. Välj `Repeating` i fältet `Set when to send the Email Summary`.

1. I fältet `Set Frequency` väljer du `Daily`, `Weekly` eller `Monthly`.

1. Ange startdatumet i kalendern `Select Start Date`.

1. Ange den tid det tar att skicka e-postmeddelandet i fältet `Select time to send`.

1. (Valfritt) Om du vill ange ett slutdatum väljer du `End Date` och väljer slutdatumet i kalendern.

## Ändra befintlig e-postsammanfattning

När du har skapat och sparat en e-postsammanfattning visas en lista med alla sparade sammanfattningar på sidan `Email Summaries`. Du kan expandera (`+`) i varje rad om du vill ha mer information. Kolumnerna i den här vyn är:

* `Email Name` - Namn på e-postsammanfattning
* `Content` - Innehållstyp i sammanfattningen, till exempel namn på rapporter
* `Scheduled` - Frekvens, datum och tid när e-postsammanfattningen skickas
* `Recipients` - Mottagare av e-postsammanfattningen
* `Created Date` - Det datum då e-postsammanfattningen skapades
* `Status` - `Paused` eller `Active`

>[!NOTE]
>
>Mer information om hur du skickar en e-postsammanfattning som innehåller en rapport med inaktuella data finns i [Hantera dina kontoinställningar](../../administrator/account-management/managing-account-settings.md).

Klicka på kugghjulsikonen till höger om varje rad för att:

* `Send Now` - Skicka e-postsammanfattningen direkt till alla angivna mottagare
* `Edit` - Ändra informationen i e-postsammanfattningen
* `Pause/Active` - Pausa eller aktivera leverans av e-postsammanfattning
* `Delete` - Ta bort e-postsammanfattningen
