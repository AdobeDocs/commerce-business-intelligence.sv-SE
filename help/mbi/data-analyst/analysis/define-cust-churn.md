---
title: Definiera kundomsättning
description: Lär dig hur du konfigurerar en kontrollpanel som hjälper dig att definiera kundomsättning för dina transaktionskunder.
exl-id: fea8f7e9-c84c-4d49-a657-8b75140c113a
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager, Reports, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 0%

---

# Transactional Customer Churn

I det här avsnittet visas hur du konfigurerar en kontrollpanel som hjälper dig att definiera kundomsättning för dina transaktionskunder.

![](../../assets/churn-deashboard.png)

Den här analysen innehåller [avancerade beräknade kolumner](../data-warehouse-mgr/adv-calc-columns.md).

## Beräknade kolumner

Kolumner att skapa

* `customer_entity`-tabell
* `Customer's lifetime number of orders`
* Välj en definition: `Count`
* Välj en [!UICONTROL table]: `sales_flat_order`
* Välj en [!UICONTROL column]: **`entity_id`**
* [!UICONTROL Path]: sales_flat_order.customer_id = customer_entity.entity_id
* [!UICONTROL Filter]:
* Beställningar som räknas

* `sales_flat_order`-tabell
* `Customer's lifetime number of orders`
* Välj en definition: Förenad kolumn
* Välj en [!UICONTROL table]: `customer_entity`
* Välj en [!UICONTROL column]: `Customer's lifetime number of orders`
* [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
* [!UICONTROL Filter]: `Orders we count`

* `Seconds since created_at`
* Välj en definition: `Age`
* Välj en [!UICONTROL column]: `created_at`

* **`Customer's order number`** har skapats av en analytiker som en del av din **[DEFINING CHURN]**-biljett
* **`Is customer's last order`** har skapats av en analytiker som en del av din **[DEFINING CHURN]**-biljett
* **`Seconds since previous order`** har skapats av en analytiker som en del av din **[DEFINING CHURN]**-biljett
* **`Months since order`** har skapats av en analytiker som en del av din **[DEFINING CHURN]**-biljett
* **`Months since previous order`** har skapats av en analytiker som en del av din **[DEFINING CHURN]**-biljett

## Mått

Inga nya mätvärden!

>[!NOTE]
>
>Se till att [lägga till alla nya kolumner som mått i mätvärden](../data-warehouse-mgr/manage-data-dimensions-metrics.md) innan du skapar nya rapporter.

## Rapporter

* **Sannolikhet för inledande upprepningsorder**
* Mått A: Upprepade order vid heltids användning
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* Mått B: Heltidsbeställningar
* [!UICONTROL Metric]: Antal order

* [!UICONTROL Formula]: Sannolikhet för inledande upprepningsorder
* &#x200B;
  [!UICONTROL -formel]: `A/B`
* &#x200B;
  [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* &#x200B;
  [!UICONTROL Chart type]: `Scalar`

* **Sannolikhet för upprepade order som har angetts i månader sedan ordern**
* Mått A: Upprepa order efter månader sedan föregående order (dölj)
* [!UICONTROL Metric]: `Number of orders`
* &#x200B;
  [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* Mått B: Sista beställningen per månad sedan beställningen (dölj)
* [!UICONTROL Metric]: `Number of orders`
* &#x200B;
  [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]: `Is customer's last order? (Yes/No) = Yes`

* Mått C: Upprepade order (dölj)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* &#x200B;
  [!UICONTROL Group by]: `Independent`

* Mått D: Sista ordern för heltidsredigering (dölj)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Is customer's last order? (Yes/No) = Yes`

* &#x200B;
  [!UICONTROL Group by]: `Independent`

* [!UICONTROL Formula]: Sannolikhet för inledande upprepningsorder
* &#x200B;
  [!UICONTROL -formel]: `(C-A)/(C+D-A-B)`
* &#x200B;
  [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]: `All time`
* &#x200B;
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Months since previous order`
* Visa överkant.nederkant: De 24 översta kategorierna, sorterade efter kategorinamn

* &#x200B;
  [!UICONTROL Chart type]: `Line`

Den inledande sannolikhetsrapporten för upprepad order representerar totalt antal upprepade order/totalt antal order. Varje order är en möjlighet att göra en upprepad order. Antalet upprepade order är delmängden av de order som faktiskt gör det.

Formeln som du använder förenklar till (Totalt antal upprepade order som har inträffat efter X månader)/ (Totalt antal order som är minst X månader gamla). Det visar att det historiskt sett har gått X månader sedan en beställning och att det finns en Y-procentig chans att användaren lägger en annan order.

När du har skapat din kontrollpanel är den vanligaste frågan: Hur använder jag den för att fastställa ett tröskelvärde för bortfall?

**Det finns inget &quot;rätt svar&quot; på detta.** Adobe rekommenderar dock att du söker efter den punkt där raden korsar värdet som är hälften av den inledande upprepningssannolikheten. Här kan du säga: &quot;Om en användare tänker göra en ny beställning, skulle han eller hon antagligen ha gjort det vid det här laget.&quot; I slutändan är målet att välja tröskeln där det är rimligt att gå över från&quot;kvarhållande&quot; till&quot;reaktivering&quot;.

När du har kompilerat alla rapporter kan du ordna dem på kontrollpanelen som du vill. Resultatet kan se ut som bilden högst upp på sidan

[Kontakta support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=sv-SE) om du får frågor under arbetet med att skapa den här analysen, eller om du bara vill engagera Professional Services-teamet.
