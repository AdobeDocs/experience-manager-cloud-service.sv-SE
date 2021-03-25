---
title: Dispatcher i molnet
description: 'Dispatcher i molnet '
feature: Dispatcher
translation-type: tm+mt
source-git-commit: c11d8e36fe8ba120847c675f40e09a0388943d51
workflow-type: tm+mt
source-wordcount: '4169'
ht-degree: 6%

---


# Dispatcher i molnet {#Dispatcher-in-the-cloud}

## Konfiguration och testning av Apache och Dispatcher {#apache-and-dispatcher-configuration-and-testing}

I det här avsnittet beskrivs hur du strukturerar AEM som en Cloud Service-Apache och Dispatcher-konfiguration samt hur du validerar och kör den lokalt innan du distribuerar den i molnmiljöer. Det beskriver även felsökning i molnmiljöer. Mer information om Dispatcher finns i [AEM Dispatcher-dokumentationen](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/dispatcher.html).

>[!NOTE]
>Windows-användare måste använda Windows 10 Professional eller andra distributioner som stöder Docker. Detta är en förutsättning för att du ska kunna köra och felsöka Dispatcher på en lokal dator. Avsnitten nedan innehåller kommandon som använder Mac- eller Linux-versionerna av SDK, men Windows SDK kan användas på liknande sätt.

## Dispatcher Tools {#dispatcher-sdk}

Dispatcher Tools är en del av den övergripande AEM som en Cloud Service-SDK och tillhandahåller:

* En vaniljfilstruktur som innehåller de konfigurationsfiler som ska inkluderas i ett maven-projekt för Dispatcher.
* Verktyg för kunder som validerar att Dispatcher-konfigurationen bara innehåller AEM som direktiv som stöds av Cloud Servicen.        Dessutom validerar verktyget att syntaxen är korrekt så att apache kan startas korrekt.
* En Docker-bild som öppnar Dispatcher lokalt.

## Hämta och extrahera verktygen {#extracting-the-sdk}

Dispatcher Tools, som ingår i [AEM som en Cloud Service-SDK](/help/implementing/developing/introduction/aem-as-a-cloud-service-sdk.md), kan hämtas från en zip-fil på [Software Distribution](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html)-portalen. Alla nya konfigurationer som är tillgängliga i den nya versionen av Dispatcher Tools kan användas för att distribuera till molnmiljöer som kör den versionen av AEM i molnet eller senare.

Zippa upp SDK, som innehåller Dispatcher Tools för både macOS/Linux och Windows.

**För macOS/Linux** gör du artefakten för Dispatcher-verktyget körbar och kör den. Dispatcher Tools-filerna extraheras automatiskt under den katalog som du lagrade dem i (där `version` är versionen av Dispatcher Tools).

```bash
$ chmod +x aem-sdk-dispatcher-tools-<version>-unix.sh
$ ./aem-sdk-dispatcher-tools-<version>-unix.sh
Verifying archive integrity...  100%   All good.
Uncompressing aem-sdk-dispatcher-tools-<version>-unix.sh 100%
```

**Extrahera zip-arkivet Dispatcher Tooling för Windows**.

## Filstruktur {#file-structure}

Strukturen för projektets Dispatcher-undermapp beskrivs nedan och ska kopieras till huvudprojektmappen Dispatcher:

```bash
./
├── conf.d
│   ├── available_vhosts
│   │   └── default.vhost
│   ├── dispatcher_vhost.conf
│   ├── enabled_vhosts
│   │   ├── README
│   │   └── default.vhost -> ../available_vhosts/default.vhost
│   └── rewrites
│   │   ├── default_rewrite.rules
│   │   └── rewrite.rules
│   └── variables
|       ├── custom.vars
│       └── global.vars
└── conf.dispatcher.d
    ├── available_farms
    │   └── default.farm
    ├── cache
    │   ├── default_invalidate.any
    │   ├── default_rules.any
    │   └── rules.any
    ├── clientheaders
    │   ├── clientheaders.any
    │   └── default_clientheaders.any
    ├── dispatcher.any
    ├── enabled_farms
    │   ├── README
    │   └── default.farm -> ../available_farms/default.farm
    ├── filters
    │   ├── default_filters.any
    │   └── filters.any
    ├── renders
    │   └── default_renders.any
    └── virtualhosts
        ├── default_virtualhosts.any
        └── virtualhosts.any
```

