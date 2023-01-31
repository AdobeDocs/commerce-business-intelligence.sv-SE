---
title: Begränsa åtkomst till databasen
description: Lär dig hur du kan begränsa åtkomsten och begränsa åtkomsten till servern där databasen finns.
exl-id: 7a0bc0d7-086e-4a6e-b1dd-6db13814710e
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '221'
ht-degree: 0%

---

# Begränsa åtkomst

När vi skapar en SSH-tunnel till din server behövs ingen [!DNL MBI] för att få tillgång till allt annat än databasen. Om du inte vill [!DNL MBI] om du vill ha fullständig åtkomst till den server där databasen finns, kan du begränsa åtkomsten genom att tvinga [!DNL MBI Linux] till en [begränsat basgränssnitt](https://www.gnu.org/software/bash/manual/html_node/The-Restricted-Shell.html).

Du kan ha gissat från namnet, men ett begränsat bashylsa används för att konfigurera en miljö som är mer kontrollerad än standardskalet. Det viktiga med den här typen av gränssnitt är att begränsade gränssnittsanvändare inte har åtkomst till systemfunktioner eller kan göra några ändringar.

Begränsa [!DNL MBI Linux] -användare måste du göra två saker:

1. Ändra miljövariabeln PATH till en tom sträng. Detta innebär att användaren inte kommer att kunna komma åt systemkörbara filer.

1. Kontrollera att det kommando som körs är `bash -r`

Båda dessa kan göras inuti `authorized_keys` fil i användarens hem `dir/.ssh` som en del av det kommando som körs när användaren loggar in. Det kommer att se ut ungefär så här:

```bash
... other keys ...
command="env PATH="" /bin/bash -r" <rjmetrics public key goes here>
... other keys ...
```

När allt är klart har användaren du skapat för [!DNL MBI] kan inte göra några ändringar i systemet.
