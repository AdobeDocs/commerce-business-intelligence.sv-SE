---
title: Datamigreringstjänster
description: Lär dig allt du behöver för att skicka in en begäran och komma igång med migreringen.
exl-id: 105cd003-98ef-4358-80b9-b3190c2c57b7
source-git-commit: 9974cc5c5cf89829ca522ba620b8c0c2d509610c
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 0%

---

# Datamigrering

Att migrera till ett nytt databasschema, en ny server eller en rapportdatabas behöver inte vara stressigt. Våra **[!DNL Adobe Commerce Services - Analytics]** team erbjuder migreringshjälp - vi gör allt för hårt arbete så att du inte behöver göra det.

För att övergången ska gå så smidigt som möjligt ber vi dig att vara så detaljerad som möjligt när du skickar in din migreringsbegäran. I den här artikeln finns allt du behöver för att skicka en begäran och komma igång med migreringen. Om du ger oss en heltäckande bild av dina behov kan du garantera att projektet får rätt omfattning och att uppskattningen är korrekt.

## Komma igång {#started}

Innan vi går in bör du känna till svaren på dessa frågor:

* **Finns den nya databasen på en ny server?** Innan du skickar en begäran ska du uppdatera inställningarna för din dataanslutning under **[!UICONTROL Manage Data** > **Connections]**. Om du behöver en ny information om hur du gör det går du till [`Integrations`](../integrations/integrations.md) och hitta instruktionerna för den typ av databas du använder.
* **Finns alla historiska data i den nya databasen eller behöver de migreras?** Vi kan konsolidera historiska och nya data under migreringsprocessen. Även om du inte behöver konsolidera ber vi dig att meddela oss i din begäran.

När du har fått svar på ovanstående behöver vi veta vilken typ av migrering det är: kommer den nya databasen att ha [`same`](#sameschema) schema, eller kommer det att ha [`different`](#newschema) schema? I avsnitten nedan finns detaljerade anvisningar för varje migreringstyp.

## Migrera till en ny databas med samma schema {#sameschema}

När du skickar begäran, meddela oss att databasschemat inte ändras och att anslutningen redan har konfigurerats i [!DNL MBI].

Om databasen har ett nytt namn inkluderar du det i begäran så att dina instrumentpaneler kan migreras på rätt sätt.

Om databasnamnet inte ändras är migreringen klar. Instrumentpaneler och rapporter uppdateras när nästa fullständiga uppdatering har slutförts. Vi ber dig att fortfarande kontakta oss så att vi kan ligga steget före med eventuella problem som kan uppstå till följd av migreringen.

## Migrera till en ny databas med ett annat schema {#newschema}

>[!IMPORTANT]
>
>Om vissa datakolumner inte har motsvarande kolumner i den nya databasen finns det en risk för att vissa analyser går förlorade.

För att den här typen av migrering ska kunna slutföras måste befintliga datakolumner matchas med motsvarande data i den nya databasen. Detta är inte obligatoriskt för dig, men om du utför matchningen för oss kommer det att gå snabbare att genomföra din begäran och sänka migreringspriset.

Om du känner dig bekväm med att utföra matchningen själv följer du dessa instruktioner och bifogar det färdiga kalkylbladet till din begäran:

1. Granska alla tabeller och kolumner som synkroniseras med Data warehouse (**[!UICONTROL Manage Data** > **Data Warehouse]**).
1. I ett kalkylblad skapar du en flik för varje tabell som ska migreras till den nya databasen.
1. Skapa en kolumn för alla befintliga kolumner som behöver migreras på varje flik. Vi rekommenderar att du namnger den på något sätt `Existing column name`.
1. Du måste också skapa en ny kolumn för kolumnmotsvarigheterna i den nya databasen på varje flik i kalkylbladet. Vi rekommenderar att du ger kolumnen ett namn som `New column name`.
1. Ange de befintliga kolumnerna och deras motsvarigheter. Om en befintlig kolumn inte har någon ny motsvarighet anger du bara `N/A`.

   Om det finns ett nytt sätt att beräkna samma information i den nya databasen anger du den i dialogrutan [`New column name`] kolumn.

Här följer ett exempel:

![](../../../assets/Migration_Spreadsheet.png)

>[!NOTE]
>
>Om vissa datakolumner inte har motsvarande kolumner i den nya databasen finns det en risk för att vissa analyser går förlorade.

## Hur skickar jag en förfrågan? {#submitreq}

Du kan kontakta oss via [skicka en supportförfrågan](../../../guide-overview.md).

Om du följde stegen i föregående avsnitt för att skapa kolumnmatchande kalkylblad, glöm inte att bifoga det.

## Vad kommer härnäst? {#wrapup}

Om du fastställer projektets omfattning krävs ett visst samarbete mellan dig och analytikerna från det Commerce Services-team som utför migreringen. Förändringarnas komplexitet och hur lyhörd ni och analytikerna är påverkar direkt hur lång tid migreringen kan ta. När vi har spikat detaljerna kommer en tidslinje att upprättas och skickas till dig med en arbetsförklaring.
