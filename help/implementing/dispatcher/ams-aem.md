---
title: Migrera Dispatcher-konfigurationen från AMS till AEM as a Cloud Service
description: Migrera Dispatcher-konfigurationen från AMS till AEM as a Cloud Service
feature: Dispatcher
exl-id: ff7397dd-b6e1-4d08-8e2d-d613af6b81b3
source-git-commit: 6023a13eb4ea0533ba2f6cd00fb9f824b08a3f4a
workflow-type: tm+mt
source-wordcount: '1499'
ht-degree: 4%

---

# Migrera Dispatcher-konfigurationen från AMS till AEM as a Cloud Service {#Dispatcher-in-the-cloud}

## De viktigaste skillnaderna mellan AMS Dispatcher och AEM as a Cloud Service {#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

Konfigurationen av Apache och Dispatcher i AEM as a Cloud Service liknar den i AMS. De viktigaste skillnaderna är:

* I AEM as a Cloud Service kanske vissa Apache-direktiv inte används (till exempel `Listen` eller `LogLevel`)
* På AEM as a Cloud Service kan endast vissa delar av Dispatcher-konfigurationen placeras i inkluderingsfiler och deras namn är viktigt. Du måste till exempel lägga in filterregler som du vill återanvända på olika värdar i en fil som kallas `filters/filters.any`. Mer information finns på referenssidan.
* På AEM as a Cloud Service finns det extra validering för att inte tillåta filterregler skrivna med `/glob` för att förhindra säkerhetsproblem. För `deny *` används i stället för `allow *` (som inte kan användas) har kunderna nytta av att köra Dispatcher lokalt och göra en testversion och ett fel. Loggarna visar exakt vilka vägar Dispatcher-filtren blockerar för att de ska kunna läggas till.
* På AEM as a Cloud Service rekommenderas [välja att använda det flexibla källäget för dispatcher-konfigurationen](/help/implementing/dispatcher/disp-overview.md#validation-debug) t.ex. för att använda konfigurationspipelines på webbnivå eller ha större flexibilitet vad gäller antal och struktur för konfigurationsfiler.

## Riktlinjer för migrering av dispatcher-konfiguration från AMS till AEM as a Cloud Service

Dispatcher-konfigurationsstrukturen har skillnader mellan Managed Services och AEM as a Cloud Service. Nedan visas en steg-för-steg-guide om hur du migrerar från AMS Dispatcher-konfiguration version 2 till AEM as a Cloud Service.

## Konvertera en AMS till en AEM som en Dispatcher-konfiguration för molntjänster

I följande avsnitt ges stegvisa instruktioner för hur du konverterar en AMS-konfiguration. Det förutsätter att du har ett arkiv med en struktur som liknar den som beskrivs i [Dispatcher-konfiguration för Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)

### Extrahera arkivet och ta bort ett eventuellt prefix

Extrahera arkivet till en mapp och se till att de omedelbara undermapparna börjar med `conf`, `conf.d`,
`conf.dispatcher.d` och `conf.modules.d`. Om de inte gör det flyttar du dem uppåt i hierarkin.

### Ta bort oanvända undermappar och filer

Ta bort undermappar `conf` och `conf.modules.d`och filer som matchar `conf.d/*.conf`.

### Ta bort alla virtuella värdar som inte är publicerade

Ta bort alla virtuella värdfiler i `conf.d/enabled_vhosts` som har `author`, `unhealthy`, `health`,
`lc` eller `flush` i namnet. Alla virtuella värdfiler i `conf.d/available_vhosts` som inte är länkade till kan också tas bort.

### Ta bort eller kommentera virtuell värd-sektioner som inte refererar till port 80

Om du fortfarande har avsnitt i dina virtuella värdfiler som endast refererar till andra portar än port 80, till exempel:

```
<VirtualHost *:443>
...
</VirtualHost>
```

ta bort eller kommentera dem. Programsatser i de här avsnitten bearbetas inte, men om du behåller dem kan du ändå redigera dem utan någon effekt, vilket är förvirrande.

### Kontrollera återskrivningar

Ange katalog `conf.d/rewrites`.

Ta bort alla namngivna filer `base_rewrite.rules` och `xforwarded_forcessl_rewrite.rules` och kom ihåg att ta bort `Include` programsatser i de virtuella värdfilerna som refererar till dem.

If `conf.d/rewrites` innehåller nu en enda fil, den bör byta namn till `rewrite.rules` och glöm inte att anpassa `Include` -programsatser som refererar till den filen även i den virtuella värdfilen.

Om mappen däremot innehåller flera, virtuella värdspecifika filer, ska innehållet kopieras till `Include` -programsats som refererar till dem i de virtuella värdfilerna.

### Kontrollera variabler

Ange katalog `conf.d/variables`.

Ta bort alla namngivna filer `ams_default.vars` och kom ihåg att ta bort `Include` programsatser i de virtuella värdfilerna som refererar till dem.

If `conf.d/variables` innehåller nu en enda fil, den bör byta namn till `custom.vars` och glöm inte att anpassa `Include` -programsatser som refererar till den filen även i den virtuella värdfilen.

Om mappen däremot innehåller flera, virtuella värdspecifika filer, ska innehållet kopieras till `Include` -programsats som refererar till dem i de virtuella värdfilerna.

### Ta bort tillåtelselista

Ta bort mappen `conf.d/whitelists` och ta bort `Include` programsatser i den virtuella värdfilen som refererar till en fil i den undermappen.

### Ersätt alla variabler som inte längre är tillgängliga

I alla virtuell värd-filer:

Byt namn `PUBLISH_DOCROOT` till `DOCROOT`
Ta bort avsnitt som refererar till variabler med namnet `DISP_ID`, `PUBLISH_FORCE_SSL` eller `PUBLISH_WHITELIST_ENABLED`

### Kontrollera ditt tillstånd genom att köra valideraren

Kör Dispatcher-valideraren i din katalog med `httpd` underkommando:

```
$ validator httpd .
```

Om du ser fel som handlar om saknade inkluderingsfiler ska du kontrollera om du har bytt namn på filerna korrekt.

Om Apache-direktiv som inte är tillåtslista visas tar du bort dem.

### Ta bort alla icke-publicerade servergrupper

Ta bort en servergruppsfil i `conf.dispatcher.d/enabled_farms` som har `author`, `unhealthy`, `health`,
`lc` eller `flush` i namnet. Alla gruppfiler i `conf.dispatcher.d/available_farms` som inte är länkade till kan också tas bort.

### Byt namn på gruppfiler

Alla gårdar i `conf.dispatcher.d/enabled_farms` måste byta namn för att matcha mönstret `*.farm`, t.ex. en servergruppsfil som kallas `customerX_farm.any` ska byta namn `customerX.farm`.

### Kontrollera cache

Ange katalog `conf.dispatcher.d/cache`.

Ta bort alla filer som har prefixet `ams_`.

If `conf.dispatcher.d/cache` är nu tomt, kopiera filen `conf.dispatcher.d/cache/rules.any`
från standardkonfigurationen för Dispatcher till den här mappen. Standardkonfigurationen för Dispatcher finns i mappen `src` av denna SDK. Glöm inte att anpassa
`$include` programsatser som refererar till `ams_*_cache.any` regelfiler i servergruppsfilerna också.

Om i stället `conf.dispatcher.d/cache` innehåller nu en enda fil med suffix `_cache.any`bör namnet ändras till `rules.any` och glöm inte att anpassa `$include` programsatser som refererar till den filen i servergruppsfilerna också.

Om mappen emellertid innehåller flera servergruppsspecifika filer med det mönstret, bör innehållet kopieras till `$include` programsats som refererar till dem i servergruppsfilerna.

Ta bort alla filer som har suffixet `_invalidate_allowed.any`.

Kopiera filen `conf.dispatcher.d/cache/default_invalidate_any` från AEM i Cloud Dispatcher-konfigurationen till den platsen.

I varje gruppfil tar du bort allt innehåll i `cache/allowedClients` och ersätta den med:

```
$include "../cache/default_invalidate.any"
```

### Kontrollera klientrubriker

Ange katalog `conf.dispatcher.d/clientheaders`.

Ta bort alla filer som har prefixet `ams_`.

If `conf.dispatcher.d/clientheaders` innehåller nu en enda fil med suffix `_clientheaders.any`bör namnet ändras till `clientheaders.any` och glöm inte att anpassa `$include` programsatser som refererar till den filen i servergruppsfilerna också.

Om mappen emellertid innehåller flera servergruppsspecifika filer med det mönstret, bör innehållet kopieras till `$include` programsats som refererar till dem i servergruppsfilerna.

Kopiera filen `conf.dispatcher/clientheaders/default_clientheaders.any` från standardkonfigurationen AEM as a Cloud Service Dispatcher till den platsen.

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

Ange katalog `conf.dispatcher.d/filters`.

Ta bort alla filer som har prefixet `ams_`.

If `conf.dispatcher.d/filters` innehåller nu en enda fil som namnet ska ändras till
`filters.any` och glöm inte att anpassa `$include` programsatser som refererar till den filen i servergruppsfilerna också.

Om mappen emellertid innehåller flera servergruppsspecifika filer med det mönstret, bör innehållet kopieras till `$include` programsats som refererar till dem i servergruppsfilerna.

Kopiera filen `conf.dispatcher/filters/default_filters.any` från standardkonfigurationen AEM as a Cloud Service Dispatcher till den platsen.

Ersätt eventuella filter med programsatser som ser ut så här i varje servergruppsfil:

```
$include "/etc/httpd/conf.dispatcher.d/filters/ams_publish_filters.any"
```

med programsatsen:

```
$include "../filters/default_filters.any"
```

### Kontrollera återgivningar

Ange katalog `conf.dispatcher.d/renders`.

Ta bort alla filer i den mappen.

Kopiera filen `conf.dispatcher.d/renders/default_renders.any` från standardkonfigurationen AEM as a Cloud Service Dispatcher till den platsen.

I varje gruppfil tar du bort allt innehåll i `renders` och ersätta den med:

```
$include "../renders/default_renders.any"
```

### Kontrollera virtuella värdar

Byta namn på katalogen `conf.dispatcher.d/vhosts` till `conf.dispatcher.d/virtualhosts` och ange det.

Ta bort alla filer som har prefixet `ams_`.

If `conf.dispatcher.d/virtualhosts` innehåller nu en enda fil som namnet ska ändras till
`virtualhosts.any` och glöm inte att anpassa `$include` programsatser som refererar till den filen i servergruppsfilerna också.

Om mappen emellertid innehåller flera servergruppsspecifika filer med det mönstret, bör innehållet kopieras till `$include` programsats som refererar till dem i servergruppsfilerna.

Kopiera filen `conf.dispatcher/virtualhosts/default_virtualhosts.any` från standardkonfigurationen AEM as a Cloud Service Dispatcher till den platsen.

Ersätt eventuella filter med programsatser som ser ut så här i varje servergruppsfil:

```
$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"
```

med programsatsen:

```
$include "../virtualhosts/default_virtualhosts.any"
```

### Kontrollera ditt tillstånd genom att köra valideraren

Kör AEM as a Cloud Service Dispatcher-valideraren i din katalog med `dispatcher` underkommando:

```
$ validator dispatcher .
```

Om du ser fel som handlar om saknade inkluderingsfiler ska du kontrollera om du har bytt namn på filerna korrekt.

Om felmeddelanden som rör en odefinierad variabel `PUBLISH_DOCROOT` visas, ändrar du namnet till `DOCROOT`.

Alla andra fel finns i felsökningsavsnittet i dokumentationen för valideringsverktyget.

### Testa konfigurationen med en lokal distribution (kräver installation av Docker)

Använda skriptet `docker_run.sh` I AEM as a Cloud Service Dispatcher Tools kan du testa att din konfiguration inte innehåller några andra fel som bara skulle visas i distributionen:

### Steg 1: Generera distributionsinformation med valideraren

```
validator full -d out .
```

Detta validerar den fullständiga konfigurationen och genererar distributionsinformation i `out`

### Steg 2: Starta Dispatcher i en dockningsbild med den distributionsinformationen

När AEM publiceringsserver körs på din macOS-dator och lyssnar på port 4503 kan du köra Dispatcher framför den servern enligt följande:

```
$ docker_run.sh out docker.for.mac.localhost:4503 8080
```

Detta startar behållaren och visar Apache på den lokala porten 8080.

### Använd din nya Dispatcher-konfiguration

Grattis! Om valideraren inte längre rapporterar något problem och dockningsbehållaren startar utan fel eller varningar kan du flytta konfigurationen till en `dispatcher/src` underkatalog till din Git-databas.

**Kunder som använder AMS Dispatcher-konfiguration version 1 bör kontakta kundsupport för att hjälpa dem att migrera från version 1 till version 2 så att instruktionerna ovan kan följas.**