Nedan visas en förklaring av anteckningsfiler som kan ändras:

**Anpassningsbara filer**

Följande filer kan anpassas och överförs till din molninstans vid distributionen:

* `conf.d/available_vhosts/<CUSTOMER_CHOICE>.vhost`

Du kan ha en eller flera av dessa filer. De innehåller `<VirtualHost>`-poster som matchar värdnamn och som tillåter att Apache hanterar varje domäntrafik med olika regler. Filerna skapas i katalogen `available_vhosts` och aktiveras med en symbolisk länk i katalogen `enabled_vhosts`. Från `.vhost`-filerna inkluderas andra filer, som omskrivningar och variabler.

* `conf.d/rewrites/rewrite.rules`

Den här filen inkluderas från dina `.vhost`-filer. Den har en uppsättning omskrivningsregler för `mod_rewrite`.

>[!NOTE]
>
>För närvarande måste en enda omskrivningsfil användas i stället för filer som är platsspecifika. Som regel måste summan av innehållet i de anpassningsbara filerna vara mindre än 1 MB.

* `conf.d/variables/custom.vars`

Den här filen inkluderas från dina `.vhost`-filer. Du kan ange definitioner för Apache-variabler på den här platsen.

* `conf.d/variables/global.vars`

Den här filen inkluderas från `dispatcher_vhost.conf`-filen. Du kan ändra Dispatcher och skriva om loggnivån i den här filen.

* `conf.dispatcher.d/available_farms/<CUSTOMER_CHOICE>.farm`

Du kan ha en eller flera av de här filerna och de innehåller grupper som matchar värdnamn och som gör att Dispatcher-modulen kan hantera varje grupp med olika regler. Filerna skapas i katalogen `available_farms` och aktiveras med en symbolisk länk i katalogen `enabled_farms`. Från `.farm`-filerna inkluderas andra filer som filter, cacheregler och andra.

* `conf.dispatcher.d/cache/rules.any`

Den här filen inkluderas från dina `.farm`-filer. Den anger cachelagringsinställningar.

* `conf.dispatcher.d/clientheaders/clientheaders.any`

Den här filen inkluderas från dina `.farm`-filer. Den anger vilka begärandehuvuden som ska vidarebefordras till serverdelen.

* `conf.dispatcher.d/filters/filters.any`

Den här filen inkluderas från dina `.farm`-filer. Den har en uppsättning regler som ändrar vilken trafik som ska filtreras bort och inte hamna i bakgrunden.

* `conf.dispatcher.d/virtualhosts/virtualhosts.any`

Den här filen inkluderas från dina `.farm`-filer. Den har en lista med värdnamn eller URI-sökvägar som ska matchas med matchning av glob. Detta avgör vilken serverdel som ska användas för att hantera en begäran.

Ovanstående filer refererar till de oföränderliga konfigurationsfiler som listas nedan. Ändringar av oföränderliga filer bearbetas inte av Dispatchers i molnmiljöer.

**Oändringsbara konfigurationsfiler**

Dessa filer ingår i grundramverket och följer standarder och bästa praxis. Filerna anses oföränderliga eftersom ändringar eller borttagningar av dem lokalt inte påverkar distributionen eftersom de inte överförs till din molninstans.

Vi rekommenderar att ovanstående filer refererar till de oföränderliga filer som listas nedan, följt av eventuella ytterligare programsatser eller åsidosättningar. När Dispatcher-konfigurationen distribueras till en molnmiljö kommer den senaste versionen av de oföränderliga filerna att användas, oavsett vilken version som användes i den lokala utvecklingen.

* `conf.d/available_vhosts/default.vhost`

Innehåller ett exempel på en virtuell värd. Skapa en kopia av den här filen för din egen virtuella värd, anpassa den, gå till `conf.d/enabled_vhosts` och skapa en symbolisk länk till din anpassade kopia.

* `conf.d/dispatcher_vhost.conf`

