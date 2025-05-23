---
title: Analyserar kupongpåverkan
description: Lär dig hur du analyserar kupongpåverkan på kundvärvning och kundunderhåll.
exl-id: b0619365-fa75-49b5-a393-87f3364a390f
role: Admin, User
feature: Data Warehouse Manager, Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '1382'
ht-degree: 1%

---

# Kupongpåverkan

Analysera hur kunderna använder era kuponger för att få goda insikter om ert företag. Analysera hur ni förvärvar och behåller kunder via kuponger. I det här avsnittet behandlas analyser som kan hjälpa dig att besvara följande typer av frågor:

* Hur många kunder köper du via kuponger?
* Är det mer sannolikt att kupongförvärvade kunder gör återkommande inköp än kunder som inte har köpt via kuponger?
* Hur skiljer sig de genomsnittliga intäkterna för livstid mellan kupongförvärvade kunder och kunder som inte förvärvats via kuponger?
* Gör kunder som förvärvats från kuponger återkommande inköp med kuponger?

Svara på dessa frågor genom att fokusera på att [jämföra kupongförvärvade kunder med icke-kupongförvärvade kunder](#compare), [analysera information om första order från kupongförvärv](#firstorder) och [titta på attributen hos kunder som använder kuponger i sin första order.](#attributes)

Kom igång!

## Jämföra kupongförvärvade kunder med icke-kupongförvärvade kunder {#compare}

När du bygger analyser som utforskar förvärv och kvarhållande av kuponger bör du använda följande mätvärden:

### Antal nya kunder

Denna mätmetod visar hur många kupongköpta och icke kupongförvärvade kunder som har kommit över hela tiden. Detta kan hjälpa er att avgöra förhållandet mellan kundförvärv via kuponger.

### Genomsnittlig intäkt för livstid

Den här mätningen visar de genomsnittliga livstidsintäkterna från kuponger och icke-kupongförvärvade kunder. Detta kan hjälpa till att avgöra om en kunds livstidsvärde varierar beroende på vilken typ av förvärv kunden har.

### Antal upprepade order

Den här mätningen visar antalet upprepade order som gjorts av båda typerna av kundförvärv. Detta kan hjälpa till att avgöra om fler uppföljningsorder läggs av kupongförvärvade eller icke-kupongförvärvade kunder.

### Antal och procent upprepade order med kupong

Här visas antalet upprepade order som gjorts med en kupong och procentandelen upprepade order som gjorts med en kupong. Detta kan hjälpa er att avgöra om kupongförvärvade kunder tenderar att göra fler upprepade order med en kupong än icke-kupongförvärvade kunder och om kupongförvärvade kunder använder kuponger oproportionerligt i sina uppföljningsorder.

Titta på några exempeldata för inlösen av kuponger jämfört med icke-kuponganskaffningsvärden:

| **Kundvärvning** | **Antal nya kunder** | **Inkomster för genomsnittlig livstid** | **Antal upprepade order** | **Antal upprepade order med kupong** | **% av upprepade order med kupong** |
|-----|-----|-----|-----|-----|-----|
| Kupong | 1 206 | 356,91 USD | 2 570 | 1 248 | 48,56 % |
| Icke-kupong | 11 561 | 498,30 USD | 20 145 | 3 251 | 16,14 % |

{style="table-layout:auto"}

Se vad du kan ta bort från detta:

### Antal nya kunder

I ovanstående exempel finns ett mycket större antal förvärv som inte är kupongförvärv än kupongförvärv. Det finns dock fortfarande 1 206 kunder som förvärvats via en kupong som annars inte hade blivit kunder.

### Genomsnittlig intäkt för livstid

I det här exemplet har förvärv utan kupong en högre genomsnittlig intäkt för livstid än förvärv av kupong. Detta innebär att förvärv av icke-kuponger gör fler återkommande inköp och/eller gör större värdeinköp.

### Antal upprepade order

Antalet upprepade order för icke-kupongförvärv är mycket högre än kupongförvärv. Detta är förväntat eftersom det finns många fler kunder som inte har kupongköp.

### Antal upprepade order med kupong

På samma sätt är antalet upprepade order som görs med en kupong högre för icke-kupongförvärv.

## Procent upprepade order med kupong

Icke-kupongförvärvade kunder har en mycket lägre andel upprepade order med en kupong än kupongförvärvade kunder. För kupongförvärvade kunder tillämpas alltså nästan hälften av alla upprepade order på en kupong. I det här exemplet brukar kupongköpare göra upprepade inköp med kuponger.

## Analyserar information om första order från kupongförvärv {#firstorder}

Det här avsnittet fokuserar bara på **första order från kupongförvärv, segmenterade efter kupong.** Använd dessa mått i din analys:

### Antal order/kunder

Den här mätningen visar antalet första beställningar för varje kupong, eller antalet kunder som använde kupongen i sin första order. Detta kan hjälpa till att avgöra om en viss kupong uppmuntrar fler förstagångsköp än andra kuponger.

### Bruttointäkter

Det här måttet visar de intäkter du tjänar på en viss kupong som användes i en kunds första order. Denna intäkt är en beräkning av artiklar som sålts innan någon rabatt tillämpas.

### Rabatter från kuponger

Det här måttet visar det totala rabattbeloppet som tillämpas från kupongen.

### Nettointäkter

Det här måttet visar de intäkter du tjänar på en viss kupong som användes i en kunds första order. Denna intäkt är en beräkning av artiklar som säljs efter att alla rabatter har tillämpats. Det är viktigt att notera att nettointäkterna kanske inte har uppstått utan kupongerna.

### Genomsnittligt ordervärde

Detta mått visar det genomsnittliga ordervärdet för en viss kupong.

### Genomsnittligt antal order för livslängd

Den här mätningen hjälper till att utvärdera lojalitet och genomsnittligt antal order som genereras av kunder som använder en viss kupong.

### Genomsnittlig intäkt för livstid

Denna mätning hjälper till att utvärdera lojalitet och genomsnittliga intäkter som genereras av kunder som använder en viss kupong. När du utvärderar om kunder som använder kuponger har större värde än andra måste du ta hänsyn till hur många order varje kupong användes i för att vara säker på att du har ett stort urval.

Titta nu på ett exempel med tre olika kuponger som används för kundens första beställning:

| **Kupong** | **Första gången beställningar (FTO)** | **Bruttointäkter från FTO** | **Rabatterna tillämpas på FTO** | **Nettointäkter från FTO** | **Genomsnittligt ordervärde för FTO** |
|-----|-----|-----|-----|-----|-----|
| **25 % rabatt på $100 eller mer** | 56 | $8 531.04 | $2 132.76 | 6 398,28 USD | 152,34 USD |
| **$10 rabatt** | 87 | 3 707 USD | 426,10 USD | 3 280,97 USD | 42,61 USD |
| **20 % rabatt** | 145 | 10 975 USD | $2 195.01 | $8 780.04 | 75,69 USD |

{style="table-layout:auto"}

Vad kan man ta av detta? För det första fick kupongen&quot;20 % rabatt&quot; flest beställningar första gången. Antalet beställningar som är kopplade till varje kupong kan dock variera beroende på flera faktorer, bland annat:

* mängden annonsering för varje kupong.
* hur länge kupongen erbjuds.
* den tidpunkt på dag/vecka/månad/år då kupongen erbjöds.
* den säsong då kupongen erbjöds, beroende på verksamheten.

  **Exempel:**&quot;20 % rabatt&quot;-kupongen erbjöds under sommarmånaderna, men företaget säljer vinterkläder.
* begränsningar för kupongerna.

  **Exempel:** kupongen&quot;10 % rabatt&quot; erbjuds endast kunder som köper en vinterjacka i samma ordning.

**Bruttointäkten** för kupongen&quot;25 % rabatt på 100 USD eller mer&quot; är mycket högre än bruttointäkten för kupongen&quot;$10&quot;. Kupongen&quot;$10&quot; har emellertid ett mycket större **antal order**. Analyser av det **genomsnittliga ordervärdet** ger insikter om de här skillnaderna. Även om kupongen&quot;25 % rabatt på 100 USD eller mer&quot; hade färre order är det genomsnittliga ordervärdet mer än tre gånger så mycket som kupongen&quot;10 USD&quot;. Därför tillskrivs en större bruttointäkt&quot;25 % rabatt på 100 USD eller mer&quot;.

**Rabatterna** och **nettointäkterna** för kupongen&quot;25 % rabatt på 100 eller mer&quot; och&quot;20 % rabatt&quot; ligger nära värdet. Även om det genomsnittliga ordervärdet för&quot;25 % rabatt på 100 USD eller mer&quot; är nästan dubbelt så stort som det genomsnittliga ordervärdet för&quot;20 % rabatt&quot; har den senare kupongen lite mindre än tre gånger så många order.

## Attribut för kunder som använder kuponger i sin första order {#attributes}

Nu när ni har tittat på själva beställningarna, titta på de kunder som använder kuponger i sina första order:

| **Kundens första orderkupong** | **Antal kunder** | **Genomsnittligt antal order under hela löptiden** | **Inkomster för genomsnittlig livstid** |
|-----|-----|-----|-----|
| **25 % rabatt på $100 eller mer** | 56 | 2,8 | 554,54 USD |
| **$10 rabatt** | 87 | 1,9 | 115,50 USD |
| **20 % rabatt** | 145 | 1,3 | $103.75 |

{style="table-layout:auto"}

Ni märker att antalet förstagångsbeställningar är samma som antalet kunder för varje kupong. Detta är rimligt eftersom varje kund bara kan ha en första order.

Det största antalet kunder förvärvades genom kupongen&quot;20 % rabatt&quot;. Dessa kunder har dock det lägsta **genomsnittliga antalet order** och **genomsnittliga intäkter för livstid** som varar i genomsnitt, och de flesta kupongförvärvade kunder gör inga upprepade order. Dessutom genererar kunder som har förvärvats via kupongen&quot;25 % rabatt på 100 USD eller mer&quot; ett högre **genomsnittligt antal order under hela löptiden** och i sin tur högre **genomsnittlig intäkt under hela livstiden**. I allmänhet kommer användare som köptes via den här kupongen oftast tillbaka och gör fler återkommande inköp.

## Radbrytning {#wrapup}

Det finns en mängd analyser som ni kan skapa för att bättre förstå hur kunderna använder kuponger. Har du någonsin funderat på att analysera hur era kunder använder era kuponger eller hur lång tid det tar för kuponger att användas? Vad sägs om att hitta det optimala rabattbeloppet - vilket belopp uppmuntrar fler köpare att köpa, högre genomsnittligt ordervärde och högre intäkter under hela löptiden? [Kontakta support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=sv-SE) om du behöver hjälp med de här typerna av frågor.
