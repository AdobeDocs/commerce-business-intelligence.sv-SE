---
title: Konfigurera datakontroller
description: Lär dig hur du konfigurerar datakolumner med ändringsbara värden.
exl-id: c31ef32e-ba5a-4902-b632-fbab551cc632
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---

# Konfigurera datakontroller

I en databastabell kan det finnas datakolumner med ändringsbara värden. I en `orders` tabellen kan innehålla en kolumn som kallas `status`. När en order skrivs till databasen från början kan statuskolumnen innehålla värdet _väntar_. Ordningen replikeras i [data warehouse](../data-warehouse-mgr/tour-dwm.md) med `pending` värde.

Orderstatus kan ändras även om de inte alltid finns i en `pending` status. Så småningom kan det bli `complete` eller `cancelled`. Om du vill vara säker på att Data warehouse synkroniserar den här ändringen måste du kontrollera om kolumnen innehåller nya värden.

Hur passar det ihop med [replikeringsmetoder](../data-warehouse-mgr/cfg-replication-methods.md) som diskuterades? Bearbetningen av omkontroller varierar beroende på den valda replikeringsmetoden. The `Modified\_At` replikeringsmetod är det bästa alternativet för bearbetning av ändrade värden eftersom omkontroller inte behöver konfigureras. The `Auto-Incrementing Primary Key` och `Primary Key Batch Monitoring` metoder kräver omkontroll av konfigurationen.

Om du använder någon av dessa metoder måste ändringsbara kolumner flaggas för omkontroll. Det finns tre sätt att göra detta:

1. En granskningsprocess som körs som en del av uppdateringen flaggar kolumner som ska kontrolleras igen.

   >[!NOTE]
   >
   >Revisorn förlitar sig på en urvalsprocess och de ändrade kolumnerna kanske inte fångas omedelbart.

1. Du kan ange dem själv genom att markera kryssrutan bredvid kolumnen i Data warehouse-hanteraren och klicka på **[!UICONTROL Set Recheck Frequency]** och välja ett lämpligt tidsintervall för när du ska söka efter ändringar.

1. En medlem i [!DNL Adobe Commerce Intelligence] data warehouse team kan markera kolumnerna manuellt för omkontroll i Data warehouse. Om du känner till ändringsbara kolumner kan du kontakta teamet och begära att omkontroller är inställda. Inkludera en lista med kolumner, tillsammans med frekvens, med din begäran.

## Kontrollera frekvenser {#frequency}

**Visste du det?**
Ställa in en omkontroll på en `primary key` kolumnen kontrollerar inte om kolumnen innehåller ändrade värden. Tabellen genomsöks efter raderade rader och alla borttagningar rensas från Data warehouse.

När en kolumn flaggas för omkontroll kan du även ange hur ofta en omkontroll ska ske. Om en viss kolumn inte ändras så ofta kan du välja en mindre vanlig omkontroll [optimera uppdateringscykeln](../../best-practices/reduce-update-cycle-time.md).

Frekvensalternativen är:

* `always` - omkontroll sker under varje uppdatering
* `daily` - omkontroll sker första post midnight-uppdateringen för den deklarerade tidszonen
* `weekly` - omkontroll sker efter klockan 20.00 på fredag varje vecka för den deklarerade tidszonen
* `monthly` - omkontroll sker efter klockan 20.00 på fredag var fjärde vecka för den deklarerade tidszonen
* `once` - inträffar endast i nästa uppdatering (en engångsuppdatering)

När uppdateringstiderna är korrelerade till hur mycket data som behöver synkroniseras rekommenderar Adobe att du väljer en `daily`, `weekly`, eller `monthly` kontrollera i stället för varje uppdatering.

## Hantera frekvenser för omkontroll {#manage}

Kontrollfrekvenser kan hanteras i Data warehouse genom att klicka på ett tabellnamn och sedan kontrollera enskilda kolumner. Synkroniseringsstatus och frekvens för omkontroll ( **Förändringar?** kolumn) visas för varje kolumn i tabellen.

Om du vill ändra frekvensen för omkontroll klickar du i kryssrutan bredvid de kolumner du vill ändra. Klicka sedan på **[!UICONTROL Set Recheck Frequency]** och ange önskad frekvens.

![](../../assets/dwm-recheck.png)

Ibland ser du `Paused` i `Changes?` kolumn. Det här värdet visas när tabellen [replikeringsmetod](../../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) är inställd på `Paused`.

[!DNL Adobe] rekommenderar att du granskar dessa kolumner för att både optimera uppdateringar och se till att ändringsbara kolumner kontrolleras igen. Om frekvensen för omkontroll av en kolumn är hög med tanke på hur ofta data ändras rekommenderar Adobe att du minskar den för att optimera uppdateringarna.

Kontakta oss med frågor eller fråga om aktuella replikeringsmetoder eller omkontroller.

**Relaterat:**

* [Minskar uppdateringstiderna](../../best-practices/reduce-update-cycle-time.md)
* [Optimera databasen för analys](../../best-practices/opt-db-analysis.md)
