---
title: Skapa Google Analytics-diagram
description: Lär dig hur du skapar diagram utifrån dina Google Analytics-data.
exl-id: ee80fd0d-e3b1-4331-853d-3c2c11931d3f
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 0%

---

# Skapa [!DNL Google Analytics] diagram

(med syntaxhjälp för regex)

När du har anslutit [[!DNL Google Analytics] konto](../../data-analyst/importing-data/integrations/google-analytics.md)kan du skapa diagram med [!DNL Google Analytics] data.

## Skapa [!DNL Google Analytics] Diagram

1. Klicka på **[!UICONTROL Add Chart** > **Create New Chart]**.

1. När du väljer ett mått i `Chart Builder`, bläddra till listans nedre del för att hitta ett avsnitt som innehåller [!DNL Google Analytics] Profiler. En andra metrisk listruta visas. Här kan du välja det mätvärde som du vill analysera.

1. När du har valt måttet kan du fortsätta med det här diagrammet som vilket annat diagram som helst genom att välja `time period`, `interval`och data `perspectives` som du vill se.

1. Den största skillnaden här är att `√` använder reguljära uttryck för filter. Ett reguljärt uttryck (regex för short) är en specialtextsträng som beskriver ett sökmönster. Se exempel på regex-syntax i [[!DNL Google] guide om reguljära uttryck för analyser](https://support.google.com/analytics/answer/1034324?hl=en).

>[!NOTE]
>
>De enda specialtecken som måste föregås av ett \-tecken är Metatecken nedan:

| | | | | |
|-----|-----|-----|-----|-----|
| `^` | `[` | `]` | `$` | `(` |
| `)` | `.` | `{` | `}` | `*` |
| `+` | `?` | `\` | `\` | `-` |

{style="table-layout:auto"}
