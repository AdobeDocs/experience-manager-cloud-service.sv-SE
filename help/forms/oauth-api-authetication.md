---
title: Hur konfigurerar jag OAuth Server-to-Server-autentisering?
description: Lär dig konfigurera OAuth Server-till-Server-autentisering för Adobe Experience Manager Forms as a Cloud Service
role: Admin, Developer, User
feature: Adaptive Forms, APIs & Integrations
hide: true
hidefromtoc: true
index: false
source-git-commit: e2f57a32fcc098a2331ad74540a3d48832c2b3c3
workflow-type: tm+mt
source-wordcount: '811'
ht-degree: 0%

---


# OAuth Server-till-server-autentisering

OAuth Server-till-Server-autentisering ger säker, tokenbaserad åtkomst till AEM Forms Communications API:er utan att användaren behöver göra något. OAuth server-till-server-autentisering stöds av Adobe Developer Console.

## Förutsättningar

Kontrollera att följande krav är uppfyllda innan du börjar:

* Kontrollera att du har [åtkomst till Adobe Developer Console](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-manager/content/requirements/access-rights) för just den miljö du använder.
* [Tilldela systemadministratörs- eller utvecklarrollen i Adobe Admin Console](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-manager/content/requirements/role-based-permissions) för att aktivera åtkomst till Adobe Developer Console.

## Hur skapar man en åtkomsttoken med hjälp av OAuth Server-till-Server-autentisering?

Följ stegen nedan för att generera en åtkomsttoken från Adobe Developer-konsolen och gör ditt första API-anrop via OAuth Server-to-Server-autentisering.

### Adobe Developer Console Project Setup

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

### Lägg till Forms API:er

Lägg till Forms-API:er baserat på vad du vill göra:

* **AEM Forms Communications API:er**: använd när du behöver generera, konvertera, sätta ihop eller skydda dokument (PDF och relaterade format).
* **Adaptiva Forms Runtime API:er** - använd när du behöver återge, skicka eller bearbeta adaptiv Forms vid körning.

>[!BEGINTABS]

>[!TAB För AEM Forms Communications API:er]

1. Klicka på **Lägg till API**

   ![Lägg till API](/help/forms/assets/adc-add-api.png)

2. Välj **Forms Communication API:er**
   1. I dialogrutan _Lägg till API_ kan du filtrera efter **Experience Cloud**
   2. Välj **&quot;Forms Communication APIs&quot;**

      ![Lägg till Forms Communication API](/help/forms/assets/adc-add-forms-api.png)

   3. Klicka på **Nästa**
   4. Välj autentiseringsmetoden **OAuth Server-till-server**

      ![Välj autentiseringsmetod](/help/forms/assets/adc-add-authentication-method.png)

>[!TAB För adaptiva Forms Runtime API:er]

1. **Klicka på Lägg till API**

   ![Lägg till API](/help/forms/assets/adc-add-api.png)

2. **Välj AEM Forms-leverans- och körnings-API**
   1. I dialogrutan _Lägg till API_ kan du filtrera efter **Experience Cloud**
   2. Välj **&quot;AEM Forms Delivery and Runtime API&quot;**
      ![Lägg till Forms Communication API](/help/forms/assets/adc-add-runtime-api.png)

   3. Klicka på **Nästa**
   4. Välj autentiseringsmetoden **OAuth Server-to-Server**.
      ![Välj autentiseringsmetod](/help/forms/assets/adc-add-authentication-method.png)

>[!ENDTABS]

>[!NOTE]
>
> Du kan också lägga till API:t och autentiseringsmetoden i ditt befintliga projekt genom att klicka på **Lägg till i projekt** > **API**\
> ![Lägg till API i befintligt projekt](/help/forms/assets/add-api-existing-project.png)

### Lägg till produktprofil

Produktprofilen ger behörighet (eller behörighet) för inloggningsuppgifter för åtkomst till AEM-resurser.

1. Välj den **produktprofil** som matchar din AEM-instans-URL (`https://Service Type -Environment Type-Program XXX-Environment XXX.adobeaemcloud.com`).

   * **Tjänsttyp** - anger tjänster eller behörigheter som är associerade med AEM-instansen

   * **Miljötyp** - anger om miljön är för författare eller publiceringstjänst

   * **Program XXX** - identifierar Cloud Manager program-ID

   * **Environment XXX** - identifierar det specifika miljö-ID:t i det programmet

   >
   >
   > Produktprofiler är knutna till en viss AEM-instans (program + miljö). Välj alltid den profil som matchar din instans-URL.

2. Klicka på **Spara konfigurerat API**. API och produktprofil läggs till i ditt projekt

   ![Välj projektkonfiguration](/help/forms/assets/adc-add-product-profile.png)

### Generera och spara autentiseringsuppgifter

1. Navigera till ditt projekt i Adobe Developer Console
2. Klicka på autentiseringsuppgifter för **OAuth Server-till-Server**
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

