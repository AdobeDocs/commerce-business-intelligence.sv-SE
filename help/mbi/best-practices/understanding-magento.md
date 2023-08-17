---
title: Förstå [!DNL Commerce Intelligence] Miljö
description: Lär dig hur du arbetar med och förbättrar [!DNL Commerce Intelligence] miljö.
exl-id: 601b5fba-da02-4cc8-96ed-147c24f326f9
role: Admin, Data Architect, Data Engineer, User
feature: Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 0%

---

# Dina [!DNL Adobe Commerce Intelligence] Miljö

När ni analyserar era e-handelsdata bör ni vara medvetna om dessa faktorer och vanliga missuppfattningar. Om du behöver hjälp med att se till att du använder ditt Commerce-schema på rätt sätt går det bra att [kontakta support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

## [!DNL entity\_id]

Många av tabellerna innehåller en kolumn med namnet `entity\_id`. I varje tabell som innehåller `entity\_id`används kolumnen för att identifiera unika rader.

Till exempel varje rad i `sales\_order` tabellen är en unik order. Primärnyckeln i tabellen anropas `entity\_id`. Den här kolumnen kan tolkas som `order\_id`. I en separat tabell `customer\_entity`, representerar varje rad en unik kund. Primärnyckeln i den här tabellen anropas också `entity\_id`som man kan tänka sig som `customer\_id`.

I de tabellerna `sales\_order.entity\_id` är inte lika med `customer\_entity.entity\_id`. Detta gäller för alla tabelluppsättningar som innehåller `entity\_id`: `table\_A.entity\_id` är inte lika med `table\_B.entity\_id`.

## [!DNL Guest orders]

Om du tillåter kunder att beställa från din webbplats utan att ha ett konto (gästbeställningar) fylls dessa kunder inte i som en rad i din `customer\_entity` tabell. Dessutom har varje order som en gäst placerar ett null-värde `customer\_id` värdet på `sales\_order` tabell.

Om du vill spåra gästernas beteenden över tid måste därför alla kundnivåkolumner beräknas på `sales\_order` register, använda en kundidentifierare som `customer\_email`.

Om du använder `sales\_order` som kundregister måste ni vara försiktiga när ni skapar kundnivåstatistik. Ta till exempel en genomsnittlig intäktssiffra för livstid. Det här måttet används för att identifiera de genomsnittliga intäkterna för hela kundlivscykeln. För det första krävs det en ny kolumn som för varje kund returnerar livstidsintäkterna. Sedan måste ni beräkna genomsnittsvärdet för den här kolumnen för att få kundernas genomsnittliga livstidsintäkter.

Om du kan använda `customer\_entity` tabellen är varje rad en enda kund, och varje kund finns bara en gång i tabellen. När du har livstidsintäktskolumnen behöver du därför bara skapa ett medelvärde. Om du använder `sales\_order` tabellen som kundtabell kan en kund finnas på flera rader. När du har ställt in livstidsintäktskolumnen kommer varje order (rad) som läggs av en viss kund att visa kundens livstidsintäkt, men du vill bara inkludera den kunden en gång i det övergripande medelvärdet.

Tricket här är att ni måste lägga till ett filter i mätvärdena som ser till att ni bara inkluderar varje kund en gång. Adobe rekommenderar att du skapar och använder en filteruppsättning med namnet **Kunder vi räknar** som filtrerar efter **Kundens ordernummer = 1** (bland annat kan du behöva exkludera oönskade kunder). Genom att lägga till det här filtret kan du bara inkludera varje kund en gång i kundnivåmätningen.

## Produkter och kategorier

Produkter kan ha flera kategorier och kategorier kan användas för mer än en produkt. När du ställer in kategorinivåanalyser måste du därför vara noga med att använda rätt definitioner. Vill du ha kategorin på den översta nivån? Kategori på andra nivån? Vad händer om produkten kan delas in i flera kategorier på den översta nivån?

Föreställ dig ett par jeans som faller inom tre olika kategorinivåer, enligt en Commerce-implementering: Clothing (översta nivån), Outerwear (andra nivån) och Pants (tredje nivån). Du kanske vill analysera kategoriernas prestanda utifrån antalet sålda enheter. Det mätvärde du behöver för analysen är _Sålda artiklar_ som bygger på `sales\_order\_item` tabell. Därför måste du flytta information på kategorinivå till objekttabellen. Varje rad på `sales\_order\_item` tabellen har en associerad `product\_id`så om du vet vilka kategorier som är kopplade till en produkt, kan du överföra den informationen till önskad tabell.

Innan du flyttar data måste du känna till vilka kopplingar och filter som behövs för att du ska kunna hitta rätt kategori. För vissa analyser kan du behöva känna till &quot;myror&quot;, men i andra analyser kan &#39;Clothing&#39; vara mer lämpligt. Dessa är distinkta kategorier som identifieras separat. Genom att veta hur varje kategorinivå är definierad kan du attribuera enhetsförsäljningen till rätt kategori för din specifika analys.

Tänk dig att du också har en `Our Favorites` kategori på den översta nivån på webbplatsens hemsida. Du kanske har implementerat din Commerce Store för att inkludera dessa jeans i båda `Clothing` kategori och `Our Favorites` kategori. I så fall har dessa jeans mer än en kategori på den översta nivån. I så fall flyttas en enskild kategori på den översta nivån till `sales\_order\_item` tabellen är inte helt logisk eftersom det finns flera alternativ. För att ta hänsyn till detta föreslår Adobe att du skapar ja/nej-kolumner som söker efter specifika kategorier. Till exempel: `Is product in Clothing category?` och `Is product in Our Favorites category?` Med -kolumner kan du kontrollera om en produkt tillhör dessa specifika kategorier.
