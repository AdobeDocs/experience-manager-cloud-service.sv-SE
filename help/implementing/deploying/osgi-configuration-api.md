---
title: OSGi Configuration API
description: Beskrivning av AEM som en Cloud Service OSGi-konfigurationsyta
feature: Distribuerar
source-git-commit: 4be76f19c27aeab84de388106a440434a99a738c
workflow-type: tm+mt
source-wordcount: '389'
ht-degree: 0%

---


# OSGi Configuration API

De två listorna nedan visar AEM som en Cloud Service OSGi-konfigurationsyta och beskriver vad kunderna kan konfigurera.

1. En lista med OSGi-konfigurationer som inte får konfigureras av kundkoden
1. En lista över OSGi-konfigurationer vars egenskaper kan konfigureras, men måste följa de angivna verifieringsreglerna. Dessa regler omfattar huruvida deklarationen av egenskapen är obligatorisk, dess typ och i vissa fall dess tillåtna värdeintervall.

Om en OSGI-konfiguration inte anges kan den konfigureras med kundkod.

Dessa regler valideras under Cloud Managers byggprocess. Ytterligare regler kan läggas till över tid och det förväntade datumet för verkställighet anges i tabellen. Kunderna förväntas följa dessa regler senast vid måldatumet. Om reglerna inte följs efter borttagningsdatumet genereras fel i Cloud Manager-byggprocessen. Maven-projekt ska innehålla [AEM som en Cloud Service-SDK Build Analyzer Maven Plugin](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/build-analyzer-maven-plugin.html) för att flagga OSGI-konfigurationsfel under lokal SDK-utveckling.

Ytterligare information om OSGI-konfigurationen finns på [den här platsen](/help/implementing/deploying/configuring-osgi.md).

## OSGi-konfigurationer som inte kan ändras {#osgi-configurations-that-cannot-be-modified}

* **`org.apache.felix.webconsole.internal.servlet.OsgiManager`** (Anmälningsdatum: 2021-04-30: 7/31/2021)
* **`com.day.cq.auth.impl.cug.CugSupportImpl`** (Anmälningsdatum: 2021-04-30: 7/31/2021)
* **`com.day.cq.jcrclustersupport.ClusterStartLevelController`** (Anmälningsdatum: 2021-04-30: 7/31/2021)
* **`org.apache.felix.http (Factory)`** (Anmälningsdatum: 2021-04-30: 7/31/2021)

## OSGi-konfigurationer som omfattas av Build Validation Rules {#osgi-configurations-subject-to-build-validation-rules}

* **`org.apache.felix.eventadmin.impl.EventAdmin`** (Anmälningsdatum: 2021-04-30: 7/31/2021)
   * `org.apache.felix.eventadmin.ThreadPoolSize`
      * Typ: heltal
      * Obligatoriskt intervall: 2-100
   * `org.apache.felix.eventadmin.AsyncToSyncThreadRatio`
      * Typ: double
   * `org.apache.felix.eventadmin.Timeout`
      * Typ: heltal
   * `org.apache.felix.eventadmin.RequireTopic`
      * Typ: boolesk
   * `org.apache.felix.eventadmin.IgnoreTimeout`
      * Krävs
      * Typ: array med strängar
      * Obligatoriskt intervall: Måste innehålla minst `org.apache.felix*`, `org.apache.sling*`, `come.day*`, `com.adobe*`
   * `org.apache.felix.eventadmin.IgnoreTopic`
      * Typ: array med strängar
* **`org.apache.felix.http`** (Anmälningsdatum: 2021-04-30: 7/31/2021)
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
      * Typ: string
   * `org.eclipse.jetty.servlet.CheckingRemoteSessionIdEncoding`
      * Typ: boolesk
   * `org.eclipse.jetty.servlet.SessionCookie`
      * Typ: string
   * `org.eclipse.jetty.servlet.SessionDomain`
      * Typ: string
   * `org.eclipse.jetty.servlet.SessionPath`
      * Typ: string
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
      * Typ: string
   * `org.apache.felix.jetty.gzip.includedMethods`
      * Typ: array med strängar
   * `org.apache.felix.jetty.gzip.excludedMethods`
      * Typ: array med strängar
   * `org.apache.felix.jetty.gzip.includedPaths`
      * Typ: array med strängar
   * `org.apache.felix.jetty.gzip.excludedPaths`
      * Typ: array med strängar
   * `org.apache.felix.jetty.gzip.includedMimeTypes`
      * Typ: array med strängar
   * `org.apache.felix.jetty.gzip.excludedMimeTypes`
      * Typ: array med strängar
   * `org.apache.felix.http.session.invalidate`
      * Typ: boolesk
   * `org.apache.felix.http.session.container.attribute`
      * Typ: array med strängar
   * `org.apache.felix.http.session.uniqueid`
      * Typ: boolesk
* **`org.apache.sling.scripting.cache`** (Anmälningsdatum: 2021-04-30: 7/31/2021)
   * `org.apache.sling.scripting.cache.size`
      * Typ: heltal
      * Obligatoriskt intervall: >= 2048
   * `org.apache.sling.scripting.cache.additional_extensions`
      * Krävs
      * Typ: array med strängar
      * Obligatoriskt intervall: måste innehålla js
* **`com.day.cq.mailer.DefaultMailService`** (Anmälningsdatum: 2021-04-30: 7/31/2021)
   * `smtp.host`
      * Typ: string
   * `smtp.port`
      * Typ: heltal
      * Obligatoriskt intervall: 465, 587 eller 25
   * `smtp.user`
      * Typ: string
   * `smtp.password`
      * Typ: string
   * `from.address`
      * Typ: string
   * `smtp.ssl`
      * Typ: string
   * `smtp.starttls`
      * Typ: boolesk
   * `smtp.requiretls`
      * Typ: boolesk
   * `debug.email`
      * Typ: boolesk
   * `oauth.flow`
      * Typ: boolesk