### Generering av åtkomsttoken

Generera åtkomsttoken antingen manuellt eller programmatiskt:

>[!BEGINTABS]

>[!TAB För testning]

Generera åtkomsttoken manuellt i Adobe Developer Console:

1. **Navigera till ditt projekt**
   1. Öppna ditt projekt i Adobe Developer Console
   2. Klicka på **OAuth Server-to-Server**

2. **Generera åtkomsttoken**
   1. Klicka på knappen **&quot;Generera åtkomsttoken&quot;** i projektets API-avsnitt
   2. Kopiera genererad åtkomsttoken

   ![Generera åtkomsttoken](/help/forms/assets/adc-access-token.png)

   >[!NOTE]
   >
   > Åtkomsttoken är endast giltig i **24 timmar**

>[!TAB För produktion]

Generera tokens programmatiskt med [Adobe IMS](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/security/setting-up-ims-integrations-for-aem-as-a-cloud-service) API:

**Nödvändiga autentiseringsuppgifter:**

* Klient-ID
* Klienthemlighet
* Omfång (vanligtvis: `openid, AdobeID, read_organizations, additional_info.projectedProductContext, read_pc.dma_aem_cloud, aem.document`)

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
> Om du vill veta mer om OAuth Server-till-Server-implementering för att generera åtkomsttoken och göra API-anrop [klickar du här](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation).

## God praxis: Hantera autentiseringsuppgifter för utveckling, mellanlagring och produktion

* Använd alltid separata autentiseringsuppgifter för utveckling, mellanlagring och produktion.

* Mappa alla autentiseringsuppgifter till rätt URL för AEM-miljön.

* Lagra hemligheter på ett säkert sätt och implementera dem aldrig i källkontrollen.

* Giltigheten för spåråtkomsttoken, eftersom tokens endast är giltiga i 24 timmar.

## Nästa steg

Mer information om hur du konfigurerar miljö för synkrona Forms Communication API:er finns i [Synkron bearbetning i AEM Forms as a Cloud Service Communications](/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md).


## Relaterade artiklar

Lär dig hur du ställer in miljön för API:er för synkron (On-Demand) och asynkron (Batch) Forms Communications:

<!-- START CARDS HTML - DO NOT MODIFY BY HAND -->
<div class="columns">
    <!-- Synchronous APIs Card -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="AEM Forms Communications APIs - Synchronous">
        <div class="card" style="height: 100%; display: flex; flex-direction: column;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" title="Synkrona API:er" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="/help/forms/assets/sync-api.png" alt="Synkrona API:er"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" target="_self" rel="referrer" title="AEM Forms Communications API:er - Synkrona">API:er för AEM Forms Communications - Synkron</a>
                    </p>
                    <p class="is-size-6">Lär dig hur du konfigurerar miljö för Synkrona (on-demand) API:er för Forms Communications som genererar eller bearbetar dokument direkt. </p>
                </div>
                <a href="/help/forms/aem-forms-cloud-service-communications-on-demand-processing.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Läs mer</span>
                </a>
            </div>
        </div>
    </div>
    <!-- Asynchronous APIs Card -->
    <div class="column is-half-tablet is-half-desktop is-one-third-widescreen" aria-label="AEM Forms Communications APIs - Asynchronous">
        <div class="card" style="height: 100%; display: flex; flex-direction: column;">
            <div class="card-image">
                <figure class="image x-is-16by9">
                    <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" title="AEM Forms Communications API:er - asynkrona" target="_self" rel="referrer">
                        <img class="is-bordered-r-small" src="/help/forms/assets/async-api.png" alt="Asynkrona API:er"
                             style="width: 100%; aspect-ratio: 16 / 9; object-fit: cover; overflow: hidden; display: block; margin: auto;">
                    </a>
                </figure>
            </div>
            <div class="card-content is-padded-small" style="display: flex; flex-direction: column; flex-grow: 1; justify-content: space-between;">
                <div class="top-card-content">
                    <p class="headline is-size-6 has-text-weight-bold">
                        <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" target="_self" rel="referrer" title="Asynkrona API:er">AEM Forms Communications API:er - asynkron (batch)</a>
                    </p>
                    <p class="is-size-6">Lär dig hur du konfigurerar miljö för asynkrona (Batch) Forms Communications API:er som genererar eller bearbetar flera dokument på ett schemalagt sätt.</p>
                </div>
                <a href="/help/forms/aem-forms-cloud-service-communications-batch-processing.md" target="_self" rel="referrer" class="spectrum-Button spectrum-Button--outline spectrum-Button--primary spectrum-Button--sizeM" style="align-self: flex-start; margin-top: 1rem;">
                    <span class="spectrum-Button-label has-no-wrap has-text-weight-bold">Läs mer</span>
                </a>
            </div>
        </div>
    </div>
</div>
<!-- END CARDS HTML - DO NOT MODIFY BY HAND -->


