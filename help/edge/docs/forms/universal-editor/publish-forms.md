---
title: Publicera adaptiv Forms med Edge Delivery Services
description: Lär dig hur du publicerar, konfigurerar och får tillgång till Adaptive Forms med Edge Delivery Services för produktion.
feature: Edge Delivery Services
role: Admin, Architect, Developer
level: Intermediate
keywords: [publicera formulär, Edge Delivery Services, formulärkonfiguration, CORS, referensfilter]
exl-id: ba1c608d-36e9-4ca1-b87b-0d1094d978db
source-git-commit: cfff846e594b39aa38ffbd3ef80cce1a72749245
workflow-type: tm+mt
source-wordcount: 746
ht-degree: 0%

---

# Publicera adaptiv Forms med Edge Delivery Services

Genom att publicera ett adaptivt formulär blir det tillgängligt på Edge Delivery Services så att slutanvändarna kan öppna och skicka in det. Den här processen omfattar tre huvudfaser: publicera formuläret, konfigurera säkerhetsinställningar och få åtkomst till live-formuläret.

**Vad du ska göra:**

- Publicera formuläret i Edge Delivery Services
- Konfigurera säkerhetsinställningar för att skicka formulär
- Få åtkomst till och verifiera ditt publicerade formulär
- Ställ in rätt URL-routning och CORS-principer

## Förutsättningar

- Adaptivt formulär som skapats med Edge Delivery Services-mall
- Formuläret har testats och är klart för produktion
- AEM Forms författarbehörigheter
- Cloud Manager-åtkomst (för produktionskonfiguration)
- Utvecklare har tillgång till blockkod för formulär (för inställning av inskickning)

## Översikt över publiceringsprocessen

Publicering av formulär till Edge Delivery Services sker i tre faser:

- **Fas 1: Formulärpublikation** - Publicera formuläret till CDN och verifiera publiceringsstatus
- **Fas 2: Säkerhetskonfiguration** - Konfigurera CORS-principer och referensfilter för säkra överföringar
- **Fas 3: Åtkomst och validering** - Testa formulärfunktioner och validera hela arbetsflödet

Varje fas bygger på den föregående för att säkerställa säker, funktionell driftsättning.

### Fas 1: Publicera ditt formulär

+++ Steg 1: Starta publicering

1. **Öppna ditt formulär**: Öppna ditt adaptiva formulär i den universella redigeraren
2. **Starta publicering**: Klicka på ikonen **Publicera** i verktygsfältet

   ![Klicka på Publicera](/help/forms/assets/publish-icon-eds-form.png)

+++


+++ Steg 2: Granska och bekräfta

1. **Granska publiceringsresurser**: Systemet visar alla resurser som publiceras, inklusive ditt formulär

   ![Vid klickning på Publicera](/help/forms/assets/on-click-publish.png)

2. **Bekräfta publicering**: Klicka på **Publicera** för att fortsätta
3. **Bekräfta slutförande**: Leta efter bekräftelsemeddelandet

   ![Publiceringen lyckades](/help/forms/assets/publish-success.png)

+++


+++ Steg 3: Verifiera publikationsstatus

**Kontrollera status**: Klicka på ikonen **Publicera** igen för att visa aktuell status

![Publiceringsstatus](/help/forms/assets/publish-status.png)

**Kontrollpunkt för validering:**

- Formuläret visar statusen&quot;Publicerad&quot; i redigeraren
- Inga felmeddelanden under publiceringsprocessen
- Formuläret visas i listan med publicerade resurser

+++


+++ Hantera publicerade Forms

**Så här avpublicerar du ett formulär:**

1. Öppna formuläret i redigeraren
2. Klicka på menyn med tre punkter ( ⋯) i det övre högra hörnet
3. Välj **Avpublicera**

![Avpublicera formulär](/help/forms/assets/unpublish--form.png)

+++


### Fas 2: Konfigurera säkerhetsinställningar

+++ Varför säkerhetskonfiguration krävs

Om du vill aktivera säker formuläröverföring måste du konfigurera säkerhetsinställningar som:

- Tillåt att Edge Delivery Services skickar data till AEM
- Förhindra obehörig åtkomst till din AEM-instans
- Aktivera CORS (Cross-Origin Resource Sharing) för formulärinskickat material
- Filtrera begäranden om att endast tillåta giltiga Edge Delivery-domäner

>[!IMPORTANT]
>
>**Krävs för produktion**: De här konfigurationerna är obligatoriska för formuläröverföringar som ska fungera i produktionsmiljöer.

+++



+++ Steg 1: Konfigurera URL för att skicka formulär

**Syfte**: Skicka formulär direkt till din AEM-instans

**Filplats**: `blocks/form/constant.js` i ditt Edge Delivery Services-projekt

**Konfigurationsexempel:**

```javascript
// Production Environment
export const submitBaseUrl = 'https://publish-p120-e12.adobeaemcloud.com';

// Local Development Environment  
export const submitBaseUrl = 'http://localhost:4503';

// Staging Environment
export const submitBaseUrl = 'https://publish-staging-p120-e12.adobeaemcloud.com';
```

**Kontrollpunkt för validering:**

