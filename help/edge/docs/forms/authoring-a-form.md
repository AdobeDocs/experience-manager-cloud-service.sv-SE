---
Title: Authoring a Form
Description: This article provides information on various form authoring platforms, including the Universal Editor, document-based authoring, and Adaptive Forms editors (Core Components and Foundation Components).
Keywords: Universal Editor for WYSIWYG authoring, document-based authoring, Adaptive Forms editors, Adaptive Forms editors for Core Components authoring, Adaptive Forms editors for Foundation Components authoring
feature: Edge Delivery Services
Role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: bdc0e51a8b16df432f1f1aeabed11135fb8c8e0c
workflow-type: tm+mt
source-wordcount: '877'
ht-degree: 0%

---


# Skapa ett formulär

Adobe Experience Manager erbjuder och stöder flera redigerare för att skapa ett formulär. Du kan använda
* Universal Editor (för WYSIWYG)
* Microsoft Excel- eller Google-blad (kallas dokumentbaserad redigering)
* Adaptiva Forms-redigerare (för Core Components eller grundläggande komponentbaserad redigering)

**[bild som ska läggas till]**

## Universal Editor (för WYSIWYG)

Universell redigerare är en mångsidig visuell redigerare som har en funktion för vad du ser och vad du får (WYSIWYG) som ger en intuitiv upplevelse när du skapar formulär. Vi rekommenderar att du använder den universella redigeraren när du skapar nya formulär, eftersom den har en modern, användarvänlig design och ett bekvämt dra-och-släpp-gränssnitt.

Om du vill skapa formulär med den universella redigeraren används de Edge Delivery Services som finns i AEM. De här formulären ärver utseendet och känslan från konfigurationerna i GitHub-databasen för Edge Delivery Services. [En anslutning mellan din AEM och GitHub-databasen ](/help/edge/docs/forms/publishing-forms.md) för Edge Delivery Services har upprättats för att aktivera publicering av dessa formulär på Edge Delivery Services.

Detaljerade anvisningar om hur du skapar med den universella redigeraren finns i artikeln [Skapa innehåll med den universella redigeraren](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/sites/authoring/universal-editor/authoring).

## Microsoft Excel- eller Google-blad (kallas dokumentbaserad redigering)

Du kan skapa formulären med dokumentbaserad redigering med Microsoft Excel- eller Google Sheets-filer, vilket gör att du kan utnyttja de robusta ekosystemen och API:erna i Google Sheets, Microsoft Excel och Microsoft SharePoint. Det här arbetssättet är särskilt användbart när du skapar enkla formulär utan avancerade överföringstjänster.

