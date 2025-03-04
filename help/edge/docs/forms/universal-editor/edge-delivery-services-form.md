---
Title: How Edge Delivery Services Forms work?
Description: This article provides information on how Edge Delivery Services Forms work. It also provides information on various form authoring platforms, including the Universal Editor and document-based authoring.
Keywords: Universal Editor for WYSIWYG authoring, document-based authoring, Working of Edge Delivery Services Forms, How Edge Delivery Services Forms work?
feature: Edge Delivery Services
Role: User, Developer
hide: true
hidefromtoc: true
exl-id: db58ce85-139a-4cc1-8e18-73da76357299
source-git-commit: bb01a76ae2bfd78ae648e91545f34f20fabebd10
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 0%

---


# Edge Delivery Services Forms

Adobe Edge Delivery Services Forms förändrar hur blanketterna skapas, används och bearbetas. Genom att utnyttja Edge Delivery Services kan man skapa snabba, säkra och lättillgängliga digitala blanketter som förbättrar användarupplevelsen och effektiviteten i verksamheten i en snabb utvecklingsmiljö. Med Edge Delivery Services Forms kan du öka konverteringsgraden, minska kostnaderna och snabba upp innehållsleveransen.

## Fördelar med Edge Delivery Services Forms

* **Skapa formulär snabbare**: Bygg högpresterande formulär med perfekt Lightroom Score och övervaka kontinuerligt deras verkliga prestanda med hjälp av Real User Monitoring (RUM).

* **Effektiv redigeringsprocess**: Hantera enkelt innehåll från flera källor för större flexibilitet. Nu kan du skapa formulär både med WYSIWYG och dokumentbaserad redigering, vilket möjliggör smidig integrering av olika innehållsformat.

* **Enkel användning för icke-tekniska användare**: Edge Delivery Services ger icke-programmerare möjlighet att enkelt hantera och publicera formulär utan att behöva ha omfattande programmeringskunskaper.

* **Förbättrad användarupplevelse**: Säkerställ snabba inläsningstider och smidiga interaktioner, så att användarna får minimal väntetid och en intuitiv funktion för ifyllnad av formulär.

* **Serverlös körning**: Edge Delivery Services aktiverar serverlös körning av formulärlogik. Detta omfattar följande:

   * **Validering på klientsidan**: Validering av formulärfält sker på klientsidan, vilket minskar fördröjningar vid returnerad överföring.

   * **Förifyll &amp; Personalization**: Förifyll formulärdata hanteras på klientsidan för en smidig användarupplevelse.

   * **Bearbetning av inskickning**: Formulärinskickat material valideras och vidarebefordras säkert utan central server

## Hur fungerar Edge Delivery Services Forms?

Användare kan skapa Edge Delivery Services Forms med dokumentbaserade redigeringsverktyg som Google Drive, SharePoint eller Universal Editor (WYSIWYG-redigering) och samtidigt utnyttja de grundläggande formaten, beteendena och komponenterna som finns i GitHub-databasen. När Edge Delivery Services Forms har skrivits kan det skicka data till alla plattformar med Forms Submission Service.

![Så här fungerar Edge Delivery Services Forms](/help/edge/docs/forms/assets/eds-forms-working.png)

### Viktiga komponenter i Edge Delivery Services Forms

De viktigaste komponenterna i Edge Delivery Services Forms är:

* **GitHub-databas**: GitHub-databasen fungerar som en standardmall för att skapa Edge Delivery Services Forms. Blanketterna utnyttjar de grundläggande formaten och funktionerna från databasen och gör det möjligt att lägga till anpassningar och anpassade komponenter i Edge Delivery Services Forms.

* **Formulärredigering**: Edge Delivery Services Forms stöder två typer av redigering: WYSIWYG och dokumentbaserad redigering. Med dokumentbaserad redigering kan man skapa blanketter med välbekanta verktyg som Google Docs och Microsoft Office. Med WYSIWYG kan man utforma blanketter visuellt med den universella redigeraren så att man enkelt kan skapa och hantera blanketter utan tekniska kunskaper. Universell redigerare ger en intuitiv upplevelse när du skapar formulär och ger tillgång till en mängd olika formulärfunktioner.

* **Forms överföringstjänst**: Med Forms överföringstjänst kan du lagra data från formulär på vilken plattform som helst, t.ex. OneDrive, SharePoint eller Google Sheets, vilket gör det enkelt att komma åt och hantera formulärdata i det system du föredrar.

## Skapa ett formulär

