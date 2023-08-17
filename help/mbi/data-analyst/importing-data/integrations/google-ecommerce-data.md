---
title: Förväntat[!DNL Google ECommerce]data
description: Lär dig vilka typer av data som delas med Google ECommerce.
exl-id: 8e5d8863-f003-4c38-95c5-660bcbff48da
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# Förväntat[!DNL Google ECommerce] data

Efter [!DNL Google ECommerce] kontot har anslutits till [!DNL Commerce Intelligence]kommer systemet att börja importera data till en tabell med namnet `ecommerce`. Det här registret registrerar en datarad för varje transaktion. Detta inkluderar följande datakolumner på ordningsnivå:

| Kolumnnamn | Beskrivning |
|-----|-----|
| `\_id` | Den här kolumnen är primärnyckeln. |
| `accountId` | Den här kolumnen innehåller det konto-ID som är kopplat till din [!DNL Google Analytics] e-handelskonto. |
| `profileName` | Den här kolumnen innehåller [!DNL Google Analytics] profilnamn. |
| `profileId` | Den här kolumnen innehåller [!DNL Google Analytics] profil-ID. |
| `socialNetwork` | Den här kolumnen innehåller namnet på det sociala nätverket (till exempel [!DNL Facebook], eller [!DNL YouTube]) |
| `campaign` | Den här kolumnen innehåller kampanjnamnet (till exempel [`utm\_campaign`](https://support.google.com/analytics/answer/1033867?hl=en)). |
| `medium` | Den här kolumnen innehåller medienamnet (till exempel [`utm\_medium`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `source` | Den här kolumnen innehåller källnamnet. (till exempel [`utm\_source`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `keyword` | Den här kolumnen innehåller nyckelordsbeskrivningen (till exempel [`utm\_term`](https://support.google.com/analytics/answer/1033867?hl=en)) |
| `transactionId` | Den här kolumnen innehåller order-ID:t. Detta används för att koppla hänvisningsdata till orderdata. |
| `updated\_at` | Den här kolumnen innehåller den senaste gången dataraden uppdaterades. |

{style="table-layout:auto"}
