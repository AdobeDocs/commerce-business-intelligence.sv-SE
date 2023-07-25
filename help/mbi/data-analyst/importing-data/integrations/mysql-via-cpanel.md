---
title: Anslut MySQL via cPanel
description: Lär dig hur du ansluter MySQL via cPanel.
exl-id: 90b0a0b0-8c6b-4144-95b4-f588f18616c7
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---

# Anslut [!DNL MySQL] via [!DNL cPanel]

* [Skapa en [!DNL Commerce Intelligence] [!DNL MySQL] användare in [!DNL cPanel]](#cpanel)
* [Ange anslutning och användarinformation i [!DNL Commerce Intelligence]](#finish)

## Gå till

* [[!DNL MySQL] via SSH-tunnel](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL] via direktanslutning](../integrations/mysql-via-a-direct-connection.md)

>[!IMPORTANT]
>
>[!DNL Adobe] rekommenderar att du använder SSH eller någon annan form av kryptering för att skydda dina data! Om detta inte är ett alternativ kan du fortfarande ansluta direkt [!DNL Commerce Intelligence] till databasen enligt instruktionerna i det här avsnittet.

I det här avsnittet beskrivs hur du kopplar samman [!DNL MySQL] databas till [!DNL Commerce Intelligence] använda [!DNL cPanel]. Den här processen kan även användas för att ansluta [!DNL Adobe Commerce] och andra MySQL-baserade e-handelsdatabaser till [!DNL Commerce Intelligence].

1. Skapa en [!DNL Commerce Intelligence] [!DNL MySQL] användare in [!DNL cPanel]
1. Ange anslutning och användarinformation i [!DNL Commerce Intelligence]

Kom igång.

## Skapa en [!DNL Commerce Intelligence] [!DNL MySQL] användare in [!DNL cPanel] {#cpanel}

1. Logga in på [!DNL cPanel] via din värdleverantör.
1. Klicka **[!UICONTROL [!DNL MySQL] Databases]**, som finns i `Database` -avsnitt.
1. Bläddra nedåt till `Add New User` och skapa en användare för [!DNL Commerce Intelligence]:

   ![](../../../assets/create-mbi-mysql-user-cpanel.png)

1. Klicka **[!UICONTROL Create User]**.
1. Nu när du har skapat användaren måste du koppla den till en databas. Gå tillbaka till `Add New User` -avsnittet - se inställningarna för `Add User to Database?` Det är vad du behöver.
1. I `User` väljer användaren som du skapade.
1. I `Database` i den här delen väljer du den databas som du vill ansluta till [!DNL Commerce Intelligence].
1. Klicka **[!UICONTROL Add]**.
1. Markera kryssrutan invid `SELECT` - det här är allt [!DNL Commerce Intelligence] måste ansluta till databasen.

## Ange anslutningen och användarinformationen i [!DNL Commerce Intelligence] {#finish}

Om du vill slå ihop allt måste du ange anslutningen och användarinformationen i [!DNL Commerce Intelligence]. Gav du [!DNL MySQL] öppnas inloggningssidan? Om inte, gå till **[!UICONTROL Manage Data** > **Connections]** och klicka **[!UICONTROL Add New Data Source]** och sedan [!DNL MySQL] ikon.

Ange följande information på den här sidan i `Database Connection` avsnitt:

* `Username`: Användarnamnet för [!DNL Commerce Intelligence] [!DNL MySQL] användare
* `Password`: Lösenordet för [!DNL Commerce Intelligence] [!DNL MySQL] användare
* `Port`: MySQL-port på servern (`3306` som standard)
* `Host`: Den offentliga adressen till `MySQL` server [!DNL Commerce Intelligence] ansluter till. Det här är vanligtvis den URL som du använder för att logga in `[!DNL cPanel]`.

Om du använder en [`SSH tunnel`](../integrations/mysql-via-ssh-tunnel.md)måste du ange krypteringsinformationen. Ange `Encrypted` växla till `Yes` för att visa formuläret.

* `Connection Type`: Ange detta till `SSH Tunnel`
* `Remote Address`: Serverns IP-adress eller värdnamn [!DNL Commerce Intelligence] tunnlar in i
* `Username`: Användarnamnet för [!DNL Commerce Intelligence] `SSH (Linux)` användare, se [instruktioner](../../../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md) om hur du ska göra detta, om du inte redan gjort det)
* `SSH Port`: SSH-port på servern (`22` som standard)

När du är klar klickar du på **[!UICONTROL Save & Test]** för att slutföra installationen.

## Relaterat:

* [Återautentisera integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
