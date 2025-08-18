---
title: Standardisera data med mappningstabeller
description: Lär dig hur du arbetar med att mappa tabeller.
exl-id: e452ff87-f298-43d5-acc3-af58e53bd0bc
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '743'
ht-degree: 0%

---

# Standardisera data med mappningstabeller

Tänk dig att du håller på att `Report Builder` skapa en `Revenue by State`-rapport. Allt går bra tills du försöker lägga till en `billing state`-gruppering i din rapport och du ser följande:

![](../../assets/Messy_State_Segments.png)

## Hur skulle det här kunna hända?

Tyvärr kan bristande standardisering ibland leda till röriga data och problem när rapporter skapas. I det här exemplet kanske det inte finns någon meny eller något standardiserat sätt för kunderna att ange sin faktureringsinformation. Detta leder till olika värden - `pa`, `PA`, `penna`, `pennsylvania` och `Pennsylvania` - för samma läge, vilket leder till vissa märkliga resultat i `Report Builder`.

Det kan finnas en teknisk resurs som kan hjälpa dig att rensa data eller infoga kolumner som du behöver direkt i databasen. Annars finns det en annan lösning - **mappningstabellen**. Med en mappningstabell kan du snabbt och enkelt rensa och standardisera alla data genom att mappa data till en enda utdatafil.

>[!NOTE]
>
>Du kan inte skapa en mappningstabell för konsoliderade tabeller utan hjälp från Adobe supportteam.

## Hur skapar jag det? {#how}

**Uppdaterare för dataformatering:**

* Kontrollera att kalkylbladet har en rubrikrad.
* Undvik kommatecken! Det orsakar problem när du överför filen.
* Använd standarddatumformatet `(YYYY-MM-DD HH:MM:SS)` för datum.
* Procenttal måste anges i decimaler.
* Se till att inledande och avslutande nollor behålls korrekt.

Innan du går in rekommenderar Adobe att du [exporterar råtabellsdata](../../tutorials/export-raw-data.md). Om du tittar på rådata först kan du utforska alla möjliga kombinationer av de data du behöver städa upp, vilket säkerställer att mappningstabellen täcker allt.

Om du vill skapa en mappningstabell måste du skapa ett kalkylblad med två kolumner som följer [formateringsreglerna för filöverföringar](../../data-analyst/importing-data/connecting-data/using-file-uploader.md).

I den första kolumnen anger du de värden som lagras i databasen med **endast ett värde i varje rad**. `pa` och `PA` kan till exempel inte finnas på samma rad. Varje inmatning måste ha en egen rad. Nedan finns ett exempel.

I den andra kolumnen anger du vilka dessa värden **ska vara**. Om du vill att `pa`, `PA`, `Pennsylvania` och `pennsylvania` helt enkelt ska vara `PA` fortsätter du med exemplet med faktureringsläget och anger `PA` i den här kolumnen för varje indatavärde.

![](../../assets/Mapping_table_examples.jpg)

## Vad behöver jag göra i [!DNL Commerce Intelligence] för att använda det? {#use}

När du har skapat mappningstabellen måste du [överföra filen](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) till [!DNL Commerce Intelligence] och [skapa en sammanfogad kolumn](../../data-analyst/data-warehouse-mgr/calc-column-types.md) som omplacerar det nya fältet i den önskade tabellen. Du kan göra detta när filen har synkroniserats med din Data Warehouse.

I det här exemplet flyttas kolumnen som du skapade i tabellen `mapping_state` (`state_input`) till tabellen `customer_address` med hjälp av en sammanfogad kolumn. Detta gör att vi kan gruppera efter den rena `state_input`-kolumnen i dina rapporter i stället för `state`-kolumnen.

Om du vill skapa kolumnen `joined` navigerar du till tabellen som fältet ska flyttas till i Data Warehouse Manager. I det här exemplet är det tabellen `customer_address`.

1. Klicka på **[!UICONTROL Create a Column]**.
1. Välj `Joined Column` i listrutan `Definition`.
1. Ge kolumnen ett namn som skiljer den från kolumnen `state` i databasen. Namnge kolumnen `billing state (mapped)` så att du kan se vilken kolumn som ska användas vid segmentering i Report Builder.
1. Sökvägen som du måste koppla tabellerna finns inte, så du måste skapa en. Klicka på **[!UICONTROL Create new path]** i listrutan `Select a table and column`.

   Om du är osäker på vad tabellrelationen är eller hur du definierar primärnycklar och sekundärnycklar på rätt sätt kan du få hjälp i [självstudiekursen](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md).

   * På sidan `Many` markerar du den tabell som du flyttar fältet till (återigen, för oss är det `customer_address`) och kolumnen `Foreign Key`, eller kolumnen `state`, i exemplet.
   * Markera tabellen `One` och kolumnen `mapping` på `Primary key`-sidan. I det här fallet väljer du kolumnen `state_input` i tabellen `mapping_state`.
   * Här ser du hur banan ser ut:

     ![](../../assets/State_Mapping_Path.png)

1. När du är klar klickar du på **[!UICONTROL Save]** för att skapa banan.
1. Sökvägen kanske inte fylls i omedelbart efter att du har sparat - om det händer klickar du i rutan `Path` och väljer den sökväg du skapade.
1. Klicka på **[!UICONTROL Save]** för att skapa kolumnen.

## Vad ska jag göra nu? {#wrapup}

När en uppdateringscykel är klar kan du använda den nya sammanfogade kolumnen för att segmentera data på rätt sätt i stället för den galna kolumnen i databasen. Titta på grupperingsalternativen nu - ingen mer stress:

![](../../assets/Clean_State_Segments.png)

Mappningstabeller är användbara när du vill rensa bort data i din Data Warehouse. Mappningstabeller kan dock även användas för andra coola användningsområden, som [replikering av  [!DNL Google Analytics channels] in [!DNL Commerce Intelligence]](../data-warehouse-mgr/rep-google-analytics-channels.md).

### Relaterad

* [Förstå och utvärdera tabellrelationer](../data-warehouse-mgr/table-relationships.md)
* [Skapa/ta bort banor för beräknade kolumner](../data-warehouse-mgr/create-paths-calc-columns.md)
