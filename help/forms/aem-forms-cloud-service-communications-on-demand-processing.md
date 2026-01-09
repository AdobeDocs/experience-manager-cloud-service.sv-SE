---
title: Hur konfigurerar jag Forms Communications Synchronous API:er?
description: Konfigurera utvecklingsmiljö för Synkrona API:er för interaktiv kommunikation för Adobe Experience Manager Forms as a Cloud Service
role: Admin, Developer, User
feature: Adaptive Forms,APIs & Integrations
hide: true
hidefromtoc: true
index: false
source-git-commit: e2f57a32fcc098a2331ad74540a3d48832c2b3c3
workflow-type: tm+mt
source-wordcount: '2380'
ht-degree: 0%

---


# Konfigurera OAuth Server-till-Server-åtkomst för AEM Forms Communications Synchronous API:er

Den här guiden innehåller anvisningar för hur du konfigurerar och anropar AEM Forms Communications Synchronous API:er som nås via Adobe Developer Console med OAuth Server-to-Server-autentisering.

## Förutsättningar

Om du vill konfigurera en miljö för att köra och testa AEM Forms Communications API:er måste du ha följande:

### Åtkomst och behörigheter

Kontrollera att du har de behörigheter och behörigheter som krävs innan du börjar konfigurera kommunikations-API:erna.

**Användar- och rollbehörigheter**

- Utvecklarroll som tilldelats i Adobe Admin Console
- Behörighet att skapa projekt i Adobe Developer Console

>[!NOTE]
>
> Mer information om hur du tilldelar roller och beviljar åtkomst till användare finns i artikeln [Lägg till användare och roller](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-manager/content/requirements/users-and-roles).

**Git-databasåtkomst**

- Åtkomst till Cloud Manager Git-databas
- Git-inloggningsuppgifter för kloning och push-ändringar

>[!NOTE]
>
> Mer information om hur du integrerar Adobe Cloud Manager och Adobe Cloud Manager finns i [Git-integreringsdokumentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/git-integration.html).

### Generera åtkomsttoken med Adobe Developer Console (ADC)

- Generera åtkomsttoken via Adobe Developer Console med OAuth Server-till-Server-autentisering.
- Hämta klient-ID från Adobe Developer Console

>[!NOTE]
>
> [Klicka här](/help/forms/oauth-api-authetication.md) om du vill ha mer information om OAuth Server-till-Server-autentisering med Adobe Developer Console.

### Utvecklingsverktyg

- **Node.js** för att köra exempelprogram
- Senaste versionen av **Git**
- Åtkomst till **Terminal-/kommandorad**
- **Textredigerare eller IDE** för redigering av konfigurationsfiler (VS-kod, IntelliJ, osv.)
- **Postman** eller liknande verktyg för API-testning

>[!NOTE]
>
> Detta är en engångsprocess per miljö som måste slutföras innan du kan fortsätta med konfigurationen av AEM Forms Communications API:er.

## Konfigurera Synkrona API:er för AEM Forms Communications

AEM Forms Communication API:er nås via Adobe Developer Console med hjälp av OAuth server-till-server-autentisering.

Följ stegen nedan för att konfigurera synkrona API:er för Forms Communication för att generera PDF med hjälp av mallen och XDP-filen:

### Steg 1: Få tillgång till AEM Cloud-tjänstmiljön och AEM Forms Endpoint

Få tillgång till informationen om AEM Cloud-tjänstmiljön för att få de URL:er och identifierare som behövs för API-konfigurationen.

#### 1.1 Logga in på Adobe Cloud Manager

1. Navigera till [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com)
2. Logga in med din Adobe ID

#### 1.2 Navigera till Program Overview

Välj ditt program i listan. Du omdirigeras till sidan **Programöversikt**

![Programöversiktssida](/help/forms/assets/program-overview.png)

#### 1.3 Åtkomst och visning av AEM Cloud-tjänstmiljö

Du kan visa eller komma åt informationen om AEM Cloud-tjänstmiljön med något av följande två alternativ:

>[!BEGINTABS]

>[!TAB Alternativ 1: Från översiktssida]

1. På sidan **Programöversikt**
2. Klicka på **&quot;Miljöer&quot;** på den vänstra menyn.  Du kan se en lista över alla miljöer
3. Klicka på det specifika miljönamnet för att visa information

   ![Visa alla miljöer](/help/forms/assets/all-env.png)

