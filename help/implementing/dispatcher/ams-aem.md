---
title: Migrera Dispatcher-konfigurationen från AMS till AEM som Cloud Service
description: 'Migrera Dispatcher-konfigurationen från AMS till AEM som Cloud Service '
feature: Dispatcher
source-git-commit: 19444aacbb86f93e7a5ea8bda2ca3c03a0a44f98
workflow-type: tm+mt
source-wordcount: '1447'
ht-degree: 14%

---

# Migrera Dispatcher-konfigurationen från AMS till AEM som Cloud Service {#Dispatcher-in-the-cloud}

## De viktigaste skillnaderna mellan AMS Dispatcher och AEM som en Cloud Service {#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

Konfigurationen Apache och Dispatcher i AEM som Cloud Service liknar den i AMS. De viktigaste skillnaderna är:

* I AEM som Cloud Service kan vissa Apache-direktiv inte användas (till exempel `Listen` eller `LogLevel`)
* I AEM som Cloud Service kan endast vissa delar av Dispatcher-konfigurationen placeras i inkluderingsfiler och deras namn är viktigt. Filterregler som du vill återanvända på olika värdar måste till exempel läggas i en fil med namnet `filters/filters.any`. Mer information finns på referenssidan.
* I AEM som Cloud Service finns det extra validering för att förhindra att filterregler skrivs med `/glob` för att förhindra säkerhetsproblem. Eftersom `deny *` kommer att användas i stället för `allow *` (som inte kan användas) har kunderna nytta av att köra Dispatcher lokalt och göra testversionen och felsökningen. Loggarna visar exakt vilka sökvägar Dispatcher-filtren blockerar för att dessa ska kunna läggas till.

## Riktlinjer för att migrera dispatcher-konfiguration från AMS till AEM som Cloud Service

Dispatcher-konfigurationsstrukturen har skillnader mellan Managed Services och AEM som en Cloud Service. Nedan visas en steg-för-steg-guide om hur du migrerar från AMS Dispatcher-konfiguration version 2 till AEM som Cloud Service.

## Konvertera en AMS till en AEM som en Dispatcher-konfiguration för molntjänster

I följande avsnitt ges stegvisa instruktioner för hur du konverterar en AMS-konfiguration. Det förutsätter
att du har ett arkiv med en struktur som liknar den som beskrivs i [Cloud Manager Dispatcher configuration](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)

### Extrahera arkivet och ta bort ett eventuellt prefix

Extrahera arkivet till en mapp och se till att de omedelbara undermapparna börjar med `conf`, `conf.d`,
`conf.dispatcher.d` och `conf.modules.d`. Om de inte gör det flyttar du dem uppåt i hierarkin.

### Ta bort oanvända undermappar och filer

Ta bort undermappar `conf` och `conf.modules.d`, samt filer som matchar `conf.d/*.conf`.

### Ta bort alla virtuella värdar som inte är publicerade 

Ta bort alla virtuella värdfiler i `conf.d/enabled_vhosts` som har `author`, `unhealthy`, `health`,
`lc` eller `flush` i namnet. Alla virtuella värdfiler i `conf.d/available_vhosts` som inte
som är länkade till kan också tas bort.

### Ta bort eller kommentera virtuell värd-sektioner som inte refererar till port 80

Om du fortfarande har avsnitt i dina virtuella värdfiler som endast refererar till andra portar än port 80, till exempel:

```
<VirtualHost *:443>
...
</VirtualHost>
```

ska du ta bort eller kommentera dem. Programsatser i de här avsnitten bearbetas inte, men om du behåller dem kan du ändå redigera dem utan någon effekt, vilket är förvirrande.

### Kontrollera återskrivningar

Ange katalogen `conf.d/rewrites`.

Ta bort alla filer med namnen `base_rewrite.rules` och `xforwarded_forcessl_rewrite.rules` och kom ihåg att
ta bort `Include`-satser i de virtuella värdfilerna som refererar till dem.

