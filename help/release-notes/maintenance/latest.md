---
title: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 60952db4172b882b71a0b230fc8f4c27154e9cc0
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 1%

---

# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsutgåvan av Experience Manager as a Cloud Service.

## Utgåva 15977 {#release-15977}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 15977, som offentliggjordes den 19 april 2024. Den tidigare underhållsutgåvan släpptes 15939.

2024.4.0 Feature Activation (Aktivering av funktioner) innehåller alla funktioner som finns i den här underhållsversionen. Se [Roadmap för lanseringar av Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap) för mer information.

### Förbättringar {#enhancements-15977}

* GRANITE-51335: Optimera AEM hälsokontroll för att öka instansstabiliteten.

### Åtgärdade problem {#fixed-issues-15977}

* CQ-4357226: Korrigera regression i IMS-konfigurationer som stöder OAuth-autentiseringsuppgifter.
* GRANITE-51335: Ratelimit upgrade to 5.0.4 Fixed Felix Health Check registrations.

### Kända fel {#known-issues-15977}

* **(Endast för AEM Forms)** Efter installationen av underhållsutgåvan AEM Cloud Foundation 15977 återges fält med adaptiva formulär i fel ordning vid formulärutveckling och för publicerade formulär. Om du använder AEM Forms rekommenderar Adobe att du inte uppgraderar till version 15977 förrän problemet är löst i den kommande underhållsversionen. Om du gör det kan du undvika besvär.

### Föråldrade funktioner och API:er {#deprecated-15977}

* [Borttagning av JWT-autentiseringsuppgifter i Adobe Developer Console](/help/security/jwt-credentials-deprecation-in-adobe-developer-console.md)

* Från och med den 1 maj 2024 upphör Adobe Dynamic Media med stödet för följande:

   * SSL (Secure Socket Layer) 2.0
   * SSL 3.0
   * TLS (Transport Layer Security) 1.0 och 1.1
   * Följande svaga lärare i TLS 1.2:
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384`
      * `TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_RSA_WITH_AES_256_GCM_SHA384`
      * `TLS_RSA_WITH_AES_256_CBC_SHA256`
      * `TLS_RSA_WITH_AES_256_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_AES_128_GCM_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA256`
      * `TLS_RSA_WITH_AES_128_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_256_CBC_SHA`
      * `TLS_RSA_WITH_CAMELLIA_128_CBC_SHA`
      * `TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA`
      * `TLS_RSA_WITH_SDES_EDE_CBC_SHA`


Om du vill veta vad som är föråldrat eller borttaget i AEM as a Cloud Service kan du läsa [Föråldrade och borttagna funktioner och API:er](/help/release-notes/deprecated-removed-features.md).

### Inbäddade tekniker {#embedded-tech-15977}

| Teknik | Version | Länk |
|---|---|---|
| AEM Oak | 1.62.0 | [API för Oak API 1.62.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.62.0/index.html) |
| AEM SLING API | 2.27.2 | [API för Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTML | 1.4.20-1.4.0 | [HTML-mallens språkspecifikation](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | 2.24.6 | [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components) |
