---
title: Aktivera [!DNL MBI] Konto för lokal prenumeration
description: Läs om hur du aktiverar [!DNL MBI] konto för On-Premise-prenumerationer.
exl-id: 0efac7b4-2457-48c7-947a-d2776b90a1dd
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 0%

---

# Aktivera [!DNL MBI] Konto för lokal prenumeration

Aktivera [!DNL MBI] för lokala prenumerationer måste du först skapa en [!DNL MBI] konto, ansluta [!DNL MBI] till din Commerce-databas. Information om aktivering finns i `Cloud Starter` projekt, se [Aktivera [!DNL MBI] Konto för `Cloud Starter` Prenumerationer](../getting-started/cloud-activation.md).

1. Skapa [!DNL MBI] Konto.

   - Gå till [Adobe Commerce-kontoinloggning](https://account.magento.com/customer/account/login)

   - Gå till **[!UICONTROL My Account** > **My [!DNL MBI] Instances]**.

   - Klicka **[!UICONTROL Create Instance]**. Om du inte ser den här knappen kontaktar du kontoteamet på Adobe eller kundens tekniska rådgivare.

   - Ange dina uppgifter för att skapa ditt konto.

   ![](../assets/create-account-2.png)

   - Gå till din inkorg och verifiera din e-postadress. Om du inte har fått något e-postmeddelande [kontakta support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

   - Skapa ditt lösenord.

   ![](../assets/create-account-4.png)

   - När du har skapat ditt konto kan du lägga till användare i ditt nya konto. Nu kan tekniska administratörer läggas till för att utföra följande steg.

   ![](../assets/create-account-5.png)

1. Ange information om din butik för att ange dina inställningar.

   ![](../assets/create-account-6.png)

1. Anslut [!DNL MBI] till din Commerce-databas med hjälp av en krypterad anslutning.

   Commerce rekommenderar att du ansluter med en [`SSH tunnel`](../data-analyst/importing-data/integrations/mysql-via-ssh-tunnel.md). Om det här inte är ett alternativ kan du ändå länka [!DNL MBI] till databasen med en [`direct connection`](../data-analyst/importing-data/integrations/mysql-via-a-direct-connection.md).

1. När du har anslutit [!DNL MBI] till din Commerce-databas, kontakta ditt kontoteam på Adobe för att koordinera nästa steg, som att skapa integreringar och andra konfigurationssteg.

1. När konfigurationen är klar kan du [logga in](../getting-started/sign-in.md) till [!DNL MBI] konto.
