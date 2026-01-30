---
title: Använda MCP med AEM as a Cloud Service
description: Lär dig hur du använder Model Context Protocol med AEM as a Cloud Service
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: 3ff5ef0be78f5f5a61c81c8ab0388b56fa134047
workflow-type: tm+mt
source-wordcount: '2016'
ht-degree: 0%

---


# Använda MCP med AEM as a Cloud Service {#using-mcp-with-aem-as-a-cloud-service}

## Introduktion {#introduction}

Många AEM-team arbetar nu med IDE och chattbaserade program som Cursor, ChatGPT, Anthropic Claude och Microsoft Copilot Studio. Dessa program stöder Model Context Protocol (MCP), som gör att program kan visa back-end-verktyg för stora språkmodeller (LLM) på ett standardiserat sätt.

Med AEM MCP-integrering kan olika personer samarbeta kring samma innehåll:

* **Utvecklare** kan ordna innehållsoperationer och arbetsflöden från sina IDE- eller chattprogram
* **Personer som arbetar med innehåll** och innehållsarkitekter kan hantera webbplatser, innehållsfragment och resurser med hjälp av AI, och kan samtidigt stanna kvar i AEM befintliga behörighetsmodell.

>[!IMPORTANT]
>
> För scenarier där innehåll ändras eller tas bort bör man använda AI Assistant-gränssnittet i stället för att anropa MCP-verktygen direkt, eftersom AEM Agents som körs av AI Assistant innehåller inbyggda skyddsfunktioner.
>

I den här artikeln förklaras vad AEM MCP-funktioner innehåller, vilka MCP-program som stöds, hur de konfigureras och hur de används i praktiken.

## Därför är MCP användbart för AEM-kunder {#why-mcp-is-useful-for-aem-customers}

Modern IDE- och chattapplikationer använder MCP som ett sätt för en LLM att anropa verktyg som exponeras bakom MCP-servrar. I stället för att skriva kod mot API-specifikationer på låg nivå kan kunderna beskriva sin avsikt på ett naturligt språk (*&quot;update the hero banner for this campaign across all pages&quot;*) och låta LLM anropa rätt MCP-verktyg, som i sin tur interagerar med AEM API:er.

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

De specifika verktyg som visas av varje MCP-server kan utvecklas över tid. I praktiken kan du be ditt MCP-aktiverade program att hitta verktyg via en uppmaning som:

*&quot;Visa alla AEM MCP-verktyg som är tillgängliga från den här servern och beskriv vad de gör.&quot;*

MCP-klienten använder MCP-protokollet för att hämta verktygslistan och scheman som LLM sedan kan använda.

## MCP-program som stöds {#supported-mcp-applications}

AEM MCP-servrar är utformade för att fungera med en definierad uppsättning MCP-kompatibla program. Följande program stöds:

* Anthropic Claude
* Markör
* OpenAI ChatGPT
* Microsoft Copilot Studio

Varje program har en egen konfigurationsupplevelse, men stegen på hög nivå är liknande.

## Översikt över inställningar {#setup-overview}

Konfigurering av MCP för AEM inbegriper två huvuddelar:

1. **Konfiguration i varje MCP-klientprogram** så att programmet vet hur man ansluter till AEM MCP-servrar och utför OAuth-inloggning
1. **Markera MCP-servern** innan du börjar fråga, så att MCP-klienten vet att den ska använda den.

### AEM Configuration {#aem-configuration}

Som standard styrs åtkomsten till AEM MCP-servrar av de behörigheter som enskilda användare har i AEM. När en användare autentiserar via ett MCP-klientprogram tillämpar MCP-verktygen samma åtkomstregler som för manuella åtgärder i AEM. En användare kan bara utföra åtgärder som de redan har behörighet att utföra.

#### Tillåtna MCP-klientprogram {#permitted-mcp-client-applications}

Följande MCP-klientprogram tillåts som standard:

* ChatGPT
* Claude
* MS Copilot Studio
* Markör

#### Begränsar MCP-servrar {#restricting-mcp-servers}

Alla MCP-servrar är tillåtslista som standard. Som administratör kan du begränsa åtkomsten till vissa MCP-servrar på organisations-, program- eller miljönivå. Detta ger en detaljerad kontroll över vilka MCP-funktioner som är tillgängliga för användare i organisationen.

#### Hantera MCP-klientåtkomst {#managing-mcp-client-access}

Administratörer kan även inaktivera åtkomst för specifika MCP-klientprogram om organisationens principer kräver det. Om du vill att Adobe ska aktivera stöd för ytterligare MCP-klientprodukter skickar du en länk till produktwebbplatsen. Om du behöver tillåtslista en anpassad MCP-klient, kontakta också.

Kontakta oss gärna på **aemcs-mcp-feedback@adobe.com** för alla MCP-serverrelaterade förfrågningar.

