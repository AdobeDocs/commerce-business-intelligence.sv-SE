---
title: Anslut databaser via VPN
description: Lär dig hur du ansluter databaser via VPN i stället för SSH-tunneln.
exl-id: c7aa564d-42de-426e-92e9-f6e250a6abba
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '403'
ht-degree: 0%

---

# Anslut databaser via VPN

Adobe rekommenderar att du ansluter dina databaser med en `SSH tunnel`kan du även använda en krypterad `VPN` för att hålla saker och ting säkra. A `VPN` kan användas för alla era databasintegrationer och för att förenkla allt är processen ungefär densamma som att konfigurera en `SSH tunnel`:

1. [Skapa en [!DNL Commerce Intelligence] databasanvändare](#database)
1. [Skapa en [!DNL Commerce Intelligence] VPN-användare](#vpn)
1. [Tillåt åtkomst till [!DNL Commerce Intelligence] IP-adress](#allowlist)
1. [Ange anslutningen och VPN-användarinformationen i Commerce Intelligence](#finish)

Utöver databasinloggningsuppgifterna måste du ange autentiseringsuppgifter för en VPN-användare för att kunna kapsla in allt. Alla VPN-användare fungerar, men Adobe rekommenderar att du skapar en [!DNL Commerce Intelligence] användare eftersom det gör det enklare för dig att spåra användarna på ditt konto.

## Skapa en databasanvändare för [!DNL Commerce Intelligence] {#database}

Hur du skapar en databasanvändare varierar beroende på vilken databastyp du ansluter. Klicka på länkarna nedan om du vill se instruktionerna för varje databastyp.

* [MICROSOFT SQL](../integrations/microsoft-sql-server.md)
* [MongoDB](../integrations/databases-via-a-vpn.md)
* [MySQL](../integrations/mysql-via-a-direct-connection.md)
* [PostgreSQL](../integrations/postgresql.md)

## Skapa en `VPN` användare för [!DNL Commerce Intelligence] {#vpn}

Som tidigare nämnts gäller alla `VPN` fungerar som användare, men Adobe rekommenderar att du skapar en användare enbart för [!DNL Commerce Intelligence] använd.

## Tillåt åtkomst till [!DNL Commerce Intelligence] IP-adresser {#allowlist}

För att anslutningen ska lyckas måste du konfigurera brandväggen så att den tillåter åtkomst från dina IP-adresser. De är `54.88.76.97` och `34.250.211.151`, men det finns också på `credentials` sida för databasintegration:

![MBI_Allow_Access_IPs.png](../../../assets/MBI_allow_access_IPs.png)

## Anslutningen och `VPN` användarinformation till [!DNL Commerce Intelligence] {#finish}

Om du vill slå ihop allt måste du ange anslutningen och användarinformationen i [!DNL Commerce Intelligence]. Lämna databasen `credentials` öppnas sidan? Om inte, gå till **[!UICONTROL Manage Data** > **Connections]**. Klicka **[!UICONTROL Add New Data Source]** och klicka sedan på ikonen för den databas som du ansluter. Glöm inte att ändra `Encrypted` växla till `Yes`.

Ange följande information på den här sidan, med början på `Database Connection` avsnitt:

* `Username`: Användarnamn för [!DNL Commerce Intelligence] databasanvändare
* `Password`: Lösenordet för [!DNL Commerce Intelligence] databasanvändare
* `Port`: Databasens port på servern. Standardvärdena är:
   * `MicrosoftSQL`: `1433`
   * `MongoDB`: `27017`
   * `MySQL`: `3306`
   * `PostgreSQL`: `5432`
* `Host`: Detta är som standard localhost `127.0.0.1`, men det kan också vara serverns offentliga IP-adress eller en lokal nätverksadress.
* `Database Name (optional)`: Om du bara tillåtit åtkomst till en databas (detta anges när databasanvändaren skapar en databas) anger du namnet på den databasen här.

Under `Encryption Connection` avsnitt:

* `Encryption Type`: Ange detta till `Cisco IPsec VPN`
* `Gateway Address`: VPN-serverns IP-adress
* `Group Name`: Namnet på gruppen som används för gruppautentisering
* `Group Secret`: Lösenordet som motsvarar gruppen.
* `Username`: [!DNL Commerce Intelligence] `VPN` användarnamn
* `Password`: [!DNL Commerce Intelligence] `VPN` användarlösenord

När du är klar klickar du **[!UICONTROL Save & Test]** för att slutföra installationen.