Adobe Experience Manager erbjuder och stöder flera redigerare för att skapa ett formulär. Du kan använda
* [Universal Editor (för WYSIWYG)](#universal-editor-for-wysiwyg-authoring)
* [Microsoft Excel- eller Google-blad (kallas dokumentbaserad redigering)](#microsoft-excel-or-google-sheets-known-as-document-based-authoring)

### Universal Editor (för WYSIWYG)

Universell redigerare är en mångsidig visuell redigerare som har en funktion för vad du ser och vad du får (WYSIWYG) som ger en intuitiv upplevelse när du skapar formulär. Vi rekommenderar att du använder den universella redigeraren när du skapar nya formulär, eftersom den har en modern, användarvänlig design och ett bekvämt dra-och-släpp-gränssnitt.

För att skapa formulär med Universal Editor används Edge Delivery Services-mallar som finns i AEM-miljön. De här formulären har samma utseende och känsla som konfigurationerna i Edge Delivery Services GitHub-databasen. [En anslutning mellan din AEM-miljö och Edge Delivery Services GitHub-databasen ](/help/edge/docs/forms/universal-editor/getting-started-universal-editor.md) har upprättats för att aktivera publicering av dessa formulär på Edge Delivery Services.

Detaljerade anvisningar om hur du skapar med den universella redigeraren finns i artikeln [Skapa innehåll med den universella redigeraren](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/authoring/universal-editor/authoring).

### Microsoft Excel- eller Google-blad (kallas dokumentbaserad redigering)

Du kan skapa formulären med dokumentbaserad redigering med Microsoft Excel- eller Google Sheets-filer, vilket gör att du kan utnyttja de robusta ekosystemen och API:erna i Google Sheets, Microsoft Excel och Microsoft SharePoint. Det här arbetssättet är särskilt användbart när du skapar enkla formulär utan avancerade överföringstjänster.

Om du vill börja skapa ett formulär med Microsoft Excel eller Google Sheets [skapar du ett AEM-projekt med AEM Forms-mallen](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) och klonar motsvarande GitHub-databas på den lokala datorn. AEM Forms Edge Delivery har en funktion som kallas Adaptive Forms Block, som förenklar processen att skapa formulär för datainhämtning och datalagring. Mer information om hur du skapar och publicerar formulär med det adaptiva Forms-blocket i Edge Delivery Services finns i [Skapa ett formulär](/help/edge/docs/forms/create-forms.md).

<!--
## Adaptive Forms editors (for Core Components or foundation components based authoring)

You can author forms that are engaging, responsive and dynamic. The Adaptive Form editor provides a user-friendly wizard that allows you to quickly create Adaptive Forms. The form wizard features easy tab navigation, enabling you to select pre-configured templates for foundation or core components, themes, data models, and submission options to create a form efficiently. 

[Authoring forms with Core Components](/help/forms/creating-adaptive-form-core-components.md) allows you to leverage standardized data capture components that can be customized, reducing development time and lowering maintenance costs for digital enrollment experiences. These forms can be published using the Adaptive Forms Block on Edge Delivery Services or through the AEM Publish instance. 

[Authoring forms with Foundation Components](/help/forms/create-an-adaptive-form.md) uses classic data capture components. These forms can only be published using the AEM Publish instance. 

You can also publish forms created using Adaptive Forms Editors on Edge Delivery Services by establishing [connection between your AEM environment and the Edge Delivery Services GitHub repository](/help/edge/docs/forms/publishing-forms.md).


| **Adaptive Forms editors** | Provides a wizard-driven approach to quickly start forms authoring using templates, styling, and predefined fields. | Use these editors to create Core Components based forms or Foundation Components based forms. | These forms can be published on Edge Delivery Services or via AEM Publish instances.  | Use these editors to create Core Components based forms or Foundation Components based forms. Ideal for scenarios involving complex forms, complex workflows, custom actions, or integrations with external systems. |  



## Types of Publishing for Edge Delivery Services Forms

You can publish Edge Delivery Services Forms on one of the following:

* **Edge Delivery Services Form Submission**: Edge Delivery Services Form Submissions ensure that form interactions, including submission and data processing, are handled efficiently and securely. This enables a faster and more reliable user experience, particularly during high traffic periods. By processing form submissions at the edge, Edge Delivery Services minimizes the reliance on a centralized server.

* **AEM Publish instance**: The AEM Forms server offers a publish instance that manages the forms and related assets available to end users.
-->

### Hur väljer man mellan olika typer av formulärutveckling?

Följande tabell visar funktionerna och användningsexemplen för varje redigeringsprogram, som hjälper dig att välja rätt baserat på dina krav och behov av att skicka in formulär.

| **Redigerare för formulärredigering** | **Nyckelmetod** | **Funktioner** | **Publiceringsmetod** | **Användningsexempel** |
|--------|-----------|-------|-------|------------------------------------------------|
| **Dokumentbaserad redigering** | Utnyttja välbekanta verktyg som Google Docs och Microsoft Office för att skapa blanketter. | Forms är utformat med hjälp av kalkylblad, med data som skickas direkt till Google eller Microsoft Excel-blad. </br> </br> Dessa formulär är snabbare att skapa och distribuera. Du behöver inte ha någon tidigare kunskap om AEM för att utveckla anpassade komponenter och format för dessa formulär. | De här formulären publiceras på Edge Delivery Services och har mycket höga Google Lighthuse-poäng. </br> </br> Det höga poängtalet ger snabbare återgivning och bättre SEO. | De här formulären är idealiska för att snabbt skapa prototyper eller för att skapa grundläggande formulär där avancerade inlämningstjänster inte behövs. </br> </br> De här är väl lämpade för enkäter, registrering eller feedbackformulär som kräver datalagring i kalkylblad. Dessa formulär publiceras på Edge Delivery tjänster |
| **Universell redigerare** </br> </br> Om du skapar ett nytt formulär använder du Universell redigerare för att skapa formulär. | Har ett WYSIWYG-gränssnitt för intuitiv blankettkonstruktion. | Forms är utformat med ett intuitivt dra och släpp-gränssnitt. </br> </br> De här formulären lånar ut utseende och känsla från den konfigurerade Edge Delivery Services GitHub-databasen för motsvarande formulär. | De här formulären publiceras på Edge Delivery Services och har mycket höga Google Lighthuse-poäng. </br> </br> Det höga poängtalet ger snabbare återgivning och bättre SEO. | De här formulären är idealiska för att skapa formulär för webbplatser och sidor i Edge Delivery Service. Dessa formulärscenarier omfattar komplexa formulär, komplexa arbetsflöden, anpassade åtgärder eller integrering med externa system |

>[!NOTE]
>
>
> Om du upptäcker funktioner som saknas i den universella redigeraren och som tidigare fanns i den adaptiva Forms-redigeraren kan du begära dem via e-post till mailto:aem-forms-ea@adobe.com med din officiella e-postadress.

## Se även

{{see-more-forms-eds}}