### Konfiguration av MCP-klientprogram {#mcp-client-application-configuration}

Det här steget utförs av varje användare (eller av en administratör för MCP-klientprogrammet, där det stöds). Konfigurationsinformationen varierar något mellan programmen. MCP-klienter utvecklas snabbt och stöd för MCP-fjärrservrar utvecklas aktivt. Du kan behöva aktivera utvecklarläget för att få åtkomst till funktionerna för att lägga till fjärrservrar, men den allmänna processen är:

1. Lägg till URL:er för AEM MCP-server
   * Konfigurera MCP-slutpunkterna från tabellen ovan. Till exempel:`https://mcp.adobeaemcloud.com/adobe/mcp/content-readonly`
1. Utlös anslutningen
   * Spara eller aktivera konfigurationen så att MCP-klientprogrammet försöker ansluta till AEM MCP-servern
1. Logga in med Adobe ID
   * Fyll i inloggningsflödet för Adobe när du uppmanas att göra det så att programmet kan få OAuth-tokens kopplade till din Adobe ID
1. Verifiera identifierade verktyg
   * När programmet har autentiserats identifieras MCP-verktygen från servern. Du kan sedan börja fråga LLM om du vill utföra AEM-åtgärder.

Nedan finns exempel på hur detta ser ut i alla program som stöds på en hög nivå.

**ChatGPT**

![Konfigurera ChatGPT-steg 1](assets/chatgpt-1.png)

![Konfigurera ChatGPT-steg 2](assets/chatgpt-2.png)

![Konfigurera ChatGPT-steg 3](assets/chatgpt-3.png)

![Konfigurera ChatGPT-steg 4](assets/chatgpt-4.png)

![Konfigurera ChatGPT-steg 5](assets/chatgpt-5.png)

![Konfigurera ChatGPT-steg 6](assets/chatgpt-6.png)

![Konfigurera ChatGPT-steg 7](assets/chatgpt-7.png)

* Lägg till URL:er för AEM MCP-server i området där MCP-anslutningar eller verktyg är konfigurerade
* Utlös anslutningen och logga in med din Adobe ID när den omdirigeras
* I en chatt kan du t.ex. hänvisa till de konfigurerade AEM-verktygen i dina uppmaningar:

  *&quot;Använd de konfigurerade AEM MCP-verktygen för att lista alla webbplatser i vår författarmiljö.&quot;*

**Claude**

![Konfigurera Claude Step 1](assets/claude-1.png)

![Konfigurera Claude Step 2](assets/claude-2.png)

![Konfigurera Claude Step 3](assets/claude-3.png)

![Konfigurera Claude Step 4](assets/claude-4.png)

![Konfigurera Claude Step 5](assets/claude-5.png)

![Konfigurera Claude Step 6](assets/claude-6.png)

![Konfigurera Claude Step 7](assets/claude-7.png)

* Registrera AEM MCP-serverns URL:er i Claude&#39;s MCP-konfiguration
* Slutför Adobe inloggningsflöde
* Du kan även aktivera automatisk bekräftelse för vissa verktyg i konfigurationsområdet. Detta rekommenderas för sökning och skrivskyddade åtgärder.
* Kontrollera att MCP-servern är markerad innan du startar konversationen
* Be Claude att utföra AEM-relaterade uppgifter. Claude väljer AEM-verktyg som exponeras av MCP-servern baserat på uppmaningen.

**Markör**

![Konfigurera markör, steg 1](assets/cursor-1.png)

![Konfigurera markör, steg 2](assets/cursor-2.png)

![Konfigurera markör, steg 3](assets/cursor-3.png)

![Konfigurera markör, steg 4](assets/cursor-4.png)

![Konfigurera markör, steg 5](assets/cursor-5.png)

* Skapa en ny MCP-serverpost med AEM MCP-URL:er i Markörens MCP-inställningar
* Autentisera med din Adobe ID när du uppmanas till det
* Du kan även aktivera eller inaktivera enskilda verktyg genom att klicka på verktygsnamnen. Alla verktyg är aktiverade som standard.
* Använd Markörens redigerare eller chatt för att starta AEM-verktyg som en del av arbetsflödena för utveckling och innehåll.

**Microsoft Copilot Studio**

![Konfigurera Copilot-steg 1](assets/copilot-1.png)

![Konfigurera Copilot-steg 2](assets/copilot-2.png)

![Konfigurera Copilot-steg 3](assets/copilot-3.png)

![Konfigurera Copilot-steg 4](assets/copilot-4.png)

![Konfigurera Copilot-steg 5](assets/copilot-5.png)

![Konfigurera Copilot-steg 6](assets/copilot-6.png)

![Konfigurera Copilot-steg 7](assets/copilot-7.png)

