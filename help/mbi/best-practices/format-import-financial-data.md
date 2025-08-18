---
title: Formatera och importera finansiella data
description: Lär dig formatera och importera ekonomiska data.
exl-id: cdbed262-7cf1-4fd6-ad5a-c44d26dffba7
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 0%

---

# Formatera och importera ekonomiska data

I det här avsnittet beskrivs det bästa sättet att importera ekonomiska data för analys i [!DNL Adobe Commerce Intelligence].

En tvådimensionell datatabell med flera flikar är ofta det format som används för finansiella data. När värden kategoriseras efter etiketter i både kolumner och rader kan den här typen av layout vara enkel att visa med mänskliga ögon och kalkylbladsverktyg, men den är inte anpassad för databaser.

![](../../mbi/assets/crosstab.png)

Om du vill importera och analysera dessa data i [!DNL Commerce Intelligence] måste tabellen förenklas till en endimensionell lista. Vid förenkling kategoriseras varje datavärde av flera etiketter som alla finns på en rad, där varje rad är unik eller har en unik identifierare, till exempel en primärnyckelkolumn.

![](../../mbi/assets/flattened.png)

## Formatera Excel-filer för import

Så här förenklar du en tvådimensionell tabell med en pivottabell på [!DNL Excel]:

1. Öppna filen med den tvådimensionella datatabellen.
1. Öppna Pivottabellguiden. I [!DNL Windows] är genvägen `Alt-D`. Ange [!DNL Mac OS] i `Command-Option-P`.
1. Markera **[!UICONTROL Multiple consolidated ranges]** och klicka på **[!UICONTROL Next]**.
1. Markera **[!UICONTROL I will create the page fields]** och klicka på **[!UICONTROL Next]**.
1. Markera hela datauppsättningen i den tvådimensionella tabellen, inklusive etiketterna. Kontrollera att `0` har valts för antalet sidfält och klicka på **[!UICONTROL Next]**.
1. Skapa pivottabellen i ett nytt blad och klicka på **[!UICONTROL Finish]**.
1. Avmarkera kolumn- och radfälten i fältlistan.
1. Dubbelklicka på det resulterande numeriska värdet för att visa de separerade källdata i ett nytt blad.
   ![](../../mbi/assets/pivot-table-double-click.png)
1. Spara som en `CSV`-fil.

## Radbrytning

Datatabellen har konverterats till ett listformat och bevarar all ursprunglig information. Den kan nu [importeras till  [!DNL Commerce Intelligence]](../data-analyst/importing-data/connecting-data/using-file-uploader.md) för analys.
