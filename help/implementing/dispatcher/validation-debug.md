---
title: Validera och felsöka med Dispatcher Tools
description: Lär dig mer om lokal validering, felsökning, filstrukturen i flexibelt läge och hur du migrerar från äldre läge till flexibelt läge.
feature: Dispatcher
exl-id: 9e8cff20-f897-4901-8638-b1dbd85f44bf
source-git-commit: 2cb57347856568da979b34832ce12cce295841dd
workflow-type: tm+mt
source-wordcount: '3028'
ht-degree: 0%

---

# Validera och felsöka med Dispatcher Tools {#Dispatcher-in-the-cloud}

## Introduktion {#apache-and-dispatcher-configuration-and-testing}

>[!NOTE]
>Mer information om Dispatcher i molnet och hur du hämtar Dispatcher-verktyg finns i [Dispatcher i molnet](/help/implementing/dispatcher/disp-overview.md) sida. Om Dispatcher-konfigurationen är i äldre läge finns mer information i [dokumentation för äldre läge](/help/implementing/dispatcher/validation-debug-legacy.md).

I följande avsnitt beskrivs filstrukturen för flexibelt läge, lokal validering, felsökning och migrering från äldre läge till flexibelt läge.

I den här artikeln förutsätts att i projektets Dispatcher-konfiguration ingår filen `opt-in/USE_SOURCES_DIRECTLY`. Den här filen gör att SDK och körningsmiljön validerar och distribuerar konfigurationen på ett bättre sätt jämfört med det äldre läget, vilket eliminerar begränsningar i antal och storlek på filer.

