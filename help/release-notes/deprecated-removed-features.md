---
title: Föråldrade och borttagna funktioner
description: Versionsinformation som är specifik för borttagna och borttagna funktioner i  [!DNL Adobe Experience Manager]  som en [!DNL Cloud Service].
exl-id: ef082184-4eb7-49c7-8887-03d925e3da6f
feature: Release Information
role: Admin
source-git-commit: 3d294b2b4fbd11f16ee8b0fbb5a9a46ab039dbae
workflow-type: tm+mt
source-wordcount: '2858'
ht-degree: 0%

---

# Föråldrade och borttagna funktioner och API:er {#deprecated-and-removed-features-apis}

>[!CONTEXTUALHELP]
>id="aem_cloud_deprecated_features"
>title="Borttagna funktioner i AEM as a Cloud Service"
>abstract="AEM as a Cloud Service har en distributionsmodell som bygger på molnet. På den här fliken markeras funktioner som ersatts av deras molnbaserade motsvarigheter."

Adobe utvärderar ständigt produktfunktioner för att med tiden kunna förnya eller ersätta äldre funktioner med modernare alternativ för att förbättra det totala kundvärdet, alltid under noggrant övervägande av bakåtkompatibilitet. Eftersom [!DNL Adobe Experience Manager] som [!DNL Cloud Service] använder en molnbaserad distributionsmodell ersätts vissa funktioner med molnbaserade motsvarigheter.

Följande regler gäller för att kommunicera den förestående borttagningen/ersättningen av [!DNL Experience Manager]-funktioner:

1. Föråldringsanmälan kommer först. Föråldrade funktioner är fortfarande tillgängliga men har inte förbättrats ytterligare.
1. Funktioner som annonserats vara borttagna så snart som möjligt i den senare större versionen. Det faktiska måldatumet för borttagning tillkännages.

Den här processen ger kunderna minst en releasecykel för att anpassa implementeringen till en ny version eller en efterföljare till en borttagningsfunktion, innan den faktiska borttagningen.

## Föråldrade funktioner {#deprecated-features}

I det här avsnittet visas funktioner som har markerats som borttagna i [!DNL Experience Manager] som [!DNL Cloud Service]. Vanligtvis ställs funktioner som ska tas bort i en framtida version in för borttagning först, med ett alternativ.

Kunderna rekommenderas att granska om de använder funktionen/funktionen i den aktuella distributionen och planera för att ändra implementeringen så att den använder det alternativ som erbjuds.

