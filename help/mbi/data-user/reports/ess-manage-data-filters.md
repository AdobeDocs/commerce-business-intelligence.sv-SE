---
title: Skapa filteruppsättningar för mätvärden
description: Lär dig hur du skapar sparade filteruppsättningar och använder dem på mätvärdena.
exl-id: 6ef8b67c-bebd-45eb-bca7-95832ec34fc8
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '274'
ht-degree: 0%

---

# Skapa filteruppsättningar

Om du har flera mätvärden i [!DNL Commerce Intelligence] som måste filtreras på ett liknande sätt (t.ex. filtrera bort testorder) kan du skapa sparade filteruppsättningar och använda dem för mätvärdena. Detta sparar tid eftersom du inte behöver lägga till enskilda filter när du skapar eller redigerar ett mätresultat.

Se [utbildningsvideo](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-training-video-filter-sets.html) för mer information.

>[!NOTE]
>
>Kräver [Administratörsbehörigheter](../../administrator/user-management/user-management.md).

1. Klicka **[!DNL Manage Data** > **Filter Sets]** i sidlisten.

   ![](../../assets/create-filter-sets.png)

1. Klicka **[!UICONTROL Add Filter Set]** överst på sidan.

1. Markera tabellen som innehåller de mätvärden som du vill filtrera.

   Om du till exempel vill filtrera `Total number of orders` och bygger på `orders` markerar du tabellen.

1. Namnge `Filter Set`.

1. Lägg till alla relevanta filter.

   Om du t.ex. bara vill inkludera beställningar med statusen Fullständig i `Total number of orders` metrisk skulle du använda ett filter som utesluter alla order som inte har status = `complete`.

1. Kontrollera filterlogiken och att parenteser och operatorer är korrekt placerade: till exempel `\[A\] AND \[B\]; (\[A\] OR \[B\]) AND \[C\]`.

   Ett felaktigt filter orsakar ofta avvikelser i data mellan [!DNL Commerce Intelligence] rapporter och förväntade resultat.

1. Spara `Filter Set`.

När en filteruppsättning har sparats kan du använda den på alla mätvärden som använder samma tabell. Om du till exempel har skapat en `Filter Set` på `orders` tabell kan du använda den på *alla mått* som bygger på denna tabell, som `Revenue`.

>[!NOTE]
>
>`Filter Sets` kan även användas på beräknade kolumner i [!DNL Commerce Intelligence]. Du kan begära att en filteruppsättning används för en datamängd som skapats i [!DNL Commerce Intelligence] genom att kontakta supporten.

## Relaterad

* [Metodtips för segmentering och filtrering](../../best-practices/segment-filter.md)
