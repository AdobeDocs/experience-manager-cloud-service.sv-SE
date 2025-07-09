---
title: Konfigurera Skicka-åtgärder för AEM Forms med Edge Delivery Services
description: Lär dig hur du konfigurerar skicka-åtgärder i AEM Forms med Edge Delivery Services. Välj mellan Forms Submission Service och AEM Publish Submit Action för att hantera formulärdata på ett säkert och effektivt sätt.
feature: Edge Delivery Services
role: Admin, Architect, Developer
source-git-commit: bca160763fdd1e96f1350ac74eb76ff7c26ac00b
workflow-type: tm+mt
source-wordcount: '2166'
ht-degree: 0%

---


# Konfigurera formuläröverföringar: Var finns dina data?

När en användare har klickat på **skicka** i ditt formulär måste du tala om för Edge Delivery Services vad du ska göra med dessa data. Du har två huvudalternativ:

## Metod 1: Använda AEM Forms Submission Service (förenklad)

Den här tjänsten är idealisk för vanliga, enkla åtgärder som att skicka data till ett kalkylblad eller ett e-postmeddelande.

**Vad är det och hur kan det hjälpa dig?**

[Forms Submission Service](/help/forms/forms-submission-service.md) är en slutpunkt som hanteras av Adobe. När formuläret skickar data till det tar tjänsten över och utför en förkonfigurerad åtgärd. Den är lätt att installera. Du kan konfigurera: Skicka till kalkylblad eller e-post:

* **Skicka till kalkylblad:** Lägg automatiskt till skickade formulärdata som en ny rad i en Google-mall eller en Microsoft Excel-fil (som lagras på OneDrive eller SharePoint).
* **Skicka e-post:** Skicka ett e-postmeddelande som innehåller formulärdata till en eller flera e-postadresser som du anger.

#### Viktigt: Installationskrav

* **Åtkomst till kalkylblad:** Adobe-tjänstkontot (ofta `forms@adobe.com`) behöver **redigeringsbehörighet** för att kunna skicka data till ett Google-blad eller en Excel-fil på OneDrive/SharePoint.
* **Tidig åtkomst:** Vissa funktioner i den här tjänsten, särskilt för kalkylblad, kan ingå i ett program för tidig åtkomst. Du kan behöva begära åtkomst genom att skicka ett e-postmeddelande till `aem-forms-ea@adobe.com` eller fylla i ett specifikt Adobe-formulär med projektinformationen. Kontrollera alltid den senaste Adobe-dokumentationen.

**Forms Submission Service Flödesschema**
<!--
```mermaid
    graph TD
    UserForm[User Submits Form on Your EDS Site] >|Data Sent| FormSubmissionService[AEM Forms Submission Service]
    FormSubmissionService -- "If configured for Google Sheets" > GoogleSheet[Data written to Google Sheet]
    FormSubmissionService -- "If configured for Excel (OneDrive or SharePoint)" > ExcelSheet[Data written to Excel]
    FormSubmissionService -- "If configured for Email" > Email[Email with data is sent]

    style UserForm fill:#ccf,stroke:#333
    style FormSubmissionService fill:#fca,stroke:#333
    style GoogleSheet fill:#90ee90,stroke:#333
    style ExcelSheet fill:#90ee90,stroke:#333
    style Email fill:#add8e6,stroke:#333
```-->
![Forms Submission](/help/forms/assets/eds-fss.png)

I det här flödesdiagrammet visas hur Forms överföringstjänst tar emot skickade data och skickar dem till ett konfigurerat kalkylblad eller ett konfigurerat e-postmeddelande.

## Metod 2: Skicka till din AEM Publish Instance (avancerat)

För mer komplexa behov kan [formulär (särskilt sådana som har skapats med den universella redigeraren) skicka data direkt till din AEM as a Cloud Service Publish-instans](/help/forms/configure-submit-actions-core-components.md). Detta frigör AEM fulla backend-kraft.

**När måste du skicka till AEM Publish?**