Om `conf.d/rewrites` nu innehåller en enda fil bör namnet på den ändras till `rewrite.rules` och inte
Glöm inte att anpassa `Include`-programsatserna som refererar till den filen i de virtuella värdfilerna också.

Om mappen emellertid innehåller flera, virtuella värdspecifika filer bör innehållet i dem vara
kopieras till `Include`-satsen som refererar till dem i de virtuella värdfilerna.

### Kontrollera variabler

Ange katalogen `conf.d/variables`.

Ta bort en fil med namnet `ams_default.vars` och kom ihåg att ta bort `Include`-satser i den virtuella
värdfiler som refererar till dem.

Om `conf.d/variables` nu innehåller en enda fil bör namnet på den ändras till `custom.vars` och inte
Glöm inte att anpassa `Include`-programsatserna som refererar till den filen i de virtuella värdfilerna också.

Om mappen emellertid innehåller flera, virtuella värdspecifika filer bör innehållet i dem vara
kopieras till `Include`-satsen som refererar till dem i de virtuella värdfilerna.

### Ta bort tillåtelselista

Ta bort mappen `conf.d/whitelists` och ta bort `Include`-satser i de virtuella värdfilerna som refererar till
en fil i den undermappen.

### Ersätt alla variabler som inte längre är tillgängliga

I alla virtuell värd-filer:

Byt namn på `PUBLISH_DOCROOT` till `DOCROOT`
Ta bort avsnitt som refererar till variabler med namnen `DISP_ID`, `PUBLISH_FORCE_SSL` eller `PUBLISH_WHITELIST_ENABLED`

### Kontrollera status genom att köra valideraren

Kör Dispatcher-valideraren i din katalog med underkommandot `httpd`:

```
$ validator httpd .
```

Om felmeddelanden om saknade inkluderingsfiler visas, ska du kontrollera om du har bytt namn på filerna korrekt.

Om Apache-direktiv som inte är tillåtslista visas tar du bort dem.

### Ta bort alla icke-publicerade servergrupper

Ta bort alla servergruppsfiler i `conf.dispatcher.d/enabled_farms` som har `author`, `unhealthy`, `health`,
`lc` eller `flush` i namnet. Alla servergruppsfiler i `conf.dispatcher.d/available_farms` som inte
som är länkade till kan också tas bort.

### Byta namn på servergruppsfiler

Alla grupper i `conf.d/enabled_farms` måste byta namn för att matcha mönstret `*.farm`, så t.ex. a
servergruppsfilen `customerX_farm.any` ska byta namn på `customerX.farm`.

### Kontrollera cache

Ange katalogen `conf.dispatcher.d/cache`.

Ta bort alla filer som har prefixet `ams_`.

Om `conf.dispatcher.d/cache` nu är tomt kopierar du filen `conf.dispatcher.d/cache/rules.any`
från standardkonfigurationen för Dispatcher till den här mappen. Standardutskickaren
finns i mappen `src` för denna SDK. Glöm inte att anpassa
`$include`-satser som refererar till regelfilerna `ams_*_cache.any` i servergruppsfilerna
också.

Om i stället `conf.dispatcher.d/cache` nu innehåller en enda fil med suffixet `_cache.any`,
det ska byta namn till `rules.any` och glöm inte att anpassa `$include`-programsatserna
även referera till den filen i servergruppsfilerna.

Om mappen däremot innehåller flera, gruppspecifika filer med det mönstret, kommer deras innehåll att
ska kopieras till `$include`-satsen som refererar till dem i servergruppsfilerna.

Ta bort alla filer som har suffixet `_invalidate_allowed.any`.

Kopiera filen `conf.dispatcher.d/cache/default_invalidate_any` från standardvärdet
AEM i Cloud Dispatcher-konfigurationen till den platsen.

