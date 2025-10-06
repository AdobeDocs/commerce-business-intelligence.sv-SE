---
title: Skapa filteruppsättningar för mätvärden
description: Lär dig hur du skapar sparade filteruppsättningar och använder dem på mätvärdena.
exl-id: 6ef8b67c-bebd-45eb-bca7-95832ec34fc8
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 0%

---

# Skapa filteruppsättningar

Om du har flera mätvärden i [!DNL Commerce Intelligence] som måste filtreras på ett liknande sätt (till exempel filtrera bort testorder) kan du skapa sparade filteruppsättningar och använda dem för mätvärdena. Detta sparar tid eftersom du inte behöver lägga till enskilda filter när du skapar eller redigerar ett mätresultat.

Mer information finns i [utbildningsvideon](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-filter-sets.html?lang=sv-SE).

>[!NOTE]
>
>Kräver [administratörsbehörighet](../../administrator/user-management/user-management.md).

1. Klicka på **[!DNL Manage Data** > **Filter Sets]** i sidlisten.

   ![Skapa gränssnitt för filteruppsättningar med alternativet Lägg till filteruppsättning](../../assets/create-filter-sets.png)

1. Klicka på **[!UICONTROL Add Filter Set]** överst på sidan.

1. Markera tabellen som innehåller de mätvärden som du vill filtrera.

   Om du till exempel vill filtrera `Total number of orders`-måttet och det är baserat på tabellen `orders` markerar du tabellen.

1. Namnge `Filter Set`.

1. Lägg till alla relevanta filter.

   Om du till exempel bara vill inkludera order med statusen slutförd i måttet `Total number of orders`, använder du ett filter som utesluter alla order som inte har statusen = `complete`.

1. Kontrollera filterlogiken och att parenteser och operatorer har placerats korrekt: till exempel `\[A\] AND \[B\]; (\[A\] OR \[B\]) AND \[C\]`.

   Ett felaktigt filter beror ofta på datameddelanden mellan [!DNL Commerce Intelligence]-rapporter och dina förväntade resultat.

1. Spara `Filter Set`.

När en filteruppsättning har sparats kan du använda den på alla mätvärden som använder samma tabell. Om du till exempel har skapat en `Filter Set` i tabellen `orders` kan du använda den på *alla mått* som bygger på tabellen, till exempel `Revenue`.

>[!NOTE]
>
>`Filter Sets` kan också användas för beräknade kolumner i [!DNL Commerce Intelligence]. Du kan begära att en filteruppsättning tillämpas på en datamängd som skapats i [!DNL Commerce Intelligence] via support.

## Relaterad

* [Bästa tillvägagångssätt för segmentering och filtrering](../../best-practices/segment-filter.md)
