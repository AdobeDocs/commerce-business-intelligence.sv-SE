---
title: Inbyggda instrumentpaneler
description: Lär dig mer om färdiga instrumentpaneler för att få insikt i verksamheten.
exl-id: fe61c92e-de87-4317-96d7-01d2a9846bf9
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '2235'
ht-degree: 0%

---

# Inkörbara kontrollpaneler

[!DNL MBI] innehåller färdiga kontrollpaneler som ger inblick i verksamheten. På kontrollpaneler kan du kontrollera hälsan hos viktiga mätvärden som användarlivstidsintäkter, antal upprepade köp, toppprodukter som köpts under en viss tidsperiod och mycket annat. Dessa förkonfigurerade instrumentpaneler har skapats för att hjälpa dig att fatta välgrundade affärsbeslut.

>[!NOTE]
>
>Åtkomsten till dessa instrumentpaneler beror på kontotypen och din åtkomstnivå. Om du inte ser de här instrumentpanelerna kontaktar du [support](../../guide-overview.md).

## Rapporttillgänglighet

För `Customers` och `Executive Summary` på kontrollpaneler är vissa rapporter bara tillgängliga beroende på butikens utcheckningskonfiguration. Om din butik tillåter gästutcheckning eller inte tillåter gästutcheckning.

## Kunder (gästutcheckning tillåts)

Instrumentpanelen Kunder (tillåten gästutcheckning) ger information om din kundbas, till exempel om deras köpbeteende. Den här kontrollpanelen kan hjälpa er att få fler kunder att stanna kvar och avgöra vilka kunder som får störst intäkter.

### Rapporter

| Namn | Beskrivning |
|---|---|
| `Orders by New Customers (Past 30 Days)` | Beställ de senaste 30 dagarna från kunder som aldrig tidigare lagt en order. |
| `Orders by Existing Customers (Past 30 Days)` | Beställ de senaste 30 dagarna från kunder som tidigare har gjort minst en beställning. |
| `Total Unique Customers (Past 30 Days)` | Antal unika kunder som lagt order de senaste 30 dagarna. |
| `Orders by New vs Existing Customers` | Antal beställningar som gjorts av kunder utan tidigare beställningar jämfört med kunder med minst en tidigare beställning. |
| `Subsequent Order Probability (All Time)` | Sannolikheten för att kunder som har lagt en order lägger en annan. |
| `% of Customers with Multiple Orders (All Time)` | Procent av alla kunder som har gjort mer än en beställning. |
| `Median Time Between Orders (All Time)` | Genomsnittlig tid varje kund tar mellan att göra en beställning och nästa. |
| `Subsequent Order Probability` | Sannolikheten för att kunder som har gjort en beställning placerar en annan, uppdelad efter ordernummer (dvs. i procent av kunder med en order som lägger en andra, i procent med två som placerar en tredjedel osv.). |
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
| Kontoregistrering (senaste 30 dagarna) | Antalet personer som har registrerats för ett konto hos din butik de senaste 30 dagarna. |
| Registrerade konton (senaste 30 dagarna) med 1 eller fler order | Antalet personer som har registrerats för ett konto hos din butik under de senaste 30 dagarna och som också har gjort minst en beställning. |
| % konvertering från registrering till första order (senaste 30 dagarna) | Procent av konton som registrerats under de senaste 30 dagarna och som har beställt. |
| % konvertering från registrering till första order | Procent av registrerade konton som har gjort en beställning, per registreringsmånad. |
| Beställningar av nya jämfört med befintliga kunder | Antal beställningar som gjorts av kunder utan tidigare beställningar jämfört med kunder med minst en tidigare beställning. |
| Efterföljande ordersannolikhet (hela tiden) | Sannolikheten för att kunder som har lagt en order lägger en annan. |
| % av kunderna med flera beställningar (hela tiden) | Procent av alla kunder som har gjort mer än en beställning. |
| Mediantid mellan order (hela tiden) | Genomsnittlig tid varje kund tar mellan att göra en beställning och nästa. |
| Sannolikhet för efterföljande order | Sannolikheten för att kunder som har gjort en beställning placerar en annan, uppdelad efter ordernummer (dvs. i procent av kunder med en order som lägger en andra, i procent med två som placerar en tredjedel osv.). |
| Tid mellan order | Genomsnittlig och mediantid som kunderna tar mellan beställningarna, uppdelat efter ordernummer (dvs. tiden mellan beställningarna ett och två, två och tre osv.). |
| Antal kunder - livstidsbeställningar | För ett givet antal order som läggs under en kunds livstid, antalet kunder som har lagt så många order och den procentandel av hela kundbasen som talet representerar. |
| Engångskunder som köpt för 3-6 månader sedan | Kunder som gjorde sina första inköp för endast tre till sex månader sedan. |
| Genomsnittlig LTV efter första beställningen | Jämför de kumulativa genomsnittliga intäkterna för kundlivstid mellan kohorter. Kohorter definieras av den månad då kunden först gjorde ett köp. Exempel: En Jan 2020-kohort visar ett ackumulerat genomsnittligt LTV för kunder vars första inköp gjordes i januari 2020. |
| Kundens första 30-dagars intäkter kontra livstidsintäkter | Jämförelse av genomsnittliga intäkter från kunder under de 30 dagarna efter deras första inköp jämfört med under hela deras livstid. Varje bubbla motsvarar en fraktregion, och storleken på varje bubbla representerar antalet kunder som förvärvats från den regionen. |

