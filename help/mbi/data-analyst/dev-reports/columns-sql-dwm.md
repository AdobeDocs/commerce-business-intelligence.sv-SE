---
title: Skillnader mellan SQL och Data warehouse Manager
description: Lär dig skillnaderna mellan SQL och Data warehouse Manager.
exl-id: 31dd7a04-5c03-4399-b67e-f51703eb9fea
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# Skillnader mellan SQL och Data warehouse Manager

Det finns två viktiga skillnader mellan kolumner som skapas i [SQL Report Builder](../dev-reports/sql-rpt-bldr.md) och de som skapats med [data warehouse Manager](../data-warehouse-mgr/creating-calculated-columns.md): ett är beroende av uppdateringscykler, det andra är hur kolumner sparas i ditt konto.

## Kolumner i `SQL Report Builder`

Kolumnerna är inte beroende av uppdateringscykler, så du behöver inte längre vänta på en som ska slutföras innan du kan iterera i kolumnen. Om du gör ett misstag behöver du bara göra några tangenttryckningar för att korrigera det - du slipper vänta på att två uppdateringar ska sammanfogas innan du kan börja arbeta igen.

>[!IMPORTANT]
>
>Kolumnerna som du skapar med SQL-redigeraren sparas inte på Data warehouse. Du har alltid tillgång till frågan som innehåller kolumnen, men om du vill använda kolumnen i mer än en rapport måste du återskapa den i frågan för varje rapport. Detta innebär att kolumner som skapats med SQL-redigeraren inte kan användas i den traditionella `Report Builder`.

## Kolumner i Data warehouse Manager

Kolumnerna är beroende av uppdateringscykler, så en fullständig cykel måste slutföras innan de kan redigeras. De här kolumnerna sparas i Data warehouse Manager och kan användas i den traditionella `Report Builder` eller `SQL Report Builder`.
