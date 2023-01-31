---
title: Optimera dina SQL-frågor
description: Lär dig hur du optimerar dina SQL-frågor.
exl-id: 2782c707-6a02-4e5d-bfbb-eff20659fbb2
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '823'
ht-degree: 0%

---

# Optimera dina SQL-frågor

Med SQL Report Builder kan du fråga efter och upprepa dessa frågor när du vill. Detta är användbart när du behöver ändra en fråga utan att behöva vänta på att en uppdateringscykel ska slutföras innan en kolumn eller rapport som du har skapat realiseras och behöver uppdateras.

Innan en fråga körs [[!DNL MBI] beräknar kostnaden](https://support.magento.com/hc/en-us/articles/360016730391). Kostnaden tar hänsyn till hur lång tid och hur många resurser som krävs för att köra en fråga. Om kostnaden anses vara för hög eller om antalet returnerade rader överstiger våra gränser, kommer frågan inte att köras. Vi har sammanställt en lista med rekommendationer om hur du ska ställa frågor till data warehouse, så att du kan vara säker på att du skriver så smidiga frågor som möjligt.

## Använda SELECT eller Markera alla kolumner

Om du markerar alla kolumner blir frågan inte aktuell och enkel att köra. Frågor som använder `SELECT *` kan ta en hel del tid att köra, särskilt om tabellen har ett stort antal kolumner.

Därför rekommenderar vi att du undviker att använda `SELECT *` där det är möjligt, och endast inkludera de kolumner du behöver:

| **Istället för det här..** | **Prova det här!** |
|-----|-----|
| ![](../../mbi/assets/Select_all_1.png) | ![](../../mbi/assets/Select_all_2.png) |

{style=&quot;table-layout:auto&quot;}

## Använda fullständiga yttre hörn

Yttre kopplingar markerar hela tabellen som kopplas, vilket ökar frågans beräkningskostnad. Det innebär att det tar längre tid att köra frågan och att den troligtvis misslyckas eftersom det kan ta längre tid än vad som krävs för att returnera resultatet.

I stället för att använda den här typen av förening bör du använda en inre eller vänster koppling. Inre kopplingar returnerar bara resultat där tHere är en kolumnmatchning mellan tabeller (till exempel `order_id` finns i båda en typisk `customers` och `orders` tabell), vänsterkopplingar returnerar alla resultat från den vänstra (första) tabellen tillsammans med matchande resultat i den högra (andra) tabellen.

Ta en titt på hur vi kan skriva om en FULL OUTER JOIN-fråga:

| **Istället för det här..** | **Prova det här!** |
|-----|-----|
| ![](../../mbi/assets/Full_Outer_Join_1.png) | ![](../../mbi/assets/Full_Outer_Join_2.png) |

{style=&quot;table-layout:auto&quot;}

Som du ser är de här frågorna identiska på alla sätt förutom den typ av JOIN de använder.

## Använda flera hörn

Även om du kan ta med flera kopplingar i frågan måste du komma ihåg att det kan leda till högre kostnader för frågan. För att undvika att hamna på kostnadströskeln rekommenderar vi att du undviker flera kopplingar där det är möjligt.

## Använda filter

Använd filter när det är möjligt. `WHERE` och `HAVING` -satser kommer att filtrera dina resultat och ge dig bara de data du verkligen vill ha.

## Använda filter i JOIN-satser

Om du använder ett filter när du gör en koppling måste du använda det på båda tabellerna i kopplingen. Även om det är överflödigt minskar detta beräkningskostnaderna för frågan och förkortar körningstiden.

| **Istället för det här..** | **Prova det här!** |
|-----|-----|
| ![](../../mbi/assets/Join_filters_1.png) | ![](../../mbi/assets/Join_filters_2.png) |

{style=&quot;table-layout:auto&quot;}

## Använda operatorer

När du skriver frågor bör du överväga att använda operatorer som är så dyra som möjligt. Varje fråga har en beräkningskostnad som bestäms av de funktioner, operatorer och filter som frågan består av. Vissa operatorer kräver mindre datorarbete, vilket gör dem billigare än andra operatorer.

Jämförelseoperatorer (>, &lt;, = o.s.v.) är de mest kostsamma, följt av [SOM. LIKNANDE operatorer till och POSIX-operatorer](https://www.postgresql.org/docs/9.5/functions-matching.html) som är de dyraste operatörerna.

## Använda EXIST jämfört med IN

Använda `EXISTS` kontra `IN` beror på vilken typ av resultat du försöker returnera. Om du bara är intresserad av ett enda värde använder du `EXISTS` -sats i stället för `IN`. `IN` används tillsammans med listor med kommaavgränsade värden, vilket ökar frågans beräkningskostnad.

När `IN` frågor körs, systemet måste först bearbeta underfrågan (den `IN` -programsats), sedan hela frågan baserat på relationen som anges i `IN` -programsats. `EXISTS` är mycket effektivare eftersom frågan inte behöver köras flera gånger - ett sant/falskt värde returneras när relationen som anges i frågan kontrolleras.

Kort sagt: systemet inte behöver bearbeta så mycket när det använder `EXISTS`.

| **Istället för det här..** | **Prova det här!** |
|-----|-----|
| ![](../../mbi/assets/Exists_1.png) | ![](../../mbi/assets/Exists_2.png) |

{style=&quot;table-layout:auto&quot;}

## Använda ORDER BY

`ORDER BY` är en dyr funktion i SQL och kan avsevärt öka kostnaden för en fråga. Om du får ett felmeddelande om att EXPLAIN-kostnaden för din fråga är för hög kan du försöka med att ta bort eventuella `ORDER BY`är från din fråga såvida det inte är absolut nödvändigt.

Det här är inte att säga att `ORDER BY` inte kan användas - bara att det bara ska användas när det är nödvändigt.

## Använda GROUP BY och BESTÄLL AV

Även om det finns vissa situationer där detta tillvägagångssätt inte överensstämmer med det du försöker göra, är den allmänna regeln att om du använder en `GROUP BY` och `ORDER BY`ska du placera kolumnerna i båda satserna i samma ordning. Till exempel:

| **Istället för det här..** | **Prova det här!** |
|-----|-----|
| ![](../../mbi/assets/Group_by_2.png) | ![](../../mbi/assets/Group_by_1.png) |

{style=&quot;table-layout:auto&quot;}

## Radbrytning

Det bästa sättet att lära sig skriva SQL - och göra det effektivt - är genom testversioner och fel. Om du vill hitta det som fungerar bäst för dig kan du försöka återskapa några rapporter med enbart SQL-redigeraren.
