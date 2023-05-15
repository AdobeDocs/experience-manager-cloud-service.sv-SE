---
title: Dispatcher i molnet
description: Dispatcher i molnet
feature: Dispatcher
exl-id: 6d78026b-687e-434e-b59d-9d101349a707
source-git-commit: 98eff568686c72c626d2bf77d82e8c3f224eda42
workflow-type: tm+mt
source-wordcount: '983'
ht-degree: 1%

---

# Dispatcher i molnet {#Dispatcher-in-the-cloud}

>[!CONTEXTUALHELP]
>id="aemcloud_nonbpa_dispoverview"
>title="Dispatcher i molnet"
>abstract="Den här sidan beskriver hur du hämtar och extraherar Dispatcher-verktygen, de Apache-moduler som stöds och ger en översikt på hög nivå över de äldre och flexibla lägena."

## Introduktion {#apache-and-dispatcher-configuration-and-testing}

På den här sidan beskrivs Dispatcher-verktygen och hur du hämtar och extraherar dem, de Apache-moduler som stöds och en översikt över de äldre och flexibla lägena. Det finns också ytterligare referenser för validering och felsökning och migrering av Dispatcher-konfigurationen från AMS till AEM as a Cloud Service. <!-- ERROR: NOT FOUND (HTTP ERROR 404) Also, see [this video](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-5/cloud5-aem-dispatcher-cloud.html) for additional details about deploying dispatcher files in a cloud service environment. -->

## Dispatcher Tools {#dispatcher-sdk}

Dispatcher-verktygen är en del av den övergripande AEM as a Cloud Service SDK:n och tillhandahåller:

* En vaniljfilstruktur som innehåller de konfigurationsfiler som ska inkluderas i ett maven-projekt för Dispatcher.
* Verktyg för kunder för att verifiera att Dispatcher-konfigurationen bara innehåller AEM direktiv som stöds as a Cloud Service. Verktyget validerar också att syntaxen är korrekt så att Apache kan startas utan problem.
* En Docker-bild som öppnar Dispatcher lokalt.

## Hämta och extrahera verktygen {#extracting-the-sdk}

Dispatcher Tools, en del av [AEM as a Cloud Service SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md), kan laddas ned från en zip-fil i [Programvarudistribution](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html) portal. Alla nya konfigurationer som är tillgängliga i den nya versionen av Dispatcher Tools kan användas för att distribuera till molnmiljöer som kör den versionen av AEM i molnet eller senare.

Zippa upp SDK, som innehåller Dispatcher Tools för macOS, Linux® och Windows.

**För macOS/Linux**, gör att artefakten för verktyget Dispatcher kan köras. Det extraherar Dispatcher Tools-filerna under katalogen som du lagrade dem till (där `version` är versionen av Dispatcher Tools).

```bash
$ chmod +x aem-sdk-dispatcher-tools-<version>-unix.sh
$ ./aem-sdk-dispatcher-tools-<version>-unix.sh
Verifying archive integrity...  100%   All good.
Uncompressing aem-sdk-dispatcher-tools-<version>-unix.sh 100%
```

**För Windows**, extrahera zip-arkivet för Dispatcher Tooling.

## Validera och felsöka med Dispatcher Tools {#validation-debug}

Dispatcher-verktygen används för att validera och felsöka projektets Dispatcher-konfiguration. Lär dig mer om hur du använder dessa verktyg på de sidor som refereras nedan, baserat på om projektets Dispatcher-konfiguration är strukturerad i flexibelt läge eller äldre läge:

* **Flexibelt läge** - det rekommenderade läget och standardvärdet för [AEM 28](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html?lang=en) och senare, som också används av Cloud Manager för nya miljöer som skapats efter Cloud Manager 2021.7.0. Kunder kan aktivera det här läget genom att lägga till mappen och filen `opt-in/USE_SOURCES_DIRECTLY`. Om du använder det här mer flexibla läget finns det inga begränsningar i filstrukturen i mappen för omskrivning som i det äldre läget krävde en enda `rewrite.rules` -fil. Det finns heller ingen begränsning för hur många regler du kan lägga till. Mer information om mappstruktur och lokal validering finns i [Validera och felsöka med Dispatcher Tools](/help/implementing/dispatcher/validation-debug.md).

* **Äldre läge** - mer information om mappstrukturen och lokal validering för äldre Dispatcher-konfigurationsläge finns i [Validera och felsöka med Dispatcher Tools (äldre)](/help/implementing/dispatcher/validation-debug-legacy.md)

