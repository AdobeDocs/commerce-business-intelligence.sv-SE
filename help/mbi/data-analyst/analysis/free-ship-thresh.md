---
title: Gräns för fri frakt
description: Lär dig hur du konfigurerar en kontrollpanel som spårar prestanda för ditt tröskelvärde för fri frakt.
exl-id: a90ad89b-96d3-41f4-bfc4-f8c223957113
role: Admin,  User
feature: Data Warehouse Manager, Dashboards, Reports
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---

# Fri frakt

>[!NOTE]
>
>Det här avsnittet innehåller instruktioner för klienter som använder den ursprungliga arkitekturen och den nya arkitekturen. Du använder den nya arkitekturen om du har avsnittet `Data Warehouse Views` tillgängligt efter att du har valt `Manage Data` i huvudverktygsfältet.

I det här avsnittet visas hur du konfigurerar en kontrollpanel som spårar prestanda för ditt tröskelvärde för fri frakt. Den här instrumentpanelen, som visas nedan, är ett bra sätt att testa två kostnadsfria leveranströsklar. Företaget kan till exempel vara osäkert om du ska erbjuda fri frakt på 50 eller 100 dollar. Du bör utföra ett A/B-test av två slumpmässiga deluppsättningar av dina kunder och utföra analysen i [!DNL Commerce Intelligence].

Innan du börjar vill du identifiera två separata tidsperioder där du har haft olika värden för butikens tröskelvärde för fri frakt.

![Diagram över analys av tröskelvärde för fri frakt och fördelning av ordervärde](../../assets/free_shipping_threshold.png)

Den här analysen innehåller [avancerade beräknade kolumner](../data-warehouse-mgr/adv-calc-columns.md).

## Beräknade kolumner

Om du använder den ursprungliga arkitekturen (om du t.ex. inte har alternativet `Data Warehouse Views` på menyn `Manage Data`) vill du kontakta supportteamet för att bygga ut kolumnerna nedan. På den nya arkitekturen kan dessa kolumner skapas från sidan `Manage Data > Data Warehouse`. Detaljerade instruktioner finns nedan.

* **`sales_flat_order`**-tabell
   * Den här beräkningen skapar buketter i steg i förhållande till dina vanliga kundvagnsstorlekar. Detta kan variera från steg som 5, 10, 50, 100

* **`Order subtotal (buckets)`** Ursprunglig arkitektur: skapad av en analytiker som en del av din `[FREE SHIPPING ANALYSIS]`-biljett
* **`Order subtotal (buckets)`** Ny arkitektur:
   * Som nämnts ovan skapar den här beräkningen bucklor i steg i förhållande till de typiska kundvagnarna. Om du har en intern delsummeringskolumn som `base_subtotal` kan den användas som grund för den nya kolumnen. Annars kan det vara en beräknad kolumn som utesluter frakt och rabatter från intäkter.

  >[!NOTE]
  >
  >&quot;Bucket&quot;-storlekarna beror på vad som passar dig som kund. Du kan börja med din `average order value` och skapa vissa bucklor som är mindre än och större än den mängden. När du tittar på beräkningen nedan ser du hur enkelt det är att kopiera en del av frågan, redigera den och skapa ytterligare bucklor. Exemplet görs i steg om 50.

   * `Column type - Same table, Column definition - Calculation, Column Inputs-` `base_subtotal` eller `calculated column`, `Datatype`: `Integer`
   * [!UICONTROL Calculation]: `case when A >= 0 and A<=200 then 0 - 200`
when `A< 200` och `A <= 250` then `201 - 250`
när `A<251` och `A<= 300` sedan `251 - 300`
när `A<301` och `A<= 350` sedan `301 - 350`
när `A<351` och `A<=400` sedan `351 - 400`
när `A<401` och `A<=450` sedan `401 - 450`
else &#39;över 450&#39;
end


## Mått

Inga nya mätvärden!

>[!NOTE]
>
>Se till att [lägga till alla nya kolumner som mått i mätvärden](../data-warehouse-mgr/manage-data-dimensions-metrics.md) innan du skapar nya rapporter.

## Rapporter

* **Genomsnittligt ordervärde med leveransregel A**
   * [!UICONTROL Metric]: `Average order value`

* Mått `A`: `Average Order Value`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
  [!UICONTROL Interval]: `None`
* 
  [!UICONTROL Chart Type]: `Scalar`

* **Antal order per delsummeringsbucket med leveransregel A**
   * [!UICONTROL Metric]: `Number of orders`

  >[!NOTE]
  >
  >Du kan skära bort slutänden genom att visa de översta `X` `sorted by` `Order subtotal` (hinkar) i `Show top/bottom`.

* Mått `A`: `Number of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* 
  [!UICONTROL Chart Type]: `Column`

* **Procent av order per delsumma med leveransregel A**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * 
     [!UICONTROL Group by]: `Independent`
   * [!UICONTROL Formula]: `(A / B)`
   * 
     [!UICONTROL Format]: `%`

* Mått `A`: `Number of orders by subtotal (hide)`
* Mått `B`: `Total number of orders (hide)`
* [!UICONTROL Formula]: `% of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* 
  [!UICONTROL Chart Type]: `Line`

* **Procent av order med en delsumma som överstiger leveransregel A**
   * [!UICONTROL Metric]: `Number of orders`
   * 
     [!UICONTROL Perspective]: `Cumulative`

   * [!UICONTROL Metric]: `Number of orders`
   * 
     [!UICONTROL Group by]: `Independent`

   * [!UICONTROL Formula]: `1- (A / B)`
   * 
     [!UICONTROL Format]: `%`

* Mått `A`: `Number of orders by subtotal`
* Mått `B`: `Total number of orders (hide)`
* [!UICONTROL Formula]: `% of orders`
* [!UICONTROL Time period]: `Time period with shipping rule A`
* 
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Order subtotal (buckets)`
* 
  [!UICONTROL Chart Type]: `Line`


Upprepa stegen ovan och rapporterna för Leverans B och tidsperioden med leveransregel B.

När du har kompilerat alla rapporter kan du ordna dem på kontrollpanelen som du vill. Resultatet kan se ut som bilden högst upp på den här sidan.
