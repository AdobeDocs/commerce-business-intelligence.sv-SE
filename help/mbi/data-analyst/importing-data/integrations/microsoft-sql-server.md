---
title: Anslut Microsoft SQL Server
description: Lär dig hur du ansluter din Microsoft SQL-databas till  [!DNL Commerce Intelligence]  i en fyrstegsprocess.
exl-id: 7f49d1dc-8fbb-4a8c-9d07-9a8195c266f5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Anslut servern [!DNL Microsoft SQL]

>[!NOTE]
>
>Kräver [administratörsbehörighet](../../../administrator/user-management/user-management.md).

![Microsoft SQL Server-logotyp](../../../assets/MicrosoftSQLServer-logo.png)

I det här avsnittet förklaras hur du ansluter din [!DNL Microsoft SQL]-databas till [!DNL Commerce Intelligence] i en fyrstegsprocess. Den här processen kräver viss teknisk expertis relaterad till serveranslutningar och SQL, och kan kräva stöd från utvecklare i ditt team.

[!DNL Commerce Intelligence] har stöd för [!DNL Amazon RDS], [!DNL EC2], [!DNL Microsoft SQL Azure] och de flesta andra molnserverleverantörer. Om du har en fråga till din värddator [skickar du en supportanmälan](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=sv-SE) och ber oss att ange den här informationen.

Systemet måste köra SELECT-frågor i din databas. Detta görs först för att få en ögonblicksbild av databasstrukturen och sedan regelbundet övertid för att hålla dina data uppdaterade. Dina uppdateringar är stegvisa och Adobe begränsar uppdateringsfrekvens och -tid för att förhindra oönskad belastning på servern.

Det bästa sättet är att ansluta till databasservern via TCP/IP. Skapa en användare för oss som bara kan köra SELECT-frågor (och, om du vill, bara kan välja data från de tabeller du anger). Detta måste göras för var och en av de servrar du ansluter till [!DNL Commerce Intelligence].

## Ansluter `Microsoft SQL` till [!DNL Commerce Intelligence]:

1. Kontrollera att servern tillåter anslutningar över TCP/IP och autentisering i blandat läge.

1. Kontrollera att brandväggen tillåter att serverns dedikerade IP-adress kan anslutas.

   Du kan hitta den IP-adress som används för att ansluta till servern i anslutningsavsnittet på `Settings`-sidan.

1. Skapa en användare som du kan använda för att logga in på databasservern. Du har två alternativ, antingen via `UI` eller via en `query`:
   * `UI`
   * [`Query`](http://sqlserverplanet.com/security/add-user) (andra exempel)

1. Ange serverns IP-adress, användarnamn och lösenord i [!DNL Commerce Intelligence] under **[!UICONTROL Manage Data** > **Connections]**.

   ![Sidan Hantera dataanslutningar med databasintegreringar](../../../assets/manage-data-connections.png)

1. Klicka på **[!UICONTROL Add a Data Source]**.

1. Välj att ansluta en `Microsoft SQL`-databas och ange dina autentiseringsuppgifter i fälten på den nya `Connections`-sidan.

   Om du använder `Windows Azure` måste du även ange ett databasnamn.
