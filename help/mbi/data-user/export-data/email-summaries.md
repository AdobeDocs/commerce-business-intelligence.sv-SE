---
title: Skapa automatiska e-postsammanfattningar
description: Lär dig hur du skapar automatiska e-postsammanfattningar.
exl-id: a9aea4fc-9193-467f-8554-3ad77ac3fa73
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# Skapa automatiska e-postsammanfattningar

E-postsammanfattningar är ett kraftfullt kommunikationsverktyg som du kan använda för att dela status och trender i din verksamhet med viktiga intressenter. Med e-postsammanfattningar kan du:

* E-posta grafiska sammanfattningar som innehåller rapporter
* Inkludera eller exkludera e-postsammanfattningens författare från att ta emot e-postmeddelandet
* Schemalägg när e-postmeddelandet skickas
* Redigera, ta bort och pausa befintliga schemalagda e-postsammanfattningar

## Skapa ny e-postsammanfattning

1. Klicka **[!DNL Manage Data]** sedan **[!UICONTROL Email Summary]** i sidlisten.

   Om det är första gången du skapar en e-postsammanfattning visas inga sparade sammanfattningar på den här sidan.

1. Klicka **[!UICONTROL Create New Email Summary]** i det övre högra hörnet.

1. Ange ett namn för sammanfattningen.

   Välj ett namn som visar vad som ingår i sammanfattningen. Till exempel: `AOV Comparison`.

1. I `Choose Content` markerar du de rapporter som du vill ta med i sammanfattningen.

   Du kan välja upp till tio rapporter som du äger. När du har valt en rapport använder du de ikoner som visas för att välja om du vill att rapporten ska skickas som en tabell eller ett diagram. Om du sparade rapporten som ett nummer kan du bara skicka den som ett nummer. Information om hur du skickar en e-postsammanfattning som innehåller en rapport med inaktuella data finns i [Hantera dina kontoinställningar](../../administrator/account-management/managing-account-settings.md).

   >[!NOTE]
   >
   >`Cohort` rapporter är bara tillgängliga om du använder den nya arkitekturen.

1. (Valfritt) Välj `Send Email To Me` om du vill få e-postmeddelandet.

1. Om du vill inkludera andra användare i e-postmeddelandet anger du deras e-postadresser i dialogrutan `Add Email Recipients` fält avgränsade med kommatecken, blanksteg, tabbar eller semikolon.

## Schemalägg e-postsammanfattning

I `Set when to send the Email Summary` kan du ange när e-postsammanfattningarna ska skickas. Alternativen är:

* `Manual`
* `Once`
* `Repeating`

### Spara e-postsammanfattning som ska skickas senare

1. Välj `Manual` från `Set when to send the Email Summary` fält.

1. Klicka **[!UICONTROL Save]**.

   Sammanfattningen sparas då i listan med e-postsammanfattningar.

1. När du är klar att skicka sammanfattningen klickar du på kugghjulsikonen och väljer `Send Now`.

### Skicka e-postsammanfattning en gång

1. Välj `Once` från `Set when to send the Email Summary` fält.

1. Ange startdatum i dialogrutan `Select Start Date` kalender.

1. Ange när e-postmeddelandet ska skickas i dialogrutan `Select time to send` fält.

### Skapa upprepande schema

1. Välj `Repeating` från `Set when to send the Email Summary` fält.

1. I `Set Frequency` fält, markera `Daily`, `Weekly`, eller `Monthly`.

1. Ange startdatum i dialogrutan `Select Start Date` kalender.

1. Ange när e-postmeddelandet ska skickas i dialogrutan `Select time to send` fält.

1. (Valfritt) Om du vill ange ett slutdatum väljer du `End Date` och välj slutdatumet i kalendern.

## Ändra befintlig e-postsammanfattning

När du har skapat och sparat en e-postsammanfattning kan du `Email Summaries` visas en lista med alla sparade sammanfattningar. Du kan expandera (`+`) varje rad för mer information. Kolumnerna i den här vyn är:

* `Email Name` - Namn på e-postsammanfattning
* `Content` - Typ av innehåll i sammanfattningen, t.ex. namn på rapporter. Information om hur du skickar en e-postsammanfattning som innehåller en rapport med inaktuella data finns i [Hantera dina kontoinställningar](../../administrator/account-management/managing-account-settings.md).
* `Scheduled` - Frekvens, datum och tid när e-postsammanfattningen skickas
* `Recipients` - Mottagare av e-postsammanfattning
* `Created Date` - Det datum då e-postsammanfattningen skapades
* `Status` - `Paused` eller `Active`

Klicka på kugghjulsikonen till höger om varje rad för att:

* `Send Now` - Skickar e-postsammanfattningen omedelbart till alla angivna mottagare
* `Edit` - Gör att du kan ändra informationen i e-postsammanfattningen
* `Pause/Active` - Gör att du kan pausa att e-postsammanfattningen levereras eller aktivera sammanfattningen baserat på hur den har konfigurerats
* `Delete` - Tar bort e-postsammanfattningen
