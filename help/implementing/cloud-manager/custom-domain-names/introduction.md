---
title: Introduktion till anpassade domännamn
description: Med Cloud Manager användargränssnitt kan du lägga till en anpassad domän för att identifiera din webbplats med ett unikt, varumärkesprofilerat namn på ett självbetjäningssätt.
exl-id: ed03bff9-dfcc-4dfe-a501-a7facd24aa7d
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 4e887b753eaf09e104c68484792f00dcb08ee304
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 1%

---


# Introduktion till anpassade domännamn {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_domains"
>title="Hantera anpassade domännamn"
>abstract="Med Cloud Manager användargränssnitt kan du lägga till en anpassad domän för att identifiera din webbplats med ett unikt, varumärkesprofilerat namn på ett självbetjäningssätt."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name" text="Lägga till ett anpassat domännamn"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/managing-custom-domain-names" text="Visa och uppdatera anpassat domännamn"

Adobe Experience Manager as a Cloud Service har etablerats med ett standarddomännamn som slutar på `*.adobeaemcloud.com`. Med hjälp av Cloud Manager användargränssnitt kan du lägga till en anpassad domän för att identifiera din webbplats med ett unikt, varumärkesprofilerat namn på ett självbetjäningssätt. Standarddomännamnet `*.adobeaemcloud.com` kvarstår, även efter att du har associerat anpassade domännamn till webbplatsen.

## Vad är anpassade domännamn? {#what-are-custom-domain-names}

Varje webbplats har en unik, maskinläsbar, numerisk adress som är associerad med den, till exempel `184.33.123.64`. DNS (Domain Name System) är det som gör att du kan ha anpassade, varumärkesanpassade domäner kopplade till webbplatser genom att översätta numeriska adresser till minnesvärda adresser som `wknd.com`.

Det är god praxis att ha ett domännamn för er webbplats som är minnesvärt för era kunder och som speglar ert varumärke.

Du kan köpa ett domännamn från en domännamnsregistrator, ett företag eller en organisation som hanterar och säljer domännamn. Domännamnsregistrerare hanterar domännamn på DNS-servrar.

>[!IMPORTANT]
>
>Cloud Manager är inte en domännamnsregistrator och tillhandahåller inga DNS-tjänster.

## Anpassade domännamn och ta med egna CDN:er {#byo-cdn}

AEM as a Cloud Service har ett inbyggt nätverk för innehållsleverans (CDN), men du kan även använda ditt eget CDN för att använda det med AEM. Anpassade domäner kan installeras antingen i det AEM CDN eller i ett CDN som du hanterar.

* Cloud Manager hanterar anpassade domännamn och certifikat som installeras i det AEM hanterade CDN.
* Anpassade domännamn och certifikat som installeras i ett BYO CDN hanteras direkt i det CDN:et.

**Domäner som hanteras i ditt eget CDN kräver inte installation via Cloud Manager**. De blir tillgängliga för AEM via X-Forwarded-Host och matchar de värdar som definierats i Dispatcher. Se [CDN-dokumentationen](/help/implementing/dispatcher/cdn.md).

I en miljö kan du ha båda domänerna installerade i det AEM hanterade CDN och installerade i ett BYO CDN.

## Arbetsflöde {#workflow}

Om du vill lägga till ett anpassat domännamn måste DNS-tjänsten och Cloud Manager interagera. På grund av det här arbetsflödet krävs flera steg för att installera, konfigurera och verifiera anpassade domännamn. I följande tabell visas en översikt över de steg som krävs, inklusive länkar till dokumentationsresurser för att slutföra de stegen.

| Steg | Beskrivning | Dokumentation |
|---|---|---|
| 1 | Lägg till SSL-certifikat i Cloud Manager | [Lägg till ett SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) |
| 2 | Lägg till anpassad domän i Cloud Manager | [Lägg till ett anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) |
| 3 | Lägg till TXT-post för att verifiera domän | [Lägg till en TXT-post](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) |
| 4 | Granska domänverifieringsstatus | [Kontrollera domännamnsstatus](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 5 | Konfigurera DNS-inställningar genom att lägga till DNS CNAME- eller APEX-poster som pekar på AEM as a Cloud Service | [Konfigurera DNS-inställningar](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) |
| 6 | Kontrollera DNS-poststatus | [Kontrollera DNS-poststatus](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |

>[!TIP]
>
>Att konfigurera anpassade domännamn med AEM som en molntjänst är vanligtvis en enkel process. Ibland kan dock problem med domändelegering uppstå som kan ta 1-2 arbetsdagar att lösa. Därför rekommenderar vi att du installerar domänerna långt innan de publiceras. Mer information finns i dokumentet [Kontrollera domännamnsstatus](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).

## Begränsningar {#limitations}

Det finns flera begränsningar för hur du använder anpassade domännamn med AEMaaCS.

* Anpassade domännamn stöds i Cloud Manager endast för publicerings- och förhandsgranskningstjänster för Sites-program.
   * Anpassade domäner för författartjänster stöds inte.
* Varje Cloud Manager-miljö har plats för upp till 500 anpassade domäner per miljö.
* Det går inte att lägga till domännamn i miljöer när det finns en aktuell pågående pipeline som är kopplad till dessa miljöer.
* Samma domännamn kan inte användas i mer än en miljö.
* Det går bara att lägga till ett domännamn åt gången.
* AEM as a Cloud Service stöder inte jokerdomäner som `*.example.com`.
* Innan du lägger till ett anpassat domännamn måste ett giltigt SSL-certifikat som innehåller det anpassade domännamnet (jokerteckenscertifikat är giltiga) installeras för programmet.

## Kom igång {#get-started}

* Kom igång med att konfigurera ett nytt anpassat domännamn för ditt projekt genom att [lägga till ett SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md).
* Hantera dina befintliga domännamn genom att granska dokumentet [Hantera anpassade domännamn](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md).
