---
title: Hur lägger jag in e-signaturer i en blankett med hjälp av klottersignaturer?
description: Lär dig använda elektroniska signaturer i ett formulär med hjälp av klottersignaturer.
uuid: ffeba886-9b24-4ed1-95c0-e19356ff2f23
products: SG_EXPERIENCEMANAGER/FORMS
topic-tags: author
feature: Adaptive Forms, Foundation Components
exl-id: dc89ecb1-2d9e-4d1d-b85b-af90c550e7d8
role: User, Developer
source-git-commit: b5340c23f0a2496f0528530bdd072871f0d70d62
workflow-type: tm+mt
source-wordcount: '1318'
ht-degree: 0%

---

# E-signera ett formulär med hjälp av klottersignaturer{#apply-electronic-signatures-to-a-form-using-deprecated-scribble-signatures}

>[!NOTE]
>
> Adobe rekommenderar att du använder den moderna och utbyggbara datainhämtningen [Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) för [att skapa nya adaptiva Forms](/help/forms/creating-adaptive-form-core-components.md) eller [lägga till adaptiva Forms på AEM Sites-sidor](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). De här komponenterna utgör ett betydande framsteg när det gäller att skapa adaptiva Forms-filer, vilket ger imponerande användarupplevelser. I den här artikeln beskrivs det äldre sättet att skapa Adaptiv Forms med baskomponenter.

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/signing-forms-using-scribble.html) |
| AEM as a Cloud Service | Den här artikeln |


Du kan använda komponenten **Klottsignatur** för att rita (Klottra) signatur i ett anpassat formulär. <!-- The Signature step component displays a PDF version of the Adaptive Form. You require a Document of Record option enabled or form template based Adaptive Forms to use the Signature step component. -->

![Dialogrutan Klottertecken](assets/scribble-signature.png)

## Olika alternativ finns i signaturfönstret

* **A:** Klicka på ikonen **Målarpensel** för att rita din signatur på arbetsytan.
* **B:** Klicka på ikonen **Rensa** för att rensa signaturen på arbetsytan.
* **C:** Klicka på ikonen **Geolocation** för att lägga till geopositionering tillsammans med signaturen.
* **D:** Klicka på ikonen **Tangentbord** för att skriva ditt namn på arbetsytan.

När du har valt ikonen Klar ![aem_forms_save](assets/aem_forms_save.png) i fönstret Klottsignatur kan du inte redigera signaturen. Om du vill redigera signaturen måste du bortse från den aktuella signaturen och signera igen med alternativet Målningspensel/Tangentbord ovan.

Du kan välja ikonen **Konfigurera** ![konfigurera ikon](assets/configure.png) för att ställa in proportionen för arbetsytan med klottersignaturer. Konfigurera ikon
* När proportionerna för arbetsytan Klottra signatur är mindre än 1 läggs platsinformationen till längst ned på arbetsytan Klottra signatur.


* När proportionerna för arbetsytan Klottra signatur är större än 1 läggs geopositioneringsinformationen till till höger på arbetsytan Klottra signatur.


![scribble signature-bottom](assets/scribble-signature-aspectratio.PNG)



>[!NOTE]
>
>Signaturer sparas alltid i PNG-format.
>

## Konfigurera ett anpassat formulär för att använda skriptsignatur {#configure-an-adaptive-form-to-use-scribble-signature}

