---
title: Hantera dina kontoinställningar
description: Lär dig hur du anpassar dina kontoinställningar för din Data Warehouse.
exl-id: 847d51b1-287e-4c14-b64e-0bd9bfcccedc
role: Admin, User
feature: Accounts
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%

---

# Anpassa kontoinställningarna

>[!NOTE]
>
>Kräver [administratörsbehörighet.](../../administrator/user-management/user-management.md)

I ditt [!DNL Commerce Intelligence]-konto kan du anpassa dina kontoinställningar för din Data Warehouse. Du kommer åt dessa genom att välja ditt organisationsnamn i det övre högra hörnet på valfri skärm och sedan välja **[!UICONTROL Account Settings]** i listrutan.

* **[!UICONTROL Client Name:]** Den här inställningen visas i det övre högra hörnet av alla instrumentpaneler och på andra ställen i ditt konto. Om du vill ändra **[!UICONTROL "Vandelay Industries Co., Ltd]** till bara **[!UICONTROL "Vandelay]** är det här du ska göra det.

* **[!UICONTROL Currency:]** Det här är *standardvalutan* för alla monetära värden i ditt konto. När ett decimalvärde eller valutavärde synkroniseras med Datan Warehouse, bestämmer den här inställningen symbolen som placerats före det värdet i dina rapporter.

* **[!UICONTROL Blackout Hours:]** Den här inställningen garanterar att din Data Warehouse inte kommer åt dina anslutna databaser under de valda timmarna på dagen. Alla timmar uttrycks vid noll timmen och i EST (Eastern Standard Time). Om du till exempel inte vill att din produktionsdatabas ska vara tillgänglig mellan klockan 9.00 EST och 1:00 EST, skriver du följande matris med siffror: **9, 10, 11, 12**.

* **[!UICONTROL Forced update hours:]** Den här inställningen ser till att en Data Warehouse uppdateras automatiskt på ditt konto *under de timmar* du har angett. Precis som med utbrottstimmar är dessa också inom utbildning. Om du till exempel vill att Datan Warehouse ska uppdateras automatiskt vid **midnatt** och **förmiddag** EST, skriver du följande siffermatris: **0, 12**.

* **[!UICONTROL Send email summaries if the data has not updated yet:]** Det här alternativet hanterar situationer när en e-postsammanfattning är schemalagd att skicka *innan data i någon av dess rapporter* uppdateras. Om du väljer **Nej** hoppar ditt konto över att skicka e-postmeddelandet vid den schemalagda tidpunkten. I stället skickar ditt konto det när dina data har uppdaterats. Om du väljer **[!UICONTROL Yes]** skickar ditt konto e-postmeddelandet, ett meddelande som förklarar att data är inaktuella och ett e-postmeddelande skickas när dina data har uppdaterats.

* **[!UICONTROL Enable data updates:]** Det här alternativet ser till att datauppdateringar körs på ditt konto. Om du ändrar inställningen till **[!UICONTROL No]** avbryts datasynkronisering och kolumnberäkningar i ditt konto.

>[!NOTE]
>
>Välj **[!UICONTROL Save Customizations]** när du har gjort några ändringar.