* Används för att utlösa anpassade AEM-arbetsflöden efter inskickning.
* Använda AEM Form Data Model (FDM) för att integrera med databaser eller andra affärssystem.
* För att få kontakt med tredjepartstjänster som Marketo, Microsoft Power Automate eller Adobe Workfront Fusion.
* Att lagra data på specifika platser som Azure Blob Storage eller SharePoint-listor/dokumentbibliotek (inte bara enkla kalkylblad).
* När du har komplex validering på serversidan eller databearbetningslogik i AEM.

**Tillgängliga överföringsåtgärder (AEM Publish Submissions)**

* [Skicka till en REST-slutpunkt](/help/forms/configure-submit-action-restpoint.md)
* [Skicka e-post (med AEM e-posttjänster)](/help/forms/configure-submit-action-send-email.md)
* [Skicka med hjälp av formulärdatamodell (FDM)](/help/forms/configure-data-sources.md)
* [Starta ett AEM-arbetsflöde](/help/forms/aem-forms-workflow-step-reference.md)
* [Skicka till SharePoint (som listobjekt eller dokument)](/help/forms/configure-submit-action-sharepoint.md)
* [Skicka till OneDrive (som dokument)](/help/forms/configure-submit-action-onedrive.md)
* [Skicka till Azure Blob Storage](/help/forms/configure-submit-action-azure-blob-storage.md)
* [Skicka till Microsoft Power Automate](/help/forms/forms-microsoft-power-automate-integration.md)
* [Skicka till Adobe Workfront Fusion](/help/forms/submit-adaptive-form-to-workfront-fusion.md)
* [Skicka till Adobe Marketo Engage](/help/forms/submit-adaptive-form-to-marketo-engage.md)

>[!NOTE]
>
> Även om du har Google Sheet/Excel från AEM Publish som mål innehåller det andra konfigurationssteg än Forms Submission Service.

**AEM Publicera inskickningsflödesschema**

<!--```mermaid
    graph TD
    UEForm[User Submits Universal Editor Form on EDS Site] >|Data sent to AEM Publish URL - example: /adobe/forms/af/submit/...| AEMPublish[AEM Publish Instance]
    AEMPublish -- Configured to run AEM Workflow > AEMWorkflow[AEM Workflow is Triggered]
    AEMPublish -- Configured to use Form Data Model > FDM[FDM updates Backend System or Database]
    AEMPublish -- Configured for Marketo > Marketo[Data sent to Marketo Engage]
    AEMPublish -- Other configured actions... > OtherIntegrations[...]

    style UEForm fill:#ccf,stroke:#333
    style AEMPublish fill:#fca,stroke:#333
    style AEMWorkflow fill:#add8e6,stroke:#333
    style FDM fill:#add8e6,stroke:#333
    style Marketo fill:#add8e6,stroke:#333
```-->

![AEM Publicera inskickningsflödesschema](/help/forms/assets/eds-aem-publish.png)
I det här flödesdiagrammet visas ett formulär som skickas till AEM Publish, som sedan hanterar komplexa backend-uppgifter.

### Forms Submission Service vs. AEM Publish Submissions

| Funktion | Forms Submission Service | AEM Publish Submissions |
| :- | :- | :-- |
| **Bäst för** | Enkel datainhämtning till kalkylblad, e-postmeddelanden | Komplexa arbetsflöden, företagsintegrering, anpassad logik |
| **Formulärredigering** | Bra för dokumentbaserade formulär; OK för enkla UE-formulär | Bäst för universella redigeringsformulär |
| **Inställningsåtgärd** | Låg (ofta enkel konfiguration) | Högre (kräver AEM Publish, Dispatcher, OSGi, CDN-installation) |
| **Backend System** | Adobe värdtjänst | Din AEM as a Cloud Service Publish-instans |
| **Flexibilitet** | Begränsat till blad/e-post | Mycket flexibelt, fullt utbud av AEM Forms-åtgärder |
| **Exempel** | Kontakta blankettdata på ett Google-blad | Låneansökan som utlöser ett arbetsflöde för godkännande av AEM |

## Så här bäddar du in Forms på olika webbplatser eller sidor

Ibland kanske du vill visa ett formulär som har skapats och hanterats på ett och samma ställe (t.ex. en central&quot;formulärwebbplats&quot;) på en annan webbsida eller webbplats.

### Varför skulle du bädda in ett formulär?