I varje servergruppsfil tar du bort allt innehåll i `cache/allowedClients`-avsnittet och ersätter det
med:

```
$include "../cache/default_invalidate.any"
```

### Kontrollera klientrubriker

Ange katalogen `conf.dispatcher.d/clientheaders`.

Ta bort alla filer som har prefixet `ams_`.

Om `conf.dispatcher.d/clientheaders` nu innehåller en enda fil med suffixet `_clientheaders.any`,
det ska byta namn till `clientheaders.any` och glöm inte att anpassa `$include`-programsatserna
även referera till den filen i servergruppsfilerna.

Om mappen däremot innehåller flera, gruppspecifika filer med det mönstret, kommer deras innehåll att
ska kopieras till `$include`-satsen som refererar till dem i servergruppsfilerna.

Kopiera filen `conf.dispatcher/clientheaders/default_clientheaders.any` från standardvärdet
AEM som en Cloud Service Dispatcher-konfiguration till den platsen.

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
`filters.any` och glöm inte att anpassa `$include`-programsatserna som refererar till det
i servergruppsfilerna också.

Om mappen däremot innehåller flera, gruppspecifika filer med det mönstret, kommer deras innehåll att
ska kopieras till `$include`-satsen som refererar till dem i servergruppsfilerna.

Kopiera filen `conf.dispatcher/filters/default_filters.any` från standardvärdet
AEM som en Cloud Service Dispatcher-konfiguration till den platsen.

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
AEM som en Cloud Service Dispatcher-konfiguration till den platsen.

I varje servergruppsfil tar du bort allt innehåll i `renders`-avsnittet och ersätter det
med:

```
$include "../renders/default_renders.any"
```

### Kontrollera virtuella värdar

Byt namn på katalogen `conf.dispatcher.d/vhosts` till `conf.dispatcher.d/virtualhosts` och ange den.

Ta bort alla filer som har prefixet `ams_`.

Om `conf.dispatcher.d/virtualhosts` nu innehåller en enda fil bör namnet ändras till
`virtualhosts.any` och glöm inte att anpassa `$include`-programsatserna som refererar till det
i servergruppsfilerna också.

Om mappen däremot innehåller flera, gruppspecifika filer med det mönstret, kommer deras innehåll att
ska kopieras till `$include`-satsen som refererar till dem i servergruppsfilerna.

Kopiera filen `conf.dispatcher/virtualhosts/default_virtualhosts.any` från standardvärdet
AEM som en Cloud Service Dispatcher-konfiguration till den platsen.

Ersätt eventuella filter med programsatser som ser ut så här i varje servergruppsfil:

```
$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"
```

med programsatsen:

```
$include "../virtualhosts/default_virtualhosts.any"
```

### Kontrollera status genom att köra valideraren

Kör AEM som en Cloud Service Dispatcher-validerare i din katalog med underkommandot `dispatcher`:

```
$ validator dispatcher .
```

Om felmeddelanden om saknade inkluderingsfiler visas, ska du kontrollera om du har bytt namn på filerna korrekt.

Om felmeddelanden som rör en odefinierad variabel `PUBLISH_DOCROOT` visas, ändrar du namnet till `DOCROOT`.

Alla andra fel finns i felsökningsavsnittet i dokumentationen för valideringsverktyget. 

### Testa konfigurationen med en lokal distribution (kräver installation av Docker)

Om du använder skriptet `docker_run.sh` i AEM som Cloud Service Dispatcher Tools kan du testa att
din konfiguration inte innehåller något annat fel som bara skulle visas i
distribution:

### Steg 1: Generera distributionsinformation med valideraren

```
validator full -d out .
```

Detta validerar den fullständiga konfigurationen och genererar distributionsinformation i `out`

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

**Kunder som använder AMS Dispatcher-konfiguration version 1 bör kontakta kundsupport för att hjälpa dem att migrera från version 1 till version 2 så att instruktionerna ovan kan följas.**
