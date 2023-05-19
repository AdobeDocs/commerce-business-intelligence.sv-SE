---
title: Datamigreringstjänster
description: Lär dig allt du behöver för att skicka in en begäran och komma igång med migreringen.
exl-id: 105cd003-98ef-4358-80b9-b3190c2c57b7
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 0%

---

# Datamigrering

Att migrera till ett nytt databasschema, en ny server eller en rapportdatabas behöver inte vara stressigt. The [[!DNL Adobe] Tjänstteam](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) erbjuder migreringshjälp.

För att övergången ska bli så smidig som möjligt bör du vara så detaljerad som möjligt när du skickar in din migreringsbegäran. Det här avsnittet innehåller allt du behöver för att skicka en begäran och komma igång med migreringen. Om du ger oss en heltäckande bild av dina behov kan du garantera att projektet har rätt omfattning och att uppskattningen är korrekt.

## Komma igång {#started}

Innan du börjar måste du känna till svaren på följande frågor:

* **Finns den nya databasen på en ny server?** Innan du skickar en begäran ska du uppdatera inställningarna för din dataanslutning under **[!UICONTROL Manage Data** > **Connections]**. Om du behöver en ny information om hur du gör det går du till [`Integrations`](../integrations/integrations.md) och hitta instruktionerna för den typ av databas du använder.

* **Finns alla historiska data i den nya databasen eller behöver de migreras?** Du kan konsolidera historiska och nya data under migreringsprocessen. Meddela oss i din begäran även om du inte behöver någon konsolidering.

När du har svaren på ovanstående behöver du veta vilken typ av migrering du har. Har den nya databasen [`same`](#sameschema) schema, eller kommer det att ha [`different`](#newschema) schema? I diskussionerna nedan hittar du detaljerade anvisningar för varje migreringstyp.

## Migrera till en ny databas med samma schema {#sameschema}

När du skickar begäran, meddela oss att databasschemat inte ändras och att anslutningen redan har konfigurerats i [!DNL Adobe Commerce Intelligence].

Om databasen har ett nytt namn inkluderar du det i begäran så att dina instrumentpaneler kan migreras på rätt sätt.

Om databasnamnet inte ändras är migreringen klar. Instrumentpaneler och rapporter uppdateras när nästa fullständiga uppdatering har slutförts.

## Migrera till en ny databas med ett annat schema {#newschema}

>[!IMPORTANT]
>
>Om vissa datakolumner inte har motsvarande kolumner i den nya databasen finns det en risk för att vissa analyser går förlorade.

För att den här typen av migrering ska kunna slutföras måste befintliga datakolumner matchas med motsvarande data i den nya databasen. Detta är inte obligatoriskt, men om vi utför matchningen hjälper det till att snabba upp omvändningstiden för din begäran och sänka migreringspriset.

Om du känner dig bekväm med att utföra matchningen själv följer du dessa instruktioner och bifogar det färdiga kalkylbladet till din begäran:

1. Granska alla tabeller och kolumner som synkroniseras med Data warehouse (**[!UICONTROL Manage Data** > **Data Warehouse]**).

1. I ett kalkylblad skapar du en flik för varje tabell som ska migreras till den nya databasen.

1. Skapa en kolumn för alla befintliga kolumner som behöver migreras på varje flik. Adobe rekommenderar att du ger den ett namn som `Existing column name`.

1. Du måste också skapa en ny kolumn för kolumnmotsvarigheterna i den nya databasen på varje flik i kalkylbladet. Adobe rekommenderar att du ger kolumnen ett namn som `New column name`.

1. Ange de befintliga kolumnerna och deras motsvarigheter. Om en befintlig kolumn inte har någon ny motsvarighet anger du `N/A`.

   Om det finns ett nytt sätt att beräkna samma information i den nya databasen anger du den i dialogrutan [`New column name`] kolumn.

Här följer ett exempel:

![](../../../assets/Migration_Spreadsheet.png)

>[!NOTE]
>
>Om vissa datakolumner inte har motsvarande kolumner i den nya databasen finns det en risk för att vissa analyser går förlorade.

## Hur skickar jag en förfrågan? {#submitreq}

Du kan kontakta oss via [skicka en supportförfrågan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

Om du följde stegen i föregående avsnitt för att skapa ett kalkylblad som matchar kolumner, glöm inte att bifoga det.

## Vad kommer härnäst? {#wrapup}

För att fastställa projektets omfattning krävs ett visst samarbete mellan dig och analytikerna från det Commerce Services-team som utför migreringen. Förändringarnas komplexitet och hur lyhörd ni och analytikerna är påverkar direkt hur lång tid migreringen kan ta. När du har spikat ned detaljerna kommer en tidslinje att upprättas och skickas till dig med en arbetsförklaring.
