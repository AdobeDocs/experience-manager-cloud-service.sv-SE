---
title: Föråldrade och borttagna funktioner
description: Versionsinformation som är specifik för borttagna och borttagna funktioner i [!DNL Adobe Experience Manager] som en [!DNL Cloud Service].
exl-id: ef082184-4eb7-49c7-8887-03d925e3da6f
source-git-commit: 725cc82aa5794b53e5a43d95359fe1fd148b59ac
workflow-type: tm+mt
source-wordcount: '484'
ht-degree: 5%

---

# Inaktuella och borttagna funktioner {#deprecated-and-removed-features}

>[!CONTEXTUALHELP]
>id="aem_cloud_deprecated_features"
>title="Borttagna och borttagna funktioner i AEM som en Cloud Service"
>abstract="AEM som Cloud Service har en molnbaserad distributionsmodell. Vissa funktioner har ersatts av molnbaserade motsvarigheter och på den här fliken visas dessa funktioner."


Adobe utvärderar ständigt produktfunktioner för att så småningom förnya eller ersätta äldre funktioner med modernare alternativ för att förbättra det totala kundvärdet, alltid med noggrant övervägande av bakåtkompatibilitet. Eftersom [!DNL Adobe Experience Manager] som [!DNL Cloud Service] tillhandahåller en molnbaserad distributionsmodell ersattes vissa funktioner av molnbaserade motsvarigheter.

Följande regler gäller för att kommunicera den förestående borttagningen/ersättningen av [!DNL Experience Manager]-funktioner:

1. Föråldringsanmälan kommer först. Föråldrade funktioner är fortfarande tillgängliga men har inte förbättrats ytterligare.
1. Funktioner som annonserats vara borttagna så snart som möjligt i den senare större versionen. Det faktiska måldatumet för borttagning tillkännages.

Den här processen ger kunderna minst en releasecykel för att anpassa implementeringen till en ny version eller en efterföljare till en borttagningsfunktion, innan den faktiska borttagningen.

## Inaktuella funktioner {#deprecated-features}

I det här avsnittet visas funktioner som har markerats som borttagna i [!DNL Experience Manager] som [!DNL Cloud Service]. Vanligtvis är funktioner som ska tas bort i en framtida version först inaktuella, med ett alternativ.

Kunderna rekommenderas att granska om de använder funktionen/funktionen i den aktuella distributionen och planera för att ändra implementeringen så att den använder det alternativ som erbjuds.

| Funktioner | Inaktuell funktion | Ersättning |
| ------------ | ------------------ | ----------- |
| [!DNL Assets] | `DAM Asset Update` arbetsflöde för att bearbeta inkapslade bilder. | Tillgångsintaget använder [tillgångsmikrotjänster](/help/assets/asset-microservices-overview.md) nu. |
| [!DNL Assets] | Överför resurser direkt till [!DNL Experience Manager]. Se [API:er för inaktuell överföring av resurser](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api). | Använd [direkt binär överföring](/help/assets/add-assets.md). Mer teknisk information finns i [API:er för direkt överföring](/help/assets/developer-reference-material-apis.md#upload-binary). |
| [!DNL Assets] | [Vissa arbetsflödessteg ](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps) i  `DAM Asset Update` arbetsflödet stöds inte, inklusive anrop av kommandoradsverktyg som ImageMagick. | [Resursmikrotjänster ](/help/assets/asset-microservices-overview.md) ersätter många arbetsflöden. Använd [efterbearbetningsarbetsflöden](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) för anpassad bearbetning. |
| [!DNL Assets] | Konvertera videofilmer till mpeg. | Använd [Resursmikrotjänster](/help/assets/asset-microservices-overview.md) för att generera miniatyrbilder för MPEG. Använd [Dynamic Media](/help/assets/manage-video-assets.md) för MPEG-omkodning. |

## Borttagna funktioner {#removed-features}

I det här avsnittet visas funktioner som har tagits bort från [!DNL Experience Manager] med [!DNL Experience Manager] som [!DNL Cloud Service].

| Yta | Funktion | Ersättning |
| ------------ | ------------------ | ----------- |
| Användargränssnitt | Klassiskt användargränssnitt har tagits bort från produktanvändargränssnittet. Det finns ett fåtal klassiska användargränssnittsdialogrutor för vissa funktioner, som Länkkontroll, Rensa version och vissa Cloud Service. Kommande [produktuppdateringar](/help/release-notes/home.md) kan ta bort tillgängligheten för Classic UI ytterligare. | Standardgränssnitt |
| [!DNL Dynamic Media] | Tidigare integreringar med [Dynamic Media Classic](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/scene7.html#integration) och [Dynamic Media hybridläge](https://experienceleague.adobe.com/docs/experience-manager-65/assets/dynamic/config-dynamic.html#dynamic) är inte tillgängliga i [!DNL Experience Manager] som [!DNL Cloud Service]. | Använd [Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) som medföljer [!DNL Experience Manager] som [!DNL Cloud Service]. |
| [!DNL Sites] | Portal Director och Portlet Component | Dessa funktioner har tagits bort i [!DNL Experience Manager] 6.4 och har nu tagits bort från [!DNL Experience Manager]. |
| [!DNL Sites] | Designimporteraren | Den här funktionen har tagits bort eftersom oföränderliga avsnitt i [!DNL Experience Manager]-databasen inte är tillgängliga vid körning. |
| [!DNL Assets] | [!DNL Assets] Det går inte att dela med Marketing Cloud Assets Core Service och Creative Cloud. | Använd [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) för integrering med [!DNL Adobe Creative Cloud]. |
