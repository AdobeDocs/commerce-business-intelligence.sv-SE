---
title: Analysera webbplatsaktivitet och kundkonverteringsgrader
description: Lär dig hur du konfigurerar en kontrollpanel som kan spåra webbplatsens aktivitet - inklusive sidvisningar, sessioner och användare - och hur stor kundkonverteringen är över tid.
exl-id: 2b57d5b3-3bbf-4ec9-86a6-9fa850c1c459
role: Admin, User
feature: Reports, Data Integration
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 0%

---

# Analyserar webbplatsaktivitet

Med [!DNL Adobe Commerce Intelligence] kan du enkelt integrera dina annonsdata med resten av dina data. Detta gör det inte bara möjligt för er att förstå webbplatsens aktivitet, utan gör det möjligt för er att ta reda på hur många besökare på er webbplats som blir registrerade användare eller gör ett köp.

I det här avsnittet visas hur du konfigurerar en kontrollpanel som ska spåra webbplatsens aktivitet - inklusive sidvisningar, sessioner och användare - och hur stor kundkonverteringsgraden är över tiden.

## Förutsättningar

**Importera dina annonskostnadsuppgifter** - Anslut [!DNL [Google AdWords]](../importing-data/integrations/google-adwords.md) till [!DNL Adobe Commerce Intelligence] - detta synkroniserar automatiskt dina [!DNL AdWords]-utgifter i Commerce Intelligence.

**Spåra kanaldata för kundvärvning** - Om du vill koppla dina [!DNL Google AdWords]-data till specifika order i din databas måste du [spåra kundvärvning](../analysis/google-track-user-acq.md) via [!DNL Google Analytics E-commerce]. På så sätt kan du koppla varje beställning till en utm-källa och ett medium.

## Kampanjer för att värva användare

Den här rapportsamlingen skapas med följande:

* Mätvärden som genereras automatiskt när du ansluter dina [!DNL Google AdWords]-data
* Grundläggande mätvärden som redan ska vara tillgängliga för ditt konto, som `Number of orders` och `New users`
* Dimensioner som skapas när dina [!DNL Google Analytics Ecommerce]-data kopplas till din databas, som orderns utm-källa och orderns utm-medium. Kontakta supportteamet om fälten inte är tillgängliga i ditt konto

## Bygga rapporter

**Börja med att skapa en rapport som visar antalet sidvisningar, sessioner och användare över tiden:**

1. Skapa en rapport.
1. Klicka på **[!UICONTROL Add Metric]**, håll muspekaren över avsnittet [!DNL Google Analytics] längst ned i listrutan och välj `Page Views`.
1. Lägg till ytterligare ett mätvärde, och för musen över avsnittet [!DNL Google Analytics] igen, den här gången väljer du `Sessions`.
1. Lägg till ett tredje mätvärde, återigen för musen över avsnittet [!DNL Google Analytics], den här gången väljer du `Users`.
1. Ändra nu tidsperioden till ett rörligt intervall, från 31 dagar sedan till 1 dag sedan, och justera tidsintervallet till `by day`.
1. Ge rapporten ett namn (till exempel `Page views, sessions and users by day`) och klicka på **[!UICONTROL Save]**.

**Den andra rapporten tittar på antalet sidvisningar under det senaste året:**

1. Skapa en rapport.
1. Klicka på **[!UICONTROL Add Metric]**, håll muspekaren över avsnittet [!DNL Google Analytics] längst ned i listrutan och välj _Sidvyer_.
1. Ändra din tidsperiod till ett rörligt intervall, från för 13 månader sedan till för 1 månad sedan, och justera tidsintervallet till `by month`.
1. Ge rapporten ett namn, som `Page views by month,` och klicka på **[!UICONTROL Save]**.

**Det tredje diagrammet tittar på studsfrekvensen det senaste året:**

