---
title: Föråldrade och borttagna funktioner
description: Versionsinformation om borttagna och borttagna funktioner i [!DNL Adobe Experience Manager] som [!DNL Cloud Service].
exl-id: ef082184-4eb7-49c7-8887-03d925e3da6f
source-git-commit: bbd8277fc5ed81bc656900ec3a993630aa5ffad5
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 5%

---

# Föråldrade och borttagna funktioner {#deprecated-and-removed-features}

>[!CONTEXTUALHELP]
>id="aem_cloud_deprecated_features"
>title="Föråldrade och borttagna funktioner i AEM as a Cloud Service"
>abstract="AEM as a Cloud Service har en distributionsmodell som bygger på molnet. Vissa funktioner har ersatts av molnbaserade motsvarigheter och på den här fliken visas dessa funktioner."


Adobe utvärderar ständigt produktfunktioner för att så småningom förnya eller ersätta äldre funktioner med modernare alternativ för att förbättra det totala kundvärdet, alltid med noggrant övervägande av bakåtkompatibilitet. Som [!DNL Adobe Experience Manager] som [!DNL Cloud Service] innehåller en distributionsmodell som bygger på molnet, och vissa funktioner har ersatts av molnbaserade motsvarigheter.

Att meddela att borttagning/ersättning av [!DNL Experience Manager] funktioner gäller följande regler:

1. Föråldringsanmälan kommer först. Föråldrade funktioner är fortfarande tillgängliga men har inte förbättrats ytterligare.
1. Funktioner som annonserats vara borttagna så snart som möjligt i den senare större versionen. Det faktiska måldatumet för borttagning tillkännages.

Den här processen ger kunderna minst en releasecykel för att anpassa implementeringen till en ny version eller en efterföljare till en borttagningsfunktion, innan den faktiska borttagningen.

## Borttagna funktioner {#deprecated-features}

I det här avsnittet visas funktioner som har markerats som inaktuella i [!DNL Experience Manager] som [!DNL Cloud Service]. Vanligtvis är funktioner som ska tas bort i en framtida version först inaktuella, med ett alternativ.

Kunderna rekommenderas att granska om de använder funktionen/funktionen i den aktuella distributionen och planera för att ändra implementeringen så att den använder det alternativ som erbjuds.

| Funktioner | Inaktuell funktion | Ersättning |
| ------------ | ------------------ | ----------- |
| [!DNL Sites] | Upplev fragmentegenskaper för **Status för sociala medier**. | Funktionen kommer snart att tas bort. |
| [!DNL Sites] | Mallbaserade enkla innehållsfragment. | [Modellbaserade strukturerade innehållsfragment](/help/assets/content-fragments/content-fragments-models.md) nu. |
| [!DNL Assets] | `DAM Asset Update` arbetsflöde för att bearbeta inkapslade bilder. | Tillgångsanvändning [tillgångsmikrotjänster](/help/assets/asset-microservices-overview.md) nu. |
| [!DNL Assets] | Överför resurser direkt till [!DNL Experience Manager]. Se [inaktuella API:er för överföring av resurser](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api). | Använd [Direkt binär överföring](/help/assets/add-assets.md). Mer teknisk information finns i [API:er för direktöverföring](/help/assets/developer-reference-material-apis.md#upload-binary). |
| [!DNL Assets] | [Vissa arbetsflödessteg](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps) in `DAM Asset Update` arbetsflödet stöds inte, inklusive anrop av kommandoradsverktyg som [!DNL ImageMagick]. | [Resursmikrotjänster](/help/assets/asset-microservices-overview.md) som ersätter många arbetsflöden. Använd [efterbehandlingsarbetsflöden](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows). |
| [!DNL Assets] | Konvertera videofilmer till mpeg. | Använd vid generering av miniatyrbilder för MPEG [Resursmikrotjänster](/help/assets/asset-microservices-overview.md). För MPEG-omkodning använder du [Dynamic Media](/help/assets/manage-video-assets.md). |
| [!DNL Foundation] | Gränssnitt för trädreplikering på fliken Distribuera i replikeringsagenten (borttagning efter 30 september 2021) | [Hantera publikation](/help/operations/replication.md#manage-publication) eller [arbetsflöde för publicera innehållsträd](/help/operations/replication.md#publish-content-tree-workflow) metoder |

## Borttagna funktioner {#removed-features}

I det här avsnittet visas funktioner som har tagits bort från [!DNL Experience Manager] med [!DNL Experience Manager] som [!DNL Cloud Service].

| Yta | Funktion | Ersättning |
| ------------ | ------------------ | ----------- |
| Användargränssnitt | Klassiskt användargränssnitt har tagits bort från produktanvändargränssnittet. Det finns ett fåtal klassiska användargränssnittsdialogrutor för vissa funktioner, som Länkkontroll, Rensa version och vissa Cloud Service. Kommande [produktuppdateringar](/help/release-notes/home.md) kan ta bort Classic UI-tillgängligheten ytterligare. | Standardgränssnitt |
| [!DNL Dynamic Media] | Tidigare integreringar med [Dynamic Media Classic](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/scene7.html#integration) och [Dynamic Media hybridläge](https://experienceleague.adobe.com/docs/experience-manager-65/assets/dynamic/config-dynamic.html#dynamic) är inte tillgängliga i [!DNL Experience Manager] som [!DNL Cloud Service]. | Använd [Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) tillhandahålls med [!DNL Experience Manager] som [!DNL Cloud Service]. |
| [!DNL Sites] | Portal Director och Portlet Component | Dessa funktioner har tagits bort i [!DNL Experience Manager] 6.4 och har nu tagits bort från [!DNL Experience Manager]. |
| [!DNL Sites] | Designimporteraren | Den här funktionen har tagits bort som oföränderliga avsnitt i [!DNL Experience Manager] databasen är inte tillgänglig vid körning. |
| [!DNL Assets] | [!DNL Assets] Det går inte att dela med Marketing Cloud Assets Core Service och Creative Cloud. | För integrering med [!DNL Adobe Creative Cloud], använda [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html). |
| [!DNL Foundation] | Stöd för Apache Sling-datakällor (OSGi bundle org.apache.sling.datasource) | Ej tillämpligt |
| [!DNL Foundation] | Stöd för JST-skriptmallar (OSGi bundle org.apache.sling.scripting.jst) | Ej tillämpligt |
| [!DNL Foundation] | Stöd för Apache Felix Http Whiteboard | OSGi Http Whiteboard |

## Java API {#java-api}

Se [den här sidan](/help/release-notes/deprecated-apis.md) för borttagna eller borttagna Java-API:er som ibland introduceras.

## OSGI-konfiguration {#osgi-configuration}

Se [den här artikeln](/help/implementing/deploying/osgi-configuration-api.md) för eventuella begränsningar av konfigureringen av OSGI-egenskaper, varav vissa kan införas över tiden.
