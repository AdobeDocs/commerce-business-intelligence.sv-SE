---
title: Ansluta MySQL via SSH-tunneln
description: Lär dig hur du ansluter MySQL via SSH-tunneln.
exl-id: 6b691a6a-9542-4e47-9b1d-d6d3c3dac357
source-git-commit: 8de036e2717aedef95a8bb908898fd9b9bc9c3fa
workflow-type: tm+mt
source-wordcount: '644'
ht-degree: 0%

---

# Anslut `MySQL` via `SSH Tunnel`

* [Hämta [!DNL MBI] publik nyckel](#retrieve)
* [Tillåt åtkomst till [!DNL MBI] IP-adress](#allowlist)
* [Skapa en Linux](#linux)
* [Skapa en MySQL-användare för [!DNL MBI]](#mysql)
* [Ange anslutningen och användarinformationen i [!DNL MBI]](#finish)

## GÅ TILL

* `MySQL via SSH tunnel`
* [&quot;MySQL&quot;](../integrations/mysql-via-a-direct-connection.md)
* [&quot;MySQL&quot;](../integrations/mysql-via-cpanel.md)

Koppla samman `MySQL` databas till [!DNL MBI] via `SSH tunnel`måste du (eller ditt team, om du inte är tekniker) göra några saker:

1. Hämta [!DNL MBI] `public key`
1. Tillåt åtkomst till [!DNL MBI] `IP address`
1. Skapa en `Linux` användare för [!DNL MBI]
1. Skapa en `MySQL` användare för [!DNL MBI]
1. Ange anslutningen och användarinformationen i [!DNL MBI]

Kom igång.

## Hämtar [!DNL MBI] publik nyckel {#retrieve}

The `public key` används för att auktorisera [!DNL MBI] `Linux` användare. I nästa avsnitt skapar du användaren och importerar nyckeln.

1. Gå till **[!UICONTROL Manage Data** > **Connections]** och klicka **[!UICONTROL Add New Data Source]**.
1. Klicka på `MySQL` ikon.
1. Efter `MySQL credentials` öppnas, ange `Encrypted` växla till `Yes`. Då visas SSH-konfigurationsformuläret.
1. The `public key` finns under det här formuläret.

Lämna den här sidan öppen genom hela självstudiekursen - du behöver den i nästa avsnitt och i slutet.

Så här navigerar du om du är lite vilse [!DNL MBI] för att hämta nyckeln:

![](../../../assets/MySQL_SSH.gif)<!--{: width="770"}-->

## Tillåt åtkomst till [!DNL MBI] IP-adress {#allowlist}

För att anslutningen ska lyckas måste du konfigurera brandväggen så att den tillåter åtkomst från dina IP-adresser. De är `54.88.76.97` och `34.250.211.151` men de är också på `MySQL credentials` sida. Ser du den blå lådan i GIF ovan? Så ja!

## Skapa en `Linux` användare för [!DNL MBI] {#linux}

Detta kan vara en produktionsmaskin eller en sekundär maskin, förutsatt att den innehåller realtidsdata (eller ofta uppdaterade). Du kan [begränsa den här användaren](../../../administrator/account-management/restrict-db-access.md) på vilket sätt du vill, förutsatt att du behåller rätten att ansluta till `MySQL` server.

1. Om du vill lägga till den nya användaren kör du följande kommandon som rot på din `Linux` server:

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. Kom ihåg `public key` hämtas du i första avsnittet? Om du vill vara säker på att användaren har åtkomst till databasen måste du importera nyckeln till `authorized\_keys`.

   Kopiera hela nyckeln till `authorized\_keys` på följande sätt:

```bash
        touch /home/rjmetric/.ssh/authorized_keys
        "<PASTE KEY HERE>" >> /home/rjmetric/.ssh/authorized_keys
```

1. Slutför skapandet av användaren genom att ändra behörigheterna för `/home/rjmetric` katalog som ger åtkomst via `SSH`:

```bash
        chown -R rjmetric:rjmetric /home/rjmetric
        chmod -R 700 /home/rjmetric/.ssh
        chmod 400 /home/rjmetric/.ssh/authorized_keys
```

>[!IMPORTANT]
>
>Om `sshd\_config` filen som är associerad med servern är inte inställd på standardalternativet, endast vissa användare har serveråtkomst - detta förhindrar att anslutningen till [!DNL MBI]. I dessa fall måste du köra ett kommando som `AllowUsers` för att `rjmetric` användaråtkomst till servern.

## Skapa en `MySQL` användare för [!DNL MBI] {#mysql}

Din organisation kan kräva en annan process, men det enklaste sättet att skapa den här användaren är att köra följande fråga när användaren är inloggad `MySQL` som en användare med behörighet att bevilja behörigheter:

```sql
    GRANT SELECT ON *.* TO 'rjmetric'@'localhost' IDENTIFIED BY '<secure password here>';
```

Ersätt `secure password here` med ett säkert lösenord, som kan skilja sig från `SSH` lösenord.

Om du vill hindra den här användaren från att komma åt data i specifika databaser, tabeller eller kolumner kan du köra GRANT-frågor som bara tillåter åtkomst till de data som du tillåter.

## Ange anslutningen och användarinformationen i [!DNL MBI] {#finish}

Om du vill slå ihop allt måste du ange anslutningen och användarinformationen i [!DNL MBI]. Gav du `MySQL credentials` öppnas sidan? Om inte, gå till **[!UICONTROL Data** > **Connections]** och klicka **[!UICONTROL Add New Data Source]** och sedan ikonen MySQL. Glöm inte att ställa in `Encrypted` växla till `Yes`.

Ange följande information på den här sidan, med början i avsnittet Databasanslutning:

* `Username`: Användarnamnet för [!DNL MBI] MySQL-användare
* `Password`: Lösenordet för [!DNL MBI] MySQL-användare
* `Port`: MySQL-port på servern (3306 som standard)
* `Host` Som standard är detta localhost. I allmänhet är det bind-adresvärdet för MySQL-servern, som är standard `127.0.0.1 (localhost)`, men kan också vara en lokal nätverksadress (till exempel `192.168.0.1`) eller serverns offentliga IP-adress.

   Värdet finns i `my.cnf` fil (finns på `/etc/my.cnf`) under raden som läser `\[mysqld\]`. Om bind-adresslinjen kommenteras ut i den filen skyddas servern från externa anslutningsförsök.

I `SSH Connection` avsnitt:

* `Remote Address`: Serverns IP-adress eller värdnamn [!DNL MBI] tunnlar in i
* `Username`: Användarnamnet för [!DNL MBI] SSH-användare (Linux®)
* `SSH Port`: SSH-port på servern (22 som standard)

Så ja! När du är klar klickar du på **[!UICONTROL Save & Test]** för att slutföra installationen.

## Relaterat:

* [Återautentisera integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=en)
