---
title: Validera och felsöka med Dispatcher Tools (äldre)
description: Validera och felsöka med Dispatcher Tools (äldre)
feature: Dispatcher
hidefromtoc: true
source-git-commit: 4be76f19c27aeab84de388106a440434a99a738c
workflow-type: tm+mt
source-wordcount: '2305'
ht-degree: 1%

---

# Validera och felsöka med Dispatcher Tools (äldre)  {#Dispatcher-tools-legacy}

## Introduktion {#apache-and-dispatcher-configuration-and-testing}

>[!NOTE]
>Mer information om Dispatcher i molnet och hur du hämtar Dispatcher Tools finns i [Dispatcher på sidan Cloud](/help/implementing/dispatcher/disp-overview.md).

I följande avsnitt beskrivs filstrukturen för äldre läge, lokal validering, felsökning och hur du migrerar från det äldre läget till [flexibelt läge](/help/implementing/dispatcher/validation-debug.md).

I den här artikeln förutsätts att projektets dispatcherkonfiguration inte innehåller filens opt-in/USE_SOURCES_DIRECTLY. Det innebär att antalet filer och deras storlek begränsas, till exempel:

* en enda omskrivningsfil som måste användas i stället för filer som är platsspecifika.
* summan av innehållet i de anpassningsbara filerna måste vara mindre än 1 MB.

Från och med Cloud Manager 2021.7.0 genererar nya Cloud Manager-program maven-projektstrukturer med AEM 28 eller senare, som innehåller den ovannämnda filen.