1. Skapa en rapport.
1. Klicka på **[!UICONTROL Add Metric]**, håll muspekaren över avsnittet [!DNL Google Analytics] längst ned i listrutan och välj _Studsfrekvens_.
1. Ändra din tidsperiod till ett rörligt intervall, från för 13 månader sedan till för 1 månad sedan, och justera tidsintervallet till `by month`.
1. Ge rapporten ett namn, som `Bounce rate by month`, och klicka på **[!UICONTROL Save]**.

**Titta nu på den genomsnittliga sessionslängden för nya besökare jämfört med återkommande besökare:**

1. Skapa en rapport.
1. Klicka på **UICONTROL Add Metric**, håll muspekaren över avsnittet [!DNL Google Analytics] längst ned i listrutan och välj `Average Session Length`.
1. Vill du ändra tidsperioden till ett rörligt intervall, från 13 månader sedan till 1 månad sedan, och justera tidsintervallet till `by month`?
1. Lägg till en `Group by` och välj `New or returning visitor`.  Markera rutan `Show All` och klicka sedan på **[!UICONTROL Apply]**.
1. Ge rapporten ett namn, som `Average session length`, och klicka på **[!UICONTROL Save]**.

**Titta sedan på dina viktigaste refererande domäner de senaste 30 dagarna:**

1. Skapa en rapport.
1. Klicka på **[!UICONTROL Add Metric]**, håll muspekaren över avsnittet [!DNL Google Analytics] längst ned i listrutan och välj `Sessions`.
1. Ändra din tidsperiod till ett rörligt intervall, från 31 dagar sedan till 1 dag sedan, och justera tidsintervallet till `none`.
1. Lägg till en `Group by` och välj `ga:source`.  Markera rutan _Visa alla_ och klicka sedan på **[!UICONTROL Apply]**.
1. Lägg till ytterligare `group by` och välj `ga:medium`. Återigen, markera rutan `Show All` och klicka sedan på **[!UICONTROL Apply]**.
1. Ge rapporten ett namn, som `Top 20 Referring Domains, 30 Days`, och klicka på **[!UICONTROL Save]**.

**Titta slutligen på konverteringen:**

1. Skapa en rapport.
1. Lägg till följande mått:

* `New users`
   * Klicka på **[!UICONTROL Hide]** under måttnamnet

* `Number of orders`
   * Lägg till ett filter för `Customer's order number` = 1 och klicka på **[!UICONTROL Apply]**
   * Byt namn på måttet genom att klicka på måttnamnet, anropa det `Number of first orders` och sedan klicka på **[!UICONTROL Hide]**

* `Number of orders`
   * **[!UICONTROL Hide]** måttet

* `Users`
   * **[!UICONTROL Hide]** måttet
   * Ändra tidsperioden till `24 months ago to now` och justera tidsintervallet till `by month`.
   * Lägg till följande formler genom att klicka på **[!UICONTROL Formula]**.
   * A/D-klicka sedan på **[!UICONTROL Apply]**
   * Byt namn på formeln `Registration conversion`
   * B/D-klicka sedan på **[!UICONTROL Apply]**
   * Byt namn på formeln `First order conversion`
   * C/D-klicka sedan på **[!UICONTROL Apply]**
   * Byt namn på formeln `Any order conversion`

* Ge rapporten ett namn, som `Conversion by month`, och klicka sedan på **[!UICONTROL Save]**.

## Nästa steg

Nu när du har tillgång till data om din webbtrafik och konverteringsgrader kan du börja med att lösa detta för att fatta affärsbeslut, som vilka webbplatser som är bäst på att köra trafik till din webbplats? eller vilka av era kampanjer som är mest effektiva när det gäller att värva kunder med ett högt värde för hela livet?

När du justerar annonsutgifter och marknadsföringsstrategi kan du fortsätta att spåra resultaten i [!DNL Commerce Intelligence] och iterera på den här instrumentpanelen för att uppfylla ditt företags föränderliga prioriteringar.