| Funktioner | Inaktuell funktion | Ersättning |
| ------------ | ------------------ | ----------- |
| Sites | [PWA-funktioner](/help/sites-cloud/authoring/sites-console/enable-pwa.md) | Ingen |
| Sites | [SPA-redigerare](/help/implementing/developing/hybrid/introduction.md) | De redigerare som rekommenderas för att hantera headless-innehåll i AEM är:<br>- [Universell redigerare](/help/edge/wysiwyg-authoring/authoring.md) för visuell redigering.<br>- [Innehållsfragmentredigeraren](/help/assets/content-fragments/content-fragments-managing.md) för formulärbaserad redigering. |
| [!DNL Sites] | [JavaScript Use API](https://github.com/adobe/htl-spec/blob/master/SPECIFICATION.md#42-javascript-use-api) | [Java Use API](https://experienceleague.adobe.com/en/docs/experience-manager-htl/content/java-use-api) |
| [!DNL Sites] | Upplev fragmentegenskaper för **Status för sociala medier**. | Funktionen är planerad att tas bort snart. |
| [!DNL Sites] | Mallbaserade enkla innehållsfragment. | [Modellbaserade strukturerade innehållsfragment](/help/assets/content-fragments/content-fragments-models.md). |
| [!DNL Assets] | `DAM Asset Update` arbetsflöde för att bearbeta inkapslade bilder. | Tillgångsintaget använder [tillgångsmikrotjänster](/help/assets/asset-microservices-overview.md) nu. |
| [!DNL Assets] | Överför resurser direkt till [!DNL Experience Manager]. Se [inaktuella API:er för överföring av resurser](/help/assets/developer-reference-material-apis.md#deprecated-asset-upload-api). | Använd [direkt binär överföring](/help/assets/add-assets.md). Mer teknisk information finns i [API:er för direktöverföring](/help/assets/developer-reference-material-apis.md#upload-binary). |
| [!DNL Assets] | [Vissa arbetsflödessteg](/help/assets/developer-reference-material-apis.md#post-processing-workflows-steps) i `DAM Asset Update`-arbetsflödet stöds inte, inklusive anrop av kommandoradsverktyg som [!DNL ImageMagick]. | [Resursmikrotjänster](/help/assets/asset-microservices-overview.md) ersätter många arbetsflöden. Använd [efterbearbetningsarbetsflöden](/help/assets/asset-microservices-configure-and-use.md#post-processing-workflows) för anpassad bearbetning. |
| [!DNL Assets] | Konvertera videofilmer till mpeg. | Använd [Resursmikrotjänster](/help/assets/asset-microservices-overview.md) för att skapa miniatyrbilder för MPEG. Använd [Dynamiska media](/help/assets/manage-video-assets.md) för MPEG-omkodning. |
| [!DNL Foundation] | Gränssnitt för trädreplikering på fliken Distribuera för replikeringsagenter (borttagning efter 30 september 2021) | [Hantera arbetsflödesmetoderna för publikation](/help/operations/replication.md#manage-publication) eller [Trädaktivering](/help/operations/replication.md#tree-activation). |
| [!DNL Foundation] | Administratörsskärmbilden för replikeringsagenten har fliken Distribuera och replikerings-API:t kan inte replikera innehållspaket som är större än 10 MB. | [Hantera publikation](/help/operations/replication.md#manage-publication) eller [Arbetsflöde för trädaktivering](/help/operations/replication.md#tree-activation) |
| [!DNL Foundation] | Integrering med hjälp av autentiseringsuppgifter som genererats från Adobe Developer Console-projekt förlorar gradvis stöd för JWT-autentiseringsuppgifter (Service Account). Från och med den 1 maj 2024 går det inte att skapa nya JWT-autentiseringsuppgifter i Adobe Developer Console. Befintliga JWT-autentiseringsuppgifter (Service Account) är fortfarande användbara för konfigurerade integreringar fram till 1 januari 2025. Därefter slutar de fungera, vilket kräver att kunderna migrerar till OAuth Server-till-Server-autentiseringsuppgifter. [Läs mer](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/jwt-credentials-deprecation-in-adobe-developer-console). | [Migrera](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/migration/#migration-overview) till autentiseringsuppgifter för OAuth Server-till-Server. |
| [!DNL Foundation] | Publicera arbetsflöde för innehållsträd och det relaterade arbetsflödessteget Publicera innehållsträd, som användes för replikeringar av innehållshierarkier. | Använd [Arbetsflödessteget för trädaktivering](/help/operations/replication.md#tree-activation), vilket är mer prestandaförbättrat. |
| Sites | [Experience Cloud Setup Automation](/help/sites-cloud/integrating/adobe-analytics-exc-setup-automation.md) | Ingen |


## Borttagna funktioner {#removed-features}

I det här avsnittet visas funktioner som har tagits bort från [!DNL Experience Manager] med [!DNL Experience Manager] som [!DNL Cloud Service].

| Område | Funktion | Ersättning | Borttagningsdatum för mål |
| ------------ | ------------------ | ----------- | ------------------- |
| Användargränssnitt | Klassiskt användargränssnitt har tagits bort från produktanvändargränssnittet. Det finns några dialogrutor för klassiskt användargränssnitt för ett fåtal utvalda funktioner, som Länkkontroll, Rensa version och vissa Cloud Service-konfigurationer. De kommande [produktuppdateringarna](/help/release-notes/home.md) kan ta bort Classic UI-tillgängligheten ytterligare. | Standardgränssnitt | Borttagen |
| [!DNL Dynamic Media] | Tidigare integreringar med [Dynamic Media Classic](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/sites/administering/integration/scene7#integration) och [Dynamic Media Hybrid Mode](https://experienceleague.adobe.com/en/docs/experience-manager-65/content/assets/dynamic/config-dynamic#dynamic) är inte tillgängliga i [!DNL Experience Manager] som [!DNL Cloud Service]. | Använd [Dynamiska media](/help/assets/dynamic-media/dynamic-media.md) som tillhandahålls med [!DNL Experience Manager] som [!DNL Cloud Service]. | Borttagen |
| [!DNL Sites] | Portal Director och Portlet Component | Dessa funktioner har tagits bort i [!DNL Experience Manager] 6.4 och har nu tagits bort från [!DNL Experience Manager]. | Borttagen |
| [!DNL Sites] | Designimporteraren | Den här funktionen har tagits bort eftersom oföränderliga avsnitt i databasen [!DNL Experience Manager] inte är tillgängliga vid körning. | Borttagen |
| [!DNL Assets] | Det går inte att dela [!DNL Assets] med tjänsten Assets Core och Creative Cloud. | Använd [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) för integrering med [!DNL Adobe Creative Cloud]. | Borttagen |
| [!DNL Foundation] | Stöd för Apache Sling-datakällor (OSGi bundle org.apache.sling.datasource) | Ej tillämpligt | Borttagen |
| [!DNL Foundation] | Stöd för JST-skriptmallar (OSGi bundle org.apache.sling.scripting.jst) | Ej tillämpligt | Borttagen |
| [!DNL Foundation] | Stöd för Apache Felix Http Whiteboard | OSGi Http Whiteboard | Mars 2022 |
| [!DNL Foundation] | Stöd för com.adobe.granite.oauth.server | Integrering med Adobe IMS | Mars 2023 |
| [!DNL Foundation] | Stöd för funktionen org.apache.sling.servicusermapping till [hämta tjänstanvändar-ID](https://sling.apache.org/apidocs/sling12/org/apache/sling/serviceusermapping/ServiceUserMapper.html#getServiceUserID-org.osgi.framework.Bundle-java.lang.String-) | Ej tillämpligt | 8/30/24 |


## AEM API:er {#aem-apis}

Nedan finns en omfattande lista över borttagna AEM-API:er och deras förväntade borttagningsdatum. Kunder förväntas ta bort API:erna vid målborttagningsdatumet från sin kod. All användning av API:t efter borttagningsdatumet kan generera fel i den lokala SDK/Development Environment och Cloud Manager byggprocess.

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
    <td>Använd Slings gränssnitt Auth Core/Auth Core SPI som ett alternativ. <a href="#org.apache.sling.commons.auth">Se borttagningsanteckningar nedan.</a></td>
    <td>2015</td>
    <td>8/31/2025</td>
  </tr>
  <tr>
    <td>org.apache.sling.runmode</td>
    <td></td>
    <td>2015</td>
    <td>7/30/2021</td>
  </tr>
  <tr>
    <td>org.json</td>
    <td>Apache Johnzon-implementeringen av <a href="https://johnzon.apache.org/index.html">javax.json</a> rekommenderas och bör användas. </td>
    <td>4/30/2021</td>
    <td>12/31/2021</td>
  </tr>
  <tr>
    <td>org.apache.commons.lang<br>org.apache.commons.lang.enums<br>org.apache.commons.lang.builder<br>org.apache.commons.lang.exception<br>org.apache.commons.lang.math<br>org.apache.commons.lang.mutable<br>org.apache.commons.lang.reflect<br>org.apache.commons.lang.text<br>org.apache.commons.lang.time</td>
    <td>Commons Lang 2 är i underhållsläge. Kommandon Lang 3 bör användas i stället. <a href="#apache.commons">Se borttagningsanteckningar nedan.</a></td>
    <td>4/30/2021</td>
    <td>12/31/2021</td>
  </tr>
  <tr>
    <td>org.apache.commons.collections<br>org.apache.commons.collections.bag<br>org.apache.commons.collections.bidimap<br>org.apache.commons.collections.buffer<br>org.apache.commons.collections.collection<br>org.apache.commons.collections.comparators<br>org.apache.commons.collections.functors<br>org.apache.commons.collections.iterators<br>org.apache.commons.collections.keyvalue<br>org.apache.commons.collections.list<br>org.apache.commons.collections.map<br>org.apache.commons.collections.set</td>
    <td>Commons Collections 3 är i underhållsläge. Commons Collections 4 ska användas i stället. <a href="#apache.commons">Se borttagningsanteckningar nedan.</a></td>
    <td>4/30/2021</td>
    <td>12/31/2021</td>
  </tr>
  <tr>
    <td>org.apache.felix.webconsole<br>org.apache.felix.webconsole.bundleinfo<br>org.apache.felix.webconsole.i18n<br>org.apache.felix.webconsole.spi</td>
    <td>Felix webbkonsol stöds inte i molnmiljöer. <a href="#org.apache.felix.webconsole">Se borttagningsanteckningar nedan.</a></td>
    <td>4/30/2021</td>
    <td>8/31/2025</td>
  </tr>
  <tr>
<td>org.eclipse.jetty.client<br>org.eclipse.jetty.client.api<br>org.eclipse.jetty.client.http<br>org.eclipse.jetty.client.util<br>org.eclipse.jetty.http<br>org.eclipse.jetty.http.pathmap<br>org.eclipse.jetty.io<br>org.eclipse.jetty.io.ssl<br>org.eclipse.jetty.security<br>org.eclipse.jetty.server<br>org.eclipse.jetty.server.handler<br>org.eclipse.jetty.server.handler.gzip<br>org.eclipse.jetty.server.session<br>org.eclipse.jetty.servlet<br>org.eclipse.jetty.servlet.listener<br>org.eclipse.jetty.util<br>org.eclipse.jetty.util.annotation<br>org.eclipse.jetty.util.component<br>org.eclipse.jetty.util.log<br>org.eclipse.jetty.util.resource<br>org.eclipse.jetty.util.security<br>org.eclipse.jetty.util.ssl<br>org.eclipse.jetty.util.statistic<br>org.eclipse.jetty.util.thread</td>
    <td>Paketen Eclipse Jetty och Felix Http Jetty stöds inte längre. <a href="#org.eclipse.jetty">Se borttagningsanteckningar nedan.</a></td>
    <td>2021-05-27</td>
    <td>8/31/2025</td>
  </tr>
  <tr>     <td>com.mongodb<br>com.mongodb.annotations<br>com.mongodb.assertions<br>com.mongodb.async<br>com.mongodb.binding<br>com.mongodb.bulk<br>com.mongodb.client<br>com.mongodb.client.gridfs<br>com.mongodb.client.gridfs.codecs<br>com.mongodb.client.gridfs.model<br>com.mongodb.client.jndi<br>com.mongodb.client.model<br>com.mongodb.client.model.changestream<br>com.mongodb.client.model.geojson<br>com.mongodb.client.model.geojson.codecs<br>com.mongodb.client.result<br>com.mongodb.connection<br>com.mongodb.connection.netty<br>com.mongodb.diagnostics.logging<br>com.mongodb.event<br>com.mongodb.gridfs<br>com.mongodb.internal<br>com.mongodb.internal.async<br>com.mongodb.internal.authentication<br>com.mongodb.internal.connection<br>com.mongodb.internal.dns<br>com.mongodb.internal.event<br>com.mongodb.internal.management.jmx<br>com.mongodb.internal.session<br>com.mongodb.internal.thread<br>com.mongodb.internal.validator<br>com.mongodb.management<br>com.mongodb.operation<br>com.mongodb.selector<br>com.mongodb.session<br>com.mongodb.util</td>
    <td>Användning av detta API stöds inte i AEM as a Cloud Service. <a href="#com.mongodb">Se borttagningsanteckningar nedan.</a></td>
    <td>2021-05-27</td>
    <td>8/31/2025</td>
  </tr>
  <tr>
    <td>org.apache.abdera<br>org.apache.abdera.model<br>org.apache.abdera.factory<br>org.apache.abdera.ext.media<br>org.apache.abdera.util<br>org.apache.abdera.i18n.iri<br>org.apache.abdera.writer<br>org.apache.abdera.i18n.rfc4646<br>org.apache.abdera.i18n.rfc4646.enums<br>org.apache.abdera.i18n.text<br>org.apache.abdera.filter<br>org.apache.abdera.xpath<br>org.apache.abdera.i18n.text.io<br>org.apache.abdera.i18n.text.data<br>org.apache.abdera.parser</td>
    <td>API:t används inte eftersom Apache Abdera är ett projekt som har gått tillbaka sedan 2017. <a href="#org.apache.abdera_or_org.apache.sling.atom.taglib">Se borttagningsanteckningar nedan.</a></td>
    <td>7/29/2021</td>
    <td>8/31/2025</td>
  </tr>
  <tr>
    <td>org.apache.abdera.ext.opensearch<br>org.apache.abdera.ext.opensearch.model<br>org.apache.abdera.ext.opensearch.server<br>org.apache.abdera.ext.opensearch.server.impl<br>org.apache.abdera.ext.opensearch.server.processors<br>org.apache.abdera.i18n.iri.data<br>org.apache.abdera.i18n.lang<br>org.apache.abdera.i18n.templates<br>org.apache.abdera.i18n.unicode.data<br>org.apache.abdera.parser.stax<br>org.apache.abdera.parser.stax.util<br>org.apache.abdera.protocol<br>org.apache.abdera.protocol.client<br>org.apache.abdera.protocol.client.cache<br>org.apache.abdera.protocol.client.util<br>org.apache.abdera.protocol.error<br>org.apache.abdera.protocol.server<br>org.apache.abdera.protocol.server.context<br>org.apache.abdera.protocol.server.filters<br>org.apache.abdera.protocol.server.impl<br>org.apache.abdera.protocol.server.multipart<br>org.apache.abdera.protocol.server.processors<br>org.apache.abdera.protocol.server.provider.basic<br>org.apache.abdera.protocol.server.provider.managed<br>org.apache.abdera.protocol.server.servlet<br>org.apache.abdera.protocol.util<br>org.apache.abdera.util.filter</td>
    <td>API:t används inte eftersom Apache Abdera är ett projekt som har gått tillbaka sedan 2017. <a href="#org.apache.abdera_or_org.apache.sling.atom.taglib">Se borttagningsanteckningar nedan.</a></td>
    <td>4/8/2019</td>
    <td>8/31/2025</td>
  </tr>
  <tr>
    <td>org.apache.felix.http.whiteboard</td>
    <td>Apache Felix Http Whiteboard stöds inte längre. Migrera koden till OSGi Http Whiteboard. <a href="#org.apache.felix.http.whiteboard">Se borttagningsanteckningar nedan.</a></td>
    <td>2022-1-27</td>
    <td>8/31/2025</td>
  </tr>
  <tr>
    <td>org.apache.cocoon.xml.dom<br>org.apache.cocoon.xml.sax</td>
    <td>Detta API är inaktuellt. Migrera koden till de XML-API:er som finns i JDK.</td>
    <td>2022-1-27</td>
    <td>8/31/2025</td>
  </tr>
  <tr>
    <td>ch.qos.logback.classic<br>ch.qos.logback.classic.boolex<br>ch.qos.logback.classic.db.names<br>ch.qos.logback.classic.db.script<br>ch.qos.logback.classic.encoder<br>ch.qos.logback.classic.filter<br>ch.qos.logback.classic.helpers<br>ch.qos.logback.classic.html<br>ch.qos.logback.classic.jmx<br>ch.qos.logback.classic.joran<br>ch.qos.logback.classic.joran.action<br>ch.qos.logback.classic.jul<br>ch.qos.logback.classic.layout<br>ch.qos.logback.classic.log4j<br>ch.qos.logback.classic.net<br>ch.qos.logback.classic.net.server<br>ch.qos.logback.classic.pattern<br>ch.qos.logback.classic.pattern.color<br>ch.qos.logback.classic.selector<br>ch.qos.logback.classic.selector.servlet<br>ch.qos.logback.classic.servlet<br>ch.qos.logback.classic.sift<br>ch.qos.logback.classic.spi<br>ch.qos.logback.classic.turbo<br>ch.qos.logback.classic.util<br>ch.qos.logback.core<br>ch.qos.logback.core.boolex<br>ch.qos.logback.core.encoder<br>ch.qos.logback.core.filter<br>ch.qos.logback.core.helpers<br>ch.qos.logback.core.hook<br>ch.qos.logback.core.html<br>ch.qos.logback.core.joran<br>ch.qos.logback.core.joran.action<br>ch.qos.logback.core.joran.conditional<br>ch.qos.logback.core.joran.event<br>ch.qos.logback.core.joran.event.stax<br>ch.qos.logback.core.joran.node<br>ch.qos.logback.core.joran.spi<br>ch.qos.logback.core.joran.util<br>ch.qos.logback.core.joran.util.beans<br>ch.qos.logback.core.layout<br>ch.qos.logback.core.net<br>ch.qos.logback.core.net.server<br>ch.qos.logback.core.net.ssl<br>ch.qos.logback.core.pattern<br>ch.qos.logback.core.pattern.color<br>ch.qos.logback.core.pattern.parser<br>ch.qos.logback.core.pattern.util<br>ch.qos.logback.core.property<br>ch.qos.logback.core.read<br>ch.qos.logback.core.recovery<br>ch.qos.logback.core.rolling<br>ch.qos.logback.core.rolling.helper<br>ch.qos.logback.core.sift<br>ch.qos.logback.core.spi<br>ch.qos.logback.core.status<br>ch.qos.logback.core.subst<br>ch.qos.logback.core.util</td>
    <td>AEM as a Cloud Service stöder inte detta interna API för återloggning. <a href="#ch.qos.logback">Se borttagningsanteckningar nedan.</a></td>
    <td>2022-1-27</td>
    <td>8/31/2025</td>
  </tr>
  <tr>
    <td>org.slf4j.spi</td>
    <td>AEM as a Cloud Service stöder inte detta interna log4j API. <a href="#org.slf4j">Se borttagningsanteckningar nedan.</a></td>
    <td>2022-1-27</td>
    <td>8/31/2025</td>
  </tr>
  <tr>
    <td>org.apache.log4j<br>org.apache.log4j.helpers<br>org.apache.log4j.spi<br>org.apache.log4j.xml</td>
    <td>Apache Log4j 1 upphörde 2015 och stöds inte längre. <a href="#org.apache.log4j">Se borttagningsanteckningar nedan.</a></td>
    <td>2022-1-27</td>
    <td>8/31/2025</td>
  </tr>
  <tr>
    <td>com.day.cq.contentsync.handler.util</td>
    <td>Detta API är inaktuellt. Använd Apache Sling's Builders i stället.</td>
    <td>10/31/2022</td>
    <td>1/01/2023</td>
  </tr>
  <tr><td>org.apache.sling.commons.json<br>org.apache.sling.commons.json.http<br>org.apache.sling.commons.json.io<br>org.apache.sling.commons.json.jcr<br>org.apache.sling.commons.json.sling<br>org.apache.sling.commons.json.util<br>org.apache.sling.commons.json.xml</td>
    <td>AEM as a Cloud Service stöder inte detta API.</td>
    <td>5/15/2023</td>
    <td>15/6/2023</td>
  </tr><td>com.google.common.annotations<br>com.google.common.base<br>com.google.common.cache<br>com.google.common.collect<br>com.google.common.escape<br>com.google.common.eventbus<br>com.google.common.hash<br>com.google.common.html<br>com.google.common.io<br>com.google.common.math<br>com.google.common.net<br>com.google.common.primitives<br>com.google.common.reflect<br>com.google.common.util.concurrent<br>com.google.common.xml</td>
    <td>Google Guava Core Libraries är föråldrat.</td>
    <td>5/15/2023</td>
    <td>8/31/2025</td>
  </tr>
  <tr>
    <td>org.slf4j.event</td>
    <td>AEM as a Cloud Service stöder inte detta interna slf4j-API. <a href="#org.slf4j">Se borttagningsanteckningar nedan.</a></td>
    <td>4/11/2022</td>
    <td>8/31/2025</td>
  </tr>
  <tr>
    <td>com.day.cq.xss<br>com.day.cq.xss.taglib<br>com.day.cq.xss.impl</td>
    <td>Använd org.apache.sling.xss i stället.</td>
    <td>12/12/2023</td>
    <td>6/30/2024</td>
  </tr>
  <tr>
    <td>com.adobe.granite.xss<br>com.adobe.granite.xss.impl</td>
    <td>Använd org.apache.sling.xss i stället.</td>
    <td>12/12/2023</td>
    <td>6/30/2024</td>
  </tr>
  <tr>
    <td>com.drew.*</td>
    <td>Du bör extrahera metadata från bilder och videoklipp via Asset Compute i Cloud Service eller via Apache POI eller Apache Tika.</td>
    <td>9/17/2024</td>
    <td>8/31/2025</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.oak.plugins.blob.*</td>
    <td>Detta API är endast internt.</td>
    <td>9/23/2024</td>
    <td>8/31/2025</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.oak.plugins.memory</td>
    <td>Detta API är endast internt.</td>
    <td>9/23/2024</td>
    <td>8/31/2025</td>
  </tr>
  <tr>
    <td>org.bson<br/>org.bson.assertions<br/>org.bson.codecs<br/>org.bson.codecs.configuration<br/>org.bson.codecs.pojo<br/>org.bson.codecs.pojo.annotations<br/>org.bson.conversions<br/>org.bson.diagnostics<br/>org.bson.internal<br/>org.bson.io<br/>org.bson.json<br/>org.bson.types<br/>org.bson.util</td>
    <td>Användning av detta API stöds inte i AEM as a Cloud Service.</td>
    <td>10/31/2022</td>
    <td>8/31/2025</td>
  </tr>
</tbody>
</table>
</details>

Nedan finns en omfattande lista över borttagna AEM API:er.

<details>
  <summary>Expandera om du vill visa listan över borttagna API:er.</summary>
<table style="table-layout:auto">
  <tr>
    <th>Paket/klass</th>
    <th>Kommentar</th>
  </tr>
<tbody>
  <tr>
    <td>com.day.cq.jcrclustersupport</td>
    <td>Använd Sling Discovery API som ett alternativ</td>
  </tr>
  <tr>
    <td>org.apache.fop.apps</td>
    <td></td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.vault.util.xml.xerces.dom<br>org.apache.jackrabbit.vault.util.xml.xerces.util<br>org.apache.jackrabbit.vault.util.xml.xerces.xni<br>org.apache.jackrabbit.vault.util.xml.xerces.xni.parser</td>
    <td></td>
  </tr>
  <tr>
    <td>org.apache.felix.cm<br>org.apache.felix.cm.file</td>
    <td>Anpassade beständiga hanterare stöds inte i AEM as a Cloud Service.</td>
  </tr>
  <tr>
    <td>org.apache.felix.systemready</td>
    <td>Du bör använda API:t Apache Felix HealthCheck i stället</td>
  </tr>
  <tr> <td>org.apache.felix.http.jetty<br>org.eclipse.jetty.client.jmx<br>org.eclipse.jetty.jmx<br>org.eclipse.jetty.server.handler.jmx<br>org.eclipse.jetty.server.nio<br>org.eclipse.jetty.server.jmx<br>org.eclipse.jetty.servlet.jmx<br>org.eclipse.jetty.util.preventers<br>org.eclipse.jetty.util.thread.strategy<br>org.eclipse.jetty.webapp<br>org.eclipse.jetty.websocket.api<br>org.eclipse.jetty.websocket.api.annotations<br>org.eclipse.jetty.websocket.api.extensions<br>org.eclipse.jetty.websocket.api.util<br>org.eclipse.jetty.websocket.client<br>org.eclipse.jetty.websocket.client.io<br>org.eclipse.jetty.websocket.client.masks<br>org.eclipse.jetty.websocket.common<br>org.eclipse.jetty.websocket.common.events<br>org.eclipse.jetty.websocket.common.events.annotated<br>org.eclipse.jetty.websocket.common.extensions<br>org.eclipse.jetty.websocket.common.extensions.compress<br>org.eclipse.jetty.websocket.common.extensions.fragment<br>org.eclipse.jetty.websocket.common.extensions.identity<br>org.eclipse.jetty.websocket.common.frames<br>org.eclipse.jetty.websocket.common.io<br>org.eclipse.jetty.websocket.common.io.http<br>org.eclipse.jetty.websocket.common.io.payload<br>org.eclipse.jetty.websocket.common.message<br>org.eclipse.jetty.websocket.common.scopes<br>org.eclipse.jetty.websocket.common.util<br>org.eclipse.jetty.websocket.server<br>org.eclipse.jetty.websocket.server.pathmap<br>org.eclipse.jetty.websocket.servlet<br>org.eclipse.jetty.xml</td>
    <td>Paketen Eclipse Jetty och Felix Http Jetty stöds inte längre.</td>
  </tr>
  <tr>
    <td>org.apache.felix.metatype<br>org.apache.felix.scr<br>org.apache.felix.scr.info<br>org.apache.felix.scr.component</td>
    <td>Apache Felix-metatypen och SCR-API:erna är föråldrade.  Använd OSGi-metatypen och deklarativa tjänstens API:er i stället.</td>
  </tr>
  <tr>
    <td>org.slf4j.impl</td>
    <td>Loggimplementeringsklasser är inte kompatibla med AEM as a Cloud Service.</td>
  </tr>
  <tr>
    <td>org.apache.sling.startupfilter<br>com.adobe.granite.crypto.spi<br>com.adobe.granite.crpyto.spi.base<br>com.adobe.agl.impl.data.icudt40b<br>com.adobe.agl.impl.data.icudt40b.brkitr<br>com.adobe.agl.impl.data.icudt40b.coll<br>com.adobe.agl.impl.data.icudt40b.rbnf<br>com.<br>adobe.agl.impl.data.icudt40b.translit<br>com.adobe.internal.pdf.tika<br>com.adobe.internal.pdftoolkit.color<br>com.adobe.internal.pdftoolkit.core.encryption<br>com.adobe.internal.pdftoolkit.core.encryption.impl<br>com.adobe.internal.pdftoolkit.core.traverser<br>com.adobe.internal.pdftoolkit.graphicsDOM<br>com.adobe.internal.pdftoolkit.graphicsDOM.shading<br>com.adobe.internal.pdftoolkit.graphicsDOM.utils<br>com.adobe.internal.pdftoolkit.image<br>com.adobe.internal.pdftoolkit.pdf.content<br>com.adobe.internal.pdftoolkit.pdf.content.processor<br>com.adobe.internal.pdftoolkit.pdf.content.processor.base14fontwidths<br>com.adobe.internal.pdftoolkit.pdf.contentmodify<br>com.adobe.internal.pdftoolkit.pdf.contentmodify.impl<br>com.adobe.internal.pdftoolkit.pdf.digsig<br>com.adobe.internal.pdftoolkit.pdf.document<br>com.adobe.internal.pdftoolkit.pdf.document.listener<br>com.adobe.internal.pdftoolkit.pdf.document.permissionhandlers<br>com.adobe.internal.pdftoolkit.pdf.filters<br>com.adobe.internal.pdftoolkit.pdf.graphics<br>com.adobe.internal.pdftoolkit.pdf.graphics.colorspaces<br>com.adobe.internal.pdftoolkit.pdf.graphics.colorspaces.cmykresources<br>com.adobe.internal.pdftoolkit.pdf.graphics.font<br>com.adobe.internal.pdftoolkit.pdf.graphics.font.encodings<br>com.adobe.internal.pdftoolkit.pdf.graphics.font.impl<br>com.adobe.internal.pdftoolkit.pdf.graphics.impl<br>com.adobe.internal.pdftoolkit.pdf.graphics.optionalcontent<br>com.adobe.internal.pdftoolkit.pdf.graphics.patterns<br>com.adobe.internal.pdftoolkit.pdf.graphics.shading<br>com.adobe.internal.pdftoolkit.pdf.graphics.xobject<br>com.adobe.internal.pdftoolkit.pdf.impl<br>com.adobe.internal.pdftoolkit.pdf.inlineimage<br>com.adobe.internal.pdftoolkit.pdf.interactive<br>com.adobe.internal.pdftoolkit.pdf.interactive.action<br>com.adobe.internal.pdftoolkit.pdf.interactive.annotation<br>com.adobe.internal.pdftoolkit.pdf.interactive.forms<br>com.adobe.internal.pdftoolkit.pdf.interactive.forms.impl<br>com.adobe.internal.pdftoolkit.pdf.interactive.geospatial<br>com.adobe.internal.pdftoolkit.pdf.interactive.markedcontent<br>com.adobe.internal.pdftoolkit.pdf.interactive.navigation<br>com.adobe.internal.pdftoolkit.pdf.interactive.navigation.collection<br>com.adobe.internal.pdftoolkit.pdf.interactive.readerrequirements<br>com.adobe.internal.pdftoolkit.pdf.interactive.requirement<br>com.adobe.internal.pdftoolkit.pdf.interchange<br>com.adobe.internal.pdftoolkit.pdf.interchange.documentparts<br>com.adobe.internal.pdftoolkit.pdf.interchange.metadata<br>com.adobe.internal.pdftoolkit.pdf.interchange.prepress<br>com.adobe.internal.pdftoolkit.pdf.interchange.structure<br>com.adobe.internal.pdftoolkit.pdf.multimedia<br>com.adobe.internal.pdftoolkit.pdf.page<br>com.adobe.internal.pdftoolkit.pdf.rendering<br>com.adobe.internal.pdftoolkit.pdf.transparency<br>com.adobe.internal.pdftoolkit.pdf.utils<br>com.adobe.internal.pdftoolkit.services.Jpeg2000<br>com.adobe.internal.pdftoolkit.services.fontresources<br>com.adobe.internal.pdftoolkit.services.fontresources.subsetting<br>com.adobe.internal.pdftoolkit.services.interchange.structure<br>com.adobe.internal.pdftoolkit.services.optionalcontent<br>com.adobe.internal.pdftoolkit.services.optionalcontent.impl<br>com.adobe.internal.pdftoolkit.services.pdfParser<br>com.adobe.internal.pdftoolkit.services.permissions<br>com.adobe.internal.pdftoolkit.services.rasterizer<br>com.adobe.internal.pdftoolkit.services.readingorder<br>com.adobe.internal.pdftoolkit.services.security<br>com.adobe.internal.pdftoolkit.services.swf<br>com.adobe.internal.pdftoolkit.services.textextraction<br>com.adobe.internal.pdftoolkit.services.textextraction.impl<br>com.adobe.internal.pdftoolkit.services.xmp<br>com.adobe.internal.util.base64<br>com.adobe.internal.xmp.utils<br>com.day.crx.core.cluster<br>com.day.crx.packaging<br>com.day.crx.packaging.gfx<br>com.day.crx.query<br>com.day.crx.sling.server.jmx<br>com.day.durbo<br>com.day.durbo.io<br>com.day.imageio.plugins<br>org.apache.aries.jmx.codec<br>org.h2.mvstore<br>org.h2.mvstore.rtree<br>org.h2.mvstore.type<br>org.openxmlformats.schemas.drawingml.x2006.chart.impl<br>org.openxmlformats.schemas.drawingml.x2006.main.impl<br>org.openxmlformats.schemas.drawingml.x2006.picture.impl<br>org.openxmlformats.schemas.drawingml.x2006.spreadsheetDrawing.impl<br>org.openxmlformats.schemas.drawingml.x2006.wordprocessingDrawing.impl<br>org.openxmlformats.schemas.officeDocument.x2006.customProperties.impl<br>org.openxmlformats.schemas.officeDocument.x2006.docPropsVTypes.impl<br>org.openxmlformats.schemas.officeDocument.x2006.extendedProperties.impl<br>org.openxmlformats.schemas.officeDocument.x2006.relationships.impl<br>org.openxmlformats.schemas.presentationml.x2006.main.impl<br>org.openxmlformats.schemas.spreadsheetml.x2006.main.impl<br>org.openxmlformats.schemas.wordprocessingml.x2006.main.impl<br>org.openxmlformats.schemas.xpackage.x2006.contentTypes<br>org.openxmlformats.schemas.xpackage.x2006.contentTypes.impl<br>org.openxmlformats.schemas.xpackage.x2006.digitalSignature<br>org.openxmlformats.schemas.xpackage.x2006.digitalSignature.impl<br>org.openxmlformats.schemas.xpackage.x2006.metadata.coreProperties<br>org.openxmlformats.schemas.xpackage.x2006.metadata.coreProperties.impl<br>org.openxmlformats.schemas.xpackage.x2006.relationships<br>org.openxmlformats.schemas.xpackage.x2006.relationships.impl<br>com.adobe.internal.afml<br>com.adobe.internal.agm<br>com.adobe.internal.pdftoolkit.legacy.services.ap.es2<br>com.adobe.internal.pdftoolkit.legacy.services.ap.es3<br>com.adobe.internal.pdftoolkit.pdf.pieceinfo.compoundtype<br>com.adobe.internal.pdftoolkit.pdf.pieceinfo.editablepdf<br>com.adobe.internal.pdftoolkit.services.ap<br>com.adobe.internal.pdftoolkit.services.ap.annot<br>com.adobe.internal.pdftoolkit.services.ap.extension<br>com.adobe.internal.pdftoolkit.services.ap.impl<br>com.adobe.internal.pdftoolkit.services.ap.spi<br>com.adobe.internal.pdftoolkit.services.digsig<br>com.adobe.internal.pdftoolkit.services.digsig.cryptoprovider<br>com.adobe.internal.pdftoolkit.services.digsig.docmodanalysis<br>com.adobe.internal.pdftoolkit.services.digsig.spi<br>com.adobe.internal.pdftoolkit.services.fdf<br>com.adobe.internal.pdftoolkit.services.formflattener<br>com.adobe.internal.pdftoolkit.services.forms<br>com.adobe.internal.pdftoolkit.services.imageconversion<br>com.adobe.internal.pdftoolkit.services.javascript<br>com.adobe.internal.pdftoolkit.services.javascript.extension<br>com.adobe.internal.pdftoolkit.services.manipulations<br>com.adobe.internal.pdftoolkit.services.manipulations.impl<br>com.adobe.internal.pdftoolkit.services.optimizer<br>com.adobe.internal.pdftoolkit.services.pdfa<br>com.adobe.internal.pdftoolkit.services.pdfa.error<br>com.adobe.internal.pdftoolkit.services.pdfa2<br>com.adobe.internal.pdftoolkit.services.pdfa2.error<br>com.adobe.internal.pdftoolkit.services.pdfa2.error.codes<br>com.adobe.internal.pdftoolkit.services.pdfa3<br>com.adobe.internal.pdftoolkit.services.pdfport<br>com.adobe.internal.pdftoolkit.services.portfolio<br>com.adobe.internal.pdftoolkit.services.rcg<br>com.adobe.internal.pdftoolkit.services.rcg.impl<br>com.adobe.internal.pdftoolkit.services.redaction<br>com.adobe.internal.pdftoolkit.services.redaction.handler<br>com.adobe.internal.pdftoolkit.services.sanitization<br>com.adobe.internal.pdftoolkit.services.xbm<br>com.adobe.internal.pdftoolkit.services.xdp<br>com.adobe.internal.pdftoolkit.services.xfa<br>com.adobe.internal.pdftoolkit.services.xfa.form<br>com.adobe.internal.pdftoolkit.services.xfatext<br>com.adobe.internal.pdftoolkit.services.xfdf<br>com.adobe.internal.pdftoolkit.services.xobjhandler<br>com.adobe.internal.pdftoolkit.xml<br>com.adobe.octopus.extract<br>opennlp.tools.doccat<br>opennlp.tools.entitylinker<br>opennlp.tools.formats<br>opennlp.tools.formats.ad<br>opennlp.tools.formats.brat<br>opennlp.tools.formats.convert<br>opennlp.tools.formats.frenchtreebank<br>opennlp.tools.formats.muc<br>opennlp.tools.formats.ontonotes<br>opennlp.tools.lemmatizer<br>opennlp.tools.parser<br>opennlp.tools.parser.chunking<br>opennlp.tools.parser.lang.en<br>opennlp.tools.parser.lang.es<br>opennlp.tools.parser.treeinsert<br>opennlp.tools.sentdetect<br>opennlp.tools.sentdetect.lang<br>opennlp.tools.sentdetect.lang.th<br>opennlp.tools.stemmer<br>opennlp.tools.stemmer.snowball<br>opennlp.tools.tokenize.lang.en<br>org.apache.commons.imaging.color<br>org.apache.commons.imaging.common<br>org.apache.commons.imaging.common.itu_t4<br>org.apache.commons.imaging.common.mylzw<br>org.apache.commons.imaging.formats.bmp<br>org.apache.commons.imaging.formats.dcx<br>org.apache.commons.imaging.formats.gif<br>org.apache.commons.imaging.formats.icns<br>org.apache.commons.imaging.formats.ico<br>org.apache.commons.imaging.formats.jpeg<br>org.apache.commons.imaging.formats.jpeg.decoder<br>org.apache.commons.imaging.formats.jpeg.exif<br>org.apache.commons.imaging.formats.jpeg.iptc<br>org.apache.commons.imaging.formats.jpeg.segments<br>org.apache.commons.imaging.formats.jpeg.xmp<br>org.apache.commons.imaging.formats.pcx<br>org.apache.commons.imaging.formats.png<br>org.apache.commons.imaging.formats.png.chunks<br>org.apache.commons.imaging.formats.png.scanlinefilters<br>org.apache.commons.imaging.formats.png.transparencyfilters<br>org.apache.commons.imaging.formats.pnm<br>org.apache.commons.imaging.formats.psd<br>org.apache.commons.imaging.formats.psd.dataparsers<br>org.apache.commons.imaging.formats.psd.datareaders<br>org.apache.commons.imaging.formats.rgbe<br>org.apache.commons.imaging.formats.tiff<br>org.apache.commons.imaging.formats.tiff.constants<br>org.apache.commons.imaging.formats.tiff.datareaders<br>org.apache.commons.imaging.formats.tiff.fieldtypes<br>org.apache.commons.imaging.formats.tiff.photometricinterpreters<br>org.apache.commons.imaging.formats.tiff.taginfos<br>org.apache.commons.imaging.formats.tiff.write<br>org.apache.commons.imaging.formats.wbmp<br>org.apache.commons.imaging.formats.xbm<br>org.apache.commons.imaging.formats.xpm<br>org.apache.commons.imaging.icc<br>org.apache.commons.imaging.palette<br>org.apache.commons.imaging.util<br>com.adobe.dam.print.ids.utils<br>com.day.cq.dam.api.reporting<br>com.day.cq.dam.entitlement.api<br>com.day.cq.dam.handler.standard.epub<br>com.day.cq.dam.handler.standard.keynote<br>com.day.cq.dam.handler.standard.mp3<br>com.day.cq.dam.handler.standard.msoffice<br>com.day.cq.dam.handler.standard.msoffice.wmf<br>com.day.cq.dam.handler.standard.ooxml<br>com.day.cq.dam.handler.standard.pdf<br>com.day.cq.dam.handler.standard.pict<br>com.day.cq.dam.handler.standard.ps<br>com.day.cq.dam.handler.standard.psd<br>com.day.cq.dam.handler.standard.zip<br>com.day.cq.dam.word.extraction<br>com.day.cq.dam.word.process<br>com.adobe.xmp.worker.files<br>com.adobe.cq.address.api<br>com.adobe.cq.address.api.location<br>com.day.cq.mcm.emailprovider.impl.types<br>com.day.io<br>com.day.io.disk<br>com.day.io.file<br>org.apache.commons.exec.environment<br>org.apache.commons.exec.launcher<br>org.apache.commons.exec.util<br>com.google.zxing<br>com.google.zxing.common<br>com.google.zxing.common.reedsolomon<br>com.google.zxing.qrcode.decoder<br>com.google.zxing.qrcode.encoder<br>com.adobe.cq.dam.dm.internalapi.image_server<br>com.day.cq.dam.api.s7dam.jobs<br>com.day.cq.dam.api.s7dam.omnisearch<br>com.day.cq.dam.api.s7dam.scene7<br>com.day.cq.dam.scene7<br>com.day.cq.dam.scene7.api.net<br>com.day.cq.analytics.sitecatalyst.rsmerger<br>com.day.cq.searchpromote<br>com.day.cq.searchpromote.xml<br>com.day.cq.searchpromote.xml.form<br>com.day.cq.searchpromote.xml.result&gt;</td>
    <td>Äldre AEM 6.x API.</td>
  </tr>
  <tr>
    <td>org.apache.sling.discovery.commons<br>org.apache.sling.discovery.commons.providers<br>org.apache.sling.discovery.commons.providers.base<br>org.apache.sling.discovery.commons.providers.spi<br>org.apache.sling.discovery.commons.providers.spi.base<br>org.apache.sling.discovery.commons.providers.util</td>
    <td>Detta API stöds inte i Cloud Service.</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.vault.util.xml<br>org.apache.jackrabbit.vault.util.xml.serialize</td>
    <td>Util-klasser som är relaterade till Apache Xerces tas bort i efterföljande versioner, vilket orsakar en större versionsändring. Eftersom de här verktygen är avsedda för intern användning i File-valvet, kommer API:t att bli inaktuellt från den offentliga API-ytan.</td>
  </tr>
  <tr>
    <td>org.apache.sling.atom.taglib<br>org.apache.sling.atom.taglib.media</td>
    <td>Äldre AEM 6.x API. <a href="#org.apache.abdera_or_org.apache.sling.atom.taglib">Se borttagningsanteckningar nedan.</a></td>
  </tr>
  <tr>
    <td>org.apache.sling.commons.log.logback<br>org.apache.sling.commons.log.logback.webconsole</td>
    <td>AEM as a Cloud Service stöder inte detta interna API för återloggning.</td>
  </tr>
  <tr>
    <td>com.github.jknack.handlebars.js</td>
    <td>Uppgradering av handtag krävs från 4.0.5 till 4.3.0 på grund av en säkerhetslucka. Paketet finns inte längre i de uppgraderade verktygsfälten.</td>
  </tr>
  <tr>
    <td>com.adobe.granite.resourceresolverhelper</td>
    <td>Detta API stöds inte längre. Använd org.apache.sling.api.resource.ResourceResolverFactory i stället.</td>
  </tr>
  <tr>
    <td>org.apache.sling.repoinit.jcr<br>org.apache.sling.repoinit.parser.operations</td>
    <td>Användning av detta API stöds inte i AEM as a Cloud Service.</td>
  </tr>
  <tr>
    <td>org.apache.jackrabbit.oak.cache</td>
    <td>Detta API är endast internt.</td>
  </tr>
</tbody>
</table>
</details>

### Tar bort `org.apache.sling.commons.auth*` {#org.apache.sling.commons.auth}

Om du använder `org.apache.sling.commons.auth`, `org.apache.sling.commons.auth.spi`, eller båda, kan användningen ersättas genom att du migrerar koden till `org.apache.sling.auth`-svar. `org.apache.sling.auth.spi`. Om du använder en gammal version av [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/) måste du uppdatera till den senaste versionen.

Åtgärdslista:

* Uppdatera ACS AEM Commons till den senaste versionen (minst 6.11.0)
* Migrera från `org.apache.sling.commons.auth` och/eller `org.apache.sling.commons.auth.spi` till `org.apache.sling.auth`. `org.apache.sling.auth.spi`.

### Tar bort `org.apache.felix.webconsole*` {#org.apache.felix.webconsole}

Om du använder paket från `org.apache.felix.webconsole*` tar du bort den här koden från ditt projekt. Webbkonsolen är inte tillgänglig i Cloud Service.

Åtgärdslista:

* Ta bort kod med paket från `org.apache.felix.webconsole*`

### Tar bort `org.eclipse.jetty*` {#org.eclipse.jetty}

Om du använder något från paketet `org.eclipse.jetty` eller något av dess underpaket kanske du vill migrera till andra tredjepartsbibliotek med liknande funktioner. Om migrering inte är möjlig lägger du till de paket som krävs från listan nedan i ditt projekt.

Åtgärdslista:

* Ersätt användning av `org.eclipse.jetty`-paket med andra tredjepartsbibliotek/egen kod eller
* Välj de paket som behövs från den här listan och lägg till dem i ditt projekt:
   * `org.eclipse.jetty:jetty-client:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-http:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-io:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-security:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-servlet:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-server:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-util:9.4.54.v20240208`
   * `org.eclipse.jetty:jetty-util-ajax:9.4.54.v20240208`

### Tar bort `com.mongodb` {#com.mongodb}

Lägg till Mongo-klient-API i ditt projekt.

Åtgärdslista:

* Lägg till det här paketet i ditt projekt
   * `org.mongodb:mongo-java-driver:3.12.7`

### Tar bort `Apache Commons Lang 2 and Apache Commons Collections 3` {#apache.commons}

Ta bort användningen av de icke underhållna Apache Commons-biblioteken och ersätt dem med användning av supportversionerna. I de flesta fall kräver detta bara att paketimporterna justeras, i vissa fall har bara klasser eller metoder fått ett nytt namn. Om du använder en gammal version av [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/) måste du uppdatera till den senaste versionen.

Åtgärdslista:

* Uppdatera ACS AEM Commons till den senaste versionen (minst 6.11.0)
* Ersätt importer av `org.apache.commons.lang*` med `org.apache.commons.lang3`
* Ersätt importer av `org.apache.commons.collections*` med `org.apache.commons.collecitons4`

### Användning av `org.apache.abdera*` och `org.apache.sling.atom.taglib` {#org.apache.abdera_or_org.apache.sling.atom.taglib}

Ersätt användningen av ett paket från `org.apache.abdera` och `org.apache.sling.atom.taglib` med ett tredjepartsbibliotek med liknande funktionalitet eller egen kod.

Åtgärdslista:

* Ersätt användningen av paket från `org.apache.abdera` och `org.apache.sling.atom.taglib` med andra bibliotek från tredje part/egen kod.

### Användning av `org.apache.felix.http.whiteboard` {#org.apache.felix.http.whiteboard}

Ersätt användningen av `org.apache.felix.http.whiteboard` med [OSGi Http Whiteboard](https://docs.osgi.org/specification/osgi.cmpn/7.0.0/service.http.whiteboard.html). Det officiella OSGi-API:t har liknande funktioner och oftast behöver du bara ändra tjänstregistreringsegenskaperna för att ersätta dem.

Åtgärdslista:

* Ersätt användningen av `org.apache.felix.http.whiteboard` med [OSGi Http Whiteboard](https://docs.osgi.org/specification/osgi.cmpn/7.0.0/service.http.whiteboard.html)

### Användning av `ch.qos.logback*` {#ch.qos.logback}

Återloggning stöds inte i Cloud Service. Ta bort all användning. Om du använder en gammal version av [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/) måste du uppdatera till den senaste versionen.

Åtgärdslista:

* Uppdatera ACS AEM Commons till den senaste versionen (minst 6.11.0)
* Ta bort koden med paket från `ch.qos.logback`

### Användning av `org.slf4j.event and org.slf4j.spi` {#org.slf4j}

Om du använder `org.slf4j.event` eller `org.slf4j.spi` tar du bort all användning av den. Om du använder en gammal version av [ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/) måste du uppdatera till den senaste versionen.

Åtgärdslista:

* Uppdatera ACS AEM Commons till den senaste versionen (minst 6.11.0)
* Ta bort koden med `org.slf4j.event` och `org.slf4j.spi`

### Användning av `org.apache.log4j` {#org.apache.log4j}

Om du använder `org.apache.log4j` växlar du till SLF4J (`org.slf4j`) eller Log4J 2.x (`org.apache.logging.log4j`).

Åtgärdslista:

* Ersätt användningen av `org.apache.log4j` med `org.slf4j` (rekommenderas) eller `org.apache.logging.log4j`

## OSGI-konfiguration {#osgi-configuration}

De två listorna nedan återspeglar konfigurationsytan för AEM as a Cloud Service OSGi och beskriver vad kunderna kan konfigurera.

1. Kundkoden får inte konfigurera de listade OSGi-konfigurationerna.
1. En lista över OSGi-konfigurationer vars egenskaper kan konfigureras, men måste följa de angivna verifieringsreglerna. Dessa regler omfattar huruvida deklarationen av egenskapen är obligatorisk, dess typ och i vissa fall dess tillåtna värdeintervall.

Kundkoden kan konfigurera OSGi-konfigurationer som inte finns med i listan.

Dessa regler valideras under Cloud Manager byggprocess. Ytterligare regler kan läggas till över tid och det förväntade datumet för verkställighet anges i tabellen. Kunderna förväntas följa dessa regler senast vid måldatumet. Om reglerna inte följs efter borttagningsdatumet genereras fel i Cloud Manager byggprocess. Maven-projekt bör innehålla [AEM as a Cloud Service SDK Build Analyzer Maven Plugin](https://experienceleague.adobe.com/en/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin) för att flagga OSGI-konfigurationsfel under lokal SDK-utveckling.

Ytterligare information om OSGI-konfigurationen finns på [den här platsen](/help/implementing/deploying/configuring-osgi.md).

+++OSGi-konfigurationer som inte kan ändras.

* **`org.apache.felix.webconsole.internal.servlet.OsgiManager`** (Anmälningsdatum: 2021-04-30, Kräftelsedatum: 2021-07-31)
* **`com.day.cq.auth.impl.cug.CugSupportImpl`** (Anmälningsdatum: 2021-04-30, Kräftelsedatum: 2021-07-31)
* **`com.day.cq.jcrclustersupport.ClusterStartLevelController`** (Anmälningsdatum: 2021-04-30, Kräftelsedatum: 2021-07-31)
* **`org.apache.felix.http (Factory)`** (Anmälningsdatum: 2021-04-30, Kräftelsedatum: 2021-07-31)
* **`org.apache.sling.jcr.davex.impl.servlets.SlingDavExServlet`** (Tillkännagivandedatum: 2021-08-25, Kräftelsedatum: 2021-08-26)
+++

+++OSGi-konfigurationer som omfattas av build-valideringsregler.

* **`org.apache.felix.eventadmin.impl.EventAdmin`** (Anmälningsdatum: 2021-04-30, Kräftelsedatum: 2021-07-31)
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
   * Obligatoriskt intervall: Måste innehålla minst `org.apache.felix*`, `org.apache.sling*`, `come.day*`, `com.adobe*`
* `org.apache.felix.eventadmin.IgnoreTopic`
   * Typ: strängmatris
* **`org.apache.felix.http`** (Anmälningsdatum: 2021-04-30, Kräftelsedatum: 2021-07-31)
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
* **`org.apache.sling.scripting.cache`** (Anmälningsdatum: 2021-04-30, Kräftelsedatum: 2021-07-31)
   * `org.apache.sling.scripting.cache.size`
      * Typ: heltal
      * Obligatoriskt intervall: >= 2048
   * `org.apache.sling.scripting.cache.additional_extensions`
      * Obligatoriskt
      * Typ: strängmatris
      * Obligatoriskt intervall: måste innehålla js
* **`com.day.cq.mailer.DefaultMailService`** (Anmälningsdatum: 2021-04-30, Kräftelsedatum: 2021-07-31)
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
* **`org.apache.sling.commons.log.LogManager.factory.config`** (Meddelande: 11/16/21, Kräftelsedatum: 2/16/21)
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

## Java runtime update to version 21 {#java-runtime-update-21}

Adobe Experience Manager as a Cloud Service går över till Java 21 runtime. För att säkerställa kompatibilitet är det viktigt att uppdatera biblioteksversionerna enligt [Runtime Requirements](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/build-environment-details.md#runtime-requirements).

<!-- (OLD Removed from here to end of topic 1/16/25 as per instruction in https://wiki.corp.adobe.com/pages/viewpage.action?pageId=3359689801) AEM as a Cloud Service will be moving to Java 21 runtime. In order to ensure compatibility, it is essential to make the following adjustments:

### Runtime Requirements

These adjustments are required to ensure compatibility with the Java 21 runtime. The libraries can be updated at any time as they are compatible with older versions of Java.

#### Minimum version of org.objectweb.asm {#org.objectweb.asm}

Update the usage of org.objectweb.asm to version 9.5 or higher to ensure support for newer JVM runtimes.

#### Minimum version of org.apache.groovy {#org.apache.groovy}

Update the usage of org.apache.groovy to version 4.0.22 or higher to ensure support for newer JVM runtimes.

This bundle can be indirectly included by adding third party dependencies such as the AEM Groovy Console.

### Build-time Requirements

These adjustments are required to allow building the project with newer versions of Java but not required for runtime compatibility. The Maven plug-ins can be updated at any time as they are compatible with older versions of Java.

#### Minimum version of bnd-maven-plugin {#bnd-maven-plugin}

Update the usage of bnd-maven-plugin to version 6.4.0 to ensure support for newer JVM runtimes. Versions 7 or higher are not compatible with Java 11 or lower so an upgrade to that version is not recommended at this time.

#### Minimum version of aemanalyser-maven-plugin {#aemanalyser-maven-plugin}

Update the usage of aemanalyser-maven-plugin to version 1.6.6 or higher to ensure support for newer JVM runtimes.

#### Minimum version of maven-bundle-plugin  {#maven-bundle-plugin}

Update the usage of maven-bundle-plugin to version 5.1.5 or higher to ensure support for newer JVM runtimes.

#### Update dependencies in maven-scr-plugin  {#maven-scr-plugin}

The `maven-scr-plugin` is not directly compatible with Java 17 and 21. However, it is possible to generate the descriptor files by updating the ASM dependency version within the plugin configuration, similar to the snippet below:

```
[source,xml]
 <project>
   ...
   <build>
     ...
     <plugins>
       ...
       <plugin>
         <groupId>org.apache.felix</groupId>
         <artifactId>maven-scr-plugin</artifactId>
         <version>1.26.4</version>
         <executions>
           <execution>
             <id>generate-scr-scrdescriptor</id>
             <goals>
               <goal>scr</goal>
             </goals>
           </execution>
         </executions>
         <dependencies>
           <dependency>
             <groupId>org.ow2.asm</groupId>
             <artifactId>asm-analysis</artifactId>
             <version>9.7.1</version>
             <scope>compile</scope>
           </dependency>
         </dependencies>
       </plugin>
       ...
     </plugins>
     ...
   </build>
   ...
 </project>
```
-->