1. Öppna ett adaptivt formulär i redigeringsläge.
1. Dra och släpp komponenten **Klottsignatur** från komponentwebbläsaren till det adaptiva formuläret.
1. Välj ikonen **Konfigurera** ![konfigurera](assets/configure.png) . Egenskaper öppnas i webbläsaren och egenskaper för komponenten Skriptsignatur visas. [Konfigurera egenskaper för Klottsignatur](#properties-of-scribble-signature-component) enligt beskrivningen i nästa avsnitt.

   ![Klottersignatur](/help/forms/assets/scribblesig.png)

1. Välj ikonen Klar ![aem_forms_save](assets/aem_forms_save.png) om du vill spara ändringarna. Signaturen har konfigurerats.

## Konfigurera egenskaper för komponenten Klottsignatur

Med dialogrutan Konfigurera kan du enkelt anpassa din skriptsigneringskomponent för besökare.

### Fliken Grundläggande

![Fliken Grundläggande](/help/forms/assets/scribblesig-basic.png)

* **Namn** - Du kan enkelt identifiera en formulärkomponent med dess unika namn både i formuläret och i regelredigeraren, men namnet får inte innehålla blanksteg eller specialtecken.

* **Titel** - Med titeln kan du enkelt identifiera en komponent i ett formulär. Som standard visas titeln ovanpå komponenten. Om du inte lägger till en titel visas komponentens namn i stället för rubriktexten.

* **Tillåt RTF-text för rubrik** - Med den här funktionen kan användare formatera oformaterad text med funktioner som fet, kursiv, understruken text, olika teckensnitt, teckenstorlekar, färger och ytterligare alternativ för att förbättra visuell presentation och anpassning. Det ger större flexibilitet och kreativ kontroll när det gäller att få titlar att sticka ut i dokument, på webbplatser och i tillämpningar.\
  När du markerar kryssrutan för **Tillåt RTF-text för titel** visas formateringsalternativ som formaterar komponentens titel. Om du vill visa alla tillgängliga formateringsalternativ klickar du på fliken ![Helskärmsikon](/help/forms/assets/fullscreen-icon.png) .

  ![RTF-stöd](/help/forms/assets/richtext-support-title.png)

* **Dölj titel** - Välj alternativet för att dölja komponentens titel.
* **Obligatoriskt fält** - Välj alternativet att göra fältet obligatoriskt.
* **Obligatoriskt fältmeddelande** - **Obligatoriskt fältmeddelande** är ett anpassningsbart meddelande som visas för användare när de försöker skicka ett formulär utan att fylla i ett obligatoriskt fält.
* **Bindningsreferens för datamodell** - En bind-referens är en referens till ett dataelement som lagras i en extern datakälla och används i ett formulär. Med den binda referensen kan du binda data dynamiskt till formulärfält så att formuläret kan visa de senaste data från datakällan. En bindningsreferens kan till exempel användas för att visa en kunds namn och adress i ett formulär baserat på kundens ID som anges i formuläret. Bindningsreferensen kan också användas för att uppdatera datakällan med data som anges i formuläret. På så sätt kan AEM Forms skapa formulär som interagerar med externa datakällor, vilket ger en smidig användarupplevelse för att samla in och hantera data.
* **Dölj objekt** - Välj alternativet för att dölja komponenten från formuläret. Komponenten är fortfarande tillgänglig för andra syften, som att använda den för beräkningar i regelredigeraren. Detta är användbart när du behöver lagra information som inte behöver visas eller ändras direkt av användaren.
* **Inaktivera objekt** - Välj alternativet att inaktivera komponenten. Den inaktiverade komponenten är inte aktiv eller redigerbar av slutanvändaren. Användaren kan se fältets värde, men kan inte ändra det. Komponenten är fortfarande tillgänglig för andra syften, som att använda den för beräkningar i regelredigeraren.
* **Proportioner** - Proportionerna i en klottersignaturkomponent definierar det proportionella förhållandet mellan dess bredd och höjd.
* **Fältlayout** - Alternativet **Fältlayout** avgör hur formulärelement, inklusive etiketter (bildtexter) och felmeddelanden, placeras i förhållande till komponenten. Bildtexten **och felmeddelandet överst i widgeten** placerar fältets bildtext (etikett) och felmeddelanden ovanför komponenten. **Ärv från adaptiv formulärkonfiguration** använder de standardfältlayoutinställningar som anges i konfigurationen för adaptiv form.
* **CSS-klass** - Med **CSS-klassen** kan du använda egna format på en komponent genom att tilldela en eller flera CSS-klasser som definieras i formatmallen. Det möjliggör enhetlig anpassning av format och layout i hela det adaptiva formuläret.

### Hjälpinnehåll

![Fliken Hjälpinnehåll](/help/forms/assets/scribblesig-help.png)

* **Kort beskrivning** - En kort beskrivning är en kort textförklaring som ger ytterligare information eller förtydliganden om syftet med ett visst formulärfält. Det hjälper användaren att förstå vilken typ av data som ska anges i fältet och kan ge riktlinjer eller exempel som hjälper till att säkerställa att den angivna informationen är giltig och uppfyller de önskade kriterierna. Som standard är korta beskrivningar dolda. Aktivera alternativet **Visa alltid kort beskrivning** för att visa det under komponenten.

* **Visa alltid kort beskrivning** - Aktivera alternativet att visa den korta beskrivningen under komponenten.

* **Lång beskrivning** - Det hänvisar till ytterligare information eller vägledning som användaren får för att hjälpa dem att fylla i ett formulärfält korrekt. Det visas när användaren klickar på hjälpikonen (i) som finns bredvid komponenten. Den ger mer detaljerad information än etiketten eller platshållartexten för ett formulärfält och är utformad för att hjälpa användaren förstå kraven eller begränsningarna för fältet. Den kan också ge förslag eller exempel som gör det enklare och exaktare att fylla i formuläret.

### Fliken Tillgänglighet {#accessibility}

![Fliken Tillgänglighet](/help/forms/assets/scribblesig-acc.png)

På fliken **Hjälpmedel** anges värden för [ARIA-hjälpmedelsetiketter](https://www.w3.org/WAI/standards-guidelines/aria/) för komponenten. Det finns olika alternativ för att använda texten för skärmläsare:

* **Företräde för Reader på skärm** - Företräde för Reader på skärm avser extra text som är särskilt avsedd att läsas av hjälpmedelstekniker, t.ex. skärmläsare, som används av personer med nedsatt syn. Den här texten innehåller en ljudbeskrivning av formulärfältets syfte och kan innehålla information om fältets titel, beskrivning, namn och relevanta meddelanden (anpassad text). Skärmläsartexten ser till att formuläret är tillgängligt för alla användare, även användare med nedsatt syn, och ger dem en fullständig förståelse för formulärfältet och dess krav.

   * **Egen text**: Välj det här alternativet om du vill använda den anpassade texten för ARIA-hjälpmedelsetiketter. Om du väljer det här alternativet visas dialogrutan Egen text. Du kan lägga till relevant information i dialogrutan Egen text.
   * **Kort beskrivning**: Välj det här alternativet om du vill använda beskrivningen för ARIA-hjälpmedelsetiketter.
   * **Titel**: Välj det här alternativet om du vill använda titeln för ARIA-hjälpmedelsetiketter.
   * **Namn**: Välj det här alternativet om du vill använda namnet på ARIA-hjälpmedelsetiketter.
   * **Inget**: Välj det här alternativet om du inte vill lägga till för hjälpmedelsetiketter för ARIA.

<!--

 * **Element Name**: Specify name of the component.

    * **Title:** Specify unique title of the component.
    * **Template message:** Specify the message to be displayed while the signature PDF is being loaded. Adobe Sign services take some time to prepare and load signature PDF.
    * **Signing Service:** Select the **Scribble Signature** option.

    * **CSS Class**: Specify CSS class of the client library, if any. Adobe recommends using [themes](themes.md) and [in-line styles](inline-style-adaptive-forms.md) instead of CSS Class.
## Sign an Adaptive Form using Scribble Signature {#sign-an-adaptive-form-using-scribble-signature}

1. After you fill an Adaptive Form and reach the Signature Step page, the signature screen is displayed.

   ![Signature screen for EchoSign page](assets/esignscribblesign.jpg)

1. Click **[!UICONTROL Sign]**. The scribble sign dialog appears. Sign the form and click the Done ![aem_forms_save](assets/aem_forms_save.png) icon to save the signature.

   ![Scribble sign dialog](assets/scribblewidget.png)

1. Click complete to finish the signing process.

   ![Complete the signing process](assets/scribblecomplete.jpg)

The signatures are added to the form and the form control moves to the next panel. -->

## Se även {#see-also}

{{see-also}}