---
title: Använd filöverföring
description: Lär dig hur ni samlar alla era data i en enda Data Warehouse.
exl-id: 28db0e78-0222-431d-bbb9-6ef133686603
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1279'
ht-degree: 0%

---

# Använd filöverföring

>[!NOTE]
>
>Kräver [administratörsbehörighet](../../../administrator/user-management/user-management.md).

[!DNL Adobe Commerce Intelligence] är kraftfull inte bara på grund av dess visualiseringsfunktioner, utan även för att den ger dig möjlighet att samla alla dina data i en enda Data Warehouse. Även data som finns utanför dina databaser och integreringar kan hämtas till [!DNL Commerce Intelligence] med hjälp av filöverföringsverktyget i Data Warehouse Manager.

Använd annonskampanjer som exempel. Om ni kör både online- och offlinekampanjer kan ni inte få hela bilden om ni bara analyserar data från en onlineintegrering. Om du överför ett kalkylblad med offlinekampanjdata kan du analysera båda uppsättningarna data och få en mer robust förståelse för kampanjresultaten.

## Begränsningar och krav {#require}

1. **Det enda format som stöds för filöverföringar är `CSV` eller`comma separated values`**. Om du arbetar i Excel kan du använda funktionen Spara som för att spara filen i formatet `.csv`.
1. **`CSV`filer måste använda`UTF-8 encoding`**. För det mesta är detta inte något problem. Om det här felet inträffar när du överför en fil [läser du den här supportartikeln](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/resolving-utf-8-errors-for-csv-file-uploads.html?lang=sv-SE).
1. **Filerna får inte vara större än 100 MB**. Om filen är större än så delar du upp tabellen i segment och sparar dem som enskilda filer. Du kan lägga till data när den första filen har lästs in.
1. **Alla tabeller måste ha en`primary key`**. Det måste finnas minst en kolumn i tabellen som kan användas som `primary key`, eller en unik identifierare för varje rad i tabellen. Alla kolumner som har angetts som `primary key` kan *aldrig* vara null. En `primary key` kan vara så enkel som att lägga till en kolumn som ger ett nummer till varje rad, eller så kan två kolumner sammanfogas för att skapa en kolumn med unika värden (till exempel `campaign name` och `date`).

   Om en kolumn (eller kolumner) har angetts som unik men det finns dubbletter importeras inte dubblettrader.

## Formatera data för överföring {#formatting}

Innan du kan överföra dina data till [!DNL Commerce Intelligence] måste du kontrollera att de är formaterade enligt riktlinjerna i det här avsnittet.

### Rubrikrad {#header}

För att kolumnerna ska kunna märkas och importeras på rätt sätt måste du se till att den första raden i kalkylbladet är en rubrik som beskriver data i varje kolumn.

Kolumnnamn måste vara unika och får bara innehålla bokstäver, siffror, blanksteg och följande symboler: `$ % # /`. Om ett kolumnnamn innehåller kommatecken delas det i två kolumner när filen överförs. Adobe rekommenderar dessutom att det finns färre än 85 kolumner i filen för att optimera uppdateringshastigheten.

### Data med komma {#commas}

Eftersom filerna måste vara i formatet `CSV` kan användning av kommatecken orsaka problem vid överföring av data. `CSV`-filer använder kommatecken för att ange nya värden, och därför läses en kolumn med namnet `Campaigns`, `August` som två kolumner (`Campaigns` och `August`) i stället för en, så att alla data flyttas över en rad. Adobe rekommenderar att du undviker kommatecken när det är möjligt. Du kan använda `Data Preview` för att se om dina data visas korrekt när en uppdatering har slutförts.

### Datum

