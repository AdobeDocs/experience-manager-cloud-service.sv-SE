---
title: Styrningsagent - översikt
description: Läs om hur AEM Governance Agent skyddar varumärkets integritet och efterlevnad i hela AEM
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
exl-id: 2c73c578-6655-43bf-b03a-cb3eb2284d07
source-git-commit: 568fd17353da93df0fa20e0c10e48d35890e7ed6
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 0%

---


# Styrningsagent - översikt {#governance-agent}

**Styrningsagenten** är en lösning som utformats för att skydda varumärkets integritet och efterlevnad i hela Adobe Experience Manager. Den tillämpar säkerhetsregler, regler och varumärkesregler för att säkerställa att alla interaktioner och aktiveringar följer etablerade standarder. Styrningsagenten är helt integrerad i AI-assistenten och är utformad för att fungera sömlöst i företagsmiljöer genom att utnyttja verktygen **A2A (Agent-to-Agent)** och **MCP (Model Control Protocol)**. Dessa integreringar gör att agenten kan ansluta till avancerade AI-koordinatorer som ChatGPT, Claude och andra externa AI-system, vilket säkerställer flexibel och skalbar intelligens på olika plattformar.

Viktiga funktioner:

* **Varumärkesstyrning:** Bevara varumärkets enhetlighet och minska antalet manuella granskningar genom att automatisera varumärkeskontroller för innehåll och resurser
* **Behörigheter och Digital Rights Management (DRM):** Säkerställer säkert och kompatibelt samarbete genom att styra behörigheter och användningsrättigheter för digitala resurser.

Genom att kombinera dessa funktioner minskar man riskerna och möjliggör snabb, säker och skalbar leverans.

>[!IMPORTANT]
>
>AI-genererade svar kan vara felaktiga eller vilseledande. Kontrollera att du dubbelkontrollerar föreslagna korrigeringar och svar.
>
>Se även [Adobe Experience Cloud Generative AI User Guidelines](https://www.adobe.com/legal/licenses-terms/adobe-dx-gen-ai-user-guidelines.html).

## Kompetens i AEM Governance Agent {#skills-in-aem-governance-agent}

### Varumärkesstyrning {#brand-governance}

Styrningsagenten kan validera innehåll mot varumärkesriktlinjer för att säkerställa enhetlighet i alla digitala upplevelser. Det använder fördefinierade varumärkesregler som ton, anspråk, logotypanvändning, typografi och bilder. Det fungerar i realtid i chatt, redigerare och gruppläge i Experience Hub, vilket gör det idealiskt för AI-genererat innehåll, webbplatsmigreringar och kortfattad framtagning av webbplatser.

![Varumärkesstyrning - översikt](/help/ai-in-aem/agents/governance/assets/brand-governance.png)

**Exempel på fråga:**

* *Är den här sidan anpassad efter mitt varumärke?`https://www.website/en.html`*
* *Följer `https://www.website/en.html` riktlinjer för varumärkesmeddelanden?*
* *Kontrollera om `https://www.website/homepage` följer varumärkesriktlinjerna*
* *Visa mina varumärkesriktlinjer*

### Behörighet och Digital Rights Management {#permission-and-digital-rights-management}

#### Behörighetshantering i Content Hub {#permission-management-in-content-hub}

I Content Hub säkerställer ledningsagenten att bara rätt personer har tillgång till rätt resurser vid rätt tidpunkt. Genom att tillämpa detaljerade, attributbaserade kontroller och användarrättigheter skyddar den känsligt innehåll samtidigt som det möjliggör säkert samarbete. Detta innebär minskad efterlevnadsrisk, starkare varumärkesintegritet och snabbare arbetsflöden. Teamen kan tryggt dela och återanvända resurser utan att behöva oroa sig för obehörig åtkomst eller missbruk. Denna balans mellan säkerhet och flexibilitet innebär ökad effektivitet och förtroende i hela organisationen.

![Översikt över behörighetshantering](/help/ai-in-aem/agents/governance/assets/permission-management.png)

**Exempel på fråga:**

* *Visa alla befintliga Content Hub ABAC-regler.*
* *Skapa en regel som ger gruppen&quot;Marknadsföring&quot; åtkomst till alla resurser.*
* *Ge säljgruppen åtkomst till resurser där marknadsföring :segment är lika med EMEA.*
* *Ta bort alla regler som ger åtkomst till extern byrå*
* *Vad är ABAC i Content Hub och vad kan du hjälpa mig med?*

#### Assets Digital Rights Management {#assets-digital-rights-management}

Med agenten kan ni hantera Assets digitala rättigheter i hela ert innehållsekosystem. Den styr behörigheter och användningsrättigheter på detaljnivå och ser till att resurser bara är tillgängliga och används inom definierade efterlevnadsgränser. Detta ger sinnesfrid, skyddar immateriell egendom, minskar de lagstadgade riskerna och upprätthåller varumärkets integritet. Genom att automatisera användningen av behörigheter kan teamen samarbeta säkert och säkert och därmed snabba upp innehållsdistributionen utan att äventyra säkerheten eller regelefterlevnaden.

![DRM-hanteringsöversikt](/help/ai-in-aem/agents/governance/assets/drm-management.png)

**Exempel på fråga:**

* *Förfaller någon av mina resurser snart?*
* *Hitta alla cykelresurser som gick ut förra månaden.*
* *Vilka resurser har nyligen gått ut?*
* *Hitta resurser utan förfallodatum*
* *Visa alla resurser i /content/dam/products som snart upphör att gälla inom 14 dagar*
