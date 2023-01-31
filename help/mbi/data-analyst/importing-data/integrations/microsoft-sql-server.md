---
title: Anslut Microsoft SQL Server
description: Lär dig hur du ansluter din Microsoft SQL-databas till [!DNL MBI] i en fyrstegsprocess.
exl-id: 7f49d1dc-8fbb-4a8c-9d07-9a8195c266f5
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 0%

---

# Anslut Microsoft SQL Server

>[!NOTE]
>
>Kräver [Administratörsbehörigheter](../../../administrator/user-management/user-management.md).

![](../../../assets/MicrosoftSQLServer-logo.png)

I den här artikeln beskrivs hur du ansluter `Microsoft SQL` databas till [!DNL MBI] i en fyrstegsprocess. Den här processen kräver viss teknisk expertis relaterad till serveranslutningar och SQL, och kan kräva stöd från utvecklare i ditt team.

Vi ger support [!DNL Amazon RDS], [!DNL EC2], [!DNL Microsoft SQL Azure]och de flesta andra molnserverleverantörer. Om du har en fråga om din värddator [skicka en supportanmälan](../../../guide-overview.md) be oss att lämna dessa uppgifter.

Systemet måste köra SELECT-frågor i din databas. Vi gör detta först för att få en ögonblicksbild av databasstrukturen och sedan regelbundet övertid för att hålla våra data uppdaterade. Våra uppdateringar är stegvisa och vi begränsar uppdateringsfrekvens och -tid för att förhindra oönskad belastning på servern.

Det bästa sättet är att ansluta till databasservern via TCP/IP. Skapa en användare för oss som bara kan köra SELECT-frågor (och, om du vill, bara kan välja data från de tabeller du anger). Detta måste göras för varje server som du ska ansluta till [!DNL MBI].

## Ansluter `Microsoft SQL` till [!DNL MBI]:

1. Kontrollera att servern tillåter anslutningar via TCP/IP och autentisering i blandat läge.

1. Kontrollera att din brandvägg tillåter att serverns dedikerade IP-adress ansluter.

   Du hittar IP-adressen som vi kommer att använda för att ansluta till servern under Anslutningar i din `Settings` sida.

1. Skapa en användare som vi ska använda för att logga in på databasservern.  Du har två alternativ: antingen via `UI` eller via `query`:
   * `UI`
   * [`Query`](http://sqlserverplanet.com/security/add-user) (andra exemplet)

1. Ange serverns IP-adress, användarnamn och lösenord i [!DNL MBI] under **[!UICONTROL Manage Data** > **Connections]**.

   ![](../../../assets/manage-data-connections.png)

1. Klicka **[!UICONTROL Add a Data Source]**.

1. Välj om du vill ansluta en `Microsoft SQL` och ange dina uppgifter i fälten på den nya `Connections` sida.

   Om du använder `Windows Azure`måste du även ange ett databasnamn.