## Sammanfattning (gästutcheckning tillåts)

Instrumentpanelen för den verkställande sammanfattningen (gästutcheckning tillåts) ger dig en kort bild av hur verksamheten fungerar när det gäller order och intäkter. Kontrollpanelen är utformad för chefer som vill få en övergripande förståelse för hur verksamheten fungerar, men den kan även vara insiktsfull för andra.

### Rapporter

| Namn | Beskrivning |
|---|---|
| Intäkter (aktuell månad) | Intäkterna som har genererats av din butik för den aktuella månaden. I det här fallet definieras intäkter som det slutpris som en kund betalar på en order. |
| Intäkter (senaste sex månaderna per dag) | Total daglig intäkt, utöver den genomsnittliga dagliga intäkten under de föregående sju dagarna. I det här fallet definieras intäkter som det slutpris som en kund betalar på en order. |
| % förändring i intäkter (MoM MTD) | Jämförelse av intäkter för den aktuella månaden (hittills) jämfört med samma del av föregående månad. |
| Intäkter från nya eller befintliga kunder (aktuell månad) | Intäkter för den innevarande månaden (hittills) som tilldelats nya (första gången) kunder jämfört med befintliga kunder (andra eller senare). |
| Genomsnittligt ordervärde (aktuell månad) | Dagsmedelvärde för order som lagts under den aktuella månaden (hittills). Ordervärdet definieras som det slutpris som en kund betalar på en order. |
| Beställningar (aktuell månad) | Antalet order som lagts i din butik för den aktuella månaden (hittills). |
| % ändring i order (MoM MTD) | Jämförelse mellan antalet order för den aktuella månaden (hittills) och samma del av föregående månad. |
| Beställningar efter nya kunder (aktuell månad) | Beställningar för den aktuella månaden från kunder som aldrig tidigare lagt en order. |
| Beställningar efter befintliga kunder (aktuell månad) | Beställningar för den aktuella månaden från kunder som tidigare har gjort minst en beställning. |
| Beställningar efter nya eller befintliga kunder (aktuellt år efter vecka) | Antal order av kunder utan tidigare order jämfört med kunder med minst en tidigare order, för varje vecka under innevarande år (hittills). |

## Sammanfattning (ingen gästutcheckning tillåts)

Instrumentpanelen för den verkställande sammanfattningen (ingen gästutcheckning tillåts) ger dig en kort bild av hur verksamheten fungerar när det gäller order, intäkter och kontoregistreringar. Kontrollpanelen är utformad för chefer som vill få en övergripande förståelse för hur verksamheten fungerar, men den kan även vara insiktsfull för andra.

### Rapporter

| Namn | Beskrivning |
|---|---|
| Intäkter (aktuell månad) | Intäkterna som har genererats av din butik den här månaden. I det här fallet definieras intäkter som det slutpris som en kund betalar på en order. |
| Intäkter (senaste sex månaderna per dag) | Total daglig intäkt, utöver den genomsnittliga dagliga intäkten under de föregående sju dagarna. I det här fallet definieras intäkter som det slutpris som en kund betalar på en order. |
| % förändring i intäkter (MoM MTD) | Jämförelse av intäkter hittills i den här månaden jämfört med samma del av föregående månad. |
| Intäkter från nya eller befintliga kunder (aktuell månad) | Intäkter för den innevarande månaden (hittills) som tilldelats nya (första gången) kunder jämfört med befintliga kunder (andra eller senare). |
| Genomsnittligt ordervärde (aktuell månad) | Dagsmedelvärde för order som lagts under den aktuella månaden (hittills). Ordervärdet definieras som det slutpris som en kund betalar på en order. |
| Beställningar (aktuell månad) | Antalet order som lagts i din butik för den aktuella månaden (hittills). |
| % ändring i order (MoM MTD) | Jämförelse mellan antalet order för den aktuella månaden (hittills) och samma del av föregående månad. |
| Kontoregistreringar (aktuell månad) | Antalet nyregistrerade konton hittills under den här månaden. |
| % konvertering från registrering till första order (aktuell månad) | Procentandel av konton som hittills registrerats den här månaden och som har beställt. |
| % konvertering från registrering till första order (aktuellt år efter vecka) | Andelen konton som registrerats varje vecka hittills i år och som har beställts. |

## Beställningar

Instrumentpanelen för beställningar ger insikter om transaktionsvolym för beställningar, deras status, vilka kupongkoder som används, genererade intäkter och vilka betalningsmetoder som används. Du kan till exempel spåra leveransprocessen och se till att det inte finns några problem eller flaskhalsar.

>[!NOTE]
>
>Rapporterna på den här instrumentpanelen är tillgängliga för konton som är anslutna till arkiv med någon typ av konfiguration (gästutcheckning, ingen gästutcheckning).

