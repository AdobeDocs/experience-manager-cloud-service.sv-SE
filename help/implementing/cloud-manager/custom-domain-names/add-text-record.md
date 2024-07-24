---
title: Lägga till en TXT-post
description: Lär dig hur du lägger till TXT-post för att verifiera din ägarskap av en anpassad domän som kan användas med Cloud Manager.
exl-id: d441de29-af41-4d3e-9155-531af9702841
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 06e961febd7cb2ea1d8fca00cb3dee7f7ca893c9
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---


# Lägga till en TXT-post {#adding-txt}

Lär dig hur du lägger till TXT-post för att verifiera din ägarskap av en anpassad domän som kan användas med Cloud Manager.

## Vad är en TXT-post? {#what-is}

En textpost (kallas även TXT-post) är en typ av resurspost i DNS (Domain Name System). Det gör det möjligt att associera godtycklig text med ett värdnamn, till exempel läsbar information om ett värdnamn som server- eller nätverksinformation.

Cloud Manager använder en specifik TXT-post för att godkänna att en domän är värd för en CDN-tjänst. Du måste skapa en DNS TXT-post i zonen som tillåter Cloud Manager att distribuera CDN-tjänsten med den anpassade domänen och associera den med serverdelstjänsten. Den här associationen står helt under din kontroll och godkänner att Cloud Manager skickar innehåll från tjänsten till en domän. Detta tillstånd får beviljas och återkallas. TXT-posten är specifik för domänen och Cloud Manager-miljön.

## Krav {#requirements}

Du måste uppfylla dessa krav innan du lägger till en TXT-post.

* Du måste identifiera din domänvärd eller registrator om du inte redan känner till den.
* Du måste kunna redigera DNS-posterna för din organisations domän eller kontakta rätt person som kan göra det.
* Du måste först lägga till ett anpassat domännamn enligt beskrivningen i dokumentet [Lägga till ett anpassat domännamn.](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)

## Lägga till en TXT-post för verifiering {#verification}

En TXT-post läggs till som en del av verifieringen av ett anpassat domännamn som ska användas med Cloud Manager.

1. Du måste först lägga till ett anpassat domännamn enligt beskrivningen i dokumentet [Lägga till ett anpassat domännamn.](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md)

1. På fliken **Verifiering** i dialogrutan **Lägg till domännamn** visar Cloud Manager det namn och TXT-värde som ska användas för verifiering. Kopiera det här värdet.

   ![Verifiering av domännamn](/help/implementing/cloud-manager/assets/cdn/cdn-create6.png)

1. Logga in på din domänvärd och hitta avsnittet med DNS-poster.

1. Lägg till `_aemverification.[yourdomainname]` som **namn** för värdet och lägg till TXT-värdet exakt som det visas i dialogrutan **Lägg till domännamn**.

   * Se [exemplen i följande avsnitt.](#examples)

1. Spara TXT-posten till domänvärden.

## Exempel på TXT-post {#examples}

| Domän | Namn | TXT Value |
|--- |--- |---|
| `example.com` | `_aemverification.example.com` | Kopiera hela värdet som visas i Cloud Manager-gränssnittet. Detta är specifikt för domänen och miljön. Till exempel:<br>`adobe-aem-verification=example.com/[program]/[env]/..*` |
| `www.example.com` | `_aemverification.www.example.com` | Kopiera hela värdet som visas i Cloud Manager-gränssnittet. Detta är specifikt för domänen och miljön. Till exempel:<br>`adobe-aem-verification=www.example.com/[program]/[env]/..*` |

## Verifiera TXT-post {#verify}

När du är klar kan du verifiera resultatet genom att köra följande kommando.

```shell
dig _aemverification.[yourdomainname] -t txt
```

Det förväntade resultatet ska visa det TXT-värde som anges på fliken **Verifiering** i dialogrutan **Lägg till domännamn** i Cloud Manager-gränssnittet.

Om din domän till exempel är `example.com` kör du:

```shell
dig TXT _aemverification.example.com -t txt
```

>[!TIP]
>
>Det finns flera [tillgängliga DNS-sökverktyg](https://www.ultratools.com/tools/dnsLookup). Google DoH kan användas för att söka efter TXT-postposter och identifiera om TXT-posten saknas eller är felaktig.

>[!NOTE]
>
>DNS-verifiering kan ta några timmar att behandla på grund av fördröjd DNS-spridning.
>
>Cloud Manager kontrollerar ägarskap och uppdaterar statusen som visas i tabellen Domäninställningar. Mer information finns i [Kontrollera status för anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).

## Nästa steg {#next-steps}

Nu när du har skapat din TXT-post kan du verifiera din domännamnsstatus. Fortsätt till dokumentet [Kontrollerar domännamnsstatus](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) om du vill fortsätta konfigurera det anpassade domännamnet.

>[!TIP]
>
>TXT-posten och CNAME- eller A-posten kan anges samtidigt på den styrande DNS-servern, vilket sparar tid.
>
>Om du vill göra det ska du först granska hela processen med att konfigurera ett anpassat domännamn enligt beskrivningen i dokumentet [Introduktion till anpassade domännamn](/help/implementing/cloud-manager/custom-domain-names/introduction.md). Observera då dokumentet [help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) och uppdatera dina DNS-inställningar på lämpligt sätt.