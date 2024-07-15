---
title: Beräknad kolumn för händelsenummer
description: Lär dig syftet med och användningsområdena för den beräknade kolumnen för händelsenummer.
exl-id: c234621e-2e68-4e63-8b0d-7034d1b5fe1f
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 1%

---

# Beräknad kolumn för händelsenummer

I det här avsnittet beskrivs syftet med och användningsområdena för den beräknade kolumnen `Event Number` som är tillgänglig på sidan **[!DNL Manage Data > Data Warehouse]**. Nedan visas en förklaring av vad det gör, följt av ett exempel, och hur det fungerar.

**Förklaring**

Kolumntypen `Event Number` identifierar den sekvens i vilken händelser inträffade för en viss **händelseägare**, till exempel `customer` eller `user`. Om du känner till SQL är den här kolumntypen identisk med funktionen `RANK`. Den kan användas för att observera skillnader i beteende mellan förstagångshändelser, upprepningar eller nth-händelser i dina data.

Om det finns en slips innehåller den här kolumnen samma **rankning** för de kopplade händelserna och de efterföljande siffrorna hoppas över. Om den till exempel rankade siffrorna 5,8,10,10,12, skulle rankningarna vara 1,2,3,3,5.

Det vanligaste användningsexemplet i den här kolumnen är att analysera förstagångsköpare och upprepa köpare. Första gången köpare identifieras genom att ett filter (till ett mätvärde eller en rapport) läggs till på `Customer's order number` = 1. `Customer's order number` är en kolumn av typen `Event Number`.

**Exempel**

| **`event_id`** | **`owner_id`** | **`timestamp`** | **`Owner's event number`** |
|--- |--- |--- |--- |
| **1 | A | 2015-01-01 00:00:00 | 1 |
| **2 | B | 2015-01-01 00:30:00 | 1 |
| **3 | A | 2015-01-01 02:00:00 | 2 |
| **4 | A | 2015-01-02 13:00:00 | 3 |
| **5 | B | 2015-01-03 13:00:00 | 2 |

I ovanstående exempel är kolumnen `Owner's event number` en `Event Number`-kolumn. Ägarens händelser rangordnas i den ordning som de inträffade (baserat på kolumnen `timestamp`).

Ta till exempel alla rader där `owner_id = A` finns. Den första raden i tabellen är den tidigaste tidsstämpeln för den här ägaren, följt av den tredje raden i tabellen, följt av den fjärde raden i tabellen.

**Mekanik**

Här följer några instruktioner om hur du skapar en `Event Number`-kolumn:

1. Navigera till sidan **[!UICONTROL Manage Data > Data Warehouse]**.

1. Navigera till tabellen som du vill skapa den här kolumnen för.

1. Klicka på **[!UICONTROL Create a Column]** och välj kolumntypen `EVENT_NUMBER (…)` under avsnittet `Same Table`.

1. Den första listrutan `Event Owner` anger entiteten som rangordningen ska bestämmas för. Om en `Customer's order number` används är en kundidentifierare som `customer_id` eller `customer_email` `Event Owner`.

1. Den andra listrutan `Event Rank` anger kolumnen som tvingar sekvensen som bestämmer radens rangordning. Om `Customer's order number` används är tidsstämpeln `created_at` `Event Rank`.

1. I listrutan `Options` kan du lägga till filter för att utesluta rader från övervägandet. De uteslutna raderna har ett `NULL`-värde för den här kolumnen.

1. Ange ett namn för kolumnen och klicka på **[!UICONTROL Save]**.

1. Kolumnen kan användas _omedelbart._
