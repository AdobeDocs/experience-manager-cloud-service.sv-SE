---
title: Dispatcher i molnet
description: 'Dispatcher i molnet '
translation-type: tm+mt
source-git-commit: fe4202cafcab99d22e05728f58974e1a770a99ed
workflow-type: tm+mt
source-wordcount: '3824'
ht-degree: 9%

---


# Dispatcher i molnet {#Dispatcher-in-the-cloud}

## Apache and Dispatcher configuration and testing {#apache-and-dispatcher-configuration-and-testing}

I det här avsnittet beskrivs hur du strukturerar AEM som en Cloud Service-Apache och Dispatcher-konfigurationer samt hur du validerar och kör den lokalt innan du distribuerar den i molnmiljöer. Det beskriver även felsökning i molnmiljöer. Mer information om Dispatcher finns i [AEM Dispatcher-dokumentationen](https://docs.adobe.com/content/help/en/experience-manager-dispatcher/using/dispatcher.html).

>[!NOTE]
>
>Windows-användare måste använda Windows 10 Professional eller andra distributioner som stöder Docker. Detta är en förutsättning för att du ska kunna köra och felsöka Dispatcher på en lokal dator. Avsnitten nedan innehåller kommandon som använder Mac- eller Linux-versionerna av SDK, men Windows SDK kan användas på liknande sätt.

>[!WARNING]
>
>Windowsanvändare: den aktuella versionen av AEM som en Cloud Service lokal Dispatcher Tools (v2.0.20) är inte kompatibel med Windows. Kontakta [Adobe Support](https://daycare.day.com/home.html) för att få uppdateringar om Windows-kompatibilitet.

## Dispatcher Tools {#dispatcher-sdk}

Dispatcher-verktygen utgör en del av den övergripande AEM som en Cloud Service-SDK och tillhandahåller:

* En vaniljfilstruktur som innehåller de konfigurationsfiler som ska ingå i ett maven-projekt för dispatcher.
* Verktyg för att kunderna ska kunna validera en dispatcherkonfiguration lokalt.
* En Docker-bild som tar upp dispatchern lokalt.

## Hämta och extrahera verktygen {#extracting-the-sdk}

Dispatcher Tools kan laddas ned från en zip-fil på [Software Distribution](https://downloads.experiencecloud.adobe.com/content/software-distribution/en/aemcloud.html) portal. Observera att åtkomsten till SDK-listorna är begränsad till dem som har AEM Managed Services eller AEM som en Cloud Service-miljö. Alla nya konfigurationer som är tillgängliga i den nya versionen av dispatcher Tools kan användas för att distribuera till molnmiljöer där den versionen av AEM körs i molnet eller senare.

**För macOS och Linux** hämtar du gränssnittsskriptet till en mapp på datorn, gör det körbart och kör det. Det extraherar Dispatcher Tools-filerna under den katalog som du lagrade dem i (där `version` är versionen av dispatcher Tools).

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
>
>AEM som en Cloud Service maven-arkityp genererar samma konfigurationsfilstruktur för dispatcher.

Avsnitten nedan beskriver hur konfigurationen valideras lokalt så att den kan skicka den associerade kvalitetsgaten i Cloud Manager när en intern release distribueras.

## Lokal validering av Dispatcher-konfiguration {#local-validation-of-dispatcher-configuration}

Valideringsverktyget finns i SDK på `bin/validator` en binär Mac OS-, Linux- eller Windows-fil, vilket gör att kunderna kan köra samma validering som Cloud Manager gör när en release skapas och distribueras.

Den anropas som: `validator full [-d folder] [-w whitelist] zip-file | src folder`

Verktyget validerar Apache- och Dispatcher-konfigurationen. Den söker igenom alla filer med mönster `conf.d/enabled_vhosts/*.vhost` och kontrollerar att endast tillåtelselistad direktiv används. De direktiv som är tillåtna i Apache-konfigurationsfiler kan listas genom att köra validerarens tillåtelselista-kommando:

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

Kunder kan inte lägga till godtyckliga moduler, men ytterligare moduler kan övervägas för att ingå i produkten i framtiden. Kunderna hittar listan över direktiv som är tillgängliga för en viss Dispatcher-version genom att köra validerarens tillåtelselista-kommando i SDK enligt beskrivningen ovan.

tillåtelselista innehåller en lista över Apache-direktiv som tillåts i en kundkonfiguration. Om ett direktiv inte är tillåtelselistad loggas ett fel och en avslutningskod som inte är noll returneras. Om ingen tillåtelselista anges på kommandoraden (vilket är det sätt som det ska anropas) använder verktyget en tillåtelselista som Cloud Manager använder som standard för validering innan det distribueras till molnmiljöer.

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

Observera att valideringsverktyget endast rapporterar förbjuden användning av Apache-direktiv som inte har tillåtelselistad. Den rapporterar inte syntaktiska eller semantiska problem med din Apache-konfiguration eftersom den här informationen endast är tillgänglig för Apache-moduler i en körningsmiljö.

När inga valideringsfel rapporteras är konfigurationen klar för distribution.

Nedan visas felsökningstekniker för felsökning av vanliga valideringsfel som genereras av verktyget:

**det går inte att hitta en undermapp`conf.dispatcher.d`i arkivet**

Arkivet bör innehålla mapparna `conf.d` och `conf.dispatcher.d`. Observera att du **inte** bör
använda prefixet `etc/httpd` i arkivet.

**det gick inte att hitta någon servergrupp i`conf.dispatcher.d/enabled_farms`**

De aktiverade grupperna ska finnas i den undermappen.

**filen som ingår (..) måste ha följande namn: ...**

Det finns två avsnitt i servergruppskonfigurationen som **måste** innehålla en specifik fil: `/renders` och `/allowedClients` i `/cache` avsnittet. De här avsnitten måste se ut så här:

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

Det finns fyra avsnitt i servergruppskonfigurationen där du kan inkludera din egen fil: `/clientheaders`, `filters`, `/rules` i `/cache` avsnitt och `/virtualhosts`. De inkluderade filerna måste ha följande namn:

| Avsnitt | Inkludera filnamn |
|------------------|--------------------------------------|
| `/clientheaders` | `../clientheaders/clientheaders.any` |
| `/filters` | `../filters/filters.any` |
| `/rules` | `../cache/rules.any` |
| `/virtualhosts` | `../virtualhosts/virtualhosts.any` |

Du kan också inkludera **standardversionen** av de filerna, vars namn börjar med ordet `default_`, t.ex. `../filters/default_filters.any`.

**include-sats på (..), utanför känd plats: ...**

Förutom de sex avsnitt som nämns i styckena ovan, får du inte använda programsatsen `$include` . Följande skulle t.ex. generera detta fel:

```
/invalidate {
    $include "../cache/invalidate.any"
}
```

**Tillåtna klienter/renderare inkluderas inte från: ...**

Det här felet genereras när du inte anger någon inkludering för `/renders` och `/allowedClients` i `/cache` avsnittet. Se den **fil som ingår (..) måste ha följande namn: ...** för mer information.

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

Du kan också testa din Apache- och Dispatcher-konfiguration lokalt. Docker måste vara installerat lokalt och konfigurationen måste godkännas för den validering som beskrivs ovan.

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

Detta startar dispatchern i en behållare med dess serverdel pekande på en AEM som körs på din lokala Mac OS-dator vid port 4503.

## Felsöka Apache- och Dispatcher-konfigurationen {#debugging-apache-and-dispatcher-configuration}

Loggnivåer definieras av variablerna `DISP_LOG_LEVEL` och `REWRITE_LOG_LEVEL` i `conf.d/variables/global.var`s&quot;. Mer information finns i [loggningsdokumentationen](/help/implementing/developing/introduction/logging.md#apache-web-server-and-dispatcher-logging) .

## Olika Dispatcher-konfigurationer per miljö {#different-dispatcher-configurations-per-environment}

Nu används samma dispatcherkonfiguration för alla AEM som en Cloud Service-miljö. Körningsmiljön kommer att ha en miljövariabel `ENVIRONMENT_TYPE` som innehåller det aktuella körningsläget (dev, stage eller prod) samt en definition. Definitionen kan vara `ENVIRONMENT_DEV`, `ENVIRONMENT_STAGE` eller `ENVIRONMENT_PROD`. I Apache-konfigurationen kan variabeln användas direkt i ett uttryck. Definitionen kan också användas för att skapa logik:

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

I Dispatcher-konfigurationen är samma systemvariabel tillgänglig. Om mer logik krävs definierar du variablerna enligt exemplet ovan och använder dem sedan i konfigurationsavsnittet för Dispatcher:

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

## Visa den Dispatcher-konfiguration som används av Docker-behållaren {#viewing-dispatcher-configuration-in-use-by-docker-container}

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

## De viktigaste skillnaderna mellan AMS Dispatcher och AEM som Cloud Service {#main-differences-between-ams-dispatcher-configuration-and-aem-as-a-cloud-service}

Som beskrivs på referenssidan ovan liknar Apache- och Dispatcher-konfigurationen i AEM som en Cloud Service AMS-konfigurationen. De viktigaste skillnaderna är:

* I AEM som Cloud Service kan vissa Apache-direktiv inte användas (till exempel `Listen` eller `LogLevel`)
* I AEM som Cloud Service kan endast vissa delar av Dispatcher-konfigurationen placeras i inkluderingsfiler och deras namn är viktigt. Filterregler som du vill återanvända på olika värdar måste till exempel läggas i en fil som kallas `filters/filters.any`. Mer information finns på referenssidan.
* I AEM som Cloud Service finns det extra validering för att förhindra att filterregler skrivs med `/glob` för att förhindra säkerhetsproblem. Eftersom `deny *` används i stället för `allow *` (vilket inte kan användas) har man nytta av att köra Dispatcher lokalt och göra en testversion och felsökning. Loggarna visar exakt vilka vägar Dispatcher-filtren blockerar för att dessa ska kunna läggas till.

## Riktlinjer för att migrera dispatcher-konfiguration från AMS till AEM som Cloud Service

Dispatcher-konfigurationsstrukturen har olika Managed Services och AEM som en Cloud Service. Nedan visas en steg-för-steg-guide om hur du migrerar från AMS Dispatcher version 2 till AEM som Cloud Service.

## Konvertera en AMS till en AEM som en konfiguration för Cloud-tjänstdispatcher

I följande avsnitt ges stegvisa instruktioner för hur du konverterar en AMS-konfiguration. It assumes
that you have an archive with a structure similar to the one described in [Cloud Manager dispatcher configuration](https://docs.adobe.com/content/help/en/experience-manager-cloud-manager/using/getting-started/dispatcher-configurations.html)

### Extrahera arkivet och ta bort ett eventuellt prefix

Extrahera arkivet till en mapp och kontrollera att de omedelbara undermapparna börjar med `conf`, `conf.d``conf.dispatcher.d` och `conf.modules.d`. Om de inte gör det flyttar du dem uppåt i hierarkin.

### Ta bort oanvända undermappar och filer

Remove subfolders `conf` and `conf.modules.d`, as well as files matching `conf.d/*.conf`.

### Ta bort alla virtuella värdar som inte är publicerade 

Ta bort alla virtuella värdfiler i `conf.d/enabled_vhosts` som har `author`, `unhealthy`, `health`eller`lc` `flush` i sitt namn. All virtual host files in `conf.d/available_vhosts` that are not
linked to can be removed as well.

### Ta bort eller kommentera virtuell värd-sektioner som inte refererar till port 80

Om du fortfarande har avsnitt i dina virtuell värd-filer som endast refererar till andra portar än port 80, t.ex.

```
<VirtualHost *:443>
...
</VirtualHost>
```

ska du ta bort eller kommentera dem. Programsatser i de här avsnitten bearbetas inte, men om du behåller dem kan du ändå redigera dem utan någon effekt, vilket är förvirrande.

### Kontrollera återskrivningar

Ange katalog `conf.d/rewrites`.

Remove any file named `base_rewrite.rules` and `xforwarded_forcessl_rewrite.rules` and remember to
remove `Include` statements in the virtual host files referring to them.

If `conf.d/rewrites` now contains a single file, it should be renamed to `rewrite.rules` and don&#39;t
forget to adapt the `Include` statements referring to that file in the virtual host files as well.

If the folder however contains multiple, virtual host specific files, their contents should be
copied to the `Include` statement referring to them in the virtual host files.

### Kontrollera variabler

Ange katalog `conf.d/variables`.

Remove any file named `ams_default.vars` and remember to remove `Include` statements in the virtual
host files referring to them.

If `conf.d/variables` now contains a single file, it should be renamed to `custom.vars` and don&#39;t
forget to adapt the `Include` statements referring to that file in the virtual host files as well.

If the folder however contains multiple, virtual host specific files, their contents should be
copied to the `Include` statement referring to them in the virtual host files.

### Ta bort tillåtelselista

Remove the folder `conf.d/whitelists` and remove `Include` statements in the virtual host files referring to
some file in that subfolder.

### Ersätt alla variabler som inte längre är tillgängliga

I alla virtuell värd-filer:

Byt namn `PUBLISH_DOCROOT` till `DOCROOT`Ta bort avsnitt som refererar till variabler med namnet `DISP_ID`, `PUBLISH_FORCE_SSL` eller `PUBLISH_WHITELIST_ENABLED`

### Kontrollera status genom att köra valideraren

Run the dispatcher validator in your directory, with the `httpd` subcommand:

```
$ validator httpd .
```

Om felmeddelanden om saknade inkluderingsfiler visas, ska du kontrollera om du har bytt namn på filerna korrekt.

Om Apache-direktiv som inte är tillåtelselistad visas tar du bort dem.

### Ta bort alla icke-publicerade servergrupper

Remove any farm file in `conf.dispatcher.d/enabled_farms` that has `author`, `unhealthy`, `health`,
`lc` or `flush` in its name. All farm files in `conf.dispatcher.d/available_farms` that are not
linked to can be removed as well.

### Byta namn på servergruppsfiler

All farms in `conf.d/enabled_farms` must be renamed to match the pattern `*.farm`, so e.g. a
farm file called `customerX_farm.any` should be renamed `customerX.farm`.

### Kontrollera cache

Ange katalog `conf.dispatcher.d/cache`.

Ta bort alla filer som har prefixet `ams_`.

If `conf.dispatcher.d/cache` is now empty, copy the file `conf.dispatcher.d/cache/rules.any`
from the standard dispatcher configuration to this folder. The standard dispatcher
configuration can be found in the folder `src` of this SDK. Don&#39;t forget to adapt the
`$include` statements referring to the `ams_*_cache.any` rule files  in the farm files
as well.

If instead `conf.dispatcher.d/cache` now contains a single file with suffix `_cache.any`,
it should be renamed to `rules.any` and don&#39;t forget to adapt the `$include` statements
referring to that file in the farm files as well.

If the folder however contains multiple, farm specific files with that pattern, their contents
should be copied to the `$include` statement referring to them in the farm files.

Remove any file that has the suffix `_invalidate_allowed.any`.

Kopiera filen `conf.dispatcher.d/cache/default_invalidate_any` från defaultAEM i Cloud Dispatcher-konfigurationen till den platsen.

In each farm file, remove any contents in the `cache/allowedClients` section and replace it
with:

```
$include "../cache/default_invalidate.any"
```

### Kontrollera klientrubriker

Ange katalog `conf.dispatcher.d/clientheaders`.

Ta bort alla filer som har prefixet `ams_`.

If `conf.dispatcher.d/clientheaders` now contains a single file with suffix `_clientheaders.any`,
it should be renamed to `clientheaders.any` and don&#39;t forget to adapt the `$include` statements
referring to that file in the farm files as well.

If the folder however contains multiple, farm specific files with that pattern, their contents
should be copied to the `$include` statement referring to them in the farm files.

Kopiera filen `conf.dispatcher/clientheaders/default_clientheaders.any` från defaultAEM som en Cloud Service dispatcher-konfiguration till den platsen.

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

Ta bort alla filer som har prefixet `ams_`.

If `conf.dispatcher.d/filters` now contains a single file it should be renamed to
`filters.any` and don&#39;t forget to adapt the `$include` statements referring to that
file in the farm files as well.

If the folder however contains multiple, farm specific files with that pattern, their contents
should be copied to the `$include` statement referring to them in the farm files.

Kopiera filen `conf.dispatcher/filters/default_filters.any` från defaultAEM som en Cloud Service dispatcher-konfiguration till den platsen.

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

Kopiera filen `conf.dispatcher.d/renders/default_renders.any` från defaultAEM som en Cloud Service dispatcher-konfiguration till den platsen.

In each farm file, remove any contents in the `renders` section and replace it
with:

```
$include "../renders/default_renders.any"
```

### Kontrollera virtuella värdar

Rename the directory `conf.dispatcher.d/vhosts` to `conf.dispatcher.d/virtualhosts` and enter it.

Ta bort alla filer som har prefixet `ams_`.

If `conf.dispatcher.d/virtualhosts` now contains a single file it should be renamed to
`virtualhosts.any` and don&#39;t forget to adapt the `$include` statements referring to that
file in the farm files as well.

If the folder however contains multiple, farm specific files with that pattern, their contents
should be copied to the `$include` statement referring to them in the farm files.

Kopiera filen `conf.dispatcher/virtualhosts/default_virtualhosts.any` från defaultAEM som en Cloud Service dispatcher-konfiguration till den platsen.

Ersätt alla filter med programsatser som ser ut så här i varje servergruppsfil: 

```
$include "/etc/httpd/conf.dispatcher.d/vhosts/ams_publish_vhosts.any"
```

med programsatsen:

```
$include "../virtualhosts/default_virtualhosts.any"
```

### Kontrollera status genom att köra valideraren

Kör AEM som en Cloud Service dispatcher-validerare i din katalog med `dispatcher` underkommandot:

```
$ validator dispatcher .
```

Om felmeddelanden om saknade inkluderingsfiler visas, ska du kontrollera om du har bytt namn på filerna korrekt.

Om felmeddelanden som rör en odefinierad variabel `PUBLISH_DOCROOT` visas, ändrar du namnet till `DOCROOT`.

Alla andra fel finns i felsökningsavsnittet i dokumentationen för valideringsverktyget. 

### Testa konfigurationen med en lokal distribution (kräver installation av Docker)

Using the script `docker_run.sh` in the AEM as a Cloud Service Dispatcher Tools, you can test that
your configuration does not contain any other error that would only show up in
deployment:

### Steg 1: Generera distributionsinformation med valideraren

```
validator full -d out .
```

This validates the full configuration and generates deployment information in `out`

### Steg 2: Starta dispatchern i en buffertavbildning med den distributionsinformationen

När AEM-publiceringsservern körs på din macOS-dator och lyssnar på port 4503 kan du köra dispatchern framför den servern enligt följande:

```
$ docker_run.sh out docker.for.mac.localhost:4503 8080
```

Detta startar behållaren och visar Apache på den lokala porten 8080.

### Använd din nya dispatcherkonfiguration

Grattis! If the validator no longer reports any issue and the
docker container starts up without any failures or warnings, you&#39;re
ready to move your configuration to a `dispatcher/src` subdirectory
of your git repository.

**Kunder som använder AMS Dispatcher version 1 bör kontakta kundsupport för att hjälpa dem att migrera från version 1 till version 2 så att instruktionerna ovan kan följas.**
