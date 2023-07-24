---
title: UTM-spårning i Google Analytics
description: Läs mer om de effektivaste strategierna för UTM-spårning (taggning) i Google Analytics.
exl-id: 70bfd855-3b3f-469b-99bc-deb8251904b7
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# UTM-spårning

`UTM` tracking är en taggningskonvention för URL:er som gör att du kan analysera varifrån användarna kommer. Om du tittar på de URL:er du klickar på i de flesta marknadsföringsannonser eller banners visas UTM-taggning. Det är de långa länkarna som slutar med saker som `utm\_source` och `utm\_medium`.

[!DNL Google Analytics] använder `UTM` taggning för att ta reda på var trafiken kommer ifrån. En del av den här informationen kommer från [HTTP-referens](https://en.wikipedia.org/wiki/HTTP_referer) men resten måste du ge dig själv `UTM` parametrar. När du ser `google adwords` eller `email marketing`betyder det `UTM` parametrar som spelas in från den ursprungliga länkklickningen och sedan lagras i användarens cookies. Därifrån [!DNL Google Analytics] använder dessa data för [attributintressanta beteenden](../data-analyst/analysis/google-track-user-acq.md) på din webbplats. Genom att förstå vad de här parametrarna är till för får du en förståelse för hur du bäst konfigurerar och använder UTM-taggning.

## Bästa tillvägagångssätt för UTM-taggning

Nedan visas de fem viktigaste sakerna att komma ihåg när du konfigurerar dina URL-adresser med `UTM` taggning.

### 1. Rikta in dig på att tagga varje URL som du kan styra när du kommer till webbplatsen

Varje gång du ber någon klicka på en länk bör du konfigurera `UTM` taggning. Detta inkluderar alla e-postlänkar (din e-postleverantör har troligen ett sätt att automatiskt tagga dina URL:er), annonslänkar, pressartiklar och blogginlägg.

### 2. Skapa URL:en med ett verktyg

`UTM`URL:er med -taggar kan vara krångliga. Använd ett verktyg i stället för att försöka skriva ut dem på lång sikt [gillar detta](https://support.google.com/analytics/answer/1033867?hl=en) för att hjälpa dig. Detta garanterar att du funderar genom att lägga till alla rimliga parametrar till URL:en, och du får URL:en att kopiera och klistra in direkt från den. För att hantera sociala länkar, verktyg som [!DNL Hootsuite] kan du lägga till egna URL-parametrar till alla länkar.

### 3. Se till att du är skiftlägeskänslig i parametervärdena

Det är viktigt att komma ihåg att taggen `utm\_source=adwords` är en annan tagg än `utm\_source=Adwords`. Överväg att göra allt i gemener.

### 4. Lagra UTM-parametervärden i databasen

Varje gång en transaktion eller händelse inträffar vill ni utvärdera resultatet av era marknadsföringsaktiviteter. Du kan göra detta genom att läsa värdena för UTM-parametervärdena från [[!DNL Google Analytics] cookie-fil i din databas](../data-analyst/analysis/google-track-user-acq.md).

### 5. Fundera på hur ni namnger kampanjer

För att kunna spåra hur marknadsföringsarbetet förbättras med tiden måste ni vara smarta med namngivningskonventionerna. Gör det enkelt och minimera så mycket som möjligt. Komplicerade namnsystem är svårare att underhålla.

När ni väl har samlat in dessa data i databasen kan ni utvärdera resultatet av er marknadsföring och annonsering genom mer sofistikerade analyser, bland annat [Kundens livstidsvärde](../data-analyst/analysis/ess-expected-ltv.md), [Upprepa inköpsavgifter](../data-analyst/analysis/repurchase-behavior.md)och [Genomsnittligt ordervärde](../data-analyst/analysis/basic-analytics.md).
