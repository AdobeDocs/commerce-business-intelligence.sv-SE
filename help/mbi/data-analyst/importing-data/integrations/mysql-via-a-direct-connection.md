---
title: Ansluta MySQL via en direktanslutning
description: Lär dig ansluta [!DNL MongoDB] via direktanslutning.
exl-id: 53765844-c9bb-4a16-b00c-ce9672f87415
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---

# Anslut [!DNL MongoDB] via direktanslutning

## I den här artikeln

* [Tillåt åtkomst till [!DNL MBI] IP-adress](#allowlist)
* [Skapa en ](#steptwo)
* [Ange anslutningsinformation i [!DNL MBI]](#stepthree)

## Gå till

* [&quot;MySQL via SSH-tunnel`](../integrations/mysql-via-ssh-tunnel.md)
* `MySQL via direct connection`
* [&quot;MySQL via cPanel&quot;](../integrations/mysql-via-cpanel.md)

>[!NOTE]
>
>Adobe rekommenderar att du använder [SSH](../integrations/mysql-via-ssh-tunnel.md) eller någon annan form av kryptering för att skydda dina data! Om detta inte är ett alternativ kan du fortfarande ansluta direkt [!DNL MBI] till databasen enligt instruktionerna i den här artikeln.

I den här artikeln beskrivs hur du ansluter din MySQL-databas direkt till [!DNL MBI]. De här inställningarna kan även användas med Commerce eller andra e-handelsdatabaser som använder MySQL.

## Tillåt åtkomst till [!DNL MBI] IP-adresser {#allowlist}

För att anslutningen ska lyckas måste du konfigurera brandväggen så att den tillåter åtkomst från dina IP-adresser. De är `54.88.76.97` och `34.250.211.151`, men finns även på inloggningssidan för MySQL:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Skapa en MySQL-användare för [!DNL MBI]

Det enklaste sättet att skapa `MySQL` användare för [!DNL MBI] ska köra följande fråga när du loggar in `MySQL` med `GRANT` behörighet. Ersätt `MBI IP Address` med [!DNL MBI] IP-adress och ersättning `secure password` med ett säkert lösenord:

```sql
    GRANT SELECT ON *.* TO 'magentobi'@'<MBI IP address>' IDENTIFIED BY '<secure password>';
```

Om du vill hindra den här användaren från att komma åt data i specifika databaser, tabeller eller kolumner kan du köra `GRANT` frågor som bara tillåter åtkomst till de data du tillåter.

**Kör GRANT-frågan igen för alla nödvändiga IP-adresser med samma användare och lösenord.**

## Ange anslutningsinformation i MBI

Om du vill slå ihop allt måste du ange anslutningen och användarinformationen i [!DNL MBI]. Lämna sidan MySQL-autentiseringsuppgifter öppen? Om inte, gå till **[!UICONTROL Data** > **Connections]** och klicka **[!UICONTROL Add New Data Source]** och sedan ikonen MySQL. Glöm inte att ändra `Encrypted` växla till `Yes`.

Ange följande information på den här sidan, med början på `Database Connection` avsnitt:

* `Connection Nickname`: Ange ett namn för integreringen (till exempel Ecommerce Store)
* `Username`: Användarnamnet för [!DNL MBI] MySQL-användare
* `Password`: Lösenordet för [!DNL MBI] MySQL-användare
* `Port`: MySQL-port på servern (`3306` som standard)
* `Host`: Som standard är detta localhost. I allmänhet är det bind-adresvärdet för MySQL-servern, som är standard `127.0.0.1 (localhost)`, men kan också vara en lokal nätverksadress (till exempel `192.168.0.1`) eller serverns offentliga IP-adress.

   Värdet finns i `my.cnf` fil (finns på `/etc/my.cnf`) under raden som läser `\[mysqld\]`. Om bind-adresslinjen kommenteras ut i den filen skyddas servern från externa anslutningsförsök.

Så ja! När du är klar klickar du på **[!UICONTROL Save & Test]** för att slutföra installationen.

## Relaterad dokumentation

* [Återautentisera integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
