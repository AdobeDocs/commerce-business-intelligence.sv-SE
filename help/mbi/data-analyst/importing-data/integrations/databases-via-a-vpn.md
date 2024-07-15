---
title: Anslut databaser via VPN
description: Lär dig hur du ansluter databaser via VPN i stället för SSH-tunneln.
exl-id: c7aa564d-42de-426e-92e9-f6e250a6abba
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 0%

---

# Anslut databaser via VPN

Adobe rekommenderar att du ansluter dina databaser med en `SSH tunnel`, men du kan även använda en krypterad `VPN`-anslutning för att skydda saker och ting. En/ett `VPN` kan användas för alla dina databasintegreringar och för att förenkla allt är processen ungefär densamma som att konfigurera en/ett `SSH tunnel`:

1. [Skapa en [!DNL Commerce Intelligence] databasanvändare](#database)
1. [Skapa en  [!DNL Commerce Intelligence] VPN-användare](#vpn)
1. [Tillåt åtkomst till  [!DNL Commerce Intelligence] IP-adressen](#allowlist)
1. [Ange anslutning och VPN-användarinformation i Commerce Intelligence](#finish)

Utöver databasinloggningsuppgifterna måste du ange autentiseringsuppgifter för en VPN-användare för att kunna kapsla in allt. Alla VPN-användare fungerar, men Adobe rekommenderar att du skapar en [!DNL Commerce Intelligence]-användare eftersom det gör det enklare för dig att spåra användarna på ditt konto.

## Skapar en databasanvändare för [!DNL Commerce Intelligence] {#database}

Hur du skapar en databasanvändare varierar beroende på vilken databastyp du ansluter. Klicka på länkarna nedan om du vill se instruktionerna för varje databastyp.

* [MICROSOFT SQL](../integrations/microsoft-sql-server.md)
* [MongoDB](../integrations/databases-via-a-vpn.md)
* [MySQL](../integrations/mysql-via-a-direct-connection.md)
* [PostgreSQL](../integrations/postgresql.md)

## Skapar en `VPN`-användare för [!DNL Commerce Intelligence] {#vpn}

Som tidigare nämnts fungerar alla giltiga `VPN`-användare, men Adobe rekommenderar att du skapar en användare enbart för [!DNL Commerce Intelligence]-användning.

## Tillåt åtkomst till IP-adresserna för [!DNL Commerce Intelligence] {#allowlist}

För att anslutningen ska lyckas måste du konfigurera brandväggen så att den tillåter åtkomst från dina IP-adresser. De är `54.88.76.97` och `34.250.211.151`, men de finns också på `credentials`-sidan för alla databasintegreringar:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Anslutningen och `VPN` användarinformation anges i [!DNL Commerce Intelligence] {#finish}

Du måste ange anslutning och användarinformation i [!DNL Commerce Intelligence] för att kunna slå ihop allt. Lämnade du databassidan `credentials` öppen? Om inte går du till **[!UICONTROL Manage Data** > **Connections]**. Klicka på **[!UICONTROL Add New Data Source]** och sedan på ikonen för den databas du ansluter. Glöm inte att ändra `Encrypted` till `Yes`.

Ange följande information på den här sidan, med början i avsnittet `Database Connection`:

* `Username`: Användarnamnet för databasanvändaren [!DNL Commerce Intelligence]
* `Password`: Lösenordet för databasanvändaren [!DNL Commerce Intelligence]
* `Port`: Databasens port på servern. Standardvärdena är:
   * `MicrosoftSQL`: `1433`
   * `MongoDB`: `27017`
   * `MySQL`: `3306`
   * `PostgreSQL`: `5432`
* `Host`: Som standard är det här localhost `127.0.0.1`, men det kan också vara serverns offentliga IP-adress eller en lokal nätverksadress.
* `Database Name (optional)`: Om du bara tillåter åtkomst till en databas (detta anges när databasanvändaren skapar ett steg) anger du namnet på den databasen här.

Under avsnittet `Encryption Connection`:

* `Encryption Type`: Ange det här till `Cisco IPsec VPN`
* `Gateway Address`: VPN-serverns IP-adress
* `Group Name`: Namnet på gruppen som används för gruppautentisering
* `Group Secret`: Lösenordet som motsvarar gruppen.
* `Username`: Användarnamnet [!DNL Commerce Intelligence] `VPN`
* `Password`: Användarlösenordet [!DNL Commerce Intelligence] `VPN`

När du är klar klickar du på **[!UICONTROL Save & Test]** för att slutföra konfigurationen.
