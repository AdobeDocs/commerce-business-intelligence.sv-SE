---
title: Förstå och utvärdera tabellrelationer
description: Lär dig hur du förstår hur många möjliga förekomster i en tabell som kan tillhöra en enhet i en annan.
exl-id: e7256f46-879a-41da-9919-b700f2691013
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '965'
ht-degree: 0%

---

# Förstå och utvärdera tabellrelationer

När du utvärderar relationen mellan två angivna tabeller måste du förstå hur många möjliga förekomster i en tabell som kan tillhöra en enhet i en annan, och vice versa. Använd till exempel en `users` tabell och en `orders` tabell. I det här fallet vill du veta hur många **order** en given **användare** har placerats ut och hur många som är möjliga **användare** en **order** kan tillhöra.

Förståelse av relationer är avgörande för att upprätthålla dataintegriteten, eftersom det påverkar precisionen i dina [beräknade kolumner](../data-warehouse-mgr/creating-calculated-columns.md) och [dimensioner](../data-warehouse-mgr/manage-data-dimensions-metrics.md). Mer information finns på [relationstyper](#types) och [hur du utvärderar tabellerna i Data warehouse.](#eval)

## Relationstyper {#types}

Det finns tre typer av relationer mellan två tabeller:

1. [&quot;1:1&quot;](#onetoone)
1. [&quot;en-till-många&quot;](#onetomany)
1. [&quot;många-till-många&quot;](#manytomany)

### `One-to-One` {#onetoone}

I en `one-to-one` relation, en post i register `B` tillhör endast en post i registret `A`. Och en post i tabellen `A` tillhör endast en post i tabellen `B`.

I förhållandet mellan människor och körkortsnummer kan en person t.ex. bara ha ett körkortsnummer och ett körkortsnummer tillhör endast en person.

![](../../assets/one-to-one.png)

### `One-to-Many` {#onetomany}

I en `one-to-many` relation, en post i register `A` kan eventuellt tillhöra flera poster i tabellen `B`. Fundera på relationen mellan `orders` och `items` - en order kan innehålla många artiklar, men en artikel tillhör en enda order. I det här fallet `orders` tabellen är den ena sidan och `items` bordet är många sidor.

![](../../assets/one-to-many_001.png)

### `Many-to-Many` {#manytomany}

I en `many-to-many` relation, en post i register `B` kan eventuellt tillhöra flera poster i tabellen `A`. Och vice versa, en post i tabellen `A` kan eventuellt tillhöra flera poster i tabellen `B`.

Fundera på relationen mellan **produkter** och **kategorier**: en produkt kan tillhöra många kategorier och en kategori kan innehålla många produkter.

![](../../assets/many-to-many.png)

## Utvärdera dina tabeller {#eval}

Med tanke på vilka typer av relationer som finns mellan tabeller kan du lära dig hur du utvärderar tabellerna i Data warehouse. När de här relationerna utformar hur flertabellskalkylerade kolumner definieras är det viktigt att du förstår hur du identifierar tabellrelationer och vilken sida - `one` eller `many` - tabellen tillhör.

Det finns två metoder som du kan använda för att utvärdera relationerna mellan ett givet tabellpar i Data warehouse. Den första metoden använder en [konceptuellt ramverk](#concept) som beaktar hur tabellens enheter interagerar med varandra. Den andra metoden använder [tabellschema](#schema).

### Använda konceptuella ramverk {#concept}

Den här metoden använder ett konceptuellt ramverk för att beskriva hur enheter i de två tabellerna kan interagera med varandra. Det är viktigt att förstå att detta ramverk bedömer vad som är möjligt, med tanke på relationen.

När du till exempel tänker på användare och beställningar bör du tänka på allt som är möjligt i relationen. En registrerad användare får inte göra några beställningar, bara en beställning eller flera beställningar under sin livstid. Om du har startat din verksamhet och inga beställningar har gjorts är det möjligt att en viss användare kan göra många beställningar under sin livstid. Tabellerna är byggda för att passa detta.

Så här använder du den här metoden:

1. Identifiera den enhet som beskrivs i varje tabell. **Tips: det är vanligtvis ett substantiv**. Till exempel `user` och `orders` tabeller beskriver uttryckligen användare och order.

1. Identifiera ett eller flera verb som beskriver hur dessa enheter interagerar. När man jämför användare med beställningar lägger man order. I den andra riktningen&quot;tillhör&quot; order användare.

Den här typen av ramverk kan användas på alla tabellpar i Data warehouse. På så sätt kan du enkelt identifiera relationstypen och vilken tabell som är en sida och vilken tabell som är en många.

När du har identifierat terminologin som beskriver hur de två tabellerna interagerar bildruta interaktionen i båda riktningarna genom att överväga hur en viss instans av den första entiteten relaterar till den andra. Här är några exempel på varje relation:

### `One-to-One`

En person kan bara ha ett körkortsnummer. En förares körkortsnummer tillhör endast en person.

Det här är en `one-to-one` relation där varje tabell är en sida.

![](../../assets/one-to-one3.png)

### `One-to-Many`

En viss order kan innehålla många artiklar. En given artikel tillhör endast en order.

Det här är en `one-to-many` relation där ordertabellen är den ena sidan och artikeltabellen är många.

![](../../assets/one-to-many3.png)

### `Many-to-Many`

En viss produkt kan eventuellt tillhöra många kategorier. En viss kategori kan innehålla många produkter.

Det här är en `many-to-many` en relation där varje tabell är på många sidor.

![](../../assets/many-to-many3.png)

### Använda tabellens schema {#schema}

Den andra metoden använder tabellschemat. Schemat definierar vilka kolumner som är [`Primary`](https://en.wikipedia.org/wiki/Unique_key) och [`Foreign`](https://en.wikipedia.org/wiki/Foreign_key) nycklar. Du kan använda de här tangenterna för att länka samman tabeller och för att fastställa relationstyper.

När du har identifierat kolumnerna som länkar samman två tabeller använder du kolumntyperna för att utvärdera tabellrelationen. Här är några exempel:

### `One-to-one`

Om tabellerna är länkade med `primary key` för båda tabellerna beskrivs samma unika enhet i varje tabell och relationen är `one-to-one`.

Till exempel en `users` tabellen kan fånga upp de flesta användarattribut (till exempel namn) medan en extra `user_source` tabellen innehåller källor för användarregistrering. I varje tabell representerar en rad en användare.

![](../../assets/one-to-one1.png)

### `One-to-many`

>[!NOTE]
>
>Accepterar du gästbeställningar? Se [Gästorder](../data-warehouse-mgr/guest-orders.md) om du vill veta hur gästbeställningar kan påverka registerrelationerna.

När tabeller länkas med en `Foreign key` peka på en `primary key`beskriver denna konfiguration `one-to-many` relation. Den ena sidan är tabellen som innehåller `primary key` och många sidor är tabellen som innehåller `foreign key`.

![](../../assets/one-to-many1.png)

### `Many-to-many`

Om något av följande är sant är relationen `many-to-many`:

* `Non-primary key` kolumner används för att länka två tabeller
  ![](../../assets/many-to-many1.png)
* Del av en sammansatt bild `primary key` används för att länka två tabeller

![](../../assets/many-to-mnay2.png)

## Nästa steg

En korrekt bedömning av tabellrelationerna är avgörande för att data ska kunna modelleras korrekt. Nu när du förstår hur tabeller är relaterade till varandra kan du se [vad du kan göra med Data warehouse Manager](../data-warehouse-mgr/tour-dwm.md).