* Du har ett standardformulär för&quot;Kontakta oss&quot; som skapats med en universell redigerare som måste visas på flera landningssidor som byggts med dokumentbaserad redigering.
* Huvudinnehållet på webbplatsen är i Document Authoring (DA) och du måste ha ett specialanpassat formulär.
* Du vill återanvända ett enda, välunderhållet formulär i flera olika EDS-projekt.

### Hur formulärinbäddning fungerar tekniskt

Sidan där du vill att formuläret ska visas (vi kallar den &quot;värdsida&quot;) kommer att innehålla kod (vanligtvis ett särskilt block eller skript). När en användare besöker värdsidan skickar koden en begäran till webbadressen där det faktiska formuläret finns (vi kallar det&quot;Form Source&quot;). Formuläret Source skickar sedan tillbaka sin HTML som värdsidan injicerar och visar.

**Inbäddad formulärarkitektur**

<!--```mermaid
   graph LR
    User[User] >|Visits| HostPage[Host Page - for example: your-site.com/landing-page]
    HostPage >|Contains code to embed form| FetchForm{Host Page Requests Form HTML}
    FetchForm >|HTTP GET request to the form URL| FormSource[Form Source - for example: forms-repo.hlx.page/my-form]
    FormSource >|Returns form HTML| FetchForm
    FetchForm >|Injects form HTML into page| HostPage
    HostPage >|Displays full page with embedded form| User

    subgraph Submission ["Form Submission from Host Page"]
        HostPage_Form[Embedded form on the host page] >|User submits| TargetEndpoint[Submission endpoint - FSS or AEM Publish]
    end

    style HostPage fill:#e6f3ff,stroke:#333
    style FormSource fill:#ffe6e6,stroke:#333
    style FetchForm fill:#fff2cc,stroke:#333
    style Submission fill:#f0fff0,stroke:#333
```-->
![Inbäddad formulärarkitektur](/help/forms/assets/eds-embedded-form.png)
I det här diagrammet visas hur värdsidan hämtar HTML från Source och visar det. Vid överföring används det ursprungliga formulärets konfigurerade slutpunkt.

## Konfigurera CORS för inbäddad Forms

