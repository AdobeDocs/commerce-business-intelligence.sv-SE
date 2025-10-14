---
title: Ansluta MySQL via en direktanslutning
description: Lär dig hur du ansluter [!DNL MongoDB] via direktanslutning.
exl-id: 53765844-c9bb-4a16-b00c-ce9672f87415
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---

# Anslut [!DNL MySQL] via direktanslutning

## I det här avsnittet

* [Tillåt åtkomst till  [!DNL Commerce Intelligence] IP-adressen](#allowlist)
* [Skapa en [!DNL MySQL] användare för [!DNL Commerce Intelligence]](#steptwo)
* [Ange anslutningsinformation i  [!DNL Commerce Intelligence]](#stepthree)

## Gå till

* [[!DNL MySQL] via &#x200B;](../integrations/mysql-via-ssh-tunnel.md)
* [[!DNL MySQL] via [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

>[!NOTE]
>
>[!DNL Adobe] rekommenderar att du använder [SSH](../integrations/mysql-via-ssh-tunnel.md) eller någon annan form av kryptering för att skydda dina data! Om detta inte är ett alternativ kan du fortfarande ansluta [!DNL Commerce Intelligence] direkt till databasen med hjälp av instruktionerna i det här avsnittet.

I det här avsnittet beskrivs hur du ansluter din [!DNL MySQL]-databas direkt till [!DNL Commerce Intelligence]. De här inställningarna kan även användas med [!DNL Adobe Commerce] eller andra e-handelsdatabaser som använder MySQL.

## Tillåt åtkomst till IP-adresserna för [!DNL Commerce Intelligence] {#allowlist}

För att anslutningen ska lyckas måste du konfigurera brandväggen så att den tillåter åtkomst från dina IP-adresser. De är `54.88.76.97` och `34.250.211.151`, men det finns även på sidan med [!DNL MySQL] inloggningsuppgifter:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Skapa en [!DNL MySQL]-användare för [!DNL Commerce Intelligence]

Det enklaste sättet att skapa en `MySQL`-användare för [!DNL Commerce Intelligence] är att köra följande fråga när du är inloggad på `MySQL` med `GRANT` behörighet. Ersätt `Commerce Intelligence IP Address` med [!DNL Commerce Intelligence]-IP-adressen och ersätt `secure password` med ett säkert lösenord som du väljer:

```sql
    GRANT SELECT ON *.* TO 'magentobi'@'<Commerce Intelligence IP address>' IDENTIFIED BY '<secure password>';
```

Om du vill hindra den här användaren från att komma åt data i specifika databaser, tabeller eller kolumner kan du i stället köra `GRANT`-frågor som bara tillåter åtkomst till de data som du tillåter.

**Kör om GRANT-frågan för alla nödvändiga IP-adresser med samma användare och lösenord.**

## Ange anslutningsinformation i Commerce Intelligence

Du måste ange anslutning och användarinformation i [!DNL Commerce Intelligence] för att kunna slå ihop allt. Har du lämnat sidan med [!DNL MySQL] inloggningsuppgifter öppen? Om inte går du till **[!UICONTROL Data** > **Connections]**, klickar på **[!UICONTROL Add New Data Source]** och sedan på ikonen [!DNL MySQL] . Glöm inte att ändra `Encrypted` till `Yes`.

Ange följande information på den här sidan, med början i avsnittet `Database Connection`:

* `Connection Nickname`: Ange ett namn för integreringen (till exempel Ecommerce Store)
* `Username`: Användarnamnet för användaren [!DNL Commerce Intelligence] [!DNL MySQL]
* `Password`: Lösenordet för användaren [!DNL Commerce Intelligence] [!DNL MySQL]
* `Port`: MySQL-port på servern (`3306` som standard)
* `Host`: Detta är som standard localhost. I allmänhet är det bind-adressvärdet för din [!DNL MySQL]-server, som är `127.0.0.1 (localhost)` som standard, men det kan också vara en lokal nätverksadress (till exempel `192.168.0.1`) eller serverns offentliga IP-adress.

  Värdet finns i filen `my.cnf` (som finns på `/etc/my.cnf`) under raden som läser `\[mysqld\]`. Om bind-adresslinjen kommenteras ut i den filen skyddas servern från externa anslutningsförsök.

När du är klar klickar du på **[!UICONTROL Save & Test]** för att slutföra konfigurationen.

## Relaterad dokumentation

* [Återautentiserar integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=sv-SE)
