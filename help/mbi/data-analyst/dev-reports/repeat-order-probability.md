---
title: Sannolikhetsrapport för upprepade order
description: Lär dig mer och förstå rapporten om sannolikhet för upprepad order.
exl-id: 2c88b85a-7320-44ca-87a5-5b91250348ea
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 0%

---

# Sannolikhetsrapport för upprepade order

## När är `Incremental Event Probability` tillgängliga perspektiv?

The `incremental event probability` perspektiv är bara tillgängligt när filter använder dimensioner som är lika för alla order (till exempel användarens `gender`, användarens `age` eller användarens `source`)

Detta beror på att perspektivet bygger på en dimension som kallas `User's order number` för segmentering, som numrerar en användares inköp (t.ex. Johns första, andra och tredje order).

Om vi lägger till ett filter som använder en dimension som inte är lika för alla order (till exempel `Order's Region`), `User's order number` dimensionen skulle inte längre vara exakt eftersom den inte tar hänsyn till specifika regioner när en användares order numreras (t.ex. så är John:s första, andra och tredje order fortfarande desamma oavsett region).

## Förvandla en orderspecifik dimension till en användarspecifik dimension

I vissa fall kan vi kanske ändra `order-specific` dimension till en `user-specific` dimension som ska läggas till som filter i `Repeat Order Probability` diagram. I dessa fall returnerar vi beställningsattributet för en användares första order eller senaste order (t.ex. användarens namn för första orderområde).

Om du vill skapa en sådan ny dimension [kontakta support](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).

## Jämföra upprepningssannolikhet för order med olika attribut

Om du vill jämföra antalet upprepade köp för olika orderattribut (till exempel orderns `region`) rekommenderar vi att du skapar ett diagram som liknar `Users by lifetime number of orders` som visar hur många användare som har skapat 1, 2, 3,.. antal order under hela löptiden och lägg till ordernivåfiltret. (med andra ord, detta kan visa dig om användarna gör fler eller mindre upprepade inköp i en region eller en annan.)

Siffrorna som utgör ett sådant diagram kan sedan exporteras till excel för att beräkna sannolikhetsförhållandet för upprepade order. Att se sannolikheten för kunder som `(x)` order att skapa `(x+1)` order, enkelt` divide the number of people who've made at least (x+1) purchases by the number of people who have made at least (x)` inköp.

### Exempel:

|  |  |
|---|---|
| Antal kunder som gjort ett köp under sin livstid | `90` |
| Antal kunder som gjort två inköp under sin livstid | `30` |
| Antal kunder som gjort tre inköp under sin livstid | `10` |
| Sannolikheten för upprepade order för kunder som har gjort ett köp under sin livstid för att göra ett andra inköp | `(30 + 10) / (30+10+90) = 30.77%` |
