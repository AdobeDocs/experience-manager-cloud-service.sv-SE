---
title: Lägga till en TXT-post
description: Lägga till ett anpassat domännamn
exl-id: d441de29-af41-4d3e-9155-531af9702841
source-git-commit: 12849a79975f70dafd59f4b6ebf4b4ff24145cbf
workflow-type: tm+mt
source-wordcount: '313'
ht-degree: 0%

---

# Lägga till en TXT-post {#adding-txt}

En DNS TXT-post tillåter en domän att vara värd för en CDN-tjänst. Kunden måste skapa en DNS TXT-post i den zon som tillåter Cloud Manager att distribuera CDN-tjänsten med den anpassade domänen och associera den med serverdelstjänsten. Den här associationen styrs helt av kunden och ger molnhanteraren rätt att skicka innehåll från tjänsten till en domän. Tillståndet får beviljas och återkallas.

Du måste följa stegen nedan innan du skapar en TXT-post:

* Ha möjlighet att ändra DNS-posterna för organisationens domän, eller kontakta rätt person som kan det.
* Identifiera din domänvärd eller registrator om du inte redan känner till den.

När du initierar domänverifiering får du det namn och TXT-värde du ska använda för verifiering i Cloud Manager. Lägg till en TXT-post till domänens DNS-server med det angivna namnet och värdet.

1. Logga in på din domänvärd och gå till avsnittet DNS-poster.
1. Lägg till `_aemverification.[yourdomainname]` som namn och lägg till TXT-värdet exakt som det visas.
Se exemplen i tabellen nedan.

| Domän | Namn | TXT-värde |
|--- |--- |---|
| `example.com` | `_aemverification.example.com` | Kopiera hela värdet som visas i användargränssnittet i Cloud Manager. Detta är specifikt för domänen och miljön. Exempel:<br>*adobe-aem-verification=example.com/[program]/[env]/..* |
| `www.example.com` | `_aemverification.www.example.com` | Kopiera hela värdet som visas i användargränssnittet i Cloud Manager. Detta är specifikt för domänen och miljön. Exempel:<br>*adobe-aem-verification=www.example.com/[program]/[env]/..* |

När du är klar kan du verifiera resultatet genom att köra: `dig _aemverification.[yourdomainname] -t txt`.
Det förväntade resultatet ska visa det TXT-värde som anges i användargränssnittet i molnhanteraren.

Om din domän till exempel är `example.com`och kör sedan: `dig TXT _aemverification.example.com -t txt`.

>[!NOTE]
>Det finns också olika [Verktyg för DNS-sökning](https://www.ultratools.com/tools/dnsLookup)kan Google DoH användas för att söka efter TXT-postposter och identifiera om TXT-posten saknas eller är felaktig.
