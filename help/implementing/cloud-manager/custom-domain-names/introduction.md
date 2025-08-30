---
title: Introduktion till anpassade domännamn
description: Med Cloud Manager användargränssnitt kan du lägga till en anpassad domän för att identifiera din webbplats med ett unikt, varumärkesprofilerat namn på ett självbetjäningssätt.
exl-id: ed03bff9-dfcc-4dfe-a501-a7facd24aa7d
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: fdd86b966f0480c00b7cd975d63a48b82fb1d027
workflow-type: tm+mt
source-wordcount: '698'
ht-degree: 1%

---


# Introduktion till anpassade domännamn {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_domains"
>title="Hantera anpassade domännamn"
>abstract="Med Cloud Manager användargränssnitt kan du lägga till en anpassad domän för att identifiera din webbplats med ett unikt, varumärkesprofilerat namn på ett självbetjäningssätt."
>additional-url="https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name" text="Lägga till ett anpassat domännamn"
>additional-url="https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/managing-custom-domain-names" text="Visa och uppdatera anpassat domännamn"

Adobe Experience Manager as a Cloud Service har etablerats med ett standarddomännamn som slutar på `*.adobeaemcloud.com`. Med hjälp av Cloud Manager användargränssnitt kan du lägga till en anpassad domän för att identifiera din webbplats med ett unikt, varumärkesprofilerat namn på ett självbetjäningssätt. Standarddomännamnet `*.adobeaemcloud.com` kvarstår, även efter att du har associerat anpassade domännamn till webbplatsen.

## Vad är anpassade domännamn? {#what-are-custom-domain-names}

Varje webbplats har en unik, maskinläsbar, numerisk adress som är associerad med den, till exempel `184.33.123.64`. DNS (Domain Name System) är det som gör att du kan ha anpassade, varumärkesanpassade domäner kopplade till webbplatser genom att översätta numeriska adresser till minnesvärda adresser som `wknd.com`.

Det är god praxis att ha ett domännamn för er webbplats som är minnesvärt för era kunder och som speglar ert varumärke.

Du kan köpa ett domännamn från en domännamnsregistrator, ett företag eller en organisation som hanterar och säljer domännamn. Domännamnsregistrerare hanterar domännamn på DNS-servrar.

>[!IMPORTANT]
>
>Cloud Manager är inte en domännamnsregistrator och tillhandahåller inga DNS-tjänster.

## Anpassade domännamn och ta med dina egna CDN:er {#byo-cdn}

AEM as a Cloud Service har en inbyggd CDN-tjänst (Content Delivery Network) som även gör att du kan använda ditt eget CDN tillsammans med AEM. Anpassade domäner kan installeras antingen i det CDN som hanteras av AEM eller i ett CDN som du hanterar.

* Cloud Manager hanterar anpassade domännamn och certifikat som installeras i det AEM-hanterade CDN.
* Anpassade domännamn och certifikat som installeras i ett BYO CDN hanteras direkt i det CDN:et.

**Domäner som hanteras i ditt eget CDN kräver inte installation via Cloud Manager**. De görs tillgängliga för AEM via X-Forwarded-Host och matchar de värdar som definierats i Dispatcher. Se [CDN-dokumentationen](/help/implementing/dispatcher/cdn.md).

I en miljö kan du ha båda domänerna installerade i det AEM-hanterade CDN och installerade i ett BYO CDN.

## Arbetsflöde {#workflow}

Om du vill lägga till ett anpassat domännamn måste DNS-tjänsten och Cloud Manager interagera. På grund av det här arbetsflödet krävs flera steg för att installera, konfigurera och verifiera anpassade domännamn. I följande tabell beskrivs de steg som krävs, med länkar till dokumentationsresurserna för att slutföra de stegen.

>[!WARNING]
>
>Kör endast steg 4 (Konfigurera DNS) *när* steg 3 (Lägg till domänmappning) har slutförts. Efter den här ordern registreras domänen med Adobe CDN och rätt routning ställs in, vilket skyddar din webbplats från domänövertaganden.

| Steg | Beskrivning |
| --- | --- |
| 1 | [Lägg till SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) |
| 2 | [Lägg till en anpassad domän](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) |
| 3 | [Lägg till domänmappning](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) |
| 4 | [Konfigurera DNS](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#config-dns) |
| 5 | [Kontrollera DNS-status](/help/implementing/cloud-manager/custom-domain-names/check-dns-record-status.md) |

>[!TIP]
>
>Att konfigurera anpassade domännamn med AEM som en molntjänst är vanligtvis en enkel process. Ibland kan dock problem med domändelegering uppstå som kan ta 1-2 arbetsdagar att lösa. Därför rekommenderar vi att du installerar domänerna långt innan de blir aktiva. Mer information finns i dokumentet [Kontrollera domännamnsstatus](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md).

## Användningsinformation {#usage-notes}

* Anpassade domännamn stöds i Cloud Manager endast för publicerings- och förhandsgranskningstjänster för Sites-program.
   * Anpassade domäner för författartjänster stöds inte.
* Varje Cloud Manager-miljö har plats för upp till 500 anpassade domäner per miljö.
* Det går inte att lägga till domännamn i miljöer när det finns en aktuell pågående pipeline som är kopplad till dessa miljöer.
* Samma domännamn kan inte användas i mer än en miljö.
* Det går bara att lägga till ett domännamn åt gången.
* AEM as a Cloud Service stöder inte jokerdomäner som `*.example.com`.
* Innan du lägger till ett anpassat domännamn måste ett giltigt SSL-certifikat som innehåller det anpassade domännamnet (jokerteckenscertifikat är giltiga) installeras för programmet.
* Ytterligare konfigurationssteg krävs för att använda ett anpassat domännamn med funktionen [Front-End Pipeline](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md#custom-domains).

## Kom igång {#get-started}

* Kom igång med att konfigurera ett nytt anpassat domännamn för ditt projekt genom att [lägga till ett SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md).
* Hantera dina befintliga domännamn genom att granska dokumentet [Hantera anpassade domännamn](/help/implementing/cloud-manager/custom-domain-names/managing-custom-domain-names.md).