### Rapporter

| Namn | Beskrivning |
|---|---|
| Beställningar (senaste 30 dagarna) | Antalet beställningar som gjorts i din butik under de senaste 30 dagarna. |
| Intäkter (senaste 30 dagarna) | De intäkter som har genererats av din butik under de senaste 30 dagarna. Intäkter definieras som det slutpris som en kund betalar på en order. |
| Genomsnittligt ordervärde (senaste 30 dagarna) | Genomsnittligt ordervärde under de senaste 30 dagarna. Ordervärdet definieras som det slutpris som en kund betalar på en order. |
| Beställningar | Antalet beställningar som görs i din butik varje månad. |
| Intäkter per betalningssätt | Intäkterna som har genererats av din butik, uppdelade efter betalningsmetod. Intäkter definieras som det slutpris som en kund betalar på en order. |
| AOV från nya kontra befintliga kunder | Månadsmedelvärdet av order som gjorts i din butik, delat på order som gjorts av kunder utan tidigare order jämfört med kunder med minst en tidigare order. Ordervärdet definieras som det slutpris som en kund betalar på en order. |
| % beställningar efter status (senaste 30 dagarna) | Procent av order från varje dag under de senaste 30 dagarna som för närvarande har respektive orderstatus. |
| Ofullständiga beställningar (skapade för mer än en dag sedan) | En lista över alla order som lagts för mer än en dag sedan och som fortfarande är ofullständiga (inte annullerade eller fullständiga). |
| Beställningar per timme (senaste 7 dagarna) | Beställ volym per dag och timme. |
| Information om intäkter (senaste 30 dagarna) | Daglig intäktsfördelning de senaste 30 dagarna i alla komponenter av det totala intäktsvärdet. |
| Beställningsinformation per kupongkod (senaste 30 dagarna) | För varje kupongkod som din butik erbjuder ska du ange hur kupongkoden användes och vilka returer den har fått under de senaste 30 dagarna. |
| % beställningar med kupong (senaste 30 dagarna) | Procentandelen order som lagts under de senaste 30 dagarna som använde en kupong jämfört med de som inte gjorde det. |

## Produkter

På produktkontrollpanelen visas den allmänna produktprestandan i termer av beställda produkter, deras bruttovärde för försäljning (GMV) samt de viktigaste produkter som köpts och återbetalats. Det kan hjälpa er att balansera inköp och returer och avgöra om produkterna blir framgångsrika och populära. Din butik måste vara [konfigurerad för att spåra återbetalningar](https://experienceleague.adobe.com/docs/commerce-admin/customers/customer-accounts/store-credit/credit-configure.html) för att dessa diagram ska fyllas i.

>[!NOTE]
>
>Rapporterna på den här instrumentpanelen är tillgängliga för konton som är anslutna till arkiv med någon typ av konfiguration (gästutcheckning, ingen gästutcheckning).

### Rapporter

| Namn | Beskrivning |
|---|---|
| GMV (senaste 30 dagarna) | Bruttovaruvärdet för alla produkter som sålts de senaste 30 dagarna. GMV definieras som beställd kvantitet multiplicerad med baspriset för varje produkt. |
| % GMV (senaste 30 dagarna) återförd | Procent GMV för produkter som köpts under de senaste 30 dagarna och som resulterat i återbetalning. |
| Beställd produktkvantitet (senaste 30 dagarna) | Totalt antal beställda artiklar under de senaste 30 dagarna. |
| % inköpta produkter (senaste 30 dagarna) återförda | Procent av artiklar som köpts under de senaste 30 dagarna och som resulterat i återbetalning. |
| Bruttoomsättningsvärde | Bruttovaruvärdet för alla sålda produkter, per månad. GMV definieras som beställd kvantitet multiplicerad med baspriset för varje produkt. |
| Inköp kontra återbetalning per produkt (senaste 30 dagarna) | För varje produkt, en jämförelse mellan det totala antalet beställda under de senaste 30 dagarna och den ränta som produkten återbetalas med. Storleken på varje bubbla motsvarar återbetalningsnivån. |
| Produktprestandainformation (senaste 30 dagarna) | Detaljerad information om försäljning och efterföljande återbetalningar under de senaste 30 dagarna, per produktsku och produktnamn. |
| Mest köpta produkter av GMV (senaste 30 dagarna) | Produkter som sålts under de senaste 30 dagarna och som genererade störst intäkter (de tio främsta). |
| Mest återfakturerade produkter av GMV (senaste 30 dagarna) | Produkter som köpts under de senaste 30 dagarna och som resulterat i den största förlusten av GMV på grund av återbetalningar (de 10 högsta). |
| Mest köpta produkter per kvantitet (senaste 30 dagarna) | Produkter som sålts de senaste 30 dagarna i det största antalet (de tio bästa). |
| De vanligaste återfakturerade produkterna efter kvantitet (senaste 30 dagarna) | Produkter som köpts under de senaste 30 dagarna och som resulterat i den största återbetalningsmängden (de 10 högsta). |
