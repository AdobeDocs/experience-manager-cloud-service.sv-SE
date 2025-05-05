---
title: Migrera Dispatcher-konfigurationen från AMS till AEM as a Cloud Service
description: Migrera Dispatcher-konfigurationen från AMS till AEM as a Cloud Service
feature: Dispatcher
exl-id: ff7397dd-b6e1-4d08-8e2d-d613af6b81b3
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 4%

---

# Migrera Dispatcher-konfigurationen från AMS till AEM as a Cloud Service {#Dispatcher-in-the-cloud}

## De viktigaste skillnaderna mellan AMS Dispatcher och AEM as a Cloud Service {#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

Apache- och Dispatcher-konfigurationen i AEM as a Cloud Service liknar AMS. De viktigaste skillnaderna är:

* I AEM as a Cloud Service kanske vissa Apache-direktiv inte används (till exempel `Listen` eller `LogLevel`)
* I AEM as a Cloud Service kan endast vissa delar av Dispatcher-konfigurationen placeras i inkluderingsfiler och deras namn är viktigt. Filterregler som du vill återanvända på olika värdar måste till exempel läggas i en fil med namnet `filters/filters.any`. Mer information finns på referenssidan.
* I AEM as a Cloud Service finns det extra validering som förhindrar att filterregler som har skrivits med `/glob` tillåts för att förhindra säkerhetsproblem. Eftersom `deny *` används i stället för `allow *` (som inte kan användas) har kunderna nytta av att köra Dispatcher lokalt och göra en testversion och felsökning. Loggarna visar exakt vilka sökvägar Dispatcher-filtren blockerar för att de ska kunna läggas till.
* I AEM as a Cloud Service rekommenderas för närvarande [att du väljer att använda det flexibla källäget för dispatcherconfig](/help/implementing/dispatcher/disp-overview.md#validation-debug), t.ex. för att använda konfigurationspipelines på webbnivå eller för att få större flexibilitet vad gäller antal och struktur för konfigurationsfiler.

## Riktlinjer för migrering av dispatcherkonfiguration från AMS till AEM as a Cloud Service

Konfigurationsstrukturen för Dispatcher skiljer sig åt mellan Managed Services och AEM as a Cloud Service. Nedan visas en steg-för-steg-guide om hur du migrerar från AMS Dispatcher version 2 till AEM as a Cloud Service.

## Konvertera en AMS till en AEM som en Dispatcher-konfiguration för molntjänster

I följande avsnitt ges stegvisa instruktioner för hur du konverterar en AMS-konfiguration. Det förutsätter
att du har ett arkiv med en struktur som liknar den som beskrivs i [Cloud Manager Dispatcher-konfigurationen](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html?lang=sv-SE)

### Extrahera arkivet och ta bort ett eventuellt prefix

Extrahera arkivet till en mapp och kontrollera att de omedelbara undermapparna börjar med `conf`, `conf.d`,
`conf.dispatcher.d` och `conf.modules.d`. Om de inte gör det flyttar du dem uppåt i hierarkin.

### Ta bort oanvända undermappar och filer

Ta bort undermapparna `conf` och `conf.modules.d` och filer som matchar `conf.d/*.conf`.

### Ta bort alla virtuella värdar som inte är publicerade

Ta bort alla virtuella värdfiler i `conf.d/enabled_vhosts` som har `author`, `unhealthy`, `health`,
`lc` eller `flush` i namnet. Alla virtuella värdfiler i `conf.d/available_vhosts` som inte är
länkade till kan också tas bort.

### Ta bort eller kommentera virtuell värd-sektioner som inte refererar till port 80

Om du fortfarande har avsnitt i dina virtuella värdfiler som endast refererar till andra portar än port 80, till exempel:

```
<VirtualHost *:443>
...
</VirtualHost>
```

ta bort eller kommentera dem. Programsatserna i de här avsnitten kommer inte att bearbetas, men om du
Om du behåller dem kan det hända att du redigerar dem utan någon effekt, vilket är förvirrande.

### Kontrollera återskrivningar

Ange katalogen `conf.d/rewrites`.

Ta bort alla filer med namnen `base_rewrite.rules` och `xforwarded_forcessl_rewrite.rules` och kom ihåg att
ta bort `Include` -programsatser i de virtuella värdfilerna som refererar till dem.

Om `conf.d/rewrites` nu innehåller en enda fil bör namnet på den ändras till `rewrite.rules` och inte
glöm att anpassa `Include` -programsatserna som refererar till den filen i de virtuella värdfilerna också.

Om mappen emellertid innehåller flera, virtuella värdspecifika filer bör innehållet i dem vara
kopieras till programsatsen `Include` som refererar till dem i de virtuella värdfilerna.

### Kontrollera variabler

Ange katalogen `conf.d/variables`.

Ta bort alla filer med namnet `ams_default.vars` och kom ihåg att ta bort `Include`-satser i den virtuella
värdfiler som refererar till dem.

Om `conf.d/variables` nu innehåller en enda fil bör namnet på den ändras till `custom.vars` och inte
glöm att anpassa `Include` -programsatserna som refererar till den filen i de virtuella värdfilerna också.

Om mappen emellertid innehåller flera, virtuella värdspecifika filer bör innehållet i dem vara
kopieras till programsatsen `Include` som refererar till dem i de virtuella värdfilerna.

### Ta bort tillåtelselista

Ta bort mappen `conf.d/whitelists` och ta bort `Include`-satser i de virtuella värdfilerna som refererar till
en fil i den undermappen.

### Ersätt alla variabler som inte längre är tillgängliga

I alla virtuell värd-filer:

Byt namn på `PUBLISH_DOCROOT` till `DOCROOT`
Ta bort avsnitt som refererar till variabler med namnen `DISP_ID`, `PUBLISH_FORCE_SSL` eller `PUBLISH_WHITELIST_ENABLED`

### Kontrollera ditt tillstånd genom att köra valideraren

Kör Dispatcher-valideraren i din katalog med underkommandot `httpd`:

```
$ validator httpd .
```

Om du ser fel som handlar om saknade inkluderingsfiler ska du kontrollera om du har bytt namn på dem korrekt
filer.

Om Apache-direktiv som inte är tillåtslista visas tar du bort dem.

### Ta bort alla icke-publicerade servergrupper

Ta bort alla servergruppsfiler i `conf.dispatcher.d/enabled_farms` som har `author`, `unhealthy`, `health`,
`lc` eller `flush` i namnet. Alla gruppfiler i `conf.dispatcher.d/available_farms` som inte är
länkade till kan också tas bort.

### Byt namn på gruppfiler

Alla grupper i `conf.dispatcher.d/enabled_farms` måste byta namn för att matcha mönstret `*.farm`, så till exempel en
servergruppsfilen med namnet `customerX_farm.any` ska byta namn `customerX.farm`.

### Kontrollera cache

Ange katalogen `conf.dispatcher.d/cache`.

Ta bort alla filer som har prefixet `ams_`.

Om `conf.dispatcher.d/cache` nu är tomt kopierar du filen `conf.dispatcher.d/cache/rules.any`
från Dispatcher standardkonfiguration till den här mappen. Dispatcher
konfigurationen finns i mappen `src` för denna SDK. Glöm inte att anpassa
`$include`-programsatser som refererar till `ams_*_cache.any`-regelfilerna i servergruppsfilerna
också.

Om `conf.dispatcher.d/cache` nu innehåller en enda fil med suffixet `_cache.any`,
det ska byta namn till `rules.any` och glöm inte att anpassa `$include` -programsatserna
även referera till den filen i servergruppsfilerna.

Om mappen däremot innehåller flera, servergruppsspecifika filer med det mönstret, kommer deras innehåll att
ska kopieras till programsatsen `$include` som refererar till dem i servergruppsfilerna.

Ta bort alla filer som har suffixet `_invalidate_allowed.any`.

Kopiera filen `conf.dispatcher.d/cache/default_invalidate_any` från standardvärdet
AEM i Cloud Dispatcher-konfigurationen till den platsen.

Ta bort allt innehåll i avsnittet `cache/allowedClients` i varje servergruppsfil och ersätt det
med:

```
$include "../cache/default_invalidate.any"
```

### Kontrollera klientrubriker

Ange katalogen `conf.dispatcher.d/clientheaders`.

Ta bort alla filer som har prefixet `ams_`.

Om `conf.dispatcher.d/clientheaders` nu innehåller en enda fil med suffixet `_clientheaders.any`,
det ska byta namn till `clientheaders.any` och glöm inte att anpassa `$include` -programsatserna
även referera till den filen i servergruppsfilerna.

Om mappen däremot innehåller flera, servergruppsspecifika filer med det mönstret, kommer deras innehåll att
ska kopieras till programsatsen `$include` som refererar till dem i servergruppsfilerna.

Kopiera filen `conf.dispatcher/clientheaders/default_clientheaders.any` från standardvärdet
AEM as a Cloud Service Dispatcher-konfiguration till den platsen.

Ersätt alla inkluderingssatser för klienthuvuden i varje servergruppsfil som ser ut så här:

```
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_publish_clientheaders.any"
$include "/etc/httpd/conf.dispatcher.d/clientheaders/ams_common_clientheaders.any"
```

med programsatsen:

```
$include "../clientheaders/default_clientheaders.any"
```

### Kontrollera filter

Ange katalogen `conf.dispatcher.d/filters`.

Ta bort alla filer som har prefixet `ams_`.

Om `conf.dispatcher.d/filters` nu innehåller en enda fil bör namnet ändras till
`filters.any` och glöm inte att anpassa de `$include` -programsatser som refererar till det
i servergruppsfilerna också.

Om mappen däremot innehåller flera, servergruppsspecifika filer med det mönstret, kommer deras innehåll att
ska kopieras till programsatsen `$include` som refererar till dem i servergruppsfilerna.

Kopiera filen `conf.dispatcher/filters/default_filters.any` från standardvärdet
AEM as a Cloud Service Dispatcher-konfiguration till den platsen.

Ersätt eventuella filter med programsatser som ser ut så här i varje servergruppsfil:

```
$include "/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"
```

med programsatsen:

```
$include "../filters/default_filters.any"
```

### Kontrollera återgivningar

Ange katalogen `conf.dispatcher.d/renders`.

Ta bort alla filer i den mappen.

Kopiera filen `conf.dispatcher.d/renders/default_renders.any` från standardvärdet
AEM as a Cloud Service Dispatcher-konfiguration till den platsen.

Ta bort allt innehåll i avsnittet `renders` i varje servergruppsfil och ersätt det
med:

```
$include "../renders/default_renders.any"
```

### Kontrollera virtuella värdar

Byt namn på katalogen `conf.dispatcher.d/vhosts` till `conf.dispatcher.d/virtualhosts` och ange den.

Ta bort alla filer som har prefixet `ams_`.

Om `conf.dispatcher.d/virtualhosts` nu innehåller en enda fil bör namnet ändras till
`virtualhosts.any` och glöm inte att anpassa de `$include` -programsatser som refererar till det
i servergruppsfilerna också.

Om mappen däremot innehåller flera, servergruppsspecifika filer med det mönstret, kommer deras innehåll att
ska kopieras till programsatsen `$include` som refererar till dem i servergruppsfilerna.

Kopiera filen `conf.dispatcher/virtualhosts/default_virtualhosts.any` från standardvärdet
AEM as a Cloud Service Dispatcher-konfiguration till den platsen.

Ersätt eventuella filter med programsatser som ser ut så här i varje servergruppsfil:

```
$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"
```

med programsatsen:

```
$include "../virtualhosts/default_virtualhosts.any"
```

### Kontrollera ditt tillstånd genom att köra valideraren

Kör AEM as a Cloud Service Dispatcher-valideraren i din katalog med underkommandot `dispatcher`:

```
$ validator dispatcher .
```

Om du ser fel som handlar om saknade inkluderingsfiler ska du kontrollera om du har bytt namn på dem korrekt
filer.

Om felmeddelanden som rör en odefinierad variabel `PUBLISH_DOCROOT` visas, ändrar du namnet till `DOCROOT`.

Information om alla andra fel finns i avsnittet Felsökning i
dokumentation för valideringsverktyg.

### Testa konfigurationen med en lokal distribution (kräver installation av Docker)

Med skriptet `docker_run.sh` i AEM as a Cloud Service Dispatcher Tools kan du testa att
din konfiguration inte innehåller något annat fel som bara skulle visas i
distribution:

### Steg 1: Generera distributionsinformation med valideraren

```
validator full -d out .
```

Detta verifierar den fullständiga konfigurationen och genererar distributionsinformation i `out`

### Steg 2: Starta Dispatcher i en dockningsbild med den distributionsinformationen

När AEM publiceringsserver körs på din macOS-dator, lyssnar på port 4503,
Du kan köra Dispatcher framför den servern enligt följande:

```
$ docker_run.sh out docker.for.mac.localhost:4503 8080
```

Detta startar behållaren och visar Apache på den lokala porten 8080.

### Använd din nya Dispatcher-konfiguration

Grattis! Om valideraren inte längre rapporterar något problem och
dockningsbehållaren startas utan fel eller varningar. Du är
redo att flytta konfigurationen till en `dispatcher/src`-underkatalog
av din Git-databas.

**Kunder som använder AMS Dispatcher-konfigurationversion 1 bör kontakta kundsupport för att hjälpa dem att migrera från version 1 till version 2 så att instruktionerna ovan kan följas.**
