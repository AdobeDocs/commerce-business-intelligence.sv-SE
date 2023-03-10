---
title: Formatera och importera finansiella data
description: Lär dig formatera och importera ekonomiska data.
exl-id: cdbed262-7cf1-4fd6-ad5a-c44d26dffba7
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---

# Formatera och importera ekonomiska data

I det här avsnittet beskrivs det bästa sättet att importera finansiella data för analys i [!DNL MBI].

En tvådimensionell datatabell med flera flikar är ofta det format som används för finansiella data. När värden kategoriseras efter etiketter i både kolumner och rader kan den här typen av layout vara enkel att visa med mänskliga ögon och kalkylbladsverktyg, men den är inte anpassad för databaser.

![](../../mbi/assets/crosstab.png)

Importera och analysera dessa data i [!DNL MBI]måste tabellen förenklas till en endimensionell lista. Vid förenkling kategoriseras varje datavärde av flera etiketter som alla finns på en rad, där varje rad är unik eller har en unik identifierare, till exempel en primärnyckelkolumn.

![](../../mbi/assets/flattened.png)

## Formatera Excel-filer för import

Så här förenklar du en tvådimensionell tabell med en pivottabell i Excel:

1. Öppna filen med den tvådimensionella datatabellen.
1. Öppna Pivottabellguiden. I Windows är genvägen `Alt-D`. I Mac OS anger du `Command-Option-P`.
1. Välj **[!UICONTROL Multiple consolidated ranges]** och klicka **[!UICONTROL Next]**.
1. Välj **[!UICONTROL I will create the page fields]** och klicka **[!UICONTROL Next]**.
1. Markera hela datauppsättningen i den tvådimensionella tabellen, inklusive etiketterna. Se till att `0` väljs för antalet önskade sidfält och klickar **[!UICONTROL Next]**.
1. Skapa pivottabellen i ett nytt blad och klicka på **[!UICONTROL Finish]**.
1. Avmarkera kolumn- och radfälten i fältlistan.
1. Dubbelklicka på det resulterande numeriska värdet för att visa de separerade källdata i ett nytt blad.
   ![](../../mbi/assets/pivot-table-double-click.png)
1. Spara som `CSV` -fil.

Så ja! Datatabellen har konverterats till ett listformat och bevarar all ursprunglig information. Den kan nu konverteras [importerat till [!DNL MBI]](../data-analyst/importing-data/connecting-data/using-file-uploader.md) för analys.
