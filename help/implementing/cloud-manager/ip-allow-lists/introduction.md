---
title: Introduktion till IP Tillåtelselista
description: Lär dig hur IP Tillåtelselista kan begränsa från vilka adresser användare kan få åtkomst till domäner i AEM as a Cloud Service.
exl-id: 352fae8e-d116-40b0-ba54-d7f001f076e8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 500e1b78fb9688601848fc17f312fc23be83bcb0
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---


# Introduktion till IP Tillåtelselista {#introduction}

Lär dig hur IP Tillåtelselista kan begränsa från vilka adresser användare kan få åtkomst till domäner i AEM as a Cloud Service.

>[!CONTEXTUALHELP]
>id="aemcloud_golive_ipallowlist"
>title="Hantera IP-Tillåtelselista"
>abstract="AEM as a Cloud Service är tillgängligt via Internet och skyddas genom användarautentisering och behörighet. Cloud Manager IP Tillåtelselista kan användas för att begränsa och styra åtkomsten enbart till betrodda IP-adresser. Cloud Manager-användare med lämplig behörighet kan skapa tillåtelselista med betrodda IP-adresser från vilka webbplatsens användare kan komma åt sina AEM-domäner."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/add-ip-allow-lists" text="Lägg till en IP-Tillåtelselista"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/managing-ip-allow-lists" text="Visa och uppdatera en IP-Tillåtelselista"

## Ökning {#overview}

AEM som molntjänst är som standard tillgängligt via Internet. Säkerhet hanteras genom användarautentisering och -auktorisering, men IP-registrering är ett sätt att begränsa åtkomsten enbart till betrodda IP-adresser.

Cloud Manager IP Tillåtelselista kan bara användas för att begränsa och styra åtkomsten till betrodda IP-adresser. Cloud Manager-användare med lämplig behörighet kan [skapa och lägga till IP-Tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md) med betrodda IP-adresser som webbplatsens användare kan komma åt sina AEM-domäner från.

När du har lagt till [IP-Tillåtelselista kan det användas eller tas bort ](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) flera gånger som en enhet eller entitet i en författartjänst, en utgivartjänst eller båda delarna, i en miljö.

>[!NOTE]
>
>Om IP Tillåtelselista inte används tillåts som standard alla IP-adresser. När ett IP-Tillåtelselista används tillåts inga IP-adresser förutom adresser på IP-Tillåtelselista.

## Begränsningar {#limitations}

Innan du använder IP Tillåtelselista bör du vara medveten om följande begränsningar vad gäller funktioner, användning och effekt på andra funktioner.

### Allmänna begränsningar för IP Tillåtelselista {#general}

* Högst 50 IP-Tillåtelselista kan läggas till i programmet.
* Högst 50 IP/CIDR-adresser kan läggas till i varje IP-Tillåtelselista.
* IP-Tillåtelselista-namn stöds i Cloud Manager för författartjänsten, eller publiceringstjänsten, eller båda, i en miljö.

### Front-End Pipelines och IP Tillåtelselista {#front-end-pipeline}

Om du använder, eller tänker använda, [front-end-pipeline för att utveckla webbplatser](/help/implementing/developing/introduction/developing-with-front-end-pipelines.md) måste följande Cloud Manager IP Tillåtelselista läggas till i förväg.

När du [lägger till IP-adressen Tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/add-ip-allow-lists.md#add-cm-allowlist), ger den namnet *`Cloud Manager`*, kopierar listan nedan och klistrar in dem i dialogrutan IP-Tillåtelselista.

```text
52.254.106.192/28
20.186.185.181
52.254.106.240/28
52.254.107.128/28
52.254.105.192/28
52.254.106.176/28
20.186.185.227
52.254.106.144/28
52.254.107.64/28
20.186.185.239
20.22.83.112
52.254.107.80/28
52.254.107.144/28
52.254.106.224/28
20.14.241.153
52.254.107.0/28
52.254.107.32/28
52.254.106.208/28
40.70.154.136/29
52.254.106.160/28
52.254.107.16/28
52.254.106.0/28
4.152.211.251
```

För att undvika avbrott i frontledningens körning bör du se till att detta Cloud Manager IP Tillåtelselista läggs till. Tillämpa sedan listan på redigeringsmiljön *innan* du aktiverar pipelinen.

Mer information finns i [Använd IP Tillåtelselista](/help/implementing/cloud-manager/ip-allow-lists/apply-allow-list.md) och [Aktivera frontendpipeline](/help/sites-cloud/administering/site-creation/enable-front-end-pipeline.md).

### Universal Editor och IP Tillåtelselista {#universal-editor}

{{ip-allow-lists-ue}}