Alla datauppsättningar som innehåller datum måste använda standarddatumformatet [&#128279;](https://dev.mysql.com/doc/refman/5.7/en/datetime.html) `YYYY-MM-DD HH:MM:SS` eller `MM/DD/YYYY`.

### Specialtecken

Vissa specialtecken accepteras inte. Piplinjen `& # 1 2 4` tolkas som att en kolumn skapas och orsakar fel när en fil överförs.

### Decimaltal

Valutavärden ska ha datatypen `Decimal Number` markerad och kolumnerna avrundas automatiskt till två decimaler i din Data Warehouse. Om du inte vill avrunda dina decimaltal eller ha en större precision än detta bör du välja datatypen `Non-Currency Decimal Number`.

### Procenttal

Procenttal måste anges i decimaler. Exempel:

| **Höger:** | **Fel:** |
|-----|-----|
| `.05` | `5%` |
| `.23` | `23` |

{style="table-layout:auto"}

### Värden med inledande och/eller avslutande nollor {#zeroes}

Vissa värden i filen - som ZIP-koder och ID:n - kan börja eller sluta med nollor. Om du vill vara säker på att nollorna behålls och överförs på rätt sätt kan du ändra formateringstypen (till exempel [ från tal till text](https://support.microsoft.com/en-us/office/format-numbers-as-text-583160db-936b-4e52-bdff-6f1863518ba4?ui=en-us&rs=en-us&ad=us)) eller framtvinga nummerformatering.

Använd `US ZIP codes` som exempel på hur du ändrar talformatering. I [!DNL Excel] markerar du kolumnen som innehåller `ZIP codes` och [ändrar talformatet ](https://support.microsoft.com/en-us/office/display-numbers-as-postal-codes-61b55c9f-6fe3-4e54-96ca-9e85c38a5a1d?ui=en-us&rs=en-us&ad=us) till `ZIP code`. Du kan också välja ett eget nummerformat och ange `Type` i fönstret `00000`. Tänk på att den här metoden kan orsaka problem om vissa koder är formaterade som `00000` och andra är `00000-0000`.

`Type` kan [formateras på olika sätt för att passa andra datatyper](https://support.microsoft.com/en-us/office/keeping-leading-zeros-and-large-numbers-1bf7b935-36e1-4985-842f-5dfa51f85fe7?correlationid=e1d4c2d3-cd5d-4a14-999d-437800274a90&ui=en-us&rs=en-us&ad=us), t.ex. ID:n. Om en `ID` är nio siffror lång, till exempel, kan `Type` vara `000000000` eller `000-000-000`. Detta skulle ändra `123456` till `000-123-456`.

För [!DNL Google Docs]- och [!DNL Apple Numbers]-resurser, se listan [Relaterade](#related) längst ned på den här sidan.

## Överför data {#uploading}

Nu när kalkylbladet är korrekt formaterat och [!DNL Commerce Intelligence]-anpassat lägger du till det i din Data Warehouse.

1. Gå till **[!UICONTROL Data** > **File Uploads]** om du vill komma igång.

1. Klicka på fliken **[!UICONTROL Upload to New Table]**.

1. Klicka på **[!UICONTROL Choose File]** och markera filen. Klicka på **[!UICONTROL Open]** för att starta överföringen.

   När överföringen är klar visas en lista med kolumnerna [!DNL Commerce Intelligence] som hittades i filen.

1. Kontrollera att kolumnnamnen och datatyperna är korrekta. Kontrollera i synnerhet att datumkolumner läses som datum och inte nummer.

   >[!NOTE]
   >
   >`datatype` är viktigt, så hoppa inte över det här steget!

1. Markera kolumnen (eller kolumnerna) som utgör `primary key` för tabellen med hjälp av kryssrutorna under nyckelikonen.

1. Namnge tabellen.

1. Klicka på **[!UICONTROL Save Table]**.

*Klart!*-meddelandet visas högst upp på skärmen när tabellen har sparats.

Om du behöver en bild, titta på hela processen:

![](../../../assets/fileupload.gif)

Överförda tabeller visas under avsnittet **Filöverföringar** i tabelllistan (i alternativen Alla tabeller och Synkroniserade tabeller) i Data Warehouse Manager:

![](../../../assets/upload-tables.png)

## Uppdatera eller bifoga data till en befintlig tabell {#appending}

Har du några nya data att lägga till i en fil som du redan har överfört? Inga problem - du kan enkelt uppdatera och lägga till data i [!DNL Commerce Intelligence].

1. Gå till **[!UICONTROL Manage Data** > **File Uploads]** om du vill komma igång.

1. Klicka på fliken **[!UICONTROL Edit/Upload `.csv`till befintliga tabeller]**.

1. Klicka på namnet på den tabell som du vill uppdatera eller lägga till i listrutan.

1. Använd listrutan för att välja alternativet för hantering av dubblettrader:

   | Alternativ | Beskrivning |
   |---|---|
   | `Overwrite old row with new row` | Befintliga data skrivs över med nya data om en rad har samma primärnyckel både i den befintliga tabellen och i den nya filen. Det här är den metod som ska användas för kolumner med värden som ändras över tid, till exempel en statuskolumn. Befintliga data skrivs över och uppdateras med nya data. Rader med primärnycklar som inte finns i den befintliga tabellen läggs till som nya rader. |
   | `Retain old row; discard new row` | Detta gör att nya data ignoreras om en rad har samma primärnyckel både i den befintliga tabellen och i den nya filen. |
   | `Purge all existing rows first and ignore duplicate keys within the file` | Då tas alla befintliga data bort och ersätts med nya data från filen. Använd bara det här alternativet om du inte behöver några data i den befintliga tabellen. |

1. Klicka på **[!UICONTROL Choose File]** och markera filen.

1. Klicka på **[!UICONTROL Open]** för att starta överföringen.

   När överföringen är klar validerar [!DNL Commerce Intelligence] filens datastruktur. *Klart!*-meddelandet visas högst upp på skärmen när tabellen har sparats.

## Tillgänglighet {#availability}

Precis som beräknade kolumner är data från filöverföringar tillgängliga när nästa uppdateringscykel har slutförts. Om en uppdatering pågick under filöverföringen är informationen inte tillgänglig förrän efter nästa uppdatering. När en uppdateringscykel har slutförts kan du navigera till fliken `Data Preview` i Data Warehouse för att kontrollera att filen som har överförts är korrekt och att data visas som förväntat.

## Radbrytning {#wrapup}

Det här avsnittet handlar endast om grunderna för att importera data, men du kanske vill göra något mer avancerat. Läs mer i Relaterade artiklar om hur du formaterar och importerar ekonomiska data, e-handel, annonskostnader och andra typer av data.

Dessutom är filöverföring inte det enda sättet att hämta data till [!DNL Commerce Intelligence]. Med funktionerna för [API:t för dataimport](https://developer.adobe.com/commerce/services/reporting/import-api/) kan du skicka godtyckliga data till din [!DNL Commerce Intelligence] Data Warehouse.

## Relaterad {#related}

* [Formatera och importera ekonomiska data](../../../best-practices/format-import-financial-data.md)
* [Importera offlinebaserade eller andra annonsutgiftsdata](../connecting-data/import-offline-ad-data.md)
* [[!DNL Google ECommerce] data förväntades](../integrations/google-ecommerce-data.md)

## Resurser från tredje part

* [Riktlinje för dataformatering för siffror](http://www.dummies.com/how-to/content/how-to-choose-a-number-format-in-your-numbers-spre.html)
* [[!DNL Google Docs] Handbok för dataformatering](https://support.google.com/docs/answer/56470?hl=en)
