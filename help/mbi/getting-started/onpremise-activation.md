---
title: Aktivera ditt [!DNL Adobe Commerce Intelligence] konto
description: Lär dig vem du ska kontakta för att aktivera ditt [!DNL Commerce Intelligence] konto.
exl-id: 0efac7b4-2457-48c7-947a-d2776b90a1dd
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 736dbdc3ea6bc8b7c852f06110705765f040c31f
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 0%

---

# Aktivera ditt [!DNL Commerce Intelligence]-konto för On-Premise- och Starter-prenumerationer

Om du vill aktivera [!DNL Commerce Intelligence] för lokala prenumerationer skapar du först ett [!DNL Commerce Intelligence]-konto, anger din inställningsinformation och ansluter sedan [!DNL Commerce Intelligence] till din [!DNL Commerce]-databas. <!-- For information about activation in `Cloud Starter` projects, see [Activating your [!DNL Commerce Intelligence] Account for `Cloud Starter` Subscriptions](../getting-started/cloud-activation.md).-->

## Skapa ditt [!DNL Commerce Intelligence]-konto

Om du vill skapa ett konto kontaktar du Adobe Account Team eller kundens tekniska rådgivare.

## Skapa ditt lösenord

När ditt konto har skapats kan du kontrollera din e-postadress för att få ett e-postmeddelande från [!DNL The Magento BI Team@rjmetrics.com]. Använd länken i e-postmeddelandet för att komma åt ditt [!DNL Commerce Intelligence]-konto och skapa ditt lösenord. Gå till din inkorg och verifiera din e-postadress.

[Kontakta support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=sv-SE) om du inte fått något e-postmeddelande.

![Skapa lösenordsskärm för nytt Commerce Intelligence-konto](../assets/create-account-4.png)

## Ange dina butiksinställningar

Fyll i formuläret för lagringsinformation innan du konfigurerar databasanslutningen. Den här informationen krävs för att slutföra installationen av **[!UICONTROL Connect your Database]**.

![Lagra informationsformulär med företagsnamn, valuta och tidszonsfält](../assets/create-account-6.png)

## Lägg till [!DNL Commerce Intelligence] användare

När du har angett ditt lösenord och loggat in på [!DNL Commerce Intelligence] kan du lägga till andra användare i ditt [!DNL Commerce Intelligence]-konto. När du lägger till användare lägger du till administratörsanvändare med lämplig behörighet för att slutföra aktiveringsprocessen.

![Lägg till användarformulär med e-postadresser och behörighetsnivåfält](../assets/create-account-5.png)

## Skapa en dedikerad [!DNL Commerce Intelligence]-användare i [!DNL Commerce]-administratören

Om du vill använda [!DNL Commerce Intelligence] måste du lägga till en permanent och dedikerad användare i [!DNL Commerce]-projektet. Den här dedikerade användaren fungerar som en permanent anslutning till [!DNL Commerce] som gör det möjligt att hämta och överföra nya data till kontots [!DNL Commerce Intelligence] Data Warehouse.

Om du konfigurerar en dedikerad [!DNL Commerce Intelligence]-användare försäkrar du dig om att kontot inte inaktiveras eller tas bort och därmed avbryts anslutningen till [!DNL Commerce Intelligence].


>[!NOTE]
>
>Adobe rekommenderar att du använder ett kontonamn som anger dess permanenta status (t.ex. ACI-dedikerad, ACI-database-connector).

När du har skapat den dedikerade användaren för [!DNL Commerce Intelligence] i Admin lägger du till samma användare i den primära miljön för [!DNL Commerce]-projektet med inställningen **[!UICONTROL Master]** för `Contributor`.

![Commerce lägger till användargränssnitt med rollen inställd på Contributor](../assets/commerce-add-user-settings.png)

## Skaffa dina Commerce Intelligence SSH-nycklar

1. Bläddra nedåt och välj [!UICONTROL Connect your database] på sidan [!DNL Commerce Intelligence] för **[!UICONTROL Encryption settings]**-konfiguration.

1. För **krypteringstyp** väljer du `SSH Tunnel`.

1. Kopiera den offentliga nyckeln som anges i listrutan.

   ![Sidan med krypteringsinställningar som visar SSH-tunneltypen och fältet för offentlig nyckel](../assets/encryption-setting-new-account.png)

## Lägg till din offentliga nyckel i [!DNL Commerce Intelligence]

1. Logga in från [!DNL Commerce Admin] med inloggningsinformationen för den [!DNL Commerce Intelligence]-användare du just skapade.

1. Välj fliken **Kontoinställningar**.

