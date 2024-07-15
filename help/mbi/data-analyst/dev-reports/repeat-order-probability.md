---
title: Sannolikhetsrapport för upprepad order
description: Lär dig mer och förstå rapporten om sannolikhet för upprepad order.
exl-id: 2c88b85a-7320-44ca-87a5-5b91250348ea
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 0%

---

# Sannolikhetsrapport för upprepad order

## När är perspektivet `Incremental Event Probability` tillgängligt?

Perspektivet `incremental event probability` är bara tillgängligt när filter använder dimensioner som är lika för alla order (till exempel användarens `gender`, användarens `age` eller användarens `source`).

Detta beror på att det här perspektivet bygger på en dimension som kallas `User's order number` för segmentering, som numrerar användarens inköp (till exempel Johns första, andra och tredje order).

Om du lade till ett filter som använder en dimension som inte är lika för alla order (till exempel `Order's Region`), skulle dimensionen `User's order number` inte längre vara exakt. Detta beror på att det inte tar hänsyn till specifika regioner när man numrerar en användares order (t.ex. John&#39;s 1st, 2nd, 3rd order är fortfarande desamma oavsett region).

## Förvandla en orderspecifik dimension till en användarspecifik dimension

I vissa fall kan du omvandla en `order-specific`-dimension till en `user-specific`-dimension som du kan lägga till som filter i `Repeat Order Probability`-diagrammet. I dessa fall returnerar du attributet order för en användares första order eller senaste order (t.ex. användarens namn för första orderområde).

[Kontakta support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) om du vill skapa en sådan ny dimension.

## Jämföra upprepningssannolikhet för order med olika attribut

Om du vill jämföra antalet upprepade köp för olika orderattribut (till exempel orderns `region`) rekommenderar Adobe att du skapar ett diagram som liknar `Users by lifetime number of orders`. Här visas antalet användare som har gjort 1, 2, 3,.. antal order under livstid och lagt till ordernivåfiltret. (med andra ord, detta kan visa dig om användarna gör fler eller mindre upprepade inköp i en region eller en annan.)

Siffrorna som utgör ett sådant diagram kan sedan exporteras till excel för att beräkna sannolikhetsförhållandet för upprepade order. Om du vill se sannolikheten för att kunder som har gjort `(x)` beställningar gör `(x+1)` beställningar behöver du bara ` divide the number of people who've made at least (x+1) purchases by the number of people who have made at least (x)` inköp.

### Exempel:

| Kategori | Värde |
|---|---|
| Antal kunder som gjort ett köp under sin livstid | `90` |
| Antal kunder som gjort två inköp under sin livstid | `30` |
| Antal kunder som gjort tre inköp under sin livstid | `10` |
| Sannolikheten för upprepade order för kunder som har gjort ett köp under sin livstid för att göra ett andra inköp | `(30 + 10) / (30+10+90) = 30.77%` |
