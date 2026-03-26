---
title: Local Development with AI Tools
description: Lär dig hur du konfigurerar AI-kodningsverktyg med projektsammanhang, agentfärdigheter och MCP-servrar för att snabba upp AEM as a Cloud Service-utvecklingen.
feature: Developing
role: Developer
source-git-commit: 0bc00b6e14be6ba111ac26ce69f07e138ca400e4
workflow-type: tm+mt
source-wordcount: '1428'
ht-degree: 0%

---


# Local Development with AI Tools {#local-development-with-ai-tools}

>[!IMPORTANT]
>
>De funktioner som beskrivs i den här artikeln är **beta**. Genom att få tidig åtkomst till funktioner som Adobe utvecklar kan kunder och partners ge feedback (genom att skicka ett e-postmeddelande till [aemcs-ai-ide-tools-feedback@adobe.com](mailto:aemcs-ai-ide-tools-feedback@adobe.com)) och utforma produktutvecklingen. Det hjälper dem också att förbereda sig för att införa nya funktioner före allmän tillgänglighet.
>
>Beta-releaser kan innehålla defekter och tillhandahålls i befintligt skick utan någon garanti av något slag. Adobe har ingen skyldighet att upprätthålla, korrigera, uppdatera, ändra, modifiera eller på annat sätt ge support (via Adobe Support Services eller på annat sätt) för betaversioner. Adobe rekommenderar sina kunder att iaktta försiktighet och inte förlita sig på att betaversioner fungerar eller fungerar som de ska, eller på medföljande dokumentation eller material. Funktioner och API:er i betaversionen kan ändras utan föregående meddelande. Därför är all användning av betaversioner helt och hållet på kundens egen risk.

