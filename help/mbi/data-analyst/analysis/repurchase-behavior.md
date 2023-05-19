---
title: Analyserar kundens återköpsbeteende
description: Lär dig hur du analyserar kundens beteende vid återköp.
exl-id: 62666d08-5240-4f19-bf8e-e5b2d79a25c4
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '851'
ht-degree: 1%

---

# Kundens återköpsbeteende

Om ni erbjuder mer än en produkt undrar ni antagligen hur kunder som köper en viss produkt beter sig annorlunda över tiden jämfört med andra kunder. I det här avsnittet behandlas analyser som kan hjälpa dig att svara på följande frågor.

Till kunder som köper en *specifikt objekt*,

* Hur sannolikt är det att de gör ett nytt inköp?
* Hur lång tid tar det för dem att göra ett nytt inköp?
* Vilket är det genomsnittliga antalet order kunderna lägger på kort/lång sikt?
* Hur stor är den genomsnittliga intäkten som kunderna genererar på kort eller lång sikt?

## Rekommenderade mått

När du bygger kundrepriser rekommenderar Adobe att du använder följande mått:

### Sannolikhet för upprepad order

Detta mått definieras som det totala antalet upprepade order, i procent av den totala ordern. Med andra ord är detta sannolikheten för att en order följs av en annan order. Den här åtgärden identifierar objekt som sannolikt kommer att locka kunderna att återvända till din butik.

### Genomsnittligt antal beställningar

Detta visar kundernas inköpsbeteende, närmare bestämt hur många beställningar kunderna har gjort under en viss tidsperiod. Du kan välja att begränsa det här måttet för att se kundernas beteende på kort, medellång eller lång sikt. Vissa produkter kan uppmuntra kunderna att handla ofta på kortare sikt, medan andra kan påverka kundens långsiktiga lojalitet. Om det här antalet är högre för en artikel än för andra artiklar, skulle det tyda på att de som köper den här artikeln är de som kommer tillbaka till din butik.

### Genomsnittlig omsättning för kundens livslängd

Med denna mätmetod kan ni förstå om kunder som köper specifika artiklar är mer värdefulla under deras livstid. Om det här antalet är högre för ett objekt än för andra objekt med liknande pris, kan det tyda på att era kunder med högre värde tenderar att köpa det här objektet.

### Tid till nästa order

Detta mått visar kundens orderfrekvens eller den tid det tar för kunden att beställa igen. Om tiden till nästa beställning är kortare för ett objekt jämfört med andra objekt, kan det tyda på att personer som köper det här objektet ofta kommer tillbaka tidigare.

## Exempel: kaffeprodukter

Se ett exempel på hur man använder kaffeprodukter.

| **Produktnamn** | **Sannolikhet för upprepad order** | **Genomsnittligt antal order under hela livstiden** | **Genomsnittlig intäkt för livstid** | **Mediantid till nästa order** |
|-----|-----|-----|-----|-----|
| Kaffekbryggare i en kopp | 94.98% | 7.92 | $549.82 | 57.01 dagar |
| Kaffekapslar | 93.82% | 8.68 | $479.98 | 63.48 dagar |
| Kaffebönor | 41.92% | 6.07 | $99.82 | 27.31 dagar |

{style="table-layout:auto"}

Nu när ni har era data, vad innebär detta för alla mätvärden?

### Sannolikhet för upprepad order

I det här exemplet är sannolikheten för upprepade order - eller sannolikheten för att en order följs av en annan ordning - mycket högre för kaffebryggare och kaffekapslar med en kopp än för kaffebönor.

Eftersom kunder som köper bryggaren är&quot;engagerade&quot; att köpa de kapslar som hör ihop framöver är detta rimligt. På samma sätt har kunder som köpt kapslar en bryggare som är kompatibel med kapslarna. Kaffebönor är dock inte specifika för någon särskild brygga.

### Genomsnittligt antal order för livslängd

Baserat på ovanstående data kan du se att personer som köper bryggeriet eller kapslarna i genomsnitt har gjort fler inköp under sin livstid jämfört med kunder som har köpt kaffebönor.

### Genomsnittlig omsättning för kundens livslängd

Kunder som köper ett bryggeri har den högsta genomsnittliga livstidsintäkten, vilket är rimligt med tanke på att kostnaden för bryggaren ingår i denna åtgärd. Kunder som köper kaffebönor köper däremot normalt bara lågkostnadsprodukter.

### Tid till nästa order

Bland kunder som köpt kaffekapslar gör hälften en ny beställning på ungefär två månader. Men bland kunder som har köpt kaffebönor gör hälften en återkommande beställning på ungefär en månad. Detta kan bero på att personer som beställer kapslar antingen (1) inte dricker så mycket kaffe, eller (2) beställer i bulk (till exempel köper två månaders kaffe i en order).

## Vilka andra analyser kan jag bygga?

Med hjälp av de mätvärden som beskrivs i det här avsnittet kan du även skapa andra användbara återköpsanalyser. Du kan till exempel även se hur kunderna återköper **samma objekt** - till exempel om de köper påfyllningar regelbundet. Kapslar och kaffebönor kan återköpas regelbundet, men det skulle vara oväntat att se kunderna göra upprepade inköp av kaffebryggaren. Om ni fokuserar på återfyllnad eller återinsättning är den här analysen användbar.

Förutom att analysera återköpets beteende hos era kunder kan ni också skapa analyser som tittar på kundlojaliteten. Överväg att analysera mönster i kundomsättning - var lämnar era kunder er webbplats och inte kommer tillbaka? I vilken takt inträffar detta?

När du har identifierat varför det händer något kan du använda din analys för att skapa en `reactivation` kampanj. Med hjälp av dessa data kan du identifiera användare som har blivit inaktiva, hur länge det har varit sedan deras senaste besök, vilket deras senaste köp var och så vidare. På så sätt kan ni fatta konkreta beslut som får kunderna att komma tillbaka.

Om du behöver hjälp med analys [kontakta support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
