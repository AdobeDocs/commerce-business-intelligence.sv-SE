---
title: Definiera kundomsättning
description: Lär dig hur du skapar en kontrollpanel som hjälper dig att definiera kundomsättning för dina transaktionskunder.
exl-id: fea8f7e9-c84c-4d49-a657-8b75140c113a
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# Transactional Customer Churn

I den här artikeln visas hur du konfigurerar en kontrollpanel som hjälper dig att definiera kundomsättning för dina transaktionskunder.

![](../../assets/churn-deashboard.png)

Denna analys innehåller [avancerade beräknade kolumner](../data-warehouse-mgr/adv-calc-columns.md).

## Beräknade kolumner

Kolumner att skapa

* `customer_entity` table
* `Customer's lifetime number of orders`
* Välj en definition: `Count`
* Välj en [!UICONTROL table]: `sales_flat_order`
* Välj en [!UICONTROL column]: **`entity_id`**
* [!UICONTROL Path]: sales_flat_order.customer_id = customer_entity.entity_id
* [!UICONTROL Filter]:
* Beställningar som räknas

* `sales_flat_order` table
* `Customer's lifetime number of orders`
* Välj en definition: Kopplad kolumn
* Välj en [!UICONTROL table]: `customer_entity`
* Välj en [!UICONTROL column]: `Customer's lifetime number of orders`
* [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
* [!UICONTROL Filter]: `Orders we count`

* `Seconds since created_at`
* Välj en definition: `Age`
* Välj en [!UICONTROL column]: `created_at`

* **`Customer's order number`** skapas av en analytiker som en del av **[DEFINIERA KURN]** biljett
* **`Is customer's last order`** skapas av en analytiker som en del av **[DEFINIERA KURN]** biljett
* **`Seconds since previous order`** skapas av en analytiker som en del av **[DEFINIERA KURN]** biljett
* **`Months since order`** skapas av en analytiker som en del av **[DEFINIERA KURN]** biljett
* **`Months since previous order`** skapas av en analytiker som en del av **[DEFINIERA KURN]** biljett

## Mått

Inga nya mätvärden!

>[!NOTE]
>
>Se till att [lägga till alla nya kolumner som dimensioner till mått](../data-warehouse-mgr/manage-data-dimensions-metrics.md) innan du skapar nya rapporter.

## Rapporter

* **Sannolikhet för inledande upprepad order**
* Mått A: Upprepa order hela tiden
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* Mått B: Heltidsbeställningar
* [!UICONTROL Metric]: Antal order

* [!UICONTROL Formula]: Sannolikhet för inledande upprepad order
* 
   [!UICONTROL-formel]: `A/B`
* 

   [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 

   [!UICONTROL Chart type]: `Scalar`

* **Sannolikhet för upprepade order som har angetts månader sedan ordern**
* Mått A: Upprepa order efter månader sedan föregående order (dölj)
* [!UICONTROL Metric]: `Number of orders`
* 
   [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* Mått B: Senaste order per månad sedan ordern (dölj)
* [!UICONTROL Metric]: `Number of orders`
* 
   [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]: `Is customer's last order? (Yes/No) = Yes`

* Mått C: Upprepade order hela tiden (dölj)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* 

   [!UICONTROL Group by]: `Independent`

* Mått D: Senaste order hela tiden (dölj)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Is customer's last order? (Yes/No) = Yes`

* 

   [!UICONTROL Group by]: `Independent`

* [!UICONTROL Formula]: Sannolikhet för inledande upprepad order
* 
   [!UICONTROL-formel]: `(C-A)/(C+D-A-B)`
* 

   [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Months since previous order`
* Visa top.bottom: De 24 viktigaste kategorierna, sorterade efter kategorinamn

* 

   [!UICONTROL Chart type]: `Line`

Den inledande sannolikhetsrapporten för upprepad order representerar totalt antal upprepade order/totalt antal order. Varje beställning ger möjlighet att göra en upprepad beställning. antalet upprepade order är delmängden av de som faktiskt gör det.

Formeln som du använder förenklar till (Totalt antal upprepade order som har inträffat efter X månader)/ (Totalt antal order som är minst X månader gamla). Det visar att det historiskt sett har gått X månader sedan en beställning och att det finns en Y-procentig chans att användaren lägger en annan order.

När du väl har skapat din kontrollpanel är den vanligaste frågan: Hur använder jag detta för att fastställa ett tröskelvärde för bortfall?

**Det finns inget&quot;rätt svar&quot; på detta.** Adobe rekommenderar dock att du hittar den punkt där raden korsar värdet som är hälften av den inledande upprepningssannolikheten. Här kan du säga: &quot;Om en användare tänker göra en ny beställning, skulle han eller hon antagligen ha gjort det vid det här laget.&quot; I slutändan är målet att välja tröskeln där det är rimligt att gå över från&quot;kvarhållande&quot; till&quot;reaktivering&quot;.

När du har kompilerat alla rapporter kan du ordna dem på kontrollpanelen som du vill. Resultatet kan se ut som bilden högst upp på sidan

Om du stöter på några frågor när du skapar den här analysen eller bara vill engagera Professional Services-teamet, [kontakta support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
