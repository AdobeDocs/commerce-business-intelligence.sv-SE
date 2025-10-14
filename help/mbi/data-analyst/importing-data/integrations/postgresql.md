---
title: Connect PostgreSQL via SSH-tunneln
description: Lär dig hur du ansluter PostgreSQL-databasen till Commerce Intelligence via en SSH-tunnel.
exl-id: da610988-21c1-4f5f-b4e2-e2deb175a2aa
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---

# Anslut [!DNL PostgreSQL] via [!DNL SSH Tunnel]

Om du vill ansluta din [!DNL PostgreSQL]-databas till [!DNL Commerce Intelligence] via en `SSH tunnel` måste du göra några saker:

1. [Hämta den offentliga nyckeln  [!DNL Commerce Intelligence] &#x200B;](#retrieve)
1. [Tillåt åtkomst till  [!DNL Commerce Intelligence] IP-adressen](#allowlist)
1. [Skapa en [!DNL Linux] användare för [!DNL Commerce Intelligence]](#linux)
1. [Skapa en [!DNL PostgreSQL] användare för [!DNL Commerce Intelligence]](#postgres)
1. [Ange anslutningen och användarinformationen i  [!DNL Commerce Intelligence]](#finish)

## Hämtar [!DNL Commerce Intelligence] [!DNL public key] {#retrieve}

`public key` används för att auktorisera användaren [!DNL Commerce Intelligence] [!DNL Linux]. Nu ska du skapa användaren och importera nyckeln.

1. Gå till **[!UICONTROL Manage Data** > **Connections]** och klicka på **[!UICONTROL Add a Data Source]**.
1. Klicka på ikonen [!DNL PostgreSQL].
1. När sidan `PostgreSQL credentials` öppnas anger du `Encrypted` till `Yes`. Detta visar konfigurationsformuläret `SSH`.
1. `public key` finns under det här formuläret.

Lämna den här sidan öppen genom hela självstudiekursen - du behöver den i nästa avsnitt och i slutet.

Nedan visas hur du navigerar genom [!DNL Commerce Intelligence] för att hämta nyckeln:

![Hämtar den offentliga nyckeln för RJMetrics](../../../assets/get-mbi-public-key.gif)

## Tillåt åtkomst till IP-adressen [!DNL Commerce Intelligence] {#allowlist}

För att anslutningen ska lyckas måste du konfigurera brandväggen så att den tillåter åtkomst från din IP-adress. Det är `54.88.76.97/32`, men det finns även på sidan för `PostgreSQL`-autentiseringsuppgifter. Se den blå rutan i GIF ovan.

## Skapar en [!DNL Linux]-användare för [!DNL Commerce Intelligence] {#linux}

Detta kan vara en produktionsmaskin eller en sekundär maskin, förutsatt att den innehåller realtidsdata (eller ofta uppdaterade). Du kan [begränsa den här användaren](../../../administrator/account-management/restrict-db-access.md) som du vill, förutsatt att du behåller rätten att ansluta till servern [!DNL PostgreSQL].

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
```

>[!IMPORTANT]
>
>Om filen `sshd\_config` som är associerad med servern inte är inställd på standardalternativet har bara vissa användare serveråtkomst, vilket förhindrar att anslutningen till [!DNL Commerce Intelligence] lyckas. I dessa fall måste du köra ett kommando som `AllowUsers` för att tillåta den grundläggande användaråtkomsten till servern.

## Skapar en [!DNL Commerce Intelligence] [!DNL Postgres]-användare {#postgres}

Din organisation kan behöva utföra en annan process, men det enklaste sättet att skapa den här användaren är att köra följande fråga när användaren är inloggad i Postgres som en användare med behörighet att bevilja behörigheter. Användaren ska också äga schemat som [!DNL Commerce Intelligence] beviljas åtkomst till.

```sql
    GRANT CONNECT ON DATABASE <database name> TO rjmetric WITH PASSWORD <secure password>;GRANT USAGE ON SCHEMA <schema name> TO rjmetric;GRANT SELECT ON ALL TABLES IN SCHEMA <schema name> TO rjmetric;ALTER DEFAULT PRIVILEGES IN SCHEMA <schema name> GRANT SELECT ON TABLES TO rjmetric;
```

Ersätt `secure password` med ditt eget säkra lösenord, som kan skilja sig från SSH-lösenordet. Se även till att du ersätter `database name` och `schema name` med lämpliga namn i databasen.

Om du vill ansluta flera databaser eller scheman upprepar du den här processen efter behov.

## Anslutningen och användarinformationen anges i [!DNL Commerce Intelligence] {#finish}

Du måste ange anslutning och användarinformation i [!DNL Commerce Intelligence] för att kunna slå ihop allt. Har du lämnat sidan med [!DNL PostgreSQL] inloggningsuppgifter öppen? Om inte går du till **[!UICONTROL Manage Data > Connections]** och klickar på **[!UICONTROL Add a Data Source]** och sedan på ikonen [!DNL PostgreSQL] . Glöm inte att ställa in växeln `Encrypted` på `Yes`.

Ange följande information på den här sidan, med början i avsnittet `Database Connection`:

* `Username`: RJMetrics Postgres-användarnamn (ska vara rjmetric)
* `Password`: Lösenordet för RJMetrics Postgres
* `Port`: PostgreSQL-port på servern (5432 som standard)
* `Host`: 127.0.0.1

Under `SSH Connection`:

* `Remote Address`: IP-adressen eller värdnamnet för den server som du ska SSH till
* `Username`: Ditt SSH-inloggningsnamn (bör vara kritiskt)
* `SSH Port`: SSH-port på servern (22 som standard)

När du är klar klickar du på **Spara och testa** för att slutföra konfigurationen.

### Relaterad

* [Återautentiserar integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html?lang=sv-SE)
