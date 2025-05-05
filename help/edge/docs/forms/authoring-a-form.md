---
title: Hur skapar man blanketter i AEM?
description: Lär dig mer om de olika plattformar för formulärframtagning som finns i Adobe Experience Manager (AEM) och hur du väljer rätt plattform baserat på dina behov.
feature: Edge Delivery Services, Adaptive Forms, Core Components
role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: f6c6b4c17482eb519fb0d4287704d775d0a5da00
workflow-type: tm+mt
source-wordcount: '1176'
ht-degree: 0%

---


# Hur skapar jag Forms i Adobe Experience Manager (AEM)?

Adobe Experience Manager (AEM) är en flexibel plattform för att skapa formulär som är engagerande, responsiva, dynamiska och anpassningsbara. Det har ett intuitivt användargränssnitt och en mängd färdiga komponenter för att bygga och hantera adaptiva Forms. Forms kan skapas med eller utan en formulärmodell eller ett schema, beroende på dina behov.

## Viktiga överväganden när du väljer en redigeringsplattform

AEM har flera alternativ för att skapa interaktiva och engagerande blanketter. När du väljer en formulärredigeringsmiljö bör du tänka på följande faktorer:

| ? **Övervägande** | ? **Fråga** |
|----------------------|--------------------|
| **Användarexpertis** | Vilka skapar formulären - utvecklare, företagsanvändare eller innehållsförfattare? |
| **Komplexitet för formulär** | Behöver formuläret avancerade regler, dynamiska avsnitt eller integreringar? |
| **Återanvändbarhetsbehov** | Kommer delar av formuläret att återanvändas i olika formulär eller projekt? |
| **Flexibilitet för design** | Behöver du full kontroll över layout, teman och format? |
| **Integrationskrav** | Behöver formuläret ansluta till datamodeller, arbetsflöden eller externa system? |
| **Lätt att använda** | Är plattformen intuitiv för teamets tekniska kompetensnivå? |
| **Prestanda och skalbarhet** | Kommer blanketten att användas i stor skala eller i trafikmiljöer? |
| **Flerkanalsleverans** | Kommer formuläret att användas på webbplatser, i mobilappar, i kioskdatorer eller i flera kanaler? |
| **Flexibilitet för publicering** | Var kommer formulären att publiceras på AEM, Edge Delivery eller i anpassade appar? |

## Översikt över formulärredigeringsmetoder i AEM

AEM har stöd för flera redigeringsmetoder, som alla passar olika användarbehov, kunskapsnivåer och publiceringsmål.

* [Foundation Components](/help/forms/create-adaptive-form-tutorial.md): Använd Foundation Components för att skapa traditionella, interaktiva formulär. Passar bäst för formulär som integreras med äldre system eller som är beroende av etablerade arbetsflöden. Forms som skapats med Foundation Components kan bara publiceras på AEM och är inte kompatibla med Edge Delivery Services.

* [Kärnkomponenter](/help/forms/creating-adaptive-form-core-components.md): Använd kärnkomponenter för att skapa moderna, responsiva och skalbara formulär. De har stöd för återanvändbarhet, tillgänglighet och bättre prestanda. Forms som skapats med Core Components kan publiceras på både AEM och Edge Delivery Services, vilket ger flexibilitet på olika plattformar.

* [Edge Delivery Services Forms](/help/edge/docs/forms/overview.md): Edge Delivery Services Forms förändrar hur formulär skapas, körs och bearbetas. Genom att utnyttja Edge Delivery Services kan man skapa snabba, säkra och lättillgängliga digitala blanketter som förbättrar användarupplevelsen och effektiviteten i verksamheten i en snabb utvecklingsmiljö. Du kan skapa Edge Delivery Services Forms på två sätt:
   * [WYSIWYG Authoring](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md): Använd den universella redigeraren för att skapa visuella, dra-och-släpp-formulär som är idealiska för innehållsförfattare med begränsad teknisk kunskap. Forms som skapats med Universal Editor levereras med Edge Delivery Services för snabb och enkel rendering.
   * [Dokumentbaserad redigering](/help/edge/docs/forms/tutorial.md): Använd verktyg som Microsoft Excel eller Google Sheets för att definiera formulärstruktur och innehåll. Den här metoden är användbar för företagsanvändare som föredrar kalkylbladsdrivna indata. Dessa formulär publiceras vanligtvis via Edge Delivery Services och är lämpliga för att användas i små och stora volymer.