Om du vill börja skapa ett formulär med Microsoft Excel eller Google Sheets, [skapar du ett AEM med AEM Forms-standardmall](/help/edge/docs/forms/tutorial.md#create-a-new-aem-project-pre-configured-with-adaptive-forms-block) och klonar motsvarande GitHub-databas på den lokala datorn. AEM Forms Edge Delivery har en funktion som kallas Adaptive Forms Block, som förenklar processen att skapa formulär för datainhämtning och datalagring. Mer information om hur du skapar och publicerar formulär med det adaptiva Forms-blocket på Edge Delivery Services finns i [Skapa ett formulär](/help/edge/docs/forms/create-forms.md).

## Adaptiva Forms-redigerare (för Core Components eller grundläggande komponentbaserad redigering)

Ni kan skapa formulär som är engagerande, responsiva och dynamiska. Med redigeraren för adaptiva formulär kan du snabbt skapa adaptiva Forms med en användarvänlig guide. Formulärguiden har enkel tabbnavigering, vilket gör att du kan välja förkonfigurerade mallar för grundkomponenter eller kärnkomponenter, teman, datamodeller och överföringsalternativ för att skapa ett formulär på ett effektivt sätt.

Med [redigeringsformulär med kärnkomponenter](/help/forms/creating-adaptive-form-core-components.md) kan du utnyttja standardiserade komponenter för datainhämtning som kan anpassas, vilket minskar utvecklingstiden och minskar underhållskostnaderna för digitala registreringsupplevelser. Dessa formulär kan publiceras med Adaptive Forms Block på Edge Delivery Services eller via AEM Publish-instans.

[När du redigerar formulär med Foundation Components](/help/forms/create-an-adaptive-form.md) används klassiska datainhämtningskomponenter. Dessa formulär kan bara publiceras med AEM Publish-instans.

Du kan också publicera formulär som skapats med adaptiva Forms-redigerare på Edge Delivery Services genom att upprätta en [anslutning mellan din AEM och Edge Delivery Servicens GitHub-databas](/help/edge/docs/forms/publishing-forms.md).

## Hur väljer man mellan olika typer av formulärutveckling?

Följande tabell visar funktionerna och användningsexemplen för varje redigeringsprogram, som hjälper dig att välja rätt baserat på dina krav och behov av att skicka in formulär.

| **Redigerare för formulärredigering** | **Nyckelmetod** | **Funktioner** | **Publiceringsmetod** | **Användningsexempel** |
|--------|-----------|-------|-------|------------------------------------------------|
| **Dokumentbaserad redigering** | Utnyttja välbekanta verktyg som Google Docs och Microsoft Office för att skapa blanketter. | Forms är utformat med hjälp av kalkylblad, med data som skickas direkt till Google eller Microsoft Excel-blad. </br> </br> Dessa formulär är snabbare att skapa och distribuera. Du behöver inte ha någon tidigare kunskap om AEM för att kunna utveckla anpassade komponenter och format för dessa formulär. | De här formulären publiceras på Edge Delivery Services och har mycket höga Google Lighthuse-poäng. </br> </br> Det höga poängtalet ger snabbare återgivning och bättre SEO. | De här formulären är idealiska för att snabbt skapa prototyper eller för att skapa grundläggande formulär där avancerade inlämningstjänster inte behövs. </br> </br> De här är väl lämpade för enkäter, registrering eller feedbackformulär som kräver datalagring i kalkylblad. Dessa formulär publiceras på Edge Delivery tjänster |
| **Universell redigerare** </br> </br> Om du skapar ett nytt formulär använder du Universell redigerare för att skapa formulär. | Har ett WYSIWYG-gränssnitt för intuitiv blankettkonstruktion. | Forms är utformat med ett intuitivt dra och släpp-gränssnitt. </br> </br> De här formulären lånar ut utseende och känsla från den konfigurerade Edge Delivery Servicens GitHub-databas för motsvarande formulär. | De här formulären publiceras på Edge Delivery Services och har mycket höga Google Lighthuse-poäng. </br> </br> Det höga poängtalet ger snabbare återgivning och bättre SEO. | De här formulären är idealiska för att skapa formulär för webbplatser och sidor i Edge Delivery Service. Dessa formulärscenarier omfattar komplexa formulär, komplexa arbetsflöden, anpassade åtgärder eller integrering med externa system |
| **Adaptiva Forms-redigerare** | En guidestyrd metod för att snabbt börja skapa formulär med hjälp av mallar, format och fördefinierade fält. | Använd dessa redigerare för att skapa grundkomponentbaserade formulär eller grundkomponentbaserade formulär. | Dessa formulär kan publiceras på Edge Delivery Services eller via AEM Publish-instanser. | Använd dessa redigerare för att skapa grundkomponentbaserade formulär eller grundkomponentbaserade formulär. Perfekt för scenarier som omfattar komplexa formulär, komplexa arbetsflöden, anpassade åtgärder eller integrering med externa system. |


>[!NOTE]
>
>
> Om du upptäcker funktioner som saknas i den universella redigeraren och som tidigare fanns i den adaptiva Forms-redigeraren kan du begära dem via e-post till mailto:aem-forms-ea@adobe.com med din officiella e-postadress.

## Relaterad artikel

* [Dokumentbaserad redigering med Microsoft Excel eller Google Sheets](/help/edge/docs/forms/create-forms.md)
* [Universell redigerare för WYSIWYG-redigering](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/wysiwyg-authoring/authoring)
* [Skapa ett adaptivt formulär (grundkomponenter)](/help/forms/creating-adaptive-form.md)
* [Skapa en adaptiv form (kärnkomponenter)](/help/forms/create-an-adaptive-form.md)

## Se även

{{see-more-forms-eds}}