- `constant.js` fil uppdaterad med korrekt publicerings-URL för AEM
- URL:en matchar din miljö (produktion, mellanlagring eller lokal)
- Inget avslutande snedstreck i URL

+++



+++ Steg 2: Konfigurera CORS-inställningar

**Syfte**: Tillåt förfrågningar om formuläröverföring från Edge Delivery Services-domäner

**Implementering**: Lägg till CORS-konfiguration till din AEM-dispatcher eller Apache-konfiguration

```apache
# Local Development Environment
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(http://localhost(:\d+)?$)#" CORSTrusted=true

# Edge Delivery Services - Preview/Stage Environment  
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.page$)#" CORSTrusted=true

# Edge Delivery Services - Production Environment
SetEnvIfExpr "env('CORSProcessing') == 'true' && req_novary('Origin') =~ m#(https://.*\.hlx\.live$)#" CORSTrusted=true
```

**Kontrollpunkt för validering:**

- CORS-regler som tillämpas på dispatcherkonfigurationen
- Alla nödvändiga domäner (localhost, hlx.page, hlx.live) ingår
- Konfigurationen har distribuerats till målmiljön

**Referensdokumentation:**

- [CORS - konfigurationsguide](https://experienceleague.adobe.com/en/docs/experience-manager-learn/getting-started-with-aem-headless/deployments/configurations/cors)
- [Dokumentation för referentfilter](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/headless/deployment/referrer-filter)

+++



+++ Steg 3: Konfigurera referensfilter

**Syfte**: Begränsa skrivåtgärder till auktoriserade Edge Delivery Services-domäner

**Implementeringsmetod**: Konfigurera via Cloud Manager i AEM as a Cloud Service

**Konfigurationsfil**: Lägg till i projektets OSGi-konfiguration

```json
{
  "allow.empty": false,
  "allow.hosts": [],
  "allow.hosts.regexp": [
    "https://.*\\.hlx\\.page:443",
    "https://.*\\.hlx\\.live:443"
  ],
  "filter.methods": [
    "POST",
    "PUT", 
    "DELETE",
    "COPY",
    "MOVE"
  ],
  "exclude.agents.regexp": [
    ""
  ]
}
```

**Konfigurationsfördelning:**

- **`allow.empty`**: Avvisar begäranden utan referentrubriker
- **`allow.hosts.regexp`**: Tillåtna begäranden från Edge Delivery Services-domäner
- **`filter.methods`**: Tillämpar filtrering på dessa HTTP-metoder
- **`exclude.agents.regexp`**: Användaragenter exkluderades från filtrering

**Kontrollpunkt för validering:**

- Refererarfilterkonfiguration distribuerad via Cloud Manager
- Konfiguration aktiv i AEM publiceringsinstans
- Testa att skicka formulär från Edge Delivery Services
- Obehöriga domäner hindras från att skicka formulär

**Referensdokumentation:**

- [Konfigurera referensfilter via Cloud Manager](https://experienceleague.adobe.com/en/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing)

+++


### Fas 3: Få tillgång till ditt publicerade formulär



+++ URL-struktur för Edge Delivery Services

**Standard-URL-format:**

```
https://<branch>--<repo>--<owner>.aem.live/content/forms/af/<form_name>
```

**URL-komponenter:**

- **`<branch>`**: Git-förgreningsnamn (vanligtvis `main`)
- **`<repo>`**: Databasnamn
- **`<owner>`**: GitHub-organisation eller användarnamn
- **`<form_name>`**: Formulärets namn (gemener, avstavade)

**Miljöspecifika URL:er:**

```
# Production Environment (.aem.live)
https://main--universaleditor--wkndforms.aem.live/content/forms/af/wknd-form

# Preview Environment (.aem.page) 
https://main--universaleditor--wkndforms.aem.page/content/forms/af/wknd-form
```

+++



+++ Slutliga valideringssteg

**Verifiera formulärtillgänglighet:**

1. **Testa inläsning av formulär**: Besök din formulär-URL och bekräfta att det läses in korrekt
2. **Testa formulärskickning**: Fyll i och skicka formuläret för att verifiera databearbetningen
3. **Kontrollera responsiv design**: Testa formulär på olika enheter och skärmstorlekar
4. **Verifiera säkerhet**: Kontrollera att CORS och referensfiltret fungerar korrekt

**Förväntade resultat:**

- Formuläret läses in utan fel
- Alla formulärfält återges korrekt
- Blankettinskickningsprocesserna har slutförts
- Data visas i konfigurerad destination (kalkylblad, e-post osv.)
- Inga konsolfel relaterade till CORS eller säkerhetsprinciper

+++


## Nästa steg


- [Konfigurera formuläröverföringsåtgärder](/help/edge/docs/forms/universal-editor/submit-action.md)
- [Stila och tema dina formulär](/help/edge/docs/forms/universal-editor/style-theme-forms.md)
- [Skapa responsiva formulärlayouter](/help/edge/docs/forms/universal-editor/responsive-layout.md)
- [Lägg till reCAPTCHA-skydd](/help/edge/docs/forms/universal-editor/recaptcha-forms.md)



