---
title: Sannolikhetsrapport för upprepade order
description: Lär dig mer och förstå rapporten om sannolikhet för upprepad order.
exl-id: 2c88b85a-7320-44ca-87a5-5b91250348ea
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---

# Sannolikhetsrapport för upprepade order

## När är `Incremental Event Probability` tillgängliga perspektiv?

The `incremental event probability` perspektiv är bara tillgängligt när filter använder dimensioner som är lika för alla order (till exempel användarens `gender`, användarens `age` eller användarens `source`).

Detta beror på att perspektivet bygger på en dimension som kallas `User's order number` för segmentering, som numrerar en användares inköp (t.ex. Johns första, andra och tredje order).

Om du har lagt till ett filter som använder en dimension som inte är lika för alla order (till exempel `Order's Region`), `User's order number` dimensionen skulle inte längre vara korrekt. Detta beror på att det inte tar hänsyn till specifika regioner när man numrerar en användares order (t.ex. John&#39;s 1st, 2nd, 3rd order är fortfarande desamma oavsett region).

## Förvandla en orderspecifik dimension till en användarspecifik dimension

I vissa fall kan du kanske ändra `order-specific` dimension till en `user-specific` dimension som ska läggas till som filter i `Repeat Order Probability` diagram. I dessa fall returnerar du attributet order för en användares första order eller senaste order (t.ex. användarens namn för första orderområde).

Om du vill skapa en sådan ny dimension [kontakta support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).

## Jämföra upprepningssannolikhet för order med olika attribut

Om du vill jämföra antalet upprepade köp för olika orderattribut (till exempel orderns `region`) rekommenderar Adobe att du skapar ett diagram som liknar `Users by lifetime number of orders`. Här visas hur många användare som har skapat 1, 2, 3,.. antal order under hela löptiden och lägg till ordernivåfiltret. (med andra ord, detta kan visa dig om användarna gör fler eller mindre upprepade inköp i en region eller en annan.)

Siffrorna som utgör ett sådant diagram kan sedan exporteras till excel för att beräkna sannolikhetsförhållandet för upprepade order. Att se sannolikheten för kunder som `(x)` order att skapa `(x+1)` order, enkelt` divide the number of people who've made at least (x+1) purchases by the number of people who have made at least (x)` inköp.

### Exempel:

| Kategori | Värde |
|---|---|
| Antal kunder som gjort ett köp under sin livstid | `90` |
| Antal kunder som gjort två inköp under sin livstid | `30` |
| Antal kunder som gjort tre inköp under sin livstid | `10` |
| Sannolikheten för upprepade order för kunder som har gjort ett köp under sin livstid för att göra ett andra inköp | `(30 + 10) / (30+10+90) = 30.77%` |
