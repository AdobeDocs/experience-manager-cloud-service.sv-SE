---
title: Edge Delivery Services for AEM Forms - översikt
description: Lär dig använda Edge Delivery Services för att skapa och leverera högpresterande blanketter med AEM Forms, vilket möjliggör snabb utveckling och smidig datainsamling.
feature: Edge Delivery Services
exl-id: ecea1e05-d36b-4d63-af9d-c69dafd2f94f
role: Admin, Architect, Developer
source-git-commit: 1ddf97f56e5a9b7c95959da47a748f5a6d128e43
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 0%

---


# Edge Delivery Services för AEM Forms


Edge Delivery Services för AEM Forms är en sammansatt uppsättning tjänster som möjliggör en snabb utvecklingsmiljö där författare snabbt kan uppdatera, publicera och öppna nya formulär. Dessa tjänster ger enastående och slagkraftiga formulärupplevelser som skapar engagemang och konverteringar. Dessa blankettupplevelser är enkla att skapa och utveckla.

* **Snabbare upplevelser:** Forms levereras från ett globalt leveransnätverk (CDN), vilket gör att de läses in snabbt för användarna.
* **Snabb utveckling:** En smidig utvecklingsprocess ger snabbare uppdateringar. Ändringar kan publiceras utan att vänta på långa pipelinebyggen.
* **Flexibel redigering:** Välj bland olika verktyg för att skapa formulär, inklusive dokumentbaserad redigering (Microsoft Word, Google Docs/Sheets) eller en visuell WYSIWYG-redigerare (Universal Editor).

## Så här fungerar det

Med Edge Delivery Services kan formulärets struktur och innehåll ligga i källor som AEM as a Cloud Service, Microsoft SharePoint eller Google Drive. Detta innehåll publiceras till ett globalt CDN. När en användare besöker din plats, skickas formuläret direkt från närmaste CDN-edge-server för optimala prestanda.

![Förenklat arkitekturdiagram med innehållskällor, ett CDN och användaren.](/help/forms/assets/eds-simplified-architecture.png)
**Förenklad Edge Delivery Services-arkitektur med Forms**

De data som användarna skickar kan skickas till olika destinationer, från ett enkelt kalkylblad till en kraftfull AEM-server för vidare bearbetning.

## Välja en redigeringsmetod

Du kan skapa formulär för dina Edge Delivery Services-webbplatser på flera olika sätt. Vilken metod som är bäst beror på teamets kompetens, formulärets komplexitet och projektkraven.

![Beslutsträd som hjälper dig att välja en formulärredigeringsmetod.](/help/forms/assets/eds-authoring-selection.png)
**Beslutsträd för formulärredigering**

### Dokumentbaserad redigering

Med den här metoden kan du [skapa formulär med Microsoft Word eller Google Docs/Sheets](/help/edge/docs/forms/create-forms.md). Du definierar formulärfält, etiketter och typer i ett dokument med ett specifikt tabellformat. Edge Delivery Services konverterar det här dokumentet till ett interaktivt HTML-formulär.

**Funktioner:**

* Skriv i välkända verktyg: Word, Google Docs eller Google Sheets.
* Definiera fält som textinmatningar, e-post, listrutor, kryssrutor och alternativknappar.
* Ange grundläggande valideringsregler, till exempel obligatoriska fält.
* Integrera Google reCAPTCHA för att skydda skräppost.
* Stöd för filöverföringar.
* Skicka data direkt till ett kalkylblad eller en e-postadress.
* Utöka med anpassad kod via GitHub för avancerade komponenter och format.

**Bäst för:**

* Team som i första hand använder dokumentredigerare för att skapa innehåll.
* Skapa snabbt enkla till måttligt komplexa formulär.
* Enkel datainsamling till kalkylblad eller e-post.

Överföringar från dokumentbaserade formulär hanteras vanligtvis av [AEM Forms Submission Service](/help/forms/forms-submission-service.md) som dirigerar data till ett konfigurerat kalkylblad eller en konfigurerad e-postadress.

### Redigering i Universal Editor

Den universella redigeraren [har ett modernt WYSIWYG-gränssnitt](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md) som gör att du kan skapa formulär genom att dra och släppa.

**Funktioner:**

* Skapa formulär visuellt genom att dra och släppa med ett bibliotek med färdiga komponenter.
* Konfigurera realtidsvalidering och komplex affärslogik (t.ex. visa/dölj fält baserat på användarval).
* Direktförhandsvisning för olika enheter.
* Djupgående integrering med AEM as a Cloud Service-funktioner som Content Fragments, AEM Workflows och user permissions.
* Skapa och redigera AI-assisterade formulär med&quot;Experience Builder&quot;.

**Bäst för:**

* Skapa komplexa formulär med villkorsstyrd logik, flerstegspaneler eller personalisering.
* Team (t.ex. marknadsförare, affärsanvändare) som föredrar visuella verktyg.
* Projekt som kräver stark integrering med AEM serverdel för databearbetning och arbetsflöden.

