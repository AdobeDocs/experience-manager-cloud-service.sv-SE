---
title: Använda MCP med AEM as a Cloud Service
description: Lär dig hur du använder Model Context Protocol med AEM as a Cloud Service
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
exl-id: ddb7fc8c-affc-4374-8e08-d45d96017109
source-git-commit: 6fccf4f197fbfd38aa6a84422dc347b02d03061d
workflow-type: tm+mt
source-wordcount: '1786'
ht-degree: 0%

---

# Använda MCP med AEM as a Cloud Service {#using-mcp-with-aem-as-a-cloud-service}

## Introduktion {#introduction}

Många Adobe Experience Manager-team (AEM) arbetar nu i Integrated Development Environment (IDE) och chattbaserade program som Cursor, OpenAI ChatGPT, Anthropic Claude och Microsoft Copilot Studio. Dessa program stöder Model Context Protocol (MCP), som gör att program kan visa back-end-verktyg för stora språkmodeller (LLM) på ett standardiserat sätt.

Med AEM MCP-integrering kan olika personer samarbeta kring samma innehåll:

* **Utvecklare** kan ordna innehållsoperationer och arbetsflöden från sina IDE- eller chattprogram
* **Personer som arbetar med innehåll** och innehållsarkitekter kan hantera webbplatser, innehållsfragment och resurser med hjälp av AI, och kan samtidigt stanna kvar i AEM befintliga behörighetsmodell.

>[!IMPORTANT]
>
> För scenarier där innehåll ändras eller tas bort bör man använda AI Assistant-gränssnittet i stället för att anropa MCP-verktygen direkt. AEM Agents som drivs av AI Assistant innehåller inbyggda skyddsfunktioner.
>

I den här artikeln förklaras vad AEM MCP-funktioner innehåller, vilka MCP-program som stöds, hur de konfigureras och hur de används i praktiken.

## Därför är MCP användbart för AEM-kunder {#why-mcp-is-useful-for-aem-customers}

Modern IDE- och chattapplikationer använder MCP som ett sätt för en LLM att anropa verktyg som exponeras bakom MCP-servrar. Kunderna kan beskriva sina avsikter på ett naturligt språk i stället för att skriva kod mot API-specifikationer på låg nivå. En uppmaning som *&quot;uppdaterar hjältebannern för den här kampanjen på alla sidor&quot;* gör att LLM kan anropa rätt MCP-verktyg, som sedan interagerar med AEM API:er.

Några viktiga fördelar:

* **Interaktion på naturspråk i stället för API-rörning**
MCP-verktygen beskriver vilka åtgärder som är tillgängliga och hur de anropas. LLM använder dessa scheman för att bestämma vilka verktyg som ska anropas och med vilka parametrar.
* **Enhetlig upplevelse i alla program**
Samma AEM MCP-verktyg kan användas från flera MCP-kompatibla program, vilket gör att man kan arbeta där man är mest produktiv samtidigt som man anropar samma underliggande AEM-funktioner.
* **Säkerhet och styrning bevaras**
Begäranden till AEM MCP-verktyg körs under den autentiserade användarens identitet och varje verktyg tillämpar användarens befintliga AEM-behörigheter. AI-assisterad verksamhet följer samma åtkomstregler som för manuellt arbete i AEM.

## MCP-servrar från AEM {#mcp-servers-provided-by-aem}

AEM visar MCP-servrar som HTTP-slutpunkter. Slutpunkterna som anges nedan är relativa till:

`https://mcp.adobeaemcloud.com/adobe/mcp/`

### MCP-servrar {#mcp-servers}

| **MCP-server** | **Slutpunkt** | **Beskrivning** |
|---|---|----------------------------------------------------------------------------------------------------------------------|
| **Innehåll** | `/content` | Alla lågnivååtgärder för innehåll, inklusive skapa, läsa, uppdatera och ta bort (CRUD) för sidor, fragment och resurser. |
| **Innehåll (skrivskyddat)** | `/content-readonly` | Skrivskyddade innehållsåtgärder (Hämta, Lista/Sök) för sidor, fragment och resurser. |
| **Cloud Manager** | `/cloudmanager` | Hantera Cloud Manager-enheter som program, miljöer, databaser och rörledningar som också kan aktiveras. <br><br>*Den här MCP-servern är nu i **beta**. Om du vill begära åtkomst skickar du ett e-postmeddelande till [aemcs-mcp-feedback@adobe.com](mailto:aemcs-mcp-feedback@adobe.com) med en beskrivning av ditt användningsfall.* |

