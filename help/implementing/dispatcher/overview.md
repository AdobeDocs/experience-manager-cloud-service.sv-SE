---
title: Dispatcher i molnet
description: 'Dispatcher i molnet '
translation-type: tm+mt
source-git-commit: 2ab8a4fb492b85c1a9b42442d868cdbc329756cf

---


# Dispatcher i molnet {#Dispatcher-in-the-cloud}

## Konfiguration och testning av Apache och Dispatcher {#apache-and-dispatcher-configuration-and-testing}

I det här avsnittet beskrivs hur du strukturerar AEM som en molntjänst-API- och Dispatcher-konfiguration samt hur du validerar och kör den lokalt innan du distribuerar den i molnmiljöer. Det beskriver även felsökning i molnmiljöer. Mer information om Dispatcher finns i dokumentationen [till](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/dispatcher.html)AEM Dispatcher.

>[!NOTE]
>Windows-användare måste använda Windows 10 Professional eller andra distributioner som stöder Docker. Detta är en förutsättning för att du ska kunna köra och felsöka Dispatcher på en lokal dator. Avsnitten nedan innehåller kommandon som använder Mac- eller Linux-versionerna av SDK, men Windows SDK kan användas på liknande sätt.

## Dispatcher Tools {#dispatcher-sdk}

Dispatcher-verktygen är en del av den övergripande AEM-filen som en molntjänst-SDK och tillhandahåller:

* En vaniljfilstruktur som innehåller de konfigurationsfiler som ska ingå i ett maven-projekt för dispatcher.
* Verktyg för att kunderna ska kunna validera en dispatcherkonfiguration lokalt.
* En Docker-bild som tar upp dispatchern lokalt.

## Hämta och extrahera verktygen {#extracting-the-sdk}

Dispatcher Tools kan laddas ned från en zip-fil på [Software Distribution](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html) portal. Observera att åtkomsten till SDK-listorna är begränsad till dem som har AEM Managed Services eller AEM som molntjänster. Alla nya konfigurationer som är tillgängliga i den nya versionen av dispatcher Tools kan användas för att distribuera till molnmiljöer där den versionen av AEM körs i molnet eller senare.

**För macOS och Linux** hämtar du gränssnittsskriptet till en mapp på datorn, gör det körbart och kör det. Det extraherar Dispatcher Tools-filerna under den katalog som du lagrade dem i (där `version` är versionen av Dispatcher Tools).

```bash
$ chmod +x DispatcherSDKv<version>.sh
$ ./DispatcherSDKv<version>.sh
Verifying archive integrity...  100%   All good.
Uncompressing DispatcherSDKv<version>  100% 
```

**För Windows** hämtar du zip-arkivet och extraherar det.

## Filstruktur {#file-structure}

Strukturen för projektets dispatcher-undermapp beskrivs nedan och bör kopieras till maven project dispatcher-mappen:

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

Du kan ha en eller flera av dessa filer. De innehåller `<VirtualHost>` poster som matchar värdnamn och tillåter att Apache hanterar varje domäntrafik med olika regler. Filerna skapas i `available_vhosts` katalogen och aktiveras med en symbolisk länk i `enabled_vhosts` katalogen. Från `.vhost` filerna inkluderas andra filer, som omskrivningar och variabler.

* `conf.d/rewrites/rewrite.rules`

Den här filen inkluderas inifrån dina `.vhost` filer. Den har en uppsättning regler för omskrivning `mod_rewrite`.

>[!NOTE]
>
>För närvarande måste en enda omskrivningsfil användas i stället för platsspecifika filer. Filstorleken måste vara mindre än 1 MB.

* `conf.d/variables/custom.vars`

Den här filen inkluderas inifrån dina `.vhost` filer. Du kan ange definitioner för Apache-variabler på den här platsen.

* `conf.d/variables/global.vars`

Den här filen inkluderas inifrån `dispatcher_vhost.conf` filen. Du kan ändra din dispatcher och skriva om loggnivån i den här filen.

* `conf.dispatcher.d/available_farms/<CUSTOMER_CHOICE>.farm`

Du kan ha en eller flera av de här filerna och de innehåller grupper som matchar värdnamn och som gör att dispatchermodulen kan hantera varje grupp med olika regler. Filerna skapas i `available_farms` katalogen och aktiveras med en symbolisk länk i `enabled_farms` katalogen. Från `.farm` filerna inkluderas andra filer som filter, cacheregler och andra.

* `conf.dispatcher.d/cache/rules.any`

Den här filen inkluderas inifrån dina `.farm` filer. Den anger cachelagringsinställningar.

* `conf.dispatcher.d/clientheaders/clientheaders.any`

Den här filen inkluderas inifrån dina `.farm` filer. Den anger vilka begärandehuvuden som ska vidarebefordras till serverdelen.

* `conf.dispatcher.d/filters/filters.any`

Den här filen inkluderas inifrån dina `.farm` filer. Den har en uppsättning regler som ändrar vilken trafik som ska filtreras bort och inte hamna i bakgrunden.

* `conf.dispatcher.d/virtualhosts/virtualhosts.any`

Den här filen inkluderas inifrån dina `.farm` filer. Den har en lista med värdnamn eller URI-sökvägar som ska matchas med matchning av glob. Detta avgör vilken serverdel som ska användas för att hantera en begäran.

