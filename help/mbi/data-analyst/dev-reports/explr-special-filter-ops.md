---
title: Speciella filteroperatorer
description: Lär dig mer om några specialoperatorer som används i filter när du skapar en rapport eller ett mätresultat.
exl-id: 12837490-b9ca-4040-bb71-8988b5dde485
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# Filteralternativ

I det här avsnittet utforskas några speciella `operators` som används i `filters` när [en rapport](../../tutorials/using-visual-report-builder.md){: target=&quot;_blank&quot;} eller [som skapar ett mätvärde](../../data-user/reports/ess-manage-data-metrics.md){: target=&quot;_blank&quot;} skapas.

## `Filter Operators`

* `LIKE` för mönstermatchning. Detta måste användas med jokertecknen % (för jokertecken med varierande antal bokstäver) eller _ (för jokertecken med en bokstav).  Begränsningen `LIKE \_ake%` returnerar till exempel true för `Jake Stein`, `Jake Smith` eller `Fake Smith`.  Det returnerar false för `Drake Smith`.

* `NOT LIKE` liknar mönstermatchning ovan, men kontrollerar vilka mönster som inte matchar.

* `IS` kontrollerar om kolumnen är `NULL` eller tom.

* `IS NOT` liknar operatorn `IS` ovan, men söker efter icke-NULL-kolumner.

* `IN` söker efter ett värdes närvaro i en kommaavgränsad lista. (t.ex. &quot;Färg `IN` röd, orange&quot; motsvarar färgen `equal to` röd ELLER färg `equal to` orange).

* `NOT IN` liknar `IN` ovan, men söker efter ett värdes frånvaro.
