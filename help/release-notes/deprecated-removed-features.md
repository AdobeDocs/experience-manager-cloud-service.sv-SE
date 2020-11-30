---
title: Föråldrade och borttagna funktioner
description: Versionsinformation som är specifik för borttagna och borttagna funktioner i Adobe Experience Manager som Cloud Service.
translation-type: tm+mt
source-git-commit: 0a9a462f1b92a0dcb712163574bbf57582f8145c
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 16%

---


# Föråldrade och borttagna funktioner {#deprecated-and-removed-features}

Adobe utvärderar ständigt produktfunktioner för att så småningom förnya eller ersätta äldre funktioner med modernare alternativ för att förbättra det totala kundvärdet, alltid med noggrant övervägande av bakåtkompatibilitet. Eftersom Adobe Experience Manager som Cloud Service erbjuder en molnbaserad distributionsmodell ersattes dessutom vissa funktioner av molnbaserade motsvarigheter.

Följande regler gäller för att informera om den förestående borttagningen/ersättningen av AEM:

1. Föråldringsanmälan kommer först. Föråldrade funktioner är fortfarande tillgängliga men har inte förbättrats ytterligare.
1. Funktioner som annonserats vara borttagna så snart som möjligt i den senare större versionen. Det faktiska måldatumet för borttagning tillkännages.

Den här processen ger kunderna minst en releasecykel för att anpassa implementeringen till en ny version eller en efterföljare till en borttagningsfunktion, innan den faktiska borttagningen.

## Deprecated features {#deprecated-features}

I det här avsnittet listas funktioner som har markerats som borttagna i Experience Manager som en Cloud Service. Vanligtvis är funktioner som ska tas bort i en framtida version först inaktuella, med ett alternativ.

Kunderna rekommenderas att granska om de använder funktionen/funktionen i den aktuella distributionen och planera för att ändra implementeringen så att den använder det alternativ som finns.

| Funktioner | Inaktuell funktion | Ersättning |
| ------------ | ------------------ | ----------- |
| Assets | `DAM Asset Update` arbetsflöde för att bearbeta inkapslade bilder. | Tillgångsintaget använder [tillgångsmikrotjänster](/help/assets/asset-microservices-overview.md) nu. |
| Assets | Överför resurser direkt till AEM. Se [inaktuella API:er för överföring av resurser](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api). | Använd [direkt binär överföring](/help/assets/add-assets.md). Mer teknisk information finns i API:er för [direktöverföring](/help/assets/developer-reference-material-apis.md#upload-binary). |
| Assets | [Vissa arbetsflödessteg](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps) i `DAM Asset Update` arbetsflödet stöds inte, inklusive anrop av kommandoradsverktyg som ImageMagick. | [Resursmikrotjänster](/help/assets/asset-microservices-overview.md) ersätter många arbetsflöden. Använd [efterbearbetningsarbetsflöden](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows)för anpassad bearbetning. |
| Assets | Konvertera videofilmer till mpeg. | Använd [Resursmikrotjänster](/help/assets/asset-microservices-overview.md)för att skapa miniatyrbilder förMPEG. Använd [Dynamic Media](/help/assets/manage-video-assets.md)för MPEG-omkodning. |

## Borttagna funktioner {#removed-features}

I det här avsnittet visas funktioner som har tagits bort från AEM med Experience Manager som Cloud Service.

| Yta | Funktion | Ersättning |
| ------------ | ------------------ | ----------- |
| UI | En del klassiska användargränssnittsdialogrutor finns för närvarande kvar för vissa funktioner, som Länkkontroll, Rensa Cloud Service och vissa användarkonfigurationer, men åtkomst till det klassiska användargränssnittet i allmänhet har tagits bort i AEM produktgränssnitt. | Standardgränssnitt |
| Dynamic Media | Tidigare integreringar med [Dynamic Media Classic (Scene7)](https://helpx.adobe.com/se/experience-manager/6-5/sites/administering/using/scene7.html) och [Dynamic Media-hybridläge](https://helpx.adobe.com/se/experience-manager/6-5/assets/using/config-dynamic.html) är inte tillgängliga i AEM as a Cloud Service. | Använd [Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) som ingår i Experience Manager as a Cloud Service. |
| Sites | Portal Director och Portlet Component | Dessa funktioner har tagits bort i AEM 6.4 och har nu tagits bort från AEM. |
| Sites | Designimporteraren | Den här funktionen har tagits bort eftersom oföränderliga avsnitt i AEM inte är tillgängliga vid körning. |
| Assets | [AEM Assets-delning med Marketing Cloud Assets Core Service och Creative Cloud](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/configure-assets-cc-integration.html) är inte tillgängligt. | Om du vill integrera med Creative Cloud använder du [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html). |
