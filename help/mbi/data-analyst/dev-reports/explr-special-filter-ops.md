---
title: Speciella filteroperatorer
description: Lär dig mer om några specialoperatorer som används i filter när du skapar en rapport eller ett mätresultat.
exl-id: 12837490-b9ca-4040-bb71-8988b5dde485
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# Filteralternativ

I den här artikeln ska vi utforska några speciella `operators` används i `filters` när [skapa en rapport](../../tutorials/using-visual-report-builder.md){: target=&quot;_blank&quot;} eller [skapa ett mått](../../data-user/reports/ess-manage-data-metrics.md){: target=&quot;_blank&quot;}.

## `Filter Operators`

* `LIKE` för mönstermatchning. Detta måste användas tillsammans med jokertecknen % (för jokertecken med varierande antal bokstäver) eller _ (för jokertecken med en bokstav).  Begränsningen `LIKE \_ake%` skulle returnera true för `Jake Stein`, `Jake Smith`, eller `Fake Smith`.  Det returnerar false för `Drake Smith`.

* `NOT LIKE` liknar mönstermatchning ovan, men kontrollerar för vilka mönster inte matchar.

* `IS` kontrollerar om kolumnen är `NULL`, eller tom.

* `IS NOT` liknar `IS` -operatorn ovan, men söker efter icke-NULL-kolumner.

* `IN` kontrollerar om ett värde finns i en kommaavgränsad lista. (t.ex. &quot;Färg `IN` red,orange&quot; motsvarar färg `equal to` röd eller färg `equal to` orange).

* `NOT IN` liknar `IN` ovan, men söker efter ett värdes frånvaro.
