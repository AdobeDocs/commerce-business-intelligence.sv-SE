---
title: Bygga en kontrollpanel för investerare
description: Lär dig hur du skapar en instrumentpanel för investerare.
exl-id: 917e7628-3498-4413-a7e1-61799989a7dd
role: Admin, Data Architect, Data Engineer, User
feature: Dashboards, Data Integration
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '284'
ht-degree: 0%

---

# Bygg Investor Dashboard

Många kunder arbetar med investerare och behöver dela information från plattformen, men de instrumentpaneler ni skapar för att fatta vardagliga affärsbeslut kanske inte är vad en investerare är ute efter. Nedan beskrivs några tips om hur du kan skapa en kontrollpanel som är omfattande men enkel och idealisk för delning med aktiva och potentiella investerare.

Här är vad du behöver skapa rapporter för din instrumentpanel för investerare:

## Skalbara rapporter

* **[!UICONTROL All-time revenue]**
* **[!UICONTROL Distinct buyers]**
* **[!UICONTROL All-time number of orders]**
* **[!UICONTROL AOV]**
* **[!UICONTROL Items sold]**

## Visuella rapporter

* **[!UICONTROL Revenue by quarter]**
   * Mått - intäkt
* **[!UICONTROL Revenue from 1st time orders vs repeat orders]**
   * Mått - Inkomster av förstagångsorder
   * Filter - användarens ordernummer är lika med 1
   * Mått 2 - Upprepa orderintäkt
      * Filter - användarens ordernummer är större än 1
   * Avmarkera kryssrutan för flera Y-axlar
   * Ändra till ett staplat stapeldiagram
* **[!UICONTROL AOV by quarter]**
   * Mått 1 - Intäkter
      * Dölj det här måttet
   * Mått 2 - Antal order
      * Dölj det här måttet
   * Formel - AOV
      * A/B
* **[!UICONTROL All-time revenue by source]**
   * Mått - intäkt
   * Gruppera efter kundens `utm_source`
* **[!UICONTROL Revenue from top 10 products]**
   * Mått - produktintäkter
      * Dölj diagrammet
      * Gruppera efter produktnamn. Välj alla produkter.
      * Ställ in tidsintervallet till heltid
      * Ange tidsintervallet till Ingen
      * Visa bara de tio främsta sorterade efter produktvinst i Visa topp/botten
* **[!UICONTROL Cumulative distinct buyers by quarter]**
   * Metrisk - distinkta köpare
      * Perspektiv - ackumulerat
* **[!UICONTROL Site visits - New vs. repeat by month]**
* Sessioner

Med [!DNL Google Analytics] kan du lägga in rapporter om:

* Besök
* Konverteringsgrad

Med [Commerce Data Enrichment Services](https://business.adobe.com/products/magento/magento-commerce.html)kan du ta med rapporter om:

* Unika kunder per stat/region, ålder, kön.

## Andra tips

* Använd en tydlig och koncis [namnkonvention](../best-practices/naming-elements.md)
* Dela instrumentpanelen med investeraranvändare
* Eller skicka det via **[!UICONTROL Automated email summary]**(../data-user/export-data/email-summaries.md)
* Skapa bara en kontrollpanel. Detta gör innehållet enklare att underhålla och du vet exakt vad era investerare tittar på.

Ordna dina rapporter noggrant och var uppmärksam på detaljerna. När kontrollpanelen är klar ser den ut ungefär så här:

![](../../mbi/assets/investor-dboard-example.png)
