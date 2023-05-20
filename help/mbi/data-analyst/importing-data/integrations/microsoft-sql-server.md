---
title: Anslut Microsoft SQL Server
description: Lär dig hur du ansluter Microsoft SQL-databasen till [!DNL Commerce Intelligence] i fyra steg.
exl-id: 7f49d1dc-8fbb-4a8c-9d07-9a8195c266f5
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# Anslut [!DNL Microsoft SQL] Server

>[!NOTE]
>
>Kräver [Administratörsbehörigheter](../../../administrator/user-management/user-management.md).

![](../../../assets/MicrosoftSQLServer-logo.png)

Det här avsnittet förklarar hur du ansluter [!DNL Microsoft SQL] databas till [!DNL Commerce Intelligence] i fyra steg. Den här processen kräver viss teknisk expertis relaterad till serveranslutningar och SQL, och kan kräva support från utvecklare i teamet.

[!DNL Commerce Intelligence] stöder [!DNL Amazon RDS], [!DNL EC2], [!DNL Microsoft SQL Azure]och de flesta andra molnserverleverantörer. Om du har en fråga om just din värd, [skicka ett supportärende](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) ber oss att lämna denna information.

Systemet måste köra SELECT-frågor i databasen. Detta görs först för att få en ögonblicksbild av databasstrukturen och sedan regelbundet övertid för att hålla data uppdaterade. Uppdateringarna är stegvisa och Adobe begränsar uppdateringsfrekvensen och uppdateringstiden för att förhindra oönskad belastning på servern.

Det bästa sättet att göra detta är att ansluta till din databasserver via TCP/IP. Skapa en användare åt oss som bara kan köra SELECT-frågor (och, om du vill, bara kan välja data från de tabeller du anger). Detta måste göras för alla dina servrar som du ansluter till [!DNL Commerce Intelligence].

## Ansluter `Microsoft SQL` till [!DNL Commerce Intelligence]:

1. Kontrollera att servern tillåter anslutningar över TCP/IP och autentisering i blandat läge.

1. Kontrollera att brandväggen tillåter att serverns dedikerade IP-adress ansluts.

   Du hittar IP-adressen som används för att ansluta till servern i anslutningsavsnittet i `Settings` sidan.

1. Skapa en användare som ska användas för att logga in på databasservern. Du har två alternativ; antingen via `UI` eller via en `query`:
   * `UI`
   * [`Query`](http://sqlserverplanet.com/security/add-user) (andra exemplet)

1. Ange serverns IP-adress, användarnamn och lösenord i [!DNL Commerce Intelligence] enligt **[!UICONTROL Manage Data** > **Connections]**.

   ![](../../../assets/manage-data-connections.png)

1. Klicka **[!UICONTROL Add a Data Source]**.

1. Välj för att ansluta en `Microsoft SQL` databasen och ange dina inloggningsuppgifter i fälten på den nya `Connections` sidan.

   Om du använder `Windows Azure`, du måste även ange ett databasnamn.
