---
title: Avlasta [!DNL Commerce Intelligence] Konto
description: Lär dig hur du rensar upp dina [!DNL Commerce Intelligence] konto.
exl-id: 5fcdac2d-41ca-4011-b646-a699d9ecc6e4
role: Admin, User
feature: Accounts
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 0%

---

# Rensa [!DNL Adobe Commerce Intelligence] Konto

Om du har varit med [!DNL Commerce Intelligence] i sex månader eller sex år är det avgörande för att ni ska få ut det mesta av plattformen att ha ett välbekväm konto. Med tiden är det naturligt att det finns användare, kontrollpaneler, rapporter, mätvärden och kolumner som inte längre behövs. Du kanske skapade en rapport för engångsbruk och glömde den eller en användare som lämnade företaget hade aldrig inaktiverat sitt konto.

Med [standardiserad, tydlig namngivning för alla element](../best-practices/naming-elements.md)) [!DNL Commerce Intelligence] kontots granskningssteg nedan hjälper dig att minska trassel och onödiga analyser för dina användare. Ytterligare en förmån innefattar [snabbare uppdateringscykler](../best-practices/reduce-update-cycle-time.md).

## Steg 1: Identifiera dina icke-aktiva användare

Det första steget i att rensa ditt konto är att inaktivera konton för dina icke-aktiva användare, till exempel personer som har lämnat företaget eller inte längre använder [!DNL Commerce Intelligence] i sina nuvarande roller.

Klicka på företagets namn i det övre högra navigeringsfältet och välj **[!UICONTROL Manage Users]**. Välj sedan den användare som du vill inaktivera och klicka på **[!UICONTROL Deactivate User]**.

>[!NOTE]
>
>Du behöver [Administratörsbehörigheter](../administrator/user-management/user-management.md) för att göra detta.

