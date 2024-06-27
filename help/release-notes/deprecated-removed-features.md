---
title: Föråldrade och borttagna funktioner
description: Versionsinformation om borttagna och borttagna funktioner i [!DNL Adobe Experience Manager] som [!DNL Cloud Service].
exl-id: ef082184-4eb7-49c7-8887-03d925e3da6f
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '2193'
ht-degree: 0%

---

# Föråldrade och borttagna funktioner och API:er {#deprecated-and-removed-features-apis}

>[!CONTEXTUALHELP]
>id="aem_cloud_deprecated_features"
>title="Borttagna funktioner i AEM as a Cloud Service"
>abstract="AEM as a Cloud Service har en distributionsmodell som bygger på molnet. Vissa funktioner har ersatts av molnbaserade motsvarigheter och på den här fliken visas dessa funktioner."


Adobe utvärderar ständigt produktfunktioner och kan med tiden förnya eller ersätta äldre funktioner med modernare alternativ för att förbättra det totala kundvärdet, alltid under noggrant övervägande av bakåtkompatibilitet. Som [!DNL Adobe Experience Manager] som [!DNL Cloud Service] innehåller en distributionsmodell som bygger på molnet, och vissa funktioner har ersatts av molnbaserade motsvarigheter.

Att informera om den förestående borttagningen/ersättningen av [!DNL Experience Manager] funktioner gäller följande regler:

1. Föråldringsanmälan kommer först. Föråldrade funktioner är fortfarande tillgängliga men har inte förbättrats ytterligare.
1. Funktioner som annonserats vara borttagna så snart som möjligt i den senare större versionen. Det faktiska måldatumet för borttagning tillkännages.

Den här processen ger kunderna minst en releasecykel för att anpassa implementeringen till en ny version eller en efterföljare till en borttagningsfunktion, innan den faktiska borttagningen.

## Föråldrade funktioner {#deprecated-features}

I det här avsnittet visas funktioner som har markerats som inaktuella i [!DNL Experience Manager] som [!DNL Cloud Service]. Vanligtvis är funktioner som ska tas bort i en framtida version först inaktuella, med ett alternativ.

Kunderna rekommenderas att granska om de använder funktionen/funktionen i den aktuella distributionen och planera för att ändra implementeringen så att den använder det alternativ som erbjuds.