>[!TAB Alternativ 2: Från miljöavsnitt]

1. På sidan **Programöversikt**
2. Leta reda på avsnittet **Miljöer**
3. Klicka på **&quot;Visa alla&quot;** om du vill visa alla miljöer
4. Klicka på menyn **ellips (..)** bredvid miljön
5. Välj **&quot;Visa detaljer&quot;**

   ![Alternativ1-Miljöinformation](/help/forms/assets/option2-env-details.png)

>[!ENDTABS]

#### &#x200B;4. Hitta din AEM Forms-slutpunkt

Observera din AEM URL-instans på informationssidan **Miljö** .

![Alternativ1-Miljöinformation](/help/forms/assets/option1-env.png)

>[!NOTE]
>
> Information om hur du får åtkomst till AEM Cloud-tjänstmiljön och AEM Forms Endpoint finns i [Hantera miljödokumentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-environments.html?lang=sv-SE).

### Steg 2: Klona Git-databas

Klona Cloud Manager Git-databasen för att hantera API-konfigurationsfilerna.

#### 2.1 Leta rätt på avsnittet Databas

1. Klicka på fliken **Databaser** på sidan **Programöversikt**
2. Leta reda på databasnamnet och klicka på ellipsmenyn (..)
3. Kopiera databas-URL

   ![Kopiera repo-URL](/help/forms/assets/copy-repo-url.png)

>[!NOTE]
>
> URL-formatet är vanligtvis `https://git.cloudmanager.adobe.com/<org>/<program>/`

#### 2.2 Klona med Git-kommando

1. Öppna kommandotolken eller terminalen
2. Kör kommandot `git clone` för att klona Git-databasen.

   ```bash
   git clone [repository-url]
   ```

>[!NOTE]
>
> Använd inloggningsuppgifterna från Adobe Cloud Manager för att klona Git-databasen.

Om du till exempel vill klona din Git-databas kör du följande kommando:

```bash
https://git.cloudmanager.adobe.com/formsinternal01/AEMFormsInternal-ReleaseSanity-pXXX-ukYYYY/
```

![Klonar Git-databasen](/help/forms/assets/repo-clone.png)

Mer information om hur du integrerar Adobe Cloud Manager och Adobe Cloud Manager finns i [Git-integreringsdokumentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/managing-code/git-integration.html).

### Steg 3: Adobe Developer Console Project Setup

#### 3.1 Åtkomst till Adobe Developer Console

