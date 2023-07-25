---
title: Skillnader mellan SQL och Data warehouse Manager
description: Lär dig skillnaderna mellan SQL och Data warehouse Manager.
exl-id: 31dd7a04-5c03-4399-b67e-f51703eb9fea
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# Skillnader mellan [!DNL SQL] och [!DNL Data Warehouse Manager]

Det finns två viktiga skillnader mellan kolumner som skapas i [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) och de som skapats med [[!DNL Data Warehouse Manager]](../data-warehouse-mgr/creating-calculated-columns.md). Det ena är beroendet av uppdateringscykler och det andra är hur kolumner sparas i ditt konto.

## Kolumner i [!DNL SQL Report Builder]

Kolumnerna är inte beroende av uppdateringscykler, så du behöver inte längre vänta på en som ska slutföras innan du kan iterera i kolumnen. Om du gör ett misstag behöver du bara göra några tangenttryckningar för att korrigera det - du slipper vänta på att två uppdateringar ska sammanfogas innan du kan börja arbeta igen.

>[!IMPORTANT]
>
>Kolumnerna som du skapar med [!DNL SQL] redigeraren sparas inte i Data warehouse. Du har alltid tillgång till frågan som innehåller kolumnen, men om du vill använda kolumnen i mer än en rapport måste du återskapa den i frågan för varje rapport. Detta innebär att kolumner som skapats med [!DNL SQL] redigeraren kan inte användas i [!DNL Report Builder].

## Kolumner i Data warehouse Manager

Kolumner är beroende av uppdateringscykler, så en fullständig cykel måste slutföras innan de kan redigeras. De här kolumnerna sparas i Data warehouse Manager och kan användas i den traditionella [!DNL Report Builder] eller [!DNL SQL Report Builder].
