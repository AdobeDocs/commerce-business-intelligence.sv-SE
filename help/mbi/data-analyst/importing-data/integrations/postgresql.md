---
title: Connect PostgreSQL via SSH-tunneln
description: Lär dig hur du ansluter PostgreSQL-databasen till Commerce Intelligence via en SSH-tunnel.
exl-id: da610988-21c1-4f5f-b4e2-e2deb175a2aa
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export, SQL Report Builder
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 0%

---

# Anslut [!DNL PostgreSQL] via [!DNL SSH Tunnel]

Koppla samman [!DNL PostgreSQL] databas till [!DNL Commerce Intelligence] via `SSH tunnel`måste du göra några saker:

1. [Hämta [!DNL Commerce Intelligence] publik nyckel](#retrieve)
1. [Tillåt åtkomst till [!DNL Commerce Intelligence] IP-adress](#allowlist)
1. [Skapa en [!DNL Linux] användare för [!DNL Commerce Intelligence]](#linux)
1. [Skapa en [!DNL PostgreSQL] användare för [!DNL Commerce Intelligence]](#postgres)
1. [Ange anslutningen och användarinformationen i [!DNL Commerce Intelligence]](#finish)

## Hämtar [!DNL Commerce Intelligence] [!DNL public key] {#retrieve}

The `public key` används för att auktorisera [!DNL Commerce Intelligence] [!DNL Linux] användare. Nu ska du skapa användaren och importera nyckeln.

1. Gå till **[!UICONTROL Manage Data** > **Connections]** och klicka **[!UICONTROL Add a Data Source]**.
1. Klicka på [!DNL PostgreSQL] ikon.
1. Efter `PostgreSQL credentials` öppnas, ange `Encrypted` växla till `Yes`. Här visas `SSH` installationsformulär.
1. The `public key` finns under det här formuläret.

Lämna den här sidan öppen genom hela självstudiekursen - du behöver den i nästa avsnitt och i slutet.

Nedan visas hur du navigerar i [!DNL Commerce Intelligence] för att hämta nyckeln:

![Hämta den offentliga nyckeln för RJMetrics](../../../assets/get-mbi-public-key.gif)

## Tillåt åtkomst till [!DNL Commerce Intelligence] IP-adress {#allowlist}

För att anslutningen ska lyckas måste du konfigurera brandväggen så att den tillåter åtkomst från din IP-adress. Det är `54.88.76.97/32`, men det finns också på `PostgreSQL` inloggningssida. Se den blå rutan i GIF ovan.

## Skapa en [!DNL Linux] användare för [!DNL Commerce Intelligence] {#linux}

Detta kan vara en produktionsmaskin eller en sekundär maskin, förutsatt att den innehåller realtidsdata (eller ofta uppdaterade). Du kan [begränsa den här användaren](../../../administrator/account-management/restrict-db-access.md) på vilket sätt du vill, förutsatt att du behåller rätten att ansluta till [!DNL PostgreSQL] server.

1. Om du vill lägga till den nya användaren kör du följande kommandon som rot på din [!DNL Linux] server:

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
```

>[!IMPORTANT]
>
>Om `sshd\_config` filen som är associerad med servern är inte inställd på standardalternativet, endast vissa användare har serveråtkomst - detta förhindrar att anslutningen till [!DNL Commerce Intelligence]. I dessa fall måste du köra ett kommando som `AllowUsers` för att ge den seriösa användaren åtkomst till servern.

## Skapa en [!DNL Commerce Intelligence] [!DNL Postgres] användare {#postgres}

Din organisation kan behöva utföra en annan process, men det enklaste sättet att skapa den här användaren är att köra följande fråga när användaren är inloggad i Postgres som en användare med behörighet att bevilja behörigheter. Användaren ska också äga schemat som [!DNL Commerce Intelligence] beviljas åtkomst till.

```sql
    GRANT CONNECT ON DATABASE <database name> TO rjmetric WITH PASSWORD <secure password>;GRANT USAGE ON SCHEMA <schema name> TO rjmetric;GRANT SELECT ON ALL TABLES IN SCHEMA <schema name> TO rjmetric;ALTER DEFAULT PRIVILEGES IN SCHEMA <schema name> GRANT SELECT ON TABLES TO rjmetric;
```

Ersätt `secure password` med ditt eget säkra lösenord, som kan skilja sig från SSH-lösenordet. Se även till att ersätta `database name` och `schema name` med rätt namn i databasen.

Om du vill ansluta flera databaser eller scheman upprepar du den här processen efter behov.

## Ange anslutningen och användarinformationen i [!DNL Commerce Intelligence] {#finish}

Om du vill slå ihop allt måste du ange anslutningen och användarinformationen i [!DNL Commerce Intelligence]. Gav du [!DNL PostgreSQL] öppnas inloggningssidan? Om inte, gå till **[!UICONTROL Manage Data > Connections]** och klicka **[!UICONTROL Add a Data Source]** och sedan [!DNL PostgreSQL] ikon. Glöm inte att ställa in `Encrypted` växla till `Yes`.

Ange följande information på den här sidan, med början på `Database Connection` avsnitt:

* `Username`: RJMetrics Postgres-användarnamn (ska vara rjmetric)
* `Password`: Lösenordet för RJMetrics Postgres
* `Port`: PostgreSQL-port på servern (5432 som standard)
* `Host`: 127.0.0.1

Under `SSH Connection`:

* `Remote Address`: IP-adressen eller värdnamnet för den server som du ska ansluta till
* `Username`: Ditt SSH-inloggningsnamn (bör vara jmetriskt)
* `SSH Port`: SSH-port på servern (22 som standard)

När du är klar klickar du på **Spara och testa** för att slutföra installationen.

### Relaterad

* [Återautentisera integreringar](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
