---
title: Använd filöverföring
description: Lär dig hur ni samlar alla era data i en enda Data warehouse.
exl-id: 28db0e78-0222-431d-bbb9-6ef133686603
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '1369'
ht-degree: 0%

---

# Använd filöverföring

>[!NOTE]
>
>Kräver [Administratörsbehörigheter](../../../administrator/user-management/user-management.md).

[!DNL Adobe Commerce Intelligence] är kraftfull inte bara på grund av visualiseringsfunktionerna, utan även för att den ger er möjlighet att samla alla data i en enda Data warehouse. Även data som finns utanför era databaser och integreringar kan föras in i [!DNL Commerce Intelligence] genom att använda filöverföringsverktyget i Data warehouse Manager.

Använd annonskampanjer som exempel. Om ni kör både online- och offlinekampanjer kan ni inte få hela bilden om ni bara analyserar data från en onlineintegrering. Om du överför ett kalkylblad med offlinekampanjdata kan du analysera båda uppsättningarna data och få en mer robust förståelse för kampanjresultaten.

## Begränsningar och krav {#require}

1. **Det enda format som stöds för filöverföringar är `CSV` eller`comma separated values`**. Om du arbetar i Excel kan du använda funktionen Spara som för att spara filen i `.csv` format.
1. **`CSV`måste använda`UTF-8 encoding`**. För det mesta är detta inte något problem. Om det här felet uppstår när du överför en fil, [Läs den här supportartikeln](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/resolving-utf-8-errors-for-csv-file-uploads.html).
1. **Filerna får inte vara större än 100 MB**. Om filen är större än så delar du upp tabellen i segment och sparar dem som enskilda filer. Du kan lägga till data när den första filen har lästs in.
1. **Alla tabeller måste ha en`primary key`**. Det måste finnas minst en kolumn i tabellen som kan användas som `primary key`eller en unik identifierare för varje rad i tabellen. Valfri kolumn som betecknas som `primary key` kan *aldrig* vara null. A `primary key` kan vara så enkelt som att lägga till en kolumn som ger ett nummer till varje rad, eller kan vara två kolumner sammanfogade för att skapa en kolumn med unika värden (till exempel `campaign name` och `date`).

   Om en kolumn (eller kolumner) har angetts som unik men det finns dubbletter importeras inte dubblettrader.

## Formatera data för överföring {#formatting}

Innan du kan överföra dina data till [!DNL Commerce Intelligence]kontrollerar du att den är formaterad enligt riktlinjerna i det här avsnittet.

### Rubrikrad {#header}

För att kolumnerna ska kunna märkas och importeras på rätt sätt måste du se till att den första raden i kalkylbladet är en rubrik som beskriver data i varje kolumn.

Kolumnnamn måste vara unika och får endast innehålla bokstäver, siffror, blanksteg och följande symboler: `$ % # /`. Om ett kolumnnamn innehåller kommatecken delas det i två kolumner när filen överförs. Adobe rekommenderar dessutom att det finns färre än 85 kolumner i filen för att optimera uppdateringshastigheten.

### Data med kommatecken {#commas}

Eftersom filer måste finnas i `CSV` om du använder kommatecken kan det uppstå problem när du överför data. `CSV` filer använder kommatecken för att ange nya värden, vilket innebär att en kolumn med ett namn som `Campaigns`, `August` läses som två kolumner (`Campaigns` och `August`) i stället för en, så att alla data flyttas över en rad. Adobe rekommenderar att man undviker kommatecken där det är möjligt. Du kan använda `Data Preview` för att se om dina data visas korrekt när en uppdatering har slutförts.

### Datum