Ovanstående filer refererar till de oföränderliga konfigurationsfiler som listas nedan. Ändringar av oföränderliga filer bearbetas inte av utskickare i molnmiljöer.

**Oändringsbara konfigurationsfiler**

Dessa filer ingår i grundramverket och följer standarder och bästa praxis. Filerna anses oföränderliga eftersom ändringar eller borttagningar av dem lokalt inte påverkar distributionen eftersom de inte överförs till din molninstans.

Vi rekommenderar att ovanstående filer refererar till de oföränderliga filer som listas nedan, följt av eventuella ytterligare programsatser eller åsidosättningar. När dispatcherkonfigurationen distribueras till en molnmiljö används den senaste versionen av de oföränderliga filerna, oavsett vilken version som användes i den lokala utvecklingen.

* `conf.d/available_vhosts/default.vhost`

Innehåller ett exempel på en virtuell värd. För din egen virtuella värd skapar du en kopia av den här filen, anpassar den, går till `conf.d/enabled_vhosts` och skapar en symbolisk länk till din anpassade kopia.

* `conf.d/dispatcher_vhost.conf`

En del av basramverket, som används för att illustrera hur dina virtuella värdar och globala variabler inkluderas.

* `conf.d/rewrites/default_rewrite.rules`

Standardregler för omskrivning som är lämpliga för ett standardprojekt. Ändra `rewrite.rules`om du behöver anpassa. När du anpassar kan du fortfarande inkludera standardreglerna först, om de passar dina behov.

* `conf.dispatcher.d/available_farms/default.farm`

Innehåller en exempelgrupp för dispatcher. Skapa en kopia av den här filen för din egen servergrupp, anpassa den, gå till `conf.d/enabled_farms` och skapa en symbolisk länk till din anpassade kopia.

* `conf.dispatcher.d/cache/default_invalidate.any`

En del av basramverket genereras vid start. Du **måste** inkludera den här filen i alla grupper som du definierar i `cache/allowedClients` avsnittet.

* `conf.dispatcher.d/cache/default_rules.any`

Standardcacheregler som är lämpliga för ett standardprojekt. Ändra `conf.dispatcher.d/cache/rules.any`om du behöver anpassa. När du anpassar kan du fortfarande inkludera standardreglerna först, om de passar dina behov.

* `conf.dispatcher.d/clientheaders/default_clientheaders.any`

Standardbegäranrubriker som ska vidarebefordras till serverdelen, lämpliga för ett standardprojekt. Ändra `clientheaders.any`om du behöver anpassa. När du anpassar kan du fortfarande inkludera standardrubrikerna för begäran först, om de passar dina behov.

* `conf.dispatcher.d/dispatcher.any`

En del av grundramverket, som används för att illustrera hur dina dispatchergrupper inkluderas.

* `conf.dispatcher.d/filters/default_filters.any`

Standardfilter som passar för ett standardprojekt. Ändra `filters.any`om du behöver anpassa. När du anpassar kan du fortfarande inkludera standardfiltren först, om de passar dina behov.

* `conf.dispatcher.d/renders/default_renders.any`

Den här filen genereras vid start och ingår i det grundläggande ramverket. Du **måste** inkludera den här filen i alla grupper som du definierar i `renders` avsnittet.

* `conf.dispatcher.d/virtualhosts/default_virtualhosts.any`

Standardvärdglobbning som passar för ett standardprojekt. Ändra `virtualhosts.any`om du behöver anpassa. När du anpassar bör du inte ta med standardvärddatorns ordlista, eftersom den matchar **varje** inkommande begäran.

>[!NOTE]
>AEM som en molntjänstens maven-arkityp genererar samma filstruktur för dispatcherkonfiguration.

Avsnitten nedan beskriver hur konfigurationen valideras lokalt så att den kan skicka den associerade kvalitetsgaten i Cloud Manager när en intern release distribueras.

## Lokal validering av Dispatcher-konfiguration {#local-validation-of-dispatcher-configuration}

Valideringsverktyget finns i SDK på `bin/validator` en binär Mac OS-, Linux- eller Windows-fil, vilket gör att kunderna kan köra samma validering som Cloud Manager gör när en release skapas och distribueras.

Den anropas som: `validator full [-d folder] [-w whitelist] zip-file | src folder`

Verktyget validerar Apache- och Dispatcher-konfigurationen. Den söker igenom alla filer med mönster `conf.d/enabled_vhosts/*.vhost` och kontrollerar att endast godkända direktiv används. De direktiv som tillåts i Apache-konfigurationsfiler kan listas genom att köra validerarens vitlistkommando:

```
$ validator whitelist
Cloud manager validator 2.0.4
 
Whitelisted directives:
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
| `mod_auth_basic` | [https://httpd.apache.org/docs/2.4/mod/mod_auth_basic.html](https://httpd.apache.org/docs/2.4/mod/mod_auth_basic.html) |
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

Kunder kan inte lägga till godtyckliga moduler, men ytterligare moduler kan övervägas för att ingå i produkten i framtiden. Kunderna hittar listan över direktiv som är tillgängliga för en viss Dispatcher-version genom att köra&quot;validator whitelist&quot; i SDK:n, vilket beskrivs i Dispatcher Tools-dokumentationen.

Vitlistan innehåller en lista över Apache-direktiv som tillåts i en kundkonfiguration. Om ett direktiv inte är vitlistat loggas ett fel och en avslutningskod som inte är noll returneras. Om ingen vitlista anges på kommandoraden (vilket är det sätt som det ska anropas) använder verktyget en standardvitlista som Cloud Manager använder för validering innan distributionen till molnmiljöer.

Dessutom genomsöks alla filer med mönster `conf.dispatcher.d/enabled_farms/*.farm` och följande kontrolleras:

* Det finns ingen filterregel som tillåter via `/glob` (mer information finns i [CVE-2016-0957](https://nvd.nist.gov/vuln/detail/CVE-2016-0957) )
* Ingen administratörsfunktion visas. Åtkomst till banor som `/crx/de or /system/console`.

När programmet körs mot din maven-artefakt eller din `dispatcher/src` underkatalog rapporterar det valideringsfel:

```
$ validator full dispatcher/src
Cloud manager validator 1.0.4
2019/06/19 15:41:37 Apache configuration uses non-whitelisted directives:
 conf.d/enabled_vhosts/aem_publish.vhost:46: LogLevel
2019/06/19 15:41:37 Dispatcher configuration validation failed:
 conf.dispatcher.d/enabled_farms/999_ams_publish_farm.any: filter allows access to CRXDE
```

Observera att valideringsverktyget endast rapporterar förbjuden användning av Apache-direktiv som inte har vitlistats. Den rapporterar inte syntaktiska eller semantiska problem med din Apache-konfiguration eftersom den här informationen endast är tillgänglig för Apache-moduler i en körningsmiljö.

När inga valideringsfel rapporteras är konfigurationen klar för distribution.

Nedan visas felsökningstekniker för felsökning av vanliga valideringsfel som genereras av verktyget:

**det går inte att hitta en undermapp`conf.dispatcher.d`i arkivet**

Arkivet bör innehålla mappar `conf.d` och `conf.dispatcher.d`. Observera att du **inte** bör använda prefixet `etc/httpd` i ditt arkiv.

**det gick inte att hitta någon servergrupp i`conf.dispatcher.d/enabled_farms`**

De aktiverade grupperna ska finnas i den undermappen.

**filen som ingår (..) måste ha följande namn:...**

Det finns två avsnitt i servergruppskonfigurationen som **måste** innehålla en specifik fil: och `/renders` i `/allowedClients` `/cache` avsnittet. De här avsnitten måste se ut så här:

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

**filen finns på okänd plats:...**

Det finns fyra avsnitt i servergruppskonfigurationen där du kan inkludera din egen fil: `/clientheaders`, `filters`, `/rules` i `/cache` avsnitt och `/virtualhosts`. De inkluderade filerna måste ha följande namn:

| Avsnitt | Inkludera filnamn |
|------------------|--------------------------------------|
| `/clientheaders` | `../clientheaders/clientheaders.any` |
| `/filters` | `../filters/filters.any` |
| `/rules` | `../cache/rules.any` |
| `/virtualhosts` | `../virtualhosts/virtualhosts.any` |

Du kan också inkludera **standardversionen** av de filer vars namn är föregånget av ordet `default_`, t.ex. `../filters/default_filters.any`.

**include-sats på (..), utanför känd plats:...**

Förutom de sex avsnitt som nämns i styckena ovan, får du inte använda programsatsen `$include` . Följande skulle t.ex. generera detta fel:

```
/invalidate {
    $include "../cache/invalidate.any"
}
```

**Tillåtna klienter/renderare inkluderas inte från:...**

Det här felet genereras när du inte anger någon inkludering för `/renders` och `/allowedClients` i `/cache` avsnittet. **Se den** fil som ingår (..) måste ha följande namn:... för mer information.

**filtret får inte använda glob-mönster för att tillåta förfrågningar**

Det är inte säkert att tillåta förfrågningar med en `/glob` formatregel som matchas mot den fullständiga förfrågningsraden, t.ex.

```
/0100 {
    /type "allow" /glob "GET *.css *"
}
```

Programsatsen är avsedd att tillåta begäranden om `css` filer, men tillåter även begäranden till **alla** resurser följt av frågesträngen `?a=.css`. Det är därför förbjudet att använda sådana filter (se även CVE-2016-0957).

**den inkluderade filen (..) matchar ingen känd fil**

Det finns två typer av filer i din virtuella värdkonfiguration för Apache som kan anges enligt följande: skriver om och variabler.
De inkluderade filerna måste ha följande namn:

| Typ | Inkludera filnamn |
|-----------|---------------------------------|
| Skriver om | `conf.d/rewrites/rewrite.rules` |
| Variabler | `conf.d/variables/custom.vars` |

Du kan också inkludera **standardversionen** av reglerna för omskrivning, vars namn är `conf.d/rewrites/default_rewrite.rules`.
Observera att det inte finns någon standardversion av variabelfilerna.

**Inaktuell konfigurationslayout har identifierats, kompatibilitetsläge aktiveras**

Det här meddelandet anger att din konfiguration har den föråldrade layouten version 1 som innehåller en completeApache-konfiguration och filer med `ams_` prefix. Detta stöds fortfarande för bakåtkompatibilitet, men du bör växla till den nya layouten.

## Testa Apache- och Dispatcher-konfigurationen lokalt {#testing-apache-and-dispatcher-configuration-locally}

Du kan också testa konfigurationen av Apache och Dispatcher lokalt. Docker måste vara installerat lokalt och konfigurationen måste godkännas enligt den validering som beskrivs ovan.

Genom att använda parametern &quot;`-d`&quot; skickar valideraren en mapp med alla konfigurationsfiler som behövs för dispatchern.

Sedan kan skriptet peka på den mappen och påbörja `docker_run.sh` behållaren med din konfiguration.

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

Detta startar dispatchern i en behållare med dess serverdel som pekar på en AEM-instans som körs på din lokala Mac OS-dator vid port 4503.

## Felsöka konfigurationen av Apache och Dispatcher {#debugging-apache-and-dispatcher-configuration}

Följande strategi kan användas för att öka loggutdata för dispatchermodulen och för att se resultatet av `RewriteRule` utvärderingen i både lokala miljöer och molnmiljöer.

Loggnivåer för dessa moduler definieras av variablerna `DISP_LOG_LEVEL` och `REWRITE_LOG_LEVEL`. De kan ställas in i filen `conf.d/variables/global.vars`. Den relevanta delen är följande:

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

När du kör Dispatcher lokalt skrivs loggarna också ut direkt till terminalutdata. Oftast ska loggarna vara i DEBUG, vilket kan uppnås genom att skicka felsökningsnivån som en parameter när Docker körs. Exempel:

`DISP_LOG_LEVEL=Debug ./bin/docker_run.sh out docker.for.mac.localhost:4503 8080`

Loggar för molnmiljöer visas via loggningstjänsten i Cloud Manager.

## Olika Dispatcher-konfigurationer per miljö {#different-dispatcher-configurations-per-environment}

Nu används samma dispatcherkonfiguration för alla AEM-miljöer som molntjänstmiljöer. Körningsmiljön kommer att ha en miljövariabel `ENVIRONMENT_TYPE` som innehåller det aktuella körningsläget (dev, stage eller prod) samt en definition. Definitionen kan vara `ENVIRONMENT_DEV`, `ENVIRONMENT_STAGE` eller `ENVIRONMENT_PROD`. I Apache-konfigurationen kan variabeln användas direkt i ett uttryck. Definitionen kan också användas för att skapa logik:

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

När du testar konfigurationen lokalt kan du simulera olika miljötyper genom att skicka variabeln `DISP_RUN_MODE` till `docker_run.sh` skriptet direkt:

```
$ DISP_RUN_MODE=stage docker_run.sh out docker.for.mac.localhost:4503 8080
```

Standardkörningsläget när inget värde för DISP_RUN_MODE skickas är &quot;dev&quot;.
Om du vill se en fullständig lista över tillgängliga alternativ och variabler kör du skriptet `docker_run.sh` utan argument.

## Visa Dispatcher-konfigurationen som används av Docker-behållaren {#viewing-dispatcher-configuration-in-use-by-docker-container}

Med miljöspecifika konfigurationer kan det vara svårt att avgöra hur den faktiska Dispatcher-konfigurationen ser ut. När du har startat din dockningsbehållare med `docker_run.sh` den kan den dumpas enligt följande:

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

## De viktigaste skillnaderna mellan AMS Dispatcher och AEM som molntjänst {#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

Som beskrivs på referenssidan ovan liknar konfigurationen av Apache och Dispatcher i AEM som en molntjänst AMS. De viktigaste skillnaderna är:

* I AEM som en molntjänst kan vissa Apache-direktiv inte användas (till exempel `Listen` eller `LogLevel`)
* I AEM som en molntjänst kan endast vissa delar av Dispatcher-konfigurationen placeras i inkluderingsfiler och deras namn är viktigt. Filterregler som du vill återanvända på olika värdar måste till exempel läggas i en fil som kallas `filters/filters.any`. Mer information finns på referenssidan.
* I AEM som en molntjänst finns det extra validering för att förhindra säkerhetsproblem och förhindra att filterregler skrivs med `/glob` . Eftersom `deny *` används i stället för `allow *` (vilket inte kan användas) har kunderna nytta av att köra Dispatcher lokalt och göra testversionen och felsökningen. Loggarna visar exakt vilka sökvägar Dispatcher-filtren blockerar för att de ska kunna läggas till.

## Riktlinjer för migrering av dispatcherkonfiguration från AMS till AEM som en molntjänst

Konfigurationsstrukturen för dispatcher har skillnader mellan hanterade tjänster och AEM som en molntjänst. Nedan visas en steg-för-steg-guide om hur du migrerar från AMS Dispatcher-konfiguration version 2 till AEM som en molntjänst.

## Konvertera en AMS till en AEM-tjänst som en konfiguration för Cloud Service Dispatcher

I följande avsnitt ges stegvisa instruktioner för hur du konverterar en AMS-konfiguration. Du förutsätts ha ett arkiv med en struktur som liknar den som beskrivs i [Cloud Manager Dispatcher-konfigurationen](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)

### Extrahera arkivet och ta bort ett eventuellt prefix

Extrahera arkivet till en mapp och kontrollera att de omedelbara undermapparna börjar med `conf`, `conf.d``conf.dispatcher.d` och `conf.modules.d`. Om de inte gör det flyttar du dem uppåt i hierarkin.

### Ta bort oanvända undermappar och filer

Ta bort undermappar `conf` och `conf.modules.d`filer som matchar `conf.d/*.conf`.

### Ta bort alla virtuella värdar som inte är publicerade

Ta bort alla virtuella värdfiler i `conf.d/enabled_vhosts` som har `author`, `unhealthy`, `health`eller`lc` `flush` i sitt namn. Alla virtuella värdfiler i `conf.d/available_vhosts` som inte är länkade till kan också tas bort.

### Ta bort eller kommentera virtuella värdsektioner som inte refererar till port 80

Om du fortfarande har avsnitt i dina virtuella värdfiler som endast refererar till andra portar än port 80, t.ex.

```
<VirtualHost *:443>
...
</VirtualHost>
```

ta bort eller kommentera dem. Programsatserna i de här avsnitten bearbetas inte, men om du behåller dem kan du ändå redigera dem utan någon effekt, vilket är förvirrande.

### Kontrollera återskrivningar

Ange katalog `conf.d/rewrites`.

Ta bort alla filer med namn `base_rewrite.rules` och `xforwarded_forcessl_rewrite.rules` komma ihåg att ta bort `Include` programsatser i de virtuella värdfilerna som refererar till dem.

Om det `conf.d/rewrites` nu finns en enda fil bör namnet ändras till `rewrite.rules` `Include` och glöm inte att anpassa de programsatser som refererar till den filen i de virtuella värdfilerna.

Om mappen däremot innehåller flera, virtuella värdspecifika filer, ska deras innehåll kopieras till den programsats som refererar till dem i de virtuella värdfilerna. `Include`

### Kontrollera variabler

Ange katalog `conf.d/variables`.

Ta bort alla filer med namnet `ams_default.vars` och kom ihåg att ta bort `Include` programsatser i virtualhost-filerna som refererar till dem.

Om det `conf.d/variables` nu finns en enda fil bör namnet ändras till `custom.vars` `Include` och glöm inte att anpassa de programsatser som refererar till den filen i de virtuella värdfilerna.

Om mappen däremot innehåller flera, virtuella värdspecifika filer, ska deras innehåll kopieras till den programsats som refererar till dem i de virtuella värdfilerna. `Include`

### Ta bort vitlistor

Ta bort mappen `conf.d/whitelists` och ta bort `Include` programsatser i de virtuella värdfilerna som refererar till en fil i den undermappen.

### Ersätt alla variabler som inte längre är tillgängliga

I alla virtuella värdfiler:

Byt namn `PUBLISH_DOCROOT` till `DOCROOT`Ta bort avsnitt som refererar till variabler med namnet `DISP_ID`, `PUBLISH_FORCE_SSL` eller `PUBLISH_WHITELIST_ENABLED`

### Kontrollera ditt tillstånd genom att köra valideraren

Kör dispatchervalideraren i din katalog med `httpd` underkommandot:

```
$ validator httpd .
```

Om du ser fel om saknade inkluderingsfiler ska du kontrollera om du har bytt namn på filerna korrekt.

Om Apache-direktiv som inte är vitlistade visas tar du bort dem.

### Ta bort alla icke-publicerade servergrupper

Ta bort en servergruppsfil i `conf.dispatcher.d/enabled_farms` som har `author`, `unhealthy`, `health`eller`lc` `flush` i sitt namn. Alla gruppfiler i `conf.dispatcher.d/available_farms` som inte är länkade till kan också tas bort.

### Byt namn på servergruppsfiler

Alla grupper i `conf.d/enabled_farms` måste byta namn för att matcha mönstret `*.farm`så t.ex. en servergruppsfil som anropas `customerX_farm.any` bör byta namn `customerX.farm`.

### Kontrollera cache

Ange katalog `conf.dispatcher.d/cache`.

Ta bort alla filer som har prefix `ams_`.

Om `conf.dispatcher.d/cache` är tomt kopierar du filen `conf.dispatcher.d/cache/rules.any`från standarddispatcherkonfigurationen till den här mappen. Standardkonfigurationen för skickning finns i mappen `src` för denna SDK. Glöm inte att`$include` även anpassa de satser som refererar till `ams_*_cache.any` regelfilerna i servergruppsfilerna.

Om den `conf.dispatcher.d/cache` nu innehåller en enda fil med suffix `_cache.any`bör du byta namn på den `rules.any` `$include` och inte glömma att anpassa programsatserna som refererar till den filen i servergruppsfilerna.

Om mappen emellertid innehåller flera, gruppspecifika filer med det mönstret, ska deras innehåll kopieras till den programsats som refererar till dem i servergruppsfilerna. `$include`

Ta bort alla filer som har suffixet `_invalidate_allowed.any`.

Kopiera filen `conf.dispatcher.d/cache/default_invalidate_any` från defaultAEM i Cloud Dispatcher-konfigurationen till den platsen.

I varje servergruppsfil tar du bort allt innehåll i `cache/allowedClients` avsnittet och ersätter det med:

```
$include "../cache/default_invalidate.any"
```

### Kontrollera klientrubriker

Ange katalog `conf.dispatcher.d/clientheaders`.

Ta bort alla filer som har prefix `ams_`.

Om `conf.dispatcher.d/clientheaders` nu innehåller en enda fil med suffix `_clientheaders.any`bör du byta namn på den `clientheaders.any` `$include` och inte glömma att anpassa programsatserna som refererar till den filen i servergruppsfilerna.

Om mappen emellertid innehåller flera, gruppspecifika filer med det mönstret, ska deras innehåll kopieras till den programsats som refererar till dem i servergruppsfilerna. `$include`

Kopiera filen `conf.dispatcher/clientheaders/default_clientheaders.any` från defaultAEM som en konfiguration för Cloud Service Dispatcher till den platsen.

Ersätt alla klientrubriker med programsatser som ser ut så här i varje servergruppsfil:

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

Ta bort alla filer som har prefix `ams_`.

Om det `conf.dispatcher.d/filters` nu finns en enda fil bör namnet ändras till`filters.any` `$include` den och glöm inte att anpassa de programsatser som refererar till den filen i servergruppsfilerna också.

Om mappen emellertid innehåller flera, gruppspecifika filer med det mönstret, ska deras innehåll kopieras till den programsats som refererar till dem i servergruppsfilerna. `$include`

Kopiera filen `conf.dispatcher/filters/default_filters.any` från defaultAEM som en konfiguration för Cloud Service Dispatcher till den platsen.

Ersätt alla filter med programsatser som ser ut så här i varje servergruppsfil:

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

Kopiera filen `conf.dispatcher.d/renders/default_renders.any` från defaultAEM som en konfiguration för Cloud Service Dispatcher till den platsen.

I varje servergruppsfil tar du bort allt innehåll i `renders` avsnittet och ersätter det med:

```
$include "../renders/default_renders.any"
```

### Kontrollera virtuella värdar

Byt namn på katalogen `conf.dispatcher.d/vhosts` till `conf.dispatcher.d/virtualhosts` och ange den.

Ta bort alla filer som har prefix `ams_`.

Om det `conf.dispatcher.d/virtualhosts` nu finns en enda fil bör namnet ändras till`virtualhosts.any` `$include` den och glöm inte att anpassa de programsatser som refererar till den filen i servergruppsfilerna också.

Om mappen emellertid innehåller flera, gruppspecifika filer med det mönstret, ska deras innehåll kopieras till den programsats som refererar till dem i servergruppsfilerna. `$include`

Kopiera filen `conf.dispatcher/virtualhosts/default_virtualhosts.any` från defaultAEM som en konfiguration för Cloud Service Dispatcher till den platsen.

Ersätt alla filter med programsatser som ser ut så här i varje servergruppsfil:

```
$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"
```

med programsatsen:

```
$include "../virtualhosts/default_virtualhosts.any"
```

### Kontrollera ditt tillstånd genom att köra valideraren

Kör AEM som en Cloud Service Dispatcher-validerare i din katalog med `dispatcher` underkommandot:

```
$ validator dispatcher .
```

Om du ser fel om saknade inkluderingsfiler ska du kontrollera om du har bytt namn på filerna korrekt.

Om du ser fel som rör en odefinierad variabel `PUBLISH_DOCROOT`ändrar du namnet till `DOCROOT`.

Mer information om alla andra fel finns i felsökningsavsnittet i dokumentationen för verktyget för felsökning.

### Testa konfigurationen med en lokal distribution (kräver installation av Docker)

Om du använder skriptet `docker_run.sh` i AEM som ett verktyg för Cloud Service Dispatcher kan du testa att din konfiguration inte innehåller några andra fel som bara skulle visas vid distribution:

### Steg 1: Generera distributionsinformation med valideraren

```
validator full -d out .
```

Detta validerar den fullständiga konfigurationen och genererar distributionsinformation i `out`

### Steg 2: Starta dispatchern i en buffertavbildning med den distributionsinformationen

När AEM-publiceringsservern körs på macOS-datorn och du lyssnar på port 4503 kan du köra dispatchern framför den servern enligt följande:

```
$ docker_run.sh out docker.for.mac.localhost:4503 8080
```

Detta startar behållaren och visar Apache på den lokala porten 8080.

### Använd din nya dispatcherkonfiguration

Grattis! Om valideraren inte längre rapporterar något problem och dockningsbehållaren startar utan fel eller varningar kan du flytta konfigurationen till en `dispatcher/src` underkatalog i Git-databasen.

**Kunder som använder AMS Dispatcher-konfiguration version 1 bör kontakta kundsupport för att hjälpa dem att migrera från version 1 till version 2 så att instruktionerna ovan kan följas.**

## Dispatcher och CDN {#dispatcher-cdn}

Leverans av publiceringstjänstinnehåll inkluderar:

* CDN (hanteras vanligtvis av Adobe)
* AEM Dispatcher
* AEM-publicering

Dataflödet är följande:

1. URL:en läggs till i webbläsaren
1. Begäran gjordes till CDN som mappats i DNS till den domänen
1. Om innehållet cachelagras fullständigt i CDN skickas det till webbläsaren av CDN
1. Om innehållet inte är fullständigt cachelagrat anropar CDN (omvänd proxy) till dispatchern
1. Om innehållet är fullständigt cachelagrat när avsändaren skickar det till CDN
1. Om innehållet inte är fullständigt cachelagrat anropar avsändaren (omvänd proxy) till AEM-publiceringen
1. Innehållet återges av webbläsaren, som också kan cachelagra det beroende på sidhuvudena

Det mesta innehållet upphör att gälla efter fem minuter, vilket är ett tröskelvärde som både dispatcherns cache och CDN respekterar. Under omdistributioner av publiceringstjänsten rensas dispatchercachen och varnas därefter innan den nya publiceringsnoden tar emot trafik.

Avsnitten nedan innehåller mer detaljerad information om innehållsleverans, inklusive CDN-konfiguration och cache-lagring av dispatcher.

Information om replikering från författartjänsten till publiceringstjänsten finns [här](/help/operations/replication.md).

>[!NOTE]
>Trafiken går igenom en webbserver med apache som har stöd för moduler som dispatchern. Avsändaren används främst som cache för att begränsa bearbetningen av publiceringsnoderna för att öka prestandan.

### CDN {#cdn}

AEM erbjuder tre alternativ:

1. Adobe Managed CDN - AEM&#39;s out-of-the-box CDN. Detta är det rekommenderade alternativet eftersom det är väl integrerat.
1. Kundhanterad CDN - Kunden har ett eget CDN och är helt ansvarig för att hantera det.
1. Peka på Adobe Managed CDN - kunden pekar på ett CDN till AEM&#39;s out-of-box CDN.

>[!CAUTION]
>Det första alternativet rekommenderas. Adobe kan inte hållas ansvarigt för resultatet av en felkonfiguration om du väljer det andra alternativet.

Det andra och tredje alternativet är tillåtet från fall till fall. Detta innebär att uppfylla vissa krav, inklusive, men inte begränsat till, kunden som har en äldre integrering med sin CDN-leverantör som är svår att ångra.

#### Adobe Managed CDN {#adobe-managed-cdn}

Det är enkelt att förbereda sig för innehållsleverans med hjälp av Adobes färdiga CDN enligt beskrivningen nedan:

1. Du skickar det signerade SSL-certifikatet och den hemliga nyckeln till Adobe genom att dela en länk till ett säkert formulär som innehåller den här informationen. Samordna med kundsupport för den här uppgiften.
Obs! Aem as a Cloud Service does not support Domain Validated (DV) certificates.
1. Kundsupport koordinerar sedan med dig tidpunkten för en CNAME DNS-post och pekar på deras FQDN till `adobe-aem.map.fastly.net`.
1. Du meddelas när SSL-certifikaten upphör att gälla så att du kan skicka om de nya SSL-certifikaten.

Som standard kan all offentlig trafik för en Adobe-hanterad CDN-installation gå vidare till publiceringstjänsten, både för produktionsmiljöer och icke-produktionsmiljöer (utvecklingsmiljöer och scenmiljöer). Om du vill begränsa trafiken till publiceringstjänsten för en viss miljö (t.ex. begränsa mellanlagring med ett intervall av IP-adresser) bör du tillsammans med kundsupporten arbeta med att konfigurera dessa begränsningar.

#### Kundhanterad CDN {#customer-managed-cdn}

Du får hantera ditt eget CDN, förutsatt att:

1. Du har ett befintligt CDN.
1. Det måste vara ett CDN som stöds. För närvarande stöds Akamai. Om din organisation vill hantera ett CDN som inte stöds kontaktar du kundsupporten.
1. Du kommer att klara det.
1. Du måste kunna konfigurera CDN så att det fungerar med AEM som en molntjänst - se konfigurationsinstruktionerna nedan.
1. Du har tekniska CDN-experter som är i kontakt om problem uppstår.
1. Du måste tillhandahålla vitlistor med CDN-noder till Cloud Manager, enligt konfigurationsinstruktionerna.
1. Du måste utföra och godkänna ett lasttest innan du går till produktion.

Konfigurationsinstruktioner:

1. Ge CDN-leverantören vitlista till Adobe genom att anropa miljöns create/update API med en lista över CIDR:er som vitlistas.
1. Ange domännamnet som `X-Forwarded-Host` huvud.
1. Ange värdhuvudet med ursprungsdomänen, som är AEM som en molntjänst som ingress. Värdet ska komma från Adobe.
1. Skicka SNI-huvudet till origo. Sni-huvudet måste vara den ursprungliga domänen.
1. Ange `X-Edge-Key` vilket som behövs för att dirigera trafik korrekt till AEM-servrarna. Värdet ska komma från Adobe.

Innan du godkänner direkttrafik bör du med Adobes kundsupport validera att hela trafikflödet fungerar korrekt.

#### Peka på Adobe Managed CDN {#point-to-point-CDN}

Stöds om du vill använda ditt befintliga CDN, men inte kan uppfylla kraven från ett kundhanterat CDN. I så fall hanterar du ditt eget CDN, men pekar på Adobes hanterade CDN.

Kunderna måste utföra och klara ett lasttest innan de kan börja producera.

Konfigurationsinstruktioner:

1. Ange domännamnet som `X-Forwarded-Host` huvud.
1. Ange värdhuvudet med ursprungsdomänen, som är Adobes CDN:s ingress. Värdet ska komma från Adobe.
1. Skicka SNI-huvudet till origo. Precis som med värdhuvudet måste sni-huvudet vara den ursprungliga domänen.
1. Ange `X-Edge-Key`, vilket krävs för att dirigera trafik korrekt till AEM-servrarna. Värdet ska komma från Adobe.

#### Cacheogiltigförklaring av CDN {#CDN-cache-invalidation}

Cacheogiltigförklaring följer dessa regler:

* Vanligtvis cachelagras HTML-innehåll i CDN i 5 minuter, baserat på det cache-kontrollhuvud som skickas av dispatchern.
* Klientbibliotek (JavaScript och CSS) cachelagras oavbrutet med cachekontrollen inställd på antingen oföränderlig eller 30 dagar för äldre webbläsare som inte respekterar det oföränderliga värdet. Observera att klientbiblioteken hanteras på en unik sökväg som ändras om klientbiblioteken ändras. Med andra ord kommer HTML som refererar till klientbiblioteken att produceras efter behov så att du kan uppleva nytt innehåll när det publiceras.
* Som standard cachelagras inte bilder.

Innan man kan ta emot direkttrafik bör man med Adobes kundsupport validera att hela trafikflödet fungerar som det ska.

## Cacheogiltigförklaring av explicit dispatcher {#explicit-invalidation}

Som tidigare nämnts går trafiken igenom en webbserver med huvudfunktioner, som har stöd för moduler som innehåller dispatchern. Avsändaren används främst som cache för att begränsa bearbetningen av publiceringsnoderna för att öka prestandan.

I allmänhet behöver du inte göra innehåll i dispatchern ogiltigt manuellt, men det är möjligt om det behövs, vilket beskrivs nedan.

Före AEM som molntjänst fanns det två sätt att ogiltigförklara dispatchercachen.

1. Anropa replikeringsagenten och ange agenten för rensning av publiceringsutgivaren
2. Anropa `invalidate.cache` API:t direkt (t.ex. POST /dispatcher/invalidate.cache)

Det finns inte längre stöd för `invalidate.cache` metoden eftersom den bara riktar sig till en viss dispatchernod.
AEM som en molntjänst arbetar på tjänstenivå, inte på den enskilda nodnivån, och därför är inte längre invalideringsinstruktionerna i [Dispatcher Help](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/dispatcher.html) -dokumentationen korrekta.
Istället bör agenten för tömning av replikering användas. Detta kan göras med replikerings-API:t. Dokumentationen för replikerings-API finns [här](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/replication/Replicator.html) . Ett exempel på hur du tömmer cachen finns på exempelsidan [för](https://helpx.adobe.com/experience-manager/using/aem64_replication_api.html) API. Exemplet `CustomStep` innehållerexempel på hur du skickar en replikeringsåtgärd av typen ACTIVATE till alla tillgängliga agenter. Slutpunkten för rensningsagenten är inte konfigurerbar, men förkonfigurerad att peka mot dispatchern, matchad med publiceringstjänsten som kör rensningsagenten. Flush-agenten kan oftast aktiveras av OSGi-händelser eller arbetsflöden.

<!--The diagram below illustrates this.

![CDN](assets/cdn.png "CDN")-->

Om det finns oro för att dispatchercachen inte rensas kontaktar du kundsupport som kan tömma dispatchercachen om det behövs.

CDN som hanteras av Adobe respekterar TTL:er och behöver därför inte tömmas. Om du misstänker ett problem kan du kontakta kundsupport som kan tömma ett Adobe-hanterat CDN-cache vid behov.

### Invalidering av Dispatcher-cache under aktivering/inaktivering {#cache-activation-deactivation}

Precis som i tidigare versioner av AEM rensas innehållet från dispatchercachen när du publicerar eller avpublicerar sidor. Om ett problem med cachning misstänks bör kunderna publicera om sidorna i fråga.

När publiceringsinstansen tar emot en ny version av en sida eller resurs från författaren, används justeringsagenten för att göra lämpliga sökvägar ogiltiga i dess dispatcher. Den uppdaterade sökvägen tas bort från dispatchercachen, tillsammans med dess överordnade, upp till en nivå (du kan konfigurera den med [statusfilnivån](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/configuring/dispatcher-configuration.html#invalidating-files-by-folder-level)).

### Enhetligt innehåll och enhetlig version {#content-consistency}

* Sidorna består av HTML, Javascript, CSS och bilder.
* Du bör använda clientlibs-ramverket för att importera JavaScript- och CSS-resurser till HTML-sidor, med hänsyn tagen till beroenden mellan JS-bibliotek.
* Automatisk versionshantering tillhandahålls, vilket innebär att utvecklare kan checka in ändringar i JS-bibliotek i källkontrollen och att den senaste versionen blir tillgänglig när en release publiceras. Utan detta skulle utvecklare behöva ändra HTML manuellt med referenser till den nya versionen av biblioteket, vilket är särskilt betungande om många HTML-mallar delar samma bibliotek.
* När de nya versionerna av biblioteken släpps i produktion uppdateras de refererande HTML-sidorna med nya länkar till de uppdaterade biblioteksversionerna. När webbläsarens cache har gått ut för en viss HTML-sida finns det ingen oro för att de gamla biblioteken kommer att läsas in från webbläsarens cache eftersom den uppdaterade sidan (från AEM) nu garanterat refererar till de nya versionerna av biblioteken. En uppdaterad HTML-sida kommer med andra ord att innehålla alla de senaste biblioteksversionerna.