Om Dispatcher-konfigurationen inte innehåller den tidigare nämnda filen rekommenderar Adobe att du migrerar från äldre läge till det flexibla läget enligt anvisningarna i [Migrera från äldre läge till flexibelt läge](#migrating) -avsnitt.

## Filstruktur {#flexible-mode-file-structure}

Strukturen för projektets Dispatcher-undermapp är följande:

```bash
./
├── conf.d
│   ├── available_vhosts
│   │   ├── my_site.vhost # Created by customer
│   │   └── default.vhost
│   ├── dispatcher_vhost.conf
│   ├── enabled_vhosts
│   │   ├── README
│   │   └── my_site.vhost -> ../available_vhosts/my_site.vhost  # Created by customer
│   └── rewrites
│   │   ├── default_rewrite.rules
│   │   └── rewrite.rules
│   └── variables
|       ├── custom.vars
│       └── global.vars
│── opt-in
│   └── USE_SOURCES_DIRECTLY
└── conf.dispatcher.d
    ├── available_farms
    │   ├── my_farm.farm # Created by customer
    │   └── default.farm
    ├── cache
    │   ├── default_invalidate.any
    │   ├── default_rules.any
    │   ├── marketing_query_parameters.any
    │   └── rules.any
    ├── clientheaders
    │   ├── clientheaders.any
    │   └── default_clientheaders.any
    ├── dispatcher.any
    ├── enabled_farms
    │   ├── README
    │   └── my_farm.farm -> ../available_farms/my_farm.farm  # Created by customer
    ├── filters
    │   ├── default_filters.any
    │   └── filters.any
    ├── renders
    │   └── default_renders.any
    └── virtualhosts
    │   ├── default_virtualhosts.any
    │   └── virtualhosts.any
    
```

Nedan visas en förklaring av anteckningsfiler som kan ändras:

**Anpassningsbara filer**

Följande filer kan anpassas och överförs till din molninstans vid distributionen:

* `conf.d/available_vhosts/<CUSTOMER_CHOICE>.vhost`

Du kan ha en eller flera av dessa filer. De innehåller `<VirtualHost>` poster som matchar värdnamn och som tillåter att Apache hanterar varje domäntrafik med olika regler. Filerna skapas i `available_vhosts` och aktiveras med en symbolisk länk i `enabled_vhosts` katalog. Från `.vhost` filer, andra filer, som omskrivningar och variabler, inkluderas.

>[!NOTE]
>
>I det flexibla läget bör du använda relativa sökvägar i stället för absoluta sökvägar.

Kontrollera att det alltid finns minst en virtuell värd som matchar ServerAlias `\*.local`, `localhost`och `127.0.0.1` som behövs för att göra Dispatcher-ogiltigförklaringen. Serveralias `*.adobeaemcloud.net` och `*.adobeaemcloud.com` krävs också i minst en värdkonfiguration och behövs för interna Adobe-processer.

Om du vill matcha den exakta värden eftersom du har flera värdfiler kan du följa följande exempel:

```
<VirtualHost *:80>
    ServerName    "example.com"
    # Put names of which domains are used for your published site/content here
    ServerAlias     "*example.com" "\*.local" "localhost" "127.0.0.1" "*.adobeaemcloud.net" "*.adobeaemcloud.com"
    # Use a document root that matches the one in conf.dispatcher.d/default.farm
    DocumentRoot "${DOCROOT}"
    # URI dereferencing algorithm is applied at Sling's level, do not decode parameters here
    AllowEncodedSlashes NoDecode
    # Add header breadcrumbs for help in troubleshooting which vhost file is chosen
    <IfModule mod_headers.c>
        Header add X-Vhost "publish-example-com"
    </IfModule>
  ...
</VirtualHost>
```

* `conf.d/enabled_vhosts/<CUSTOMER_CHOICE>.vhost`

Den här mappen innehåller relativa symboliska länkar till filer under conf.dispatcher.d/available_vhosts.

Exempelkommandon som krävs för att skapa dessa symboliska länkar:

Apple macOS, Linux och WSL

```
ln -s ../available_vhosts/wknd.vhost wknd.vhost
```

Microsoft Windows

```
mklink wknd.vhost ..\available_vhosts\wknd.vhost
```

>[!NOTE]
>
> När du arbetar med symboliska länkar under Windows bör du köra i en förhöjd kommandotolk, i Windows-undersystemet för Linux eller ha [Skapa symboliska länkar](https://learn.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/create-symbolic-links) privilegium tilldelat.

* `conf.d/rewrites/rewrite.rules`

Filen inkluderas inifrån `.vhost` filer. Den har en uppsättning regler för omskrivning av `mod_rewrite`.

* `conf.d/variables/custom.vars`

Filen inkluderas inifrån `.vhost` filer. Du kan lägga till definitioner för Apache-variabler på den här platsen.

* `conf.d/variables/global.vars`

Filen inkluderas inifrån `dispatcher_vhost.conf` -fil. Du kan ändra Dispatcher och skriva om loggnivån i den här filen.

* `conf.dispatcher.d/available_farms/<CUSTOMER_CHOICE>.farm`

Du kan ha en eller flera av de här filerna och de innehåller grupper som matchar värdnamn och som gör att Dispatcher-modulen kan hantera varje grupp med olika regler. Filerna skapas i `available_farms` och aktiveras med en symbolisk länk i `enabled_farms` katalog. Från `.farm` filer, andra filer som filter, cacheregler och andra inkluderas.

* `conf.dispatcher.d/enabled_farms/<CUSTOMER_CHOICE>.farm`

Den här mappen innehåller relativa symboliska länkar till filer under conf.dispatcher.d/available_farm.

Exempelkommandon som krävs för att skapa dessa symboliska länkar:

Apple macOS, Linux och WSL

```
ln -s ../available_farms/wknd.farm wknd.farm
```

Microsoft Windows

```
mklink wknd.farm ..\available_farms\wknd.farm
```

>[!NOTE]
>
> När du arbetar med symboliska länkar under Windows bör du köra i en förhöjd kommandotolk, i Windows-undersystemet för Linux eller ha [Skapa symboliska länkar](https://learn.microsoft.com/en-us/windows/security/threat-protection/security-policy-settings/create-symbolic-links) privilegium tilldelat.

* `conf.dispatcher.d/cache/rules.any`

Filen inkluderas inifrån `.farm` filer. Den anger cachelagringsinställningar.

* `conf.dispatcher.d/clientheaders/clientheaders.any`

Filen inkluderas inifrån `.farm` filer. Den anger vilka begärandehuvuden som ska vidarebefordras till serverdelen.

* `conf.dispatcher.d/filters/filters.any`

Filen inkluderas inifrån `.farm` filer. Den har en uppsättning regler som ändrar vilken trafik som ska filtreras bort och inte hamna i bakgrunden.

* `conf.dispatcher.d/virtualhosts/virtualhosts.any`

Filen inkluderas inifrån `.farm` filer. Den har en lista med värdnamn eller URI-sökvägar som ska matchas med matchning av glob. Denna matchning avgör vilken serverdel som ska användas för att hantera en begäran.

* `opt-in/USE_SOURCES_DIRECTLY`

Den här filen ger en mer flexibel Dispatcher-konfiguration och tar bort tidigare begränsningar för antal och storlek på filer. SDK och runtime-modulen gör också att konfigurationen valideras och distribueras på ett bättre sätt.

Ovanstående filer refererar till de oföränderliga konfigurationsfiler som listas nedan. Ändringar av oföränderliga filer bearbetas inte av Dispatcher i molnmiljöer.

**Oändringsbara konfigurationsfiler**

Dessa filer ingår i grundramverket och följer standarder och bästa praxis. Filerna anses oföränderliga eftersom ändringar eller borttagningar lokalt inte påverkar distributionen eftersom de inte överförs till din molninstans.

Vi rekommenderar att ovanstående filer refererar till de oföränderliga filer som listas nedan, följt av eventuella ytterligare programsatser eller åsidosättningar. När Dispatcher-konfigurationen distribueras till en molnmiljö används den senaste versionen av de oföränderliga filerna, oavsett vilken version som användes i den lokala utvecklingen.

* `conf.d/available_vhosts/default.vhost`

Innehåller ett exempel på en virtuell värd. Skapa en kopia av den här filen för din egen virtuella värd, anpassa den, gå till `conf.d/enabled_vhosts` och skapa en symbolisk länk till en egen kopia.
Kopiera inte filen default.vhost direkt till `conf.d/enabled_vhosts`.

Kontrollera att det alltid finns ett virtuellt värdsystem som matchar ServerAlias `\*.local`, `localhost`och `127.0.0.1` som behövs för att göra Dispatcher-ogiltigförklaringen. Serveralias `*.adobeaemcloud.net` och `*.adobeaemcloud.com` behövs för interna Adobe-processer.

* `conf.d/dispatcher_vhost.conf`

En del av basramverket, som används för att illustrera hur dina virtuella värdar och globala variabler inkluderas.

* `conf.d/rewrites/default_rewrite.rules`

Skriv om standardregler som är lämpliga för ett standardprojekt. Om du behöver anpassa kan du ändra `rewrite.rules`. När du anpassar kan du fortfarande inkludera standardreglerna först, om de passar dina behov.

* `conf.dispatcher.d/available_farms/default.farm`

Innehåller ett exempel på en Dispatcher-servergrupp. Skapa en kopia av den här filen för din egen servergrupp, anpassa den, gå till `conf.d/enabled_farms` och skapa en symbolisk länk till en egen kopia.

* `conf.dispatcher.d/cache/default_invalidate.any`

En del av basramverket genereras vid start. Du är **obligatoriskt** för att inkludera den här filen i alla grupper som du definierar, i `cache/allowedClients` -avsnitt.

* `conf.dispatcher.d/cache/default_rules.any`

Standardcacheregler som är lämpliga för ett standardprojekt. Om du behöver anpassa kan du ändra `conf.dispatcher.d/cache/rules.any`. När du anpassar kan du fortfarande inkludera standardreglerna först, om de passar dina behov.

* `conf.dispatcher.d/clientheaders/default_clientheaders.any`

Standardbegäranrubriker som ska vidarebefordras till serverdelen, lämpliga för ett standardprojekt. Om du behöver anpassa kan du ändra `clientheaders.any`. När du anpassar kan du fortfarande inkludera standardrubrikerna för begäran först, om de passar dina behov.

* `conf.dispatcher.d/dispatcher.any`

En del av grundramverket som används för att illustrera hur Dispatcher-grupper inkluderas.

* `conf.dispatcher.d/filters/default_filters.any`

Standardfilter som passar för ett standardprojekt. Om du behöver anpassa kan du ändra `filters.any`. När du anpassar kan du fortfarande inkludera standardfiltren först, om de passar dina behov.

* `conf.dispatcher.d/renders/default_renders.any`

Den här filen genereras vid start och ingår i det grundläggande ramverket. Du är **obligatoriskt** för att inkludera den här filen i alla grupper som du definierar, i `renders` -avsnitt.

* `conf.dispatcher.d/virtualhosts/default_virtualhosts.any`

Standardvärdglobbning som passar för ett standardprojekt. Om du behöver anpassa kan du ändra `virtualhosts.any`. När du anpassar bör du inte ta med standardvärdglobbning, eftersom den matchar **var** inkommande begäran.

## Apache-moduler som stöds {#apache-modules}

Se [Apache-moduler som stöds](/help/implementing/dispatcher/disp-overview.md#supported-directives).

## Lokal validering {#local-validation-flexible-mode}

>[!NOTE]
>
>Avsnitten nedan innehåller kommandon som använder Mac- eller Linux®-versionerna av SDK, men Windows SDK kan också användas på ett liknande sätt.

Använd `validate.sh` skript enligt nedan:

```
$ validate.sh src/dispatcher
opt-in USE_SOURCES_DIRECTLY marker file detected
Phase 1: Dispatcher validator
Cloud manager validator 2.0.32
Phase 1 finished
Phase 2: httpd -t validation in docker image
values.csv not found in deployment folder: /Users/foo/src - using files in 'conf.d' and 'conf.dispatcher.d' subfolders directly
processing configuration subfolder: conf.d
processing configuration subfolder: conf.dispatcher.d
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

Skriptet har följande tre faser:

1. Den kör valideraren. Om konfigurationen inte är giltig misslyckas skriptet.
2. Det kör `httpd -t` för att testa om syntaxen är korrekt så att Apache httpd kan starta. Om det lyckas bör konfigurationen vara klar för distribution.
3. Kontrollerar att delmängden av Dispatcher SDK-konfigurationsfilerna, som är avsedda att vara oföränderliga enligt beskrivningen i [Filstruktursektion](##flexible-mode-file-structure), har inte ändrats och matchar den aktuella SDK-versionen.

Under en driftsättning av Cloud Manager `httpd -t` syntaxkontrollen körs också och fel inkluderas i Cloud Manager `Build Images step failure` log.

>[!NOTE]
>
>Se [Automatisk omladdning och validering](#automatic-loading) för ett effektivt alternativ till att köra `validate.sh` efter varje konfigurationsändring.

### Fas 1 {#first-phase}

Om ett direktiv inte är tillåtslista loggas ett fel och en avslutningskod som inte är noll returneras. Dessutom genomsöks alla filer ytterligare med mönstret `conf.dispatcher.d/enabled_farms/*.farm` och kontrollerar att

* Det finns ingen filterregel som tillåter via `/glob` (se [CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957)) om du vill ha mer information.
* Ingen administratörsfunktion visas. Åtkomst till banor som `/crx/de or /system/console`.

Valideringsverktyget rapporterar endast förbjuden användning av Apache-direktiv som inte har tillåtslista. Den rapporterar inte syntaktiska eller semantiska problem med din Apache-konfiguration eftersom den här informationen endast är tillgänglig för Apache-moduler i en körningsmiljö.

Nedan visas felsökningstekniker för felsökning av vanliga valideringsfel som genereras av verktyget:

**Det går inte att hitta en `conf.dispatcher.d` undermapp i arkivet**

Arkivet bör innehålla mapparna `conf.d` och `conf.dispatcher.d`. Observera att du **inte** bör
använda prefixet `etc/httpd` i arkivet.

**Det går inte att hitta någon servergrupp i`conf.dispatcher.d/enabled_farms`**

De aktiverade grupperna bör finnas i den angivna undermappen.

**Den inkluderade filen (..) måste ha följande namn: ...**

Det finns två avsnitt i servergruppskonfigurationen som **måste** inkludera en specifik fil: `/renders` och `/allowedClients` i `/cache` -avsnitt. Dessa avsnitt måste se ut så här:

```
/renders {
    $include "../renders/default_renders.any"
}
```

Och:

```
/allowedClients {
    $include "../cache/default_invalidate.any"
}
```

**Filen finns på en okänd plats: ...**

Det finns fyra avsnitt i servergruppskonfigurationen där du kan inkludera egna filer: `/clientheaders`, `filters`, `/rules` in `/cache` och `/virtualhosts`. De inkluderade filerna måste ha följande namn:

| Avsnitt | Inkludera filnamn |
|------------------|--------------------------------------|
| `/clientheaders` | `../clientheaders/clientheaders.any` |
| `/filters` | `../filters/filters.any` |
| `/rules` | `../cache/rules.any` |
| `/virtualhosts` | `../virtualhosts/virtualhosts.any` |

Du kan även inkludera **standard** version av dessa filer, vars namn föregås av ordet `default_`, till exempel `../filters/default_filters.any`.

**Inkludera programsats vid (..), utanför känd plats: ...**

Förutom de sex avsnitt som nämns i styckena ovan, får du inte använda `$include` följande skulle till exempel generera detta fel:

```
/invalidate {
    $include "../cache/invalidate.any"
}
```

**Tillåtna klienter/återgivningar inkluderas inte från: ...**

Det här felet genereras när du inte anger något &quot;include&quot; för `/renders` och `/allowedClients` i `/cache` -avsnitt. Se
**fil som ingår (..) måste ha följande namn: ...** för mer information.

**Filtret får inte använda glob-mönster för att tillåta förfrågningar**

Det är inte säkert att tillåta begäranden med `/glob` formatregel, som matchas mot den fullständiga förfrågningsraden, till exempel

```
/0100 {
    /type "allow" /glob "GET *.css *"
}
```

Den här programsatsen är avsedd att tillåta begäranden för `css` -filer, men tillåter även förfrågningar till **alla** resurs följt av frågesträng `?a=.css`. Det är därför förbjudet att använda sådana filter (se även CVE-2016-0957).

**Den inkluderade filen (..) matchar inte någon känd fil**

Som standard kan två typer av filer i din virtuella värdkonfiguration för Apache anges som bland annat: omskrivningar och variabler.

| Typ | Inkludera filnamn |
|-----------|---------------------------------|
| Skriver om | `conf.d/rewrites/rewrite.rules` |
| Variabel | `conf.d/variables/custom.vars` |

I flexibelt läge kan även andra filer inkluderas, förutsatt att de finns i underkataloger (på alla nivåer) av `conf.d` katalog med följande prefix.

| Inkludera filens övre katalogprefix |
|-------------------------------------|
| `conf.d/includes` |
| `conf.d/modsec` |
| `conf.d/rewrites` |

Du kan till exempel inkludera en fil i en skapad katalog under `conf.d/includes` katalog enligt följande:

```
Include conf.d/includes/mynewdirectory/myincludefile.conf
```

Du kan även inkludera **standard** version av omskrivningsreglerna, vars namn är `conf.d/rewrites/default_rewrite.rules`.
Observera att det inte finns någon standardversion av variabelfilerna.

**Inaktuell konfigurationslayout har identifierats, kompatibilitetsläge aktiveras**

Det här meddelandet anger att din konfiguration har den föråldrade layouten version 1 som innehåller en fullständig Apache-konfiguration och filer med `ams_` prefix. Den här konfigurationen stöds fortfarande för bakåtkompatibilitet, men du bör växla till den nya layouten.

Den första fasen kan också **kör separat**, i stället för från wrapper `validate.sh` skript.

När du springer mot din maven-artefakt eller din `dispatcher/src` underkatalog rapporterar den misslyckade valideringen:

```
$ validator full -relaxed dispatcher/src
Cloud manager validator 1.0.4
2019/06/19 15:41:37 Apache configuration uses non-allowlisted directives:
  conf.d/enabled_vhosts/aem_publish.vhost:46: LogLevel
2019/06/19 15:41:37 Dispatcher configuration validation failed:
  conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any: filter allows access to CRXDE
```

I Windows är Dispatcher-valideraren skiftlägeskänslig. Därför kan det misslyckas med att validera konfigurationen om du inte respekterar skiftläget för sökvägen där konfigurationen finns, till exempel:

```
bin\validator.exe -relaxed full src
Cloud manager validator 2.0.xx
2021/03/15 18:15:40 Dispatcher configuration validation failed:
  conf.dispatcher.d\available_farms\default.farm:15: parent directory outside server root: c:\k\a\aem-dispatcher-sdk-windows-symlinks-testing3\dispatcher\src
```

Undvik det här felet genom att kopiera och klistra in sökvägen från Utforskaren i Windows och sedan i kommandotolken med en `cd` till den banan.

### Fas 2 {#second-phase}

Den här fasen kontrollerar Apache-syntaxen genom att starta Apache HTTPD i en dockningsbehållare. Docker måste installeras lokalt, men observera att AEM inte behöver köras.

>[!NOTE]
>
>Windows-användare måste använda Windows 10 Professional eller andra distributioner som stöder Docker. Detta krav är ett krav för att köra och felsöka Dispatcher på en lokal dator.
>För både Windows och macOS rekommenderar Adobe att du använder Docker Desktop.

Denna fas kan också köras oberoende av varandra `bin/docker_run.sh src/dispatcher host.docker.internal:4503 8080`.

Under en driftsättning av Cloud Manager `httpd -t` syntaxkontroll körs också och eventuella fel inkluderas i felloggen för stegen Build Images i Cloud Manager.

### Fas 3 {#third-phase}

Om ett fel uppstår i den här fasen betyder det att Adobe har ändrat en eller flera oföränderliga filer. I så fall måste du ersätta motsvarande oföränderliga filer med den nya versionen som finns i `src` SDK-katalogen. Loggexemplet nedan visar detta problem:

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

Denna fas kan också köras oberoende av varandra `bin/docker_immutability_check.sh src/dispatcher`.

Dina lokala oföränderliga filer kan uppdateras genom att köra `bin/update_maven.sh src/dispatcher` skript i Dispatcher-mappen, där `src/dispatcher` är Dispatcher-konfigurationskatalogen. Skriptet uppdaterar även `pom.xml` filen i den överordnade katalogen så att också Maven immutability-kontrollerna uppdateras.

## Felsöka konfigurationen av Apache och Dispatcher {#debugging-apache-and-dispatcher-configuration}

Du kan köra Apache Dispatcher lokalt med `./bin/docker_run.sh src/dispatcher docker.for.mac.localhost:4503 8080`.

Som tidigare nämnts måste Docker installeras lokalt och det är inte nödvändigt att AEM körs. Windows-användare måste använda Windows 10 Professional eller andra distributioner som stöder Docker. Detta krav är ett krav för att köra och felsöka Dispatcher på en lokal dator.

Följande strategi kan användas för att öka loggutdata för modulen Dispatcher och för att se resultaten av `RewriteRule` utvärdering i både lokala miljöer och molnmiljöer.

Loggnivåer för dessa moduler definieras av variablerna `DISP_LOG_LEVEL` och `REWRITE_LOG_LEVEL`. De kan anges i filen `conf.d/variables/global.vars`. Den relevanta delen är följande:

```
# Log level for the dispatcher
#
# Possible values are: error, warn, info, debug and trace1
# Default value: warn
#
# Define DISP_LOG_LEVEL warn
 
# Log level for mod_rewrite
#
# Possible values are: error, warn, info, debug and trace1 - trace8
# Default value: warn
#
# To debug your RewriteRules, it is recommended to raise your log
# level to trace2.
#
# More information can be found at:
# https://httpd.apache.org/docs/current/mod/mod_rewrite.html#logging
#
# Define REWRITE_LOG_LEVEL warn
```

När du kör Dispatcher lokalt skrivs loggarna ut direkt till terminalutdata. Oftast vill du att de här loggarna ska vara i felsökningsversionen, vilket du kan göra genom att skicka felsökningsnivån som en parameter när du kör Docker. Till exempel: `DISP_LOG_LEVEL=Debug ./bin/docker_run.sh src docker.for.mac.localhost:4503 8080`.

Loggar för molnmiljöer visas via loggningstjänsten i Cloud Manager.

>[!NOTE]
>
>För miljöer på AEM as a Cloud Service är felsökningen den högsta nivån för vertikal intensitet. Spårningsloggsnivån stöds inte, så du bör undvika att ange den när du arbetar i molnmiljöer.

### Automatisk omladdning och validering {#automatic-reloading}

>[!NOTE]
>
>På grund av en Windows-begränsning är den här funktionen bara tillgänglig för macOS- och Linux®-användare.

Istället för att köra lokal validering (`validate.sh`) och starta dockningsbehållaren (`docker_run.sh`) varje gång konfigurationen ändras kan du köra `docker_run_hot_reload.sh` skript. Skriptet söker efter ändringar i konfigurationen och läser automatiskt in den igen och kör valideringen igen. Genom att använda det här alternativet kan du spara mycket tid vid felsökning.

Du kan köra skriptet med följande kommando: `./bin/docker_run_hot_reload.sh src/dispatcher host.docker.internal:4503 8080`

De första utdataraderna ser ut ungefär som de skulle köras för `docker_run.sh`. Till exempel:

```
~ bin/docker_run_hot_reload.sh src host.docker.internal:8081 8082
opt-in USE_SOURCES_DIRECTLY marker file detected
Running script /docker_entrypoint.d/10-check-environment.sh
Running script /docker_entrypoint.d/15-check-pod-name.sh
Running script /docker_entrypoint.d/20-create-docroots.sh
Running script /docker_entrypoint.d/30-wait-for-backend.sh
Waiting until host.docker.internal is available
host.docker.internal resolves to 192.168.65.2
Running script /docker_entrypoint.d/40-generate-allowed-clients.sh
Running script /docker_entrypoint.d/50-check-expiration.sh
Running script /docker_entrypoint.d/60-check-loglevel.sh
Running script /docker_entrypoint.d/70-check-forwarded-host-secret.sh
Running script /docker_entrypoint.d/80-frontend-domain.sh
Running script /docker_entrypoint.d/zzz-import-sdk-config.sh
WARN Mon Jul  4 09:53:54 UTC 2022: Pseudo symlink conf.d seems to point to a non-existing file!
INFO Mon Jul  4 09:53:55 UTC 2022: Copied customer configuration to /etc/httpd.
INFO Mon Jul  4 09:53:55 UTC 2022: Start testing
Cloud manager validator 2.0.43
2022/07/04 09:53:55 No issues found
INFO Mon Jul  4 09:53:55 UTC 2022: Testing with fresh base configuration files.
INFO Mon Jul  4 09:53:55 UTC 2022: Apache httpd informationServer version: Apache/2.4.54 (Unix)
```

### Infoga anpassade miljövariabler {#environment-variables}

Du kan använda anpassade miljövariabler med SDK:n för dispatcher genom att ange dem i en separat fil och referera till dem i `ENV_FILE` systemvariabel innan den lokala dispatchern startas.

En fil med anpassade miljövariabler skulle se ut så här:

```
COMMERCE_ENDPOINT=commerce-host
AEM_HTTP_PROXY_HOST=host.docker.internal
AEM_HTTP_PROXY_PORT=8000
```

Och den kan användas i den lokala SDK:n för dispatcher med följande kommandon:

```
export ENV_FILE=custom.env
./bin/docker_run.sh src/dispatcher docker.for.mac.localhost:4503 8080
```

## Olika Dispatcher-konfigurationer per miljö {#different-dispatcher-configurations-per-environment}

För närvarande används samma Dispatcher-konfiguration för alla miljöer på AEM as a Cloud Service. Körningsmiljön har en miljövariabel `ENVIRONMENT_TYPE` som innehåller det aktuella körningsläget (utveckling, scen eller produktion) och en&quot;definition&quot;. &quot;define&quot; kan vara `ENVIRONMENT_DEV`, `ENVIRONMENT_STAGE`, eller `ENVIRONMENT_PROD`. I Apache-konfigurationen kan variabeln användas direkt i ett uttryck. Alternativt kan&quot;define&quot; användas för att bygga logik:

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

Du kan också använda Cloud Manager-miljövariabler i din httpd/dispatcher-konfiguration, men inte miljöhemligheter. Den här metoden är särskilt viktig om ett program har flera dev-miljöer och vissa av dessa dev-miljöer har olika värden för httpd/dispatcher-konfigurationen. Samma ${VIRTUALHOST} syntax används som i exemplet ovan, men Define-deklarationerna i variabelfilen ovan används inte. Läs [Dokumentation för Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) för instruktioner om hur du konfigurerar Cloud Manager-miljövariabler.

När du testar konfigurationen lokalt kan du simulera olika miljötyper genom att skicka variabeln `DISP_RUN_MODE` till `docker_run.sh` direkt:

```
$ DISP_RUN_MODE=stage docker_run.sh src docker.for.mac.localhost:4503 8080
```

Standardkörningsläget när inget värde för DISP_RUN_MODE skickas är &quot;dev&quot;.
Kör skriptet för att få en fullständig lista över tillgängliga alternativ och variabler `docker_run.sh` utan argument.

## Visa Dispatcher-konfigurationen som används av Docker-behållaren {#viewing-dispatcher-configuration-in-use-by-docker-container}

Med miljöspecifika konfigurationer kan det vara svårt att avgöra hur Dispatcher-konfigurationen ser ut. När du har startat din dockningsbehållare med `docker_run.sh`kan den dumpas enligt följande:

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

## Migrera från äldre läge till flexibelt läge {#migrating}

Med Cloud Manager 2021.7.0 genererar nya Cloud Manager-program maven-projektstrukturer med [AEM 28](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/overview.html) eller högre, som innehåller filen **opt-in/USE_SOURCES_DIRECTLY**. Det tar bort tidigare begränsningar i [äldre läge](/help/implementing/dispatcher/validation-debug-legacy.md) runt antalet och storleken på filer, vilket även gör att SDK och runtime-modulen validerar och distribuerar konfigurationen på ett förbättrat sätt. Om Dispatcher-konfigurationen inte har den här filen rekommenderar vi att du migrerar. Följ de här stegen för att säkerställa en säker övergång:

1. **Lokal testning.** Lägg till mappen och filen med hjälp av SDK:t för de senaste Dispatcher-verktygen `opt-in/USE_SOURCES_DIRECTLY`. Följ instruktionerna för lokal validering i den här artikeln så att du kan testa att Dispatcher fungerar lokalt.
1. **Molnutvecklingstestning:**
   * Verkställ filen `opt-in/USE_SOURCES_DIRECTLY` till en Git-gren som distribueras av icke-produktionsflödet till en molnutvecklingsmiljö.
   * Använd Cloud Manager för att distribuera till en molnutvecklingsmiljö.
   * Testa noggrant. Det är viktigt att verifiera att konfigurationen av Apache och Dispatcher fungerar som du förväntar dig innan du distribuerar ändringar i högre miljöer. Kontrollera alla beteenden som hör till din anpassade konfiguration. Registrera en kundsupportanmälan om du tror att den distribuerade Dispatcher-konfigurationen inte återspeglar din anpassade konfiguration.

   >[!NOTE]
   >
   >I det flexibla läget bör du använda relativa sökvägar i stället för absoluta sökvägar.
1. **Distribuera till produktion:**
   * Verkställ filen `opt-in/USE_SOURCES_DIRECTLY` till en Git-gren som distribueras via produktionsflödet till molnscenen och produktionsmiljöerna.
   * Använd Cloud Manager för att distribuera till testmiljöer.
   * Testa noggrant. Det är viktigt att verifiera att konfigurationen av Apache och Dispatcher fungerar som du förväntar dig innan du distribuerar ändringar i högre miljöer. Kontrollera alla beteenden som är relaterade till din anpassade konfiguration. Registrera en kundsupportanmälan om du tror att den distribuerade Dispatcher-konfigurationen inte återspeglar din anpassade konfiguration.
   * Använd Cloud Manager för att fortsätta distributionen till produktionen.
