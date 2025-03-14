---
title: Introduktion till  [!DNL AEM Forms] as a Cloud Service
description: Upptäck AEM Forms för att ta fram företagsklara formulär, skapa arbetsflöden för företagsprocesser och använda dokumenttjänster för att ta fram och skydda dokument.
landing-page-description: Lär dig hur du använder formulär i AEM as a Cloud Service.
role: Admin, Developer, User
feature: Adaptive Forms, Release Information
exl-id: aa5ef10c-ba78-4a9d-8b2b-a72a7a306888
source-git-commit: f4b079837dee960401a16073293969954cad3e77
workflow-type: tm+mt
source-wordcount: '1165'
ht-degree: 3%

---


# AEM Forms as a Cloud Service - introduktion {#introduction}

<!-- Version Navigation -->
<div class="version-selector">
  <p><strong>Letar du efter dokumentation för en annan version?</strong></p>
  <ul>
    <li><a href="https://experienceleague.adobe.com/docs/experience-manager-65/forms/home.html">AEM 6.5 Forms Documentation</a></li>
    <li><strong>AEM Forms as a Cloud Service</strong> (aktuell)</li>
  </ul>
</div>

Adobe [!DNL Experience Manager Forms as a Cloud Service] erbjuder en lösning för plattformsspecifika tjänster (Platform as a Service) i molnet som gör det möjligt för företag att skapa, hantera, publicera och uppdatera komplexa digitala formulär samtidigt som inskickade data integreras med bakomliggande processer, affärsregler och data sparas i ett externt datalager.

Tjänsten är alltid aktuell, alltid tillgänglig och alltid tillgänglig. Organisationer kan använda [!DNL AEM Forms] as a Cloud Service och få alla dessa funktioner i molnet utan att det krävs någon lokal infrastruktur. Tjänsten befriar också organisationer från komplexa uppgraderingscykler eftersom den alltid är uppdaterad med de senaste funktionerna.

Adobe [!DNL Experience Manager Forms as a Cloud Service] är en kundcentrerad lösning som stöder varje steg i kundresan:

## Digitalisera och effektivisera registreringen och introduktionsupplevelsen

Du kan använda tjänsten för att skapa och distribuera interaktiva och engagerande digitala formulär. Ta till exempel en organisation som vill digitalisera sin kundregistreringsresa. De har flera datakällor med befintliga kunddata. De vill fylla i formulär i förväg, lägga till e-signera sina formulär och arkivera ifyllda formulär som PDF-filer. Dessutom har man flera tryckta blanketter (PDF forms) som man också vill konvertera till digitala blanketter.

Organisationen kan använda [!DNL AEM Forms] as a Cloud Service för att skapa digitala formulär, koppla formulär till befintliga datakällor, integrera formulär med [!DNL Adobe Sign] för att lägga till e-signaturer i formulär och generera DoR (Document of Record) för att arkivera skickade formulär som PDF-filer. Man kan också använda tjänsten för att konvertera sin befintliga PDF forms till digitala blanketter.

I stora företag skapas formulär ofta en gång och återanvänds genom att man kopierar till ett innehållshanteringssystem. Det kan vara en stor utmaning att hålla en stor databas med blanketter uppdaterad och lätt att hitta. AEM har en anpassningsbar Forms Portal som ser till att kunderna hittar och har tillgång till de formulär de behöver via både webben och mobila kanaler. Du kan anpassa utseendet, varumärkesprofileringen och logotyperna i Forms Portal så att de passar organisationens specifika behov.

## Leverera personaliserad kommunikation

En viktig komponent i en effektiv självbetjäningsdigital upplevelse är att förmedla skräddarsydd information som användarna kommer åt var de än är och på vilken enhet de vill. Personlig kommunikation i rätt tid kan förbättra både konverteringsgraden och användarnöjdheten.

Med AEM Forms kan man skapa övertygande personaliserade användarupplevelser genom att anpassa dokumentmallar och lägga in information från bakomliggande processer till mallarna. En uppsättning intuitiva API:er hjälper företag att ange regler som bestämmer när ett meddelande ska skapas baserat på en förfrågan eller med regelbundna intervall i grupper.


Personaliserade dokument som kvitton, kvitton, välkomstpaket och kontoutdrag kan enkelt genereras. Organisationer kan driva trafik till personaliserade webbportaler, vilket leder till registrering eller inköp av ytterligare tjänster.


