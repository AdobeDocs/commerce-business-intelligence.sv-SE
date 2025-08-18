---
title: Onboarding Adobe Commerce Intelligence
description: Läs mer om hur du registrerar Adobe Commerce Intelligence.
exl-id: e0cce957-af2c-4514-9afd-c9aaa651a4f0
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---

# Onboarding [!DNL Adobe Commerce Intelligence]

Startfrågorna som rör inställningarna för `store` och `database` säkerställer att du har konfigurerat din rapportering korrekt. Med dessa svar levererar Adobe rapporter som är skräddarsydda efter hur er butik ser ut.

## Lagringsinställningar

- *Accepterar din butik gästutcheckning?* - Välj **yes** om du tillåter kunderna att göra ett köp från din butik utan att registrera ett konto.

- `Timezone` - Välj den `timezone` som du vill se dina rapporter i.

- `Currency` - Välj den `currency` som din butik arbetar i.

- `Your week starts on...` - Välj den dag i veckan som du vill ska vara veckostart i dina rapporter.

- *Vilken version av Commerce använder du?* - Välj den `currency` som din butik arbetar i.

- *Är din butik baserad i EU?* - Om du svarar `Yes` på den här frågan är Adobe värd för din Data Warehouse och alla dina data i EU, i enlighet med GDPR.

## Databasinställningar

- `Database name` - Vad är *namnet på [!DNL MySQL]-databasen* där dina transaktionsdata från Commerce finns?

- `Table prefix (optional)` - Är tabellerna i din Commerce-databas prepended (till exempel `store_`)? Detta är vanligtvis inte fallet, men det är en anpassning som kan göras.
