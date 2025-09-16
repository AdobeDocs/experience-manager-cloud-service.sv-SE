---
title: 'Form Builder: Välj metod'
description: Jämför formulärbyggare och hitta rätt sätt att skapa anpassningsbara formulär. Vare sig du är formulärskapare och behöver mallar eller vill skapa komplexa formulär väljer du den bästa formulärskaparen.
keywords: formulärbyggare, AEM-formulär, formulärskapare, skapa formulär, formulärskapare, adaptiva formulär, grundkomponenter, baskomponenter, kantleveranstjänster, skapa formulär
feature: Adaptive Forms, Core Components, Edge Delivery Services
role: User, Developer, Admin
level: Beginner
exl-id: choose-form-builder-guide
source-git-commit: ab84a96d0e206395063442457a61f274ad9bed23
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 0%

---


# Form Builder: Välj metod {#choose-your-form-builder}

Adobe Experience Manager (AEM) Forms har tre kraftfulla metoder för att skapa formulär, som var och en är utformad för olika användningsområden, tekniska krav och publiceringssätt. Vare sig du är formulärskapare och letar efter mallar eller utvecklare som skapar komplexa formulär, hjälper den här guiden dig att välja rätt formulärbyggare för ditt projekt.

## Snabbguide

Använd den här korta referensen för att identifiera den bästa formulärbyggaren för dina behov:

| **Om du behöver..** | **Välj** |
|-------------------|------------|
| **Moderna, skalbara formulär med de senaste funktionerna** | Kärnkomponenter |
| **Blixtsnabba formulär för webbplatser med hög trafik** | Universal Editor |
| **Underhåll befintliga formulär eller äldre integreringar** | Foundation Components |
| **Skapa genom att dra och släppa visuellt** | Core Components or Universal Editor |
| **Skapa kalkylbladsbaserade formulär** | Dokumentbaserad redigering |
| **Flerkanalsleverans (webb, mobil, kioskdatorer)** | Kärnkomponenter (med headless API:er) |
| **Anpassade klientprogram (React, Angular)** | Kärnkomponenter (med headless API:er) |
| **Full kontroll över formuläråtergivning** | Kärnkomponenter (med headless API:er) |

## Förstå alternativen för formulärbyggaren

AEM Forms erbjuder tre huvudmetoder för att bygga formulär, var och en utformade för olika typer av formulärskapare och användningsområden. Vare sig du behöver en enkel formulärtillverkare för snabba uppgifter eller avancerade funktioner för att skapa formulär för komplexa projekt finns det en lösning som passar dina behov:

### Foundation Component Form Builder

Foundation Components är den klassiska AEM Forms-redigeringsupplevelsen. Även om de fortfarande stöds rekommenderas de främst för att underhålla befintliga formulär i stället för att skapa nya.

**Viktiga egenskaper:**

- Traditionellt AEM-gränssnitt
- Beprövad stabilitet i befintliga arbetsflöden
- Begränsat till publicering endast för AEM
- Grundläggande komponentbibliotek

### Bygg kärnkomponentformulär

Core Components ger de senaste AEM Forms-funktionerna med förbättrade prestanda, tillgänglighet och flexibilitet. Denna formulärbyggare är idealisk för formulärskapare som behöver professionella resultat med moderna funktioner. Programmet har stöd för både AEM- och Edge Delivery Services-publicering och producerar automatiskt headless-formulär för API-driven leverans på flera plattformar.

**Viktiga egenskaper:**

- Moderna, standardiserade komponenter
- Förbättrade prestanda och tillgänglighet
- Flexibla publiceringsalternativ (AEM + Edge Delivery)
- Avancerade anpassningsfunktioner
- Framtidssäker arkitektur
- Automatisk generering av headless-formulär för flerkanalsleverans

### Universell redigerare (Edge Delivery Services)

Universell redigerare har två kraftfulla redigeringsmetoder för Edge Delivery Services: WYSIWYG visuella redigering och dokumentbaserad redigering med kalkylblad. Den här metoden är perfekt för användare som snabbt vill skapa formulär med enastående prestanda.

**Viktiga egenskaper:**

- Exceptionella prestanda (hög ljusstyrka)
- Två redigeringsmetoder: WYSIWYG och dokumentbaserade
- Optimerat för Edge Delivery Services
- Exceptionell prestanda och SEO
- Snabb utveckling och driftsättning


## Detaljerad jämförelse

### Teknisk kapacitet

| **Funktion** | **Foundation** | **Core** | **Universell redigerare** | **Dokumentbaserad** |
|----------------|----------------|----------|---------------------|-------------------|
| **Formulärkomplexitet** | Grundläggande | Avancerat | Avancerat | Enkel till måttlig |
| **Regelmotor** | Avancerat | Avancerat | Avancerat | Begränsad |
| **Anpassade komponenter** | ✅ | ✅ | ✅ | ✅ |
| **Teman** | ✅ | ✅ | Projektnivå | Projektnivå |
| **Mallar** | ✅ | ✅ | Endast ursprungligt innehåll |  |
| **Fragment** | ✅ | ✅ | ✅ | ✅ |
| **Lokalisering** | ✅ | ✅ | Via AEM Sites | Manuell/funktion |

### Integration och inlämning

