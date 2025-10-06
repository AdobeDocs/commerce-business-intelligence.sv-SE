---
title: Delutar ditt [!DNL Commerce Intelligence] konto
description: Lär dig hur du rensar ditt [!DNL Commerce Intelligence] konto.
exl-id: 5fcdac2d-41ca-4011-b646-a699d9ecc6e4
role: Admin, User
feature: Accounts
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '904'
ht-degree: 0%

---

# Rensa ditt [!DNL Adobe Commerce Intelligence]-konto

Oavsett om du har varit med [!DNL Commerce Intelligence] i sex månader eller sex år så är det av största vikt att du har ett tidskonto för att få ut så mycket som möjligt av plattformen. Med tiden är det naturligt att det finns användare, kontrollpaneler, rapporter, mätvärden och kolumner som inte längre behövs. Du kanske skapade en rapport för engångsbruk och glömde den eller en användare som lämnade företaget hade aldrig inaktiverat sitt konto.

Med [standardiserad, tydlig namngivning för alla element ](../best-practices/naming-elements.md)) i ditt [!DNL Commerce Intelligence]-konto kan du minska problem och onödiga analyser för användarna genom att följa stegen nedan. Ytterligare en förmån är [potentiellt snabbare uppdateringscykler](../best-practices/reduce-update-cycle-time.md).

## Steg 1: Identifiera dina icke-aktiva användare

Det första steget för att rensa ditt konto är att inaktivera konton för dina icke-aktiva användare, till exempel personer som har lämnat företaget eller inte längre använder [!DNL Commerce Intelligence] i sina nuvarande roller.

Det gör du genom att klicka på företagets namn i det övre högra navigeringsfältet och sedan välja **[!UICONTROL Manage Users]**. Välj sedan den användare som du vill inaktivera och klicka på **[!UICONTROL Deactivate User]**.

>[!NOTE]
>
>Du behöver [administratörsbehörighet](../administrator/user-management/user-management.md) för att göra detta.