En del av basramverket, som används för att illustrera hur dina virtuella värdar och globala variabler inkluderas.

* `conf.d/rewrites/default_rewrite.rules`

Standardregler för omskrivning som är lämpliga för ett standardprojekt. Om du behöver anpassa kan du ändra `rewrite.rules`. När du anpassar kan du fortfarande inkludera standardreglerna först, om de passar dina behov.

* `conf.dispatcher.d/available_farms/default.farm`

Innehåller ett exempel på en Dispatcher-servergrupp. Skapa en kopia av den här filen för din egen servergrupp, anpassa den, gå till `conf.d/enabled_farms` och skapa en symbolisk länk till din anpassade kopia.

* `conf.dispatcher.d/cache/default_invalidate.any`

En del av basramverket genereras vid start. Du måste **ta med den här filen i alla grupper som du definierar i `cache/allowedClients`-avsnittet.**

* `conf.dispatcher.d/cache/default_rules.any`

Standardcacheregler som är lämpliga för ett standardprojekt. Om du behöver anpassa kan du ändra `conf.dispatcher.d/cache/rules.any`. När du anpassar kan du fortfarande inkludera standardreglerna först, om de passar dina behov.

* `conf.dispatcher.d/clientheaders/default_clientheaders.any`

Standardbegäranrubriker som ska vidarebefordras till serverdelen, lämpliga för ett standardprojekt. Om du behöver anpassa kan du ändra `clientheaders.any`. När du anpassar kan du fortfarande inkludera standardrubrikerna för begäran först, om de passar dina behov.

* `conf.dispatcher.d/dispatcher.any`

En del av grundramverket som används för att illustrera hur Dispatcher-grupper inkluderas.

* `conf.dispatcher.d/filters/default_filters.any`

Standardfilter som passar för ett standardprojekt. Om du behöver anpassa kan du ändra `filters.any`. När du anpassar kan du fortfarande inkludera standardfiltren först, om de passar dina behov.

* `conf.dispatcher.d/renders/default_renders.any`

Den här filen genereras vid start och ingår i det grundläggande ramverket. Du måste **ta med den här filen i alla grupper som du definierar i `renders`-avsnittet.**

* `conf.dispatcher.d/virtualhosts/default_virtualhosts.any`

Standardvärdglobbning som passar för ett standardprojekt. Om du behöver anpassa kan du ändra `virtualhosts.any`. När du anpassar bör du inte ta med standardvärddatorns ordlista, eftersom den matchar **varje** inkommande begäran.

>[!NOTE]
>
>AEM som en Cloud Service maven-arkityp genererar samma Dispatcher-konfigurationsfilstruktur.

Avsnitten nedan beskriver hur konfigurationen valideras lokalt så att den kan skicka den associerade kvalitetsgaten i Cloud Manager när en intern release distribueras.

## Lokal validering av direktiv som stöds i Dispatcher-konfigurationen {#local-validation-of-dispatcher-configuration}

Valideringsverktyget finns i SDK på `bin/validator` som binär Mac OS, Linux eller Windows, vilket gör att kunderna kan köra samma validering som Cloud Manager gör när en release skapas och distribueras.

Den anropas som: `validator full [-d folder] [-w allowlist] zip-file | src folder`

Verktyget kontrollerar att Dispatcher-konfigurationen använder rätt direktiv som stöds av AEM som en molntjänst genom att skanna alla filer med mönstret `conf.d/enabled_vhosts/*.vhost`.

I Windows är dispatchervalideraren skiftlägeskänslig. Därför kan det misslyckas med att validera konfigurationen om du inte respekterar skiftläget för sökvägen där konfigurationen finns, till exempel:

```
bin\validator.exe full src
Cloud manager validator 2.0.xx
2021/03/15 18:15:40 Dispatcher configuration validation failed:
  conf.dispatcher.d\available_farms\default.farm:15: parent directory outside server root: c:\k\a\aem-dispatcher-sdk-windows-symlinks-testing3\dispatcher\src
  
```

Undvik det här felet genom att kopiera och klistra in sökvägen från Utforskaren i Windows och sedan i kommandotolken med kommandot `cd` i sökvägen.

