---
title: Forms Submission Service for Edge Delivery Services
description: Lagra inskickade blanketter direkt i kalkylblad med Adobe värdbaserade Forms Submission Service. Lär dig hur Google Sheets, OneDrive och SharePoint integreras med konfiguration, konfiguration och API-användning.
keywords: Forms Submission Service, Edge Delivery Services-formulär, integration av kalkylblad, Google Sheets-formulär, OneDrive-formulär, SharePoint-formulär, formulärdatainsamling
feature: Edge Delivery Services
role: User, Developer, Admin
level: Beginner, Intermediate
hide: true
hidefromtoc: true
exl-id: 12b4edba-b7a1-4432-a299-2f59b703d583
source-git-commit: 44a8d5d5fdd2919d6d170638c7b5819c898dcefe
workflow-type: tm+mt
source-wordcount: '1573'
ht-degree: 0%

---

# Forms Submission Service for Edge Delivery Services

Forms Submission Service är en värdbaserad lösning från Adobe som automatiskt lagrar data som skickas in direkt i kalkylblad: Google Sheets, Microsoft OneDrive eller SharePoint. Detta eliminerar behovet av komplex backend-infrastruktur samtidigt som datainsamling och -hantering i realtid tillhandahålls.



## Ökning

![Forms överföringstjänst](/help/forms/assets/form-submission-service.png)
*Bild: Arbetsflöde för Forms Sändningstjänst - från formulärsändning till kalkylarkslagring*

+++ Vem ska använda den här tjänsten?

**Perfekt för:**

- **Innehållsskapare** skapar enkla datainsamlingsformulär
- **Små företag** som behöver snabba arbetsflöden mellan formulär och kalkylblad
- **Marknadsföringsteam** samlar in leadinformation
- **Händelseorganisatörer** hanterar registreringar

**Överväg alternativ för:**

- Komplexa arbetsflöden som kräver anpassad logik
- Företagsintegrering med databaser
- Forms behöver avancerad validering eller bearbetning

+++

+++ Vanliga användningsfall

| Användningsfall | Exempel | Fördelar med kalkylblad |
|----------|---------|-------------------|
| **Kontakta Forms** | Webbplatsfrågor → Google Sheets | Enkel uppföljning och CRM-import |
| **Händelseregistrering** | Konferensregistreringar → Excel Online | Spårning av deltagare i realtid |
| **Leadgenerering** | Nyhetsbrev - signaturer → SharePoint | Analys av marknadsföringskampanjer |
| **Feedback-samling** | Undersökningssvar → Google Sheets | Snabb datavisualisering |

+++

## Viktiga fördelar

Forms Submission Service har flera fördelar för smidig datainsamling:



+++ Förenklad installation

- **Ingen backend-infrastruktur krävs** - Adobe är värd för överföringsslutpunkten
- **Direktintegrering** med populära kalkylbladsplattformar
- **Automatisk datamappning** från formulärfält till kalkylbladskolumner

+++


+++ Datahantering i realtid

- **Datainhämtning direkt** - inskickade data visas omedelbart i kalkylbladet
- **Strukturerad lagring** - strukturerade kolumner för enkel analys
- **Live-samarbete** - flera teammedlemmar kan komma åt och analysera data

+++

+++ Inbyggd säkerhets- och åtkomstkontroll

- **Utnyttjar befintliga behörigheter** - använd kalkylbladsplattformens delningskontroller
- **Adobe-hanterad säkerhet** - säker slutpunkt för överföring med företagsskydd
- **Dataägarskap** - dina data ligger kvar på den kalkylbladsplattform du valt

+++

## Förutsättningar

Innan du konfigurerar Forms Submission Service bör du kontrollera att du har:



+++ Tekniska krav

- **GitHub-databasen** har konfigurerats för ditt Edge Delivery Services-projekt med det senaste adaptiva Forms-blocket installerat
- **Åtkomstgodkännande** - databasen har lagts till i tillåtelselista

+++

+++ Inställningar för kalkylbladsplattform


Välj en av de plattformar som stöds:

- **Google-blad** - Google-konto med behörighet att skapa blad
- **Microsoft OneDrive** - Microsoft 365-konto med åtkomst via Excel Online
- **SharePoint** - SharePoint-åtkomst med list-/biblioteksbehörigheter

+++

+++ Behörigheter och åtkomst

- **Redigera behörigheter** för målkalkylbladet
- **Delningsfunktioner** som ger åtkomst till `forms@adobe.com`
- **Länkgenerering** behörigheter för den valda plattformen

