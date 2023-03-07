---
title: MongoDB-datamodellering
description: Lär dig hur du undviker datamönster som kan utgöra ett problem.
exl-id: 556c854b-5d7c-4f72-8ed7-5bc08d9ee5b9
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '128'
ht-degree: 0%

---

# [!DNL MongoDB] Datamodellering

När [!DNL MBI] pullin [!DNL MongoDB] data, översätts dessa data till en relationsmodell.

De dåliga nyheterna: Även om de flesta datamönster inte utgör något problem finns det några som, på grund av översättningen till en relationsmodell, [!DNL MBI] stöder inte.

Goda nyheter: Alla dessa mönster kan undvikas.

## Underkapslade arrayer {#subnested}

Om din samling ser ut som exemplet nedan [!DNL MBI] replikerar bara data i arrayen items. Data från underobjektarrayen hämtas inte.

```bash
    {
        _id: 0000000000000001
        items: [
            {
                _id: 0000000000000002
               subItems: [
                   {
                       _id: 0000000000000003
                      name: "Donut"
                      description: "glazed"
                   }
               ]
            }
        ]
    }
```

## Variabla objektnycklar {#varobjectkeys}

Samlingar som innehåller objekt med variabla objektnycklar replikeras inte i [!DNL MBI]. Till exempel:

```bash
    {
        _id: 0000000000000001
        friends: {
            0000000000000002: "Jimmy",
            0000000000000004: "Roger",
            0000000000000005: "Susan"
        },
    }
```

Det här inträffar vanligtvis när ett objekt används och en array är lämpligare. Nu kan du omarbeta ovanstående exempel:

```bash
    {
        _id: 0000000000000001
        friends: [
            { friend_id: 0000000000000002, name: "Jimmy" },
            { friend_id: 0000000000000004, name: "Roger" },
            { friend_id: 0000000000000005, name: "Susan"}
        ]
    }
```