1. Bläddra nedåt och utöka listrutan **[!UICONTROL SSH Keys]**. Välj sedan **[!UICONTROL Add a public key]**.

   ![Sidan Kontoinställningar med SSH-nycklar och knappen Lägg till offentlig nyckel &#x200B;](../assets/add-public-key.png)

1. Klistra in den offentliga nyckeln som du kopierade i steget [!DNL Encryption Type] ovan.

   ![Lägg till formulär med offentlig nyckel med nyckeltextfält och Skicka-knapp](../assets/paste-public-key.png)

## Ange autentiseringsuppgifter för [!DNL Commerce Intelligence] Essentials `MySQL`

1. Uppdatera din `.magento/services.yaml`.

   ![Kod som visar konfigurationen för MySQL-tjänsten i services.yaml-filen](../assets/update-magento-services-yaml.png)

1. Uppdatera din `.magento.app.yaml`.

   ![Kod som visar databasrelationskonfigurationen i filen app.yaml](../assets/magento-app-yaml-relationships.png)

## Hämta databasanslutningsinformation

Hämta databasanslutningsinformationen till databasen [!DNL Commerce] till [!DNL Commerce Intelligence]

1. Hämta dina uppgifter genom att köra följande.

   `echo $MAGENTO_CLOUD_RELATIONSHIPS | base64 --decode | json_pp`

1. Granska databasinformationen som ska se ut ungefär som i följande exempel.

   ![JSON-utdata som visar autentiseringsuppgifter för databasanslutning inklusive värd, port och användarnamn](../assets/example-database-information.png)

## Anslut [!DNL Commerce Intelligence] till din [!DNL Commerce]-databas med en krypterad anslutning

>[!NOTE]
>
>Adobe rekommenderar att du använder en [`SSH tunnel`](../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md)-tunnel för att skapa en databasanslutning. Om den här metoden inte är ett alternativ kan du ändå länka [!DNL Commerce Intelligence] till databasen med en [`direct connection`](../data-analyst/importing-data/integrations/mysql-via-a-direct-connection.md).

Ange din [!DNL Commerce Intelligence]-information på skärmen [!UICONTROL Connect your Magento Database].

![Anslut databasformuläret med fält för integrationsnamn, värd, port, användarnamn, lösenord och databasnamn](../assets/connect-magento-db.png)

**Indata:**

[!UICONTROL Integration Name]: [välj ett namn för din [!DNL Commerce Intelligence]-instans]

[!UICONTROL Host]: `mbi.internal`

[!UICONTROL Port]: `3306`

[!UICONTROL -användarnamn]: `mbi`

[!UICONTROL Password]: [indatalösenordet visas i föregående avsnitt]

[!UICONTROL Database Name]: `main`

[!UICONTROL Table Prefixes]: [lämna tomt om det inte finns några tabellprefix]

## Ange dina [!UICONTROL **tidszonsinställningar**]

![Formulär för tidszonsinställningar med databasens tidszon och önskade listrutefält för tidszon](../assets/time-zone-settings.png)

**Indata:**

[!UICONTROL Database Timezone]: `UTC`

[!UICONTROL Desired Timezone]: [välj den tidszon som du vill att dina data ska visas för]

## Hämta information om krypteringsinställningarna

Projektgränssnittet tillhandahåller en SSH-åtkomststräng. Strängen kan användas för att samla in den information som krävs för [!UICONTROL **fjärradressen**] och [!UICONTROL **användarnamnet**]. Använd SSH-åtkomststrängen genom att markera åtkomstplatsknappen i huvudgrenen i projektgränssnittet. Leta sedan reda på din [!UICONTROL User Name] och [!UICONTROL Remote Address] så som visas nedan.

![Projektgränssnittet som visar SSH-åtkomstinformation med användarnamn och fjärradress](../assets/master-branch-settings.png)

## Ange dina [!DNL Encryption]-inställningar

![Formulär för krypteringsinställningar med fält för krypteringstyp, fjärradress, användarnamn och port](../assets/encryption-settings-2.png)

**Indata:**

[!UICONTROL Encryption Type]: `SSH Tunnel`

[!UICONTROL Remote Address]: `ssh.us-3.magento.cloud` [från föregående steg]

[!UICONTROL Username]: `vfbfui4vmfez6-master-7rqtwti—mymagento` [från föregående steg]

[!UICONTROL Port]: `22`

## Spara på integreringen.

När du är klar med konfigurationsstegen tillämpar du ändringarna genom att välja [!UICONTROL **Spara integrering**].

Du har nu anslutit din [!DNL Commerce]-databas till ditt [!DNL Commerce Intelligence]-konto.

>[!NOTE]
>
>Om du är [!DNL Adobe Commerce Intelligence Pro]-kund kontaktar du din Customer Success Manager eller kundens tekniska rådgivare för att koordinera nästa steg.

När du har slutfört konfigurationen [loggar du in](../getting-started/sign-in.md) på ditt [!DNL Commerce Intelligence]-konto.

<!---# Activate your [!DNL Commerce Intelligence] Account

To activate [!DNL Commerce Intelligence] for on-premise or `Cloud Pro` subscriptions, [contact support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=sv-SE).

>[!NOTE]
>
>Adobe no longer supports new `Cloud Starter` subscriptions.--->
