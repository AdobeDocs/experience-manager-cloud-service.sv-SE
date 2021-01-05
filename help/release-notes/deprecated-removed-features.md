---
title: Föråldrade och borttagna funktioner
description: Versionsinformation som är specifik för borttagna och borttagna funktioner i Adobe Experience Manager som Cloud Service.
translation-type: tm+mt
source-git-commit: e31ac0c2d28f60d7b98036c16f154a09da51d6bf
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 9%

---


# Inaktuella och borttagna funktioner {#deprecated-and-removed-features}

Adobe utvärderar ständigt produktfunktioner för att så småningom förnya eller ersätta äldre funktioner med modernare alternativ för att förbättra det totala kundvärdet, alltid med noggrant övervägande av bakåtkompatibilitet. Eftersom Adobe Experience Manager som Cloud Service erbjuder en molnbaserad distributionsmodell ersattes dessutom vissa funktioner av molnbaserade motsvarigheter.

Följande regler gäller för att informera om den förestående borttagningen/ersättningen av AEM:

1. Föråldringsanmälan kommer först. Föråldrade funktioner är fortfarande tillgängliga men har inte förbättrats ytterligare.
1. Funktioner som annonserats vara borttagna så snart som möjligt i den senare större versionen. Det faktiska måldatumet för borttagning tillkännages.

Den här processen ger kunderna minst en releasecykel för att anpassa implementeringen till en ny version eller en efterföljare till en borttagningsfunktion, innan den faktiska borttagningen.

## Inaktuella funktioner {#deprecated-features}

I det här avsnittet listas funktioner som har markerats som borttagna i Experience Manager som en Cloud Service. Vanligtvis är funktioner som ska tas bort i en framtida version först inaktuella, med ett alternativ.

Kunderna rekommenderas att granska om de använder funktionen/funktionen i den aktuella distributionen och planera för att ändra implementeringen så att den använder det alternativ som finns.

| Funktioner | Inaktuell funktion | Ersättning |
| ------------ | ------------------ | ----------- |
| Assets | `DAM Asset Update` arbetsflöde för att bearbeta inkapslade bilder. | Tillgångsintaget använder [tillgångsmikrotjänster](/help/assets/asset-microservices-overview.md) nu. |
| Resurser | Överför resurser direkt till AEM. Se [API:er för inaktuell överföring av resurser](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api). | Använd [direkt binär överföring](/help/assets/add-assets.md). Mer teknisk information finns i [API:er för direkt överföring](/help/assets/developer-reference-material-apis.md#upload-binary). |
| Resurser | [Vissa arbetsflödessteg ](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps) i  `DAM Asset Update` arbetsflödet stöds inte, inklusive anrop av kommandoradsverktyg som ImageMagick. | [Resursmikrotjänster ](/help/assets/asset-microservices-overview.md) ersätter många arbetsflöden. Använd [efterbearbetningsarbetsflöden](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) för anpassad bearbetning. |
| Resurser | Konvertera videofilmer till mpeg. | Använd [Resursmikrotjänster](/help/assets/asset-microservices-overview.md) för att generera miniatyrbilder för MPEG. Använd [Dynamic Media](/help/assets/manage-video-assets.md) för MPEG-omkodning. |

## Borttagna funktioner {#removed-features}

I det här avsnittet visas funktioner som har tagits bort från AEM med Experience Manager som Cloud Service.

| Yta | Funktion | Ersättning |
| ------------ | ------------------ | ----------- |
| UI | En del klassiska användargränssnittsdialogrutor finns för närvarande kvar för vissa funktioner, som Länkkontroll, Rensa Cloud Service och vissa användarkonfigurationer, men åtkomst till det klassiska användargränssnittet i allmänhet har tagits bort i AEM produktgränssnitt. | Standardgränssnitt |
| Dynamic Media | Tidigare integreringar med [Dynamic Media Classic](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/scene7.html#integration) och [Dynamic Media hybridläge](https://experienceleague.adobe.com/docs/experience-manager-65/assets/dynamic/config-dynamic.html#dynamic) är inte tillgängliga i AEM som Cloud Service. | Använd [Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) som ingår i Experience Manager as a Cloud Service. |
| Sites | Portal Director och Portlet Component | Dessa funktioner har tagits bort i AEM 6.4 och har nu tagits bort från AEM. |
| Webbplatser | Designimporteraren | Den här funktionen har tagits bort eftersom oföränderliga avsnitt i AEM inte är tillgängliga vid körning. |
| Resurser | [AEM Assets-delning med Marketing Cloud Assets Core Service och Creative Cloud ](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/configure-assets-cc-integration.html) service är inte tillgängligt. | Använd [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) för integrering med Creative Cloud. |
