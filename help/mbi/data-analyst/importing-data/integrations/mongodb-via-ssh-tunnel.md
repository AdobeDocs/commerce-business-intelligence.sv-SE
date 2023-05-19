---
title: Anslut [!DNL MongoDB] via SSH-tunnel
description: Lär dig ansluta [!DNL MongoDB] via SSH-tunneln.
exl-id: 3557a8c7-c4c5-4742-ae30-125c719aca39
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 0%

---

# Anslut [!DNL MongoDB] via SSH-tunneln

Koppla samman [!DNL MongoDB] databas till [!DNL Commerce Intelligence] via en SSH-tunnel måste du göra några saker:

1. [Hämta [!DNL Commerce Intelligence] publik nyckel](#retrieve)
1. [Tillåt åtkomst till [!DNL Commerce Intelligence] IP-adress](#allowlist)
1. [Skapa en Linux-användare för Commerce Intelligence](#linux)
1. [Skapa en [!DNL MongoDB] användare för Commerce Intelligence](#mongodb)
1. [Ange anslutningen och användarinformationen i [!DNL Commerce Intelligence]](#finish)

>[!NOTE]
>
>På grund av installationens tekniska karaktär rekommenderar Adobe att du gör en slinga i en utvecklare för att få hjälp om du inte gjort detta tidigare.

## Hämtar [!DNL Commerce Intelligence] publik nyckel {#retrieve}

The `public key` används för att auktorisera [!DNL Commerce Intelligence] `Linux` användare. I nästa avsnitt får du hjälp med att skapa användaren och importera nycklarna.

1. Gå till **[!UICONTROL Data** > **Connections]** och klicka **[!UICONTROL Add New Data Source]**.
1. Klicka på [!DNL MONGODB] ikon.
1. Efter [!DNL MongoDB] inloggningssidan öppnas, ändra `Encrypted` växla till `Yes`. Då visas SSH-konfigurationsformuläret.
1. The `public key` finns under det här formuläret.

Lämna den här sidan öppen genom hela självstudiekursen - du behöver den i nästa avsnitt och i slutet.

Om du är lite vilse gör du så här [!DNL Commerce Intelligence] för att hämta nyckeln:

![Hämta den offentliga nyckeln för RJMetrics](../../../assets/MongoDB_Public_Key.gif)<!--{:.zoom}-->

## Tillåt åtkomst till [!DNL Commerce Intelligence] IP-adress {#allowlist}

För att anslutningen ska lyckas måste du konfigurera brandväggen så att den tillåter åtkomst från dina IP-adresser. De är `54.88.76.97` och `34.250.211.151`, men det finns också på [!DNL MongoDB] inloggningssida:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Skapa en `Linux` användare för [!DNL Commerce Intelligence] {#linux}

>[!IMPORTANT]
>
>Om `sshd_config` filen som är associerad med servern är inte inställd på standardalternativet, endast vissa användare har serveråtkomst - detta förhindrar att anslutningen till [!DNL Commerce Intelligence]. I dessa fall måste du köra ett kommando som `AllowUsers` för att `rjmetric` användaråtkomst till servern.

Detta kan vara en produktionsmaskin eller en sekundär maskin, förutsatt att den innehåller realtidsdata (eller ofta uppdaterade). Du kan begränsa den här användaren hur du vill så länge den behåller rätten att ansluta till [!DNL MongoDB] server.

Om du vill lägga till den nya användaren kör du följande kommandon som rot på din `Linux` server:

```bash
    adduser rjmetric -p
    mkdir /home/rjmetric
    mkdir /home/rjmetric/.ssh
```

Kom ihåg `public key` hämtas du i första avsnittet? Om du vill vara säker på att användaren har åtkomst till databasen måste du importera nyckeln till `authorized_keys`. Kopiera hela nyckeln till `authorized_keys` på följande sätt:

```bash
    touch /home/rjmetric/.ssh/authorized_keys
    "< PASTE KEY HERE >" >> /home/rjmetric/.ssh/authorized_keys
```

Slutför skapandet av användaren genom att ändra behörigheterna i katalogen /home/rjmetric så att åtkomst tillåts via SSH:

```bash
    chown -R rjmetric:rjmetric /home/rjmetric
    chmod -R 700 /home/rjmetric/.ssh
```

## Skapa en [!DNL Commerce Intelligence] [!DNL MongoDB] användare {#mongodb}

[!DNL MongoDB] servrar har två körningslägen - [en med alternativet &quot;auth&quot;](#auth) `(mongod -- auth)` och en utan [som är standard](#default). Stegen för att skapa en [!DNL MongoDB] användaren varierar beroende på vilket läge servern använder. Kontrollera läget innan du fortsätter.

### Om servern använder `Auth` Alternativ: {#auth}

När du ansluter till flera databaser kan du lägga till användaren genom att logga in [!DNL MongoDB] som administratör och kör följande kommandon.

>[!NOTE]
>
>Om du vill visa alla tillgängliga databaser [!DNL Commerce Intelligence] användaren kräver behörighet att köra `listDatabases.`

Det här kommandot ger [!DNL Commerce Intelligence] användaråtkomst `to all databases`:

```bash
    use admin
    db.createUser('rjmetric', '< secure password here >', true)
```

Använd det här kommandot för att ge [!DNL Commerce Intelligence] användaråtkomst `to a single database`:

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

Om servern inte används `auth` läge, ditt [!DNL MongoDB] -servern är tillgänglig även utan användarnamn och lösenord. Du bör dock se till att `mongodb.conf` fil `(/etc/mongodb.conf)` har följande rader - om inte, starta om servern när du har lagt till dem.

```bash
    bind_ip = 127.0.0.1
    noauth = true
```

Så här binder du [!DNL MongoDB] till en annan adress justerar du databasens värdnamn i nästa steg.

## Ange anslutningen och användarinformationen i [!DNL Commerce Intelligence] {#finish}

Om du vill slå ihop allt måste du ange anslutningen och användarinformationen i [!DNL Commerce Intelligence]. Gav du [!DNL MongoDB] öppnas inloggningssidan? Om inte, gå till **[!UICONTROL Data > Connections]** och klicka **[!UICONTROL Add New Data Source]** och sedan [!DNL MongoDB] ikon. Glöm inte att ändra `Encrypted` växla till `Yes`.

Ange följande information på den här sidan, med början på `Database Connection` avsnitt:

* `Host`: `127.0.0.1`
* `Username`: The [!DNL Commerce Intelligence] [!DNL MongoDB] användarnamn (bör `rjmetric`)
* `Password`: The [!DNL Commerce Intelligence] [!DNL MongoDB] lösenord
* `Port`: MongoDB-port på servern (`27017` som standard)
* `Database Name` (Valfritt): Om du bara tillåter åtkomst till en databas anger du namnet på den databasen här.

Under `SSH Connection` avsnitt:

* `Remote Address`: IP-adressen eller värdnamnet för den server som du ska ansluta till
* `Username`: The [!DNL Commerce Intelligence] Linux (SSH), användarnamn (ska vara jmetriskt)
* `SSH Port`: SSH-porten på servern (22 som standard)

När du är klar klickar du på **[!UICONTROL Save Test]** för att slutföra installationen.

### Relaterad

* [Återautentisera integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
