---
title: Beräknad kolumn för händelsenummer
description: Lär dig syftet med och användningsområdena för den beräknade kolumnen för händelsenummer.
exl-id: c234621e-2e68-4e63-8b0d-7034d1b5fe1f
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 0%

---

# Beräknad kolumn för händelsenummer

I det här avsnittet beskrivs syftet med och användningsområdena för `Event Number` beräknad kolumn tillgänglig i **[!DNL Manage Data > Data Warehouse]** sida. Nedan visas en förklaring av vad det gör, följt av ett exempel, och hur det går till att skapa det.

**Förklaring**

The `Event Number` kolumntyp: identifierar i vilken ordning händelser inträffade för en viss **händelseägare**, som `customer` eller `user`. Om du känner till SQL är den här kolumntypen identisk med `RANK` funktion. Den kan användas för att observera skillnader i beteende mellan förstagångshändelser, upprepningar eller nth-händelser i dina data.

Om det finns flera sorters noder innehåller den här kolumnen samma **rankning** för de kopplade händelserna och hoppar över efterföljande nummer. Om den till exempel rankade siffrorna 5,8,10,10,12, skulle rankningarna vara 1,2,3,3,5.

Det vanligaste användningsexemplet i den här kolumnen är att analysera förstagångsköpare och upprepa köpare. Första gången köpare identifieras genom att ett filter (till ett mätvärde eller en rapport) läggs till på `Customer's order number` = 1. `Customer's order number` är en kolumn av typen `Event Number`.

**Exempel**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Owner's event number`** |
|--- |--- |--- |--- |
| **1 | A | 2015-01-01 00:00:00 | 1 |
| **2 | B | 2015-01-01 00:30:00 | 1 |
| **3 | A | 2015-01-01 02:00:00 | 2 |
| **4 | A | 2015-01-02 13:00:00 | 3 |
| **5 | B | 2015-01-03 13:00:00 | 2 |

I ovanstående exempel är kolumnen `Owner's event number` är en `Event Number` kolumn. Den rangordnar ägarens händelser i den ordning de inträffade (baserat på `timestamp` kolumn).

Ta till exempel alla rader där `owner_id = A`. Den första raden i tabellen är den tidigaste tidsstämpeln för den här ägaren, följt av den tredje raden i tabellen, följt av den fjärde raden i tabellen.

**Mekanik**

Här följer några instruktioner om hur du skapar en `Event Number` kolumn:

1. Navigera till **[!UICONTROL Manage Data > Data Warehouse]** sida.
1. Navigera till tabellen som du vill skapa den här kolumnen för.
1. Klicka **[!UICONTROL Create a Column]** och väljer `EVENT_NUMBER (…)` kolumntyp: under `Same Table` -avsnitt.
1. Den första listrutan `Event Owner` anger den enhet för vilken rangordningen ska fastställas. Om `Customer's order number`, en kundidentifierare som `customer_id` eller `customer_email` skulle vara `Event Owner`.
1. Den andra listrutan `Event Rank` Anger den kolumn som tvingar den sekvens som bestämmer radens rangordning. Om `Customer's order number`, `created_at` tidsstämpeln är `Event Rank`.
1. Under `Options` kan du lägga till filter för att utesluta rader från övervägandet. De uteslutna raderna har en `NULL` värdet för den här kolumnen.
1. Ange ett namn för kolumnen och klicka på **[!UICONTROL Save]**.
1. Kolumnen kommer att vara tillgänglig att använda _omedelbart._