* [Headless Authoring](https://experienceleague.adobe.com/sv/docs/experience-manager-headless-adaptive-forms/using/tutorial/build-engaging-forms-using-core-components-and-headless-adaptive-forms-aem-forms-cloud-service): Använd API:er för att återge formulär som JSON för alla frontend, till exempel React, Angular, mobilappar eller kioskdatorer, utan att vara beroende av AEM. För närvarande stöder endast Core Components headless-leverans. Headless-formulär är idealiska för flerkanaliga användningsområden och används oberoende av AEM sidåtergivning, vilket gör dem flexibla för anpassade front-end-distributioner.

### Jämförelseanalys av AEM blankettkonstruktion

&#x200B; följande tabell innehåller en kortfattad jämförelse av olika metoder för att skapa AEM-formulär, där du kan markera metoder, funktioner, publiceringsalternativ och idealiska användningsområden för att du ska kunna välja den lämpligaste metoden.

| **Övervägande** | **Foundation Components** | **Kärnkomponenter** | **Universell redigerare (WYSIWYG)** | **Dokumentbaserad redigering** | **Headless Authoring** |
|--------------------------|---------------------------------------------------------------------|------------------------------------------------------------------------|-------------------------------------------------------------------------|---------------------------------------------------------------------------|-------------------------------------------------------------------------|
| **Idealiskt för** | Bevara gamla blanketter och arbetsflöden i AEM | Skalbara, moderna formulär med komplexa arbetsflöden och integreringar | Skapa blanketter för Edge Delivery Service-sajter med komplexa krav | Snabb framtagning av prototyper eller grundläggande formulär utan avancerade inskickningstjänster | Flerkanalsupplevelser över olika plattformar (webb, mobil, kioskdatorer etc.) |
| **Användarexpertis** | Utvecklare, innehållsförfattare | Utvecklare, Avancerade författare | Affärsanvändare, innehållsförfattare | Affärsanvändare | Utvecklare |
| **Komplexitet för formulär** | Grundläggande formulär | Komplexa formulär med dynamiska avsnitt | Komplexa formulär med anpassade åtgärder | Enkla formulär | Mycket komplexa, API-drivna formulär |
| **Flexibilitet för design** | Begränsad | Hög (CSS/JS-anpassning) | Måttligt (baserat på mallar) | Begränsad | Hög (frontend framework control) |
| **Integreringsfunktion** | Grundläggande AEM-arbetsflöden | Avancerat (datamodeller, arbetsflöden) | Integrerat med externa system | Grundläggande (Google Sheets, Excel) | Full kontroll via API:er |
| **Publiceringsmetod** | Endast AEM | AEM och Edge Delivery Services | Edge Delivery Services | Edge Delivery Services | Alla frontend via API:er |
| **Prestanda och SEO** | Standard | Förbättrat jämfört med Foundation Components | Google Lighthushud ger snabbare rendering och bättre SEO | Google Lighthushud ger snabbare rendering och bättre SEO | Beroende på implementering |
| **Flerkanalsleverans** | Begränsad | Måttlig | Måttlig | Begränsad | Hög |

<!--
| **Form authoring methods** | **Key Approach** | **Features** | **Publishing Method** | **Use Cases** |
|-----------------------------|------------------|--------------|-----------------------|---------------|
| **Foundation Components** | Classic AEM authoring interface designed for standard web pages. | Includes basic components like text, images, tables, and charts. Limited reuse capabilities and primarily web-based. | Published on AEM only. | Best for maintaining legacy forms and workflows within AEM. |
| **Core Components** | Provides a modern, flexible approach with high customization capabilities. | Component-based authoring within AEM, offering high customization with CSS and JS. Built around accessibility guidelines and integrated with AEM Sites. | Published on AEM and Edge Delivery Services. | Suitable for scalable, modern forms with complex workflows and integrations. |
| **Universal Editor (WYSIWYG)** | Offers a WYSIWYG interface for intuitive form creation. | Forms are designed using an intuitive drag-and-drop interface. These forms inherit look and feel from the configured Edge Delivery Services GitHub repository for the corresponding form. | Published on Edge Delivery Services, achieving high Google Lighthouse scores for faster rendering and better SEO. | Ideal for creating forms for Edge Delivery Service sites and pages, especially scenarios involving complex forms, workflows, custom actions, or integrations with external systems. |
| **Document-based Authoring** | Uses familiar tools like Google Docs and Microsoft Office for form creation. | Forms are designed using spreadsheets, with data directly submitted to Google Sheets or Microsoft Excel. These forms are faster to create and deploy. No prior knowledge of AEM is required to develop custom components and styles for these forms. | Published on Edge Delivery Services, achieving high Google Lighthouse scores for faster rendering and better SEO. | Ideal for quick prototyping or basic forms where advanced submission services are not needed. Well-suited for surveys, registration, or feedback forms requiring data storage in spreadsheets. |
| **Headless Authoring** | Enables API-driven content creation for omnichannel delivery. | Full control via frontend frameworks, allowing content delivery across various platforms through APIs. | Can be integrated with any frontend via APIs. | Ideal for omnichannel experiences across platforms, suitable for web, mobile, kiosks, and more. |-->

### Jämförelse av AEM blankettkonstruktion

I följande tabell finns en detaljerad jämförelse av de viktigaste funktionerna i olika AEM-metoder för att skapa formulär, som hjälper dig att välja den metod som passar bäst för dina behov. &#x200B;

| **Funktion** | **Foundation Components** | **Kärnkomponenter** | **Universell redigerare (WYSIWYG)** | **Dokumentbaserad redigering** | **Headless Authoring** |
|-----------------------------------------|---------------------------|---------------------|-------------------------------|-----------------------------|------------------------|
| **Enhetlig komposition med platser** | ❌ | ✅ | ✅ | ❌ | ❌ |
| **Stöd för inbäddning av formulär** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **Regler (dynamiskt beteende)** | Avancerad regelredigerare med anpassade funktioner | Avancerad regelredigerare med anpassade funktioner | Avancerad regelredigerare med anpassade funktioner | Begränsad: Visa/dölj, beräkna värde, anpassade funktioner | Begränsad: Kräver anpassad implementering |
| **Stöd för bifogade filer** | ✅ | ✅ | ✅ | ℹ️ (tidig åtkomst) | ❌ |
| **CAPTCHA-stöd** | reCAPTCHA v2/Enterprise, Captcha (EA), Turnstile (EA) | reCAPTCHA v2/Enterprise, hCaptcha (EA) | reCAPTCHA Enterprise | reCAPTCHA Enterprise | Kräver anpassad integrering |
| **Överföringsfunktioner** | REST endpoint, Email, Form Data Model (FDM), Invoke AEM Workflow, SharePoint, OneDrive, Azure Blob Storage, Power Automate, Workfront Fusion (EA) | REST endpoint, Email, Form Data Model (FDM), Invoke AEM Workflow, SharePoint, OneDrive, Azure Blob Storage, Power Automate, Workfront Fusion (EA) | REST endpoint, Email, Form Data Model (FDM), Invoke AEM Workflow, SharePoint, OneDrive, Azure Blob Storage, Power Automate, Workfront Fusion (EA) | Endast kalkylblad | Anpassade API-slutpunkter |
| **Dataschema** | FDM, anpassad | FDM, anpassad | FDM, anpassad | Egen | Egen |
| **Förifyll** | ✅ | ✅ | ? (via guide) | ✅ | Anpassad implementering |
| **Fragment** | ✅ | ✅ | ✅ | ✅ | ❌ |
| **Visuell regelredigerare** | ✅ | ✅ | ✅ | ❌ | ❌ |
| **Lokalisering** | ✅ | ✅ | ? (via platser) | ℹ️ (Excel - manuell, Google Sheets-funktion) | Anpassad implementering |
| **Dataschema (dataträd)** | ✅ | ✅ | ? (via UI-tillägg) | ❌ | Anpassad implementering |
| **Mallstöd** | ✅ | ✅ | Endast ursprungligt innehåll, ingen princip | ❌ | Anpassad implementering |
| **Portal** | ✅ | ✅ | ❌ | ❌ | ❌ |
| **DoR-redigering** | ✅ | ✅ | ? (via Derlina) | ❌ | ❌ |
| **DoR-generering** | ✅ | ✅ | ? (FORMS-2475 Nyhet) | ❌ | ❌ |
| **Tema** | ✅ | ✅ | ℹ️ (på projektnivå) | ℹ️ (på projektnivå) | Anpassad implementering |
| **Egen komponent** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **OTB och anpassade funktioner** | ✅ | ✅ | ✅ | ✅ | ✅ |
| **Fragmentreferens** | ✅ | ❌ | ❌ | ❌ | ❌ |
| **Signeringsintegrering** | ✅ | ❌ | ❌ | ❌ | ❌ |
| **RTL-stöd** | ❌ | ✅ | ? | ? | Anpassad implementering |
| **Experimentation** | ❌ | ❌ | ✅ | ✅ | Anpassad implementering |
| **Aktivitetshantering via Workfront** | ❌ | ❌ | ✅ | ❌ | ❌ |
| **Personalization-tillägg** | ❌ | ❌ | ? | ❌ | Anpassad implementering |
| **Anpassning av redigerare** | ❌ | ❌ | ✅ (via UI-tillägg) | ❌ | Anpassad implementering |
| **Skicka åtgärd** | ✅ | ✅ | ✅ | Endast kalkylblad | Anpassad implementering |


## Relaterad artikel

* [Dokumentbaserad redigering med Microsoft Excel eller Google Sheets](/help/edge/docs/forms/create-forms.md)
* [Universell redigerare för WYSIWYG-redigering](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring)
* [Skapa ett adaptivt formulär (grundkomponenter)](/help/forms/creating-adaptive-form.md)
* [Skapa en adaptiv form (kärnkomponenter)](/help/forms/create-an-adaptive-form.md)
