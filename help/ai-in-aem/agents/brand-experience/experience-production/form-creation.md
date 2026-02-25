---
title: Skapad av formulär
description: Läs mer om hur Brand Experience Agent skapar formulär och hur man använder naturligt språk för att skapa formulär från grunden.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
exl-id: 24ad5f36-405b-4ea2-9819-de6aea856a7a
source-git-commit: 36f4ba8207da67b8e68c9c9851311defc909b495
workflow-type: tm+mt
source-wordcount: '509'
ht-degree: 0%

---


# Skapad av formulär {#form-creation-job}

Jobbet för att skapa formulär är en funktion hos [varumärkesagenten](/help/ai-in-aem/agents/brand-experience/overview.md) som har utvecklats för att utveckla formulär med hjälp av naturliga språkuppmaningar. Det här jobbet genererar automatiskt lämplig formulärstruktur och fälttyper. Jobbet nås via AI Assistant.

Några av fördelarna med att skapa formulär:

* **Snabbare formulärutveckling**: Skapa formulär snabbt med enkla naturliga språkkommandon, så att du slipper lära dig traditionella produktgränssnitt.
* **Enhetliga varumärkesanpassade och varumärkesanpassade upplevelser**: Skapa formulär som följer företagets riktlinjer för varumärken, mallar och format med hjälp av godkända mallar och format.
* **Lägre tekniska hinder**: Låt företagsanvändare enkelt skapa formulär utan att behöva ha avancerade tekniska eller djupgående produktkunskaper.

## Funktioner {#capabilities}

* **Skapa ett nytt formulär med en normal textfråga**: Du kan skapa ett formulär genom att skicka in dina krav på ett vanligt språk. Kunskapen genererar automatiskt lämplig formulärstruktur, fälttyper och varumärkesupplevelser baserat på din naturliga språkbeskrivning och angivna mall. Detta snabbar upp framtagningen av blanketter samtidigt som varumärke och regelefterlevnad upprätthålls.

* **Importera ett PDF-dokument och konvertera det till formulär**: Du kan importera och omvandla befintliga PDF-dokument till formulär. Kunskapen analyserar överfört innehåll för att identifiera fälttyper, bevara layouter och förbättra formulär med responsiv design- och valideringslogik samtidigt som varumärkes- och efterlevnadsstandarder upprätthålls.

När du använder någon av dessa funktioner uppmanas du att välja vilken typ av formulär som ska skapas. Ange antingen en Core Components-baserad mall för adaptiva formulär eller en Edge Delivery Services-baserad mall för adaptiva formulär och ange den sökväg du vill spara formuläret på. Om du skapar ett formulär baserat på Edge Delivery Services kan du även ange GitHub-URL:en för din databas.


### Exempelfrågor {#sample-prompts}

* *Skapa ett formulär för feedbacksamling med namn, e-post och meddelandefält*
* *Skapa ett formulär för kundfeedback med produktbetyg (1-5 stjärnor), kommentarsfält och valfritt e-postmeddelande*
* *Skapa ett kontaktformulär med namn, e-post, listruta med ämnen och meddelandefält*
* *Skapa ett registreringsformulär med personlig information, kontoinställningar och accepterande av villkor*
* *Skapa ett kreditkortsansökningsformulär genom att importera PDF-filen som finns på`https://[aem-author-url]/path/to/pdf/file`*
* *Skapa ett feedbackformulär med mallsidan på`https://github.com/wkndforms/wesecure`*

## Förfina formuläret {#refine-with-forms-experience-builder}

När du har skapat en inledande formulärstruktur med hjälp av AI-assistenten kan du använda Forms Experience Builder för att:

* **Uppdatera formulär**: Lägg till eller ändra fält, justera fälttyper och uppdatera format efter behov med den visuella redigeraren.

* **Uppdatera layout**: Ordna om avsnitt, grupper eller fält, justera mellanrum och ändra den visuella hierarkin för att förbättra användbarheten och säkerställa att formuläret är tydligt och intuitivt för läsarna.

* **Lägg till affärslogik**: Skapa villkorslogik, visa/dölj regler, fältberoenden och definiera valideringsregler.

* **Konfigurera sändning**: Konfigurera var formulärdata skickas, inklusive konfigurera e-postmeddelanden, integrering med arbetsflöden eller anslutningar till externa system.

Mer information finns i [dokumentationen för Forms Experience Builder.](/help/forms/experience-builder/product-overview.md)

## Aktivering {#activation}

Du kan utforska AEM Agents via [Playground](https://www.aem.live/developer/aem-playground) eller ansluta till din CSM eller TAM för att diskutera åtkomst via din SKU.

<!-- 
#### Import and convert {#import-and-convert}

Transform existing documents into interactive digital forms. The agent analyzes uploaded content to detect field types, preserve layouts, and enhance forms with responsive design and validation logic. Supported formats include Acroforms, XFA PDFs, flat PDFs, images (JPG, PNG), and hand-drawn form photographs.

>[!VIDEO](https://video.tv.adobe.com/v/3474042)

**Prompt examples:**

* *Convert the attached PDF file to an adaptive form*
* *Transform this scanned form image into an interactive digital form*
* *Import the employee onboarding PDF and create an editable form*
* *Convert this paper form photograph into a digital form with validation*
-->

<!-- 
### Embed an existing form to a sites page {#embed-existing-form}

The form creation skill enables seamless integration of existing forms into any sites page through natural language commands. Rather than manually locating, copying, and embedding form components, users can simply specify which form to add and where to place it. The agent handles the technical implementation, ensuring proper rendering and functionality.

>[!VIDEO](https://video.tv.adobe.com/v/PLACEHOLDER)

**Prompt examples:**

* *Embed the contact form to the homepage*
* *Add the existing customer feedback form to the support page*
* *Insert the newsletter signup form into the footer section*
* *Place the registration form on /content/site/signup*
* *Add form "contact-us-2024" to the current page*
-->

<!-- 
### Build and add a form to an existing sites page {#build-and-add-form}

The form creation skill combines form creation and site integration in a single conversational workflow. Users can describe the form they need and specify where to add it, and the agent creates the form and embeds it into the specified page automatically. This eliminates the traditional multi-step process of creating a form separately and then manually adding it to a page.

>[!VIDEO](https://video.tv.adobe.com/v/PLACEHOLDER)

**Prompt examples:**

* *Create a newsletter signup form with email field and add it to the footer*
* *Build a quick contact form with name, email, and message, then add it to /content/about-us*
* *Add a feedback form with rating stars and comment field to this page*
* *Create a simple survey form with 5 questions and embed it on the customer portal homepage*
* *Build an event registration form with name, email, and date selection, then add it to /content/events/conference-2025*
-->
