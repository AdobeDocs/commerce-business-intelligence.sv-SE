---
title: Ansluter [!DNL MySQL] via SSH-tunneln
description: Lär dig hur du ansluter [!DNL MySQL] via SSH-tunneln.
exl-id: 6b691a6a-9542-4e47-9b1d-d6d3c3dac357
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 0%

---

# Anslut [!DNL MySQL] via [!DNL SSH Tunnel]

* [Hämta den offentliga nyckeln  [!DNL Commerce Intelligence] &#x200B;](#retrieve)
* [Tillåt åtkomst till  [!DNL Commerce Intelligence] IP-adressen](#allowlist)
* [Skapa en Linux-användare för  [!DNL Commerce Intelligence]](#linux)
* [Skapa en [!DNL MySQL] användare för [!DNL Commerce Intelligence]](#mysql)
* [Ange anslutningen och användarinformationen i  [!DNL Commerce Intelligence]](#finish)

## GÅ TILL

* [[!DNL MySQL] via &#x200B;](../integrations/mysql-via-a-direct-connection.md)
* [[!DNL MySQL] via [!DNL cPanel]](../integrations/mysql-via-cpanel.md)

Om du vill ansluta din [!DNL MySQL]-databas till [!DNL Commerce Intelligence] via en `SSH tunnel` måste du göra några saker:

1. Hämta [!DNL Commerce Intelligence] `public key`
1. Tillåt åtkomst till [!DNL Commerce Intelligence] `IP address`
1. Skapa en `Linux`-användare för [!DNL Commerce Intelligence]
1. Skapa en `MySQL`-användare för [!DNL Commerce Intelligence]
1. Ange anslutningen och användarinformationen i [!DNL Commerce Intelligence]


## Hämtar den offentliga nyckeln [!DNL Commerce Intelligence] {#retrieve}

`public key` används för att auktorisera användaren [!DNL Commerce Intelligence] `Linux`. I nästa avsnitt skapar du användaren och importerar nyckeln.

1. Gå till **[!UICONTROL Manage Data** > **Connections]** och klicka på **[!UICONTROL Add New Data Source]**.
1. Klicka på ikonen `MySQL`.
1. När sidan `MySQL credentials` öppnas anger du `Encrypted` till `Yes`. Då visas SSH-konfigurationsformuläret.
1. `public key` finns under det här formuläret.

Lämna den här sidan öppen genom hela självstudiekursen - du behöver den i nästa avsnitt och i slutet.

Så här navigerar du genom [!DNL Commerce Intelligence] för att hämta nyckeln:

![Animerad demonstration av MySQL-anslutning via SSH-tunnel](../../../assets/MySQL_SSH.gif)<!--{: width="770"}-->

## Tillåt åtkomst till IP-adressen [!DNL Commerce Intelligence] {#allowlist}

För att anslutningen ska lyckas måste du konfigurera brandväggen så att den tillåter åtkomst från dina IP-adresser. De är `54.88.76.97` och `34.250.211.151` men finns också på sidan `MySQL credentials`. Se den blå rutan i GIF ovan.

## Skapar en [!DNL Linux]-användare för [!DNL Commerce Intelligence] {#linux}

Detta kan vara en produktionsmaskin eller en sekundär maskin, förutsatt att den innehåller realtidsdata (eller ofta uppdaterade). Du kan [begränsa den här användaren](../../../administrator/account-management/restrict-db-access.md) som du vill, förutsatt att du behåller rätten att ansluta till servern `MySQL`.

1. Om du vill lägga till den nya användaren kör du följande kommandon som rot på [!DNL Linux]-servern:

```bash
        adduser rjmetric -p<password>
        mkdir /home/rjmetric
        mkdir /home/rjmetric/.ssh
```

1. Kommer du ihåg `public key` som du hämtade i första avsnittet? För att användaren ska ha åtkomst till databasen måste du importera nyckeln till `authorized\_keys`.

   Kopiera hela nyckeln till filen `authorized\_keys` enligt följande:

```bash
        touch /home/rjmetric/.ssh/authorized_keys
        "<PASTE KEY HERE>" >> /home/rjmetric/.ssh/authorized_keys
```

1. Slutför användarskapandet genom att ändra behörigheterna för katalogen `/home/rjmetric` så att åtkomst tillåts via `SSH`:

```bash
        chown -R rjmetric:rjmetric /home/rjmetric
        chmod -R 700 /home/rjmetric/.ssh
        chmod 400 /home/rjmetric/.ssh/authorized_keys
```

>[!IMPORTANT]
>
>Om filen `sshd\_config` som är associerad med servern inte är inställd på standardalternativet har bara vissa användare serveråtkomst, vilket förhindrar att anslutningen till [!DNL Commerce Intelligence] lyckas. I dessa fall måste du köra ett kommando som `AllowUsers` för att ge `rjmetric`-användaren åtkomst till servern.

## Skapar en [!DNL MySQL]-användare för [!DNL Commerce Intelligence] {#mysql}

Din organisation kan kräva en annan process, men det enklaste sättet att skapa den här användaren är att köra följande fråga när användaren är inloggad på [!DNL MySQL] som en användare med behörighet att bevilja behörigheter:

```sql
    GRANT SELECT ON *.* TO 'rjmetric'@'localhost' IDENTIFIED BY '<secure password here>';
```

Ersätt `secure password here` med ett säkert lösenord, som kan skilja sig från lösenordet för `SSH`.

Om du vill hindra den här användaren från att komma åt data i specifika databaser, tabeller eller kolumner kan du köra GRANT-frågor som bara tillåter åtkomst till de data som du tillåter.

## Anslutningen och användarinformationen anges i [!DNL Commerce Intelligence] {#finish}

Du måste ange anslutning och användarinformation i [!DNL Commerce Intelligence] för att kunna slå ihop allt. Lämnade du sidan `MySQL credentials` öppen? Om inte går du till **[!UICONTROL Data** > **Connections]** och klickar på **[!UICONTROL Add New Data Source]** och sedan på ikonen [!DNL MySQL] . Glöm inte att ställa in växeln `Encrypted` på `Yes`.

Ange följande information på den här sidan, med början i avsnittet `Database Connection`:

* `Username`: Användarnamnet för användaren [!DNL Commerce Intelligence] [!DNL MySQL]
* `Password`: Lösenordet för användaren [!DNL Commerce Intelligence] [!DNL MySQL]
* `Port`: [!DNL MySQL] port på servern (3306 som standard)
* `Host` Detta är som standard localhost. I allmänhet är det bind-adressvärdet för din [!DNL MySQL]-server, som är `127.0.0.1 (localhost)` som standard, men det kan också vara en lokal nätverksadress (till exempel `192.168.0.1`) eller serverns offentliga IP-adress.

  Värdet finns i filen `my.cnf` (som finns på `/etc/my.cnf`) under raden som läser `\[mysqld\]`. Om bind-adresslinjen kommenteras ut i den filen skyddas servern från externa anslutningsförsök.

I avsnittet `SSH Connection`:

* `Remote Address`: IP-adressen eller värdnamnet för servern [!DNL Commerce Intelligence] tunnlas till
* `Username`: Användarnamnet för användaren [!DNL Commerce Intelligence] SSH ([!DNL Linux])
* `SSH Port`: SSH-port på servern (22 som standard)

När du är klar klickar du på **[!UICONTROL Save & Test]** för att slutföra konfigurationen.

## Relaterat:

* [Återautentiserar integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=sv-SE)
