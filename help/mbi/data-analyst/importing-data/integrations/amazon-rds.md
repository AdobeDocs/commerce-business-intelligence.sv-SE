---
title: Anslut Amazon RDS
description: Lär dig hur du ansluter RDS-instansen.
exl-id: 02ad29c8-84d6-4b49-9ac1-e5f4feaa7fda
source-git-commit: 6f018ab220f2ae573cbc9016f9efb83c27a254be
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---

# Anslut Amazon RDS

Amazon Relational Database Services (RDS) är en hanterad databastjänst som körs på databasmotorer som du antagligen redan känner till - [[!DNL MySQL]](../integrations/mysql-via-a-direct-connection.md), [[!DNL Microsoft SQL]](../integrations/microsoft-sql-server.md)och [[!DNL PostgreSQ]](../integrations/postgresql.md).

Hur du ansluter RDS-instansen varierar något beroende på vilken typ av databas du använder (använd länkarna ovan för detaljerade anvisningar för varje databas) och om du använder en krypterad anslutning (som en [`SSH tunnel for MySQL`](../integrations/mysql-via-ssh-tunnel.md)), men här är grunderna:

## Auktorisera [!DNL MBI] för att få åtkomst till din databas

På inloggningssidan (**[!UICONTROL Manage Data** > **Integrations]**) för varje databas visas en ruta med de IP-adresser som du måste godkänna för att kunna ansluta RDS till MBI: `54.88.76.97` och `34.250.211.151`. Här är en titt på `MySQL credentials` sidan där vi markerade IP-adressrutan:

![](../../../assets/RDS_IP.png)

För [!DNL MBI] för att kunna ansluta till din RDS-instans måste du lägga till de här IP-adresserna till rätt databassäkerhetsgrupp via AWS hanteringskonsol. Dessa IP-adresser kan läggas till i en befintlig grupp eller så kan du skapa en ny. Det viktiga är att gruppen har behörighet att komma åt instansen som du vill ansluta till [!DNL MBI].

När du lägger till [!DNL MBI] IP-adresser måste du lägga till en `/32` till slutet av adressen för att ange för Amazon att det är en exakt IP-adress. Var inte orolig. AWS gränssnitt klargör att detta krävs.

## Skapa en `Linux` användare för [!DNL MBI] {#linux}

>[!NOTE]
>
>Det här steget krävs bara om du använder en krypterad anslutning. Instruktioner om hur du gör detta finns i artikeln setup för databasen som du använder (t.ex.: MySQL). The `Linux` kan vi skapa en `SSH tunnel`, som är det säkraste sättet att skicka data via Internet.

## Skapa en databasanvändare för MBI

Detta är den del av processen där stegen varierar beroende på vilken databas du använder. Idén är dock densamma: du skapar en användare för [!DNL MBI] som kommer att användas för att komma åt din databas. Instruktioner för hur du skapar en databas [!DNL MBI] -användaren finns i inställningsartikeln för den databas du använder.

## Ange anslutningsinformation i MBI

När du har beviljat [!DNL MBI] åtkomst till din instans och skapade en användare åt oss. Det sista du behöver göra är att ange anslutningsinformationen i [!DNL MBI].

Autentiseringssidor för `MySQL`, `Microsoft SQL`och `PostgreSQL` öppnas via `Integrations` sida (**[!UICONTROL Manage Data** > **Integrations]**) genom att klicka på **[!UICONTROL Add Integration]**. När listan över integreringar visas klickar du på ikonen för databasen som du använder för att gå till sidan med autentiseringsuppgifter. Om du för närvarande inte har tillgång till den integrering du behöver kontaktar du ditt Adobe-kontoteam.

Vi behöver följande information för att slutföra anslutningen:

* Den offentliga adressen för din RDS-instans: Detta finns i AWS hanteringskonsol.
* Den port som databasinstansen använder: Vissa databaser har en standardport som automatiskt fyller i `Port` fält. Den här informationen finns också i vår installationsdokumentation för databasen.
* Användarnamnet och lösenordet för användaren som du skapade för [!DNL MBI].

Om du använder en krypterad anslutning ändrar du `Encrypted` växla till `Yes`. Då visas ytterligare ett formulär för kryptering:

![](../../../assets/sql-integration-encrypted-yes.png)

Det där är allt som finns för det! Anslutningen av RDS-instansen är klar.