| Funktioner | Inaktuell funktion | Ersättning |
| ------------ | ------------------ | ----------- |
| [!DNL Sites] | Upplev fragmentegenskaper för **Status för sociala medier**. | Funktionen tas bort snart. |
| [!DNL Sites] | Mallbaserade enkla innehållsfragment. | [Modellbaserade strukturerade innehållsfragment](/help/assets/content-fragments/content-fragments-models.md) nu. |
| [!DNL Assets] | `DAM Asset Update` arbetsflöde för att bearbeta inkapslade bilder. | Tillgångsanvändning [tillgångsmikrotjänster](/help/assets/asset-microservices-overview.md) nu. |
| [!DNL Assets] | Överför resurser direkt till [!DNL Experience Manager]. Se [inaktuella API:er för överföring av resurser](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api). | Använd [Direkt binär överföring](/help/assets/add-assets.md). Mer teknisk information finns i [API:er för direktöverföring](/help/assets/developer-reference-material-apis.md#upload-binary). |
| [!DNL Assets] | [Vissa arbetsflödessteg](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps) in `DAM Asset Update` arbetsflödet stöds inte, inklusive anrop av kommandoradsverktyg som [!DNL ImageMagick]. | [Resursmikrotjänster](/help/assets/asset-microservices-overview.md) som ersätter många arbetsflöden. Använd [efterbehandlingsarbetsflöden](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows). |
| [!DNL Assets] | Konvertera videofilmer till mpeg. | Använd för att skapa miniatyrbilder av FFmpeg [Resursmikrotjänster](/help/assets/asset-microservices-overview.md). För MPEG-omkodning använder du [Dynamic Media](/help/assets/manage-video-assets.md). |
| [!DNL Foundation] | Gränssnitt för trädreplikering på fliken Distribuera i replikeringsagenten (borttagning efter 30 september 2021) | [Hantera publikation](/help/operations/replication.md#manage-publication) eller [arbetsflöde för publicera innehållsträd](/help/operations/replication.md#publish-content-tree-workflow) metoder |
| [!DNL Foundation] | Varken fliken Distribuera på administrationsskärmen för replikeringsagenten eller replikerings-API:t kan användas för att replikera innehållspaket över 10 MB. Använd antingen [Hantera publikation](/help/operations/replication.md#manage-publication) eller [arbetsflöde för publicera innehållsträd](/help/operations/replication.md#publish-content-tree-workflow) |
| [!DNL Foundation] | Integreringar som använder inloggningsuppgifter som genererats från Adobe Developer Console-projekt förlorar gradvis stöd för JWT-autentiseringsuppgifter (Service Account). Det går inte att skapa nya JWT-autentiseringsuppgifter i Adobe Developer Console den 1 maj 2024 eller senare, även om befintliga JWT-autentiseringsuppgifter fortfarande kan användas för redan konfigurerade integreringar fram till 1 januari 2025, då befintliga JWT-autentiseringsuppgifter inte längre fungerar och kunderna måste migrera till OAuth Server-till-Server-autentiseringsuppgifter. [Läs mer](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console). | [Migrera](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview) till autentiseringsuppgifter för OAuth Server-till-Server. |

## Borttagna funktioner {#removed-features}

I det här avsnittet visas funktioner som har tagits bort från [!DNL Experience Manager] med [!DNL Experience Manager] som [!DNL Cloud Service].

| Område | Funktion | Ersättning | Borttagningsdatum för mål |
| ------------ | ------------------ | ----------- | ------------------- |
| Användargränssnitt | Klassiskt användargränssnitt har tagits bort från produktanvändargränssnittet. Det finns ett fåtal klassiska användargränssnittsdialogrutor för vissa funktioner, som Länkkontroll, Rensa version och vissa Cloud Service. Kommande [produktuppdateringar](/help/release-notes/home.md) kan ta bort Classic UI-tillgängligheten ytterligare. | Standardgränssnitt | Borttagen |
| [!DNL Dynamic Media] | Tidigare integreringar med [Dynamic Media Classic](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/scene7.html#integration) och [Dynamic Media hybridläge](https://experienceleague.adobe.com/docs/experience-manager-65/assets/dynamic/config-dynamic.html#dynamic) är inte tillgängliga i [!DNL Experience Manager] som [!DNL Cloud Service]. | Använd [Dynamic Media](/help/assets/dynamic-media/dynamic-media.md) tillhandahålls med [!DNL Experience Manager] som [!DNL Cloud Service]. | Borttagen |
| [!DNL Sites] | Portal Director och Portlet Component | Dessa funktioner har tagits bort i [!DNL Experience Manager] 6.4 och har nu tagits bort från [!DNL Experience Manager]. | Borttagen |
| [!DNL Sites] | Designimporteraren | Den här funktionen har tagits bort som oföränderliga avsnitt i [!DNL Experience Manager] databasen är inte tillgänglig vid körning. | Borttagen |
| [!DNL Assets] | [!DNL Assets] Det går inte att dela med Marketing Cloud Assets Core Service och Creative Cloud. | För integrering med [!DNL Adobe Creative Cloud], använda [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html). | Borttagen |
| [!DNL Foundation] | Stöd för Apache Sling-datakällor (OSGi bundle org.apache.sling.datasource) | Ej tillämpligt | Borttagen |
| [!DNL Foundation] | Stöd för JST-skriptmallar (OSGi bundle org.apache.sling.scripting.jst) | Ej tillämpligt | Borttagen |
| [!DNL Foundation] | Stöd för Apache Felix Http Whiteboard | OSGi Http Whiteboard | Mars 2022 |
| [!DNL Foundation] | Stöd för com.adobe.granite.oauth.server | Integrering med Adobe IMS | Mars 2023 |
| [!DNL Foundation] | Stöd för org.apache.sling.servicusermapping-funktion till [hämta användar-ID för tjänsten](https://sling.apache.org/apidocs/sling12/org/apache/sling/serviceusermapping/ServiceUserMapper.html#getServiceUserID-org.osgi.framework.Bundle-java.lang.String-) | Ej tillämpligt | 8/30/24 |


## AEM API:er {#aem-apis}

Nedan finns en omfattande lista över borttagna AEM-API:er och deras förväntade borttagningsdatum. Kunder förväntas ta bort API:erna vid målborttagningsdatumet från sin kod. Om API:t används efter borttagningsdatumet genereras fel i den lokala SDK/Development Environment och Cloud Manager byggprocess.

<details>
  <summary>Expandera om du vill visa en lista över inaktuella API:er.</summary>
<table style="table-layout:auto">
  <tr>
    <th>Paket/klass</th>
    <th>Kommentar</th>
    <th>Inaktuellt datum</th>
    <th>Borttagningsdatum för mål</th>
  </tr>
<tbody>
  <tr>
    <td>org.apache.sling.commons.auth<br>org.apache.sling.commons.auth.spi</td>
    <td>Använd Sling:s gränssnitt Auth Core/Auth Core SPI som ett alternativ</td>
    <td>2015</td>
    <td>7/30/21</td>
  </tr>
  <tr>
    <td>org.apache.sling.runmode</td>
    <td></td>
    <td>2015</td>
    <td>7/30/21</td>
  </tr>
  <tr>
    <td>com.day.cq.jcrclustersupport</td>
    <td>Använd Sling Discovery API som ett alternativ</td>
    <td>2015</td>
    <td>borttagen</td>
  </tr>
  <tr>
    <td>org.apache.sling.settings</td>
    <td>AEM as a Cloud Service stöder inte körningslägen eller filsystemsåtkomst vid körning. </td>
    <td>10/5/20</td>
    <td>I slutet av 2021</td>
  </tr>
  <tr>
    <td>org.apache.fop.apps</td>
    <td></td>
    <td>3/1/21</td>
    <td>borttagen</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.vault.util.xml.xerces.dom<br>org.apache.jackrabbit.vault.util.xml.xerces.util<br>org.apache.jackrabbit.vault.util.xml.xerces.xni<br>org.apache.jackrabbit.vault.util.xml.xerces.xni.parser</td>
    <td></td>
    <td>3/5/21</td>
    <td>borttagen</td>
  </tr>
  <tr>
    <td>org.json</td>
    <td>Apache Johnzons implementering av <a href="https://johnzon.apache.org/index.html">javax.json</a> rekommenderas och bör användas. </td>
    <td>4/30/21</td>
    <td>12/31/21</td>
  </tr>
  <tr>
    <td>org.apache.felix.cm<br>org.apache.felix.cm.file</td>
    <td>Anpassade beständiga hanterare stöds inte i AEM as a Cloud Service.</td>
    <td>4/30/21</td>
    <td>borttagen</td>
  </tr>
  <tr>
    <td>org.apache.commons.lang<br>org.apache.commons.lang.enums<br>org.apache.commons.lang.builder<br>org.apache.commons.lang.exception<br>org.apache.commons.lang.math<br>org.apache.commons.lang.mutable<br>org.apache.commons.lang.reflect<br>org.apache.commons.lang.text<br>org.apache.commons.lang.time</td>
    <td>Commons Lang 2 är i underhållsläge. Kommandon Lang 3 bör användas i stället.</td>
    <td>4/30/21</td>
    <td>12/31/21</td>
  </tr>
  <tr>
    <td>org.apache.commons.collections<br>org.apache.commons.collections.bag<br>org.apache.commons.collections.bidimap<br>org.apache.commons.collections.buffer<br>org.apache.commons.collections.collection<br>org.apache.commons.collections.comparators<br>org.apache.commons.collections.functors<br>org.apache.commons.collections.iterators<br>org.apache.commons.collections.keyvalue<br>org.apache.commons.collections.list<br>org.apache.commons.collections.map<br>org.apache.commons.collections.set</td>
    <td>Commons Collections 3 är i underhållsläge. Commons Collections 4 ska användas i stället.</td>
    <td>4/30/21</td>
    <td>12/31/21</td>
  </tr>
  <tr>
    <td>org.apache.felix.systemready</td>
    <td>Du bör använda API:t Apache Felix HealthCheck i stället</td>
    <td>4/30/21</td>
    <td>borttagen</td>
  </tr>
  <tr>
    <td>org.apache.felix.webconsole<br>org.apache.felix.webconsole.bundleinfo<br>org.apache.felix.webconsole.i18n</td>
    <td>Felix webbkonsol stöds inte i molnmiljöer</td>
    <td>4/30/21</td>
    <td>7/30/21</td>
  </tr>
  <tr>
    <td>org.apache.felix.http.jetty<br>org.eclipse.jetty.http<br>org.eclipse.jetty.http.pathmap<br>org.eclipse.jetty.io<br>org.eclipse.jetty.io.ssl<br>org.eclipse.jetty.jmx<br>org.eclipse.jetty.security<br>org.eclipse.jetty.server<br>org.eclipse.jetty.server.handler<br>org.eclipse.jetty.server.handler.gzip<br>org.eclipse.jetty.server.handler.jmx<br>org.eclipse.jetty.server.jmx<br>org.eclipse.jetty.server.nio<br>org.eclipse.jetty.server.session<br>org.eclipse.jetty.servlet<br>org.eclipse.jetty.servlet.jmx<br>org.eclipse.jetty.servlet.listener<br>org.eclipse.jetty.util<br>org.eclipse.jetty.util.annotation<br>org.eclipse.jetty.util.component<br>org.eclipse.jetty.util.log<br>org.eclipse.jetty.util.preventers<br>org.eclipse.jetty.util.resource<br>org.eclipse.jetty.util.security<br>org.eclipse.jetty.util.ssl<br>org.eclipse.jetty.util.statistic<br>org.eclipse.jetty.util.thread<br>org.eclipse.jetty.util.thread.strategy<br>org.eclipse.jetty.webapp<br>org.eclipse.jetty.websocket.api<br>org.eclipse.jetty.websocket.api.annotations<br>org.eclipse.jetty.websocket.api.extensions<br>org.eclipse.jetty.websocket.api.util<br>org.eclipse.jetty.websocket.client<br>org.eclipse.jetty.websocket.client.io<br>org.eclipse.jetty.websocket.client.masks<br>org.eclipse.jetty.websocket.common<br>org.eclipse.jetty.websocket.common.events<br>org.eclipse.jetty.websocket.common.events.annotated<br>org.eclipse.jetty.websocket.common.extensions<br>org.eclipse.jetty.websocket.common.extensions.compress<br>org.eclipse.jetty.websocket.common.extensions.fragment<br>org.eclipse.jetty.websocket.common.extensions.identity<br>org.eclipse.jetty.websocket.common.frames<br>org.eclipse.jetty.websocket.common.io<br>org.eclipse.jetty.websocket.common.io.http<br>org.eclipse.jetty.websocket.common.io.payload<br>org.eclipse.jetty.websocket.common.message<br>org.eclipse.jetty.websocket.common.scopes<br>org.eclipse.jetty.websocket.common.util<br>org.eclipse.jetty.websocket.server<br>org.eclipse.jetty.websocket.server.pathmap<br>org.eclipse.jetty.websocket.servlet<br>org.eclipse.jetty.xml<br>org.eclipse.jetty.client<br>org.eclipse.jetty.client.api<br>org.eclipse.jetty.client.http<br>org.eclipse.jetty.client.jmx<br>org.eclipse.jetty.client.util</td>
    <td>Paketen Eclipse Jetty och Felix Http Jetty stöds inte längre.</td>
    <td>5/27/21</td>
    <td>8/26/21</td>
  </tr>
  <tr>
    <td>com.mongodb<br>com.mongodb.annotations<br>com.mongodb.assertions<br>com.mongodb.async<br>com.mongodb.binding<br>com.mongodb.bulk<br>com.mongodb.client<br>com.mongodb.client.gridfs<br>com.mongodb.client.gridfs.codecs<br>com.mongodb.client.gridfs.model<br>com.mongodb.client.jndi<br>com.mongodb.client.model<br>com.mongodb.client.model.changestream<br>com.mongodb.client.model.geojson<br>com.mongodb.client.model.geojson.codecs<br>com.mongodb.client.result<br>com.mongodb.connection<br>com.mongodb.connection.netty<br>com.mongodb.diagnostics.logging<br>com.mongodb.event<br>com.mongodb.gridfs<br>com.mongodb.internal<br>com.mongodb.internal.async<br>com.mongodb.internal.authentication<br>com.mongodb.internal.connection<br>com.mongodb.internal.dns<br>com.mongodb.internal.event<br>com.mongodb.internal.management.jmx<br>com.mongodb.internal.session<br>com.mongodb.internal.thread<br>com.mongodb.internal.validator<br>com.mongodb.management<br>com.mongodb.operation<br>com.mongodb.selector<br>com.mongodb.session<br>com.mongodb.util</td>
    <td>Användning av detta API stöds inte i AEM as a Cloud Service.</td>
    <td>5/27/21</td>
    <td>7/30/21</td>
  </tr>
  <tr>
    <td>org.apache.felix.metatype<br>org.apache.felix.scr<br>org.apache.felix.scr.info<br>org.apache.felix.scr.component</td>
    <td>Apache Felix-metatypen och SCR-API:erna är föråldrade.  Använd OSGi-metatypen och deklarativa tjänstens API:er i stället.</td>
    <td>5/27/21</td>
    <td>borttagen</td>
  </tr>
  <tr>
    <td>org.slf4j.impl</td>
    <td>Loggimplementeringsklasser är inte kompatibla med AEM as a Cloud Service.</td>
    <td>7/4/21</td>
    <td>borttagen</td>
  </tr>
  <tr>
    <td>org.apache.abdera<br>org.apache.abdera.model<br>org.apache.abdera.factory<br>org.apache.abdera.ext.media<br>org.apache.abdera.util<br>org.apache.abdera.i18n.iri<br>org.apache.abdera.writer<br>org.apache.abdera.i18n.rfc4646<br>org.apache.abdera.i18n.rfc4646.enums<br>org.apache.abdera.i18n.text<br>org.apache.abdera.filter<br>org.apache.abdera.xpath<br>org.apache.abdera.i18n.text.io<br>org.apache.abdera.i18n.text.data<br>org.apache.abdera.parser</td>
    <td>API:t används inte eftersom Apache Abdera är ett projekt som har gått tillbaka sedan 2017.</td>
    <td>7/29/21</td>
    <td>09/29/21</td>
  </tr>
  <tr>
    <td>org.apache.abdera.ext.opensearch<br>org.apache.abdera.ext.opensearch.model<br>org.apache.abdera.ext.opensearch.server<br>org.apache.abdera.ext.opensearch.server.impl<br>org.apache.abdera.ext.opensearch.server.processors<br>org.apache.abdera.i18n.iri.data<br>org.apache.abdera.i18n.lang<br>org.apache.abdera.i18n.templates<br>org.apache.abdera.i18n.unicode.data<br>org.apache.abdera.parser.stax<br>org.apache.abdera.parser.stax.util<br>org.apache.abdera.protocol<br>org.apache.abdera.protocol.client<br>org.apache.abdera.protocol.client.cache<br>org.apache.abdera.protocol.client.util<br>org.apache.abdera.protocol.error<br>org.apache.abdera.protocol.server<br>org.apache.abdera.protocol.server.context<br>org.apache.abdera.protocol.server.filters<br>org.apache.abdera.protocol.server.impl<br>org.apache.abdera.protocol.server.multipart<br>org.apache.abdera.protocol.server.processors<br>org.apache.abdera.protocol.server.provider.basic<br>org.apache.abdera.protocol.server.provider.managed<br>org.apache.abdera.protocol.server.servlet<br>org.apache.abdera.protocol.util<br>org.apache.abdera.util.filter</td>
    <td>API:t används inte eftersom Apache Abdera är ett projekt som har gått tillbaka sedan 2017.</td>
    <td>4/8/19</td>
    <td>09/29/21</td>
  </tr>
  <tr>
    <td>org.apache.sling.startupfilter<br>com.adobe.granite.crypto.spi<br>com.adobe.granite.crpyto.spi.base<br>com.adobe.agl.impl.data.icudt40b<br>com.adobe.agl.impl.data.icudt40b.brkitr<br>com.adobe.agl.impl.data.icudt40b.coll<br>com.adobe.agl.impl.data.icudt40b.rbnf<br>com.<br>adobe.agl.impl.data.icudt40b.translit<br>com.adobe.internal.pdf.tika<br>com.adobe.internal.pdftoolkit.color<br>com.adobe.internal.pdftoolkit.core.encryption<br>com.adobe.internal.pdftoolkit.core.encryption.impl<br>com.adobe.internal.pdftoolkit.core.traverser<br>com.adobe.internal.pdftoolkit.graphicsDOM<br>com.adobe.internal.pdftoolkit.graphicsDOM.shading<br>com.adobe.internal.pdftoolkit.graphicsDOM.utils<br>com.adobe.internal.pdftoolkit.image<br>com.adobe.internal.pdftoolkit.pdf.content<br>com.adobe.internal.pdftoolkit.pdf.content.processor<br>com.adobe.internal.pdftoolkit.pdf.content.processor.base14fontwidths<br>com.adobe.internal.pdftoolkit.pdf.contentmodify<br>com.adobe.internal.pdftoolkit.pdf.contentmodify.impl<br>com.adobe.internal.pdftoolkit.pdf.digsig<br>com.adobe.internal.pdftoolkit.pdf.document<br>com.adobe.internal.pdftoolkit.pdf.document.listener<br>com.adobe.internal.pdftoolkit.pdf.document.permissionhandlers<br>com.adobe.internal.pdftoolkit.pdf.filters<br>com.adobe.internal.pdftoolkit.pdf.graphics<br>com.adobe.internal.pdftoolkit.pdf.graphics.colorspaces<br>com.adobe.internal.pdftoolkit.pdf.graphics.colorspaces.cmykresources<br>com.adobe.internal.pdftoolkit.pdf.graphics.font<br>com.adobe.internal.pdftoolkit.pdf.graphics.font.encodings<br>com.adobe.internal.pdftoolkit.pdf.graphics.font.impl<br>com.adobe.internal.pdftoolkit.pdf.graphics.impl<br>com.adobe.internal.pdftoolkit.pdf.graphics.optionalcontent<br>com.adobe.internal.pdftoolkit.pdf.graphics.patterns<br>com.adobe.internal.pdftoolkit.pdf.graphics.shading<br>com.adobe.internal.pdftoolkit.pdf.graphics.xobject<br>com.adobe.internal.pdftoolkit.pdf.impl<br>com.adobe.internal.pdftoolkit.pdf.inlineimage<br>com.adobe.internal.pdftoolkit.pdf.interactive<br>com.adobe.internal.pdftoolkit.pdf.interactive.action<br>com.adobe.internal.pdftoolkit.pdf.interactive.annotation<br>com.adobe.internal.pdftoolkit.pdf.interactive.forms<br>com.adobe.internal.pdftoolkit.pdf.interactive.forms.impl<br>com.adobe.internal.pdftoolkit.pdf.interactive.geospatial<br>com.adobe.internal.pdftoolkit.pdf.interactive.markedcontent<br>com.adobe.internal.pdftoolkit.pdf.interactive.navigation<br>com.adobe.internal.pdftoolkit.pdf.interactive.navigation.collection<br>com.adobe.internal.pdftoolkit.pdf.interactive.readerrequirements<br>com.adobe.internal.pdftoolkit.pdf.interactive.requirement<br>com.adobe.internal.pdftoolkit.pdf.interchange<br>com.adobe.internal.pdftoolkit.pdf.interchange.documentparts<br>com.adobe.internal.pdftoolkit.pdf.interchange.metadata<br>com.adobe.internal.pdftoolkit.pdf.interchange.prepress<br>com.adobe.internal.pdftoolkit.pdf.interchange.structure<br>com.adobe.internal.pdftoolkit.pdf.multimedia<br>com.adobe.internal.pdftoolkit.pdf.page<br>com.adobe.internal.pdftoolkit.pdf.rendering<br>com.adobe.internal.pdftoolkit.pdf.transparency<br>com.adobe.internal.pdftoolkit.pdf.utils<br>com.adobe.internal.pdftoolkit.services.Jpeg2000<br>com.adobe.internal.pdftoolkit.services.fontresources<br>com.adobe.internal.pdftoolkit.services.fontresources.subsetting<br>com.adobe.internal.pdftoolkit.services.interchange.structure<br>com.adobe.internal.pdftoolkit.services.optionalcontent<br>com.adobe.internal.pdftoolkit.services.optionalcontent.impl<br>com.adobe.internal.pdftoolkit.services.pdfParser<br>com.adobe.internal.pdftoolkit.services.permissions<br>com.adobe.internal.pdftoolkit.services.rasterizer<br>com.adobe.internal.pdftoolkit.services.readingorder<br>com.adobe.internal.pdftoolkit.services.security<br>com.adobe.internal.pdftoolkit.services.swf<br>com.adobe.internal.pdftoolkit.services.textextraction<br>com.adobe.internal.pdftoolkit.services.textextraction.impl<br>com.adobe.internal.pdftoolkit.services.xmp<br>com.adobe.internal.util.base64<br>com.adobe.internal.xmp.utils<br>com.day.crx.core.cluster<br>com.day.crx.packaging<br>com.day.crx.packaging.gfx<br>com.day.crx.query<br>com.day.crx.sling.server.jmx<br>com.day.durbo<br>com.day.durbo.io<br>com.day.imageio.plugins<br>org.apache.aries.jmx.codec<br>org.h2.mvstore<br>org.h2.mvstore.rtree<br>org.h2.mvstore.type<br>org.openxmlformats.schemas.drawingml.x2006.chart.impl<br>org.openxmlformats.schemas.drawingml.x2006.main.impl<br>org.openxmlformats.schemas.drawingml.x2006.picture.impl<br>org.openxmlformats.schemas.drawingml.x2006.spreadsheetDrawing.impl<br>org.openxmlformats.schemas.drawingml.x2006.wordprocessingDrawing.impl<br>org.openxmlformats.schemas.officeDocument.x2006.customProperties.impl<br>org.openxmlformats.schemas.officeDocument.x2006.docPropsVTypes.impl<br>org.openxmlformats.schemas.officeDocument.x2006.extendedProperties.impl<br>org.openxmlformats.schemas.officeDocument.x2006.relationships.impl<br>org.openxmlformats.schemas.presentationml.x2006.main.impl<br>org.openxmlformats.schemas.spreadsheetml.x2006.main.impl<br>org.openxmlformats.schemas.wordprocessingml.x2006.main.impl<br>org.openxmlformats.schemas.xpackage.x2006.contentTypes<br>org.openxmlformats.schemas.xpackage.x2006.contentTypes.impl<br>org.openxmlformats.schemas.xpackage.x2006.digitalSignature<br>org.openxmlformats.schemas.xpackage.x2006.digitalSignature.impl<br>org.openxmlformats.schemas.xpackage.x2006.metadata.coreProperties<br>org.openxmlformats.schemas.xpackage.x2006.metadata.coreProperties.impl<br>org.openxmlformats.schemas.xpackage.x2006.relationships<br>org.openxmlformats.schemas.xpackage.x2006.relationships.impl<br>com.adobe.internal.afml<br>com.adobe.internal.agm<br>com.adobe.internal.pdftoolkit.legacy.services.ap.es2<br>com.adobe.internal.pdftoolkit.legacy.services.ap.es3<br>com.adobe.internal.pdftoolkit.pdf.pieceinfo.compoundtype<br>com.adobe.internal.pdftoolkit.pdf.pieceinfo.editablepdf<br>com.adobe.internal.pdftoolkit.services.ap<br>com.adobe.internal.pdftoolkit.services.ap.annot<br>com.adobe.internal.pdftoolkit.services.ap.extension<br>com.adobe.internal.pdftoolkit.services.ap.impl<br>com.adobe.internal.pdftoolkit.services.ap.spi<br>com.adobe.internal.pdftoolkit.services.digsig<br>com.adobe.internal.pdftoolkit.services.digsig.cryptoprovider<br>com.adobe.internal.pdftoolkit.services.digsig.docmodanalysis<br>com.adobe.internal.pdftoolkit.services.digsig.spi<br>com.adobe.internal.pdftoolkit.services.fdf<br>com.adobe.internal.pdftoolkit.services.formflattener<br>com.adobe.internal.pdftoolkit.services.forms<br>com.adobe.internal.pdftoolkit.services.imageconversion<br>com.adobe.internal.pdftoolkit.services.javascript<br>com.adobe.internal.pdftoolkit.services.javascript.extension<br>com.adobe.internal.pdftoolkit.services.manipulations<br>com.adobe.internal.pdftoolkit.services.manipulations.impl<br>com.adobe.internal.pdftoolkit.services.optimizer<br>com.adobe.internal.pdftoolkit.services.pdfa<br>com.adobe.internal.pdftoolkit.services.pdfa.error<br>com.adobe.internal.pdftoolkit.services.pdfa2<br>com.adobe.internal.pdftoolkit.services.pdfa2.error<br>com.adobe.internal.pdftoolkit.services.pdfa2.error.codes<br>com.adobe.internal.pdftoolkit.services.pdfa3<br>com.adobe.internal.pdftoolkit.services.pdfport<br>com.adobe.internal.pdftoolkit.services.portfolio<br>com.adobe.internal.pdftoolkit.services.rcg<br>com.adobe.internal.pdftoolkit.services.rcg.impl<br>com.adobe.internal.pdftoolkit.services.redaction<br>com.adobe.internal.pdftoolkit.services.redaction.handler<br>com.adobe.internal.pdftoolkit.services.sanitization<br>com.adobe.internal.pdftoolkit.services.xbm<br>com.adobe.internal.pdftoolkit.services.xdp<br>com.adobe.internal.pdftoolkit.services.xfa<br>com.adobe.internal.pdftoolkit.services.xfa.form<br>com.adobe.internal.pdftoolkit.services.xfatext<br>com.adobe.internal.pdftoolkit.services.xfdf<br>com.adobe.internal.pdftoolkit.services.xobjhandler<br>com.adobe.internal.pdftoolkit.xml<br>com.adobe.octopus.extract<br>opennlp.tools.doccat<br>opennlp.tools.entitylinker<br>opennlp.tools.formats<br>opennlp.tools.formats.ad<br>opennlp.tools.formats.brat<br>opennlp.tools.formats.convert<br>opennlp.tools.formats.frenchtreebank<br>opennlp.tools.formats.muc<br>opennlp.tools.formats.ontonotes<br>opennlp.tools.lemmatizer<br>opennlp.tools.parser<br>opennlp.tools.parser.chunking<br>opennlp.tools.parser.lang.en<br>opennlp.tools.parser.lang.es<br>opennlp.tools.parser.treeinsert<br>opennlp.tools.sentdetect<br>opennlp.tools.sentdetect.lang<br>opennlp.tools.sentdetect.lang.th<br>opennlp.tools.stemmer<br>opennlp.tools.stemmer.snowball<br>opennlp.tools.tokenize.lang.en<br>org.apache.commons.imaging.color<br>org.apache.commons.imaging.common<br>org.apache.commons.imaging.common.itu_t4<br>org.apache.commons.imaging.common.mylzw<br>org.apache.commons.imaging.formats.bmp<br>org.apache.commons.imaging.formats.dcx<br>org.apache.commons.imaging.formats.gif<br>org.apache.commons.imaging.formats.icns<br>org.apache.commons.imaging.formats.ico<br>org.apache.commons.imaging.formats.jpeg<br>org.apache.commons.imaging.formats.jpeg.decoder<br>org.apache.commons.imaging.formats.jpeg.exif<br>org.apache.commons.imaging.formats.jpeg.iptc<br>org.apache.commons.imaging.formats.jpeg.segments<br>org.apache.commons.imaging.formats.jpeg.xmp<br>org.apache.commons.imaging.formats.pcx<br>org.apache.commons.imaging.formats.png<br>org.apache.commons.imaging.formats.png.chunks<br>org.apache.commons.imaging.formats.png.scanlinefilters<br>org.apache.commons.imaging.formats.png.transparencyfilters<br>org.apache.commons.imaging.formats.pnm<br>org.apache.commons.imaging.formats.psd<br>org.apache.commons.imaging.formats.psd.dataparsers<br>org.apache.commons.imaging.formats.psd.datareaders<br>org.apache.commons.imaging.formats.rgbe<br>org.apache.commons.imaging.formats.tiff<br>org.apache.commons.imaging.formats.tiff.constants<br>org.apache.commons.imaging.formats.tiff.datareaders<br>org.apache.commons.imaging.formats.tiff.fieldtypes<br>org.apache.commons.imaging.formats.tiff.photometricinterpreters<br>org.apache.commons.imaging.formats.tiff.taginfos<br>org.apache.commons.imaging.formats.tiff.write<br>org.apache.commons.imaging.formats.wbmp<br>org.apache.commons.imaging.formats.xbm<br>org.apache.commons.imaging.formats.xpm<br>org.apache.commons.imaging.icc<br>org.apache.commons.imaging.palette<br>org.apache.commons.imaging.util<br>com.adobe.dam.print.ids.utils<br>com.day.cq.dam.api.reporting<br>com.day.cq.dam.entitlement.api<br>com.day.cq.dam.handler.standard.epub<br>com.day.cq.dam.handler.standard.keynote<br>com.day.cq.dam.handler.standard.mp3<br>com.day.cq.dam.handler.standard.msoffice<br>com.day.cq.dam.handler.standard.msoffice.wmf<br>com.day.cq.dam.handler.standard.ooxml<br>com.day.cq.dam.handler.standard.pdf<br>com.day.cq.dam.handler.standard.pict<br>com.day.cq.dam.handler.standard.ps<br>com.day.cq.dam.handler.standard.psd<br>com.day.cq.dam.handler.standard.zip<br>com.day.cq.dam.word.extraction<br>com.day.cq.dam.word.process<br>com.adobe.xmp.worker.files<br>com.adobe.cq.address.api<br>com.adobe.cq.address.api.location<br>com.day.cq.mcm.emailprovider.impl.types<br>com.day.io<br>com.day.io.disk<br>com.day.io.file<br>org.apache.commons.exec.environment<br>org.apache.commons.exec.launcher<br>org.apache.commons.exec.util<br>com.google.zxing<br>com.google.zxing.common<br>com.google.zxing.common.reedsolomon<br>com.google.zxing.qrcode.decoder<br>com.google.zxing.qrcode.encoder<br>com.adobe.cq.dam.dm.internalapi.image_server<br>com.day.cq.dam.api.s7dam.jobs<br>com.day.cq.dam.api.s7dam.omnisearch<br>com.day.cq.dam.api.s7dam.scene7<br>com.day.cq.dam.scene7<br>com.day.cq.dam.scene7.api.net<br>com.day.cq.analytics.sitecatalyst.rsmerger<br>com.day.cq.searchpromote<br>com.day.cq.searchpromote.xml<br>com.day.cq.searchpromote.xml.form<br>com.day.cq.searchpromote.xml.result&gt;</td>
    <td>Äldre AEM 6.x API.</td>
    <td>4/8/19</td>
    <td>borttagen</td>
  </tr>
  <tr>
    <td>org.apache.sling.discovery.commons<br>org.apache.sling.discovery.commons.providers<br>org.apache.sling.discovery.commons.providers.base<br>org.apache.sling.discovery.commons.providers.spi<br>org.apache.sling.discovery.commons.providers.spi.base<br>org.apache.sling.discovery.commons.providers.util</td>
    <td>Detta API stöds inte i Cloud Servicen.</td>
    <td>9/30/21</td>
    <td>borttagen</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.vault.util.xml<br>org.apache.jackrabbit.vault.util.xml.serialize</td>
    <td>Util-klasser som är relaterade till Apache Xerces tas bort i efterföljande versioner, vilket orsakar en större versionsändring. Eftersom de här verktygen är avsedda för internt bruk i Filevault är API-gränssnittet föråldrat från den offentliga API-ytan.</td>
    <td>9/1/21</td>
    <td>borttagen</td>
  <tr>
    <td>org.apache.sling.atom.taglib<br>org.apache.sling.atom.taglib.media</td>
    <td>Äldre AEM 6.x API.</td>
    <td>4/8/19</td>
    <td>09/29/21</td>
  </tr>
  <tr>
    <td>org.apache.felix.http.whiteboard</td>
    <td>Apache Felix Http Whiteboard stöds inte längre. Migrera koden till OSGi Http Whiteboard.</td>
    <td>2022-1-27</td>
    <td>03/24/2022</td>
  </tr>
  <tr>
    <td>org.apache.cocoon.xml.dom<br>org.apache.cocoon.xml.sax</td>
    <td>Detta API är inaktuellt. Migrera koden till de XML-API:er som tillhandahålls av JDK.</td>
    <td>2022-1-27</td>
    <td>3/24/2022</td>
  </tr>
  <tr>
    <td>ch.qos.logback.classic<br>ch.qos.logback.classic.boolex<br>ch.qos.logback.classic.db.names<br>ch.qos.logback.classic.db.script<br>ch.qos.logback.classic.encoder<br>ch.qos.logback.classic.filter<br>ch.qos.logback.classic.helpers<br>ch.qos.logback.classic.html<br>ch.qos.logback.classic.jmx<br>ch.qos.logback.classic.joran<br>ch.qos.logback.classic.joran.action<br>ch.qos.logback.classic.jul<br>ch.qos.logback.classic.layout<br>ch.qos.logback.classic.log4j<br>ch.qos.logback.classic.net<br>ch.qos.logback.classic.net.server<br>ch.qos.logback.classic.pattern<br>ch.qos.logback.classic.pattern.color<br>ch.qos.logback.classic.selector<br>ch.qos.logback.classic.selector.servlet<br>ch.qos.logback.classic.servlet<br>ch.qos.logback.classic.sift<br>ch.qos.logback.classic.spi<br>ch.qos.logback.classic.turbo<br>ch.qos.logback.classic.util<br>ch.qos.logback.core<br>ch.qos.logback.core.boolex<br>ch.qos.logback.core.encoder<br>ch.qos.logback.core.filter<br>ch.qos.logback.core.helpers<br>ch.qos.logback.core.hook<br>ch.qos.logback.core.html<br>ch.qos.logback.core.joran<br>ch.qos.logback.core.joran.action<br>ch.qos.logback.core.joran.conditional<br>ch.qos.logback.core.joran.event<br>ch.qos.logback.core.joran.event.stax<br>ch.qos.logback.core.joran.node<br>ch.qos.logback.core.joran.spi<br>ch.qos.logback.core.joran.util<br>ch.qos.logback.core.joran.util.beans<br>ch.qos.logback.core.layout<br>ch.qos.logback.core.net<br>ch.qos.logback.core.net.server<br>ch.qos.logback.core.net.ssl<br>ch.qos.logback.core.pattern<br>ch.qos.logback.core.pattern.color<br>ch.qos.logback.core.pattern.parser<br>ch.qos.logback.core.pattern.util<br>ch.qos.logback.core.property<br>ch.qos.logback.core.read<br>ch.qos.logback.core.recovery<br>ch.qos.logback.core.rolling<br>ch.qos.logback.core.rolling.helper<br>ch.qos.logback.core.sift<br>ch.qos.logback.core.spi<br>ch.qos.logback.core.status<br>ch.qos.logback.core.subst<br>ch.qos.logback.core.util</td>
    <td>Detta interna API för inloggning stöds inte av AEM as a Cloud Service.</td>
    <td>2022-1-27</td>
    <td>3/24/2022</td>
  </tr>
  <tr>
    <td>org.slf4j.spi</td>
    <td>Detta interna log4j-API stöds inte av AEM as a Cloud Service.</td>
    <td>2022-1-27</td>
    <td>3/24/2022</td>
  </tr>
  <tr>
    <td>org.apache.log4j<br>org.apache.log4j.helpers<br>org.apache.log4j.spi<br>org.apache.log4j.xml</td>
    <td>Apache Log4j 1 upphörde 2015 och stöds inte längre.</td>
    <td>2022-1-27</td>
    <td>3/24/2022</td>
  </tr>
  <tr>
    <td>org.apache.sling.commons.log.logback<br>org.apache.sling.commons.log.logback.webconsole</td>
    <td>Detta interna API för inloggning stöds inte av AEM as a Cloud Service.</td>
    <td>2022-1-27</td>
    <td>borttagen</td>
  </tr>
  <tr>
    <td>com.github.jknack.handlebars.js</td>
    <td>Uppgradering av handtag krävs från 4.0.5 till 4.3.0 på grund av säkerhetslucka. Det här paketet finns inte längre i de uppgraderade verktygsfälten.</td>
    <td>5/5/2022</td>
    <td>8/5/2022</td>
  </tr>
  <tr>
    <td>com.adobe.granite.resourceresolverhelper</td>
    <td>Detta API stöds inte längre. Använd org.apache.sling.api.resource.ResourceResolverFactory i stället.</td>
    <td>9/29/2022</td>
    <td>2022-11-24</td>
  </tr>
  <tr>
    <td>com.day.cq.contentsync.handler.util</td>
    <td>Detta API är inaktuellt. Använd Apache Sling's Builders i stället.</td>
    <td>10/31/2022</td>
    <td>01/01/2023</td>
  </tr>
  <tr><td>org.apache.sling.commons.json<br>org.apache.sling.commons.json.http<br>org.apache.sling.commons.json.io<br>org.apache.sling.commons.json.jcr<br>org.apache.sling.commons.json.sling<br>org.apache.sling.commons.json.util<br>org.apache.sling.commons.json.xml</td>
    <td>Detta API stöds inte av AEM as a Cloud Service.</td>
    <td>5/15/2023</td>
    <td>15/6/2023</td>
  </tr><td>com.google.common.annotations<br>com.google.common.base<br>com.google.common.cache<br>com.google.common.collect<br>com.google.common.escape<br>com.google.common.eventbus<br>com.google.common.hash<br>com.google.common.html<br>com.google.common.io<br>com.google.common.math<br>com.google.common.net<br>com.google.common.primitives<br>com.google.common.reflect<br>com.google.common.util.concurrent<br>com.google.common.xml</td>
    <td>Google Guava Core Libraries är föråldrat.</td>
    <td>5/15/2023</td>
    <td>15/6/2023</td>
  </tr>
  <tr>
    <td>org.slf4j.event	</td>
    <td>Detta interna slf4j-API stöds inte av AEM as a Cloud Service</td>
    <td>4/11/2022</td>
    <td>8/30/2024</td>
  </tr>
    <td>org.apache.sling.repoinit.jcr<br>org.apache.sling.repoinit.parser.operations</td>
    <td>Användning av detta API stöds inte i AEM as a Cloud Service.</td>
    <td>5/17/2024</td>
    <td>6/30/2024</td>
  </tr>  
</tbody>
</table>
</details>

## OSGI-konfiguration {#osgi-configuration}

De två listorna nedan återspeglar konfigurationsytan för AEM as a Cloud Service OSGi och beskriver vad kunderna kan konfigurera.

1. En lista med OSGi-konfigurationer som inte får konfigureras av kundkoden
1. En lista över OSGi-konfigurationer vars egenskaper kan konfigureras, men måste följa de angivna verifieringsreglerna. Dessa regler omfattar huruvida deklarationen av egenskapen är obligatorisk, dess typ och i vissa fall dess tillåtna värdeintervall.

Om en OSGI-konfiguration inte anges kan den konfigureras med kundkod.

Dessa regler valideras under Cloud Manager byggprocess. Ytterligare regler kan läggas till över tid och det förväntade datumet för verkställighet anges i tabellen. Kunderna förväntas följa dessa regler senast vid måldatumet. Om reglerna inte följs efter borttagningsdatumet genereras fel i Cloud Manager byggprocess. Maven-projekten bör omfatta [AEM as a Cloud Service SDK Build Analyzer Maven Plugin](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html) för att flagga OSGI-konfigurationsfel under lokal SDK-utveckling.

Ytterligare information om OSGI-konfigurationen finns på [den här platsen](/help/implementing/deploying/configuring-osgi.md).

+++OSGi-konfigurationer som inte kan ändras.
* **`org.apache.felix.webconsole.internal.servlet.OsgiManager`** (Tillkännagivande: 2021-04-30, Datum för verkställighet: 2021-07-31)
* **`com.day.cq.auth.impl.cug.CugSupportImpl`** (Tillkännagivande: 2021-04-30, Datum för verkställighet: 2021-07-31)
* **`com.day.cq.jcrclustersupport.ClusterStartLevelController`** (Tillkännagivande: 2021-04-30, Datum för verkställighet: 2021-07-31)
* **`org.apache.felix.http (Factory)`** (Tillkännagivande: 2021-04-30, Datum för verkställighet: 2021-07-31)
* **`org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`** (Tillkännagivande: 2021-08-25, Kräftelsedatum: 2021-08-26)
+++

+++OSGi-konfigurationer som omfattas av build-valideringsregler.
* **`org.apache.felix.eventadmin.impl.EventAdmin`** (Tillkännagivande: 2021-04-30, Datum för verkställighet: 2021-07-31)
* `org.apache.felix.eventadmin.ThreadPoolSize`
   * Typ: heltal
   * Obligatoriskt intervall: 2-100
* `org.apache.felix.eventadmin.AsyncToSyncThreadRatio`
   * Typ: dubbel
* `org.apache.felix.eventadmin.Timeout`
   * Typ: heltal
* `org.apache.felix.eventadmin.RequireTopic`
   * Typ: boolesk
* `org.apache.felix.eventadmin.IgnoreTimeout`
   * Obligatoriskt
   * Typ: strängmatris
   * Obligatoriskt intervall: Måste innehålla minst alla `org.apache.felix*`, `org.apache.sling*`, `come.day*`, `com.adobe*`
* `org.apache.felix.eventadmin.IgnoreTopic`
   * Typ: strängmatris
* **`org.apache.felix.http`** (Tillkännagivande: 2021-04-30, Datum för verkställighet: 2021-07-31)
   * `org.apache.felix.http.timeout`
      * Typ: heltal
   * `org.apache.felix.http.session.timeout`
      * Typ: heltal
   * `org.apache.felix.http.jetty.threadpool.max`
      * Typ: heltal
   * `org.apache.felix.http.jetty.headerBufferSize`
      * Typ: heltal
   * `org.apache.felix.http.jetty.requestBufferSize`
      * Typ: heltal
   * `org.apache.felix.http.jetty.responseBufferSize`
      * Typ: heltal
   * `org.apache.felix.http.jetty.maxFormSize`
      * Typ: heltal
   * `org.apache.felix.https.jetty.session.cookie.httpOnly`
      * Typ: boolesk
   * `org.apache.felix.https.jetty.session.cookie.secure`
      * Typ: boolesk
   * `org.eclipse.jetty.servlet.SessionIdPathParameterName`
      * Typ: sträng
   * `org.eclipse.jetty.servlet.CheckingRemoteSessionIdEncoding`
      * Typ: boolesk
   * `org.eclipse.jetty.servlet.SessionCookie`
      * Typ: sträng
   * `org.eclipse.jetty.servlet.SessionDomain`
      * Typ: sträng
   * `org.eclipse.jetty.servlet.SessionPath`
      * Typ: sträng
   * `org.eclipse.jetty.servlet.MaxAge`
      * Typ: heltal
   * `org.eclipse.jetty.servlet.SessionScavengingInterval`
      * Typ: heltal
   * `org.apache.felix.jetty.gziphandler.enable`
      * Typ: boolesk
   * `org.apache.felix.jetty.gzip.minGzipSize`
      * Typ: heltal
   * `org.apache.felix.jetty.gzip.compressionLevel`
      * Typ: heltal
   * `org.apache.felix.jetty.gzip.inflateBufferSize`
      * Typ: heltal
   * `org.apache.felix.jetty.gzip.syncFlush`
      * Typ: boolesk
   * `org.apache.felix.jetty.gzip.excludedUserAgents`
      * Typ: sträng
   * `org.apache.felix.jetty.gzip.includedMethods`
      * Typ: strängmatris
   * `org.apache.felix.jetty.gzip.excludedMethods`
      * Typ: strängmatris
   * `org.apache.felix.jetty.gzip.includedPaths`
      * Typ: strängmatris
   * `org.apache.felix.jetty.gzip.excludedPaths`
      * Typ: strängmatris
   * `org.apache.felix.jetty.gzip.includedMimeTypes`
      * Typ: strängmatris
   * `org.apache.felix.jetty.gzip.excludedMimeTypes`
      * Typ: strängmatris
   * `org.apache.felix.http.session.invalidate`
      * Typ: boolesk
   * `org.apache.felix.http.session.container.attribute`
      * Typ: strängmatris
   * `org.apache.felix.http.session.uniqueid`
      * Typ: boolesk
* **`org.apache.sling.scripting.cache`** (Tillkännagivande: 2021-04-30, Datum för verkställighet: 2021-07-31)
   * `org.apache.sling.scripting.cache.size`
      * Typ: heltal
      * Obligatoriskt intervall: >= 2048
   * `org.apache.sling.scripting.cache.additional_extensions`
      * Obligatoriskt
      * Typ: strängmatris
      * Obligatoriskt intervall: måste innehålla js
* **`com.day.cq.mailer.DefaultMailService`** (Tillkännagivande: 2021-04-30, Datum för verkställighet: 2021-07-31)
   * `smtp.host`
      * Typ: sträng
   * `smtp.port`
      * Typ: heltal
      * Obligatoriskt intervall: 465, 587 eller 25
   * `smtp.user`
      * Typ: sträng
   * `smtp.password`
      * Typ: sträng
   * `from.address`
      * Typ: sträng
   * `smtp.ssl`
      * Typ: sträng
   * `smtp.starttls`
      * Typ: boolesk
   * `smtp.requiretls`
      * Typ: boolesk
   * `debug.email`
      * Typ: boolesk
   * `oauth.flow`
      * Typ: boolesk
* **`org.apache.sling.commons.log.LogManager.factory.config`** (Tillkännagivande: 21-16-11, Datum för verkställighet: 2-16-21)
   * `org.apache.sling.commons.log.level`
      * Typ: uppräkning
      * Obligatoriskt intervall: INFO, DEBUG eller TRACE
   * `org.apache.sling.commons.log.names`
      * Typ: sträng
   * `org.apache.sling.commons.log.file`
      * Typ: sträng
   * `org.apache.sling.commons.log.additiv`
      * Typ: boolesk
+++

