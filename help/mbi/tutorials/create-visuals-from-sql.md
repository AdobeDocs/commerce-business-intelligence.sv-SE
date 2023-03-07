---
title: Skapa visualiseringar från SQL-frågor
description: Lär dig bekanta dig med den terminologi som används i SQL Report Builder och ge dig en gedigen grund för att skapa SQL-visualiseringar.
exl-id: 9b9bc205-5b64-4e64-8d23-057072e5dd72
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '626'
ht-degree: 0%

---

# Skapa visualiseringar från SQL-frågor

Målet med den här självstudiekursen är att bekanta dig med den terminologi som används i `SQL Report Builder` och ger dig en stabil grund för att skapa `SQL visualizations`.

The [`SQL Report Builder`](../data-analyst/dev-reports/sql-rpt-bldr.md) är en rapportbyggare med alternativ: du kan köra en fråga enbart i syfte att hämta en datatabell, eller så kan du omvandla dessa resultat till en rapport. I den här självstudiekursen beskrivs hur du skapar en visualisering från en SQL-fråga.

## Terminologi

Innan du börjar den här självstudiekursen ska du läsa om följande terminologi som används i `SQL Report Builder`.

- `Series`: Kolumnen som du vill mäta kallas en serie i SQL Report Builder. Vanliga exempel är `revenue`, `items sold`och `marketing spend`. Minst en kolumn måste anges som en `Series` för att skapa en visualisering.

- `Category`: Kolumnen som du vill använda för att segmentera data kallas `Category` Det här är precis som `Group By` i [`Visual Report Builder`](../data-user/reports/ess-rpt-build-visual.md). Om du till exempel vill segmentera kundernas livstidsintäkter med hjälp av deras anskaffningskälla anges kolumnen som innehåller anskaffningskällan som `Category`. Mer än en kolumn kan anges som en `Category`.

>[!NOTE]
>
>Datum och tidsstämplar kan också användas som `Categories`. De är bara en annan datakolumn i frågan och måste formateras och ordnas som du vill i själva frågan.

- `Labels`: De används som x-axeletiketter. När du analyserar datatrender över tid anges år- och månadskolumnerna som etiketter. Mer än en kolumn kan anges till Label.

## Steg 1: Skriv frågan

Tänk på följande:

- The `SQL Report Builder` använder [`Redshift SQL`](https://docs.aws.amazon.com/redshift/latest/dg/c_redshift-and-postgres-sql.html).

- Om du skapar en rapport med en tidsserie ska du se till att `ORDER BY` tidsstämpelkolumnerna. Detta garanterar att tidsstämplarna ritas i rätt ordning i rapporten.

- The `EXTRACT` är bra att använda för att analysera dag, vecka, månad eller år i tidsstämpeln. Detta är användbart när `time interval` som du vill använda i rapporten är `daily`, `weekly`, `monthly`, eller `yearly`.

Öppna `SQL Report Builder` genom att klicka **[!UICONTROL Report Builder** > **SQL Report Builder]**.

Ta som exempel den här frågan som returnerar det totala antalet artiklar som sålts per månad för varje produkt:

```sql
    SELECT SUM("qty") AS "Items Sold", "products's name" AS "product name",
    EXTRACT(year from "Order date") AS "year",
    EXTRACT(month from "Order date") AS "month"
    FROM "items"
    WHERE "products's name" LIKE '%Jeans'
    GROUP BY  "products's name", "year","month"
    ORDER BY "year" ASC,"month" ASC
    LIMIT 3500
```

Den här frågan returnerar den här resultattabellen:

![](../assets/SQL_results_table.png)

## Steg 2: Skapa visualiseringen

Med dessa resultat *hur skapar du visualiseringen?* Klicka på **[!UICONTROL Chart]** i `Results` fönster. Här visas `Chart settings` -fliken.

När en fråga körs för första gången kan rapporten se ogenomskinlig ut eftersom alla kolumner i frågan är plottade som en serie:

![](../assets/SQL_initial_report_results.png)

I det här exemplet vill du att det här ska vara ett linjediagram som utvecklas över tid. Använd följande inställningar för att skapa den:

- `Series`: Välj `Items sold` kolumn som `Series` eftersom du vill mäta det. När du har definierat en `Series` visas en enda rad i rapporten.

- `Category`: I det här exemplet vill du visa varje produkt som en rad i rapporten. För att göra detta ställer du in `Product name` som `Category`.

- `Labels`: Använda kolumnerna `year` och `month` som etiketter på x-axeln som ska kunna visas `Items Sold` som trender över tid.

>[!NOTE]
>
>Frågan måste innehålla en `ORDER BY` -satsen på etiketterna om de `date`/`time` kolumner.

Nedan följer en kort titt på hur du skapade den här visualiseringen, från att köra frågan till att konfigurera rapporten:

![](../assets/SQL_report_settings.gif)

## Steg 3: Välj en `Chart Type`

I det här exemplet används `Line` diagramtyp. Så här använder du en annan `chart type`klickar du på ikonerna ovanför avsnittet med diagramalternativ för att ändra det:

![](../assets/Chart_types.png)

## Steg 4: Spara visualiseringen

Om du vill använda rapporten igen ger du rapporten ett namn och klickar på **[!UICONTROL Save]** i det övre högra hörnet.

I listrutan väljer du `Chart` som `Type` och sedan en kontrollpanel där du vill spara rapporten.

## Grattis! Du är färdig.

Vill du ta ett steg längre? Kolla in [god praxis för frågeoptimering](../best-practices/optimizing-your-sql-queries.md).