De specifika verktyg som visas av varje MCP-server kan utvecklas över tid. I praktiken kan du be ditt MCP-aktiverade program att hitta verktyg via en uppmaning som:

```
"List all AEM MCP tools available from this server and describe what they do."
```

MCP-klienten använder MCP-protokollet för att hämta verktygslistan och scheman som LLM sedan kan använda.

Se självstudiekursen [Content MCP Server &#x200B;](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/ai/mcp-servers/accelerate-content-operations-with-aem-mcp-server) och [Cloud Manager MCP Server Video](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/ai/mcp-servers/cloud-manager) för mer information om deras funktioner och hur de används.

## MCP-program som stöds {#supported-mcp-applications}

AEM MCP-servrar är utformade för att fungera med en definierad uppsättning MCP-kompatibla program. Varje program har en egen konfigurationsupplevelse, men stegen på hög nivå är liknande.

### Chattprogram (webb och dator) {#chat-applications}

* Anthropic Claude
* OpenAI ChatGPT

### Utvecklingsverktyg (IDE-tillägg, datorprogram, CLI) {#developer-tools}

* Anthropic Claude Code (CLI, JetBrains, VS Code, Cursor)
* Förenklingskod (CLI, JetBrains, VS-kod, markör)
* Öka indrag för skrivbordsapp
* Cline (JetBrains, VS Code, Cursor)
* Markör
* GitHub Copilot (VS-kod)
* Kiro (datorprogram, CLI)
* OpenAI Codex (datorprogram)
* OpenAI Codex CLI
* Windsurf

### Enterprise Platforms {#enterprise-platforms}

* Microsoft Copilot Studio

## Översikt över inställningar {#setup-overview}

Konfigurering av MCP för AEM inbegriper två huvuddelar:

1. **Konfiguration i varje MCP-klientprogram** så att programmet vet hur man ansluter till AEM MCP-servrar och utför OAuth-inloggning
1. **Markera MCP-servern** innan du börjar fråga, så att MCP-klienten vet att den ska använda den.

### AEM Configuration {#aem-configuration}

Som standard styr de behörigheter som enskilda användare har i AEM åtkomsten till AEM MCP-servrar. När en användare autentiserar via ett MCP-klientprogram tillämpar MCP-verktygen samma åtkomstregler som för manuella åtgärder i AEM. En användare kan bara utföra åtgärder som de redan har behörighet att utföra.

#### Tillåtna MCP-klientprogram {#permitted-mcp-client-applications}

Följande MCP-klientprogram tillåts som standard:

* Anthropic Claude
* Anthropic Claude Code
* Kod för ökning
* Öka indrag
* Cline
* Markör
* GitHub Copilot
* Kiro
* Microsoft Copilot Studio
* OpenAI ChatGPT
* OpenAI Codex
* OpenAI Codex CLI
* Windsurf

#### Begränsar MCP-servrar {#restricting-mcp-servers}

Alla MCP-servrar är tillåtslista som standard. Som administratör kan du begränsa åtkomsten till vissa MCP-servrar på organisations-, program- eller miljönivå. Begränsningen ger detaljerad kontroll över vilka MCP-funktioner som är tillgängliga för användare i organisationen.

#### Hantera MCP-klientåtkomst {#managing-mcp-client-access}

Administratörer kan även inaktivera åtkomst för specifika MCP-klientprogram om organisationens principer kräver det. Om du vill att Adobe ska aktivera stöd för ytterligare MCP-klientprodukter skickar du en länk till produktwebbplatsen. Om du behöver tillåtslista en anpassad MCP-klient, kontakta också.

Kontakta oss gärna på **aemcs-mcp-feedback@adobe.com** för alla MCP-serverrelaterade förfrågningar.

### Konfiguration av MCP-klientprogram {#mcp-client-application-configuration}

Varje användare utför det här steget, eller en administratör för MCP-klientprogrammet kan utföra det där det stöds. Konfigurationsinformationen varierar något mellan programmen. MCP-klienter utvecklas snabbt och stöd för MCP-fjärrservrar utvecklas aktivt. Du kan behöva aktivera utvecklarläget för att få åtkomst till funktionerna för att lägga till fjärrservrar, men den allmänna processen är:

1. Lägg till en eller flera URL-adresser för AEM MCP-servrar
   * Konfigurera en eller flera MCP-slutpunkter från tabellen ovan. Till exempel:`https://mcp.adobeaemcloud.com/adobe/mcp/content-readonly`
1. Utlös anslutningen
   * Spara eller aktivera konfigurationen så att MCP-klientprogrammet försöker ansluta till AEM MCP-servern
1. Logga in med Adobe ID
   * Fyll i inloggningsflödet för Adobe när du uppmanas att göra det så att programmet kan få OAuth-tokens kopplade till din Adobe ID
1. Verifiera identifierade verktyg
   * När programmet har autentiserats hittar det MCP-verktyg från servern. Du kan sedan börja fråga LLM om du vill utföra AEM-åtgärder.

Nedan finns de program som stöds, varav några är länkar till steg-för-steg-guider:

#### Chattprogram (webb och dator) {#setup-chat-applications}

* [Anthropic Claude](/help/ai-in-aem/mcp-support/setup-claude.md)
* [OpenAI ChatGPT](/help/ai-in-aem/mcp-support/setup-chatgpt.md)

#### Utvecklingsverktyg (IDE-tillägg, datorprogram, CLI) {#setup-developer-tools}

* Anthropic Claude Code (CLI, JetBrains, VS Code, Cursor)
* Förenklingskod (CLI, JetBrains, VS-kod, markör)
* Öka indrag för skrivbordsapp
* Cline (JetBrains, VS Code, Cursor)
* [Markör](/help/ai-in-aem/mcp-support/setup-cursor.md)
* GitHub Copilot (VS-kod)
* Kiro (datorprogram, CLI)
* OpenAI Codex (datorprogram)
* OpenAI Codex CLI
* Windsurf

#### Enterprise Platforms {#setup-enterprise-platforms}

* [Microsoft Copilot Studio](/help/ai-in-aem/mcp-support/setup-microsoft-copilot-studio.md)

## Autentisering {#authentication}

Adobe MCP-värdservrar implementerar OAuth och är integrerade med Adobe identitetssystem.

* När ett MCP-klientprogram ansluter till en AEM MCP-server visas en inloggningsdialogruta från Adobe och autentiseras med **Adobe ID**
* När inloggningen är klar verifierar systemet att MCP-klientprogrammet tillåts i organisationen och att den begärda MCP-servern tillåts. Om någon kontroll misslyckas visas ett felmeddelande.

![MCP-klienten tillåts inte, fel](assets/MCP-Client-not-permitted.png)

* Efter verifieringen utfärdar MCP-servern tokens som används för efterföljande verktygsanrop
* MCP-verktygen respekterar användarens AEM-behörigheter. Endast användare som har behörighet att ändra ett innehållsfragment i AEM kan ändra det via MCP.

Med den här metoden kan du vara säker på att AI-assisterad verksamhet följer AEM befintliga säkerhets- och styrningsmodell.

## Använda MCP med AEM {#using-mcp-with-aem}

När AEM och dina MCP-klientprogram har konfigurerats kan du arbeta i valfritt program och uppmana LLM att utföra AEM-åtgärder. LLM läser MCP-verktygsscheman, väljer vilka verktyg som ska anropas och sekvenserar dem efter behov för att uppfylla din begäran.

>[!IMPORTANT]
>
>Frågar som innehåller flera steg eller som har olika innehållstyper som mål, till exempel bilder och text, fungerar bäst med en tänkande modell. Aktivera en tänkande modell eller välj alternativet Thinking i MCP-klienten i stället för att förlita dig på Auto-läget.

### Exempel på användning {#example-usecases}

Några exempel på scenarier:

* **Miljöidentifiering**
   * Ange miljöer och licenser för att bestämma var ett arbetsflöde ska köras.

* **Platshantering**
   * Lista webbplatser
   * Skapa, läsa, uppdatera och ta bort sidor och sidinnehåll.

* **Hantering av innehållsfragment**
   * Sök efter innehållsfragment
   * Skapa nya fragment
   * Uppdatera befintliga fragment när kampanjmeddelanden ändras.

* **Assets-hantering**
   * Importera resurser
   * Hitta befintliga resurser
   * Publicera resurser.

### Exempel på arbetsflöden {#example-workflows}

Följande exempel visar hur ett LLM kan sammanföra MCP-verktygen.

1. **Arbeta med ett innehållsfragment som en sida refererar till**
   * **Hämta sidinnehåll** - Anropa ett verktyg som `get-aem-page-content` för att hämta sidan och leta upp egenskapen `fragmentPath`.
   * **Lös fragmentsökvägen** - Använd `resolve_fragment_path` för att konvertera sökvägen till ett UUID.
   * **Hämta fragmentdata** - Anropa `get_fragment` för att hämta aktuella fält.
   * **Uppdatera fragmentet** - Anropa `patch_fragment` för att tillämpa ändringar i fragmentinnehållet.
1. **Skapa nytt innehåll baserat på en modell**
   * **Identifiera modeller** - Använd `list_models` för att se vilka innehållsfragmentmodeller som är tillgängliga.
   * **Inspektera en modell** - Använd `get_model` för att förstå modellens fältschema.
   * **Skapa innehåll** - Använd `create_fragment` om du vill skapa ett nytt fragment med värden som härleds från uppmaningen.
1. **Uppdatera befintligt innehåll på ett säkert sätt**
   * **Läs aktuella data** - Använd `get_fragment` för att hämta befintliga data och en ETag.
   * **Använd en JSON-korrigering** - Använd `patch_fragment` med ETag och ett JSON-korrigeringsdokument för att uppdatera fragmentet, med stöd för optimistisk samtidighet.

Ur användarens perspektiv kan dessa arbetsflöden initieras med frågor som:

```
"Create a new content fragment for the spring campaign based on our hero banner model and fill in its fields from this brief."
```

LLM väljer och koordinerar automatiskt nödvändiga MCP-verktyg.

## Förväntningshantering {#expectation-management}

När du arbetar med livslångt lärande via MCP bör du tänka på följande:

* **Kan användas med hög kapacitet men är inte ofelbar**
Hanterare av livslångt lärande kan utföra komplexa uppgifter men kan få tillfälliga fel. Samma uppmaning kan ge något annorlunda resultat eller presentationer utan någon självklar anledning. Granska alltid utdata innan du tillämpar ändringar på produktionsinnehållet.

* **Utvecklande funktioner**
LLM-modellerna förbättras kontinuerligt. Med tiden blir de smartare när det gäller att hitta nya sätt att kombinera MCP-verktyg för att uppnå era mål. En uppgift som kräver flera uppmaningar idag kan fungera sömlöst med en enda prompt imorgon.

* **Personlig tillsyn är nödvändig:**
Tänk på LLM som en kunnig assistent som behöver tillsyn. Det har stor kunskap och kan ta fram kreativa lösningar, men det är till nytta för er vägledning och granskning. Verifiera resultaten, särskilt för kritiska operationer, och ge feedback när resultatet inte motsvarar dina förväntningar.

* **Var försiktig med automatisk bekräftelse av verktygskörningar**
Vissa MCP-klientapplikationer, som Claude, erbjuder möjligheten att automatiskt bekräfta verktygskörningar som efterfrågats av LLM. Det här alternativet kan vara praktiskt för skrivskyddade åtgärder som att söka efter eller hämta innehåll, men var försiktig med verktyg som uppdaterar eller tar bort innehåll. Granska varje begäran om verktygskörning innan du bekräftar åtgärder som ändrar din AEM-miljö.

## Begränsningar {#limitations}

AEM stöder för närvarande konfigurering av MCP-servrar i de program som listas under [MCP-program som stöds](#supported-mcp-applications).

Om du vill använda ett annat MCP-klientprogram kan du kontakta **aemcs-mcp-feedback@adobe.com** för att begära stöd för ytterligare klienter eller för att tillåtslista en anpassad klient.
