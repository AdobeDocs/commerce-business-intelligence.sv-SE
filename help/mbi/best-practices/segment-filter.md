---
title: Rekommenderade Dimensioner för segmentering och filtrering
description: Läs om de bästa sätten att segmentera och filtrera.
exl-id: 66391bce-bdeb-4e9d-8089-1c796e00d91e
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 0%

---

# Segmentering och filtrering

Bra segmentering är vad som förvandlar en ytlig statistik till ett affärsmått som styr beslut.

Vill du veta vilka era mest värdefulla kunder är? Vilka av era mest värdefulla marknadsföringskanaler är? Vilka av era produkter rör sig snabbare och varför? För att komma till något av dessa svar måste ni börja med att segmentera era data.

Det här avsnittet behandlar viktiga segment som ofta rekommenderas för kunderna. Det går också närmare in på vilka frågor dessa segment kan hjälpa dig att svara på. Tekniskt sett är segment datakolumner i din databas. I [!DNL Adobe Commerce Intelligence]kallas de för dimensioner.

![](../../mbi/assets/mbi-critical-segments.png)


## Användarsegment

Användarsegment hjälper dig att förstå vilka användare som är och hur de beter sig.

* **Ålder/födelseår**: Hur gamla är dina användare? Hur gamla är era mest aktiva användare? Det är oftast klokt att lägga in värdena i intervall för att få en mer effektiv analys.
* **Kön**: Har olika genrer en annan relation med er webbplats?
* **Adress**: Varifrån kommer dina användare? Bör ni fokusera era marknadsföringssatsningar på en viss region? Har era senaste annonskampanjer genomförts som förväntat i era målregioner?
* **Kundvärvningskälla**\: Vet ni vilken marknadsföringskanal era användare kommer ifrån? Klickade de på en annons eller hittade dig via sökning? [Segmentera era data utifrån inhämtningskälla](../data-analyst/analysis/google-track-user-acq.md) är det första steget i att optimera kundvärvningen. Steg två är att spendera mer pengar på det som fungerar och döda det som inte gör det.
* **Registreringsenhet**: Registrerade sig användare via din mobilapp eller din webbplats? iOS eller Android™? Är er mobilbas stor nog att tilldela mer resurser för att utveckla er mobilprodukt? Om du inte har spårat detta än kan du läsa det här avsnittet [om spårning av användarenhet](../data-analyst/analysis/track-usr-dev-browser.md).
* **Refereras av** Vem är era största påverkare? Hur många användare fick direktkontakt av andra?
* **Bransch**: Om du är ett B2B-företag, i vilka branscher arbetar dina användare? Vilka branschorganisationer är det värt att gå med i?
* **Undersökningssvar**: Om du utför kundundersökningar kan du använda svaren som segment för en mer detaljerad profileringsnivå. Du kan ställa frågor som kompletterar det du redan vet om dina användare eller bekräfta dina gissningar.
* **Första orderbelopp och produktkategori**: Finns det något samband mellan en användares första order och framtida köpmönster?

## Beställningar/händelsesegment

Order- och händelsesegment hjälper till att analysera användarbeteenden och engagemang över tid.

* **[!UICONTROL Billing / Shipping Address]**: Var kommer de flesta av dina beställningar ifrån? Är det någon skillnad mellan fakturerings- och leveransadresser?
* **[!UICONTROL Status]**: Hur många av dina beställningar misslyckades? Hur stor är andelen väntande order under de senaste sju dagarna?
* **[!UICONTROL Customer acquisition source]**: Förutom att följa upp kundvärvningsdata på användarnivå kan man också [spåra det på en order- eller händelsenivå](../data-analyst/analysis/google-track-user-acq.md). En användare som har registrerats via en källa kan mycket väl fortsätta att ha åtkomst till din webbplats via andra källor.
* **[!UICONTROL Device]**: Ökar antalet mobila order? Hur stor del av era intäkter genereras via mobilköp? (Om du inte har spårat detta ännu, se det här avsnittet [om spårningsorderenhetsdata](../data-analyst/analysis/track-usr-dev-browser.md).
* **[!UICONTROL Fulfillment Center]**: Vilket av era leveranscentra genererar störst intäkter? Om ni analyserar skillnaden mellan ordertid och leveranstid, vilket leveranscenter är mest responsivt?
* **[!UICONTROL Delivery Carrier]**: Vilken är den populäraste fraktfirman? Vilken transportör har det minsta antalet returnerade artiklar?
* **[!UICONTROL Discount / Coupon Codes]**: Genererar era erbjudanden verkligen extra affärer? Hur många extra artiklar köpte era kunder utöver artikeln som såldes? Hur påverkar kuponger det genomsnittliga ordervärdet? Vilken är din genomsnittliga marginal på diskonterade jämfört med icke-diskonterade artiklar?
* **[!UICONTROL Satisfaction / Rating]**: Hur nöjda är era kunder med sina beställningar? Är det troligt att dina kunder talar om affärer för dig?

## Produktsegment

Med produktsegment kan ni fatta försäljningsbeslut.

* **[!UICONTROL Merchant / Brand]**: Säljer ett visst varumärke snabbare än resten? Vilka varumärken underpresterar?
* **[!UICONTROL Type / Category]**: Använder olika användarsegment olika typer av produkter? Vilka produktkategorier genererar de mest upprepade företagen?
* **[!UICONTROL Discount / Coupon Codes]**: Hindrar kampanjer försäljningen av icke-rabatterade produkter? Hur påverkar kuponger det upplevda värdet av dina produkter?
* **[!UICONTROL Social Activity]**: Finns det någon korrelation mellan den spännvidd som genereras i sociala medier och den mängd som säljs för en produkt?
* **[!UICONTROL Size / Variant]**: Hur stor är lagerkvoten som behövs för varje variant? Vilka varianter kan säljas till rabattpriser?

Om du är intresserad av att handla, se [hur man kan använda produktsegment för att få fler företag att komma tillbaka](../data-analyst/analysis/most-value-source-channel.md).

## Upprätta kundprofiler

Segmenteringsexperter kan vilja gå steget längre än endimensionella segment och börja skapa riktiga kundprofiler. Personer mellan 13 och 24 år som registrerat sig via en mobil enhet placerade till exempel i gruppen&quot;Ung och mobil&quot;. Hur fungerar den här gruppens beteende jämfört med resten av din användarbas?

Den här typen av analyser är vad marknadsförarna på Fortune 1000-företag gör hela dagen. Före lanseringen av molnbaserade plattformar för affärsinformation som [!DNL Commerce Intelligence]...det var i stort sett utom räckhåll för oss andra. Som tur är så är det inte längre så.

## Spåra nya segment

Det första steget för att segmentera mätvärdena med ovanstående mått är att se till att du spårar dessa data i databasen. Om den inte spåras kan du kontakta din tekniker och hitta ett sätt att börja spåra dessa data.

När du har bekräftat att data spåras i din databas, [kontakta supportteam](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) för att flytta måtten till [!DNL Commerce Intelligence] mått och diagram. Du kan också använda *Fälthantering* verktyg för att spåra fälten i [!DNL Commerce Intelligence].

## Relaterad

* [Optimera databasen för analys](../best-practices/opt-db-analysis.md)
