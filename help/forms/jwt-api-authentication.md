---
title: Hur konfigurerar jag JWT-autentisering (JSON Web Token)?
description: Lär dig konfigurera JWT-autentisering (JSON Web Token) för Adobe Experience Manager Forms as a Cloud Service
role: Admin, Developer, User
feature: Adaptive Forms, APIs & Integrations
source-git-commit: d9eb9a93aba71a5ef5940c9d1d75cfd4e738c26b
workflow-type: tm+mt
source-wordcount: '384'
ht-degree: 0%

---


# JWT-serverautentisering (JSON Web Token)

JWT server-till-server-autentisering i AEM Forms, särskilt för serverintegration med AEM as a Cloud Service, innehåller en specifik process för säker interaktion med AEM tjänster. JWT server-till-server-autentisering stöds av AEM Developer Console.

## Förutsättningar

Kontrollera att följande krav är uppfyllda innan du börjar:

* Kontrollera att du har tillgång till [Adobe Cloud Manager](https://experience.adobe.com/#/@formsinternal01/cloud-manager/landing.html) som är specifik för den miljö du använder.
* Tilldela [systemadministratörs- eller utvecklarrollen för åtkomst till Adobe Cloud Manager](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-manager/content/requirements/access-rights).

## Hur skapar man en åtkomsttoken med JWT-referenser?

Följ stegen nedan som visar hur du genererar en åtkomsttoken från JWT-autentiseringsuppgifterna.

1. **Adobe Cloud Manager**

   1. Logga in på ditt [Cloud Manager-konto](https://experience.adobe.com/#/@formsinternal01/cloud-manager/landing.html).
   2. Klicka på **[!UICONTROL Program Overview]** på det valda programmet.

      ![Cloud Manager-konto](/help/forms/assets/jwt-cloud-manager-landing.png)

   3. Klicka på menyn med tre punkter i programmet och välj **[!UICONTROL Developer Console]**.

      ![Developer Console](/help/forms/assets/jwt-developer-console.png)

2. **AEM Developer Console**
   1. Logga in på AEM Developer Console
   2. Klicka på **[!UICONTROL Integrations]** som finns på den övre menyraden.

      ![Integrationer](/help/forms/assets/jwt-integrations.png)

   3. Klicka på alternativet för att **[!UICONTROL Create new technical account]**.

      ![Skapa nytt tekniskt konto](/help/forms/assets/jwt-creae-new-tech-account.png)

   När du klickar på Skapa ett nytt tekniskt konto, krävs information för att generera åtkomsttoken som klient-id och klienthemlighet tillsammans med annan teknisk kontoinformation som privat nyckel, offentlig nyckel och utgångsdatum genereras.

   ![JWT-autentiseringsuppgifter](/help/forms/assets/jwt-credentials.png)


3. **Generera och spara autentiseringsuppgifter**

   1. Post-API-autentiseringsuppgifter

      ```text
      API Credentials:
      ================
      Client ID: <your_client_id>
      Client Secret: <your_client_secret>
      Technical Account ID: <tech_account_id>
      Organization ID: <org_id>
      Scopes: AdobeID,openid,read_organizations
      ```

4. **Generera åtkomsttoken**

   Generera tokens programmatiskt med kommandot cURL:

   **Nödvändiga autentiseringsuppgifter:**

   * Klient-ID
   * Klienthemlighet
   * Omfång (vanligtvis: `openid, AdobeID, read_organizations, additional_info.projectedProductContext, read_pc.dma_aem_cloud, aem.document`)

   **Tokenslutpunkt:**

   ```
   https://ims-na1.adobelogin.com/ims/token/v3
   ```

   **Exempelbegäran (cURL):**

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


>[!NOTE]
>
> [Klicka här](https://experienceleague.adobe.com/en/docs/experience-manager-learn/getting-started-with-aem-headless/authentication/service-credentials) om du vill veta mer om tjänstens autentiseringsuppgifter och hur du genererar en åtkomsttoken med Adobe IMS API.

Du kan nu använda den genererade åtkomsttoken för att göra API-anrop för utvecklings-, scen- eller produktionsmiljöer.

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


