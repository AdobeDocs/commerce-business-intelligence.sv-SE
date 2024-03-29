---
title: Begränsa åtkomst till databasen
description: Lär dig hur du kan begränsa åtkomsten och begränsa åtkomsten till servern där databasen finns.
exl-id: 7a0bc0d7-086e-4a6e-b1dd-6db13814710e
role: Admin, User
feature: Accounts, User Management
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 0%

---

# Begränsa åtkomst

När du skapar en SSH-tunnel till servern behöver du inte [!DNL Adobe Commerce Intelligence] för att få tillgång till allt annat än databasen. Om du inte vill [!DNL Commerce Intelligence] om du vill ha fullständig åtkomst till servern där databasen finns kan du begränsa åtkomsten genom att tvinga [!DNL Commerce Intelligence Linux] till en [begränsat basgränssnitt](https://www.gnu.org/software/bash/manual/html_node/The-Restricted-Shell.html).

Du kan ha gissat från namnet, men ett begränsat bashylsa används för att konfigurera en miljö som är mer kontrollerad än standardskalet. Det viktiga med den här typen av gränssnitt är att begränsade gränssnittsanvändare inte har åtkomst till systemfunktioner eller kan göra några ändringar.

Begränsa [!DNL Commerce Intelligence Linux] -användare måste du göra två saker:

1. Ändra miljövariabeln PATH till en tom sträng. Det innebär att användaren inte kan komma åt systemkörbara filer.

1. Kontrollera att det kommando som körs är `bash -r`

Båda dessa kan göras inuti `authorized_keys` fil i användarens hem `dir/.ssh` som en del av kommandot som körs när användaren loggar in. Den ser ut ungefär så här:

```bash
... other keys ...
command="env PATH="" /bin/bash -r" <rjmetrics public key goes here>
... other keys ...
```

När detta är klart har användaren du skapat för [!DNL Commerce Intelligence] kan inte göra ändringar i systemet.