>[!WARNING]
>
>När du inaktiverar en användare tas diagram, instrumentpaneler och andra resurser som skapats av användaren bort. Om du vill bevara dessa resurser kontaktar du [!DNL Commerce Intelligence] [support](../guide-overview.md#Submitting-a-Support-Ticket)-teamet innan du inaktiverar användaren. Support kan hjälpa dig att överföra dessa resurser till en annan användare.

### Återaktivera en användare

Om du vill återaktivera en användare bjuder du in användaren på nytt genom att återskapa kontot med samma e-postadress som inaktiverades, och åtkomst och de data användaren äger återställs vid inloggningen.

## Steg 2: Ta bort oanvända instrumentpaneler och rapporter

Nästa steg i granskningen av ditt konto är att ta bort oanvända instrumentpaneler och rapporter.

>[!NOTE]
>
>Du behöver `Admin` eller `Standard` [användarbehörigheter](../administrator/user-management/user-management.md) för att kunna göra detta.

Alla användare med `Admin`- eller `Standard`-åtkomst kan skapa rapporter och instrumentpaneler. Därför måste alla med dessa behörigheter följa stegen nedan för att identifiera och ta bort oanvända rapporter.

### Granska dina instrumentpaneler och rapporter

Innan du tar bort något bör du granska dina rapporter och kontrollpaneler för att se vad som används. Även om du kan använda funktionen **[!UICONTROL find unused reports]** som beskrivs nedan gör en inledande granskning att rensningsarbetet blir mycket mer produktivt.

### Ta bort instrumentpaneler och rapporter

När du har öppnat dina instrumentpaneler och rapporter kan du börja rensa ditt konto.

**Ta bort en rapport från en instrumentpanel**

1. Leta reda på rapporten som du vill ta bort på instrumentpanelen.
1. Välj **[!UICONTROL Options]** i rapportens övre högra hörn.
1. Klicka på **[!UICONTROL Remove From Dashboard]**.

**Ta bort hela instrumentpanelen**

1. Välj **[!UICONTROL Manage Data]** och sedan **[!UICONTROL Dashboards**].
1. Klicka på den kontrollpanel som du vill ta bort.
1. Klicka på **[!UICONTROL Delete Dashboard]**.

Du kan också välja **[!UICONTROL Dashboard Options]** och sedan **[!UICONTROL Delete]** från själva instrumentpanelen.

![Ta bort alternativ på instrumentpanelens kugghjulsmeny](../../mbi/assets/Delete_from_dashboard.png)

>[!NOTE]
>
>När du tar bort en kontrollpanel tas inte rapporterna bort, så du måste ta ett steg till för att ta bort rapporterna.

**Ta bort oanvända rapporter**

1. Välj **[!UICONTROL Manage Data]** och sedan **[!UICONTROL Reports]**.
1. Markera rutan **Visa endast oanvända rapporter** som finns under mätvärdeslistan. Detta skapar en lista med rapporter som inte används i en instrumentpanel eller e-postsammanfattning.
1. Markera de rapporter som du vill ta bort. Du kan markera alla genom att klicka i kryssrutan ovanför rapportlistan.
1. Klicka på **[!UICONTROL Delete Selected]**.

Här följer en titt på borttagningsprocessen som inte används:

![Listan med rapporter som inte används visar rapporter som inte finns på någon instrumentpanel](../../mbi/assets/unused_reports.png)

## Steg 3: Ta bort oanvända mått

När du har rensat bort användarlistan, kontrollpanelerna och rapporterna kan du börja granska din lista med mätvärden. På så sätt kan du identifiera allt som kan vara inaktuellt - till exempel har ett nytt mått skapats med en annan definition - eller som inte används.

1. Om du vill generera en lista med beroende rapporter för ett mätresultat går du till **[!DNL Manage Data]** och väljer sedan Klicka **[!UICONTROL Metrics]**.
1. Klicka på **[!UICONTROL Edit]** bredvid ett mätvärde.
1. Längst ned på sidan visas ett avsnitt med namnet **[!UICONTROL Dependent Charts]**. Klicka på länken om du vill generera en lista med beroende rapporter för det här måttet.
1. När kontrollen är klar visar [!DNL Commerce Intelligence] en lista över instrumentpaneler, rapporter och användare som använder det här måttet.

![Dialogrutan Rapportera beroenden visar vilka rapporter som använder den valda kolumnen](../../mbi/assets/report_dependecies.png)

Om du bestämmer dig för att måttet inte längre behövs går du tillbaka till sidan **[!UICONTROL Metrics]** genom att klicka på **[!UICONTROL Back to Metric List]** för att hitta måttet som du vill ta bort. Klicka på **[!UICONTROL Delete]**.

## Steg 4: Utvärdera dina synkroniserade kolumner

Det sista steget är att utvärdera de kolumner som synkroniseras i din Data Warehouse. Det går inte bara att avsynkronisera kolumner så att ditt konto rensas, det kan också minska uppdateringstiden.

Om du vill fortsätta med detta kontaktar du [!DNL Commerce Intelligence] [Support](../guide-overview.md#Submitting-a-Support-Ticket). Supportteamet kan skapa en rapport som innehåller alla kolumner som inte används i någon kontrollpanel för någon användare och som inte används i e-postsammanfattningar, exklusive SQL-rapporter. Du kan sedan använda den här rapporten som vägledning när du väljer kolumner som ska avsynkroniseras via Data Warehouse Manager.

>[!NOTE]
>
>Du kan alltid börja synkronisera de här kolumnerna igen i framtiden. Om du avsynkroniserar en kolumn tas alla data bort från din Data Warehouse. Det innebär bara att den här kolumnen inte kontrolleras om det finns nya eller uppdaterade värden under uppdateringscykeln.

**Så här avsynkroniserar du en kolumn (eller kolumner)**

1. Gå till **[!DNL Manage Data]** och sedan till **[!UICONTROL Data Warehouse]**.
1. Navigera till tabellen som innehåller kolumnen i listan **[!UICONTROL Synced Tables]**.
1. Markera en eller flera rutor bredvid en eller flera kolumner som du vill avsynkronisera.

   >[!NOTE]
   >
   >Du kan inte avsynkronisera en primärnyckelkolumn utan att släppa hela tabellen.

1. Klicka på **[!UICONTROL Remove]** om du vill avsynkronisera en eller flera kolumner.

Här är en titt på hela processen:

![Alternativet Släpp kolumn i Data Warehouse Manager](../../mbi/assets/drop_column.png)

## Radbrytning

Ditt [!DNL Commerce Intelligence]-konto bör nu vara mer tidskrävande och enklare att navigera för dig och ditt team.