## Automatisera arbetsflöden

Använd blankettbaserade arbetsflöden för att automatisera bearbetning och vidarebefordran av blankettdata till olika intressenter, t.ex. chefer och avdelningar, för granskning, godkännande eller vidare bearbetning. Dessa arbetsflöden hjälper er att minimera riskerna och upprätthålla regelefterlevnaden genom att säkerställa en konsekvent och kontrollerbar behandling av formulärdata, automatisera manuella uppgifter, tillhandahålla rollbaserad åtkomstkontroll och uppfylla myndigheternas krav.


## Optimera formulärprestanda

Tjänsten integreras med Adobe Analytics så att ni kan hämta in och spåra prestandamått för era publicerade formulär. Syftet med att analysera dessa värden är att fatta välgrundade beslut baserat på uppgifter om de ändringar som krävs för att göra formulär eller dokument mer användbara. Du kan använda Adobe Analytics för att upptäcka interaktionsmönster och problem som användare stöter på när de använder adaptiva formulär.


## Kom igång {#key-features}

AEM Forms as a Cloud Service har en omfattande uppsättning funktioner som är ordnade i följande kategorier:

### Skapa och redigera formulär {#form-creation}

Skapa engagerande, responsiva och datadrivna formulär med hjälp av olika redigeringsalternativ:

| Funktion | Beskrivning |
|---|---|
| Adaptiv Forms | Skapa och hantera interaktiva, dynamiska, responsiva, mobilvänliga och datadrivna formulär för webbplatser, appar och andra digitala kanaler och tryckkanaler: <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form.html"> Skapa ett anpassat formulär </a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/themes.html">Formatera ett anpassat formulär</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/create-or-add-an-adaptive-form-to-aem-sites-page.html?lang=en"> Lägg till ett anpassat formulär på en AEM Sites-sida </a></li></ul> |
| Edge Delivery Services för Forms | Skapa och leverera högpresterande blanketter med enastående användarupplevelse: <ul><li><a href="/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md">WYSIWYG Authoring with Universal Editor</a> - kraftfullt visuellt gränssnitt för att skapa formulär</li><li><a href="/help/edge/docs/forms/create-forms.md">Dokumentbaserad redigering</a> - skapa formulär med välbekanta verktyg som Microsoft Excel och Google Sheets</li><li>Avancerad regelredigerare för att skapa komplex formulärlogik</li><li>Uppnå Google Lightroom-bakgrundsmusik med optimerad inläsning av blanketter</li><li>Distribuera formulär snabbare med minimal utvecklingstid</li></ul> |
| Automatisk formulärkonverteringstjänst | Konvertera gamla PDF-baserade blanketter till adaptiva Forms som enkelt kan hanteras och distribueras online: <ul><li><a href="https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/configure-service.html">Konfigurera automatisk formulärkonverteringstjänst</a></li><li><a href="https://experienceleague.adobe.com/docs/aem-forms-automated-conversion-service/using/convert-existing-forms-to-adaptive-forms.html">Konvertera PDF forms till adaptiv Forms</a></li></ul> |

### Dokumentbearbetning och kommunikation {#document-processing}

Generera, sammanställ och leverera personaliserad kommunikation:

| Funktion | Beskrivning |
|---|---|
| Kommunikations-API:er | Automatisera framtagning, hantering och leverans av personaliserad, datadriven kommunikation med RESTful API:er on demand eller med regelbundna intervall: <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?#document-generation"> Generera anpassad kommunikation </a> </li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?#document-manipulation"> Sammanställa eller demontera PDF-dokument </a> </li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?#convert-to-and-validate-pdf%2Fa-compliant-documents">Skapa PDF/A-kompatibla dokument </a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html">Skydda dina dokument med DocAssurance-API:er</a></li></ul> |
| Dokument för registrering | Skapa och hantera register över inlämnade formulär för arkivering och regelefterlevnad: <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/generate-document-of-record-for-non-xfa-based-adaptive-forms.html"> Skapa en post av formuläret för långtidsarkivering</a></li><li>Utbyggbarhet på serversidan för anpassade funktioner</li><li>Dokumentation med funktioner för manipuleringssäkra arkiv</li></ul> |

