---
title: Anslut MySQL via cPanel
description: Lär dig ansluta MySQL via cPanel.
exl-id: 90b0a0b0-8c6b-4144-95b4-f588f18616c7
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '358'
ht-degree: 0%

---

# Anslut [!DNL MySQL] via [!DNL cPanel]

* [Skapa en  [!DNL Commerce Intelligence] [!DNL MySQL]-användare i  [!DNL cPanel]](#cpanel)
* [Ange anslutning och användarinformation i  [!DNL Commerce Intelligence]](#finish)

## Gå till

* [[!DNL MySQL] via SSH-tunneln](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL] via direktanslutning](../integrations/mysql-via-a-direct-connection.md)

>[!IMPORTANT]
>
>[!DNL Adobe] rekommenderar att du använder SSH eller någon annan form av kryptering för att skydda dina data! Om detta inte är ett alternativ kan du fortfarande ansluta [!DNL Commerce Intelligence] direkt till databasen med hjälp av instruktionerna i det här avsnittet.

I det här avsnittet beskrivs hur du ansluter din [!DNL MySQL]-databas direkt till [!DNL Commerce Intelligence] med [!DNL cPanel]. Den här processen kan även användas för att ansluta [!DNL Adobe Commerce] och andra MySQL-baserade e-handelsdatabaser till [!DNL Commerce Intelligence].

1. Skapa en [!DNL Commerce Intelligence] [!DNL MySQL]-användare i [!DNL cPanel]
1. Ange anslutning och användarinformation i [!DNL Commerce Intelligence]

Kom igång.

## Skapar en [!DNL Commerce Intelligence] [!DNL MySQL]-användare i [!DNL cPanel] {#cpanel}

1. Logga in på [!DNL cPanel] via din värdleverantör.
1. Klicka på **[!UICONTROL [!DNL MySQL] Databases]** i avsnittet `Database`.
1. Bläddra ned till avsnittet `Add New User` och skapa en användare för [!DNL Commerce Intelligence]:

   ![](../../../assets/create-mbi-mysql-user-cpanel.png)

1. Klicka på **[!UICONTROL Create User]**.
1. Nu när du har skapat användaren måste du koppla den till en databas. Gå tillbaka till avsnittet `Add New User` - se inställningarna för `Add User to Database?` Det behöver du.
1. I listrutan `User` i det här avsnittet väljer du den användare du skapade.
1. I listrutan `Database` i det här avsnittet väljer du den databas som du vill ansluta till [!DNL Commerce Intelligence].
1. Klicka på **[!UICONTROL Add]**.
1. När checklistan över behörigheter visas markerar du kryssrutan bredvid `SELECT` - det här är allt som [!DNL Commerce Intelligence] behöver för att ansluta till databasen.

## Anslutningen och användarinformationen anges i [!DNL Commerce Intelligence] {#finish}

Du måste ange anslutning och användarinformation i [!DNL Commerce Intelligence] för att kunna slå ihop allt. Har du lämnat sidan med [!DNL MySQL] inloggningsuppgifter öppen? Om inte går du till **[!UICONTROL Manage Data** > **Connections]** och klickar på **[!UICONTROL Add New Data Source]** och sedan på ikonen [!DNL MySQL] .

Ange följande information på den här sidan i avsnittet `Database Connection`:

* `Username`: Användarnamnet för användaren [!DNL Commerce Intelligence] [!DNL MySQL]
* `Password`: Lösenordet för användaren [!DNL Commerce Intelligence] [!DNL MySQL]
* `Port`: MySQL-port på servern (`3306` som standard)
* `Host`: Den offentliga adressen för `MySQL` server [!DNL Commerce Intelligence] ansluter till. Det här är vanligtvis den URL som du använder för att logga in på `[!DNL cPanel]`.

Om du använder en [`SSH tunnel`](../integrations/mysql-via-ssh-tunnel.md) måste du ange krypteringsinformationen. Ställ in `Encrypted`-växeln på `Yes` för att visa formuläret.

* `Connection Type`: Ange det här till `SSH Tunnel`
* `Remote Address`: IP-adressen eller värdnamnet för servern [!DNL Commerce Intelligence] tunnlas till
* `Username`: Användarnamnet för användaren [!DNL Commerce Intelligence] `SSH (Linux)`, se [instruktioner](../../../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) om hur du gör detta, om du inte redan gjort det)
* `SSH Port`: SSH-port på servern (`22` som standard)

När du är klar klickar du på **[!UICONTROL Save & Test]** för att slutföra konfigurationen.

## Relaterat:

* [Återautentiserar integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
