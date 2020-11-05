---
title: Verifierar domän
description: Verifierar domän
translation-type: tm+mt
source-git-commit: d2a98cf340dc755407250a9a9649addb75ad87d2
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 0%

---


# Verifierar domän {#verify-domain-name}

En DNS TXT-post tillåter en domän att vara värd för en CDN-tjänst. Kunden måste skapa en DNS TXT-post i den zon som tillåter Cloud Manager att distribuera CDN-tjänsten med den anpassade domänen och associera den med serverdelstjänsten. Den här associationen styrs helt av kunden och ger molnhanteraren rätt att skicka innehåll från tjänsten till en domän. Tillståndet får beviljas och återkallas. TXT-posten är specifik för domänen och Cloud Manager-miljön.

1. Logga in på din domänvärd och gå till avsnittet DNS-poster.
1. Kopiera och klistra in TXT-posten i DNS-zonen där den anpassade domänen finns, exakt som den visas. Om du behöver ett namn för bidraget, ge det `@`.

>[!NOTE]
>Olika verktyg för DNS-sökning, som [DNS-sökningsverktyget](https://www.ultratools.com/tools/dnsLookup)och Google DoH, kan användas för att söka efter TXT-postposter och identifiera om TXT-posten saknas eller är felaktig.
