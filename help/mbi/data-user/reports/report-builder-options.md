---
title: Välj en rapportbyggare
description: Lär dig hur du väljer Report Builder.
exl-id: ec4204ef-975e-45c3-b09e-fb97ffc2c497
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---

# Välj en rapportbyggare

>[!NOTE]
>&#x200B;>Kräver [administratörsbehörighet](../../administrator/user-management/user-management.md).

Nu när du har fler alternativ för att skapa analyser kan det ibland vara svårt att veta exakt vilken version av rapporten som passar dina behov. I det här avsnittet får du hjälp med att välja det bästa sättet att bygga din analys.

## När ska jag använda [!DNL SQL Report Builder]? {#whensql}

Titta på några av de vanligaste anledningarna till att du använder [!DNL SQL Report Builder] över [!DNL traditional Report Builder].

### Om du vill använda [!DNL SQL]-specifika funktioner..

En del av skönheten i [!DNL SQL Report Builder] är att det ger dig möjlighet att använda funktioner som inte är tillgängliga i Data Warehouse Manager. Tidigare kunde en analytiker ha varit tvungen att gå in för att hjälpa dig att förverkliga din vision.

[!DNL SQL Report Builder] stöder funktioner som [`LISTAGG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LISTAGG.html) och [`GETDATE`](https://docs.aws.amazon.com/redshift/latest/dg/r_GETDATE.html) som du inte tidigare kunde använda. Du kan komma åt [`full list`](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html), men några andra SQL-specifika funktioner är:

* [`Bitwise aggregate` funktioner](https://docs.aws.amazon.com/redshift/latest/dg/c_bitwise_aggregate_functions.html)
* [`CASE expression`](https://docs.aws.amazon.com/redshift/latest/dg/r_CASE_function.html)
* [`JSON_EXTRACT_PATH_TEXT`](https://docs.aws.amazon.com/redshift/latest/dg/JSON_EXTRACT_PATH_TEXT.html)
* [`LOG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LOG.html)
* [`MONTHS_BETWEEN`](https://docs.aws.amazon.com/redshift/latest/dg/r_MONTHS_BETWEEN_function.html)
* [`REPLACE`](https://docs.aws.amazon.com/redshift/latest/dg/r_REPLACE.html)
* [`SQRT`](https://docs.aws.amazon.com/redshift/latest/dg/r_SQRT.html)
* Operatorn [`concatenation` ](https://docs.aws.amazon.com/redshift/latest/dg/r_concat_op.html)

### Om du vill göra lite testning..

Om du vill testa olika tekniker och strategier för att ta reda på vad som fungerar bäst för din analys kan du använda [!DNL SQL Report Builder]. Det tar tid att skapa kolumner i Data Warehouse Manager och kolumner som du skapar med DWM är beroende av uppdateringscykler.

I bästa fall måste du vänta i en uppdateringscykel innan du kan använda kolumnen. Om du upptäcker att du gjorde ett misstag när du skapade kolumnen måste du vänta igenom *två* cykler: en för att fylla i kolumnen och en annan cykel för att ändringarna ska spridas.

### Om du bara använder en ny kolumn en gång..

Som vi nämnt ovan tar det tid att skapa en Data Warehouse i kolumnhanteraren. Om du bara planerar att använda en kolumn som du skapar i en rapport föreslår Adobe att du använder [!DNL SQL Report Builder]. Det eliminerar behovet av att vänta på att en uppdateringscykel ska slutföras så att du kommer tillbaka till arbetet snabbare.

### Om du arbetar med data som har en 1:N-relation...

Ibland kan datastrukturen göra [!DNL SQL Report Builder] till ett mer effektivt och logiskt val för att skapa din analys. Det är enkelt att skapa kolumner för en-till-en-relationer i Data Warehouse Manager, men det kan bli lite förvirrande när du hanterar en-till-många-relationer.

Säg att en produkt betraktas som en del av flera produktkategorier, och du vill se de intäkter som är kopplade till varje produktkategori. Att försöka skapa den här relationen med DWM kan vara långsamt och svårt, men det kan vara lite enklare att skriva en [!DNL SQL]-fråga:

![](../../assets/When_should_I_use_the_RB_2.png)

## När ska jag använda Report Builder? {#whentraditionalrb}

Även om [!DNL SQL Report Builder] ger dig mer kontroll och åtkomst till funktioner som inte är tillgängliga tidigare är det inte alltid rätt val. Adobe föreslår att du även ska tänka på följande när du bestämmer vilken variant av rapportverktyget som ska användas.

### Om du skapar en enkel rapport..

Om det du vill skapa är okomplicerat kan det gå mycket snabbare att använda det traditionella Report Builder än att skriva en fullständig [!DNL SQL]-fråga. Det hjälper om det redan finns kolumner som du behöver för att skapa analysen i Data Warehouse Manager.

### Om du delar ditt arbete med andra användare..

Använder/visar användarna i hela organisationen den här analysen? Beroende på vem du delar ditt arbete med kan det ibland vara bättre att hålla dig till Visual Report Builder. Användare kan snabbt titta på definitionen i [!DNL Visual Report Builder] jämfört med att läsa en potentiellt lång [!DNL SQL]-fråga.

Om det finns personer som behöver rapporten men som inte är bekanta med [!DNL SQL] föreslår Adobe att du använder den ursprungliga varianten av Report Builder. Det gör det enklare för dem.

## Radbrytning {#wrapup}

Både [!DNL SQL Report Builder] och [!DNL Visual Report Builder] passar för en mängd olika användningsområden. Detta beror vanligtvis på vilka analysbehov ni har och vilka som förbrukar analysen.
