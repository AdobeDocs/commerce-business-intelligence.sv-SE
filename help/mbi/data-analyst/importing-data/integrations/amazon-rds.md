---
title: Anslut Amazon RDS
description: Lär dig hur du ansluter RDS-instansen.
exl-id: 02ad29c8-84d6-4b49-9ac1-e5f4feaa7fda
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 0%

---

# Anslut [!DNL Amazon RDS]

[!DNL Amazon Relational Database Services (RDS)] är en hanterad databastjänst som körs på databasmotorer som du antagligen redan känner till:

* [[!DNL MySQL]](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL Microsoft SQL]](../integrations/microsoft-sql-server.md)
* [[!DNL PostgreSQL]](../integrations/postgresql.md)

Stegen för att ansluta din [!DNL RDS]-instans varierar beroende på vilken typ av databas du använder och om du använder en krypterad anslutning (som en [`SSH tunnel for MySQL`](../integrations/mysql-via-ssh-tunnel.md)), men här är grunderna.

## Auktorisera [!DNL Commerce Intelligence] att komma åt din databas

På inloggningssidan (**[!UICONTROL Manage Data** > **Integrations]**) för varje databas visas en ruta som innehåller de IP-adresser som du måste auktorisera för att kunna ansluta R[!DNL RDS] till [!DNL Commerce Intelligence]: `54.88.76.97` och `34.250.211.151`. Här är en titt på sidan `MySQL credentials` där du markerade IP-adressrutan:

![](../../../assets/RDS_IP.png)

För att [!DNL Commerce Intelligence] ska kunna ansluta till din [!DNL RDS]-instans måste du lägga till de här IP-adresserna till rätt databassäkerhetsgrupp via AWS hanteringskonsol. Dessa IP-adresser kan läggas till i en befintlig grupp eller så kan du skapa en - det viktiga är att gruppen har behörighet att komma åt instansen som du vill ansluta till [!DNL Commerce Intelligence].

När du lägger till IP-adresserna för [!DNL Commerce Intelligence] måste du lägga till en `/32` i slutet av adressen för att ange för [!DNL Amazon] att det är en exakt IP-adress. Var inte orolig - AWS gränssnitt visar tydligt att detta är nödvändigt.

## Skapa en `Linux`-användare för [!DNL Commerce Intelligence] {#linux}

>[!NOTE]
>
>Det här steget krävs bara om du använder en krypterad anslutning. Instruktioner om hur du gör detta finns i konfigurationsavsnittet för den databas du använder (t.ex. MySQL). `Linux`-användaren tillåter oss att skapa en `SSH tunnel`, vilket är den säkraste metoden att skicka data via Internet.

## Skapa en databasanvändare för [!DNL Commerce Intelligence]

Detta är den del av processen där stegen varierar beroende på vilken databas du använder. Idén är densamma, men du skapar en användare för [!DNL Commerce Intelligence] som används för att komma åt din databas. Instruktioner för hur du skapar en databas [!DNL Commerce Intelligence]-användare finns i konfigurationsavsnittet för databasen som du använder.

## Ange anslutningsinformation i [!DNL Commerce Intelligence]

När du har beviljat [!DNL Commerce Intelligence] åtkomst till din instans och skapat en användare åt oss är det sista du behöver göra att ange anslutningsinformationen i [!DNL Commerce Intelligence].

Autentiseringssidorna för `MySQL`, `Microsoft SQL` och `PostgreSQL` nås via sidan `Integrations` (**[!UICONTROL Manage Data** > **Integrations]**) genom att klicka på **[!UICONTROL Add Integration]**. När listan över integreringar visas klickar du på ikonen för databasen som du använder för att gå till sidan med autentiseringsuppgifter. Om du för närvarande inte har tillgång till den integrering du behöver kontaktar du ditt Adobe-kontoteam.

Du behöver följande information för att slutföra anslutningen:

* Den offentliga adressen för RDS-instansen: Den finns i [!DNL AWS]-hanteringskonsolen.
* Den port som databasinstansen använder: Vissa databaser har en standardport, som automatiskt fyller i fältet `Port`. Den här informationen finns även i installationsdokumentationen för databasen.
* Användarnamnet och lösenordet för användaren som du skapade för [!DNL Commerce Intelligence].

Om du använder en krypterad anslutning ändrar du växlingen `Encrypted` på databasinloggningssidan till `Yes`. Här visas ett extra formulär för att konfigurera krypteringen:

![](../../../assets/sql-integration-encrypted-yes.png)