>[!WARNING]
>
>När du inaktiverar en användare tas diagram, instrumentpaneler och andra resurser som skapats av användaren bort. Kontakta [!DNL Commerce Intelligence] [support](../guide-overview.md#Submitting-a-Support-Ticket) innan användaren inaktiveras. Support kan hjälpa dig att överföra dessa resurser till en annan användare.

### Återaktivera en användare

Om du vill återaktivera en användare bjuder du in användaren på nytt genom att återskapa kontot med samma e-postadress som inaktiverades, och åtkomst och de data användaren äger återställs vid inloggningen.

## Steg 2: Ta bort oanvända instrumentpaneler och rapporter

Nästa steg i granskningen av ditt konto är att ta bort oanvända instrumentpaneler och rapporter.

>[!NOTE]
>
>Du behöver `Admin` eller `Standard` [användarbehörigheter](../administrator/user-management/user-management.md) för att göra detta.

Alla användare med `Admin` eller `Standard` kan skapa rapporter och kontrollpaneler. Därför måste alla med dessa behörigheter följa stegen nedan för att identifiera och ta bort oanvända rapporter.

### Granska dina instrumentpaneler och rapporter

Innan du tar bort något bör du granska dina rapporter och kontrollpaneler för att se vad som används. Du kan använda **[!UICONTROL find unused reports]** som beskrivs nedan gör en inledande granskning att rensningen blir mycket mer produktiv.

### Ta bort instrumentpaneler och rapporter

När du har öppnat dina instrumentpaneler och rapporter kan du börja rensa ditt konto.

**Ta bort en rapport från en kontrollpanel**

1. Leta reda på rapporten som du vill ta bort på instrumentpanelen.
1. Välj **[!UICONTROL Options]** i rapportens övre högra hörn.
1. Klicka på **[!UICONTROL Remove From Dashboard]**.

**Ta bort en hel instrumentpanel**

1. Välj **[!UICONTROL Manage Data]**, sedan **[!UICONTROL Dashboards**].
1. Klicka på den kontrollpanel som du vill ta bort.
1. Klicka på **[!UICONTROL Delete Dashboard]**.

Du kan också välja **[!UICONTROL Dashboard Options]** sedan **[!UICONTROL Delete]** från själva kontrollpanelen.

![](../../mbi/assets/Delete_from_dashboard.png)

>[!NOTE]
>
>När du tar bort en kontrollpanel tas inte rapporterna bort, så du måste ta ett steg till för att ta bort rapporterna.

**Ta bort oanvända rapporter**

1. Välj **[!UICONTROL Manage Data]** sedan **[!UICONTROL Reports]**.
1. Kontrollera **Visa endast oanvända rapporter** rutan under mätvärdeslistan. Detta skapar en lista med rapporter som inte används i en instrumentpanel eller e-postsammanfattning.
1. Markera de rapporter som du vill ta bort. Du kan markera alla genom att klicka i kryssrutan ovanför rapportlistan.
1. Klicka på **[!UICONTROL Delete Selected]**.

Här följer en titt på borttagningsprocessen som inte används:

![](../../mbi/assets/unused_reports.png)

## Steg 3: Ta bort oanvända mått

När du har rensat bort användarlistan, kontrollpanelerna och rapporterna kan du börja granska din lista med mätvärden. På så sätt kan du identifiera allt som kan vara inaktuellt - till exempel har ett nytt mått skapats med en annan definition - eller som inte används.

1. Om du vill generera en lista med beroende rapporter för ett mätresultat går du till **[!DNL Manage Data]** och sedan klicka på **[!UICONTROL Metrics]**.
1. Klicka **[!UICONTROL Edit]** bredvid ett mätresultat.
1. Längst ned på sidan visas ett avsnitt som kallas **[!UICONTROL Dependent Charts]**. Klicka på länken om du vill generera en lista med beroende rapporter för det här måttet.
1. När kontrollen är klar [!DNL Commerce Intelligence] visar en lista med instrumentpaneler, rapporter och användare som använder det här måttet.

![](../../mbi/assets/report_dependecies.png)

Om du bestämmer dig för att måttet inte längre behövs går du tillbaka till **[!UICONTROL Metrics]** sida genom att klicka **[!UICONTROL Back to Metric List]** för att hitta måtten som du vill ta bort. Klicka på **[!UICONTROL Delete]**.

## Steg 4: Utvärdera dina synkroniserade kolumner

Det sista steget är att utvärdera de kolumner som synkroniseras i Datan Warehouse. Det går inte bara att avsynkronisera kolumner så att ditt konto rensas, det kan också minska uppdateringstiden.

Om du vill fortsätta med detta, kontakta [!DNL Commerce Intelligence] [Support](../guide-overview.md#Submitting-a-Support-Ticket). Supportteamet kan skapa en rapport som innehåller alla kolumner som inte används i någon kontrollpanel för någon användare och som inte används i e-postsammanfattningar, exklusive SQL-rapporter. Du kan sedan använda den här rapporten som vägledning när du markerar kolumner som ska avsynkroniseras via Data Warehouse Manager.

>[!NOTE]
>
>Du kan alltid börja synkronisera de här kolumnerna igen i framtiden. Om du avsynkroniserar en kolumn tas alla data bort från Datan Warehouse. Det innebär bara att den här kolumnen inte har genomsökts efter nya eller uppdaterade värden under uppdateringscykeln.

**Så här avsynkroniserar du en kolumn (eller kolumner)**

1. Gå till **[!DNL Manage Data]** sedan **[!UICONTROL Data Warehouse]**.
1. I **[!UICONTROL Synced Tables]** navigera till tabellen som innehåller kolumnen.
1. Markera en eller flera rutor bredvid en eller flera kolumner som du vill avsynkronisera.
   >[!NOTE]
   >
   >Du kan inte avsynkronisera en primärnyckelkolumn utan att släppa hela tabellen.

1. Klicka **[!UICONTROL Remove]** om du vill avsynkronisera en eller flera kolumner.

Här är en titt på hela processen:

![](../../mbi/assets/drop_column.png)

## Radbrytning

Dina [!DNL Commerce Intelligence] kontot ska nu vara mer tidsinställt och enklare att navigera i för dig och ditt team.