Forms som skapats med Universal Editor kan använda [Forms Submission Service](/help/forms/forms-submission-service.md) eller konfigureras att använda [skicka-åtgärder som tillhandahålls av OTB för avancerad datahantering](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md), till exempel skicka data till ett AEM Workflow, en REST-slutpunkt eller till en databas.

### Bädda in Forms på dokumentredigeringssidor

[Document Authoring (DA)](https://www.aem.live/developer/da-tutorial) är en Adobe-värdtjänst för hantering av webbplatsinnehåll för Edge Delivery Services. DA är inte ett själva formulärbyggverktyg, men du kan använda det för att skapa webbsidor och sedan bädda in formulär som har skapats med andra metoder.

**Så här fungerar det:**

1. **Skapa formuläret:** Bygg formuläret med antingen dokumentbaserad redigering eller den universella redigeraren.
2. **Publicera formuläret:** Kontrollera att formuläret är publicerat och tillgängligt på sin egen URL.
3. **Bädda in i DA:** Lägg till ett block på dokumentredigeringssidan som refererar till formulärets URL för att bädda in det.

Detta är ett arbetssätt för team som använder dokumentredigering som sitt primära innehållshanteringssystem för Edge Delivery Services webbplatser.

## Jämförelse av redigeringsmetod

| Kriterier | Dokumentbaserad redigering | Universal Editor (WYSIWYG) | Forms in Document Authoring (DA) |
|----------------------------------|---------------------------------------|-----------------------------------------|-------------------------------------------|
| **Primärt redigeringsverktyg** | Word/Google Docs/Sheets | Webbläsare (AEM Universal Editor) | Ej tillämpligt (Forms är *inbäddat*) |
| **Teamkunskapsnivå** | Välbekant med dokumentredigerare | Bekvämt med visuella webbverktyg | Använder DA för sidinnehåll |
| **Vanlig formulärkomplexitet** | Enkel till måttlig | Medelhög till komplex, företagsnivå | Beroende på det inbäddade formuläret |
| **Alternativ för överföring** | Forms Submission Service (to Sheet/Email) | Forms Submission Service, AEM Publish (arbetsflöde, formulärdatamodell, tredjepartsintegreringar) | Följer inbäddade formulärinställningar |
| **AEM Backend Integration** | Minimal | Hög (med AEM Publish) | Indirekt, via inbäddad Universal Editor-blankett |
| **Bäst för..** | Snabb framtagning av enkla blanketter av content team, snabb datainhämtning. | Marknadsförare och affärsanvändare som behöver visuell kontroll, komplexa blanketter eller djupgående integrering med AEM. | Webbplatser där primärt innehåll hanteras i DA. |

<!-- 
## Detailed Feature Comparison

| **Capability**                        | **Universal Editor (WYSIWYG)** | **Document-based Authoring** | **Document Authoring (DA)** |
|-----------------------------------------|-------------------------------|-----------------------------|-----------------------------|
| **Unified Composition with Sites**    | ✅                            |                              | ✅ (with embedded forms)     |
| **Embedding Form Support**            | ✅                            | ✅                          | ✅ (embed from Universal Editor or Docs)   |
| **Rules (Dynamic Behavior)**          | Advanced rules editor with custom functions | Limited: Show/hide, compute value, custom functions | Depends on embedded form     |
| **Attachment Support**                | ✅                            | ℹ️ (Early Access)           | Depends on embedded form     |
| **CAPTCHA Support**                   | reCAPTCHA Enterprise          | reCAPTCHA Enterprise       | Depends on embedded form     |
| **Submission Features**               | REST, Email, FDM, Workflow, SharePoint, OneDrive, Azure Blob, Power Automate, Workfront Fusion (EA) | Only Spreadsheet            | Follows embedded form's setup |
| **Data Schema**                       | FDM, Custom                   | Custom                      | Based on embedded form       |
| **Pre-fill**                          | 💡 (via Wizard)               | ✅                          | Depends on embedded form     |
| **Fragments**                         | ✅                            | ✅                          | Depends on embedded form     |
| **Visual Rule Editor**                | ✅                            |                              |                              |
| **Localization**                      | 💡 (via Sites)                | ℹ️ (Excel/Sheets manual)    | Depends on embedded form     |
| **Template Support**                  | Only Initial Content          |                              |                              |
| **Theme**                             | ℹ️ (at project level)         | ℹ️ (at project level)        | ℹ️ (based on hosting site)    |
| **Custom Component**                  | ✅                            | ✅                          | ✅ (if embedded component supports it) |
| **Experimentation**                   | ✅                            | ✅                          | Depends on embed context     |
| **Submit Action**                     | ✅                            | Only Spreadsheet            | Based on embedded form       |
-->



## Nästa steg

* [Skapa ett formulär med dokumentbaserad redigering](/help/edge/docs/forms/tutorial.md)
* [Läs om Universal Editor för Forms](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
* [Konfigurera formuläröverföringsåtgärder](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)
* [Läs mer om dokumentredigering (DA)](https://www.aem.live/developer/da-tutorial)
