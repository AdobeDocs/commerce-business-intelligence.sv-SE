---
title: Ändra databasen så att den stöder inkrementell replikering
description: Lär dig hur du ändrar databasen så att den stöder inkrementell replikering.
exl-id: c9a38892-6096-4eb5-8a53-35b8b7b083dc
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---

# Stöd för inkrementell replikering

Om dina tabeller för närvarande inte tillåter inkrementell replikering, se följande rekommendationer för möjliga lösningar.

## Modifieringar för Modified At

The `Modified At` som är den mest idealiska replikeringsmetoden använder en `datetime` för att identifiera nya och/eller uppdaterade data. Kom ihåg att `datetime` -kolumnen i tabeller som använder den här metoden måste indexeras och får inte innehålla null-värden när som helst.

Om tabellen inte har en `datetime` kolumn kan du lägga till ett index `modified at` kolumn. Null-värden tillåts inte i en `modified at` kolumn. Kontrollera att kolumnen är ifylld för varje rad.

För att säkerställa `Modified At` -metoden fungerar som den ska, du kan inte ta bort rader från tabellen. Du bör i stället markera raden som ogiltig genom att lägga till en `deleted` kolumn till tabellen. Den här kolumnen returnerar en `1` om raden är ogiltig och `0` i annat fall. Du kan sedan använda den här kolumnen för att filtrera bort ogiltiga rader när du skapar mätvärden och rapporter.

## Modifieringar för enskild autoökning av primärnyckel

Om `Modified At` kan inte aktiveras, då är primärnyckeln för enkel autoökning nästa bästa alternativ. Nya data identifieras i tabeller med den här metoden genom att söka efter primärnyckelvärden som är högre än det högsta värdet i Data warehouse.

Kom ihåg att tabeller som använder den här metoden är en kolumn med heltalsökning som automatiskt ökar primärnycklarna. Om du vill använda den här metoden i databasen gör du följande ändringar:

* Om primärnyckeln är antingen en sammansatt nyckel eller ett icke-heltal ändrar du primärnyckeln till ett heltal med automatisk ökning
* Om primärnyckeln är en enda heltalskolumn men nycklar kan tilldelas icke-sekventiellt, ändrar du primärnyckeln till automatisk ökning

## Radbrytning

Genom att göra mindre ändringar i tabellerna kan du dra nytta av de snabbare och effektivare inkrementella replikeringsmetoderna. Om detta inte är möjligt kan du dock utföra andra åtgärder för att [minska uppdateringstiden](../best-practices/reduce-update-cycle-time.md) och [optimera databasen](../best-practices/opt-db-analysis.md).