+++

>[!TIP]
>
>**Ny på Edge Delivery Services?** Börja med självstudiekursen [Komma igång](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/tutorial) för att konfigurera din projektgrund.

## Konfigurationsmetoder

Forms Submission Service erbjuder två konfigurationsmetoder. Välj den metod som passar ditt arbetsflöde bäst:


+++ Välj din konfigurationsmetod

| Metod | Bäst för | Tid krävs | Teknisk nivå |
|--------|----------|---------------|-----------------|
| **[Manuell inställning](#manual-configuration)** | Innehållsutvecklare, engångsinstallation | 10-15 minuter | Nybörjare |
| **[API-konfiguration](#api-configuration)** | Utvecklare, automatiserade arbetsflöden | 5-10 minuter | Mellanliggande |

+++

+++ Projektinställningar

Innan du konfigurerar någon av metoderna måste du se till att din grund för AEM-projektet är klar:

1. **Skapa eller uppdatera ditt AEM-projekt** med det senaste adaptiva Forms-blocket ([Komma igång-självstudiekurs](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/tutorial))

2. **Uppdatera`fstab.yaml`** i projektets rot:

   ```yaml
   # Replace with the path to your shared folder
   mountpoints:
     /: https://drive.google.com/drive/folders/your-shared-folder-id
   ```


3. **Dela projektmappen** med `forms@adobe.com` (redigeringsbehörighet krävs)

+++

## Manuell konfiguration

![Arbetsflöde för tjänsten för att skicka formulär](/help/forms/assets/forms-submission-service-workflow.png)
*Bild: Komplett arbetsflöde för manuell konfiguration av Forms överföringstjänst*

Följ dessa steg-för-steg-instruktioner för att ställa in formuläret genom att skicka in kalkylblad:



+++ Steg 1: Skapa en formulärdefinition

Skapa en formulärstruktur med Google Sheets eller Microsoft Excel.

**Steg för att skapa formulär:**

1. **Öppna kalkylbladsplattformen** (Google-blad eller Microsoft Excel)
2. **Skapa ett nytt kalkylblad** för ditt formulärprojekt
3. **Namnge bladet** (måste vara antingen `helix-default` eller `shared-aem`)
4. **Definiera formulärstrukturen** med hjälp av guiden [Skapa formulär](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/create-forms)

![Formulärdefinition](/help/forms/assets/form-submission-definition.png)
*Exempel: Formulärdefinition med fälttyper, etiketter och valideringsregler*

>[!IMPORTANT]
>
>**Krav för bladnamngivning**
>
>Formulärdefinitionsbladet måste ha följande namn:
>
>- `helix-default` (rekommenderas för enstaka formulär)
>- `shared-aem` (för flerformulärsprojekt)
>
>Andra bladnamn känns inte igen av systemet.

**Kontrollpunkt för validering:**

- Formulärstrukturen har fyllts i med alla obligatoriska fält
- Blad har rätt namn (`helix-default` eller `shared-aem`)
- Fälttyper och verifieringsregler är korrekt konfigurerade

+++

+++ Steg 2: Skapa datainsamlingsmallen

Skapa ett dedikerat blad för att ta emot formuläröverföringsdata.

**Inställningar för datablad:**

1. **Lägg till ett nytt blad** i ditt befintliga kalkylblad
2. **Namnge bladet exakt`incoming`** (skiftlägeskänsligt)
3. **Konfigurera kolumnrubriker** som matchar formulärfälten
4. **Spara kalkylbladet** för att säkerställa att ändringarna bevaras

![Inkommande blad](/help/forms/assets/form-submission-incoming-sheet.png)
*Exempel: Inkommande blad med kolumnrubriker som matchar formulärfält*

>[!WARNING]
>
>**Kritiskt krav**
>
>Bladet måste ha exakt namnet `incoming` (gemener). Utan detta blad:
>
>- Formulärinskickat material kommer att avvisas
>- Inga data kommer att lagras
>- Användarna ser fel när de skickar in data

**Kontrollpunkt för validering:**

- `incoming` blad finns i kalkylbladet
- Kolumnrubrikerna matchar formulärfältsnamnen
- Blad är rätt sparad och tillgänglig

>[!TIP]
>
>**Pro Tips!** Kopiera de exakta fältnamnen från formulärdefinitionen för att säkerställa perfekt matchning mellan formulärfält och kalkylbladskolumner.

+++

+++ Steg 3: Dela kalkylblad med Adobe Service

Ge Adobe Forms inskickningstjänst åtkomst till ditt kalkylblad.

**Delningsprocess:**

1. **Klicka på knappen Dela** i det övre högra hörnet av kalkylbladet
2. **Lägg till Adobe-tjänstkontot:**
   - E-post: `forms@adobe.com`
   - Behörighetsnivå: **Redigeraren** (krävs för att skriva data)
3. **Skicka delningsinbjudan**
4. **Kopiera kalkylbladslänken** för nästa steg

   ![Dela inkommande blad](/help/forms/assets/form-submission-share-incoming.png)
   *Stegvis delning för att bevilja åtkomst till Adobe-tjänster*

**Plattformsspecifika instruktioner:**

**Google-blad:**

- Lägg till `forms@adobe.com` som redigerare
- Kontrollera att &quot;Alla med länken kan visa&quot; är aktiverat
- Kopiera delningslänken

**Microsoft Excel (OneDrive/SharePoint):**

- Lägg till `forms@adobe.com` med redigeringsbehörigheter
- Ange länkdelning till&quot;Alla med länken kan redigera&quot;
- Kopiera delnings-URL

  ![Kopiera länk för inkommande blad](/help/forms/assets/form-submission-copy-link.png)
  *Exempel: Kopierar den delningsbara länken för formulärkonfigurationen*

**Kontrollpunkt för validering:**

- `forms@adobe.com` har redigeraren åtkomst till ditt kalkylblad
- Kalkylbladslänken kopieras och kan användas
- Delningsbehörigheter ger extern åtkomst

+++

+++ Steg 4: Koppla formulär till kalkylblad

Länka formulärdefinitionen till det inskickade kalkylbladet.

**Anslutning av formulär-kalkylblad:**

1. **Öppna formulärdefinitionskalkylbladet** (det med `helix-default` eller `shared-aem` ark)
2. **Leta reda på fältet Skicka** i formulärdefinitionen
3. **Klistra in den kopierade kalkylbladslänken** i kolumnen **Åtgärd** för fältet Skicka
4. **Spara ändringarna** i formulärdefinitionen

   ![Länka ett kalkylblad](/help/forms/assets/form-submission-sheet-linking.png)
   *Exempel: Ansluta sändningsåtgärden till ditt datainsamlingsblad*

**Publicerar ditt formulär:**

1. **Öppna AEM Sidekick** i webbläsaren
2. **Förhandsgranska formuläret** för att testa konfigurationen
3. **Publicera formuläret** för att göra det tillgängligt

**Slutlig validering:**

- Kalkylbladslänk läggs till korrekt i åtgärden Skicka fält
- Formulärdefinitionen sparas och publiceras
- Förhandsgranska formulär visar alla fält korrekt
- Knappen Skicka är korrekt konfigurerad

>[!SUCCESS]
>
>**Installationen är klar!** Ditt formulär är nu anslutet till Forms överföringstjänst. Testa genom att skicka exempeldata och kontrollera bladet `incoming`.

**Referensmaterial:**

- [Fullständigt exempelkalkylblad](/help/forms/assets/spreadsheet.xlsx) med rätt konfiguration
- [AEM Sidekick-dokumentation](https://www.aem.live/docs/sidekick) för publiceringsvägledning

+++

## API-konfiguration

Med API-metoden kan utvecklare programmässigt skicka data till Forms Submission Service, idealiskt för automatiserade arbetsflöden och anpassade integreringar.


+++ Använda API

**Perfekt för:**

- Automatiserade datainsamlingssystem
- Anpassade formulärimplementeringar
- Integration med befintliga tillämpningar
- Arbetsflöden för att skicka data satsvis

+++

+++ Förutsättningar för API

Innan du använder API måste du se till att du har:

- **Kalkylbladskonfiguration** har slutförts (inklusive `incoming` ark)
- **Åtkomst till Adobes tjänst** beviljad till `forms@adobe.com`
- **Formulär-ID** från ditt publicerade formulär
- **Databasinformation** (organisations- och platsnamn)

>[!IMPORTANT]
>
>**Nödvändiga installationssteg**
>
>API kräver samma kalkylbladskonfiguration som manuell konfiguration:
>
>- `incoming` blad måste finnas
>- `forms@adobe.com` måste ha redigeraråtkomst
>- Blad måste publiceras via AEM Sidekick

+++

+++ API-slutpunkt och autentisering

**Bas-URL:** `https://forms.adobe.com/adobe/forms/af/submit/{id}`

**Obligatoriska rubriker:**

- `Content-Type: application/json`
- `x-adobe-routing: tier=live,bucket=main--[repository]--[organization]`

**API-dokumentation:** [Fullständig API-referens](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/references/aem-forms-submission-service/)

+++

+++ Använda Postman

Postman har ett användarvänligt gränssnitt för att testa API-inskickade data.

**Installationsanvisningar:**

1. **Skapa en ny POST-begäran** i Postman
2. **Konfigurera slutpunkten:** `https://forms.adobe.com/adobe/forms/af/submit/{id}`
3. **Ersätt platshållare:**
   - `{id}` → Ditt faktiska formulär-ID
   - `[repository]` → Ditt GitHub-databasnamn
   - `[organization]` → Din GitHub-organisation/ditt användarnamn

**Begär konfiguration:**

    &quot;json
POST https://forms.adobe.com/adobe/forms/af/submit/your-form-id

Sidhuvuden:
Content-Type: application/json
x-adobe-routing: tier=live,bucket=main—your-repo—your-org

Body (JSON):
{
&quot;data&quot;: {
&quot;startDate&quot;: &quot;2025-01-10&quot;,
&quot;endDate&quot;: &quot;2025-01-25&quot;,
&quot;destination&quot;: &quot;Australia&quot;,
&quot;class&quot;: &quot;First Class&quot;,
&quot;budget&quot;: &quot;2000&quot;,
’belopp’: ’1000000’,
&quot;name&quot;: &quot;Mary&quot;,
&quot;age&quot;: &quot;35&quot;,
&quot;subscribe&quot;: null,
&quot;email&quot;: &quot;mary@gmail.com&quot;
}
}
&quot;

**Förväntat svar:**

- **Statuskod:** `201 Created`
- **Data visas** i ditt `incoming`-kalkylblad omedelbart

![postmansskärm](/help/forms/assets/postman-api.png)
*Exempel: API-överföringen har slutförts med Postman-gränssnittet*

+++

+++ Använda kommandorad (vändning)

För utvecklare som föredrar terminal-/kommandotolk använder du curl för att skicka data programmatiskt.

**Inställningar för kommandorad:**

Ersätt följande platshållare i kommandona nedan:

- `{id}` → Ditt faktiska formulär-ID
- `[repository]` → Ditt GitHub-databasnamn
- `[organization]` → Din GitHub-organisation/ditt användarnamn

>[!BEGINTABS]

>[!TAB macOS/Linux]

```bash
curl -X POST "https://forms.adobe.com/adobe/forms/af/submit/your-form-id" \
    --header "Content-Type: application/json" \
  --header "x-adobe-routing: tier=live,bucket=main--your-repo--your-org" \
    --data '{
        "data": {
            "startDate": "2025-01-10",
            "endDate": "2025-01-25",
            "destination": "Australia",
            "class": "First Class",
            "budget": "2000",
            "amount": "1000000",
            "name": "Joe",
            "age": "35",
            "subscribe": null,
      "email": "joe@example.com"
                }
            }'
        ```

>[!TAB Windows Command Prompt]
     
```cmd
curl -X POST "https://forms.adobe.com/adobe/forms/af/submit/your-form-id" ^
    --header "Content-Type: application/json" ^
  --header "x-adobe-routing: tier=live,bucket=main--your-repo--your-org" ^
  --data "{\"data\": {\"startDate\": \"2025-01-10\", \"endDate\": \"2025-01-25\", \"destination\": \"Australia\", \"class\": \"First Class\", \"budget\": \"2000\", \"amount\": \"1000000\", \"name\": \"Joe\", \"age\": \"35\", \"subscribe\": null, \"email\": \"joe@example.com\"}}"
```

>[!TAB Windows PowerShell]

```powershell
$body = @{
  data = @{
    startDate = "2025-01-10"
    endDate = "2025-01-25"
    destination = "Australia"
    class = "First Class"
    budget = "2000"
    amount = "1000000"
    name = "Joe"
    age = "35"
    subscribe = $null
    email = "joe@example.com"
  }
} | ConvertTo-Json -Depth 3

Invoke-RestMethod -Uri "https://forms.adobe.com/adobe/forms/af/submit/your-form-id" `
  -Method POST `
  -Headers @{"Content-Type"="application/json"; "x-adobe-routing"="tier=live,bucket=main--your-repo--your-org"} `
  -Body $body
    ```

>[!ENDTABS]

+++

+++ API Response & Verification

**Successful Response:**

```http
HTTP/1.1 201 Created
Connection: keep-alive
Content-Length: 0
X-Request-Id: 02a53839-2340-56a5-b238-67c23ec28f9f
X-Message-Id: 42ecb4dd-b63a-4674-8f1a-05a4a5b0372c
Date: Fri, 10 Jan 2025 13:06:10 GMT
Access-Control-Allow-Origin: *
```

**Dataverifiering:**

När överföringen är klar kontrollerar du att data finns i kalkylbladet:

![uppdaterat blad](/help/forms/assets/updated-sheet.png)
*Exempel: Data har skrivits till det inkommande bladet via API*

**Svarsvalidering:**

- **HTTP-status:** `201 Created` indikerar att överföringen lyckades
- **X-Request-Id:** Unik identifierare för att spåra överföringen
- **Data visas** i `incoming`-bladet på några sekunder
- **Alla formulärfält** är korrekt mappade till kalkylbladskolumner

+++

## Felsökning



+++ Vanliga problem och lösningar

**Problem: 403 Otillåtet fel**

```
Causes: Missing or incorrect access permissions
Solutions:
- Verify forms@adobe.com has Editor access to your spreadsheet
- Check that your repository is added to the allowlist
- Confirm the x-adobe-routing header format
```

**Problem: 404 Det gick inte att hitta felet**

```
Causes: Incorrect Form ID or endpoint URL
Solutions:  
- Verify your Form ID is correct
- Check the API endpoint URL format
- Ensure your form is published and live
```


**Problem: Data visas inte i kalkylblad**

```
Causes: Missing 'incoming' sheet or permission issues
Solutions:
- Confirm 'incoming' sheet exists (case-sensitive)
- Verify column headers match form field names exactly
- Check forms@adobe.com has edit permissions
- Ensure spreadsheet is shared properly
```


**Problem: Ogiltigt JSON-formatfel**

```
Causes: Malformed request body
Solutions:
- Validate JSON syntax using online JSON validators
- Ensure proper escaping of special characters
- Check quote marks and brackets are balanced
```


+++

+++ Få hjälp

**Supportkanaler:**

- **Problem med tidig åtkomst:** E-post [aem-forms-ea@adobe.com](mailto:aem-forms-ea@adobe.com)
- **API-dokumentation:** [Utvecklarreferens](https://adobedocs.github.io/experience-manager-forms-cloud-service-developer-reference/references/aem-forms-submission-service/)
- **Community Support:** [Adobe Experience League Community](https://experienceleaguecommunities.adobe.com/)

+++

## Nästa steg

Nu när du har konfigurerat Forms Submission Service kan du utforska följande relaterade ämnen:


+++ Förbättra din Forms

- **[Skapa avancerad Forms](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/getting-started-edge-delivery-services-forms/create-forms)** - Lägg till validering, villkorslogik och anpassad formatering
- **[Handbok för formulärkomponenter](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/forms-components)** - Utforska tillgängliga formulärfältstyper

+++

+++ Alternativa inlämningsmetoder

- **[AEM Publish Submissions](/help/edge/docs/forms/configure-submission-action-for-eds-forms.md)** - For complex workflows and enterprise integrations
- **[Anpassade överföringsåtgärder](/help/forms/configure-submit-actions-core-components.md)** - Avancerad överföringshantering

+++

+++ Datahantering

- **[Formuläranalys](/help/forms/view-understand-aem-forms-analytics-reports.md)** - Spåra formulärens prestanda och användning
- **[Dataintegrering](/help/forms/configure-data-sources.md)** - Koppla formulär till databaser och CRM-system

+++

## Sammanfattning

Forms Submission Service är en kraftfull, kodlös lösning för att samla in blankettdata direkt i kalkylblad. Några viktiga fördelar:

- **Snabbinstallation** - Ingen backend-infrastruktur krävs
- **Realtidsdata** - omedelbar inskickning
- **Flexibla plattformar** - Google Sheets, OneDrive eller SharePoint
- **API-åtkomst** - Programmatiska inskickningsfunktioner
- **Företagssäkerhet** - Adobe-hanterade slutpunkter med åtkomstkontroller

**Vill du komma igång?** Följ [handboken för manuell konfiguration](#manual-configuration) om du vill ha en visuell konfiguration, eller gå till [API-konfiguration](#api-configuration) om du vill ha programmatisk integrering.
