---
title: Årsrapporter, månadsrapporter och veckorapporter
description: Lär dig hur du enkelt ser trender över tid och ändrar perspektiv för tidsperioder som du kanske vill jämföra.
exl-id: 74cf11c3-7ce0-477f-9a28-9d782e5da3d9
role: Admin, Data Architect, Data Engineer, Leader, User
feature: Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 0%

---

# Rapportera över tidsperioder

>[!NOTE]
>
>Det här avsnittet innehåller instruktioner för klienter som använder den ursprungliga arkitekturen och den nya arkitekturen. Du är på den [nya arkitekturen](../../administrator/account-management/new-architecture.md) om du har avsnittet [!DNL _Data Warehouse Views_] tillgängligt när du har valt [!DNL Manage Data] i huvudverktygsfältet.

Med rapportverktyget kan du enkelt se trender över tid och ändra perspektivet för tidsperioder som du kanske vill jämföra. I det här avsnittet visas hur du konfigurerar en kontrollpanel så att du kan skapa rapporter för en vecka, en månad i taget och en år i taget.

![](../../assets/Wow__mom__yoy.png)

Innan du börjar bör du granska perspektiv mer i detalj [här](../../tutorials/using-visual-report-builder.md) och oberoende tidsalternativ [här](../../tutorials/time-options-visual-rpt-bldr.md).

Den här analysen innehåller [avancerade beräknade kolumner](../data-warehouse-mgr/adv-calc-columns.md).

## Beräknade kolumner

* **`Sales_flat_order`**-tabell
* **Ursprunglig arkitektur:** nedanstående kolumner skapas av en analytiker som en del av din `[YoY WoW MoM ANALYSIS]` biljett
* `created_at (month-day)`
* `created_at (month)`
* `created_at (day of the month)`
* `created_at (day of the week)`
* `created_at (hour of the day)`

* **Ny arkitektur:** SQL listas nedan med ett foto av ett exempel för hur du skapar beräkningen
   * `created_at (month-day)` [!UICONTROL Calculation]: **to_char(A, &#39;mm-dd&#39;)**
   * `created_at (month)` [!UICONTROL Calculation]: **to_char(A, &#39;mm-month&#39;)**
   * `created_at (day of the month)`&lt; [!UICONTROL Calculation]: **till_char(A, dd)**
   * `created_at (day of the week)` [!UICONTROL Calculation]: **to_char(A, &#39;d-Day&#39;)**
   * **`created_at (hour of the day)` [!UICONTROL Calculation]: &#x200B;** to_char(A, &#39;hh24&#39;)**
     ![](../../assets/new-arch-create-calc.png)

## Mått

Ingen.

>[!NOTE]
>
>Se till att [lägga till alla nya kolumner som mått i mätvärden](../data-warehouse-mgr/manage-data-dimensions-metrics.md) innan du skapar nya rapporter.

## Rapporter

* **Y-diagram**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Time options]: `Time range (Custom)`: `2 years ago to 1 year ago`

   * [!UICONTROL Show top/bottom]: 100 % i topp, sorterat efter **`created_at (month-day)`***

* Mått `A`: `This year`
* Mått `B`: `Last year`
* [!UICONTROL Time period]: `1 year ago to 0 years ago`
* &#x200B;
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `created_at (month-day)`
* &#x200B;
  [!UICONTROL Chart Type]: `Line`

* **MoM-diagram**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * Tidsalternativ: `Time range (Custom)`: `2 months ago to 1 month ago`

   * Visa överkant/underkant: 100 % överkant sorterat efter **`created_at (day of month)`***

* Mått `A`: Den här månaden*
* Mått `B`: förra månaden*
* [!UICONTROL Time period]: för en månad sedan till för 0 månader sedan
* &#x200B;
  [!UICONTROL Interval]: None
* [!UICONTROL Group by]: `created_at (day of month)`
* &#x200B;
  [!UICONTROL Chart Type]: Line

* **WoW-diagram**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Time options]: `Time range (Custom)`: `2 weeks ago to 1 week ago`

   * [!UICONTROL Show top/bottom]: 100 % i topp, sorterat efter `created_at (day of week)`

* Mått `A`: `This week`
* Mått `B`: `Last week`
* [!UICONTROL Time period]: `1 week ago to 0 weeks ago`
* &#x200B;
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `created_at (day of week)`
* &#x200B;
  [!UICONTROL Chart Type]: `Line`

* **DoD-diagram**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Time options]: `Time range (Custom)`: `2 days ago to 1 day ago`

   * [!UICONTROL Show top/bottom]: 100 % i topp, sorterat efter `created_at (hour of day)`

* Mått `A`: `Today`
* Mått B: `Yesterday`
* [!UICONTROL Time period]: `1 day ago to 0 days ago`
* &#x200B;
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `created_at (hour of day)`
* &#x200B;
  [!UICONTROL Chart Type]: `Line`

När du har kompilerat alla rapporter kan du ordna dem på kontrollpanelen som du vill. Resultatet kan se ut som bilden högst upp på den här sidan.
