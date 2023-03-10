---
title: Importera andra annonsutgiftsdata
description: Lär dig att importera offlinedata eller andra annonsutgifter till [!DNL MBI].
exl-id: 6f12a397-0927-4e87-95ff-3a55ccc9e14b
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '370'
ht-degree: 0%

---

# Importera andra annonsutgiftsdata

Genom att överföra dina annonsutgiftsdata kan ni mäta kampanjens avkastning genom att gifta er annonskostnad och kund `lifetime value (CLV)` av de användare ni köpt från era kampanjer.

## Överför annonsens kostnadsdata

Det första steget i att analysera annonsutgiftsdata är att hämta data. Eftersom de flesta annonsplattformar tillåter att du exporterar rapporter rekommenderar Adobe att du exporterar rådata från annonsplattformen och överför dem direkt till [!DNL MBI] utan någon manipulering. Du kan utföra åtgärder på data i Data warehouse, så du behöver inte fördubbla dina ansträngningar.

När du har exporterat annonsutgiftsdata använder du [`File Upload` funktion](../connecting-data/using-file-uploader.md) för att få in data i Data warehouse. Du kan överföra nya data till samma [!DNL MBI] bord över tid.

## Offlinekällor

Förutom era onlinekampanjer kan ni också ha annonser offline, som på radion eller en reklamtavla. Om du vill ta hänsyn till dessa fall kan du överföra ett kalkylblad med kostnadsdata manuellt till [!DNL MBI].

Tabellstrukturen nedan rekommenderas när du skapar en `.csv` fil för att registrera annonsutgiftsdata. En mallfil bifogas också längst ned i den här artikeln för att fungera som exempel. Rekommenderade kolumner är:

* `ID` - Detta är en unik identifierare för varje datarad som används av databasen som primärnyckel. Det här måste vara annorlunda för varje rad.
* `Date` - Detta är det datum då kampanjen kördes, i formatet åååå-mm-dd.
* `Amount` - Det här är det belopp som du spenderade på kampanjen.
* `campaign` - Det här är kampanjnamnet. Om du använder [!DNL Google Analytics] om du vill spåra dina andra annonsutgiftsdata, ska det matcha utm\_campaign-namnet.
* `source` - Det här är källnamnet. Om du använder [!DNL Google Analytics], detta ska matcha `utm_source` namn.
* `other` (Valfritt) - Du kan även inkludera ytterligare kolumner som hjälper dig att segmentera kampanjer och kostnader. Det kan också vara ett sätt att sammanfatta flera olika namn på UTM-kampanjer i en enda, sammanhängande kampanj för spårningsändamål. I stället för att konfigurera detta manuellt kan det vara bra att använda en V-Lookup till ett andra blad för att matcha varje Campaign-namn mot det andra namnet och rapportera det här dynamiskt.

## Relaterad

* [Anslut [!DNL AdWords] data](../integrations/google-adwords.md)
* [Öka avkastningen på annonskampanjer](../../analysis/roi-ad-camp.md)