Mer information om hur du migrerar från den äldre konfigurationsmodellen till den mer flexibla, finns i AEM 28 och framåt. [den här dokumentationen](/help/implementing/dispatcher/validation-debug.md#migrating).

## Disposition av innehåll {#content-disposition}

För publiceringsskiktet är standardinställningen för att visa blober som en bifogad fil. Åsidosätt den här inställningen med standardinställningen [dispositionshuvud för innehåll](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Disposition) i Dispatcher.

Nedan visas ett exempel på hur konfigurationen ska se ut:

```
<LocationMatch "^\/content\/dam.*\.(pdf).*">
 Header unset Content-Disposition
 Header set Content-Disposition inline
</LocationMatch>
```

## Apache-moduler som stöds {#supported-directives}

Tabellen nedan visar vilka Apache-moduler som stöds:

| Modulnamn | Referenssida |
|---|---|
| `core` | [https://httpd.apache.org/docs/2.4/mod/core.html](https://httpd.apache.org/docs/2.4/mod/core.html) |
| `mod_access_compat` | [https://httpd.apache.org/docs/2.4/mod/mod_access_compat.html](https://httpd.apache.org/docs/2.4/mod/mod_access_compat.html) |
| `mod_alias` | [https://httpd.apache.org/docs/2.4/mod/mod_alias.html](https://httpd.apache.org/docs/2.4/mod/mod_alias.html) |
| `mod_allowmethods` | [https://httpd.apache.org/docs/2.4/mod/mod_allowmethods.html](https://httpd.apache.org/docs/2.4/mod/mod_allowmethods.html) |
| `mod_authn_core` | [https://httpd.apache.org/docs/2.4/mod/mod_authn_core.html](https://httpd.apache.org/docs/2.4/mod/mod_authn_core.html) |
| `mod_authn_file` | [https://httpd.apache.org/docs/2.4/mod/core.html](https://httpd.apache.org/docs/2.4/mod/mod_authn_file.html) |
| `mod_authz_core` | [https://httpd.apache.org/docs/2.4/mod/core.html](https://httpd.apache.org/docs/2.4/mod/mod_authz_core.html) |
| `mod_authz_groupfile` | [https://httpd.apache.org/docs/2.4/mod/mod_authz_groupfile.html](https://httpd.apache.org/docs/2.4/mod/mod_authz_groupfile.html) |
| `mod_deflate` | [https://httpd.apache.org/docs/2.4/mod/mod_deflate.html](https://httpd.apache.org/docs/2.4/mod/mod_deflate.html) |
| `mod_dir` | [https://httpd.apache.org/docs/2.4/mod/mod_dir.html](https://httpd.apache.org/docs/2.4/mod/mod_dir.html) |
| `mod_env` | [https://httpd.apache.org/docs/2.4/mod/mod_env.html](https://httpd.apache.org/docs/2.4/mod/mod_env.html) |
| `mod_filter` | [https://httpd.apache.org/docs/2.4/mod/mod_filter.html](https://httpd.apache.org/docs/2.4/mod/mod_filter.html) |
| `mod_headers` | [https://httpd.apache.org/docs/2.4/mod/mod_headers.html](https://httpd.apache.org/docs/2.4/mod/mod_headers.html) |
| `mod_mime` | [https://httpd.apache.org/docs/2.4/mod/mod_mime.html](https://httpd.apache.org/docs/2.4/mod/mod_mime.html) |
| `mod_proxy` | [https://httpd.apache.org/docs/2.4/mod/mod_proxy.html](https://httpd.apache.org/docs/2.4/mod/mod_proxy.html) |
| `mod_proxy_http` | [https://httpd.apache.org/docs/2.4/mod/mod_proxy_http.html](https://httpd.apache.org/docs/2.4/mod/mod_proxy_http.html) |
| `mod_remoteip` | [https://httpd.apache.org/docs/2.4/mod/mod_remoteip.html](https://httpd.apache.org/docs/2.4/mod/mod_remoteip.html) |
| `mod_reqtimeout` | [https://httpd.apache.org/docs/2.4/mod/mod_reqtimeout.html](https://httpd.apache.org/docs/2.4/mod/mod_reqtimeout.html) |
| `mod_rewrite` | [https://httpd.apache.org/docs/2.4/mod/mod_rewrite.html](https://httpd.apache.org/docs/2.4/mod/mod_rewrite.html) |
| `mod_security` | [https://modsecurity.org/](https://modsecurity.org/) |
| `mod_setenvif` | [https://httpd.apache.org/docs/2.4/mod/mod_setenvif.html](https://httpd.apache.org/docs/2.4/mod/mod_setenvif.html) |
| `mod_ssl (only the SSLProxyEngine directive)` | [https://httpd.apache.org/docs/2.4/mod/mod_ssl.html#sslproxyengine](https://httpd.apache.org/docs/2.4/mod/mod_ssl.html#sslproxyengine) |
| `mod_substitute` | [https://httpd.apache.org/docs/2.4/mod/mod_substitute.html](https://httpd.apache.org/docs/2.4/mod/mod_substitute.html) |
| `mod_userdir` | [https://httpd.apache.org/docs/2.4/mod/mod_userdir.html](https://httpd.apache.org/docs/2.4/mod/mod_userdir.html) |
| `mod_macro` | [https://httpd.apache.org/docs/2.4/mod/mod_macro.html](https://httpd.apache.org/docs/2.4/mod/mod_macro.html) |
| `mod_include (no directives supported)` | [https://httpd.apache.org/docs/2.4/mod/mod_include.html](https://httpd.apache.org/docs/2.4/mod/mod_include.html) |


Kunder kan inte lägga till godtyckliga moduler, men ytterligare moduler kan övervägas för framtida införande. Kunder kan hitta listan över direktiv som är tillgängliga för en viss Dispatcher-version genom att köra validerarens tillåtslista-kommando i SDK:n.

De direktiv som är tillåtna i Apache-konfigurationsfiler kan listas genom att köra validerarens tillåtelselista-kommando:

```
$ validator allowlist
Cloud manager validator 2.0.4
 
Allowlisted directives:
  <Directory>
  ...
  
```

## Mappstruktur {#folder-structure}

Projektets mappstruktur Apache och Dispatcher skiljer sig något åt beroende på vilket läge projektet använder, vilket beskrivs i [Validera och felsöka med Dispatcher Tools](#validation-debug) ovan.

## Migrera Dispatcher-konfigurationen från AMS {#ams-aem}

Mer information om hur du migrerar Dispatcher-konfigurationen från AMS till AEM as a Cloud Service finns i [Migrera Dispatcher-konfigurationen från AMS till AEM](/help/implementing/dispatcher/ams-aem.md) as a Cloud Service sida.
