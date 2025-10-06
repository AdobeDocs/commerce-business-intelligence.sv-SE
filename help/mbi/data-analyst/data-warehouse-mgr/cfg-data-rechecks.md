---
title: Konfigurera datakontroller
description: Lär dig hur du konfigurerar datakolumner med ändringsbara värden.
exl-id: c31ef32e-ba5a-4902-b632-fbab551cc632
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 0%

---

# Konfigurera datakontroller

I en databastabell kan det finnas datakolumner med ändringsbara värden. I en `orders`-tabell kan det till exempel finnas en kolumn med namnet `status`. När en order skrivs till databasen från början kan statuskolumnen innehålla värdet _pending_. Ordningen replikeras i din [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) med det här `pending`-värdet.

Orderstatus kan ändras, men har inte alltid statusen `pending`. Till slut kan det bli `complete` eller `cancelled`. Om du vill vara säker på att din Data Warehouse synkroniserar den här ändringen måste du kontrollera om kolumnen innehåller nya värden.

Hur passar detta in med de [replikeringsmetoder](../data-warehouse-mgr/cfg-replication-methods.md) som diskuterades? Bearbetningen av omkontroller varierar beroende på den valda replikeringsmetoden. Replikeringsmetoden `Modified\_At` är det bästa alternativet för bearbetning av ändrade värden eftersom omkontroller inte behöver konfigureras. Metoderna `Auto-Incrementing Primary Key` och `Primary Key Batch Monitoring` kräver omkontroll av konfigurationen.

Om du använder någon av dessa metoder måste ändringsbara kolumner flaggas för omkontroll. Det finns tre sätt att göra detta:

1. En granskningsprocess som körs som en del av uppdateringen flaggar kolumner som ska kontrolleras igen.

   >[!NOTE]
   >
   >Revisorn förlitar sig på en urvalsprocess och de ändrade kolumnerna kanske inte fångas omedelbart.

1. Du kan ange dem själv genom att markera kryssrutan bredvid kolumnen i Data Warehouse-hanteraren, klicka på **[!UICONTROL Set Recheck Frequency]** och välja ett lämpligt tidsintervall för när du ska söka efter ändringar.

1. En medlem i [!DNL Adobe Commerce Intelligence] Data Warehouse-teamet kan markera kolumnerna manuellt för att kontrollera om i din Data Warehouse. Om du känner till ändringsbara kolumner kan du kontakta teamet och begära att omkontroller är inställda. Inkludera en lista med kolumner, tillsammans med frekvens, med din begäran.

## Kontrollera frekvenser {#frequency}

**Visste du det?**
Om du anger en omkontroll för en `primary key` -kolumn kontrolleras inte om kolumnen innehåller ändrade värden. Tabellen genomsöks efter raderade rader och alla borttagningar tas bort från Data Warehouse.

När en kolumn flaggas för omkontroll kan du även ange hur ofta en omkontroll ska ske. Om en viss kolumn inte ändras ofta kan du [optimera uppdateringscykeln](../../best-practices/reduce-update-cycle-time.md) genom att välja en mindre frekvent omkontroll.

Frekvensalternativen är:

* `always` - ny kontroll sker under varje uppdatering
* `daily` - omkontroll sker först efter midnatt-uppdatering för den angivna tidszonen
* `weekly` - ny kontroll sker efter klockan 20.00 fredag varje vecka för den deklarerade tidszonen
* `monthly` - ny kontroll sker efter klockan 20.00 fredag uppdatering var fjärde vecka för den deklarerade tidszonen
* `once` - förekommer endast i nästa uppdatering (en engångsuppdatering)

När uppdateringstiderna är korrelerade till hur mycket data som behöver synkroniseras rekommenderar Adobe att du väljer en `daily`, `weekly` eller `monthly` omkontroll i stället för varje uppdatering.

## Hantera frekvenser för omkontroll {#manage}

Kontrollfrekvenser kan hanteras i Data Warehouse genom att du klickar på ett tabellnamn och sedan kontrollerar enskilda kolumner. Synkroniseringsstatus och frekvens för omkontroll (**Ändringar?** kolumn) visas för varje kolumn i tabellen.

Om du vill ändra frekvensen för omkontroll klickar du i kryssrutan bredvid de kolumner du vill ändra. Klicka sedan på listrutan **[!UICONTROL Set Recheck Frequency]** och ange önskad frekvens.

![Data Warehouse Manager visar konfigurationsalternativ för omkontroll](../../assets/dwm-recheck.png)

Ibland kanske `Paused` visas i kolumnen `Changes?`. Det här värdet visas när tabellens [replikeringsmetod ](../../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) är inställd på `Paused`.

[!DNL Adobe] rekommenderar att du granskar dessa kolumner för att både optimera dina uppdateringar och se till att ändringsbara kolumner kontrolleras igen. Om frekvensen för omkontroll av en kolumn är hög med tanke på hur ofta data ändras, rekommenderar Adobe att du minskar den för att optimera uppdateringarna.

Kontakta oss med frågor eller fråga om aktuella replikeringsmetoder eller omkontroller.

**Relaterad:**

* [Minskar uppdateringstiderna](../../best-practices/reduce-update-cycle-time.md)
* [Optimera databasen för analys](../../best-practices/opt-db-analysis.md)
