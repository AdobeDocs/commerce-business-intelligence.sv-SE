---
title: Anslut Microsoft SQL Server
description: Lär dig hur du ansluter din Microsoft SQL-databas till [!DNL Commerce Intelligence] i en fyrstegsprocess.
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

I det här avsnittet beskrivs hur du ansluter [!DNL Microsoft SQL] databas till [!DNL Commerce Intelligence] i en fyrstegsprocess. Den här processen kräver viss teknisk expertis relaterad till serveranslutningar och SQL, och kan kräva stöd från utvecklare i ditt team.

[!DNL Commerce Intelligence] supports [!DNL Amazon RDS], [!DNL EC2], [!DNL Microsoft SQL Azure]och de flesta andra molnserverleverantörer. Om du har en fråga om din värddator [skicka en supportanmälan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) be oss att lämna dessa uppgifter.

Systemet måste köra SELECT-frågor i din databas. Detta görs först för att få en ögonblicksbild av databasstrukturen och sedan regelbundet övertid för att hålla dina data uppdaterade. Dina uppdateringar är stegvisa och Adobe begränsar uppdateringsfrekvens och -tid för att förhindra oönskad belastning på servern.

Det bästa sättet är att ansluta till databasservern via TCP/IP. Skapa en användare för oss som bara kan köra SELECT-frågor (och, om du vill, bara kan välja data från de tabeller du anger). Detta måste göras för varje server som du ansluter till [!DNL Commerce Intelligence].

## Ansluter `Microsoft SQL` till [!DNL Commerce Intelligence]:

1. Kontrollera att servern tillåter anslutningar över TCP/IP och autentisering i blandat läge.

1. Kontrollera att brandväggen tillåter att serverns dedikerade IP-adress kan anslutas.

   Du kan hitta den IP-adress som används för att ansluta till servern under Anslutningar i ditt `Settings` sida.

1. Skapa en användare som du kan använda för att logga in på databasservern. Du har två alternativ: antingen via `UI` eller via `query`:
   * `UI`
   * [`Query`](http://sqlserverplanet.com/security/add-user) (andra exemplet)

1. Ange serverns IP-adress, användarnamn och lösenord i [!DNL Commerce Intelligence] under **[!UICONTROL Manage Data** > **Connections]**.

   ![](../../../assets/manage-data-connections.png)

1. Klicka **[!UICONTROL Add a Data Source]**.

1. Välj om du vill ansluta en `Microsoft SQL` och ange dina uppgifter i fälten på den nya `Connections` sida.

   Om du använder `Windows Azure`måste du även ange ett databasnamn.
