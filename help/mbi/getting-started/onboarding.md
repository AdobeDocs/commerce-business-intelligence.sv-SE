---
title: Onboarding Adobe Commerce Intelligence
description: Läs mer om hur du kommer igång med Adobe Commerce Intelligence.
exl-id: e0cce957-af2c-4514-9afd-c9aaa651a4f0
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---

# Onboarding [!DNL Adobe Commerce Intelligence]

Frågor om introduktion relaterade till `store` och `database` inställningarna ser till att du ställer in rapporteringen på rätt sätt. Med dessa svar levererar Adobe rapporter som är skräddarsydda efter hur er butik ser ut.

## Lagringsinställningar

- *Tar din butik emot gästutcheckning?* - Välj **ja** om du tillåter kunderna att göra ett köp från din butik utan att registrera ett konto.

- `Timezone` - Välj `timezone` som du vill se dina rapporter i.

- `Currency` - Välj `currency` som din butik är verksam i.

- `Your week starts on...` - Välj den veckodag som du vill ska vara veckostart i dina rapporter.

- *Vilken version av Commerce använder du?* - Välj `currency` som din butik är verksam i.

- *Är din butik bosatt i EU?* - Om du svarar `Yes` På denna fråga är Adobe värd för er Data Warehouse och alla era uppgifter i EU, i enlighet med GDPR.

## Databasinställningar

- `Database name` - Vad är *namnet på [!DNL MySQL] databas* var finns era transaktionsdata i Commerce?

- `Table prefix (optional)` - Föreskrivs tabellerna i din Commerce-databas av något (till exempel `store_`)? Detta är vanligtvis inte fallet, men det är en anpassning som kan göras.
