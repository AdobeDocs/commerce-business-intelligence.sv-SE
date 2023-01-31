---
title: Välj en rapportbyggare
description: Lär dig hur du väljer Report Builder.
exl-id: ec4204ef-975e-45c3-b09e-fb97ffc2c497
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '783'
ht-degree: 0%

---

# Välj en rapportbyggare

>[!NOTE]
>>Kräver [Administratörsbehörigheter](../../administrator/user-management/user-management.md).


Vi gillar alla att ha alternativ. Men när vi möts av valmöjligheter kan en del av oss halka och frysa ned tanken på att binda sig för ett beslut. Alternativen är bra, men de kan också vara överväldigande och förvirrande.

Nu när du har fler alternativ för att skapa analyser kan det ibland vara svårt att veta exakt vilken variant av rapportverktyget som passar dina behov. Om du behöver hjälp med att välja det bästa sättet att bygga din analys är den här artikeln till dig.

## När ska jag använda `SQL Report Builder`? {#whensql}

Ta en titt på några av de vanligaste anledningarna till att använda SQL Report Builder framför det traditionella Report Builder.

### Om du vill använda SQL-specifika funktioner..

En del av skönheten i `SQL Report Builder` är att det ger dig möjlighet att använda funktioner som för närvarande inte är tillgängliga i Data warehouse Manager. Tidigare kunde en analytiker ha varit tvungen att gå in för att hjälpa dig att förverkliga din vision.

SQL Report Builder stöder funktioner som [`LISTAGG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LISTAGG.html) och [`GETDATE`](https://docs.aws.amazon.com/redshift/latest/dg/r_GETDATE.html)som du inte tidigare kunde använda. Du kommer åt [`full list`](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html), men några andra SQL-specifika funktioner är:

* [`Bitwise aggregate` funktioner](https://docs.aws.amazon.com/redshift/latest/dg/c_bitwise_aggregate_functions.html)
* [`CASE expression`](https://docs.aws.amazon.com/redshift/latest/dg/r_CASE_function.html)
* [`JSON_EXTRACT_PATH_TEXT`](https://docs.aws.amazon.com/redshift/latest/dg/JSON_EXTRACT_PATH_TEXT.html)
* [`LOG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LOG.html)
* [`MONTHS_BETWEEN`](https://docs.aws.amazon.com/redshift/latest/dg/r_MONTHS_BETWEEN_function.html)
* [`REPLACE`](https://docs.aws.amazon.com/redshift/latest/dg/r_REPLACE.html)
* [`SQRT`](https://docs.aws.amazon.com/redshift/latest/dg/r_SQRT.html)
* [`concatenation` operator](https://docs.aws.amazon.com/redshift/latest/dg/r_concat_op.html)

### Om du vill göra lite testning..

Om du vill testa olika tekniker och strategier för att ta reda på vad som fungerar bäst för din analys kan du använda `SQL Report Builder`. Det tar tid att skapa kolumner i Data warehouse Manager och kolumner som du skapar med DWM är beroende av uppdateringscykler.

I bästa fall måste du vänta i en uppdateringscykel innan du kan använda kolumnen. Om du inser att du gjorde fel när du byggde kolumnen måste du vänta igenom *två* cykler: en för att fylla i kolumnen och en annan för att ändringarna ska spridas.

### Om du bara använder en ny kolumn en gång..

Som vi nämnde i avsnittet ovan tar det tid att skapa en ny kolumn i Data warehouse Manager. Om du bara planerar att använda en kolumn som du skapar i en rapport föreslår vi att du använder `SQL Report Builder`. Detta eliminerar behovet av att vänta på att en uppdateringscykel ska slutföras, så att du kommer tillbaka till arbetet snabbare.

### Om du arbetar med data som har en 1:N-relation...

I vissa fall kan datastrukturen göra `SQL Report Builder` ett effektivare och mer logiskt val för att bygga en analys. Det är ganska enkelt att skapa kolumner för en-till-en-relationer i Data warehouse Manager, men det kan bli lite förvirrande när du har att göra med en-till-många-relationer.

Anta att en produkt betraktas som en del av flera produktkategorier, och du vill se de intäkter som är kopplade till varje kategori i varje produkt. Att försöka skapa den här relationen med DWM kan vara långsamt och svårt, men att skriva en SQL-fråga kan vara lite enklare:

![](../../assets/When_should_I_use_the_RB_2.png)

## När ska jag använda Report Builder? {#whentraditionalrb}

Med `SQL Report Builder` ger dig mer kontroll och åtkomst till funktioner som inte är tillgängliga tidigare, och det kanske inte alltid är rätt val. Vi föreslår att du också tar hänsyn till följande när du bestämmer vilken smak av rapportverktyget som ska användas.

### Om du skapar en enkel rapport..

Om det du vill skapa är okomplicerat kan det gå mycket snabbare att använda det traditionella Report Builder än att skriva en fullständig SQL-fråga. Det är också till hjälp om det redan finns kolumner som du behöver för att skapa analysen i Data warehouse Manager.

### Om du delar ditt arbete med andra användare..

Kommer användare i hela organisationen att använda/visa den här analysen? Beroende på vem du delar ditt arbete med kan det i vissa fall vara bättre att hålla dig till Visual Report Builder. Användare kan snabbt titta på definitionen i Visual Report Builder jämfört med att läsa en potentiellt lång SQL-fråga.

Om det finns personer som behöver rapporten men som inte är bekanta med SQL rekommenderar vi att du använder originalaromen från Report Builder. Det kommer att underlätta för dem.

## Radbrytning {#wrapup}

Båda `SQL Report Builder` och `Visual Report Builder` är lämpliga för en mängd olika användningsområden. Detta beror vanligtvis på vilka analysbehov ni har och vilka som kommer att konsumera analysen.