Vi rekommenderar **att du migrerar från äldre läge till flexibelt läge enligt anvisningarna i migreringsavsnittet [Migrera från äldre läge till flexibelt läge](#migrating-flexible).** Om du använder ett flexibelt läge valideras och distribueras konfigurationen på ett bättre sätt av SDK och runtime.

## Filstruktur {#legacy-mode-file-structure}

Strukturen för projektets Dispatcher-undermapp (i äldre läge) är följande:

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

Den här filen inkluderas från dina `.vhost`-filer. Du kan lägga till definitioner för Apache-variabler på den här platsen.

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

## Apache-moduler som stöds {#apache-modules}

Se [Apache-moduler som stöds](/help/implementing/dispatcher/disp-overview.md#supported-directives).

## Lokal validering {#local-validation-legacy-mode}

>[!NOTE]
>Avsnitten nedan innehåller kommandon som använder Mac- eller Linux-versioner av SDK, men Windows SDK kan också användas på ett liknande sätt.

Använd `validate.sh`-skriptet enligt nedan:

```
$ validate.sh src/dispatcher
Phase 1: Dispatcher validator
Cloud manager validator 2.0.32
Phase 1 finished
Phase 2: httpd -t validation in docker image
values.csv found in deployment folder: /tmp/dispatcher_validation_1625150390 - using files listed there
Running script /docker_entrypoint.d/10-check-environment.sh
Running script /docker_entrypoint.d/20-create-docroots.sh
Running script /docker_entrypoint.d/30-wait-for-backend.sh
Waiting until localhost is available
localhost resolves to ::1
Running script /docker_entrypoint.d/40-generate-allowed-clients.sh
Running script /docker_entrypoint.d/50-check-expiration.sh
Running script /docker_entrypoint.d/60-check-loglevel.sh
Running script /docker_entrypoint.d/70-check-forwarded-host-secret.sh
# Dispatcher configuration: (/etc/httpd/conf.dispatcher.d/dispatcher.any)
/farms {

...

}
Syntax OK
Phase 2 finished
Phase 3: Immutability check
reading immutable file list from /etc/httpd/immutable.files.txt

...

no immutable file has been changed - check is SUCCESSFUL
Phase 3 finished
```

Skriptet gör följande:

1. Den kör valideraren. Om konfigurationen inte är giltig misslyckas skriptet.
2. Det kör kommandot `httpd -t` för att testa om syntaxen är korrekt så att apache httpd kan starta. Om det lyckas bör konfigurationen vara klar för distribution.
3. Kontrollerar att delmängden av Dispatcher SDK-konfigurationsfilerna, som är avsedda att vara oföränderliga enligt beskrivningen i [Filstrukturavsnittet](##legacy-mode-file-structure), inte har ändrats. Detta är en ny kontroll som introducerades i AEM SDK version v2021.1.4738 som även innehåller Dispatcher Tools version 2.0.36. Före den här uppdateringen kan kunderna felaktigt ha antagit att lokala SDK-ändringar av dessa oföränderliga filer också skulle tillämpas på molnmiljön.

Under en distribution av Cloud Manager körs även syntaxkontrollen `httpd -t` och eventuella fel inkluderas i loggen för Cloud Manager `Build Images step failure`.

### Fas 1 {#first-phase}

Om ett direktiv inte är tillåtslista loggas ett fel och en avslutningskod som inte är noll returneras. Dessutom genomsöks alla filer med mönstret `conf.dispatcher.d/enabled_farms/*.farm` och följande kontrolleras:

* Det finns ingen filterregel som tillåter via `/glob` (mer information finns i [CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957).
* Ingen administratörsfunktion visas. Åtkomst till sökvägar som `/crx/de or /system/console`.

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

Observera att den första fasen också kan köras separat **i stället för i omslutningsskriptet `validate.sh`.**

När den körs mot din maven-artefakt eller din `dispatcher/src`-underkatalog rapporterar den valideringsfel:

```
$ validator full dispatcher/src
Cloud manager validator 1.0.4
2019/06/19 15:41:37 Apache configuration uses non-allowlisted directives:
  conf.d/enabled_vhosts/aem_publish.vhost:46: LogLevel
2019/06/19 15:41:37 Dispatcher configuration validation failed:
  conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any: filter allows access to CRXDE
```

I Windows är dispatchervalideraren skiftlägeskänslig. Därför kan det misslyckas med att validera konfigurationen om du inte respekterar skiftläget för sökvägen där konfigurationen finns, till exempel:

```
bin\validator.exe full src
Cloud manager validator 2.0.xx
2021/03/15 18:15:40 Dispatcher configuration validation failed:
  conf.dispatcher.d\available_farms\default.farm:15: parent directory outside server root: c:\k\a\aem-dispatcher-sdk-windows-symlinks-testing3\dispatcher\src
  
```

Undvik det här felet genom att kopiera och klistra in sökvägen från Utforskaren i Windows och sedan i kommandotolken med kommandot `cd` i sökvägen.

### Fas 2 {#second-phase}

Den här fasen kontrollerar apachesyntaxen genom att starta Docker i en bild. Docker måste installeras lokalt, men observera att AEM inte behöver köras.

>[!NOTE]
>Windows-användare måste använda Windows 10 Professional eller andra distributioner som stöder Docker. Detta är en förutsättning för att du ska kunna köra och felsöka Dispatcher på en lokal dator.

Den här fasen kan också köras oberoende av varandra via `validator full -d out src/dispatcher`, som genererar en out-katalog som behövs för nästa kommando `bin/docker_run.sh out host.internal.docker:4503 8080`.

Under en driftsättning av Cloud Manager körs även syntaxkontrollen `httpd -t` och eventuella fel inkluderas i felloggen för Cloud Manager Build Images.

### Fas 3 {#third-phase}

Om ett fel uppstår i den här fasen innebär det att Adobe har ändrat en eller flera oföränderliga filer och att du måste ersätta motsvarande oföränderliga filer med den nya versionen som levereras i katalogen `src` i SDK:n. Loggexemplet nedan visar detta problem:

```
Phase 3: Immutability check
reading immutable file list from /etc/httpd/immutable.files.txt
(...)
checking existing 'conf.dispatcher.d/clientheaders/default_clientheaders.any' for changes
immutable file 'conf.dispatcher.d/clientheaders/default_clientheaders.any' has been changed:
--- /etc/httpd/conf.dispatcher.d/clientheaders/default_clientheaders.any
+++ /etc/httpd-actual/conf.dispatcher.d/clientheaders/default_clientheaders.any
@@ -40,4 +40,3 @@
"Sling-uploadmode"
"x-requested-with"
"If-Modified-Since"
-"Authorization"
** error: immutable file 'conf.dispatcher.d/clientheaders/default_clientheaders.any' has been changed!
  
```

Den här fasen kan också köras oberoende av varandra via `validator full -d out src/dispatcher`, som genererar en out-katalog som behövs för nästa kommando `bin/docker_immutability_check.sh out`.

## Felsöka konfigurationen av Apache och Dispatcher {#debugging-apache-and-dispatcher-configuration}

Observera att du kan köra en apache-dispatcher lokalt med `./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`.

Som tidigare nämnts måste Docker installeras lokalt och det är inte nödvändigt att AEM körs. Windows-användare måste använda Windows 10 Professional eller andra distributioner som stöder Docker. Detta är en förutsättning för att du ska kunna köra och felsöka Dispatcher på en lokal dator.

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

## Migrera från äldre läge till flexibelt läge {#migrating-flexible}

Med Cloud Manager 2021.7.0 genererar nya Cloud Manager-program maven-projektstrukturer med AEM 28 eller senare, som innehåller filen **opt-in/USE_SOURCES_DIRECTLY**. Detta tar bort tidigare begränsningar för det äldre läget runt antalet filer och filstorleken, vilket även gör att SDK och miljön validerar och distribuerar konfigurationen på ett förbättrat sätt. Om din dispatcherkonfiguration inte har den här filen rekommenderar vi att du migrerar. Använd de metoder som beskrivs på sidan [Flexibelt läge](/help/implementing/dispatcher/validation-debug.md#migrating).
