---
title: Arbeta med SQL Report Builder
description: Lär dig hur du granskar data och mätvärden med SQL Report Builder så att du kan jämföra resultaten med data från din lokala databas.
exl-id: d1d9e099-4138-43e6-aaec-6f15ebc5c4d4
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '514'
ht-degree: 0%

---

# `SQL Report Builder`

The `SQL Report Builder` används främst för att skapa nya rapporter och iterera på analyser, men det kan också användas för att effektivt granska data och mätvärden. I följande information förklaras hur du granskar data och mätvärden med `SQL Report Builder` så att du kan jämföra resultaten med data från din lokala databas.

## Fråga ett mått

Öppna `SQL Report Builder` genom att navigera till **[!UICONTROL Report Builder > SQL Report Builder > Create Report]**. Du kan använda sidofältet i SQL-redigeraren för att infoga ett mått direkt i frågan genom att hålla markören över mätvärdet och klicka **[!UICONTROL Insert]**. Då läggs frågedefinitionen för det måttet till i redigeraren. Definitionen innehåller följande komponenter:

- The **måttåtgärd** som utförs, vilket anges av SUM() i exemplet nedan.
- The **tabell på** vilket mätvärdet är skapat, vilket anges av FROM-satsen.
- Alla **filter (och filteruppsättningar)** som har lagts till i måttet, vilket anges av WHERE-satsen i exemplet nedan.
- Komponenten i **tidsstämpel** (år, månad) som uppgifterna ska beställas på, vilket anges av ORDER BY-satsen i exemplet nedan.

Om du vill få en tydligare vy över frågan kan du ändra hur den visas i frågefältet. När du är klar väljer du `Run Query`. Resultatet fylls i som en tabell i rapportpanelen nedanför frågan.

![](../../assets/run-query-results.gif)

## Begränsa frågan

Om du försöker hitta en viss diskrepans eller datauppsättning bör du begränsa frågan till ett visst prov för att kontrollera mot den lokala databasen. Du kan göra detta genom att redigera frågan så att den matchar dina önskade begränsningar. I följande exempel begränsar du frågan till att endast inkludera intäkter från 1 januari 2013 eller senare. När du har uppdaterat frågan väljer du **[!UICONTROL Run Query]** igen för att uppdatera resultaten.

![](../../assets/restricting-query.gif)

## Spara och exportera

När rapporten uppfyller dina behov kan du spara den på en kontrollpanel genom att ge rapporten ett tydligt namn och klicka på **[!UICONTROL Save]** och välja vilken typ av rapport du vill spara och kontrollpanelen. När du granskar mätvärden rekommenderar Adobe att du sparar rapporten som `Table` och spara det på en testpanel.

När rapporten har sparats navigerar du till den instrumentpanelen genom att välja `Go to Dashboard`. Därifrån kan du exportera data genom att hitta rapporten och välja **[!UICONTROL Options gear > Full `.csv`Exportera]** eller **[!UICONTROL Full Excel Export]**.

![](../../assets/export-dboard-data.gif)

## Egna frågor

Du kan också skriva egna frågor och exportera resultaten som ska jämföras med den lokala databasen. Efter [riktlinjer för frågeoptimering](../../best-practices/optimizing-your-sql-queries.md)skriver du en fråga i SQL-redigeraren. Du kan använda knapparna högst upp i sidofältet för att växla mellan listor med tabeller och mätvärden som är tillgängliga för användning i `SQL Report Builder` och lägga till dem i din fråga. När din anpassade fråga passar dina behov kan du spara rapporten och exportera dessa data från kontrollpanelen.

### Fortfarande stumpen?

Om du hittar en diskrepans efter att ha granskat dina data kan du titta på [Kontakta support: Dataavvikelser](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-data-discrepancies.html?lang=en) om du vill ha mer information om vad du ska göra härnäst.
