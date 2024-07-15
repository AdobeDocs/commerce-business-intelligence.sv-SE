---
title: Ändra databasen så att den stöder inkrementell replikering
description: Lär dig hur du ändrar databasen så att den stöder inkrementell replikering.
exl-id: c9a38892-6096-4eb5-8a53-35b8b7b083dc
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---

# Stöd för inkrementell replikering

Om dina tabeller för närvarande inte tillåter inkrementell replikering, se följande rekommendationer för möjliga lösningar.

## Modifieringar för Modified At

Metoden `Modified At`, som är den mest idealiska replikeringsmetoden, använder en `datetime`-kolumn för att identifiera nya och/eller uppdaterade data. Kom ihåg att kolumnen `datetime` i tabeller som använder den här metoden måste indexeras och att den inte kan innehålla null-värden när som helst.

Om tabellen inte har någon `datetime`-kolumn kan du lägga till en `modified at`-indexkolumn. Null-värden tillåts inte i en `modified at`-kolumn. Kontrollera att kolumnen är ifylld för varje rad.

Du kan inte ta bort rader från tabellen om du vill vara säker på att metoden `Modified At` fungerar som den ska. Du bör i stället markera raden som ogiltig genom att lägga till en `deleted`-kolumn i tabellen. Den här kolumnen returnerar `1` om raden är ogiltig, i annat fall `0`. Du kan sedan använda den här kolumnen för att filtrera bort ogiltiga rader när du skapar mätvärden och rapporter.

## Modifieringar för enskild autoökning av primärnyckel

Om metoden `Modified At` inte kan aktiveras är primärnyckeln för enkel autoökning det näst bästa alternativet. Nya data identifieras i tabeller med den här metoden genom att söka efter primärnyckelvärden som är högre än det högsta värdet i Datan Warehouse.

Kom ihåg att tabeller som använder den här metoden är en kolumn med heltalsökning som automatiskt ökar primärnycklarna. Om du vill använda den här metoden i databasen gör du följande ändringar:

* Om primärnyckeln är antingen en sammansatt nyckel eller ett icke-heltal ändrar du primärnyckeln till ett heltal med automatisk ökning
* Om primärnyckeln är en enda heltalskolumn men nycklar kan tilldelas icke-sekventiellt, ändrar du primärnyckeln till automatisk ökning

## Radbrytning

Genom att göra mindre ändringar i tabellerna kan du dra nytta av de snabbare och effektivare inkrementella replikeringsmetoderna. Om detta inte är möjligt kan du ändå utföra andra åtgärder för att [minska uppdateringstiden](../best-practices/reduce-update-cycle-time.md) och [optimera databasen](../best-practices/opt-db-analysis.md).
