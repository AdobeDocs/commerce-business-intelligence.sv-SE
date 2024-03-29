---
title: Skapa mätvärden
description: Lär dig hur du använder statistik för att skapa diagram.
exl-id: d4c25546-3c51-4d32-b9d8-c424ec103be5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 0%

---

# Skapa mätvärden

>[!NOTE]
>
>Kräver [Administratörsbehörigheter](../../administrator/user-management/user-management.md).

Ett mätvärde är ett mått. I SQL- och databasstrukturer fungerar ett mått som en lagrad fråga över en variabelperiod.

I [!DNL Commerce Intelligence]kan du använda mätvärden för att [skapa diagram](../../data-user/reports/ess-rpt-build-visual.md). Exempelvis måttet `revenue` är det totala antalet order. Måttet `average customer revenue per order` är vad den genomsnittliga kunden spenderar per order.

När de används i rapporter kan mätvärden analyseras över en angiven tidsperiod och [filtrerad eller segmenterad](../../best-practices/segment-filter.md) efter olika kategorier. Överväg att analysera genomsnittliga kundintäkter grupperade efter kön - i det här fallet `average customer revenue per order` är mätvärdet och kön är grupperingen.

## Definiera måttet {#define}

1. Om du vill skapa ett mått klickar du på **[!UICONTROL Data** > **Metrics]**.

1. Klicka på **[!UICONTROL Create New Metric]**.

1. I listrutan klickar du på den tabell som innehåller den ursprungliga eller beräknade kolumnen som du vill använda för måttet.

1. Namnge mätvärdena.

   Adobe rekommenderar ett namn som i korthet talar om för dig vad måttet är. Exempel: `Average Order Revenue`.

1. Nästa steg är att definiera vad mätvärdena gör. Definiera måttets åtgärd med hjälp av listrutemenyerna, `operation` kolumn, och en `date` dimension:

   * Välj en åtgärd:
      * `Count` - Den här åtgärden räknar antalet rader i en datatabell
      * `Max` - Max returnerar det maximala värdet för en viss datakolumn
      * `Min` - Min returnerar det minsta värdet för en viss datakolumn
      * `Sum` - Den här åtgärden summerar värdena i en viss datakolumn
      * `Average` - Den här åtgärden beräknar medelvärdet för datakolumnvärdena
      * `Count Distinct Value` - Detta räknar det unika antalet värden i en specifik datakolumn
      * `Median` - Den här åtgärden beräknar medianvärdet för datakolumnvärdena
      * `First and Third Quartiles` - Dessa åtgärder beräknar den 25 respektive 75:e percentilen av datakolumnvärdena
      * `Tenth and Ninetieth Percentiles` - Dessa åtgärder beräknar den 10 respektive 90:e percentilen av datakolumnvärdena

   * Välj en kolumn som åtgärden ska utföras på. Om du till exempel vill hitta den totala intäkten utför du en summaåtgärd på `order total` kolumn.

     Om du redigerar ett befintligt mått kan du även [ändra måttets driftstabell](../../data-analyst/data-warehouse-mgr/change-metric-op-table.md) i det här avsnittet.

   * Välj en datumdimension som kan användas för att trenda måttet. Exempel, `order date`.

## Lägga till filter {#filters}

The `Filter` kan du skapa ett filter eller använda [sparad filteruppsättning](../../data-user/reports/ess-manage-data-filters.md) till dina mätvärden.

För `average order revenue` skulle du inte vilja inkludera några testorder som kan ha gjorts när du konfigurerar din butik - det skulle ge oss ett felaktigt resultat. Kan använda en filteruppsättning för att ta bort dessa order från datauppsättningen. När filtret har skapats gäller det alla diagram som har skapats med det här måttet.

The `Filter Logic` är där du kan definiera hur ett mätresultat ska fungera.

* &quot;\[`A`\] eller \[`B`\]&quot; tillåter alla data som uppfyller filtren \[`A`\] ELLER \[`B`\]
* &quot;\[`A`\] och \[`B`\] tillåter bara data som uppfyller båda filtren \[`A`\] och \[`B`\]
* &quot;(\[`A`\] och \[`B`\]) ELLER \[`C`\] tillåter bara data som antingen uppfyller båda filtren \[`A`\] och \[`B`\], eller uppfyller filtret \[`C`\] ensam

## Lägga till Dimensioner {#dimensions}

The [`Dimensions`](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) I visas alla tillgängliga datamått för filtrering eller gruppering. Som standard anges alla tillgängliga datakolumner som dimensioner. Om du vill segmentera dina intäkter utifrån hänvisningskälla kan du göra det här.

Förutom att ange alla tillgängliga datakolumner som dimensioner, [!DNL Commerce Intelligence] gissar på vilka kolumner som kan grupperas. *Segmentera eller gruppera data i rapporter*, kolumner måste markeras som grupperbara.

## Slutför {#finish}

Förutom att definiera hur mätvärdena fungerar kan du även ange behörighetsnivåer i `User Rights` -avsnitt. while `Admin` -användare har tillgång till alla mätvärden, måste du ange vilka användare som kan använda dessa mätvärden genom att markera rutan bredvid rätt grupp.

Om du redigerar ett befintligt mått kan du visa en lista med diagram (och vem som äger dem) som använder det här måttet i `Dependent Charts` -avsnitt.

Ändringarna sparas automatiskt och mätvärdena är nu bra att använda.