![Konfigurera Copilot-steg 8](assets/copilot-8.png)

![Konfigurera Copilot-steg 9](assets/copilot-9.png)

![Konfigurera Copilot-steg 10](assets/copilot-10.png)

* Skapa en ny agent
* Navigera till verktygsavsnittet och klicka på **Lägg till verktyg**
* Välj ett befintligt verktyg eller skapa ett nytt
* Konfigurera ett nytt MCP-verktyg som pekar på AEM MCP-serverns URL:er
* Upprätta en anslutning som kan delas eller dedikeras mellan agenter
* Logga in med din Adobe ID när den omdirigeras
* Alternativt kan du aktivera läget för automatisk bekräftelse eller kräva att slutanvändaren bekräftar för alla verktygsinteraktioner
* När du testar din agent öppnar du först anslutningshanteraren för att tilldela en anslutning till sessionen och trycker sedan på **Försök igen**.

## Autentisering {#authentication}

Adobe MCP-värdservrar implementerar OAuth och är integrerade med Adobe identitetssystem.

* När ett MCP-klientprogram ansluter till en AEM MCP-server visas en inloggningsdialogruta från Adobe och autentiseras med **Adobe ID**
* När inloggningen är klar verifierar systemet att MCP-klientprogrammet tillåts i organisationen och att den begärda MCP-servern tillåts. Om någon kontroll misslyckas visas ett felmeddelande.

![MCP-klienten tillåts inte, fel](assets/MCP-Client-not-permitted.png)

* Efter verifieringen utfärdar MCP-servern tokens som används för efterföljande verktygsanrop
* MCP-verktygen respekterar användarens AEM-behörigheter. En användare som inte har behörighet att ändra ett innehållsfragment i AEM kan inte heller ändra det via MCP.

Detta säkerställer att AI-assisterad verksamhet uppfyller AEM befintliga säkerhets- och styrningsmodell.

## Använda MCP med AEM {#using-mcp-with-aem}

När AEM och dina MCP-klientprogram har konfigurerats kan du arbeta i valfritt program och uppmana LLM att utföra AEM-åtgärder. LLM läser MCP-verktygsscheman, väljer vilka verktyg som ska anropas och sekvenserar dem efter behov för att uppfylla din begäran.

>[!IMPORTANT]
>
>För bästa resultat, särskilt med uppmaningar som innehåller flera steg eller som har olika innehållstyper som bilder och text som mål, aktiverar du en tänkande modell eller väljer alternativet Tänkning i MCP-klienten i stället för att förlita dig på läget Auto.

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

*&quot;Skapa ett nytt innehållsfragment för vårkampanjen baserat på vår hjältebanderodell och fyll i fälten i den här översikten.&quot;*

LLM väljer och koordinerar automatiskt nödvändiga MCP-verktyg.

## Förväntningshantering {#expectation-management}

När du arbetar med livslångt lärande via MCP bör du tänka på följande:

* **Kan användas med hög kapacitet men är inte ofelbar**
Hanterare av livslångt lärande kan utföra komplexa uppgifter men kan få tillfälliga fel. Samma uppmaning kan ge något annorlunda resultat eller presentationer utan någon självklar anledning. Granska alltid utdata innan du tillämpar ändringar på produktionsinnehållet.

* **Utvecklande funktioner**
LLM-modellerna förbättras kontinuerligt. Med tiden blir de smartare när det gäller att hitta nya sätt att kombinera MCP-verktyg för att uppnå era mål. En uppgift som kräver flera uppmaningar idag kan fungera sömlöst med en enda prompt imorgon.

* **Personlig tillsyn är nödvändig**
Tänk på LLM som en kunnig assistent som behöver tillsyn. Det har stor kunskap och kan ta fram kreativa lösningar, men det är till nytta för er vägledning och granskning. Verifiera resultaten, särskilt för kritiska operationer, och ge feedback när resultatet inte motsvarar dina förväntningar.

* **Var försiktig med automatisk bekräftelse av verktygskörningar**
Vissa MCP-klientapplikationer, som Claude, erbjuder möjligheten att automatiskt bekräfta verktygskörningar som efterfrågats av LLM. Detta kan vara praktiskt för skrivskyddade åtgärder som att söka efter eller hämta innehåll, men var försiktig med verktyg som uppdaterar eller tar bort innehåll. Granska varje begäran om verktygskörning innan du bekräftar åtgärder som ändrar din AEM-miljö.

## Begränsningar {#limitations}

AEM MCP-servrar är avsedda att konfigureras i ChatGPT, Claude, Cursor och Microsoft Copilot Studio.

Om du vill använda ett annat MCP-klientprogram kan du kontakta **aemcs-mcp-feedback@adobe.com** för att begära stöd för ytterligare klienter eller för att tillåtslista en anpassad klient.
