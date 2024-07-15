---
title: Använd tidsalternativ i Visual Report Builder
description: Lär dig att analysera data i rapporten under en viss tidsperiod.
exl-id: a1bb4838-f882-44b1-a29f-84b985032ceb
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1272'
ht-degree: 0%

---

# Använd [!DNL Time]-alternativ i [!DNL Visual Report Builder]

En av funktionerna i [!DNL Visual Report Builder] är de globala `Time Range`- och `Interval`-inställningarna. Med de här inställningarna kan du analysera data i rapporten under en viss tidsperiod.

För vissa analyser kan du dock behöva ta hänsyn till olika tidsintervall eller tidsintervall i samma rapport. Det är där `Time` alternativ kommer in. För att du ska få en bättre uppfattning om hur du använder `Time`-alternativ i dina rapporter omfattar den här självstudiekursen följande användningsfall:

* [Analyserar mätvärden utan tidsstämplar](#notimestamp)
* [Ger ett mätvärde och ett oberoende tidsintervall](#independenttimeinterval)
* [Jämföra samma mått över olika tidsintervall](#difftimerange)

Om du vill följa med i några av exempelrapporterna som beskrivs i det här avsnittet öppnar du [[!DNL Visual Report Builder]](../data-user/reports/ess-rpt-build-visual.md) innan du fortsätter.

## Analyserar mätvärden utan tidsstämplar {#notimestamp}

Vissa mätvärden kan inte trendas över tid eftersom data inte samlas in eller lagras med en associerad tidsstämpel. En inventeringstabell innehåller till exempel ofta bara en rad för varje SKU. I så fall bör du [skapa måttet ](../data-user/reports/ess-manage-data-metrics.md) utan att ange en tidsstämpel.

När du använder ett sådant mått i din rapportering, märker du att om du lägger till det här måttet i en rapport anges automatiskt en oberoende `Time Interval` av `None` och `Time Range` av `Global`:

![](../assets/Metrics_without_timestamps.gif)

## Ger ett mätvärde och ett oberoende tidsintervall {#independenttimeinterval}

Med alternativen i `Time` kan du skapa tidsbaserade 100 %-diagram för att identifiera vilken dag, vecka, månad eller år som har bidragit mest till värdet under ett visst tidsintervall. I det här avsnittet skapar du ett diagram som visar hur stor procentandel av intäkterna som genereras under varje kalendermånad på ett år.

Den här typen av rapport kan vara användbar om du vill jämföra intäkter som genereras år för år. Ett diagram för 2015 visar t.ex. att januari bidrog med 18 procent av årets intäkter och att ett diagram för 2016 bara visade 8 procent. Du kan börja undersöka vad som kan ha hänt.

1. Lägg till `Revenue`-måttet i rapporten.
1. Klicka på **[!UICONTROL Duplicate]** om du vill skapa en kopia av måttet.
1. Klicka på det globala alternativet **[!UICONTROL Time Range]** och sedan på **[!UICONTROL Moving Time Range]**. Ange det här till `Last Year`.
1. Klicka på det globala alternativet **[!UICONTROL Time Interval]** och ange det till `Monthly`.
1. Report Builder lägger automatiskt till en andra Y-axel för ett andra mått. Avmarkera rutan `Multiple Y-Axes`.
1. Därefter använder du en oberoende `Time Interval` för det första måttet. Klicka på **[!UICONTROL Time Options]** (klockikon) till höger om `first Revenue metric`.
1. Klicka på **[!UICONTROL Time Options]** i det utökade fönstret som visas ovanför rapporten.
1. Ange följande i listrutan:

   * `Time Interval`: ange det här till `None`.

   * `Time Range`: ange det här till `Last Year` genom att först klicka på **[!UICONTROL Custom]**, sedan **[!UICONTROL Moving Range]** och slutligen välja alternativet `Last Year`.

   * Klicka på **[!UICONTROL Apply]** om du vill spara intervall- och intervallinställningarna. Detta skapar ett mätvärde som beräknar den totala intäkten för föregående år. Därefter använder du det här måttet som nämnare i en formel.

   * Om du vill se procentandelen av intäkten för varje månad måste du lägga till en formel i rapporten. Klicka på **[!UICONTROL Add Formula]**.

   * Ange `B/A` i formelfältet och välj `% Percent` i listrutan bredvid textfältet. I denna formel delas intäktsbeloppet från en viss månad förra året upp med det totala intäktsbeloppet förra året.

   * Klicka på **[!UICONTROL Apply Changes]**.

   * Dölj båda indatavärdena och byt namn på formeln.

Nu kan du se hur effektfullt varje månad var förra året:

![](../assets/Independent_Time_Int.png)

## Jämföra samma mått över olika tidsintervall {#difftimerange}

I det här exemplet används en anpassad dimension med namnet `Day number of the month`. Om du vill skapa den här rapporten och inte redan har den här dimensionen i din Data Warehouse kan du [kontakta support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) om du behöver hjälp.

De två vanligaste exemplen i den här kategorin är (1) att jämföra tillväxtstatistik (intäkter år för år eller månad för månad) och (2) att bättre förstå de senaste trenderna inom lager- eller artikelförsäljning.

Titta på de dagliga intäkterna för föregående månad jämfört med samma månad från föregående år för att visa hur detta används. Säg att ni vill se på intäkterna för varje dag i januari 2016 och sedan jämföra dem med januari 2015, januari 2014 och så vidare - så visar den här rapporten oss det.

1. Lägg till `Revenue`-måttet i rapporten.
1. Klicka på **[!UICONTROL Duplicate]** om du vill skapa en kopia av måttet.
1. Byt namn på det första måttet till `Items sold last 7 days` och det andra till `Items sold last 28 days`.
1. Klicka på **[!UICONTROL Time Range]** och sedan på **[!UICONTROL Moving Time Range]**. Ange det här till `Last Month`.
1. Klicka på **[!UICONTROL Time Interval]** och ställ in den på `None`.
1. Klicka på **[!UICONTROL Time Options]** (klockikon) bredvid det andra `Revenue`-måttet.
1. Klicka på **[!UICONTROL Time Options]** i det utökade fönstret som visas ovanför rapporten.
1. Ange följande i listrutan:

   * `Time Interval`: ange det här till `None`.

   * `Time Range`: ange det här till `From 14 Months Ago To 13 Months Ago` genom att först klicka på **[!UICONTROL Custom]** och sedan **[!UICONTROL Moving Range]**. Använd fälten och listrutorna högst upp på menyn för att ange intervallet. Med den här inställningen kan vi se intäkterna för föregående månad, men föregående år.

   Oroa dig inte om mätvärdena försvinner från rapporten. Om du ställer in ett oberoende tidsalternativ döljs mätvärdena automatiskt från rapporten. Om du vill visa det igen klickar du på **[!UICONTROL Show]** bredvid måttet.

   ![](../assets/Different_Time_Ranges.gif)

   * Klicka på **[!UICONTROL Apply]** om du vill spara intervall- och intervallinställningarna.

   * Sedan lägger du till din anpassade `Day number of the month`-dimension genom att klicka på **[!UICONTROL Group By]** och välja dimensionen. Detta returnerar dagsnumret för månaden i en order, t.ex. returnerar en order som placerades den 2 mars `2`.

   * I listrutan `Group By` väljer du `Show All` och klickar på **[!UICONTROL Apply]**. Detta skapar rapportens X-axelvärden:

   ![](../assets/TO4.png)

   * Byt namn på måtten. I exemplet är det första måttet `Revenue - 2015` och det andra `Revenue - 2014`.

Ett annat vanligt användningsområde för anpassad `Time Options` är att fastställa leveransveckor. I synnerhet under semestersäsongen eller en särskild kampanjperiod kanske du vill överväga produkter som sålts under den sista veckan, månaden och föregående kampanjperiod för att fatta välgrundade beslut när det gäller inköp.

Kom ihåg att ange tidsintervall till vad du behöver när du skapar den här rapporten själv.

1. Lägg till `Items Sold`-måttet i rapporten.
1. Klicka på **[!UICONTROL Duplicate]** om du vill skapa en kopia av måttet.
1. Byt namn på måtten. Du kan använda samma namn eller något liknande:
   1. Byt namn på det första måttet till `Items sold last 7 days`.
   1. Byt namn på det andra måttet till `Items sold last 28 days`.
1. På måttet `Items sold last 7 days` klickar du på det globala **[!UICONTROL Time Range]**-alternativet och sedan **[!UICONTROL Moving Time Range]**. I det här exemplet ställer du in det på `Last 7 Days`.
1. Klicka på **[!UICONTROL Time Interval]** och ställ in den på `None`.
1. Därefter definierar du `Time Options` för måttet `Items sold last 28 days`. Klicka på **[!UICONTROL Time Options]** (klockikon) till höger om måttet `second Items sold`.
1. Klicka på **[!UICONTROL Time Options]** i det utökade fönstret som visas ovanför rapporten.
1. Ange följande i listrutan:

   * `Time Interval`: ange det här till `None`.
   * `Time Range`: ange det här till `From 29 days to 1 day ago` genom att först klicka på **[!UICONTROL Custom]** och sedan **[!UICONTROL Moving Range]**. Använd fälten och listrutorna högst upp på menyn för att ange intervallet.
   * Klicka på **[!UICONTROL Apply]** om du vill spara intervall- och intervallinställningarna.
   * Duplicera `Items sold last 28 days`-måttet och öppna det nya måttets `Time Options`. Ange följande alternativ:

      * `Time Interval`: lämna det här som `None`.
      * `Time Range`: ändra det här till datumintervallet som är anpassat till kampanjen som du är intresserad av genom att klicka på **[!UICONTROL Specific Date Range]** och sedan ange rätt datum.
      * Byt namn på måttet `Items sold during last promotion` eller något liknande.
      * Lägg till dina `Units on hand`-mått.
      * Därefter måste du lägga till de beräkningar som visar de aktuella veckorna, med hänsyn till försäljningstrender, för de tidsperioder (`last 7 days`, `last 28 days` och `last promo` period) som du inkluderar i rapporten. Du måste göra detta en gång för varje tidsperiod.

Om du vill skapa formlerna klickar du på **[!UICONTROL Add Formula]**. Ange formlerna nedan och klicka på **[!UICONTROL Apply Changes]** när du är klar. Upprepa detta för var och en av de tre tidsperioderna:

* Ange `D / A` i fältet `Formula` för `last 7 days time period`.
* Ange `D / (B/4)` i fältet `Formula` för `last 28 days time period`.

  >[!NOTE]
  >
  >Det är viktigt att normalisera de valda tidsintervallen här. Bryt 28 dagar i fyra veckor i det här exemplet. Du kan behöva använda en annan logik för formeln.

* Ange `D / C` i fältet `Formula` för `last promo period`.

  ![](../assets/Different_Time_Ranges_2.png)

* Skräddarsy slutligen rapporten genom att dölja måtten och lägga till en `SKU` eller en liknande dimension till rapporten som en `Group By`.

Det här exemplet visar att nuvarande lagernivåer var väl placerade för en produktövergripande 14-dagarsförsäljning. Om man lägger till en jämförbar kampanjperiod behöver företaget dock göra vissa ändringar, antingen genom att beställa mer lager och bara befordra artiklar med tillräckligt många enheter i lager.

Eftersom kunderna beter sig olika över tid kan ni förvänta er att olika data ska visas vid analyser. Genom att ställa in anpassade tidsalternativ kan du snabbt skapa komplexa analyser, vilket möjliggör datadrivna beslut som tar hänsyn till historiska trender.

