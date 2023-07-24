---
title: Optimera dina SQL-frågor
description: Lär dig hur du optimerar dina SQL-frågor.
exl-id: 2782c707-6a02-4e5d-bfbb-eff20659fbb2
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '779'
ht-degree: 0%

---

# Optimera dina SQL-frågor

The [!DNL SQL Report Builder] låter dig fråga och iterera i dessa frågor när som helst. Detta är användbart när du behöver ändra en fråga utan att behöva vänta på att en uppdateringscykel ska slutföras innan en kolumn eller rapport som du har skapat realiseras och behöver uppdateras.

Innan en fråga körs [[!DNL Commerce Intelligence] beräknar kostnaden](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/sql-queries-explain-cost-errors.html). Kostnad anger hur lång tid och hur många resurser som krävs för att köra en fråga. Om kostnaden anses vara för hög eller om antalet returnerade rader överstiger [!DNL Commerce Intelligence] begränsningar, frågan misslyckas. För att fråga [data warehouse](../data-analyst/data-warehouse-mgr/tour-dwm.md), som ser till att du skriver så smidiga frågor som möjligt, rekommenderar Adobe följande.

## Använda SELECT eller Markera alla kolumner

Om du markerar alla kolumner blir frågan inte aktuell och enkel att köra. Frågor som använder `SELECT *` kan ta en hel del tid att köra, särskilt om tabellen har många kolumner.

Därför rekommenderar Adobe att du undviker att använda `SELECT *` där det är möjligt, och endast inkludera de kolumner du behöver:

| **Istället för det här..** | **Prova det här!** |
|-----|-----|
| ![](../../mbi/assets/Select_all_1.png) | ![](../../mbi/assets/Select_all_2.png) |

{style="table-layout:auto"}

## Använda fullständiga yttre hörn

Yttre kopplingar markerar hela tabellen som kopplas, vilket ökar frågans beräkningskostnad. Det innebär att det tar längre tid att köra frågan och att den troligtvis misslyckas eftersom det kan ta längre tid än vad som krävs för att returnera resultatet.

I stället för att använda den här typen av förening bör du använda en inre eller vänster koppling. Inre kopplingar returnerar bara resultat när det finns en kolumnmatchning mellan tabeller (till exempel `order_id` finns i båda en typisk `customers` och `orders` tabell). Vänsterfogar returnerar alla resultat från den vänstra (första) tabellen tillsammans med matchande resultat i den högra (andra) tabellen.

Se hur du kan skriva om en FULL OUTER JOIN-fråga:

| **Istället för det här..** | **Prova det här!** |
|-----|-----|
| ![](../../mbi/assets/Full_Outer_Join_1.png) | ![](../../mbi/assets/Full_Outer_Join_2.png) |

{style="table-layout:auto"}

De här frågorna är identiska på alla sätt förutom den typ av JOIN som de använder.

## Använda flera hörn

Även om du kan ta med flera kopplingar i frågan måste du komma ihåg att det kan leda till högre kostnader för frågan. För att undvika att uppnå kostnadströskeln rekommenderar Adobe att man undviker flera kopplingar där det är möjligt.

## Använda filter

Använd filter när det är möjligt. `WHERE` och `HAVING` -satser filtrerar resultaten och ger dig bara de data du verkligen vill ha.

## Använda filter i JOIN-satser

Om du använder ett filter när du gör en koppling måste du använda det på båda tabellerna i kopplingen. Även om det är överflödigt minskar detta beräkningskostnaderna för frågan och minskar körningstiden.

| **Istället för det här..** | **Prova det här!** |
|-----|-----|
| ![](../../mbi/assets/Join_filters_1.png) | ![](../../mbi/assets/Join_filters_2.png) |

{style="table-layout:auto"}

## Använda operatorer

När du skriver frågor bör du överväga att använda operatorer som är så dyra som möjligt. Varje fråga har en beräkningskostnad som bestäms av de funktioner, operatorer och filter som frågan består av. Vissa operatorer kräver mindre datorarbete, vilket gör dem billigare än andra operatorer.

Jämförelseoperatorer (>, &lt;, = o.s.v.) är de mest kostsamma, följt av [SOM. LIKNANDE operatorer till och POSIX-operatorer](https://www.postgresql.org/docs/9.5/functions-matching.html) som är de dyraste operatörerna.

## Använda EXIST jämfört med IN

Använda `EXISTS` kontra `IN` beror på vilken typ av resultat du försöker returnera. Om du bara är intresserad av ett enda värde använder du `EXISTS` -sats i stället för `IN`. `IN` används med listor med kommaavgränsade värden, vilket ökar frågans beräkningskostnad.

När `IN` frågor körs, systemet måste först bearbeta underfrågan (den `IN` -programsats), sedan hela frågan baserat på relationen som anges i `IN` -programsats. `EXISTS` är mycket effektivare eftersom frågan inte behöver köras flera gånger - ett sant/falskt värde returneras när relationen som anges i frågan kontrolleras.

Kort sagt: systemet inte behöver bearbeta så mycket när det använder `EXISTS`.

| **Istället för det här..** | **Prova det här!** |
|-----|-----|
| ![](../../mbi/assets/Exists_1.png) | ![](../../mbi/assets/Exists_2.png) |

{style="table-layout:auto"}

## Använda ORDER BY

`ORDER BY` är en dyr funktion i SQL och kan avsevärt öka kostnaden för en fråga. Om du får ett felmeddelande om att EXPLAIN-kostnaden för din fråga är för hög kan du försöka med att ta bort eventuella `ORDER BY`är från din fråga om det inte behövs.

Det här är inte att säga att `ORDER BY` kan inte användas - bara att den bara ska användas när det är nödvändigt.

## Använda GROUP BY och BESTÄLL AV

Det kan finnas situationer där detta tillvägagångssätt inte överensstämmer med vad du försöker göra. Den allmänna regeln är att om du använder en `GROUP BY` och `ORDER BY`ska du placera kolumnerna i båda satserna i samma ordning. Till exempel:

| **Istället för det här..** | **Prova det här!** |
|-----|-----|
| ![](../../mbi/assets/Group_by_2.png) | ![](../../mbi/assets/Group_by_1.png) |

{style="table-layout:auto"}

## Radbrytning

Det bästa sättet att lära sig skriva SQL - och göra det effektivt - är genom testversioner och fel. Om du vill hitta det som fungerar bäst för dig kan du försöka återskapa några rapporter med enbart SQL-redigeraren.
