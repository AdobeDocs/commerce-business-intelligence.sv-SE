---
title: Anslut databaser via VPN
description: Lär dig hur du ansluter databaser via VPN i stället för SSH-tunneln.
exl-id: c7aa564d-42de-426e-92e9-f6e250a6abba
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 0%

---

# Anslut databaser via VPN

Adobe rekommenderar att du ansluter dina databaser med en SSH-tunnel, men du kan även använda en krypterad VPN-anslutning för att skydda saker och ting. A `VPN` kan användas för alla era databasintegrationer och för att förenkla allt är processen ungefär densamma som att konfigurera en `SSH tunnel`:

1. [Skapa en [!DNL MBI] databasanvändare](#database)
1. [Skapa en [!DNL MBI] VPN-användare](#vpn)
1. [Tillåt åtkomst till [!DNL MBI] IP-adress](#allowlist)
1. [Ange anslutning och VPN-användarinformation i MBI](#finish)

Utöver databasinloggningsuppgifterna måste du ange autentiseringsuppgifter för en VPN-användare för att kunna kapsla in allt. Alla VPN-användare fungerar, men Adobe rekommenderar att du skapar en [!DNL MBI] -användare - gör det enklare för dig att spåra användarna på ditt konto.

## Skapa en databasanvändare för [!DNL MBI] {#database}

Hur du skapar en databasanvändare varierar beroende på vilken databastyp du ansluter. Klicka på länkarna nedan om du vill se instruktionerna för de olika databastyperna.

* [Microsoft](../integrations/microsoft-sql-server.md)
* [MongoDB](../integrations/databases-via-a-vpn.md)
* [MySQL](../integrations/mysql-via-a-direct-connection.md)
* [PostgreSQL](../integrations/postgresql.md)

## Skapa en `VPN` användare för [!DNL MBI] {#vpn}

Som tidigare nämnts gäller alla `VPN` fungerar som användare, men Adobe rekommenderar att du skapar en användare enbart för [!DNL MBI] använd.

## Tillåt åtkomst till [!DNL MBI] IP-adresser {#allowlist}

För att anslutningen ska lyckas måste du konfigurera brandväggen så att den tillåter åtkomst från dina IP-adresser. De är `54.88.76.97` och `34.250.211.151`, men det finns också på `credentials` sida för databasintegration:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Anslutningen och `VPN` användarinformation till [!DNL MBI] {#finish}

Om du vill slå ihop allt måste du ange anslutningen och användarinformationen i [!DNL MBI]. Lämna databasen `credentials` öppnas sidan? Om inte, gå till **[!UICONTROL Manage Data** > **Connections]** och klicka **[!UICONTROL Add New Data Source]** och sedan ikonen för databasen som du ansluter. Glöm inte att ändra `Encrypted` växla till `Yes`.

Ange följande information på den här sidan, med början på `Database Connection` avsnitt:

* `Username`: Användarnamnet för [!DNL MBI] databasanvändare
* `Password`: Lösenordet för [!DNL MBI] databasanvändare
* `Port`: Databasens port på servern. Standardvärdena är:
* `MicrosoftSQL`: `1433`
* `MongoDB`: `27017`
* `MySQL`: `3306`
* `PostgreSQL`: `5432`
* `Host`: Som standard är detta localhost `127.0.0.1`, men det kan också vara serverns offentliga IP-adress eller en lokal nätverksadress.
* `Database Name (optional)`: Om du bara tillåter åtkomst till en databas (detta anges när användaren skapar en databas), anger du namnet på den databasen här.

Under `Encryption Connection` avsnitt:

* `Encryption Type`: Ange detta till `Cisco IPsec VPN`
* `Gateway Address`: VPN-serverns IP-adress
* `Group Name`: Namnet på gruppen som används för gruppautentisering
* `Group Secret`: Lösenordet som motsvarar gruppen.
* `Username`: The [!DNL MBI] `VPN` användarnamn
* `Password`: The [!DNL MBI] `VPN` användarlösenord

Så ja! När du är klar klickar du på **[!UICONTROL Save & Test]** för att slutföra installationen.
