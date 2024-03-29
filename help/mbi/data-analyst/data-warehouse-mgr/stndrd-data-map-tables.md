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

Tänk dig att du är i `Report Builder` bygga en `Revenue by State` rapport. Allt går bra tills du försöker lägga till en `billing state` gruppera efter rapporten och du ser detta:

![](../../assets/Messy_State_Segments.png)

## Hur skulle det här kunna hända?

Tyvärr kan bristande standardisering ibland leda till röriga data och problem när rapporter skapas. I det här exemplet kanske det inte finns någon meny eller något standardiserat sätt för kunderna att ange sin faktureringsinformation. Detta leder till olika värden - `pa`, `PA`, `penna`, `pennsylvania`och `Pennsylvania` - allt för samma stat, vilket leder till vissa märkliga resultat i `Report Builder`.

Det kan finnas en teknisk resurs som kan hjälpa dig att rensa data eller infoga kolumner som du behöver direkt i databasen. Annars finns det en annan lösning - **mappningstabellen**. Med en mappningstabell kan du snabbt och enkelt rensa och standardisera alla data genom att mappa data till en enda utdatafil.

>[!NOTE]
>
>Du kan inte skapa en mappningstabell för konsoliderade tabeller utan hjälp från Adobe Support-teamet.

## Hur skapar jag det? {#how}

**Uppdatering av dataformatering:**

* Kontrollera att kalkylbladet har en rubrikrad.
* Undvik kommatecken! Det orsakar problem när du överför filen.
* Använd standarddatumformatet `(YYYY-MM-DD HH:MM:SS)` för datum.
* Procenttal måste anges i decimaler.
* Se till att inledande och avslutande nollor behålls korrekt.

Innan du går in rekommenderar Adobe att du [exportera råtabellsdata](../../tutorials/export-raw-data.md). Om du tittar på rådata först kan du utforska alla möjliga kombinationer av de data du behöver städa upp, vilket säkerställer att mappningstabellen täcker allt.

Om du vill skapa en mappningstabell måste du skapa ett kalkylblad med två kolumner som följer efter [formateringsregler för filöverföringar](../../data-analyst/importing-data/connecting-data/using-file-uploader.md).

I den första kolumnen anger du de värden som lagras i databasen med **endast ett värde i varje rad**. Till exempel: `pa` och `PA` kan inte finnas på samma rad - varje inmatning måste ha en egen rad. Nedan finns ett exempel.

I den andra kolumnen anger du vilka dessa värden är **bör**. Fortsätta med exemplet med faktureringsläge, om du vill `pa`, `PA`, `Pennsylvania`och `pennsylvania` att helt enkelt `PA`, du skulle skriva `PA` i den här kolumnen för varje indatavärde.

![](../../assets/Mapping_table_examples.jpg)

## Vad behöver jag göra i [!DNL Commerce Intelligence] för att använda den? {#use}

När du har skapat mappningstabellen måste du [ladda upp filen](../../data-analyst/importing-data/connecting-data/using-file-uploader.md) till [!DNL Commerce Intelligence] och [skapa en sammanfogad kolumn](../../data-analyst/data-warehouse-mgr/calc-column-types.md) som omplacerar det nya fältet i den önskade tabellen. Du kan göra detta när filen har synkroniserats med Datan Warehouse.

Det här exemplet flyttar kolumnen som du skapade på `mapping_state` tabell (`state_input`) till `customer_address` tabell som använder en kopplad kolumn. Detta gör att vi kan gruppera efter `state_input` i dina rapporter i stället för `state` kolumn.

Skapa `joined` navigerar du till den tabell som Data Warehouse Manager ska flytta fältet till. I det här exemplet är det `customer_address` tabell.

1. Klicka på **[!UICONTROL Create a Column]**.
1. Välj `Joined Column` från `Definition` nedrullningsbar meny.
1. Ge kolumnen ett namn som skiljer den från `state` -kolumnen i databasen. Namnge kolumnen `billing state (mapped)` så att du kan se vilken kolumn som ska användas vid segmentering i Report Builder.
1. Sökvägen som du måste koppla tabellerna finns inte, så du måste skapa en. Klicka **[!UICONTROL Create new path]**  i `Select a table and column` nedrullningsbar meny.

   Om du inte är säker på vad tabellrelationen är eller hur du definierar primärnycklarna och sekundärnycklarna korrekt, kan du checka ut [självstudiekurs](../../data-analyst/data-warehouse-mgr/create-paths-calc-columns.md) för lite hjälp.

   * På `Many` markerar du tabellen som du flyttar fältet till (igen, för vi är det `customer_address`) och `Foreign Key` kolumn, eller `state` -kolumn i exemplet.
   * På `One` sida väljer du `mapping` tabellen och `Primary key` kolumn. I så fall väljer du `state_input` kolumn från `mapping_state` tabell.
   * Här ser du hur banan ser ut:

     ![](../../assets/State_Mapping_Path.png)

1. När du är klar klickar du på **[!UICONTROL Save]** för att skapa banan.
1. Sökvägen kanske inte fylls i omedelbart efter att du har sparat - om det händer klickar du på `Path` och markera den bana du skapade.
1. Klicka **[!UICONTROL Save]** för att skapa kolumnen.

## Vad ska jag göra nu? {#wrapup}

När en uppdateringscykel är klar kan du använda den nya sammanfogade kolumnen för att segmentera data på rätt sätt i stället för den galna kolumnen i databasen. Titta på grupperingsalternativen nu - ingen mer stress:

![](../../assets/Clean_State_Segments.png)

Mappningstabeller är användbara när du vill rensa upp en del potentiellt klumpiga data i Datan Warehouse. Mappningstabeller kan dock även användas för andra coola användningsområden, som [replikera [!DNL Google Analytics channels] in [!DNL Commerce Intelligence]](../data-warehouse-mgr/rep-google-analytics-channels.md).

### Relaterad

* [Förstå och utvärdera tabellrelationer](../data-warehouse-mgr/table-relationships.md)
* [Skapa/ta bort banor för beräknade kolumner](../data-warehouse-mgr/create-paths-calc-columns.md)
