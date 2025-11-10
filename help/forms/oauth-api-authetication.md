---
title: Hur konfigurerar jag OAuth Server-to-Server-autentisering?
description: Lär dig konfigurera OAuth Server-till-Server-autentisering för Adobe Experience Manager Forms as a Cloud Service
role: Admin, Developer, User
feature: Adaptive Forms, APIs & Integrations
hide: true
hidefromToC: true
index: false
source-git-commit: 69704ca8de41c655b59ce6652a4a43b788ba75ec
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 0%

---


# OAuth Server-till-server-autentisering -Rekommenderad

OAuth Server-till-Server-autentisering ger säker, tokenbaserad åtkomst till AEM Forms Communications API:er utan att användaren behöver göra något. Den här metoden är idealisk för automatiserade system, backend-tjänster och integreringar som behöver autentiseras programmatiskt.

## Förutsättningar

Kontrollera att följande krav är uppfyllda innan du börjar:

* Kontrollera att du har tillgång till [Adobe Developer Console](https://developer.adobe.com/console) som är specifik för den miljö du använder.
* Tilldela systemadministratörs- eller utvecklarrollen i Adobe Admin Console för att aktivera åtkomst till Adobe Developer Console.

## Hur skapar man en åtkomsttoken med hjälp av OAuth Server-till-Server-autentisering?

Följ stegen nedan som visar hur du skapar en åtkomsttoken från Adobe Developer-konsolen och gör ditt första API-anrop via OAuth Server-to-Server-autentisering.


1. Navigera till [Adobe Developer Console](https://developer.adobe.com/console)
2. Logga in med din Adobe ID

3. Skapa nytt projekt eller navigera till ditt befintliga projekt

   **Så här skapar du ett nytt projekt:**

   1. Klicka på **Skapa nytt projekt** i avsnittet **Snabbstart**
   2. Ett nytt projekt skapas med ett standardnamn

      ![Skapa ADC-projekt](/help/forms/assets/adc-home.png)

   3. Klicka på **Redigera projekt** längst upp till höger

      ![Redigera projekt](/help/forms/assets/adc-edit-project.png)

   4. Ange ett beskrivande namn (t.ex. &quot;formsproject&quot;)
   5. Klicka på **Spara**

      ![Redigera projektnamn](/help/forms/assets/adc-edit-projectname.png)


   **Navigera till ditt befintliga projekt:**

   1. Klicka på **Alla projekt** i Adobe Developer Console

      ![Sökprojekt](/help/forms/assets/search-adc-project.png)

   2. Leta upp projektet och klicka för att öppna det.

      ![Hitta projekt](/help/forms/assets/locate-adc-project.png)


      >[!NOTE]
      >
      > Du kan lägga till API:t och autentiseringsmetoden i ditt befintliga projekt genom att klicka på **Lägg till i projekt** > **API**\
      > ![Lägg till API i befintligt projekt](/help/forms/assets/add-api-existing-project.png)
      > Om du vill lägga till API och autentiseringsmetod utför du samma steg som beskrivs nedan för ditt befintliga projekt.

4. Lägg till olika API:er för AEM Forms Communications beroende på dina behov.

   **A. För Document Services API:er**

   1. Klicka på **Lägg till API**

      ![Lägg till API](/help/forms/assets/adc-add-api.png)

   2. Välj **Forms Communication API:er**
      1. I dialogrutan _Lägg till API_ kan du filtrera efter **Experience Cloud**
      2. Välj **&quot;Forms Communication APIs&quot;**

         ![Lägg till Forms Communication API](/help/forms/assets/adc-add-forms-api.png)


   3. Välj autentiseringsmetoden **OAuth Server-till-server**

      ![Välj autentiseringsmetod](/help/forms/assets/adc-add-authentication-method.png)


   **B. För adaptiva Forms Runtime API:er**

   1. **Klicka på Lägg till API**
Klicka på knappen **Lägg till API** i ditt projekt

      ![Lägg till API](/help/forms/assets/adc-add-api.png)

   2. **Välj AEM Forms-leverans- och körnings-API**
      1. I dialogrutan _Lägg till API_ kan du filtrera efter **Experience Cloud**
      2. Välj **&quot;AEM Forms Delivery and Runtime API&quot;**
      3. Klicka på **Nästa**

   3. **Autentiseringsmetod**
Välj autentiseringsmetoden **OAuth Server-to-Server** .


      ![Välj autentiseringsmetod](/help/forms/assets/adc-add-authentication-method.png)

5. **Lägg till produktprofil**:

   1. Välj lämplig **produktprofil** utifrån den åtkomstnivå som krävs:

      | Åtkomsttyp | Produktprofil |
      |------------------|----------------------|
      | Skrivskyddad åtkomst | `AEM Users - author - Program XXX - Environment XXX` |
      | Läs-/skrivåtkomst | `AEM Assets Collaborator Users - author - Program XXX - Environment XXX` |
      | Fullständig administrativ åtkomst | `AEM Administrators - author - Program XXX - Environment XXX` |

   2. Välj den **produktprofil** som matchar URL:en för författartjänsten (`https://author-pXXXXX-eYYYYY.adobeaemcloud.com`). Välj till exempel `https://author-pXXXXX-eYYYYY.adobeaemcloud.com`.

   3. Klicka på **Spara konfigurerat API**. API och produktprofil läggs till i ditt projekt

      ![Välj projektkonfiguration](/help/forms/assets/adc-add-product-profile.png)

6. Generera och spara autentiseringsuppgifter

   1. Navigera till ditt projekt i Adobe Developer Console
   2. Klicka på autentiseringsuppgifter för **OAuth Server-till-Server**
   3. Visa avsnittet **Information om autentiseringsuppgifter**

      ![Visa autentiseringsuppgifter](/help/forms/assets/adc-view-credential.png)

   4. Post-API-autentiseringsuppgifter

      ```text
      API Credentials:
      ================
      Client ID: <your_client_id>
      Client Secret: <your_client_secret>
      Technical Account ID: <tech_account_id>
      Organization ID: <org_id>
      Scopes: AdobeID,openid,read_organizations
      ```

7. Generering av åtkomsttoken

   **A. För testning**

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

   **B. För produktion**

   Generera tokens programmatiskt med Adobe IMS API:

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

Du kan nu använda den genererade åtkomsttoken för att göra API-anrop för utvecklings-, scen- eller produktionsmiljöer.

>[!NOTE]
>
> Om du vill veta mer om OAuth Server-till-Server-implementering för att generera åtkomsttoken och göra API-anrop [klickar du här](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation).

## Nästa steg

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


