---
title: Anslut [!DNL MongoDB]  via SSH-tunneln
description: Lär dig ansluta [!DNL MongoDB] via SSH-tunneln.
exl-id: 3557a8c7-c4c5-4742-ae30-125c719aca39
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 0%

---

# Anslut [!DNL MongoDB] via SSH-tunneln

Om du vill ansluta din [!DNL MongoDB]-databas till [!DNL Commerce Intelligence] via en SSH-tunnel måste du göra några saker:

1. [Hämta den offentliga nyckeln  [!DNL Commerce Intelligence] ](#retrieve)
1. [Tillåt åtkomst till  [!DNL Commerce Intelligence] IP-adressen](#allowlist)
1. [Skapa en Linux-användare för Commerce Intelligence](#linux)
1. [Skapa en [!DNL MongoDB] användare för Commerce Intelligence](#mongodb)
1. [Ange anslutningen och användarinformationen i  [!DNL Commerce Intelligence]](#finish)

>[!NOTE]
>
>På grund av installationens tekniska karaktär rekommenderar Adobe att du gör en slinga i en utvecklare för att få hjälp om du inte gjort detta tidigare.

## Hämtar den offentliga nyckeln [!DNL Commerce Intelligence] {#retrieve}

`public key` används för att auktorisera användaren [!DNL Commerce Intelligence] `Linux`. I nästa avsnitt får du hjälp med att skapa användaren och importera nycklarna.

1. Gå till **[!UICONTROL Data** > **Connections]** och klicka på **[!UICONTROL Add New Data Source]**.
1. Klicka på ikonen [!DNL MONGODB].
1. När sidan för inloggningsuppgifter [!DNL MongoDB] öppnas ändrar du `Encrypted` till `Yes`. Då visas SSH-konfigurationsformuläret.
1. `public key` finns under det här formuläret.

Lämna den här sidan öppen genom hela självstudiekursen - du behöver den i nästa avsnitt och i slutet.

Om du är lite vilse gör du så här för att navigera genom [!DNL Commerce Intelligence] för att hämta nyckeln:

![Hämtar den offentliga nyckeln för RJMetrics](../../../assets/MongoDB_Public_Key.gif)<!--{:.zoom}-->

## Tillåt åtkomst till IP-adressen [!DNL Commerce Intelligence] {#allowlist}

För att anslutningen ska lyckas måste du konfigurera brandväggen så att den tillåter åtkomst från dina IP-adresser. De är `54.88.76.97` och `34.250.211.151`, men det finns även på sidan med [!DNL MongoDB] inloggningsuppgifter:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Skapar en `Linux`-användare för [!DNL Commerce Intelligence] {#linux}

>[!IMPORTANT]
>
>Om filen `sshd_config` som är associerad med servern inte är inställd på standardalternativet har bara vissa användare serveråtkomst, vilket förhindrar att anslutningen till [!DNL Commerce Intelligence] lyckas. I dessa fall måste du köra ett kommando som `AllowUsers` för att ge `rjmetric`-användaren åtkomst till servern.

Detta kan vara en produktionsmaskin eller en sekundär maskin, förutsatt att den innehåller realtidsdata (eller ofta uppdaterade). Du kan begränsa den här användaren hur du vill så länge den behåller rätten att ansluta till servern [!DNL MongoDB].

Om du vill lägga till den nya användaren kör du följande kommandon som rot på `Linux`-servern:

```bash
    adduser rjmetric -p
    mkdir /home/rjmetric
    mkdir /home/rjmetric/.ssh
```

Kommer du ihåg `public key` som du hämtade i första avsnittet? För att användaren ska ha åtkomst till databasen måste du importera nyckeln till `authorized_keys`. Kopiera hela nyckeln till filen `authorized_keys` enligt följande:

```bash
    touch /home/rjmetric/.ssh/authorized_keys
    "< PASTE KEY HERE >" >> /home/rjmetric/.ssh/authorized_keys
```

Slutför skapandet av användaren genom att ändra behörigheterna i katalogen /home/rjmetric så att åtkomst tillåts via SSH:

```bash
    chown -R rjmetric:rjmetric /home/rjmetric
    chmod -R 700 /home/rjmetric/.ssh
```

## Skapar en [!DNL Commerce Intelligence] [!DNL MongoDB]-användare {#mongodb}

[!DNL MongoDB]-servrar har två körningslägen - [ett med auth-alternativet ](#auth) `(mongod -- auth)` och ett utan, [vilket är standard](#default). Stegen för att skapa en [!DNL MongoDB]-användare varierar beroende på vilket läge servern använder. Kontrollera läget innan du fortsätter.

### Om servern använder alternativet `Auth`: {#auth}

När du ansluter till flera databaser kan du lägga till användaren genom att logga in på [!DNL MongoDB] som en administratörsanvändare och köra följande kommandon.

>[!NOTE]
>
>Om du vill se alla tillgängliga databaser måste användaren [!DNL Commerce Intelligence] ha behörighet att köra `listDatabases.`

Det här kommandot ger [!DNL Commerce Intelligence]-användaren åtkomst `to all databases`:

```bash
    use admin
    db.createUser('rjmetric', '< secure password here >', true)
```

Använd det här kommandot om du vill ge [!DNL Commerce Intelligence]-användaren åtkomst `to a single database`:

```bash
    use < database name >
    db.createUser('rjmetric', '< secure password here >', true)
```

Detta skriver ut ett svar som ser ut så här:

```bash
    {
    "id": ObjectId("< some object id here >"),
    "user": "rjmetric",
    "readOnly": true,
    "pwd": "< some hash here >"
    }
```

### Om servern använder standardalternativet {#default}

Om servern inte använder läget `auth` är [!DNL MongoDB]-servern tillgänglig även utan användarnamn och lösenord. Du bör dock se till att `mongodb.conf`-filen `(/etc/mongodb.conf)` har följande rader - om inte, starta om servern när du har lagt till dem.

```bash
    bind_ip = 127.0.0.1
    noauth = true
```

Om du vill binda [!DNL MongoDB]-servern till en annan adress justerar du databasens värdnamn i nästa steg.

## Anslutningen och användarinformationen anges i [!DNL Commerce Intelligence] {#finish}

Du måste ange anslutning och användarinformation i [!DNL Commerce Intelligence] för att kunna slå ihop allt. Har du lämnat sidan med [!DNL MongoDB] inloggningsuppgifter öppen? Om inte går du till **[!UICONTROL Data > Connections]** och klickar på **[!UICONTROL Add New Data Source]** och sedan på ikonen [!DNL MongoDB] . Glöm inte att ändra `Encrypted` till `Yes`.

Ange följande information på den här sidan, med början i avsnittet `Database Connection`:

* `Host`: `127.0.0.1`
* `Username`: Användarnamnet [!DNL Commerce Intelligence] [!DNL MongoDB] (ska vara `rjmetric`)
* `Password`: Lösenordet [!DNL Commerce Intelligence] [!DNL MongoDB]
* `Port`: MongoDB-porten på servern (`27017` som standard)
* `Database Name` (Valfritt): Om du bara tillåter åtkomst till en databas anger du namnet på den databasen här.

Under avsnittet `SSH Connection`:

* `Remote Address`: IP-adressen eller värdnamnet för den server som du ska SSH till
* `Username`: [!DNL Commerce Intelligence] Linux (SSH)-användarnamn (ska vara jmetriskt)
* `SSH Port`: SSH-porten på servern (22 som standard)

När du är klar klickar du på **[!UICONTROL Save Test]** för att slutföra konfigurationen.

### Relaterad

* [Återautentiserar integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=sv-SE)
