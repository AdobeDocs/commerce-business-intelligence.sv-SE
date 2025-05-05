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
>Kräver [administratörsbehörighet](../../administrator/user-management/user-management.md).

Ett mätvärde är ett mått. I SQL- och databasstrukturer fungerar ett mått som en lagrad fråga över en variabelperiod.

I [!DNL Commerce Intelligence] kan du använda mått för att [skapa diagram](../../data-user/reports/ess-rpt-build-visual.md). Måttet `revenue` är till exempel det totala antalet order. Måttet `average customer revenue per order` är det som genomsnittskunden spenderar per order.

När mätvärden används i rapporter kan de analyseras över en angiven tidsperiod och [filtreras eller segmenteras](../../best-practices/segment-filter.md) av olika kategorier. Överväg att analysera genomsnittliga kundintäkter grupperade efter kön - i det här fallet är `average customer revenue per order` måttet och kön är grupperingen.

## Definiera måttet {#define}

1. Klicka på **[!UICONTROL Data** > **Metrics]** om du vill skapa ett mått.

1. Klicka på **[!UICONTROL Create New Metric]**.

1. I listrutan klickar du på den tabell som innehåller den ursprungliga eller beräknade kolumnen som du vill använda för måttet.

1. Namnge mätvärdena.

   Adobe rekommenderar ett namn som i korthet talar om för dig vad måttet är. Till exempel: `Average Order Revenue`.

1. Nästa steg är att definiera vad mätvärdena gör. Ange måttets åtgärd, kolumnen `operation` och en `date`-dimension med hjälp av listrutemenyerna:

   * Välj en åtgärd:
      * `Count` - Den här åtgärden räknar antalet rader i en datatabell
      * `Max` - Max returnerar det maximala värdet för en specifik datakolumn
      * `Min` - Min returnerar det minsta värdet för en specifik datakolumn
      * `Sum` - Den här åtgärden summerar värdena i en specifik datakolumn
      * `Average` - Den här åtgärden beräknar medelvärdet för datakolumnvärdena
      * `Count Distinct Value` - Detta räknar det unika antalet värden i en specifik datakolumn
      * `Median` - Den här åtgärden beräknar medianen för datakolumnvärdena
      * `First and Third Quartiles` - De här åtgärderna beräknar den 25 respektive 75:e percentilen av datakolumnvärdena
      * `Tenth and Ninetieth Percentiles` - De här åtgärderna beräknar den 10 respektive 90:e percentilen för datakolumnvärdena

   * Välj en kolumn som åtgärden ska utföras på. Om du till exempel vill hitta din totala intäkt utför du en summaåtgärd i kolumnen `order total`.

     Om du redigerar ett befintligt mått kan du även [ändra måttets användningstabell](../../data-analyst/data-warehouse-mgr/change-metric-op-table.md) i det här avsnittet.

   * Välj en datumdimension som kan användas för att trenda måttet. Exempel: `order date`.

## Lägga till filter {#filters}

I avsnittet `Filter` kan du skapa ett filter eller använda en [sparad filteruppsättning](../../data-user/reports/ess-manage-data-filters.md) i måttet.

För måttet `average order revenue` vill du inte inkludera några testorder som kan ha gjorts när du konfigurerar din butik. Det skulle ge oss ett felaktigt resultat. Kan använda en filteruppsättning för att ta bort dessa order från datauppsättningen. När filtret har skapats gäller det alla diagram som har skapats med det här måttet.

I avsnittet `Filter Logic` kan du ytterligare definiera hur ett mätresultat ska fungera.

* &quot;\[`A`\] eller \[`B`\]&quot; tillåter alla data som uppfyller filtren \[`A`\] ELLER \[`B`\]
* &quot;\[`A`\] och \[`B`\]&quot; tillåter endast data som uppfyller båda filtren \[`A`\] och \[`B`\]
* &quot;(\[`A`\] och \[`B`\]) ELLER \[`C`\]&quot; tillåter endast data som antingen uppfyller båda filtren \[`A`\] och \[`B`\], eller bara uppfyller filtret \[&lbrace;5\]`C`

## Lägga till Dimensioner {#dimensions}

Avsnittet [`Dimensions`](../../data-analyst/data-warehouse-mgr/manage-data-dimensions-metrics.md) visar alla tillgängliga datamått för filtrering eller gruppering. Som standard listas alla tillgängliga datakolumner som dimensioner. Om du vill segmentera dina intäkter utifrån hänvisningskälla kan du göra det här.

Förutom att visa alla tillgängliga datakolumner som dimensioner, gissar [!DNL Commerce Intelligence] vid vilka kolumner som kan grupperas. *Om du vill segmentera eller gruppera data i rapporter* måste kolumner markeras som grupperbara.

## Slutför {#finish}

Förutom att definiera hur mätvärdena fungerar kan du även ange behörighetsnivåer i avsnittet `User Rights`. `Admin` användare har åtkomst till alla mått, men du måste ange vilka användare som kan använda måttet genom att markera rutan bredvid rätt grupp.

Om du redigerar ett befintligt mått kan du visa en lista med diagram (och vem som äger dem) som använder det här måttet i avsnittet `Dependent Charts`.

Ändringarna sparas automatiskt och mätvärdena är nu bra att använda.