1. Navigera till [Adobe Developer Console](https://developer.adobe.com/console)
2. Logga in med din Adobe ID
3. Skapa nytt projekt eller navigera till ditt befintliga projekt

>[!BEGINTABS]

>[!TAB Så här skapar du ett nytt projekt]

1. Klicka på **Skapa nytt projekt** i avsnittet **Snabbstart**
2. Ett nytt projekt skapas med ett standardnamn

   ![Skapa ADC-projekt](/help/forms/assets/adc-home.png)

3. Klicka på **Redigera projekt** längst upp till höger

   ![Redigera projekt](/help/forms/assets/adc-edit-project.png)

4. Ange ett beskrivande namn (t.ex. &quot;formsproject&quot;)
5. Klicka på **Spara**

   ![Redigera projektnamn](/help/forms/assets/adc-edit-projectname.png)

>[!TAB Navigera till ditt befintliga projekt]

1. Klicka på **Alla projekt** i Adobe Developer Console

   ![Sökprojekt](/help/forms/assets/search-adc-project.png)

2. Leta upp projektet och klicka för att öppna det.

   ![Hitta projekt](/help/forms/assets/locate-adc-project.png)

>[!ENDTABS]

#### 3.2 Lägg till API:er för Forms Communication

1. Klicka på **Lägg till API**

   ![Lägg till API](/help/forms/assets/adc-add-api.png)

2. I dialogrutan _Lägg till API_ kan du filtrera efter **Experience Cloud**
3. Välj **&quot;Forms Communication APIs&quot;**

   ![Lägg till Forms Communication API](/help/forms/assets/adc-add-forms-api.png)

4. Klicka på **Nästa**
5. Välj autentiseringsmetoden **OAuth Server-till-server**

   ![Välj autentiseringsmetod](/help/forms/assets/adc-add-authentication-method.png)
6. Klicka på **Nästa**

#### 3.3 Lägg till produktprofil

1. Välj den **produktprofil** som matchar din AEM-instans-URL (`https://Service Type -Environment Type-Program XXX-Environment XXX.adobeaemcloud.com`).

2. Klicka på **Spara konfigurerat API**. API och produktprofil läggs till i ditt projekt

   ![Välj projektkonfiguration](/help/forms/assets/adc-add-product-profile.png)

3. Visa avsnittet **Information om autentiseringsuppgifter**

   ![Visa autentiseringsuppgifter](/help/forms/assets/adc-view-credential.png)

**Post-API-autentiseringsuppgifter**

```text
    API Credentials:
    ================
    Client ID: <your_client_id>
    Client Secret: <your_client_secret>
    Technical Account ID: <tech_account_id>
    Organization ID: <org_id>
    Scopes: AdobeID,openid,read_organizations
```

#### 3.4 Generera åtkomst

>[!BEGINTABS]

>[!TAB För testning]

Generera åtkomsttoken manuellt i Adobe Developer Console:

1. Klicka på knappen **&quot;Generera åtkomsttoken&quot;** i projektets API-avsnitt
2. Kopiera genererad åtkomsttoken

   ![Generera åtkomsttoken](/help/forms/assets/adc-access-token.png)

>[!NOTE]
>
> Åtkomsttoken är endast giltig i **24 timmar**

>[!TAB För produktion]

Generera tokens programmatiskt med [Adobe IMS](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service) API:

**Nödvändiga autentiseringsuppgifter:**

- Klient-ID
- Klienthemlighet
- Omfång (vanligtvis: `openid, AdobeID, read_organizations, additional_info.projectedProductContext, read_pc.dma_aem_cloud, aem.document`)

**Tokenslutpunkt:**

```
    https://ims-na1.adobelogin.com/ims/token/v3
```

**Exempelbegäran (url):**

```bash
    curl -X POST 'https://ims-na1.adobelogin.com/ims/token/v3' \
    -H 'Content-Type: application/x-www-form-urlencoded' \
    -d 'grant_type=client_credentials' \
    -d 'client_id=<YOUR_CLIENT_ID>' \
    -d 'client_secret=<YOUR_CLIENT_SECRET>' \
    -d 'scope=AdobeID,openid,read_organizations'
```

**Svar:**

```json
        {
        "access_token": "eyJhbGciOiJSUz...",
        "token_type": "bearer",
        "expires_in": 86399
        }
```

>[!ENDTABS]

Du kan nu använda den genererade åtkomsttoken för att göra API-anrop för utvecklings-, scen- eller produktionsmiljöer.

>[!NOTE]
>
> Mer information om OAuth server-till-server-autentisering via Adobe Developer Console finns i artikeln [OAuth Server-to-Server Authentication](/help/forms/oauth-api-authetication.md) .

### Steg 4: Registrera klient-ID med AEM Environment

Om du vill att ditt ADC-projekts klient-ID ska kunna kommunicera med AEM-instansen måste du registrera den med en YAML-konfigurationsfil och distribuera den via en konfigurationspipeline.

#### 4.1 Hitta eller skapa konfigurationskatalog

1. Navigera till den klonade AEM Project-databasen och leta reda på mappen `config`
2. Om den inte finns skapar du den på projektets rotnivå:

   ```bash
   mkdir config
   ```

3. Skapa en ny fil med namnet `api.yaml` i katalogen `config`:

   ```bash
   touch config/api.yaml
   ```

4. Lägg till följande kod i filen `api.yaml`:

   ```yaml
   kind: "API"
   version: "1"
   metadata:
   envTypes: ["dev"]  # or ["prod", "stage"] for production environments
   data:
   allowedClientIDs:
       author:
       - "<your_client_id>"
       publish:
       - "<your_client_id>"
       preview:
       - "<your_client_id>"
   ```

I följande exempel förklaras konfigurationsparametrarna:

- **sort**: Alltid inställt på `"API"` (identifierar detta som en API-konfiguration)
- **version**: API-version, vanligtvis `"1"` eller `"1.0"`
- **envTypes**: Array med miljötyper där den här konfigurationen gäller
   - `["dev"]` - Endast utvecklingsmiljöer
   - `["stage"]` - Endast mellanlagringsmiljöer
   - `["prod"]` - endast produktionsmiljöer
- **allowedClientIDs**: Klient-ID:n har åtkomst till din AEM-instans
   - **författare**: Klient-ID för författarnivå
   - **publicera**: Klient-ID för publiceringsskikt
   - **förhandsgranskning**: Klient-ID för förhandsgranskningsnivå

![Lägger till konfigurationsfil](/help/forms/assets/create-api-yaml-file.png)

#### 4.2 Verkställ och skicka ändringar

1. Navigera till rotmappen för den klonade databasen och kör kommandona nedan:


   ```bash
       git add config/api.yaml
       git commit -m "Whitelist client id for api invocation"
       git push origin <your-branch>
   ```

   ![Push Git-ändringar](/help/forms/assets/push-yaml-changes-in-git.png)


### Steg 5: Konfigurera konfigurationsförlopp

#### 5.1 Leta reda på pipelines-kortet

1. Leta reda på kortet **Pipelines** på sidan Programöversikt
2. Klicka på knappen **&quot;Lägg till&quot;**

   ![Lägg till pixel](/help/forms/assets/add-pipeline.png)

#### 5.2 Välj typ av pipeline

- **För utvecklingsmiljöer**: Välj **&quot;Lägg till icke-produktionsförlopp&quot;**. Rörledningar som inte är avsedda för produktion är avsedda för dev- och scenmiljöer

- **För produktionsmiljöer**: Välj **&quot;Lägg till produktionsförlopp&quot;**. Produktionspipelinjer kräver ytterligare godkännanden

>[!NOTE]
>
> I det här fallet skapar du en icke-produktionspipeline eftersom en utvecklingsmiljö är tillgänglig.

**1. Konfigurera pipeline - Konfigurationsflik**

På fliken **Konfiguration**:

a. **Förloppstyp**

- Välj **&quot;Distributionspipeline&quot;**

b. **Pipelinenamn**

- Ange ett beskrivande namn, t.ex. ge pipelinen namnet `api-config-pipieline`

c. **Utlösare för distribution**

- **Manuell**: Distribuera endast när manuellt utlöses (rekommenderas för den första konfigurationen)
- **Vid Git-ändringar**: Distribuera automatiskt när ändringar överförs till grenen

d. **Beteende vid viktiga mätfel**

- **Fråga varje gång**: Fråga efter åtgärder vid fel (standard)
- **Misslyckades omedelbart**: Felsök automatiskt pipeline vid måttfel
- **Fortsätt omedelbart**: Fortsätt trots fel

e. Klicka på **&quot;Fortsätt&quot;** för att fortsätta till fliken **Source-kod**

![Konfigurera pipeline](/help/forms/assets/add-config-pipeline.png)

**2. Konfigurera pipeline - Source Code Tab**

På fliken **Source Code**:

a. **Distributionstyp**

- Välj **&quot;Måldistribution&quot;**

b. **Distributionsalternativ**

- Välj **&quot;Konfig&quot;** (endast distribuera konfigurationsfiler). Den talar om för Cloud Manager att detta är en konfigurationsdistribution.

c. **Välj berättigad distributionsmiljö**

- Välj den miljö där du vill distribuera konfigurationen. I det här fallet är det en `dev`-miljö.

d. **Definiera Source-koddetaljer**

- **Databas**: Välj den databas som innehåller din `api.yaml`-fil. Välj till exempel databasen `AEMFormsInternal-ReleaseSanity-pXXXXX-ukYYYYY`.
- **Git-grenen**: Välj din gren. I det här fallet distribueras till exempel vår kod på grenen `main`.
- **Kodplats**: Ange sökvägen till katalogen `config`. Eftersom `api.yaml` finns i mappen `config` i roten anger du `/config`

e. Klicka på **&quot;Spara&quot;** för att skapa pipelinen

![Konfigurera pipeline](/help/forms/assets/confirm-pipeline-1.png)

### Steg 6: Distribuera konfiguration

Distribuera din `api.yaml`-konfiguration nu när pipeline har skapats:

#### 6.1 Från översikten för pipeline

1. På sidan Programöversikt letar du reda på kortet **Pipelines**
2. Navigera till den konfigurationspipeline du nyss skapat i listan. Du kan till exempel söka efter det pipelinenamn du skapade (t.ex. &quot;api-config-pipeline&quot;). Du kan se pipeline-information, inklusive status och senaste körning.

#### 6.2 Starta distributionen**

1. Klicka på knappen **&quot;Skapa&quot;** (eller uppspelningsikonen ▶) bredvid din pipeline
2. Bekräfta distributionen om du uppmanas att göra det och pipeline-körningen börjar

![kör pipeline](/help/forms/assets/run-config-pipeline.png)

#### 6.3 Verifiera lyckad distribution

- Vänta på att pipeline ska slutföras.
   - Om det lyckas ändras statusen till Slutfört (grön bock ✓).
   - Om det misslyckas ändras statusen till&quot;Misslyckad&quot; (röd korsning ✗). Klicka på **Hämta loggar** för att visa felinformationen.

     ![Pipelinen lyckades](/help/forms/assets/pipeline-suceess.png)

Nu kan du börja testa Forms Communications API:er. I testsyfte kan du använda Postman, curl eller någon annan REST-klient för att anropa API:erna.

### Steg 7: API-specifikationer och testning

Nu när miljön är konfigurerad kan du börja testa API:erna för AEM Forms Communication antingen med hjälp av användargränssnittet i Swagger eller programmatiskt genom att utveckla NodeJS-programmet.

>[!BEGINTABS]

>[!TAB A. Använda Swagger-gränssnittet för API-testning ]

Swagger-gränssnittet innehåller ett interaktivt gränssnitt för att testa API:er utan att behöva skriva kod. Använd funktionen **Prova** för att anropa och testa [generera Forms Communication API &#x200B;](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFForm) för PDF.

1. Navigera till [Forms Communication API Reference](https://developer.adobe.com/experience-manager-forms-cloud-service-developer-reference/) och öppna [Forms Communication API](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document) -dokumentationen i webbläsaren.
2. Expandera avsnittet **Dokumentgenerering** och välj [Skapar ett ifyllbart PDF-formulär från en XDP- eller PDF-mall, eventuellt med datasammanfogning](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/document/#operation/renderPDFForm).
3. Klicka på **Testa** i den högra rutan.

   ![Swagger-testning för API](/help/forms/assets/api-doc-generation.png)
4. Ange följande värden:

   | **Avsnitt** | **Parameter** | **Värde** |
   |--------------|---------------|------------|
   | bucket | AEM, instans | AEM-instansnamn utan Adobe-domännamn (`.adobeaemcloud.com`) Använd till exempel `pXXXXX-eYYYYY` som bucket. |
   | Dokumentskydd | Bearer Token | Använd åtkomsttoken [från autentiseringsuppgiften OAuth Server-to-Server för Adobe Developer Console Project](/help/forms/oauth-api-authetication.md#how-to-generate-an-access-token-using-oauth-server-to-server-authentication) |
   | Brödtext | mall | Överför en XDP för att generera PDF-formuläret. Du kan till exempel använda [den här XDP](/help/forms/assets/ClosingForm.xdp) för att generera en PDF. |
   | Brödtext | data | En valfri XML-fil som innehåller de data som ska sammanfogas med mallen för att generera ett förfyllt PDF-formulär. Du kan till exempel använda [den här XML](/help/forms/assets/ClosingForm.xml) för att skapa en PDF. |
   | Parametrar | X-Adobe-Accept-Experimental | 1 |

5. Klicka på **Skicka** för att anropa API:t

   ![Skicka API](/help/forms/assets/api-send.png)

6. Kontrollera svaret på fliken **Svar**:
   - Om svarskoden är `200` innebär det att PDF har skapats.
   - Om svarskoden är `400` betyder det att parametrarna för begäran är ogiltiga eller har fel format.
   - Om svarskoden är `500` betyder det att det finns ett internt serverfel.
   - Om svarskoden är `403` betyder det att det finns ett auktoriseringsfel.

   I det här fallet är svarskoden `200`, vilket betyder att PDF har skapats:

   ![Granskningssvar](/help/forms/assets/api-success.png)

   Nu kan du hämta den [skapade PDF](/help/forms/assets/create-pdf.pdf) med knappen **Hämta** och visa den i PDF Viewer:

   ![Visa PDF](/help/forms/assets/create-pdf.png)

   >[!NOTE]
   >
   > I testsyfte kan du även använda [Postman](https://www.postman.com/), [curl](https://curl.se/) eller någon annan REST-klient för att anropa AEM API:er.

>[!TAB B. Programmatiskt genom att utveckla NodeJS-program ]

Utveckla ett Node.js-program för att generera ett ifyllbart PDF-formulär från en **XDP**-mall och en **XML**-datafil med **Document Services API**

**Förutsättningar**

- Node.js är installerat på datorn
- Aktiv AEM as a Cloud Service-instans
- Bearer-token för API-autentisering från Adobe Developer Console
- Exempel på XDP-fil: [ClosingForm.xdp](/help/forms/assets/ClosingForm.xdp)
- XML-exempelfil: [ClosingForm.xml](/help/forms/assets/ClosingForm.xml)

Så här utvecklar du programmet Node.js:

**Steg 1: Skapa ett nytt Node.js-projekt**

Öppna cmd/terminal och kör nedanstående kommandon:

```bash
# Create a new directory
mkdir demo-nodejs-generate-pdf
cd demo-nodejs-generate-pdf

##### Initialize Node.js project
npm init -y
```

![Skapa nytt nodjs-projekt](/help/forms/assets/api-1.png)

**Steg 2: Installera nödvändiga beroenden**

Installera biblioteken **node-fetch**, **dotenv** och **form-data** om du vill göra HTTP-begäranden, läsa miljövariabler respektive hantera formulärdata.

```bash
npm install node-fetch
npm install dotenv
npm install form-data
```

![installera npm-beroenden](/help/forms/assets/api-2.png)

**Steg 3: Uppdatera package.json**

1. Öppna cmd/terminal och kör kommandot:

   ```bash
   code .
   ```

   ![öppna projekt i redigeraren](/help/forms/assets/api-3.png)

   Det öppnar projektet i kodredigeraren.

2. Uppdatera filen `package.json` för att lägga till `type` i `module`.

   ```bash
   {
   "name": "demo-nodejs-generate-pdf",
   "version": "1.0.0",
   "type": "module",
   "main": "index.js",
   }
   ```

   ![uppdatera paketfilen](/help/forms/assets/api-4.png)

**Steg 4: Skapa en .env-fil**

1. Skapa en .env-fil på rotnivån för ett projekt
2. Lägg till följande konfiguration och ersätt platshållarna med de faktiska värdena från ADC-projektets autentiseringsuppgifter för OAuth Server-till-server.

   ```bash
   CLIENT_ID=<ADC Project OAuth Server-to-Server credential ClientID>
   CLIENT_SECRET=<ADC Project OAuth Server-to-Server credential Client Secret>
   SCOPES=<ADC Project OAuth Server-to-Server credential Scopes>
   ```

   ![skapa miljöfil](/help/forms/assets/api-5.png)

   >[!NOTE]
   >
   > Du kan kopiera `CLIENT_ID`, `CLIENT_SECRET` och `SCOPES` från Adobe Developer Console-projektet.

**Steg 5: Skapa src/index.js**

1. Skapa filen `index.js` på projektets rotnivå
2. Lägg till följande kod och ersätt platshållarna med de faktiska värdena:

```javascript
// Import the dotenv configuration to load environment variables from the .env file
import "dotenv/config";

// Import fetch for making HTTP requests
import fetch from "node-fetch";
import fs from "fs";
import FormData from "form-data";

// REPLACE THE FOLLOWING VALUE WITH YOUR OWN
const bucket = <bucket-value>; // Your AEM Cloud Service Bucket name
const xdpFilePath = <xdp-file>;
const xmlFilePath = <xml-file>;

// Load environment variables
const clientId = process.env.CLIENT_ID;
const clientSecret = process.env.CLIENT_SECRET;
const scopes = process.env.SCOPES;

// Adobe IMS endpoint for obtaining an access token
const adobeIMSV3TokenEndpointURL = "https://ims-na1.adobelogin.com/ims/token/v3";

// Function to get an access token
const getAccessToken = async () => {
    console.log("Getting access token from IMS...");

    const options = {
        method: "POST",
        headers: {
            "Content-Type": "application/x-www-form-urlencoded",
        },
        body: `grant_type=client_credentials&client_id=${clientId}&client_secret=${clientSecret}&scope=${scopes}`,
    };

    const response = await fetch(adobeIMSV3TokenEndpointURL, options);
    const responseJSON = await response.json();

    console.log("Access token received.");
    return responseJSON.access_token;
};

// Function to generate PDF form from XDP and XML
const generatePDF = async () => {
    const accessToken = await getAccessToken();

    console.log("Generating PDF form from XDP and XML...");

    // Read XDP and XML files
    const xdpFile = fs.readFileSync(xdpFilePath);
    const xmlFile = fs.readFileSync(xmlFilePath);

    const url = `https://${bucket}.adobeaemcloud.com/adobe/document/generate/pdfform`;

    const formData = new FormData();
    formData.append("template", xdpFile, {
        filename: "form.xdp",
        contentType: "application/vnd.adobe.xdp+xml"
    });
    formData.append("data", xmlFile, {
        filename: "data.xml",
        contentType: "application/xml"
    });

    const response = await fetch(url, {
        method: "POST",
        headers: {
            Authorization: `Bearer ${accessToken}`,
            "X-Api-Key": clientId,
            "X-Adobe-Accept-Experimental": "1",
            ...formData.getHeaders()
        },
        body: formData,
    });

    if (response.ok) {
        const arrayBuffer = await response.arrayBuffer();
        fs.writeFileSync("generatedForm.pdf", Buffer.from(arrayBuffer));
        console.log("✅ PDF form generated successfully (saved as generatedForm.pdf)");
    } else {
        console.error("❌ Failed to generate PDF. Status:", response.status);
        console.error(await response.text());
    }
};

// Run the PDF generation function
generatePDF();
```

![skapa index.js](/help/forms/assets/api-6.png)

**Steg 6: Kör programmet**

```bash
node src/index.js
```

![kör programmet](/help/forms/assets/api-7.png)

PDF skapas i mappen `demo-nodejs-generate-pdf`. Navigera till mappen för att hitta den genererade filen `generatedForm.pdf`.

![visa skapad PDF](/help/forms/assets/api-8.png)

![Visa PDF](/help/forms/assets/create-pdf.png)

>[!ENDTABS]

Du kan öppna den [genererade PDF](/help/forms/assets/create-pdf.png) för att visa den.

## Felsökning

### Vanliga problem och möjliga orsaker

#### Utgåva 1: 403 Förbjudet fel

**Symtomen:**

- API-förfrågningar returnerar `403 Forbidden`
- Felmeddelande: *Obehörig åtkomst*

**Möjlig orsak:**

- Klient-ID har inte registrerats i AEM-instansens `api.yaml`-konfiguration

#### Problem 2: 401 Otillåtet fel

**Symtomen:**

- API-förfrågningar returnerar `401 Unauthorized`
- Felmeddelande: *Ogiltig eller utgången token*

**Möjliga orsaker:**

- Åtkomsttoken har gått ut (gäller endast i 24 timmar)
- Felaktigt eller felmatchat klient-ID och klienthemlighet

#### Problem 3: 404 Det gick inte att hitta felet

**Symtomen:**

- API-förfrågningar returnerar `404 Not Found`
- Felmeddelande: *Resursen hittades inte* eller *API-slutpunkten hittades inte*

**Möjlig orsak:**

- Felaktig bucket-parameter (matchar inte AEM-förekomsdentifierare)

#### Problem 4: Driftsättning av pipeline misslyckades

**Symtomen:**

- Körningen av konfigurationspipeline misslyckades
- Distributionsloggar visar fel relaterade till `api.yaml`

**Möjliga orsaker:**

- Ogiltig YAML-syntax (indrag, offert eller matrisformatproblem)
- `api.yaml` placerades i fel katalog
- Felaktigt eller felaktigt klient-ID i konfigurationen
- Ogiltig klienthemlighet

#### Problem 5: Forms Communication API:er kan inte köras

**Symtomen:**

- API-begäranden returnerar fel som anger att funktioner som inte stöds eller inte är tillgängliga.
- PDF-generering med XDP och XML fungerar inte.
- Distributionen av pipeline har slutförts, men API-anrop för körning misslyckas.

**Möjlig orsak:**

AEM-miljön kör en version som släpptes innan Forms Communication API:er introducerades eller stöddes.
Information om hur du uppdaterar AEM-miljön finns i avsnittet [Uppdatera AEM-instans](#update-aem-instance).

## Uppdatera AEM-instans

Så här uppdaterar du AEM-instansen för att hitta miljöinformation:

1. Markera ikonen `ellipsis`(..) bredvid miljönamnet och klicka på **Uppdatera**
2. Klicka på knappen **Skicka** och kör den föreslagna helstackspipelinen.

   ![Uppdateringsmiljö](/help/forms/assets/update-env.png)

## Relaterade artiklar

- Mer information om hur du konfigurerar miljö för batchbearbetning (asynkrona API:er) finns i [AEM Forms as a Cloud Service Communications Batch Processing](/help/forms/aem-forms-cloud-service-communications-batch-processing.md).