[CORS (Cross-Origin Resource Sharing)](https://experienceleague.adobe.com/en/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing) är en säkerhetsfunktion i webbläsaren. Om din värdsida (t.ex. `site-a.com`) försöker hämta ett formulär från en annan domän (t.ex. `forms-site-b.com`) blockerar webbläsaren det såvida inte `forms-site-b.com` uttryckligen tillåter det via CORS-rubriker.

Utan korrekta CORS-huvuden på **Form Source-servern** kan webbläsaren inte läsa in formuläret från värdsidan och det inbäddade formuläret visas inte.

### Hur konfigurerar jag CORS på den webbplats där ditt formulär finns?

Du måste konfigurera servern som är värd för **Form Source** så att specifika HTTP-huvuden skickas i svaret. Den exakta metoden beror på din EDS-konfiguration (t.ex. för Franklin-projekt görs detta ofta i en `helix-config.yaml` eller liknande konfigurationsfil i din GitHub-databas som styr CDN-beteendet eller edge worker logic).
Viktiga rubriker som ska läggas till i Source svar för formulär:

* `Access-Control-Allow-Origin: <URL_of_Host_Page>` (till exempel `https://your-site.com`). Du kan använda `*` för testning, men för produktion anger du de exakta domänerna.
* `Access-Control-Allow-Methods: GET, OPTIONS` (Du kan behöva `POST` om själva formuläröverföringen också är korsorigo, men vanligtvis skickas överföringar till en separat, ofta samma ursprung eller specifikt konfigurerad slutpunkt).
* `Access-Control-Allow-Headers: Content-Type` (och andra anpassade rubriker som formulärhämtningen kan använda).

**Exempel (konceptuellt för en config-fil):**

```yaml
        # In the configuration for the site HOSTING THE FORM (Form Source)
        headers:
          # Apply to paths where your forms are served, e.g., /forms/**
          - path: /forms/**
            custom:
              Access-Control-Allow-Origin: https://host-page-domain.com
              Access-Control-Allow-Methods: GET, OPTIONS
```

## Ytterligare överväganden: CDN och flera kodebaser (Helix 4)

* **CDN-regler:** CDN-nätverket kan innehålla sätt att proxybegäranden. En begäran till `host-page.com/embedded-form` kan till exempel vidarebefordras internt av CDN för att hämta innehåll från `form-source.com/actual-form`, vilket gör att det ser likadant ut i webbläsaren. Detta kan vara komplicerat att konfigurera.
* **Flera kodbaser (Helix 4):** Om din värdsida och ditt formulär-Source finns i olika GitHub-databaser (gemensamma för Helix 4-inställningar) kontrollerar du att alla JavaScript &quot;Formulärblock&quot; som behövs för att återge eller hantera formuläret finns tillgängliga i värdsidans kodbas, eller att det formulär-HTML som hämtas från Form Source är fristående med alla nödvändiga JavaScript. I originaldokumenten står det att för&quot;helix4 med olika kodebaser måste du lägga till Form-blocket på båda kodebaserna.&quot;

### Vanliga arkitekturinställningar och konfigurationssteg

Här är några vanliga sätt som du kan ställa in formulären på och kombinera redigeringsmetoder med överföringsstrategier, tillsammans med viktiga konfigurationspunkter.

#### Dokumentbaserat formulär med kalkylblad/e-postinlämning

Det här är den enklaste konfigurationen. Du skapar formuläret i Word/Google Docs och skickar data till ett kalkylblad eller e-postmeddelande via Forms inskickningstjänst.

1. Definiera formuläret i ett Word/Google-dokument/ark med hjälp av den angivna tabellstrukturen eller det angivna formulärblocket.
1. I dokumentet (eller i den relaterade konfigurationen) anger du kalkylblads-URL:en eller e-postadressen för Forms Submission Service.
1. Kontrollera att `forms@adobe.com` (eller det relevanta tjänstkontot) har redigeringsåtkomst till ditt målkalkylblad.
1. Publicera ditt dokument på din Edge Delivery-webbplats.

**Doc-Based + Forms Submissions Service Architecture**
<!--
```mermaid
    graph TD
        User[<img src='https://img.icons8.com/ios-filled/50/000000/user.png' width='30' /> User] >|Fills Out| EDS_Page_DocBased[EDS Page with Document-Based Form]
        EDS_Page_DocBased >|Submits Data| FSS[AEM Forms Submission Service]
        FSS > Target[<img src='https://img.icons8.com/color/48/000000/google-sheets.png' width='30' /> Data to Spreadsheet / <img src='https://img.icons8.com/color/48/000000/filled-sent.png' width='30' /> Email Notification]

        Authoring[Form defined in Google Doc/Sheet] >|EDS Syncs & Renders| EDS_Page_DocBased

        style EDS_Page_DocBased fill:#ccf,stroke:#333
        style FSS fill:#fca,stroke:#333
        style Target fill:#90ee90,stroke:#333
        style Authoring fill:#e6ffe6,stroke:#333
```-->

![Doc-Based + Forms Submissions Service Architecture](/help/forms/assets/eds-doc-fss.png)

#### Universellt redigeringsformulär med kalkylblad/e-postinlämning

Du använder den visuella universella redigeraren för att skapa formuläret, men du använder ändå den enkla Forms Submission Service för datainhämtning.

1. Skapa formuläret med Universal Editor i AEM.
1. Konfigurera formulärets skicka-åtgärd i EU så att du kan använda alternativet Skicka till Forms Submission Service.
1. Ange målkalkylblads-URL eller e-postadress.
1. Om du använder kalkylblad måste du se till att `forms@adobe.com` har redigeringsåtkomst.
1. Publicera den sida som innehåller formuläret från AEM på din Edge Delivery webbplats.

   **Universal Editor + Forms Submission Service Architecture**

   ![Universal Editor + Forms Submission Service Architecture](/help/forms/assets/eds-ue-fss.png)

   <!--```mermaid
    graph TD
    User[User] >|Fills Out| EDS_Page_UE[EDS Page with Universal Editor Form]
    EDS_Page_UE >|Submits Data| FSS[AEM Forms Submission Service]
    FSS > Target[Data sent to Google Sheet and Email Notification]
    AuthoringUE[Form built in Universal Editor - AEM] >|AEM Publishes to EDS| EDS_Page_UE
    style EDS_Page_UE fill:#ccf,stroke:#333
    style FSS fill:#fca,stroke:#333
    style Target fill:#90ee90,stroke:#333
    style AuthoringUE fill:#e6f3ff,stroke:#333
    ```
    -->

#### Universal Editor Form with AEM Publish Submission (Advanced)

I den här konfigurationen används den universella redigeraren för att skapa formulär och AEM Publish-instansen för kraftfull serverdelsbearbetning (arbetsflöden, FDM osv.). Detta kräver mer konfiguration.

1. **Skapa formulär i UE:** Bygg formulär i den universella redigeraren. Konfigurera sin sändningsåtgärd så att den pekar på en AEM Forms-åtgärd (t.ex.&quot;Anropa ett AEM-arbetsflöde&quot;,&quot;Skicka med formulärdatamodell&quot;).
1. **AEM Dispatcher-konfiguration (på AEM-publiceringsnivå):**
   * **Inga omdirigeringar:** Kontrollera att dina Dispatcher-regler *inte* omdirigerar begäranden som gjorts till `/adobe/forms/af/submit/...`-sökvägar.
   * **Tillåt överföringar:** Ändra dina Dispatcher-filter (t.ex. i `filters.any`) så att `allow` POST-begäranden till `/adobe/forms/af/submit/...` uttryckligen ändras från din Edge Delivery-webbplats domän eller IP-adresser.
1. **filtret för OSGi-referens i AEM (på AEM-publiceringsnivå):**
   * I AEM OSGi-konsolen (`/system/console/configMgr`) söker du efter och konfigurerar referensfiltret för Apache Sling.
   * Lägg till domäner för din Edge Delivery-webbplats (t.ex. `https://your-eds-domain.hlx.page`, `https://your-custom-eds-domain.com`) i listan Tillåt värdar eller Tillåt värdar RegExp. Detta innebär att AEM godkänner inskickade svar från din EDS-webbplats.
1. **Omdirigeringsregel för CDN (i ditt CDN-nätverk i Edge Delivery):**
   * Din Edge Delivery-webbplats (t.ex. `your-eds-domain.hlx.page`) måste skicka in begäranden korrekt till din AEM Publish-instans.
   * När formuläret på din EDS-sida skickar kan det ha en relativ sökväg som `/adobe/forms/af/submit/...` som mål. Du behöver en regel för ditt CDN (eller edge worker) i Edge Delivery som säger:&quot;Om en begäran kommer till `your-eds-domain.hlx.page/adobe/forms/af/submit/...`, vidarebefordra (proxy eller omdirigering) den till `your-aem-publish-instance.com/adobe/forms/af/submit/...`.&quot;
   * Exakt implementering beror på din CDN-leverantör (t.ex. Fast VCL, Akamai Property Manager, Cloudflare Workers).
1. **(Valfritt) `constants.js` för utveckling (i EDS-projektets kodbas):**
   * För lokal utveckling eller om dina formulärskript på klientsidan behöver känna till den fullständiga publicerings-URL:en för AEM, kan du konfigurera detta i en `constants.js` eller liknande konfigurationsfil i Edge Delivery-projektets GitHub-databas. Exempel:

   ```javascript
       // in your-eds-project/scripts/constants.js
       export const AEM_PUBLISH_URL = 'https://publish-p123-e456.adobeaemcloud.com';
            // Your form submission script might then construct the submit URL:
           // const submitUrl = `${AEM_PUBLISH_URL}/adobe/forms/af/submit/...`;
   ```

1. **Publicera:** Publicera formulärsidan från AEM till EDS och kontrollera att alla AEM-konfigurationer är aktiva på din AEM Publish-instans.

   **Universal Editor + AEM Publish Architecture**

![Universal Editor + AEM Publish Architecture](/help/forms/assets/eds-aem-publish.png)

Detta visar flödet: användare skickar data på EDS-webbplatsen, CDN dirigerar till AEM Dispatcher och sedan bearbetar AEM Publish det.

#### Bädda in ett formulär på en dokumentredigeringssida (DA)

Huvudinnehållet på webbplatsen skapas i Document Authoring (DA). Du skapar formuläret separat med antingen dokumentbaserad redigering eller Universal Editor och bäddar sedan in det på din DA-sida.

1. **Skapa och publicera formuläret:**
   * Skapa formuläret med hjälp av dokumentbaserad redigering eller en universell redigerare.
   * Konfigurera överföringsmetoden (antingen till Forms Submission Service eller AEM Publish enligt Setup 1, 2 eller 3).
   * Publicera det här formuläret så att det finns på en egen Edge Delivery-URL (t.ex. `.../forms/my-special-form`).
1. **Konfigurera CORS:** Kontrollera att CORS-huvuden är konfigurerade så att dokumentredigeringswebbplatsens domän kan hämta det på den Edge Delivery-webbplats/det-projekt som är värd för det här fristående formuläret.
1. **Författarsida i DA:** Skapa eller redigera din sida i Dokumentredigering.
1. **Bädda in formulärblock:** Använd lämpligt block i DA för att bädda in en extern URL. Peka det här blocket på URL:en för ditt fristående publicerade formulär.
1. **Publicera DA-sida:** Publicera din DA-sida. Formuläret kommer nu att hämtas och visas.

   **Forms inbäddat i DA-arkitekturen**

   ![Forms inbäddat i DA-arkitekturen](/help/forms/assets/eds-forms-embedd-da.png)

   Då visas en DA-sida som drar in ett formulär från en annan EDS-plats. Det inbäddade formuläret hanterar sin egen skickning.

## Felsökning

* **Det går inte att skicka formulär.**
   * **Kontrollera konsolfel:** Öppna webbläsarens utvecklarkonsol (vanligtvis F12) och sök efter fel på fliken Nätverk eller Konsol när du skickar.
   * **Bekräfta överförings-URL:** Försöker formuläret skicka till rätt slutpunkt (Forms överföringstjänst-URL eller AEM publiceringssökväg)?
   * **Forms överföringstjänst:** Har `forms@adobe.com` fått redigeringsåtkomst om du skickar till ett kalkylblad? Är kalkylblads-URL korrekt?
   * **Publicera inskickade AEM-filer:**
      * Tillåter din Dispatcher POST till `/adobe/forms/af/submit/...`?
      * Är Sling Referrer-filtret på AEM Publish konfigurerat för att tillåta din EDS-domän?
      * Fungerar reglerna för omdirigering av CDN för `/adobe/forms/af/submit/...` korrekt?

* **Mitt inbäddade formulär visas inte.**

   * **KORS!** Det här är den vanligaste orsaken. Kontrollera om webbläsarkonsolen innehåller CORS-fel. Kontrollera att webbplatsen *som är värd* har rätt `Access-Control-Allow-Origin`-huvuden.
   * **Korrigera formulär-URL?** Påverkar inbäddningskoden på värdsidan rätt live-URL för formuläret?
   * **JavaScript-block:** Om formuläret är beroende av ett särskilt JavaScript-formulärblock för återgivning, är det blockets kod tillgänglig på värdsidan?

* **Jag får ett &quot;403 Forbidden&quot; eller &quot;401 Unauthorized&quot; när jag skickar till AEM Publish.**

   * Detta pekar ofta på Sling Referrer-filtret i AEM Publish som inte tillåter förfrågningar från din EDS-domän. Dubbelkontrollera dess konfiguration.
   * Det kan också vara ett autentiserings-/auktoriseringsproblem om din AEM-slutpunkt kräver det, även om standardformulärinlämningar vanligtvis är anonyma.

## Nästa steg

Den här guiden innehåller en översikt över hur du använder formulär med AEM Edge Delivery Services. Mer detaljerade, stegvisa instruktioner om specifika konfigurationer finns i Adobe Experience Manager officiella dokumentation:

* [Dokumentbaserad redigering med Edge Delivery Services Forms](/help/edge/docs/forms/tutorial.md)
* [Universell redigerare med Edge Delivery Services Forms](/help/edge/docs/forms/universal-editor/overview-universal-editor-for-edge-delivery-services-for-forms.md)
* [Dokumentredigering (DA) och inbäddat innehåll](https://www.aem.live/developer/da-tutorial)
* [AEM Forms Submission Service](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)