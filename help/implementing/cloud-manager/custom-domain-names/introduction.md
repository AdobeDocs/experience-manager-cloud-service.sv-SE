---
title: Introduktion till anpassade domännamn
description: Med Cloud Managers användargränssnitt kan du lägga till en anpassad domän för att identifiera din webbplats med ett unikt, varumärkesprofilerat namn på ett självbetjäningssätt.
exl-id: ed03bff9-dfcc-4dfe-a501-a7facd24aa7d
source-git-commit: d22d657361ea6c4885babd76e6b4c10f88378994
workflow-type: tm+mt
source-wordcount: '665'
ht-degree: 1%

---


# Introduktion till anpassade domännamn {#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_domains"
>title="Hantera anpassade domännamn"
>abstract="Med Cloud Managers användargränssnitt kan du lägga till en anpassad domän för att identifiera din webbplats med ett unikt, varumärkesprofilerat namn på ett självbetjäningssätt."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name.html" text="Lägga till ett anpassat domännamn"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/custom-domain-names/view-update-replace-custom-domain-name.html" text="Visa och uppdatera anpassat domännamn"

Med Cloud Managers användargränssnitt kan du lägga till en anpassad domän för att identifiera din webbplats med ett unikt, varumärkesprofilerat namn på ett självbetjäningssätt. Adobe Experience Manager as a Cloud Service etableras med ett standarddomännamn som slutar på `*.adobeaemcloud.com`. Det här standarddomännamnet kvarstår, även efter att du har associerat anpassade domännamn till webbplatsen.

## Vad är anpassade domännamn? {#what-are-custom-domain-names}

Varje webbplats har en unik, maskinläsbar, numerisk adress, som `184.33.123.64`. DNS (Domain Name System) är en DNS-server som gör att du kan koppla anpassade domäner till webbplatser genom att översätta numeriska adresser till minnesvärda adresser som `wknd.com`.

Det är god praxis att ha ett domännamn för er webbplats som är minnesvärt för era kunder och som speglar ert varumärke.

Du kan köpa ett domännamn från en domännamnsregistrator, ett företag eller en organisation som hanterar och säljer domännamn. Domännamnsregistrerare hanterar domännamn på DNS-servrar.

>[!IMPORTANT]
>
>Cloud Manager är inte en domännamnsregistrator och tillhandahåller inga DNS-tjänster.

## Begränsningar {#limitations}

Det finns ett antal begränsningar för hur du använder anpassade domännamn med AEMaaCS.

* Anpassade domännamn stöds i Cloud Manager för både publicerings- och förhandsgranskningstjänster för Sites-program. Anpassade domäner på författarsidan stöds inte.
* Varje Cloud Manager-miljö har plats för upp till 500 anpassade domäner per miljö.
* AEM as a Cloud Service stöder inte jokerteckendomäner.
* Innan du lägger till ett anpassat domännamn måste ett giltigt SSL-certifikat som innehåller det anpassade domännamnet installeras för programmet. Mer information finns i Lägga till ett SSL-certifikat.
* Det går inte att lägga till domännamn i miljöer när det finns en aktuell pågående pipeline som är kopplad till dessa miljöer.
* Det går bara att lägga till ett domännamn åt gången.
* Samma domännamn kan inte användas i mer än en miljö.

>[!NOTE]
>
>Anpassade domäner stöds i Cloud Manager **endast** om du använder det AEM hanterade CDN. Om du har ett eget CDN och [peka på det AEM hanterade CDN](/help/implementing/dispatcher/cdn.md) du måste använda det specifika CDN för att hantera domäner, inte Cloud Manager.

## Arbetsflöde {#workflow}

Om du vill lägga till ett anpassat domännamn måste DNS-tjänsten och Cloud Manager interagera. På grund av detta krävs ett antal steg för att installera, konfigurera och verifiera anpassade domännamn. Följande tabell ger en översikt över de steg som krävs, inklusive vad som ska göras när vanliga fel inträffar.

| Steg | Beskrivning | Ansvarsområde | Läs mer |
|--- |--- |--- |---|
| 1 | Lägg till SLL-certifikat i Cloud Manager | Kund | [Lägga till ett SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) |
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