### Automatisering av arbetsflöden och processer {#workflow}

Automatisera affärsprocesser och blankettrelaterade arbetsflöden:

| Funktion | Beskrivning |
|---|---|
| Formulärarbetsflöden | Automatisera affärsprocesser som innefattar blanketter och dokumenttjänster: <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-reviews-forms.html">Skicka ett formulär eller dokument för granskning</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html?#assign-task-step">Skapa ett arbetsflöde för avvisande av godkännande</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html#enabling-server-side-validation-br"> Skicka data till ett datalager eller ett arbetsflöde </a></li></ul> |
| E-signaturer | Integrera med Adobe Sign och Adobe Sign-lösningar för myndigheter för att enkelt skicka Forms och dokument till användare för e-signering: <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/use-adobe-sign/working-with-adobe-sign.html">E-signera ett anpassat formulär med Adobe Sign </a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html?#generate-document-of-record-step">Lägg till postdokument </a> eller <a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html?#sign-document-step"> e-signera </a> steg i ett affärsarbetsflöde</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/create-form-centric-workflows/aem-forms-workflow-step-reference.html?lang=en#sign-document-step">E-signera ett dokument med Adobe Sign och AEM-arbetsflöden</a></li></ul> |

### Dataintegrering och -analys {#data-integration}

Koppla formulären till datakällor och få insikt i formulärprestanda:

| Funktion | Beskrivning |
|---|---|
| Forms Analytics | Använd Adobe Analytics för att få värdefulla insikter om användarbeteende och -preferenser: <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/services/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation.html">Ansluta ett adaptivt formulär med Adobe Analytics</a></li></ul> |
| Adobe Integrations | Koppla ihop formulären med andra lösningar från Adobe: <ul><li><a href="/help/forms/submit-adaptive-form-to-workfront-fusion.md">Anslut till Adobe Workfront Fusion</a> och skicka data till Workfront-scenarier</li><li><a href="/help/forms/integrate-form-to-marketo-engage.md">Anslut till Adobe Marketo Engage</a> och <a href="/help/forms/submit-adaptive-form-to-marketo-engage.md">skicka data till Marketo</a></li></ul> |
| Microsoft Integrations | Koppla samman formulären med Microsoft tjänster: <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-msdynamics-salesforce.html?lang=en">Anslut till Microsoft® Dynamics 365</a></li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-azure-storage.html?lang=en">Anslut till Microsoft® Azure Blob Storage</a> och <a href="/help/forms/configure-submit-action-azure-blob-storage.md">skicka data till Azure Blob Storage</a></li><li><a href="/help/forms/connect-forms-to-sharepoint-document-library.md">Anslut till Microsoft® SharePoint Document Library</a> och <a href="/help/forms/configure-submit-action-sharepoint.md">skicka data till SharePoint</a></li><li><a href="/help/forms/configure-submit-action-onedrive.md">Anslut till Microsoft® OneDrive</a> och skicka data till OneDrive</li><li><a href="/help/forms/forms-microsoft-power-automate-integration.md">Anslut till Microsoft® Power Automate</a> och aktivera flöden när formulär skickas</li><li><a href="/help/forms/ms-dynamics-odata-configuration.md">Anslut till Microsoft® Dynamics OData</a></li></ul> |
| Andra datakällor | Anslut till ytterligare datakällor och slutpunkter: <ul><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/configure-data-sources.html?lang=en">Anslut till en RDBMS- eller återställningsslutpunkt</a></li><li><a href="/help/forms/aem-forms-salesforce-integration.md">Anslut till Salesforce</a> och skicka data till Salesforce</li><li><a href="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-submit-actions-and-metadata-submission/configuring-submit-actions.html#submit-to-rest-endpoint">Skicka till REST-slutpunkt</a></li></ul> |

>[!MORELIKETHIS]
>
>* [Skapa ett anpassat formulär](/help/forms/creating-adaptive-form-core-components.md)
>* [Gå med i en Cloud Service-miljö](/help/forms/setup-forms-cloud-service.md)
>* [Konfigurera en lokal utvecklingsmiljö](/help/forms/setup-local-development-environment.md)
>* [Migrera från AEM 6.5 Forms till Cloud Service](/help/forms/migrate-to-forms-as-a-cloud-service.md)
