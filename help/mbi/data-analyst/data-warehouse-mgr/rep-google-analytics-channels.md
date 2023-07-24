---
title: Replikera Google Analytics-kanaler med hjälp av förvärvskällor
description: Lär dig hur du replikerar Google Analytics-kanaler med hjälp av förvärvskällor.
exl-id: e7248fe4-94db-4cdf-8f58-1f65061a207d
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 0%

---

# [!DNL Google Analytics] med förvärvskällor

## Vad är kanaler? {#channels}

Att skapa anpassade segment för att se hur olika trafik fungerar och för att observera trender är ett av de mest kraftfulla användningsområdena för [!DNL Google Analytics]. En segmentklass som finns som standard i [!DNL Google Analytics] är `Channels`. Kanaler är en gruppering av vanliga sätt som folk kommer till din webbplats.  [!DNL Google Analytics] sorterar automatiskt de olika sätt som du köper en användare på - sociala medier, betala per klick, e-post eller hänvisningslänkar - och paketerar dem i en bucket eller kanal.

## Varför ser jag inte min `channels` i Commerce Intelligence? {#nochannels}

`Channels` är enkla, sammansatta dataområden. Så här sorterar du dina förvärv i kanalgrupper: [!DNL Google] anger distinkta regler och definitioner med hjälp av specifika parametrar: en kombination av förvärv [Källa](https://support.google.com/analytics/answer/1033173?hl=en) (trafikens ursprung) och värvning [Medel](https://support.google.com/analytics/answer/6099206?hl=en) (källans allmänna kategori).

Även om dessa bucklar kan hjälpa dig att förstå var trafiken kommer ifrån är dessa data inte taggade av kanalen utan av en kombination av källa och medium. För [!DNL Google] skickar kanalinformation som två separata datapunkter, kanalgrupperingar visas inte automatiskt i [!DNL Commerce Intelligence].

## Vilka är standardkanalgrupperingarna? Hur skapas de?

Som standard [!DNL Google] skapar åtta olika kanaler. Reglerna som bestämmer hur kanaler skapas är nedan.

| **Kanal** | **Vad är det?** | **Hur skapas den?** |
|---|---|---|
| Direkt | Alla som kommer in direkt på er webbplats. | Källa = `Direct`<br>AND Medium = `(not set); OR Medium = (none)` |
| Organic Search | Trafik som har rankats organiskt i obetalda sökmotorer. | Medel = `organic` |
| Hänvisning | Trafik som kommer från en extern länk som inte är en organisk sökning eller från webbplatser som inte är sociala nätverk. | Medel = `referral` |
| Betalsökning | Trafik som har en UTM-spårningskod där mediet är antingen &quot;cpc&quot;, &quot;ppc&quot; eller &quot;paidsearch&quot; OCH är ett annonsdistributionsnät som inte matchar &quot;Content&quot;. | Medel = `^(cpc|ppc|paidsearch)$`<br>AND Ad Distribution Network ≠ `Content` |
| Social | Hänvisningstrafik som kommer från någon av de ungefär [400 sociala nätverk](https://www.annielytics.com/blog/analytics/sites-google-analytics-includes-in-social-reports/) och är inte taggade som annonser. | Hänvisning till social källa = `Yes`<br>ELLER Medel = `^(social|social-network|social-media|sm|social network|social media)$` |
| E-post | Trafik från sessioner som är taggade med ett medium av &quot;e-post&quot;. | UTM-spårningskod = `email` |
| Visa | Trafik som har en UTM-spårningskod där mediet antingen visas eller är kpm. Innehåller även AdWords-interaktion där annonsens distributionsnätverk matchar&quot;Content&quot; | Medel = `^(display|cpm|banner)$`<br>ELLER Ad Distribution Network = `Content`<br>AND Ad Format ≠ `Text` |
| Övriga | Sessioner från andra annonskanaler (exklusive betald sökning) som är taggade med mediet &quot;cpc&quot;, &quot;ppc&quot;, &quot;cpm&quot;, &quot;cpv&quot;, &quot;cpa&quot;, &quot;cpp&quot;, &quot;affiliate&quot;. | Medel = `^(cpv|cpa|cpp|content-text)$` |

{style="table-layout:auto"}

## Hur återskapar jag de här kanalgrupperingarna i Data warehouse? {#recreate}

Nu när du vet att kanaler bara är kombinationer av källor och medier är det en enkel process i tre steg att återskapa dessa grupperingar i Data warehouse.

1. **Aktivera[!DNL Google ECommerce]integration**

   [När aktiverat](../importing-data/integrations/google-ecommerce.md), se till att [synka](../{{ site.baseurl }}/data-analyst/data-warehouse-mgr/tour-dwm.html#syncing) **medium** och **källa** fält i Data warehouse. När detta är klart hämtas data om medium- och källförvärv till Data warehouse.

1. **Överför en mappning av Google kanalgrupperingar**

   Adobe Commerce skapar en tabell med standardgrupperingarna mappade som en fil som du kan [ladda ned](../../assets/ga-channel-mapping.csv).

   Om du är en [!DNL Google Analytics] proffsen och skapat egna kanaler vill du lägga till specifika regler i mappningstabellen innan du överför filen till [!DNL Commerce Intelligence].

   Ta in den i Data warehouse som en [Filöverföring](../importing-data/connecting-data/using-file-uploader.md).

   ![](../../assets/Setting_Primary_Keys.png)

1. **Upprätta en relation mellan[!DNL Google ECommerce]och mappningsfilöverföring**

   Så här skapar du en relation mellan[!DNL Google ECommerce] och mappningstabellen, [skicka en supportförfrågan](../../guide-overview.md#Submitting-a-Support-Ticket) till ditt Data Analyst-team och hänvisa till det här avsnittet. Analytikern skapar en ny beräknad kolumn som kallas **Kanal** i tabellen ECommerce. **Efter en fullständig uppdateringscykel**&#x200B;är den här kolumnen klar att användas i en `Filter` eller `Group by`.

Du har nu [!DNL Google Analytics Channel] grupperingar i Data warehouse, vilket innebär att du kan analysera data från ett nytt perspektiv:

![Segmentera måttet Antal order per kanal](../../assets/GA_Channel_Gif.gif)

I det här exemplet började du enkelt med att segmentera **Antal order** mått efter **Kanal**. Testa din nya kolumn och se vilka trender du kan identifiera i [!DNL Google Analytics Channel] data!

## Relaterad dokumentation

* [Använda Report Builder](../../tutorials/using-visual-report-builder.md)
* [Förväntat[!DNL Google ECommerce]data](../importing-data/integrations/google-ecommerce-data.md)
* [Byggnad[!DNL Google ECommerce]dimensioner med beställnings- och kunddata](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
* [Vilka är era mest värdefulla förvärvskällor och kanaler?](../analysis/most-value-source-channel.md)
