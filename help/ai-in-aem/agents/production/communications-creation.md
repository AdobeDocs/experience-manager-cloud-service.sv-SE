---
title: Kommunikativ förmåga
description: Lär dig mer om Experience Production Agents förmåga att skapa kommunikation och hur du använder naturligt språk för att skapa interaktiv kommunikation.
feature: Edge Delivery Services, Agentic AI
role: User, Admin, Architect, Developer
source-git-commit: aa8369979c99535f0fd77e6a51af10cc17afd971
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---


# Kunskap att skapa kommunikation {#ic-creation-skill}

>[!NOTE]
>
> Kommunikationsskapandet är för närvarande alfavärdet. Om du vill delta skickar du en förfrågan från din officiella e-postadress till [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com).

Interaktiv kommunikation är personaliserade, datadrivna dokument utformade för affärskommunikation som kontoutdrag, policydokument, räkningar, välkomstpaket och förmånsmeddelanden. Till skillnad från formulär som samlar in data från användare genererar interaktiv kommunikation utdatadokument med dynamiskt, mottagarspecifikt innehåll.

Kunskap och färdigheter i att skapa kommunikation är en funktion hos Experience Production Agent, som är utformad för att utveckla interaktiv kommunikation med hjälp av naturliga språkuppmaningar. Denna kompetens genererar automatiskt personaliserad, datadriven korrespondens för tryck (i PDF-format). Kompetensen nås via AI Assistant.

Några av fördelarna med att skapa kommunikationsfärdigheter är:

* **Snabbare kommunikationsutveckling**: Skapa kommunikation snabbt med enkla naturliga språkkommandon, så att du slipper lära dig traditionella produktgränssnitt.
* **Enhetlig och varumärkesanpassad korrespondens**: Skapa kommunikation som följer företagets riktlinjer för varumärken, mallar och format med hjälp av godkända mallar och format.
* **Lägre tekniska hinder**: Gör det möjligt för företagsanvändare att enkelt skapa kommunikation utan att behöva avancerade tekniska eller djupgående produktkunskaper.

## Funktioner {#capabilities}

<!-- * **Create personalized communications with plain text prompt**: You can create communication documents for print (in PDF format) by submitting your requirements in plain language. The agent automatically generates appropriate document structures, layouts, and data bindings based on your natural language description. -->

* **Skapa från mallar**: Du kan använda godkända organisationsmallar för att säkerställa varumärkets enhetlighet och efterlevnadsstandarder. Medarbetaren använder era befintliga mallar och stilriktlinjer för att skapa varumärkesbaserad korrespondens som uppfyller myndigheternas krav.

* **Importera och konvertera befintliga bilder och dokument till interaktiv kommunikation**: Du kan importera och omvandla befintliga dokument till interaktiv kommunikation. Agenten analyserar överfört innehåll för att identifiera fält, bevara layouter och skapa datadriven korrespondens med dynamiskt innehåll. De format som stöds är bland annat PDF-filer, bilder (JPG, PNG) och handritade mallar.


## Exempeluppmaningar {#sample-prompts}

* *Skapa en kommunikation för ett låneutdrag med hjälp av mallen på https://[aem-author-url]/path/to/pdf/file*
* *Skapa ett meddelande från PDF på https://[aem-author-url]/path/to/pdf/file*
* *Skapa en kommunikation från en bildfil på https://[aem-author-url]/path/to/image/file*
* Skapa ett brev med PDF-fil på https://[aem-author-url]/path/to/pdf/file


## Förfina kommunikationen {#refine-with-ic-editor}


När du har skapat en inledande kommunikationsstruktur med hjälp av AI Assistant kan du förfina och förbättra dokumentet med hjälp av Interactive Communications Editor. I Interactive Communications Editor kan du tillhandahålla uppmaningar på ett naturligt språk för att:

* **Lägg till fält och innehåll**: Lägg till nya fält, textblock, bilder, diagram, tabeller och andra komponenter i dina kommunikationsdokument med hjälp av naturliga språkinställningar. Agenten tolkar dina instruktioner och infogar lämpliga element med rätt struktur och formatering.

* **Redigera fält och innehåll**: Ändra befintliga fält och innehåll i kommunikationsdokument med hjälp av konversationskommandon. Uppdatera fältegenskaper, ändra textinnehåll, justera databindningar och förfina komponentkonfigurationer.

* **Ta bort fält och innehåll**: Ta bort oönskade fält, komponenter eller avsnitt från kommunikationsdokument med hjälp av naturliga språkinstruktioner. Agenten tar bort de angivna elementen samtidigt som dokumentstrukturen och layoutintegriteten bevaras.

* **Formatera fält och innehåll**: Formatera och formatera fält och innehåll med hjälp av naturliga språkuppmaningar. Justera typsnitt, färger, justering, mellanrum och andra visuella egenskaper så att de matchar varumärkets riktlinjer och designkrav.

### Exempeluppmaningar för att förfina kommunikationen {#sample-prompts-refining}

* *Generera ett kvittningsbrev för fordonsförsäkringsanspråk*
* *Gör friskrivningstexten kursiv*
* *Ändra teckenstorleken för friskrivningstexten till 12*
* *Uppdatera teckenfärgen i ansvarsfriskrivningstexten till röd*
* *Uppdatera bakgrundsfärgen i textrutorna för sidhuvud och sidfot till ljusgrå*
* *Lägg till en ny ansvarsfriskrivningspanel med signatur- och bekräftelsefält*
* *Ta bort bekräftelsefältet*
* *Lägg till en tabell med betalningsinformation med tre kolumner*
* *Uppdatera justeringen av principnummerfältet till mitten*
* *Ändra radavståndet för villkorsavsnittet till 1.5*

Mer information om funktionerna i Interactive Communication Editor finns i [Dokumentation för interaktiv kommunikation](/help/forms/introduction-to-interactive-communication.md).

## Aktivering {#activation}

Om du vill aktivera Experience Production Agent för din organisation måste aktiveringen initieras via Adobe. Börja processen genom att nå ut via:

* E-post: `experience-production-agent@adobe.com`
* Eller kontakta ett Adobe-kontoteam.

För en effektiv introduktionsupplevelse kan du förbereda och lämna följande information:

Dela följande identifierare för **AEM as a Cloud Service**:

* Organisations-ID
* `product_id`
* `profile_id`

Din AEM-administratör kan hitta följande:

1. Navigerar till <https://adminconsole.adobe.com/>
1. Väljer **Adobe Experience Manager as a Cloud Service**
1. Välja lämplig AEM-instans i din miljö
1. Välja en profil med läs-/skrivbehörighet för relevant innehåll
1. Kopiera den fullständiga webbläsarens URL från den här sidan
1. Extraherar värdena `product_id` och `profile_id` från URL:en\
   (t.ex. en URL som `https://adminconsole.adobe.com/products/profiles/users` innehåller dessa parametrar).

För **Edge Delivery Document Authoring** kan du förse ditt Adobe-team med:

* Domäner för Edge Delivery Services
* Motsvarande GitHub-information:
   * Organisation (organisation)
   * Databas (repo)
   * Gren

Fullständig och korrekt information snabbar upp aktiveringsprocessen och säkerställer att Experience Production Agent etableras i tid.

