---
title: Lägga till en TXT-post
description: Lär dig hur du lägger till en TXT-post för att lägga till ett eget domännamn i Cloud Manager.
exl-id: d441de29-af41-4d3e-9155-531af9702841
source-git-commit: 491e710223c5878bfa81c4b0a57d18ec0ec29479
workflow-type: tm+mt
source-wordcount: '332'
ht-degree: 1%

---

# Lägga till en TXT-post {#adding-txt}

En DNS TXT-post tillåter en domän att vara värd för en CDN-tjänst. Du måste skapa en DNS TXT-post i zonen som tillåter Cloud Manager att distribuera CDN-tjänsten med den anpassade domänen och associera den med serverdelstjänsten. Den här associationen står helt under din kontroll och godkänner att Cloud Manager skickar innehåll från tjänsten till en domän. Detta tillstånd kan beviljas såväl som återkallas. TXT-posten är specifik för domänen och Cloud Manager-miljön.

Du måste uppfylla dessa krav innan du lägger till en TXT-post.

* Du måste kunna ändra DNS-posterna för din organisations domän eller kontakta rätt person som kan det.
* Du måste identifiera din domänvärd eller registrator om du inte redan känner till den.

När du initierar domänverifiering får du det namn och TXT-värde du ska använda för verifiering i Cloud Manager. Lägg till en TXT-post till domänens DNS-server med det angivna namnet och värdet.

1. Logga in på din domänvärd och hitta avsnittet med DNS-poster.
1. Lägg till `_aemverification.[yourdomainname]` som **Namn** och lägg till TXT-värdet exakt som det ser ut.

Se exemplen i den här tabellen.

| Domän | Namn | TXT-värde |
|--- |--- |---|
| `example.com` | `_aemverification.example.com` | Kopiera hela värdet som visas i användargränssnittet i Cloud Manager. Detta är specifikt för domänen och miljön. Till exempel:<br>`adobe-aem-verification=example.com/[program]/[env]/..*` |
| `www.example.com` | `_aemverification.www.example.com` | Kopiera hela värdet som visas i användargränssnittet i Cloud Manager. Detta är specifikt för domänen och miljön. Till exempel:<br>`adobe-aem-verification=www.example.com/[program]/[env]/..*` |

När du är klar kan du verifiera resultatet genom att köra följande kommando

```shell
dig _aemverification.[yourdomainname] -t txt
```

Det förväntade resultatet ska visa det TXT-värde som anges i användargränssnittet i molnhanteraren.

Om din domän till exempel är `example.com`och kör sedan:

```shell
dig TXT _aemverification.example.com -t txt
```

>[!TIP]
>
>Det finns ett antal [Verktyg för DNS-sökning](https://www.ultratools.com/tools/dnsLookup) tillgängliga. Google DoH kan användas för att söka efter TXT-postposter och identifiera om TXT-posten saknas eller är felaktig.
