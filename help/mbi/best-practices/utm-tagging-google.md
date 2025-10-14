---
title: UTM-spårning i Google Analytics
description: Läs mer om de effektivaste strategierna för UTM-spårning (taggning) i Google Analytics.
exl-id: 70bfd855-3b3f-469b-99bc-deb8251904b7
role: Admin, Data Architect, Data Engineer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---

# UTM-spårning

Spårning av `UTM` är en märkordskonvention för URL:er som gör att du kan analysera varifrån användarna kommer. Om du tittar på de URL:er du klickar på i de flesta marknadsföringsannonser eller banners visas UTM-taggning. Det är de långa länkarna som slutar med saker som `utm\_source` och `utm\_medium`.

[!DNL Google Analytics] använder `UTM`-taggning för att ta reda på var trafiken kommer från. En del av den här informationen kommer från [HTTP-referenten](https://en.wikipedia.org/wiki/HTTP_referer) men resten måste du ange `UTM`-parametrar till dig själv. När du ser `google adwords` eller `email marketing` betyder det att de `UTM` parametrarna spelas in från den ursprungliga länkklickningen och sedan lagras i användarens cookies. Därifrån använder [!DNL Google Analytics] dessa data för att [attributera intressanta beteenden](../data-analyst/analysis/google-track-user-acq.md) på din webbplats. Genom att förstå vad de här parametrarna är till för får du en förståelse för hur du bäst konfigurerar och använder UTM-taggning.

## Bästa tillvägagångssätt för UTM-taggning

I följande lista visas de fem viktigaste saker som du bör komma ihåg när du konfigurerar dina URL-adresser med `UTM`-taggning.

### &#x200B;1. Rikta in dig på att tagga alla URL:er som du kan styra när du kommer till webbplatsen

Varje gång du ber någon klicka på en länk bör du konfigurera `UTM`-taggningen. Detta inkluderar alla e-postlänkar (din e-postleverantör har troligen ett sätt att automatiskt tagga dina URL:er), annonslänkar, pressartiklar och blogginlägg.

### &#x200B;2. Använd ett verktyg för att skapa URL:en

`UTM`-taggade URL:er kan vara krångliga. Istället för att försöka skriva ut dem på lång sikt kan du använda ett [liknande &#x200B;](https://support.google.com/analytics/answer/1033867?hl=en)-verktyg som kan hjälpa dig. Detta garanterar att du funderar genom att lägga till alla rimliga parametrar till URL:en, och du får URL:en att kopiera och klistra in direkt från den. Om du vill hantera sociala länkar inkluderar verktyg som [!DNL Hootsuite] alternativet att lägga till anpassade URL-parametrar till alla dina länkar.

### &#x200B;3. Kontrollera att du är skiftlägeskänslig i parametervärdena

Det är viktigt att komma ihåg att taggen `utm\_source=adwords` är en annan tagg än `utm\_source=Adwords`. Överväg att göra allt i gemener.

### &#x200B;4. Lagra UTM-parametervärdena i databasen

Varje gång en transaktion eller händelse inträffar vill ni utvärdera resultatet av era marknadsföringsaktiviteter. Du kan göra detta genom att läsa värdena för UTM-parametervärdena från [[!DNL Google Analytics] cookien till din databas](../data-analyst/analysis/google-track-user-acq.md).

### &#x200B;5. Tänk på hur ni namnger kampanjer

För att kunna spåra hur marknadsföringsarbetet förbättras med tiden måste ni vara smarta med namngivningskonventionerna. Gör det enkelt och minimera så mycket som möjligt. Komplicerade namnsystem är svårare att underhålla.

När du har samlat in dessa data i din databas kan du utvärdera marknadsförings- och annonsresultatet med en mer avancerad analys, inklusive [Kundens livstidsvärde](../data-analyst/analysis/ess-expected-ltv.md), [Upprepade inköpspriser](../data-analyst/analysis/repurchase-behavior.md) och [Genomsnittligt ordervärde](../data-analyst/analysis/basic-analytics.md).