>[!NOTE]
>
>Den här artikeln fokuserar på lokal utveckling med AI-verktyg för **AEM Java-stapelutveckling**. För Edge Delivery Services, se [Utveckla med AI-verktyg](https://www.aem.live/developer/ai-coding-agents).

AI-kodningsagenter (Claude Code, Cursor, GitHub Copilot och liknande verktyg) har goda kunskaper om AEM underliggande tekniker (Java, OSGi, Sling, JCR, HTL), men vet inte nödvändigtvis bästa sättet att generera kod och konfiguration, eller hur man felsöker vanliga AEM-utvecklingsproblem.

Fyra kompletterande komponenter åtgärdar detta:

| Komponent | Syfte |
|---|---|
| **AGENTS.md** | En projektspecifik kontextfil som anropar AI i ditt AEM Cloud-serviceprojekt för varje session |
| **Agentkunskaper** | Återanvändbara instruktionsuppsättningar för återkommande utvecklingsuppgifter som att skapa komponenter och konfigurera Dispatcher |
| **AEM Quickstart lokal MCP-server** | Exponerar data från en lokal AEM SDK-instans för felsökning |
| **Dispatcher lokal MCP-server** | Aktiverar körtidsvalidering och kontroll av en lokal Dispatcher-instans |

>[!NOTE]
>
> Det är också användbart för lokal utveckling, men inte i den här artikeln, som är AEM Cloud-tjänstens fjärr-MCP-servrar. Läs mer om dem i [Använda MCP med Cloud Service-artikeln](/help/ai-in-aem/mcp-support/using-mcp-with-aem-as-a-cloud-service.md).

## AGENTS.md {#agentsmd}

`AGENTS.md` är en Markdown-fil i roten av ditt AEM-projekt som AI-kodningsverktygen automatiskt läses in i början av varje session för att få bas med grundläggande AEM Cloud Service Java-stack-domänexpertis (och inte andra AEM-lösningar som AEM 6.5 eller Edge Delivery Services).

`AGENTS.md` är inte en statisk fil som du kopierar. Den genereras av kompetensen `ensure-agents-md` som beskrivs i nästa avsnitt. Kunskapen läser din `pom.xml` för att lösa projektnamnet, identifiera moduler och identifiera installerade tillägg, vilket skapar en fil som är anpassad till ditt specifika projekt.

>[!NOTE]
>
>När `AGENTS.md` finns i projektroten körs inte längre `ensure-agents-md`-kompetensen. Redigera filen direkt om projektstrukturen ändras.

## Agentfärdigheter {#agent-skills}

Kompetens är instruktionsuppsättningar som kodar arbetsflöden för utveckling i flera steg. När den anropas följer den artificiella intelligensen färdighetens procedur i stället för att förlita sig enbart på allmän kunskap, vilket ger konsekventa, konventionella resultat.

Adobe publicerar AEM as a Cloud Service-kunskaper i databasen **[adobe/skills](https://github.com/adobe/skills/tree/beta/skills/aem/cloud-service/skills)** på grenen `beta` eftersom den här funktionen ännu inte är allmänt tillgänglig:

| Kompetens | Syfte |
|---|---|
| `ensure-agents-md` | Bootstrap `AGENTS.md` och `CLAUDE.md` som är anpassade till projektets faktiska modulstruktur |
| `create-component` | Skafflar en komplett AEM-komponent: komponentdefinition, dialog-XML, HTML-mall, Sling Model, enhetstester och clientlibs |
| `dispatcher` | Konfigurationsassistenten Dispatcher och Apache HTTPD med AI-stöd, som omfattar konfigureringsredigering, teknisk rådgivning, incidentsvar, prestandajustering och säkerhetshärdning |
| `workflow` | En enda startpunkt för alla AEM as a Cloud Service Workflow-kunskaper. Omfattar design av arbetsflödesmodeller, anpassade processsteg och utveckling av deltagarväljare, startkonfiguration, arbetsflödesaktivering och produktionsstöd, inklusive felsökning av fastnade/misslyckade arbetsflöden, triaging av incidenter med Cloud Manager-loggar, analys av trådpooler och Sling Job Diagnotics för Granite Workflow Engine. |

### Installera färdigheter {#install-skills}

Välj den metod som matchar ditt AI-kodningsverktyg. Genom att installera kunskaper en gång blir de tillgängliga för alla projekt på den datorn.

#### Claude Code {#claude-code}

```bash
# Add the Adobe Skills marketplace (one-time setup)
/plugin marketplace add adobe/skills#beta

# Install all available skills
/plugin install aem-cloud-service@adobe-skills
```

#### Npx Skills {#npx-skills}

```bash
# Install all available skills
npx skills add https://github.com/adobe/skills/tree/beta/skills/aem/cloud-service --all
```

#### Uppgradering (GitHub CLI-tillägg) {#upskill-github-cli-extension}

```bash
# Install the gh-upskill extension (one-time setup)
gh extension install trieloff/gh-upskill

# Install all available skills
gh upskill adobe/skills --branch beta --path skills/aem/cloud-service --all
```

### Använda kompetens för säkra agenter-md {#use-the-ensure-agents-md-skill}

När du har installerat kompetensen öppnar du AI-assistenten i ett AEM Cloud-serviceprojekt som ännu inte har ett `AGENTS.md`. Kunskapen körs automatiskt innan din första begäran bearbetas och båda filerna skapas i projektets rot utan att explicit anrop krävs.

### Använda Kompetens för att skapa komponenter {#use-the-create-component-skill}

När kompetensen används första gången identifieras `project`, `package` och `group` från `pom.xml` och befintliga komponenter automatiskt. Du ombeds bekräfta de identifierade värdena och sedan skapas `.aem-skills-config.yaml` i projektets rot. Ingen manuell konfiguration krävs före första användningen.

Om du föredrar att skapa filen i förväg placerar du `.aem-skills-config.yaml` i projektroten med följande struktur:

```yaml
configured: true

project: "wknd"                                    # Check /apps/{project}/ or pom.xml
package: "com.adobe.aem.guides.wknd.core"          # Check core/pom.xml
group: "WKND Components"                           # Check existing component .content.xml files
```

Filen finns utanför kompetenskatalogen och skrivs aldrig över när kompetensen uppdateras.

Beskriv komponenten i din AI-chatt:

```
Create an AEM component called "Hero Banner"

Dialog specification:
Title (title) - Textfield, mandatory
Subtitle (subtitle) - Textfield
Background Image (backgroundImage) - Fileupload
CTA Text (ctaText) - Textfield
CTA Link (ctaLink) - Pathfield
```

Agenten kopierar fältspecifikationen för bekräftelse och genererar sedan alla komponentfiler. Mönster som stöds är multifält med sammansatta kapslade objekt, villkorsstyrd logik för att visa/dölja, Core Component-tillägg via Sling Resource Merger och JUnit 5-tester med AEM Mocks.

### Använda Dispatcher-kompetens {#use-the-dispatcher-skill}

Anropa skickligheten för alla Dispatcher- och Apache HTTPD-konfigurationer. Färdighetsvägarna begär en av sex specialistunderkunskaper beroende på vilken typ av begäran det gäller:

| Underkompetens | Syfte |
|---|---|
| `workflow-orchestrator` | Totallösning för design, konfigurationsändringar, validering och uppföljning |
| `config-authoring` | Konkreta konfigurationsändringar: filter, cacheregler, omskrivningar, värdar, rubriker och serveringar |
| `technical-advisory` | Konceptuell vägledning, policyförklaring och rekommendationer som bygger på citat |
| `incident-response` | Körningsfel, cacheavvikelser och regressioner |
| `performance-tuning` | Cache-effektivitet, fördröjning och genomströmningsoptimering |
| `security-hardening` | Granskning och skärpning av exponering |

För breda eller förstagångsbegäranden börjar du med underkompetensen `workflow-orchestrator`. Beskriv det särskilda problemet och färdighetsvägarna till lämplig specialist när det gäller riktat arbete.

Avsändarens skicklighet hanterar orkestrering och rådgivande vägledning. Dispatcher MCP-servern, som beskrivs nedan, tillhandahåller de sju validerings- och körningsverktygen som kompetensen använder när den behöver lokala bevis.

## AEM Quickstart MCP Server {#aem-quickstart-mcp-server}

MCP (Model Context Protocol) är en öppen standard som tillåter AI-kodningsverktyg att ansluta till externa datakällor och tjänster. AEM Quickstart MCP-servern är ett innehållspaket som, när det har installerats i en lokal instans av AEM SDK, exponerar körningsdata direkt för anslutna AI-verktyg, vilket gör det möjligt för agenter att hämta loggar, diagnostisera OSGi-fel och inspektera förfrågningsbearbetning utan att lämna utvecklingsmiljön.

### Installera innehållspaketet {#install-the-content-package}

Hämta innehållspaketet från [Software Distribution Portal](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?1_group.propertyvalues.property=.%2Fjcr%3Acontent%2Fmetadata%2FDc%3AsoftwareType&1_group.propertyvalues.operation=equals&1_group.propertyvalues.0_values=software-type%3Abeta) och installera `com.adobe.aem:com.adobe.aem.mcp-server-contribs-content` i din lokala QuickStart med hjälp av Package Manager på `/crx/packmgr`.

**Kompatibilitet:** Verifierad med AEM SDK `2026.2.24678.20260226T154829Z-260200` och senare.

### Tillgängliga verktyg {#available-tools}

| Verktyg | Beskrivning |
|---|---|
| `aem-logs` | Hämtar loggposter för AEM och OSGi, filtrerbara efter regex-mönster, loggnivå och antal poster |
| `diagnose-osgi-bundle` | Diagnostiserar varför ett paket eller en DS-komponent inte startar; rapporterar saknade paket, ej nöjda referenser och konfigurationsproblem |
| `recent-requests` | Returnerar senaste HTTP-begäranden med Sling:s fullständiga interna bearbetningsspårning (resursupplösning, skriptupplösning, filterkedja), filtrerbar med sökvägsregex |

### Konfigurera din IDE {#configure-your-ide}

#### Markör {#cursor}

Lägg till en ny anpassad MCP-server i Markörinställningarna:

```json
"aem-cs-sdk": {
  "type": "streamable-http",
  "url": "http://localhost:4502/bin/mcp",
  "headers": {
    "Authorization": "Basic YWRtaW46YWRtaW4="
  }
}
```

#### GitHub Copilot med IntelliJ IDEA {#github-copilot-with-ihtellij-idea}

Navigera till **Verktyg > GitHub-kompilering > MCP (Model Context Protocol)** och klicka på **Konfigurera**. Lägg till:

```json
"aem-cs-sdk": {
  "url": "http://localhost:4502/bin/mcp",
  "requestInit": {
    "headers": {
      "Authorization": "Basic YWRtaW46YWRtaW4="
    }
  }
}
```

#### Andra IDE {#other-ides}

Alla MCP-klienter kan ansluta genom att peka på `http://localhost:4502/bin/mcp` med ett `Authorization: Basic YWRtaW46YWRtaW4=`-huvud. Konfigurera anpassade rubriker med hjälp av de MCP-inställningar du har angett för IDE.

>[!NOTE]
>
>Värdet `Basic YWRtaW46YWRtaW4=` är Base64-kodningen `admin:admin`, som är standardautentiseringsuppgifter för en lokal QuickStart. Använd inte detta i icke-lokala miljöer.

## Dispatcher MCP Server {#dispatcher-mcp-server}

Dispatcher MCP-servern medföljer AEM Dispatcher SDK. Med AI-verktygen kan du validera konfigurationen av Dispatcher och Apache HTTPD, hantera spårningsbegäranden och inspektera cachebeteendet mot en Dispatcher-instans som körs lokalt i Docker.

Till skillnad från skickligheten visar Dispatcher MCP-servern endast verktyg: sju MCP-verktyg och inga uppmaningar eller resurser.

### Förutsättningar {#prerequisites}

- Docker Desktop 4.x eller senare, installerat och körs
- AEM Dispatcher SDK har hämtats från [portalen för programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?1_group.propertyvalues.property=.%2Fjcr%3Acontent%2Fmetadata%2FDc%3AsoftwareType&1_group.propertyvalues.operation=equals&1_group.propertyvalues.0_values=software-type%3Abeta)

>[!NOTE]
>
>Om du ser `client version 1.43 is too new` anger du `DOCKER_API_VERSION=1.41` i skalet eller i `mcp.json`.

### Installera Dispatcher SDK {#install-the-dispatcher-sdk}

**macOS och Linux:**

```bash
chmod +x aem-sdk-dispatcher-tools-<version>-unix.sh
./aem-sdk-dispatcher-tools-<version>-unix.sh
cd dispatcher-sdk-<version>
chmod +x ./bin/docker_run_mcp.sh
./bin/docker_run_mcp.sh test
```

**Windows:**

```powershell
Expand-Archive aem-sdk-dispatcher-tools-<version>-windows.zip
```

Kör `./bin/docker_run_mcp.sh help` för att hämta IDE-konfigurationen för kopiera och klistra in och `./bin/docker_run_mcp.sh version` för att bekräfta den paketerade MCP- och SDK-versionen. Använd `./bin/docker_run_mcp.sh diagnose` för att undersöka anslutningsproblem.

### Konfigurera markör {#configure-cursor}

Lägg till en `aem-dispatcher-mcp`-post i `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "aem-dispatcher-mcp": {
      "command": "<path_to_dispatcher_sdk>/bin/docker_run_mcp.sh",
      "env": {
        "DOCKER_API_VERSION": "1.43",
        "AEM_DEPLOYMENT_MODE": "cloud",
        "MCP_LOG_LEVEL": "trace",
        "MCP_LOG_FILE": "/tmp/dispatcher-mcp.log",
        "DISPATCHER_CONFIG_PATH": "<path_to_dispatcher_src>"
      }
    }
  }
}
```

Ersätt `<path_to_dispatcher_sdk>` med den extraherade Dispatcher SDK-platsen och `<path_to_dispatcher_src>` med projektets dispatcher `src`-katalog. Ange `DISPATCHER_CONFIG_PATH` till den config root som innehåller de filer där `/docroot` har definierats. `MCP_LOG_LEVEL` och `MCP_LOG_FILE` är valfria felsökningsinställningar. Om du ser `client version 1.43 is too new` anger du `DOCKER_API_VERSION` till `1.41`. Om andra MCP-servrar redan har konfigurerats lägger du till posten `aem-dispatcher-mcp` utan att ersätta dem. Starta om markören när du har sparat.

Andra utvecklingsmiljöer kan konfigureras på liknande sätt. SDK `docs/DispatcherMCP.md` innehåller fullständiga exempel för Claude Desktop och VS Code.

### Tillgängliga verktyg {#available-tools-dispatcher}

| Verktyg | Beskrivning |
|---|---|
| `validate` | Validerar Dispatcher- och Apache HTTPD-konfigurationer |
| `lint` | Kör lägesmedvetna statiska kontroller och metodanalys |
| `sdk` | Kör Dispatcher SDK-arbetsflöden: `validate`, `validate-full`, `three-phase-validate`, `docker-test`, `check-files`, `diff-baseline` |
| `trace_request` | Spåra begärandebeteende med körningsbevis |
| `inspect_cache` | Kontrollerar cache- och docroot-beteende för en mål-URL |
| `monitor_metrics` | Läser körningsmått från Dispatcher och HTTPD-loggar |
| `tail_logs` | Visar relevanta Dispatcher- och HTTPD-körningsloggar |

MCP-ytan visar avsiktligt endast dessa sju verktyg. Kortkommandon och resurser finns kvar i kunskapsskiktet. Fullständig referensdokumentation finns i `docs/DispatcherMCP.md` i den extraherade Dispatcher SDK.