| **Funktion** | **Foundation** | **Core** | **Universell redigerare** | **Dokumentbaserad** |
|-------------|----------------|----------|---------------------|-------------------|
| **Datamodeller** | FDM, anpassad | FDM, anpassad | FDM, anpassad | Egen |
| **Skicka åtgärder** | Flera alternativ | Flera alternativ | Flera alternativ | Endast kalkylblad |
| **Förifyll** | ✅ | ✅ | Via guide | ✅ |
| **CAPTCHA** | Flera typer | reCAPTCHA, hCaptcha | reCAPTCHA Enterprise | reCAPTCHA Enterprise |
| **Bifogade filer** | ✅ | ✅ | ✅ | Tidig tillgång |
| **Digitala signaturer** | ✅ |  |  |  |

### Publicering och prestanda

| **Proportioner** | **Foundation** | **Core** | **Universell redigerare** | **Dokumentbaserad** |
|------------|----------------|----------|---------------------|-------------------|
| **Publicerar** | Endast AEM | AEM + Edge Delivery + Headless API:er | Edge Delivery | Edge Delivery |
| **Prestanda** | Standard | Förbättrat | Höga ljusstyrkeresultat | Höga ljusstyrkeresultat |
| **SEO-optimering** | Grundläggande | Bra | Underbar | Underbar |
| **Mobil svarstid** | Bra | Underbar | Underbar | Underbar |

## Välja rätt byggare

### Välj grundkomponenter om:

- Du underhåller befintliga Foundation-baserade formulär
- Ni behöver integrera digitala signaturer
- Ditt arbetsflöde beror på etablerade grundfunktioner
- Du arbetar bara med publiceringskrav från AEM

**Perfekt för:** Formulärunderhåll, äldre systemintegration, etablerade arbetsflöden

### Välj kärnkomponenter om:

- Du skapar nya, moderna formulär
- Du behöver flexibilitet för att publicera på AEM eller Edge Delivery Services
- Du vill ha de senaste funktionerna
- Du behöver avancerade anpassningar och teman
- Tillgänglighet och prestanda är prioriterade
- Du vill ha framtidssäkrad teknik

**Perfekt för:** nya projekt, skalbara lösningar, moderna webbupplevelser

### Välj universell redigerare om:

- Du behöver enastående prestanda och SEO
- Du håller på att bygga för Edge Delivery Services webbplatser
- Du behöver komplexa formulär med anpassade åtgärder
- Integrering med externa system krävs

**Perfekt för:** Högpresterande webbplatser, Edge Delivery Services, visuella redigeringsarbetsflöden

### Välj dokumentbaserad redigering om:

- Affärsanvändare föredrar att skapa kalkylblad
- Du behöver snabba prototyper och driftsättningar
- Forms är relativt enkelt (enkäter, registreringar, feedback)
- Datainsamling i kalkylblad som uppfyller dina behov
- Inga avancerade arbetsflöden för insändning krävs

**Perfekt för:** Snabb distribution, redigering av företagsanvändare, enkel datainsamling


## Migreringsöverväganden

### Från grund till botten

- **Rekommenderad metod:** Använd verktyget [för migrering](/help/forms/migration-utility-tool-for-af-core-components.md)
- **Fördelar:** Moderna funktioner, bättre prestanda, funktioner för dubbelpublicering
- **Ansträngning:** Medelhög till hög, beroende på formulärets komplexitet

### Från traditionell till universell redigerare

- **Metod:** Återskapa formulär med WYSIWYG eller dokumentbaserad redigering i Universal Editor
- **Fördelar:** Exceptionella prestanda, modern utvecklingsupplevelse, höga SEO-poäng
- **Ansträngning:** Hög för komplexa formulär, låg för enkla formulär

## Komma igång

När du har valt formulärverktyget:

### Foundation Components

1. [Skapa ett adaptivt formulär (grundkomponenter)](/help/forms/creating-adaptive-form.md)
2. [Utvecklingshandbok för Foundation Components](/help/forms/introduction-forms-authoring.md)

### Kärnkomponenter

1. [Skapa en adaptiv form (kärnkomponenter)](/help/forms/creating-adaptive-form-core-components.md)
2. [Översikt över funktionen Core Components](/help/forms/adaptive-form-core-components-json-schema-form-model.md)

### Universell redigerare (Edge Delivery Services)

1. **WYSIWYG Authoring:** [Komma igång med Universal Editor](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md)
2. **Dokumentbaserad redigering:** [Skapa ditt första formulär med kalkylblad](/help/edge/docs/forms/tutorial.md)


## Behöver du hjälp att fatta beslut?

Är du fortfarande osäker på vilken formulärbyggare du ska välja? Tänk på följande faktorer:

- **Teamexpertis:** Vilken är ditt teams tekniska kompetensnivå?
- **Projekttidslinje:** Hur snabbt behöver du distribuera?
- **Prestandakrav:** Är hastighet och SEO kritiskt?
- **Framtida skalbarhet:** Behöver du utöka eller ändra formulär ofta?
- **Publiceringsmål:** Var kommer formulären att publiceras?

Om du vill ha personlig vägledning kan du kontakta AEM Forms implementeringsteam eller Adobe support.

## Relaterade artiklar

- [Jämförelse av formulärframtagning](/help/edge/docs/forms/authoring-a-form.md)
- [AEM Forms Core Components - översikt](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=sv-SE)
- [Edge Delivery Services for Forms - översikt](/help/edge/docs/forms/overview.md)
- [Headless Adaptive Forms with Core Components](https://experienceleague.adobe.com/sv/docs/experience-manager-headless-adaptive-forms/using/tutorial/build-engaging-forms-using-core-components-and-headless-adaptive-forms-aem-forms-cloud-service)
