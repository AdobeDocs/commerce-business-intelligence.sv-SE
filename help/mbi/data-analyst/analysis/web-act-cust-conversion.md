---
title: Analysera webbplatsaktivitet och kundkonverteringsgrader
description: Lär dig hur du konfigurerar en kontrollpanel som kan spåra webbplatsens aktivitet - inklusive sidvisningar, sessioner och användare - och hur stor kundkonverteringen är över tid.
exl-id: 2b57d5b3-3bbf-4ec9-86a6-9fa850c1c459
role: Admin, User
feature: Reports, Data Integration
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '744'
ht-degree: 0%

---

# Analyserar webbplatsaktivitet

[!DNL Adobe Commerce Intelligence] kan ni enkelt integrera era annonsdata med resten av era data. Detta gör det inte bara möjligt för er att förstå webbplatsens aktivitet, utan gör det möjligt för er att ta reda på hur många besökare på er webbplats som blir registrerade användare eller gör ett köp.

I det här avsnittet visas hur du konfigurerar en kontrollpanel som ska spåra webbplatsens aktivitet - inklusive sidvisningar, sessioner och användare - och hur stor kundkonverteringsgraden är över tiden.

## Förutsättningar

**Importera kostnadsdata för annonsering** - Connect [!DNL [Google AdWords]](../importing-data/integrations/google-adwords.md) till [!DNL Adobe Commerce Intelligence] - detta synkroniserar automatiskt [!DNL AdWords] utgifter i Commerce Intelligence.

**Spåra kanaldata för kundvärvning** - för att knyta [!DNL Google AdWords] data till specifika order i din databas måste du [spåra användarförvärv](../analysis/google-track-user-acq.md) via [!DNL Google Analytics E-commerce]. På så sätt kan du koppla varje beställning till en utm-källa och ett medium.

## Kampanjer för att värva användare

Den här rapportsamlingen skapas med följande:

* Mätvärden som genereras automatiskt när du kopplar samman [!DNL Google AdWords] data
* Grundläggande mätvärden som redan ska vara tillgängliga på ditt konto, som `Number of orders` och `New users`
* Dimensioner som skapas när du går med i [!DNL Google Analytics Ecommerce] data till databasen, som orderns utm-källa och orderns utm-medium. Kontakta supportteamet om fälten inte är tillgängliga i ditt konto

## Bygga rapporter

**Börja med att skapa en rapport som visar antalet sidvisningar, sessioner och användare över tiden:**

1. Skapa en rapport.
1. Klicka **[!UICONTROL Add Metric]** och sedan muspekaren över [!DNL Google Analytics] längst ned i listrutan och välj `Page Views`.
1. Lägg till ytterligare ett mätvärde, och för musen över [!DNL Google Analytics] avsnitt, den här gången `Sessions`.
1. Lägg till en tredje mätmetod, återigen för musen över [!DNL Google Analytics] avsnitt, den här gången `Users`.
1. Ändra nu tidsperioden till ett rörligt intervall, från 31 dagar sedan till 1 dag sedan, och justera tidsintervallet till `by day`.
1. Ge rapporten ett namn (till exempel `Page views, sessions and users by day`) och klicka på **[!UICONTROL Save]**.

**I den andra rapporten behandlas antalet sidvisningar under det senaste året:**

1. Skapa en rapport.
1. Klicka **[!UICONTROL Add Metric]**, muspekaren över [!DNL Google Analytics] längst ned i listrutan och välj _Sidvyer_.
1. Ändra din tidsperiod till ett rörligt intervall, från 13 månader sedan till 1 månad sedan, och justera tidsintervallet till `by month`.
1. Ge rapporten ett namn, som `Page views by month,` och klicka **[!UICONTROL Save]**.

**Det tredje diagrammet visar studsfrekvensen under det senaste året:**

1. Skapa en rapport.
1. Klicka **[!UICONTROL Add Metric]**, muspekaren över [!DNL Google Analytics] längst ned i listrutan och välj _Studsfrekvens_.
1. Ändra din tidsperiod till ett rörligt intervall, från 13 månader sedan till 1 månad sedan, och justera tidsintervallet till `by month`.
1. Ge rapporten ett namn, som `Bounce rate by month`och klicka **[!UICONTROL Save]**.

**Titta nu på den genomsnittliga sessionslängden för nya besökare jämfört med återkommande besökare:**

1. Skapa en rapport.
1. Klicka **UICONTROL Add Metric**, muspekaren över [!DNL Google Analytics] längst ned i listrutan och välj `Average Session Length`.
1. Ändra din tidsperiod till ett rörligt intervall, från 13 månader sedan till 1 månad sedan, och justera tidsintervallet till `by month`?
1. Lägg till en `Group by` och markera `New or returning visitor`.  Kontrollera `Show All` ruta och klicka sedan på **[!UICONTROL Apply]**.
1. Ge rapporten ett namn, som `Average session length`och klicka **[!UICONTROL Save]**.

**Titta sedan på dina viktigaste referensdomäner de senaste 30 dagarna:**

1. Skapa en rapport.
1. Klicka **[!UICONTROL Add Metric]**, muspekaren över [!DNL Google Analytics] längst ned i listrutan och välj `Sessions`.
1. Ändra din tidsperiod till ett rörligt intervall, från 31 dagar sedan till 1 dag sedan, och justera tidsintervallet till `none`.
1. Lägg till en `Group by` och markera `ga:source`.  Kontrollera _Visa alla_ ruta och klicka sedan på **[!UICONTROL Apply]**.
1. Lägg till ytterligare `group by` och markera `ga:medium`. Återigen, kontrollera `Show All` ruta och klicka sedan på **[!UICONTROL Apply]**.
1. Ge rapporten ett namn, som `Top 20 Referring Domains, 30 Days`och klicka **[!UICONTROL Save]**.

**Slutligen: se på konverteringen:**

1. Skapa en rapport.
1. Lägg till följande mått:

* `New users`
   * Klicka **[!UICONTROL Hide]** under måttnamnet

* `Number of orders`
   * Lägg till ett filter för `Customer's order number` = 1 och klicka **[!UICONTROL Apply]**
   * Byt namn på måttet genom att klicka på måttnamnet och kalla det `Number of first orders`och sedan klicka **[!UICONTROL Hide]**

* `Number of orders`
   * **[!UICONTROL Hide]** måttet

* `Users`
   * **[!UICONTROL Hide]** måttet
   * Ändra tidsperioden till `24 months ago to now`och justera tidsintervallet till `by month`.
   * Lägg till följande formler genom att klicka **[!UICONTROL Formula]**.
   * A/D och klicka sedan på **[!UICONTROL Apply]**
   * Byt namn på formeln `Registration conversion`
   * B/D och klicka sedan på **[!UICONTROL Apply]**
   * Byt namn på formeln `First order conversion`
   * C/D och klicka sedan på **[!UICONTROL Apply]**
   * Byt namn på formeln `Any order conversion`

* Ge rapporten ett namn som `Conversion by month`och klicka sedan på **[!UICONTROL Save]**.

## Nästa steg

Nu när du har tillgång till data om din webbtrafik och konverteringsgrader kan du börja med att lösa detta för att fatta affärsbeslut, som vilka webbplatser som är bäst på att köra trafik till din webbplats? eller vilka av era kampanjer som är mest effektiva när det gäller att värva kunder med ett högt värde för hela livet?

När ni anpassar annonskostnaderna och marknadsföringsstrategin kan ni fortsätta att följa resultaten i [!DNL Commerce Intelligence], och itererar på den här instrumentpanelen för att uppfylla företagets föränderliga prioriteringar.
