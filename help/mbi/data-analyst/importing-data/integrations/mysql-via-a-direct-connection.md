---
title: Ansluta MySQL via en direktanslutning
description: Lär dig ansluta [!DNL MongoDB] via direktanslutning.
exl-id: 53765844-c9bb-4a16-b00c-ce9672f87415
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# Anslut [!DNL MySQL] via direktanslutning

## I det här avsnittet

* [Tillåt åtkomst till [!DNL Commerce Intelligence] IP-adress](#allowlist)
* [Skapa en [!DNL MySQL] användare för [!DNL Commerce Intelligence]](#steptwo)
* [Ange anslutningsinformation i [!DNL Commerce Intelligence]](#stepthree)

## Gå till

* [[!DNL MySQL] via ](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL] via [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

>[!NOTE]
>
>[!DNL Adobe] rekommenderar att du använder [SSH](../integrations/mysql-via-ssh-tunnel.md) eller någon annan form av kryptering för att skydda dina data! Om detta inte är ett alternativ kan du fortfarande ansluta direkt [!DNL Commerce Intelligence] till databasen enligt instruktionerna i det här avsnittet.

I det här avsnittet beskrivs hur du kopplar samman [!DNL MySQL] databas till [!DNL Commerce Intelligence]. Dessa inställningar kan även användas med [!DNL Adobe Commerce] eller andra e-handelsdatabaser som använder MySQL.

## Tillåt åtkomst till [!DNL Commerce Intelligence] IP-adresser {#allowlist}

För att anslutningen ska lyckas måste du konfigurera brandväggen så att den tillåter åtkomst från dina IP-adresser. De är `54.88.76.97` och `34.250.211.151`, men det finns också på [!DNL MySQL] inloggningssida:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Skapa en [!DNL MySQL] användare för [!DNL Commerce Intelligence]

Det enklaste sättet att skapa `MySQL` användare för [!DNL Commerce Intelligence] ska köra följande fråga när du loggar in `MySQL` med `GRANT` behörighet. Ersätt `Commerce Intelligence IP Address` med [!DNL Commerce Intelligence] IP-adress och ersättning `secure password` med ett säkert lösenord:

```sql
    GRANT SELECT ON *.* TO 'magentobi'@'<Commerce Intelligence IP address>' IDENTIFIED BY '<secure password>';
```

Om du vill hindra den här användaren från att komma åt data i specifika databaser, tabeller eller kolumner kan du köra `GRANT` frågor som bara tillåter åtkomst till de data du tillåter.

**Kör GRANT-frågan igen för alla nödvändiga IP-adresser med samma användare och lösenord.**

## Ange anslutningsinformation i Commerce Intelligence

Om du vill slå ihop allt måste du ange anslutningen och användarinformationen i [!DNL Commerce Intelligence]. Gav du [!DNL MySQL] öppnas inloggningssidan? Om inte, gå till **[!UICONTROL Data** > **Connections]** och klicka **[!UICONTROL Add New Data Source]** klickar du på [!DNL MySQL] ikon. Glöm inte att ändra `Encrypted` växla till `Yes`.

Ange följande information på den här sidan, med början på `Database Connection` avsnitt:

* `Connection Nickname`: Ange ett namn för integreringen (till exempel Ecommerce Store)
* `Username`: Användarnamnet för [!DNL Commerce Intelligence] [!DNL MySQL] användare
* `Password`: Lösenordet för [!DNL Commerce Intelligence] [!DNL MySQL] användare
* `Port`: MySQL-port på servern (`3306` som standard)
* `Host`: Som standard är detta localhost. I allmänhet är det bind-adresvärdet för [!DNL MySQL] server, som är standard `127.0.0.1 (localhost)`, men kan också vara en lokal nätverksadress (till exempel `192.168.0.1`) eller serverns offentliga IP-adress.

  Värdet finns i `my.cnf` fil (finns på `/etc/my.cnf`) under raden som läser `\[mysqld\]`. Om bind-adresslinjen kommenteras ut i den filen skyddas servern från externa anslutningsförsök.

När du är klar klickar du på **[!UICONTROL Save & Test]** för att slutföra installationen.

## Relaterad dokumentation

* [Återautentisera integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
