---
title: Inbyggda instrumentpaneler
description: Lär dig mer om färdiga instrumentpaneler för att få insikt i verksamheten.
exl-id: fe61c92e-de87-4317-96d7-01d2a9846bf9
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '1932'
ht-degree: 0%

---

# Inkörbara kontrollpaneler

[!DNL Adobe Commerce Intelligence] innehåller färdiga kontrollpaneler som ger inblick i verksamheten. På kontrollpaneler kan du kontrollera hälsan hos viktiga mätvärden som användarlivstidsintäkter, antal upprepade köp, toppprodukter som köpts under en viss tidsperiod och mycket annat. Dessa förkonfigurerade instrumentpaneler har skapats för att hjälpa dig att fatta välgrundade affärsbeslut.

>[!NOTE]
>
>Åtkomsten till dessa instrumentpaneler beror på kontotypen och din åtkomstnivå. Om du inte ser de här instrumentpanelerna kontaktar du [support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

## Rapporttillgänglighet

För `Customers` och `Executive Summary` på kontrollpaneler är vissa rapporter bara tillgängliga beroende på butikens utcheckningskonfiguration. Om din butik tillåter gästutcheckning eller inte tillåter gästutcheckning.

## Kunder (gästutcheckning tillåts)

Kontrollpanelen Kunder (gästutcheckning tillåts) innehåller information om din kundbas, till exempel deras köpbeteende. Den här instrumentpanelen kan hjälpa er att förbättra kundlojaliteten och avgöra vilka kunder som får störst intäkter.

### Rapporter

| Namn | Beskrivning |
|---|---|
| `Orders by New Customers (Past 30 Days)` | Beställ de senaste 30 dagarna från kunder som aldrig tidigare lagt en order. |
| `Orders by Existing Customers (Past 30 Days)` | Beställ de senaste 30 dagarna från kunder som tidigare har gjort minst en beställning. |
| `Total Unique Customers (Past 30 Days)` | Antal unika kunder som lagt order de senaste 30 dagarna. |
| `Orders by New vs Existing Customers` | Antal beställningar som gjorts av kunder utan tidigare beställningar jämfört med kunder med minst en tidigare beställning. |
| `Subsequent Order Probability (All Time)` | Sannolikheten att kunder som har gjort en beställning lägger en annan. |
| `% of Customers with Multiple Orders (All Time)` | Procent av alla kunder som har gjort mer än en beställning. |
| `Median Time Between Orders (All Time)` | Genomsnittlig tid varje kund tar mellan att göra en beställning och nästa. |
| `Subsequent Order Probability` | Sannolikheten för att kunder som har lagt en order lägger en annan order, uppdelad efter ordernummer. Det vill säga procentandelen kunder med en order som lägger en andra, en procent med två som placerar en tredjedel osv. |
| `Time Between Orders` | Genomsnittlig och mediantid som kunderna tar mellan beställningarna, uppdelat efter ordernummer (dvs. tiden mellan beställningarna ett och två, två och tre osv.). |
| `Number of Customers - Lifetime Orders` | För ett givet antal order som läggs under en kunds livstid, antalet kunder som har lagt så många order och den procentandel av hela kundbasen som talet representerar. |
| `One-Time Customers who Bought 3-6 Months Ago` | Kunder som gjorde sina första inköp för endast tre till sex månader sedan. |
| `Avg LTV by First Order` | Jämför de kumulativa genomsnittliga intäkterna för kundlivstid mellan kohorter. Kohorter definieras av den månad då kunden först gjorde ett köp. Till exempel en `Jan 2020` kohort visar ackumulerat genomsnittligt LTV för kunder vars första inköp gjordes i januari 2020. |
| `Customer's First 30 Day vs Lifetime Revenue` | Jämförelse av genomsnittliga intäkter från kunder under de 30 dagarna efter deras första inköp jämfört med under hela deras livstid. Varje bubbla motsvarar en fraktregion, och storleken på varje bubbla representerar antalet kunder som förvärvats från den regionen. |

## Kunder (ingen gästutcheckning tillåts)

Instrumentpanelen Kunder (ingen gästutcheckning tillåts) ger information om din kundbas, som deras inköpsbeteende och konverteringar från kontoregistreringar till orderplaceringar. Den här kontrollpanelen kan hjälpa er att få fler kunder att stanna kvar och avgöra vilka kunder som får störst intäkter.

### Rapporter

| Namn | Beskrivning |
|---|---|
| `Account Registration (Past 30 Days)` | Antalet personer som har registrerats för ett konto hos din butik de senaste 30 dagarna. |
| `Accounts Registered (Past 30 Days) with 1 or More Orders` | Antalet personer som har registrerats för ett konto hos din butik under de senaste 30 dagarna och som också har gjort minst en beställning. |
| `% Conversion from Registration to First Order (Past 30 Days)` | Procent av konton som registrerats under de senaste 30 dagarna och som har beställt. |
| `% Conversion from Registration to First Order` | Procent av registrerade konton som har gjort en beställning, per registreringsmånad. |
| `Orders by New vs Existing Customers` | Antal beställningar som gjorts av kunder utan tidigare beställningar jämfört med kunder med minst en tidigare beställning. |
| `Subsequent Order Probability (All Time)` | Sannolikheten för att kunder som har lagt en order lägger en annan. |
| `% of Customers with Multiple Orders (All Time)` | Procent av alla kunder som har gjort mer än en beställning. |
| `Median Time Between Orders (All Time)` | Genomsnittlig tid varje kund tar mellan att göra en beställning och nästa. |
| `Subsequent Order Probability` | Sannolikheten för att kunder som har lagt en order lägger en annan, uppdelad efter ordernummer. Det vill säga, procent av kunderna med en order som lägger en andra, en procent med två som placerar en tredjedel och så vidare. |
| `Time Between Orders` | Genomsnittlig och mediantid som kunderna tar mellan beställningarna, uppdelat efter ordernummer (dvs. tiden mellan beställningarna ett och två, två och tre osv.). |
| `Number of Customers - Lifetime Orders` | För ett givet antal order som läggs under en kunds livstid, antalet kunder som har lagt så många order och den procentandel av hela kundbasen som talet representerar. |
| `One-Time Customers who Bought 3-6 Months Ago` | Kunder som gjorde sina första inköp för endast tre till sex månader sedan. |
| `Avg LTV by First Order` | Jämför de kumulativa genomsnittliga intäkterna för kundlivstid mellan kohorter. Kohorter definieras av den månad då kunden först gjorde ett köp. Exempel: En Jan 2020-kohort visar ett ackumulerat genomsnittligt LTV för kunder vars första inköp gjordes i januari 2020. |
| `Customer's First 30 Day vs Lifetime Revenue` | Jämförelse av genomsnittliga intäkter från kunder under de 30 dagarna efter deras första inköp jämfört med under hela deras livstid. Varje bubbla motsvarar en fraktregion, och storleken på varje bubbla representerar antalet kunder som förvärvats från den regionen. |

## Sammanfattning (gästutcheckning tillåts)

Instrumentpanelen för den verkställande sammanfattningen (gästutcheckning tillåts) ger dig en kort bild av hur verksamheten fungerar när det gäller order och intäkter. Kontrollpanelen är utformad för chefer som vill få en övergripande förståelse för hur verksamheten fungerar, men den kan även vara insiktsfull för andra.

### Rapporter

| Namn | Beskrivning |
|---|---|
| `Revenue (Current Month)` | Intäkterna som har genererats av din butik för den aktuella månaden. I det här fallet definieras intäkter som det slutpris som en kund betalar på en order. |
| `Revenue (Past 6 Months by Day)` | Total daglig intäkt, utöver den genomsnittliga dagliga intäkten under de föregående sju dagarna. I det här fallet definieras intäkter som det slutpris som en kund betalar på en order. |
| `% Change in Revenue (MoM MTD)` | Jämförelse av intäkter för den aktuella månaden (hittills) jämfört med samma del av föregående månad. |
| `Revenue from New vs Existing Customers (Current Month)` | Intäkter för den innevarande månaden (hittills) som tilldelats nya (första gången) kunder jämfört med befintliga kunder (andra eller senare). |
| `Average Order Value (Current Month)` | Dagsmedelvärde för order som lagts under den aktuella månaden (hittills). Ordervärdet definieras som det slutpris som en kund betalar på en order. |
| `Orders (Current Month)` | Antalet order som lagts i din butik för den aktuella månaden (hittills). |
| `% Change in Orders (MoM MTD)` | Jämförelse mellan antalet order för den aktuella månaden (hittills) och samma del av föregående månad. |
| `Orders by New Customers (Current Month)` | Beställningar för den aktuella månaden från kunder som aldrig tidigare lagt en order. |
| `Orders by Existing Customers (Current Month)` | Beställningar för den aktuella månaden från kunder som tidigare har gjort minst en beställning. |
| `Orders by New vs Existing Customers (Current Year by Week)` | Antal order av kunder utan tidigare order jämfört med kunder med minst en tidigare order, för varje vecka under innevarande år (hittills). |

## Sammanfattning (ingen gästutcheckning tillåts)

Den sammanfattande instrumentpanelen (ingen gästutcheckning tillåts) ger dig en kortfattad bild av hur det går för företaget när det gäller beställningar, intäkter och kontoregistreringar. Den här instrumentpanelen är utformad för att chefer ska få en övergripande förståelse för affärsprestanda, men den kan även vara insiktsfull för andra.

### Rapporter

| Namn | Beskrivning |
|---|---|
| `Revenue (Current Month)` | Intäkterna som har genererats av din butik den här månaden. I det här fallet definieras intäkter som det slutpris som en kund betalar på en order. |
| `Revenue (Past 6 Months by Day)` | Total daglig intäkt, utöver den genomsnittliga dagliga intäkten under de föregående sju dagarna. I det här fallet definieras intäkter som det slutpris som en kund betalar på en order. |
| `% Change in Revenue (MoM MTD)` | Jämförelse av intäkter hittills i den här månaden jämfört med samma del av föregående månad. |
| `Revenue from New vs Existing Customers (Current Month)` | Intäkterna för innevarande månad (hittills) hänförs till nya (första gången) kunder jämfört med befintliga kunder (andra eller senare beställningar). |
| `Average Order Value (Current Month)` | Medelvärde för orderingång under innevarande månad (hittills). Ordervärde definieras som det slutliga pris som en kund betalar för en order. |
| `Orders (Current Month)` | Antalet order som lagts i din butik för den aktuella månaden (hittills). |
| `% Change in Orders (MoM MTD)` | Jämförelse mellan antalet order för den aktuella månaden (hittills) och samma del av föregående månad. |
| `Account Registrations (Current Month)` | Antalet nyregistrerade konton hittills under den här månaden. |
| `% Conversion from Registration to First Order (Current Month)` | Procentandel av konton som hittills registrerats den här månaden och som har beställt. |
| `% Conversion from Registration to First Order (Current Year by Week)` | Andelen konton som registrerats varje vecka hittills i år och som har beställts. |

## Beställningar

Instrumentpanelen för beställningar ger insikter om transaktionsvolym för beställningar, deras status, vilka kupongkoder som används, genererade intäkter och vilka betalningsmetoder som används. Du kan till exempel spåra leveransprocessen och se till att det inte finns några problem eller flaskhalsar.

>[!NOTE]
>
>Rapporterna på den här instrumentpanelen är tillgängliga för konton som är anslutna till arkiv med någon typ av konfiguration (gästutcheckning, ingen gästutcheckning).

### Rapporter

| Namn | Beskrivning |
|---|---|
| `Orders (Past 30 Days)` | Antalet beställningar som gjorts i din butik under de senaste 30 dagarna. |
| `Revenue (Past 30 Days)` | De intäkter som har genererats av din butik under de senaste 30 dagarna. Intäkter definieras som det slutpris som en kund betalar på en order. |
| `Average Order Value (Past 30 Days)` | Genomsnittligt ordervärde under de senaste 30 dagarna. Ordervärdet definieras som det slutpris som en kund betalar på en order. |
| `Orders` | Antalet beställningar som görs i din butik varje månad. |
| `Revenue by Payment Method` | Intäkterna som har genererats av din butik, uppdelade efter betalningsmetod. Intäkter definieras som det slutpris som en kund betalar på en order. |
| `AOV by New vs Existing Customers` | Månadsmedelvärdet av order som gjorts i din butik, delat på order som gjorts av kunder utan tidigare order jämfört med kunder med minst en tidigare order. Ordervärdet definieras som det slutpris som en kund betalar på en order. |
| `% Orders by Status (Past 30 Days)` | Procent av order från varje dag under de senaste 30 dagarna som för närvarande har respektive orderstatus. |
| `Incomplete Orders (Created more than 1 Day Ago)` | En lista över alla order som lagts för mer än en dag sedan och som fortfarande är ofullständiga (inte annullerade eller fullständiga). |
| `Orders Per Hour (Past 7 Days)` | Beställ volym per dag och timme. |
| `Revenue Details (Past 30 Days)` | Daglig intäktsfördelning de senaste 30 dagarna i alla komponenter av det totala intäktsvärdet. |
| `Order Details by Coupon Code (Past 30 Days)` | För varje kupongkod som din butik erbjuder ska du ange hur kupongkoden användes och vilka returer den har fått under de senaste 30 dagarna. |
| `% Orders with Coupon (Past 30 Days)` | Procentandelen order som lagts under de senaste 30 dagarna som använde en kupong jämfört med de som inte gjorde det. |

## Produkter

På kontrollpanelen för produkter visas den allmänna produktprestandan i termer av beställda produkter, deras bruttovärde för försäljning (GMV) samt de viktigaste produkter som köpts och återbetalats. Det kan hjälpa er att balansera inköp och returer och avgöra om produkterna blir framgångsrika och populära. Din butik måste vara [konfigurerad för att spåra återbetalningar](https://experienceleague.adobe.com/docs/commerce-admin/customers/customer-accounts/store-credit/credit-configure.html) för att dessa diagram ska fyllas i.

>[!NOTE]
>
>Rapporterna på den här instrumentpanelen är tillgängliga för konton som är anslutna till arkiv med någon typ av konfiguration (gästutcheckning, ingen gästutcheckning).

### Rapporter

| Namn | Beskrivning |
|---|---|
| `GMV (Past 30 Days)` | Bruttovaruvärdet för alla produkter som sålts de senaste 30 dagarna. GMV definieras som beställd kvantitet multiplicerad med baspriset för varje produkt. |
| `% GMV (Past 30 Days) Refunded` | Procent GMV för produkter som köpts under de senaste 30 dagarna och som resulterat i återbetalning. |
| `Product Quantity Ordered (Past 30 Days)` | Totalt antal beställda artiklar under de senaste 30 dagarna. |
| `% Purchased Products (Past 30 Days) Refunded` | Procent av artiklar som köpts under de senaste 30 dagarna och som resulterat i återbetalning. |
| `Gross Merchandise Value` | Bruttovaruvärdet för alla sålda produkter, per månad. GMV definieras som beställd kvantitet multiplicerad med baspriset för varje produkt. |
| `Purchases vs Refund Rate per Product (Past 30 Days)` | För varje produkt, en jämförelse mellan det totala antalet beställda under de senaste 30 dagarna och den ränta som produkten återbetalas med. Storleken på varje bubbla motsvarar återbetalningsnivån. |
| `Product Performance Details (Past 30 Days)` | Detaljerad information om försäljning och efterföljande återbetalningar under de senaste 30 dagarna, per produktsku och produktnamn. |
| `Top Purchased Products by GMV (Past 30 Days)` | Produkter som sålts under de senaste 30 dagarna och som genererade störst intäkter (de tio främsta). |
| `Top Refunded Products by GMV (Past 30 Days)` | Produkter som köpts under de senaste 30 dagarna och som resulterat i den största förlusten av GMV på grund av återbetalningar (de 10 högsta). |
| `Top Purchased Products by Quantity (Past 30 Days)` | Produkter som sålts de senaste 30 dagarna i det största antalet (de tio bästa). |
| `Top Refunded Products by Quantity (Past 30 Days)` | Produkter som köpts under de senaste 30 dagarna och som resulterat i den största återbetalningsmängden (de 10 högsta). |
