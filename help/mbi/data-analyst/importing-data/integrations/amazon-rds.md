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

Stegen för att ansluta [!DNL RDS] -instansen varierar beroende på vilken typ av databas du använder och om du använder en krypterad anslutning (som [`SSH tunnel for MySQL`](../integrations/mysql-via-ssh-tunnel.md)), men här är grunderna.

## Auktorisera [!DNL Commerce Intelligence] för att få åtkomst till din databas

På inloggningssidan (**[!UICONTROL Manage Data** > **Integrations]**) för varje databas visas en ruta med de IP-adresser som du måste godkänna för att ansluta R[!DNL RDS] till [!DNL Commerce Intelligence]: `54.88.76.97` och `34.250.211.151`. Här är en titt på `MySQL credentials` sida, där du markerade IP-adressrutan:

![](../../../assets/RDS_IP.png)

För [!DNL Commerce Intelligence] för att ansluta till [!DNL RDS] Du måste till exempel lägga till dessa IP-adresser i rätt databassäkerhetsgrupp via AWS hanteringskonsol. Dessa IP-adresser kan läggas till i en befintlig grupp eller så kan du skapa en - det viktiga är att gruppen har behörighet att komma åt instansen som du vill ansluta till [!DNL Commerce Intelligence].

När du lägger till [!DNL Commerce Intelligence] IP-adresser måste du lägga till en `/32` till slutet av adressen för att ange [!DNL Amazon] att det är en exakt IP-adress. Var inte orolig. AWS gränssnitt gör det klart att detta är nödvändigt.

## Skapa en `Linux` användare för [!DNL Commerce Intelligence] {#linux}

>[!NOTE]
>
>Det här steget krävs bara om du använder en krypterad anslutning. Instruktioner om hur du gör detta finns i konfigurationsavsnittet för den databas du använder (t.ex.: MySQL). The `Linux` kan vi skapa en `SSH tunnel`, som är det säkraste sättet att skicka data via Internet.

## Skapa en databasanvändare för [!DNL Commerce Intelligence]

Detta är den del av processen där stegen varierar beroende på vilken databas du använder. Idén är dock densamma som att du skapar en användare för [!DNL Commerce Intelligence] som används för att komma åt din databas. Instruktioner för hur du skapar en databas [!DNL Commerce Intelligence] -användaren finns i konfigurationsavsnittet för databasen som du använder.

## Ange anslutningsinformation i [!DNL Commerce Intelligence]

När du har beviljat [!DNL Commerce Intelligence] åtkomst till din instans och skapade en användare åt oss. Det sista du behöver göra är att ange anslutningsinformationen i [!DNL Commerce Intelligence].

Autentiseringssidor för `MySQL`, `Microsoft SQL`och `PostgreSQL` öppnas via `Integrations` sida (**[!UICONTROL Manage Data** > **Integrations]**) genom att klicka på **[!UICONTROL Add Integration]**. När listan över integreringar visas klickar du på ikonen för databasen som du använder för att gå till sidan med autentiseringsuppgifter. Om du för närvarande inte har tillgång till den integrering du behöver kontaktar du ditt Adobe-kontoteam.

Du behöver följande information för att slutföra anslutningen:

* Den offentliga adressen för din RDS-instans: Detta finns i [!DNL AWS] hanteringskonsol.
* Den port som databasinstansen använder: Vissa databaser har en standardport som automatiskt fyller i `Port` fält. Den här informationen finns även i installationsdokumentationen för databasen.
* Användarnamnet och lösenordet för användaren som du skapade för [!DNL Commerce Intelligence].

Om du använder en krypterad anslutning ändrar du `Encrypted` växla till `Yes`. Här visas ett extra formulär för att konfigurera krypteringen:

![](../../../assets/sql-integration-encrypted-yes.png)


