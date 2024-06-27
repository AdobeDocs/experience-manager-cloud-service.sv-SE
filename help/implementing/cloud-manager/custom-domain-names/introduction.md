---
title: Introduktion till anpassade domännamn
description: Med Cloud Manager användargränssnitt kan du lägga till en anpassad domän för att identifiera din webbplats med ett unikt, varumärkesprofilerat namn på ett självbetjäningssätt.
exl-id: ed03bff9-dfcc-4dfe-a501-a7facd24aa7d
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '741'
ht-degree: 0%

---


# Introduktion till anpassade domännamn {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_domains"
>title="Hantera anpassade domännamn"
>abstract="Med Cloud Manager användargränssnitt kan du lägga till en anpassad domän för att identifiera din webbplats med ett unikt, varumärkesprofilerat namn på ett självbetjäningssätt."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name" text="Lägga till ett anpassat domännamn"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/managing-custom-domain-names" text="Visa och uppdatera anpassat domännamn"

Med Cloud Manager användargränssnitt kan du lägga till en anpassad domän för att identifiera din webbplats med ett unikt, varumärkesprofilerat namn på ett självbetjäningssätt. Adobe Experience Manager as a Cloud Service etableras med ett standarddomännamn som slutar på `*.adobeaemcloud.com`. Det här standarddomännamnet kvarstår, även efter att du har associerat anpassade domännamn till webbplatsen.

## Vad är anpassade domännamn? {#what-are-custom-domain-names}

Varje webbplats har en unik, maskinläsbar, numerisk adress, som `184.33.123.64`. Med DNS (Domain Name System) kan du ha anpassade domäner kopplade till webbplatser genom att översätta numeriska adresser till minnesvärda adresser som `wknd.com`.

Det är god praxis att ha ett domännamn för er webbplats som är minnesvärt för era kunder och som speglar ert varumärke.

Du kan köpa ett domännamn från en domännamnsregistrator, ett företag eller en organisation som hanterar och säljer domännamn. Domännamnsregistrerare hanterar domännamn på DNS-servrar.

>[!IMPORTANT]
>
>Cloud Manager är inte en domännamnsregistrator och tillhandahåller inga DNS-tjänster.

## Anpassade domännamn och CDN för BYO {#byo-cdn}

AEM as a Cloud Service har ett inbyggt nätverk för innehållsleverans (CDN), men du kan även hämta ditt eget CDN (BYO) för AEM. Anpassade domäner kan installeras antingen i det AEM CDN eller i ett CDN som du hanterar.

* Anpassade domännamn (och certifikat) som är installerade i det AEM CDN hanteras via Cloud Manager.
* Anpassade domännamn (och certifikat) som är installerade i ditt eget CDN hanteras i det specifika CDN.

Domäner som hanteras i ditt eget CDN behöver inte installeras med Cloud Manager. De görs tillgängliga för AEM via X-Forwarded-Host och matchar de värdar som definierats i Dispatcher. Se [CDN-dokumentation](/help/implementing/dispatcher/cdn.md).

I en och samma miljö kan du ha båda domänerna installerade i det AEM CDN:et och installerade i ditt eget CDN.

## Arbetsflöde {#workflow}

Om du vill lägga till ett anpassat domännamn måste DNS-tjänsten och Cloud Manager interagera. På grund av detta krävs flera steg för att installera, konfigurera och verifiera anpassade domännamn. Följande tabell ger en översikt över de steg som krävs, inklusive vad som ska göras när vanliga fel inträffar.

| Steg | Beskrivning | Ansvarsområde | Läs mer |
|--- |--- |--- |---|
| 1 | Lägg till SSL-certifikat i Cloud Manager | Kund | [Lägga till ett SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) |
| 2 | Lägg till TXT-post för att verifiera domän | Kund | [Lägga till en TXT-post](/help/implementing/cloud-manager/custom-domain-names/add-text-record.md) |
| 3 | Verifieringsstatus för domän | Kund | [Kontrollerar domännamnsstatus](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 3a | Om domänverifieringen misslyckas med statusen `Domain Verification Failure` | Kund | [Kontrollerar domännamnsstatus](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 3b | Om domänverifieringen misslyckas med statusen `Verified, Deployment Failed`, kontakta Adobe | Adobe kundtjänst | [Kontrollerar domännamnsstatus](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) |
| 4 | Konfigurera DNS-inställningar genom att lägga till DNS CNAME- eller APEX-poster som pekar på AEM as a Cloud Service | Kund | [Konfigurera DNS-inställningar](/help/implementing/cloud-manager/custom-domain-names/configure-dns-settings.md) |
| 5 | Kontrollera DNS-poststatus | Kund | [Kontrollerar DNS-poststatus](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |
| 5a | Om DNS-poststatus misslyckas med `DNS status not detected` | Kund | [Kontrollerar DNS-poststatus](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |
| 5b | Om DNS-poststatus misslyckas med `DNS resolves incorrectly` | Kund | [Kontrollerar DNS-poststatus](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |

>[!TIP]
>
>Att konfigurera anpassade domännamn med AEM som en molntjänst är vanligtvis en enkel process. Det kan dock ibland uppstå domändelegeringsproblem som kan ta 1-2 arbetsdagar att lösa. Därför rekommenderar vi att du installerar domänerna långt innan de publiceras. Se dokumentet [Kontrollerar domännamnsstatus](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) för mer information.

## Begränsningar {#limitations}

Det finns flera begränsningar för hur du använder anpassade domännamn med AEMaaCS.

* Anpassade domännamn stöds i Cloud Manager för både publicerings- och förhandsgranskningstjänster för Sites-program. Anpassade domäner för författartjänster stöds inte.
* Varje Cloud Manager-miljö har plats för upp till 500 anpassade domäner per miljö.
* Det går inte att lägga till domännamn i miljöer när det finns en aktuell pågående pipeline som är kopplad till dessa miljöer.
* Samma domännamn kan inte användas i mer än en miljö.
* Det går bara att lägga till ett domännamn åt gången.
* AEM as a Cloud Service stöder inte jokerdomäner som `*.example.com`.
* Innan du lägger till ett anpassat domännamn måste ett giltigt SSL-certifikat som innehåller det anpassade domännamnet (jokerteckenscertifikat är giltiga) installeras för programmet. Se [Lägga till ett SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) om du vill veta mer.