De direktiv som är tillåtna i Apache-konfigurationsfiler kan listas genom att köra validerarens tillåtelselista-kommando:

```
$ validator allowlist
Cloud manager validator 2.0.4
 
Allowlisted directives:
  <Directory>
  ...
  
```

Tabellen nedan visar vilka cachemoduler som stöds:

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
| `mod_remoteip` | [https://httpd.apache.org/docs/2.4/mod/mod_remoteip.html](https://httpd.apache.org/docs/2.4/mod/mod_remoteip.html) |
| `mod_reqtimeout` | [https://httpd.apache.org/docs/2.4/mod/mod_reqtimeout.html](https://httpd.apache.org/docs/2.4/mod/mod_reqtimeout.html) |
| `mod_rewrite` | [https://httpd.apache.org/docs/2.4/mod/mod_rewrite.html](https://httpd.apache.org/docs/2.4/mod/mod_rewrite.html) |
| `mod_security` | [https://modsecurity.org/](https://modsecurity.org/) |
| `mod_setenvif` | [https://httpd.apache.org/docs/2.4/mod/mod_setenvif.html](https://httpd.apache.org/docs/2.4/mod/mod_setenvif.html) |
| `mod_substitute` | [https://httpd.apache.org/docs/2.4/mod/mod_substitute.html](https://httpd.apache.org/docs/2.4/mod/mod_substitute.html) |
| `mod_userdir` | [https://httpd.apache.org/docs/2.4/mod/mod_userdir.html](https://httpd.apache.org/docs/2.4/mod/mod_userdir.html) |

Kunder kan inte lägga till godtyckliga moduler, men ytterligare moduler kan övervägas för att ingå i produkten i framtiden. Kunderna hittar listan över direktiv som är tillgängliga för en viss Dispatcher-version genom att köra validerarens tillåtslista-kommando i SDK enligt beskrivningen ovan.

Tillåtelselista innehåller en lista över Apache-direktiv som tillåts i en kundkonfiguration. Om ett direktiv inte är tillåtslista loggas ett fel och en avslutningskod som inte är noll returneras. Om ingen tillåtelselista anges på kommandoraden (vilket är det sätt som det ska anropas) använder verktyget en tillåtelselista som Cloud Manager använder som standard för validering innan det distribueras till molnmiljöer.

Dessutom genomsöks alla filer med mönstret `conf.dispatcher.d/enabled_farms/*.farm` och följande kontrolleras:

* Det finns ingen filterregel som använder `/glob` (mer information finns i [CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957))
* Ingen administratörsfunktion visas. Åtkomst till sökvägar som `/crx/de or /system/console`.

När den körs mot din maven-artefakt eller din `dispatcher/src`-underkatalog rapporterar den valideringsfel:

```
$ validator full dispatcher/src
Cloud manager validator 1.0.4
2019/06/19 15:41:37 Apache configuration uses non-allowlisted directives:
  conf.d/enabled_vhosts/aem_publish.vhost:46: LogLevel
2019/06/19 15:41:37 Dispatcher configuration validation failed:
  conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any: filter allows access to CRXDE
```

Observera att valideringsverktyget endast rapporterar förbjuden användning av Apache-direktiv som inte har tillåtslista. Den rapporterar inte syntaktiska eller semantiska problem med din Apache-konfiguration eftersom den här informationen endast är tillgänglig för Apache-moduler i en körningsmiljö.

Nedan visas felsökningstekniker för felsökning av vanliga valideringsfel som genereras av verktyget:

**det går inte att hitta en  `conf.dispatcher.d` undermapp i arkivet**

Arkivet bör innehålla mapparna `conf.d` och `conf.dispatcher.d`. Observera att du **inte** bör
använda prefixet `etc/httpd` i arkivet.

**det gick inte att hitta någon servergrupp i`conf.dispatcher.d/enabled_farms`**

De aktiverade grupperna ska finnas i den undermappen.

**filen som ingår (..) måste ha följande namn: ...**

Det finns två avsnitt i servergruppskonfigurationen som **måste** innehåller en
specifik fil: `/renders` och `/allowedClients` i avsnittet `/cache`. Dessa
-avsnitten ska se ut så här:

```
/renders {
    $include "../renders/default_renders.any"
}
```

and:

```
/allowedClients {
    $include "../cache/default_invalidate.any"
}
```

**filen finns på okänd plats: ...**

Det finns fyra avsnitt i servergruppskonfigurationen där du kan inkludera din egen fil: `/clientheaders`, `filters`, `/rules` i `/cache`-avsnittet och `/virtualhosts`. De inkluderade filerna måste ha följande namn:

| Avsnitt | Inkludera filnamn |
|------------------|--------------------------------------|
| `/clientheaders` | `../clientheaders/clientheaders.any` |
| `/filters` | `../filters/filters.any` |
| `/rules` | `../cache/rules.any` |
| `/virtualhosts` | `../virtualhosts/virtualhosts.any` |

Du kan också inkludera **standardversionen** av de filerna, vars namn börjar med ordet `default_`, t.ex. `../filters/default_filters.any`.

**include-sats på (..), utanför känd plats: ...**

Förutom de sex avsnitt som nämns i styckena ovan är du inte tillåten
om du vill använda programsatsen `$include`, t.ex. skulle följande generera detta fel:

```
/invalidate {
    $include "../cache/invalidate.any"
}
```

**Tillåtna klienter/renderare inkluderas inte från: ...**

Det här felet genereras när du inte anger någon inkludering för `/renders` och `/allowedClients` i `/cache`-avsnittet. Se
**filen som ingår (..) måste ha namnet: ...** för mer information.

**filtret får inte använda glob-mönster för att tillåta förfrågningar**

Det är inte säkert att tillåta begäranden med en `/glob`-formatregel, som matchas mot den fullständiga begäranderaden, t.ex.

```
/0100 {
    /type "allow" /glob "GET *.css *"
}
```

Programsatsen är avsedd att tillåta begäranden för `css`-filer, men den tillåter även begäranden till **alla**-resurser följt av frågesträngen `?a=.css`. Det är därför förbjudet att använda sådana filter (se även CVE-2016-0957).

**den inkluderade filen (..) matchar ingen känd fil**

Det finns två typer av filer i din virtuella värdkonfiguration för Apache som kan anges enligt följande: skriver om och variabler.
De inkluderade filerna måste ha följande namn:

| Typ | Inkludera filnamn |
|-----------|---------------------------------|
| Skriver om | `conf.d/rewrites/rewrite.rules` |
| Variabler | `conf.d/variables/custom.vars` |

Du kan också inkludera **standardversionen** av omskrivningsreglerna, vars namn är `conf.d/rewrites/default_rewrite.rules`.
Observera att det inte finns någon standardversion av variabelfilerna.

**Inaktuell konfigurationslayout har identifierats, kompatibilitetsläge aktiveras**

Det här meddelandet anger att din konfiguration har den föråldrade layouten version 1 som innehåller en fullständig
Apache-konfiguration och filer med `ams_`-prefix. Detta stöds fortfarande bakåt
bör du växla till den nya layouten.

## Lokal validering av Dispatcher-konfigurationssyntaxen så att APACH httpd kan starta {#local-validation}

När det har fastställts att Dispatcher-modulens konfiguration endast innehåller direktiv som stöds, bör du kontrollera att syntaxen är korrekt så att apache kan starta. Om du vill testa detta måste du installera dockningsfunktionen lokalt. Observera att det inte är nödvändigt att AEM körs.

Använd `validate.sh`-skriptet enligt nedan:

```
$ validate.sh src/dispatcher
Phase 1: Dispatcher validator
2019/06/19 16:02:55 No issues found
Phase 1 finished
Phase 2: httpd -t validation in docker image
Running script /docker_entrypoint.d/10-create-docroots.sh
Running script /docker_entrypoint.d/20-wait-for-backend.sh
Waiting until aemhost is available
aemhost resolves to xx.xx.xx.xx
Running script /docker_entrypoint.d/30-allowed-clients.sh
# Dispatcher configuration: (/etc/httpd/conf.dispatcher.d/dispatcher.any)
/farms {
...
}
Syntax OK
Phase 2 finished
```

Skriptet gör följande:

1. Valideraren körs från föregående avsnitt för att säkerställa att endast de direktiv som stöds inkluderas. Om konfigurationen inte är giltig misslyckas skriptet.
2. Den kör `httpd -t command` för att testa om syntaxen är korrekt så att apache httpd kan starta. Om det lyckas bör konfigurationen vara klar för distribution.
3. Kontrollerar att delmängden av Dispatcher SDK-konfigurationsfilerna, som är avsedda att vara oföränderliga enligt beskrivningen i [Filstrukturavsnittet](#file-structure), inte har ändrats. Detta är en ny kontroll som introducerades i AEM SDK version v2021.1.4738 som även innehåller Dispatcher Tools version 2.0.36. Före den här uppdateringen kan kunderna felaktigt ha antagit att lokala SDK-ändringar av dessa oföränderliga filer också skulle tillämpas på molnmiljön.

Under en distribution av Cloud Manager körs kontrollen `httpd -t syntax` också och eventuella fel inkluderas i loggen för Cloud Manager `Build Images step failure`.

## Testa Apache- och Dispatcher-konfigurationen lokalt {#testing-apache-and-dispatcher-configuration-locally}

Du kan också testa konfigurationen av Apache och Dispatcher lokalt. Det kräver att dockningsstationen installeras lokalt och att konfigurationen klarar den validering som beskrivs ovan.

Kör valideringsverktyget (observera att det skiljer sig från `validator.sh` ovan) genom att använda parametern `-d` som matar ut en mapp med alla Dispatcher-konfigurationsfiler. Kör sedan `docker_run.sh`-skriptet och skicka mappen som ett argument. Genom att ange portnumret (här: 8080) För att visa Dispatcher-slutpunkten startas en Docker-behållare som kör Dispatcher med din konfiguration.

```
$ validator full -d out src/dispatcher
2019/06/19 16:02:55 No issues found
$ docker_run.sh out docker.for.mac.localhost:4503 8080
Running script /docker_entrypoint.d/10-create-docroots.sh
Running script /docker_entrypoint.d/20-wait-for-backend.sh
Waiting until aemhost is available
aemhost resolves to xx.xx.xx.xx
Running script /docker_entrypoint.d/30-allowed-clients.sh
Starting httpd server
...
```

Detta startar Dispatcher i en behållare med dess serverdel pekande på en AEM som körs på din lokala Mac OS-dator vid port 4503.

## Felsöka konfigurationen för Apache och Dispatcher {#debugging-apache-and-dispatcher-configuration}

Följande strategi kan användas för att öka loggutdata för modulen Dispatcher och för att se resultaten av utvärderingen `RewriteRule` i både lokala miljöer och molnmiljöer.

Loggnivåer för dessa moduler definieras av variablerna `DISP_LOG_LEVEL` och `REWRITE_LOG_LEVEL`. De kan anges i filen `conf.d/variables/global.vars`. Den relevanta delen är följande:

```
# Log level for the dispatcher
#
# Possible values are: Error, Warn, Info, Debug and Trace1
# Default value: Warn
#
# Define DISP_LOG_LEVEL Warn
 
# Log level for mod_rewrite
#
# Possible values are: Error, Warn, Info, Debug and Trace1 - Trace8
# Default value: Warn
#
# To debug your RewriteRules, it is recommended to raise your log
# level to Trace2.
#
# More information can be found at:
# https://httpd.apache.org/docs/current/mod/mod_rewrite.html#logging
#
# Define REWRITE_LOG_LEVEL Warn
```

När du kör Dispatcher lokalt skrivs loggarna ut direkt till terminalutdata. Oftast vill du att de här loggarna ska vara i felsökningsversionen, vilket du kan göra genom att skicka felsökningsnivån som en parameter när du kör Docker. Till exempel: `DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`.

Loggar för molnmiljöer visas via loggningstjänsten i Cloud Manager.

## Olika Dispatcher-konfigurationer per miljö {#different-dispatcher-configurations-per-environment}

För närvarande används samma Dispatcher-konfiguration för alla AEM som en Cloud Service-miljö. Körningsmiljön kommer att ha en miljövariabel `ENVIRONMENT_TYPE` som innehåller det aktuella körningsläget (dev, stage eller prod) samt en definition. Definitionen kan vara `ENVIRONMENT_DEV`, `ENVIRONMENT_STAGE` eller `ENVIRONMENT_PROD`. I Apache-konfigurationen kan variabeln användas direkt i ett uttryck. Definitionen kan också användas för att skapa logik:

```
# Simple usage of the environment variable
ServerName ${ENVIRONMENT_TYPE}.company.com
 
# When more logic is required
<IfDefine ENVIRONMENT_STAGE>
  # These statements are for stage
  Define VIRTUALHOST stage.example.com
</IfDefine>
<IfDefine ENVIRONMENT_PROD>
  # These statements are for production
  Define VIRTUALHOST prod.example.com
</IfDefine>
```

I Dispatcher-konfigurationen är samma systemvariabel tillgänglig. Om mer logik krävs definierar du variablerna enligt exemplet ovan och använder dem sedan i Dispatcher-konfigurationsavsnittet:

```
/virtualhosts {
  { "${VIRTUALHOST}" }
}
```

När du testar konfigurationen lokalt kan du simulera olika miljötyper genom att skicka variabeln `DISP_RUN_MODE` till `docker_run.sh`-skriptet direkt:

```
$ DISP_RUN_MODE=stage docker_run.sh out docker.for.mac.localhost:4503 8080
```

Standardkörningsläget när inget värde för DISP_RUN_MODE skickas är &quot;dev&quot;.
Kör skriptet `docker_run.sh` utan argument om du vill se en fullständig lista över tillgängliga alternativ och variabler.

## Visa Dispatcher-konfigurationen som används av Docker-behållaren {#viewing-dispatcher-configuration-in-use-by-docker-container}

Med miljöspecifika konfigurationer kan det vara svårt att avgöra hur den faktiska Dispatcher-konfigurationen ser ut. När du har startat din dockningsbehållare med `docker_run.sh` kan den dumpas enligt följande:

* Bestäm vilket behållar-ID som används:

```
$ docker ps
CONTAINER ID       IMAGE
d75fbd23b29        adobe/aem-ethos/dispatcher-publish:...
```

* Kör följande kommandorad med detta behållar-ID:

```
$ docker exec d75fbd23b29 httpd-test
# Dispatcher configuration: (/etc/httpd/conf.dispatcher.d/dispatcher.any)
/farms {
  /publishfarm {
    /clientheaders {
...
```

## Huvudskillnader mellan AMS Dispatcher och AEM som en Cloud Service {#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

Som beskrivs på referenssidan ovan liknar konfigurationen av Apache och Dispatcher i AEM som en Cloud Service AMS-konfigurationen. De viktigaste skillnaderna är:

* I AEM som Cloud Service kan vissa Apache-direktiv inte användas (till exempel `Listen` eller `LogLevel`)
* I AEM som Cloud Service kan endast vissa delar av Dispatcher-konfigurationen placeras i inkluderingsfiler och deras namn är viktigt. Filterregler som du vill återanvända på olika värdar måste till exempel läggas i en fil med namnet `filters/filters.any`. Mer information finns på referenssidan.
* I AEM som Cloud Service finns det extra validering för att förhindra att filterregler skrivs med `/glob` för att förhindra säkerhetsproblem. Eftersom `deny *` kommer att användas i stället för `allow *` (som inte kan användas) har kunderna nytta av att köra Dispatcher lokalt och göra testversionen och felsökningen. Loggarna visar exakt vilka sökvägar Dispatcher-filtren blockerar för att dessa ska kunna läggas till.

## Riktlinjer för att migrera dispatcher-konfiguration från AMS till AEM som Cloud Service

Dispatcher-konfigurationsstrukturen har skillnader mellan Managed Services och AEM som en Cloud Service. Nedan visas en steg-för-steg-guide om hur du migrerar från AMS Dispatcher-konfiguration version 2 till AEM som Cloud Service.

## Konvertera en AMS till en AEM som en Dispatcher-konfiguration för molntjänster

I följande avsnitt ges stegvisa instruktioner för hur du konverterar en AMS-konfiguration. Det förutsätter
att du har ett arkiv med en struktur som liknar den som beskrivs i [Cloud Manager Dispatcher configuration](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)

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