Alla datauppsättningar som innehåller datum måste använda [standarddatumformat](https://dev.mysql.com/doc/refman/5.7/en/datetime.html) `YYYY-MM-DD HH:MM:SS` eller `MM/DD/YYYY`.

### Specialtecken

Vissa specialtecken accepteras inte. Rörsymbolen, till exempel `& # 1 2 4` tolkas som att en kolumn skapas och orsakar fel när en fil överförs.

### Decimaltal

Valutavärden ska ha datatypen `Decimal Number` markerat och de här kolumnerna avrundas automatiskt till två decimaler i Data warehouse. Om du inte vill avrunda decimaltal eller ha en större precision än så väljer du `Non-Currency Decimal Number` datatyp.

### Procenttal

Procenttal måste anges i decimaler. Till exempel:

| **Höger:** | **Fel:** |
|-----|-----|
| `.05` | `5%` |
| `.23` | `23` |

{style="table-layout:auto"}

### Värden med inledande och/eller avslutande nollor {#zeroes}

Vissa värden i filen - som ZIP-koder och ID:n - kan börja eller sluta med nollor. Om du vill vara säker på att nollorna bevaras och överförs på rätt sätt kan du ändra formateringstypen (till exempel [från tal till text](https://support.microsoft.com/en-us/office/format-numbers-as-text-583160db-936b-4e52-bdff-6f1863518ba4?ui=en-us&amp;rs=en-us&amp;ad=us)) eller framtvinga talformatering.

Använd `US ZIP codes` som ett exempel på hur du ändrar talformatering. I [!DNL Excel]markerar kolumnen som innehåller `ZIP codes` och [ändra talformatet](https://support.microsoft.com/en-us/office/display-numbers-as-postal-codes-61b55c9f-6fe3-4e54-96ca-9e85c38a5a1d?ui=en-us&amp;rs=en-us&amp;ad=us) till `ZIP code`. Du kan också välja ett eget nummerformat, och i dialogrutan `Type` window, enter `00000`. Tänk på att den här metoden kan orsaka problem om vissa koder är formaterade som `00000` och andra `00000-0000`.

The `Type` kan [formateras på olika sätt för att passa andra datatyper](https://support.microsoft.com/en-us/office/keeping-leading-zeros-and-large-numbers-1bf7b935-36e1-4985-842f-5dfa51f85fe7?correlationid=e1d4c2d3-cd5d-4a14-999d-437800274a90&amp;ui=en-us&amp;rs=en-us&amp;ad=us), t.ex. ID. Om en `ID` är nio siffror långa, till exempel `Type` kan `000000000` eller `000-000-000`. Detta skulle ändras `123456` till `000-123-456`.

För [!DNL Google Docs] och [!DNL Apple Numbers] resurser, se [Relaterad](#related) längst ned på sidan.

## Överför data {#uploading}

Nu när kalkylbladet är korrekt formaterat och [!DNL Commerce Intelligence]-vänligt, lägg till det i Data warehouse.

1. För att komma igång, gå till **[!UICONTROL Data** > **File Uploads]**.

1. Klicka på **[!UICONTROL Upload to New Table]** -fliken.

1. Klicka **[!UICONTROL Choose File]** och markera filen. Klicka **[!UICONTROL Open]** för att starta överföringen.

   När överföringen är klar visas en lista med kolumnerna [!DNL Commerce Intelligence] som finns i din fil visas.

1. Kontrollera att kolumnnamnen och datatyperna är korrekta. Kontrollera i synnerhet att datumkolumner läses som datum och inte nummer.

   >[!NOTE]
   >
   >The `datatype` är viktigt, så hoppa inte över det här steget!

1. Markera kolumnen (eller kolumnerna) som utgör `primary key` för tabellen genom att använda kryssrutorna under nyckelikonen.

1. Namnge tabellen.

1. Klicka **[!UICONTROL Save Table]**.

A *Klart!* visas högst upp på skärmen när tabellen har sparats.

Om du behöver en bild, titta på hela processen:

![](../../../assets/fileupload.gif)

Överförda tabeller visas under **Filöverföringar** i tabelllistan (i alternativen Alla tabeller och Synkroniserade tabeller) i Data warehouse Manager:

![](../../../assets/upload-tables.png)

## Uppdatera eller bifoga data till en befintlig tabell {#appending}

Har du några nya data att lägga till i en fil som du redan har överfört? Inga problem - du kan enkelt uppdatera och lägga till data i [!DNL Commerce Intelligence].

1. För att komma igång, gå till **[!UICONTROL Manage Data** > **File Uploads]**.

1. Klicka på **[!UICONTROL Edit/Upload `.csv`till befintliga tabeller]** -fliken.

1. Klicka på namnet på den tabell som du vill uppdatera eller lägga till i listrutan.

1. Använd listrutan för att välja alternativet för hantering av dubblettrader:

   | Alternativ | Beskrivning |
   |---|---|
   | `Overwrite old row with new row` | Befintliga data skrivs över med nya data om en rad har samma primärnyckel både i den befintliga tabellen och i den nya filen. Det här är den metod som ska användas för kolumner med värden som ändras över tid, till exempel en statuskolumn. Befintliga data skrivs över och uppdateras med nya data. Rader med primärnycklar som inte finns i den befintliga tabellen läggs till som nya rader. |
   | `Retain old row; discard new row` | Detta gör att nya data ignoreras om en rad har samma primärnyckel både i den befintliga tabellen och i den nya filen. |
   | `Purge all existing rows first and ignore duplicate keys within the file` | Då tas alla befintliga data bort och ersätts med nya data från filen. Använd bara det här alternativet om du inte behöver några data i den befintliga tabellen. |

1. Klicka **[!UICONTROL Choose File]** och markera filen.

1. Klicka **[!UICONTROL Open]** för att starta överföringen.

   När överföringen är klar [!DNL Commerce Intelligence] validerar filens datastruktur. A *Klart!* visas högst upp på skärmen när tabellen har sparats.

## Datatillgänglighet {#availability}

Precis som beräknade kolumner är data från filöverföringar tillgängliga när nästa uppdateringscykel har slutförts. Om en uppdatering pågick under filöverföringen är informationen inte tillgänglig förrän efter nästa uppdatering. När en uppdateringscykel är klar kan du navigera till `Data Preview` i Data warehouse för att säkerställa att filen som överförts är korrekt och att data visas som förväntat.

## Radbrytning {#wrapup}

Det här avsnittet handlar endast om grunderna för att importera data, men du kanske vill göra något mer avancerat. Läs mer i Relaterade artiklar om hur du formaterar och importerar ekonomiska data, e-handel, annonskostnader och andra typer av data.

Filöverföring är inte heller det enda sättet att få in data i [!DNL Commerce Intelligence]. The [API för dataimport](https://developer.adobe.com/commerce/services/reporting/import-api/) kan du överföra godtyckliga data till [!DNL Commerce Intelligence] data warehouse.

## Relaterad {#related}

* [Formatera och importera ekonomiska data](../../../best-practices/format-import-financial-data.md)
* [Importera offlinebaserade eller andra annonsutgiftsdata](../connecting-data/import-offline-ad-data.md)
* [Förväntat[!DNL Google ECommerce] data](../integrations/google-ecommerce-data.md)

## Resurser från tredje part

* [Guide för dataformatering av siffror](http://www.dummies.com/how-to/content/how-to-choose-a-number-format-in-your-numbers-spre.html)
* [[!DNL Google Docs] Handbok för dataformatering](https://support.google.com/docs/answer/56470?hl=en)
