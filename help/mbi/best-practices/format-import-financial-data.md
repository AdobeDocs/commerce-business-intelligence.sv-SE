---
title: Formatera och importera finansiella data
description: Lär dig formatera och importera ekonomiska data.
exl-id: cdbed262-7cf1-4fd6-ad5a-c44d26dffba7
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 0%

---

# Formatera och importera ekonomiska data

I det här avsnittet beskrivs det bästa sättet att importera ekonomiska data för analys i [!DNL Adobe Commerce Intelligence].

En tvådimensionell datatabell med flera flikar är ofta det format som används för finansiella data. När värden kategoriseras efter etiketter i både kolumner och rader kan den här typen av layout vara enkel att visa med mänskliga ögon och kalkylbladsverktyg, men den är inte anpassad för databaser.

![Korsformat som visar data i pivottabellayout](../../mbi/assets/crosstab.png)

Om du vill importera och analysera dessa data i [!DNL Commerce Intelligence] måste tabellen förenklas till en endimensionell lista. Vid förenkling kategoriseras varje datavärde av flera etiketter som alla finns på en rad, där varje rad är unik eller har en unik identifierare, till exempel en primärnyckelkolumn.

![Förenklat format som visar data i kolumnlayout](../../mbi/assets/flattened.png)

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
   ![Listan med pivottabellfält i Excel som visar dubbelklickningar för att expandera](../../mbi/assets/pivot-table-double-click.png)
1. Spara som en `CSV`-fil.

## Radbrytning

Datatabellen har konverterats till ett listformat och bevarar all ursprunglig information. Den kan nu [importeras till  [!DNL Commerce Intelligence]](../data-analyst/importing-data/connecting-data/using-file-uploader.md) för analys.
