---
title: Analysera webbplatsaktivitet och kundkonverteringsgrader
description: Lär dig hur du skapar en kontrollpanel som kan spåra webbplatsens aktivitet - inklusive sidvisningar, sessioner och användare - samt hur stor kundkonverteringsgraden är över tid.
exl-id: 2b57d5b3-3bbf-4ec9-86a6-9fa850c1c459
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '763'
ht-degree: 0%

---

# Analyserar webbplatsaktivitet

[!DNL MBI] kan ni enkelt integrera era annonsdata med resten av era data. Detta gör det inte bara möjligt för er att förstå webbplatsens aktivitet, utan gör det möjligt för er att ta reda på hur många besökare på er webbplats som blir registrerade användare eller gör ett köp.

I den här artikeln visar vi hur du skapar en kontrollpanel som kan spåra webbplatsens aktivitet - inklusive sidvisningar, sessioner och användare - samt din kundkonverteringsgrad över tid.

## Förutsättningar

**Importera kostnadsdata för annonsering** - Connect [!DNL [Google AdWords]](../importing-data/integrations/google-adwords.md) till [!DNL MBI] - detta synkroniserar automatiskt [!DNL AdWords] utgifter i BI.

**Spåra kanaldata för kundvärvning** - för att knyta [!DNL Google AdWords] data till specifika order i din databas, vi måste [spåra användarförvärv](../analysis/google-track-user-acq.md) via [!DNL Google Analytics E-commerce], vilket gör att vi kan koppla varje beställning till en utm-källa och ett medium.

## Kampanjer för att värva användare

Den här rapportsamlingen skapas med följande:

* Mätvärden som genereras automatiskt när du kopplar samman [!DNL Google AdWords] data
* Grundläggande mätvärden som redan ska vara tillgängliga på ditt konto, som `Number of orders` och `New users`
* Dimensioner som skapas när du går med i [!DNL Google Analytics Ecommerce] data till databasen, som orderns utm-källa och orderns utm-medium. Kontakta vårt supportteam om fälten inte är tillgängliga för närvarande i ditt konto

## Bygga rapporter

**Börja med att skapa en rapport som visar antalet sidvisningar, sessioner och användare över tiden:**

1. Skapa en ny rapport.
1. Klicka **[!UICONTROL Add Metric]** och sedan muspekaren över [!DNL Google Analytics] längst ned i listrutan och välj `Page Views`.
1. Lägg till ytterligare ett mätvärde, och för musen över [!DNL Google Analytics] avsnitt, den här gången `Sessions`.
1. Lägg till en tredje mätmetod, återigen för musen över [!DNL Google Analytics] avsnitt, den här gången `Users`.
1. Ändra nu tidsperioden till ett rörligt intervall, från 31 dagar sedan till 1 dag sedan, och justera tidsintervallet till `by day`.
1. Ge rapporten ett namn (till exempel `Page views, sessions and users by day`) och klicka på **[!UICONTROL Save]**.

**I vår andra rapport tittar vi på antalet sidvisningar under det senaste året:**

1. Skapa en ny rapport.
1. Klicka **[!UICONTROL Add Metric]**, muspekaren över [!DNL Google Analytics] längst ned i listrutan och välj _Sidvyer_.
1. Ändra din tidsperiod till ett rörligt intervall, från 13 månader sedan till 1 månad sedan, och justera tidsintervallet till `by month`.
1. Ge rapporten ett namn, som `Page views by month,` och klicka **[!UICONTROL Save]**.

**Den tredje tabellen visar studsfrekvensen det senaste året:**

1. Skapa en ny rapport.
1. Klicka **[!UICONTROL Add Metric]**, muspekaren över [!DNL Google Analytics] längst ned i listrutan och välj _Studsfrekvens_.
1. Ändra din tidsperiod till ett rörligt intervall, från 13 månader sedan till 1 månad sedan, och justera tidsintervallet till `by month`.
1. Ge rapporten ett namn, som `Bounce rate by month`och klicka **[!UICONTROL Save]**.

**Titta nu på den genomsnittliga sessionslängden för nya besökare jämfört med återkommande besökare:**

1. Skapa en ny rapport.
1. Klicka **UICONTROL Add Metric**, muspekaren över [!DNL Google Analytics] längst ned i listrutan och välj `Average Session Length`.
1. Ändra din tidsperiod till ett rörligt intervall, från 13 månader sedan till 1 månad sedan, och justera tidsintervallet till `by month`?
1. Lägg till en `Group by` och markera `New or returning visitor`.  Kontrollera `Show All` box; sedan klicka **[!UICONTROL Apply]**.
1. Ge rapporten ett namn, som `Average session length`och klicka **[!UICONTROL Save]**.

**Ta sedan en titt på dina viktigaste referensdomäner de senaste 30 dagarna:**

1. Skapa en ny rapport.
1. Klicka **[!UICONTROL Add Metric]**, muspekaren över [!DNL Google Analytics] längst ned i listrutan och välj `Sessions`.
1. Ändra din tidsperiod till ett rörligt intervall, från 31 dagar sedan till 1 dag sedan, och justera tidsintervallet till `none`.
1. Lägg till en `Group by` och markera `ga:source`.  Kontrollera _Visa alla_ box; sedan klicka **[!UICONTROL Apply]**.
1. Lägg till ytterligare `group by` och markera `ga:medium`. Kontrollera igen `Show All` box; sedan klicka **[!UICONTROL Apply]**.
1. Ge rapporten ett namn, som `Top 20 Referring Domains, 30 Days`och klicka **[!UICONTROL Save]**.

**Ta en titt på konverteringen:**

1. Skapa en ny rapport.
1. Lägg till följande mått:

* `New users`
   * Klicka **[!UICONTROL Hide]** under måttnamnet

* `Number of orders`
   * Lägg till ett filter för `Customer's order number` = 1 och klicka **[!UICONTROL Apply]**
   * Byt namn på måttet genom att klicka på måttets namn och anropa det `Number of first orders`klicka sedan på **[!UICONTROL Hide]**

* `Number of orders`
   * **[!UICONTROL Hide]** måttet

* `Users`
   * **[!UICONTROL Hide]** måttet
   * Ändra tidsperioden till `24 months ago to now`och justera tidsintervallet till `by month`.
   * Lägg till följande formler genom att klicka **[!UICONTROL Formula]**.
   * A/D-klicka sedan **[!UICONTROL Apply]**
   * Byt namn på formeln `Registration conversion`
   * B/D och klicka sedan **[!UICONTROL Apply]**
   * Byt namn på formeln `First order conversion`
   * C/D och klicka sedan på **[!UICONTROL Apply]**
   * Byt namn på formeln `Any order conversion`

* Ge rapporten ett namn som `Conversion by month`och klicka sedan på **[!UICONTROL Save]**.

## Nästa steg

Nu när ni har tillgång till data om er webbtrafik och konverteringsgrader kan ni börja med detta för att fatta affärsbeslut. Vilka platser är bäst när det gäller att köra trafik till er webbplats?  Vilka av era kampanjer är mest effektiva när det gäller att värva kunder med långsiktigt värde?

När ni anpassar annonskostnaderna och marknadsföringsstrategin kan ni fortsätta att följa resultaten i [!DNL MBI], och itererar på den här instrumentpanelen för att uppfylla företagets föränderliga prioriteringar.
