---
title: Hantera dina kontoinställningar
description: Lär dig hur du anpassar dina kontoinställningar för Data warehouse.
exl-id: 847d51b1-287e-4c14-b64e-0bd9bfcccedc
role: Admin, User
feature: Accounts
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 0%

---

# Anpassa kontoinställningarna

>[!NOTE]
>
>Kräver [Administratörsbehörigheter.](../../administrator/user-management/user-management.md)

I [!DNL Commerce Intelligence] kan du anpassa dina kontoinställningar för Data warehouse. Du kommer åt dessa genom att välja organisationens namn i det övre högra hörnet på valfri skärm och sedan välja **[!UICONTROL Account Settings]** i listrutan.

* **[!UICONTROL Client Name:]** Den här inställningen visas i det övre högra hörnet av alla instrumentpaneler och på andra ställen i ditt konto. Om du vill ändra **[!UICONTROL "Vandelay Industries Co., Ltd]** till bara **[!UICONTROL "Vandelay]**, det är här vi ska göra det.

* **[!UICONTROL Currency:]** Det här är *standardvaluta* för alla monetära värden på ditt konto. När ett decimalvärde eller valutavärde synkroniseras till Data warehouse bestämmer den här inställningen vilken symbol som placerats före det värdet i dina rapporter.

* **[!UICONTROL Blackout Hours:]** Med den här inställningen får Data warehouse inte tillgång till dina anslutna databaser under de valda timmarna på dagen. Alla timmar uttrycks vid noll timmen och i EST (Eastern Standard Time). Om du t.ex. inte vill att din produktionsdatabas ska vara tillgänglig mellan timmarna 9:00 EST och 1:00 EST, skriver du följande matris med siffror: **9, 10, 11, 12**.

* **[!UICONTROL Forced update hours:]** Den här inställningen ser till att en Data warehouse-uppdatering automatiskt börjar i ditt konto *under timmarna* du har angett. Precis som med utbrottstimmar är dessa också inom utbildning. Om du till exempel vill att uppdateringarna för Data warehouse ska börja automatiskt vid **midnatt** och **middag** EST, du bör skriva följande matris med siffror: **0, 12**.

* **[!UICONTROL Send email summaries if the data has not updated yet:]** Det här alternativet hanterar situationer när en e-postsammanfattning är schemalagd att skickas *innan uppgifterna i någon av rapporterna* har uppdaterats. Om du väljer **Nej** hoppar ditt konto över att skicka e-postmeddelandet vid den schemalagda tidpunkten. I stället skickar ditt konto det när dina data har uppdaterats. Om du väljer **[!UICONTROL Yes]**, ditt konto skickar e-postmeddelandet, innehåller ett meddelande som förklarar att data är inaktuella och skickar ett till e-postmeddelande när dina data har uppdaterats.

* **[!UICONTROL Enable data updates:]** Det här alternativet ser till att datauppdateringar körs på ditt konto. Om du ändrar inställningen till **[!UICONTROL No]** stoppas datasynkningar och kolumnberäkningar i ditt konto.

>[!NOTE]
>
>Se till att markera **[!UICONTROL Save Customizations]** när du har gjort några ändringar.
