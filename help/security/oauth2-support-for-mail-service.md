---
title: OAuth2-stöd för e-posttjänsten
description: Oauth2-stöd för e-posttjänsten i Adobe Experience Manager as a Cloud Service
exl-id: 93e7db8b-a8bf-4cc7-b7f0-cda481916ae9
source-git-commit: 5f8da9f846c159aa00273909b93aa10358daf609
workflow-type: tm+mt
source-wordcount: '674'
ht-degree: 0%

---

# OAuth2-stöd för e-posttjänsten {#oauth2-support-for-the-mail-service}

AEM as a Cloud Service erbjuder OAuth2-stöd för sin integrerade e-posttjänst, så att organisationer kan följa e-postkraven.

Du kan konfigurera OAuth för flera e-postleverantörer. Nedan visas steg-för-steg-instruktioner för hur du konfigurerar AEM Mail Service för att autentisera via OAuth2 med Microsoft Office 365 Outlook. Andra leverantörer kan konfigureras på liknande sätt.

Mer information om AEM as a Cloud Service Mail Service finns i [Skickar e-post](/help/implementing/developing/introduction/development-guidelines.md#sending-email).

## Microsoft Outlook {#microsoft-outlook}

1. Gå till [https://portal.azure.com/](https://portal.azure.com/) och logga in.
1. Sök efter **Azure Active Directory** i sökfältet och klicka på resultatet. Du kan även bläddra direkt till [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. Klicka på **Appregistrering** - **Ny registrering**

   ![](assets/oauth-outlook1.png)

1. Fyll i informationen enligt dina krav och klicka sedan på **Registrera**
1. Gå till den nya appen och välj **API-behörigheter**
1. Gå till **Lägg till behörighet** - **Diagrambehörighet** - **Delegerade behörigheter**
1. Välj behörigheter nedan för din app och klicka sedan på **Lägg till behörighet**:
   * `SMTP.Send`
   * `Mail.Read`
   * `Mail.Send`
   * `openid`
   * `offline_access`
1. Gå till **Autentisering** - **Lägg till en plattform** - **Webb** och i **Omdirigerings-URL** lägger du till nedanstående URL:er - en med och en utan snedstreck:
   * `http://localhost/`
   * `http://localhost`
1. Tryck **Konfigurera** efter att du lagt till varje URL-adress och konfigurerat inställningarna enligt dina önskemål
1. Nästa, gå till **Certifikat och hemligheter**, klicka på **Ny klienthemlighet** och följ stegen på skärmen för att skapa en hemlighet. Observera denna hemlighet för senare bruk
1. Tryck **Översikt** i den vänstra rutan och kopiera värdena för **Program-ID (klient)** och **Katalog-ID (klientorganisation)** för senare användning

För att komma tillbaka behöver du följande information för att konfigurera OAuth2 för e-posttjänsten på AEM sida:

* Autentiserings-URL:en som skapas med klientorganisations-ID:t. Den kommer att ha följande formulär: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/authorize`
* Token URL, som skapas med klient-ID. Den kommer att ha följande formulär: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* Uppdaterings-URL:en som skapas med klient-ID:t. Den kommer att ha följande formulär: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* Klient-ID
* Klienthemlighet

### Genererar uppdateringstoken {#generating-the-refresh-token}

Därefter måste du generera uppdateringstoken, som kommer att ingå i OSGi-konfigurationen i ett senare steg.

Så här gör du:

1. Öppna följande URL i webbläsaren när du har ersatt den `clientID` och `tenantID` med de värden som är specifika för ditt konto: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/authorize?client_id=<clientId>&response_type=code&redirect_uri=http://localhost&response_mode=query&scope=https%3A%2F%2Foutlook.office365.com%2FSMTP.Send%20EWS.AccessAsUser.All%20https%3A%2F%2Foutlook.office365.com%2FSMTP.Send%20https%3A%2F%2Foutlook.office365.com%2FMail.Read%20https%3A%2F%2Foutlook.office365.com%2FMail.Send%20openid%20offline_access&state=12345`
1. Tillåt behörighet när du tillfrågas
1. URL:en kommer att omdirigeras till en ny plats som har följande format: `http://localhost/?code=<code>&state=12345&session_state=4f984c6b-cc1f-47b9-81b2-66522ea83f81#`
1. Kopiera värdet för `<code>` i exemplet ovan
1. Använd följande cURL-kommando för att hämta refreshToken. Du måste ersätta tenantID, clientID och clientSecret med värdena för ditt konto, samt värdet för `<code>`:

   ```
   curl --location --request POST 'https://login.microsoftonline.com/<tenantId>/oauth2/v2.0/token' \
   --header 'Content-Type: application/x-www-form-urlencoded' \
   --header 'Cookie: buid=0.ARgAep0nU49DzUGmoP2wnvyIkcQjsx26HEpOnvHS0akqXQgYAAA.AQABAAEAAAD--DLA3VO7QrddgJg7Wevry9XPJSKbGVlPt5NWYxLtTl3K1W0LwHXelrffApUo_K02kFrkvmGm94rfBT94t25Zq4bCd5IM3yFOjWb3V22yDM7-rl112sLzbBQBRCL3QAAgAA; esctx=AQABAAAAAAD--DLA3VO7QrddgJg7Wevr4a8wBjYcNbBXRievdTOd15caaeAsQdXeBAQA3tjVQaxmrOXFGkKaE7HBzsJrzA-ci4RRpor-opoo5gpGLh3pj_iMZuqegQPEb1V5sUVQV8_DUEbBv5YFV2eczS5EAhLBAwAd1mHx6jYOL8LwZNDFvd2-MhVXwPd6iKPigSuBxMogAA; x-ms-gateway-slice=estsfd; stsservicecookie=estsfd; fpc=Auv6lTuyAP1FuOOCfj9w0U_5vR5dAQAAALDXP9gOAAAAwIpkkQEAAACT2T_YDgAAAA' \
   --data-urlencode 'client_id=<clientID>' \
   --data-urlencode 'scope=https://outlook.office365.com/SMTP.Send https://outlook.office365.com/Mail.Read https://outlook.office365.com/Mail.Send openid' \
   --data-urlencode 'redirect_uri=http://localhost' \
   --data-urlencode 'grant_type=authorization_code' \
   --data-urlencode 'client_secret=<clientSecret>' \
   --data-urlencode 'code=<code>'
   ```

1. Notera refreshToken och accessToken.

### Validerar token {#validating-the-tokens}

Innan du fortsätter att konfigurera OAuth på AEM-sidan måste du verifiera både accessToken och refreshToken med proceduren nedan:

1. Generera accessToken med hjälp av den refreshToken som skapades i föregående procedur. Du kan uppnå detta med följande kurva och ersätta värdena för `<client_id>`,`<client_secret>` och `<refreshToken>`:

   ```
   curl --location --request POST 'https://login.microsoftonline.com/<tenetId>/oauth2/v2.0/token' \
   --header 'Content-Type: application/x-www-form-urlencoded' \
   --header 'Cookie: buid=0.ARgAep0nU49DzUGmoP2wnvyIkcQjsx26HEpOnvHS0akqXQgYAAA.AQABAAEAAAD--DLA3VO7QrddgJg7Wevry9XPJSKbGVlPt5NWYxLtTl3K1W0LwHXelrffApUo_K02kFrkvmGm94rfBT94t25Zq4bCd5IM3yFOjWb3V22yDM7-rl112sLzbBQBRCL3QAAgAA; esctx=AQABAAAAAAD--DLA3VO7QrddgJg7Wevr4a8wBjYcNbBXRievdTOd15caaeAsQdXeBAQA3tjVQaxmrOXFGkKaE7HBzsJrzA-ci4RRpor-opoo5gpGLh3pj_iMZuqegQPEb1V5sUVQV8_DUEbBv5YFV2eczS5EAhLBAwAd1mHx6jYOL8LwZNDFvd2-MhVXwPd6iKPigSuBxMogAA; x-ms-gateway-slice=estsfd; stsservicecookie=estsfd; fpc=Auv6lTuyAP1FuOOCfj9w0U_IezHLAQAAAPeNSdgOAAAA' \
   --data-urlencode 'client_id=<client_id>' \
   --data-urlencode 'scope=https://outlook.office365.com/SMTP.Send https://outlook.office365.com/Mail.Read https://outlook.office365.com/Mail.Send openid' \
   --data-urlencode 'redirect_uri=http://localhost' \
   --data-urlencode 'grant_type=refresh_token' \
   --data-urlencode 'client_secret=<client_secret>' \
   --data-urlencode 'refresh_token=<refreshToken>'
   ```

1. Skicka ett e-postmeddelande med accessToken för att se om fungerar som det ska.

>[!NOTE]
>
> Du kan hämta Postman API-samlingen från [den här platsen](https://docs.microsoft.com/en-us/azure/active-directory/develop/v2-oauth2-auth-code-flow).

### Integrering med AEM as a Cloud Service {#integration-with-aem-as-a-cloud-service}

1. Skapa en OSGI-egenskapsfil med namnet `com.day.cq.mailer.oauth.impl.OAuthConfigurationProviderImpl.cfg.json` under `/apps/<my-project>/osgiconfig/config` med följande syntax:

   ```
   {
       authUrl: "<Authorization Url>",
       tokenUrl: "<Token Url>",
       clientId: "<clientID>",
       clientSecret: "$[secret:SECRET_SMTP_OAUTH_CLIENT_SECRET]",
       scopes: [
          "scope1",
          "scope2"
       ],
       refreshUrl: "<Refresh token Url>",
       refreshToken: "$[secret:SECRET_SMTP_OAUTH_REFRESH_TOKEN]"
   }
   ```

1. Fyll i `authUrl`, `tokenUrl` och `refreshURL` genom att konstruera dem enligt beskrivningen i föregående avsnitt.
1. Lägg till följande scope i konfigurationen:
   * `openid`
   * `offline_access`
   * `https://outlook.office365.com/Mail.Send`
   * `https://outlook.office365.com/Mail.Read`
   * `https://outlook.office365.com/SMTP.Send`
1. Skapa en OSGI-egenskapsfil `called com.day.cq.mailer.DefaultMailService.cfg.json`
under 
`/apps/<my-project>/osgiconfig/config`  med följande syntax:

   ```
   {
    "smtp.host": "<smtp hostname>"
    "smtp.user": "<user account that logged into get the oauth tokens>",
    "smtp.password": "value not used",
    "smtp.port": 587,
    "from.address": "<from address used for sending>"
    "smtp.ssl": false,
    "smtp.starttls": true,
    "smtp.requiretls": true,
    "debug.email": false,
    "oauth.flow": true
   }
   ```

1. För Outlook gäller följande `smtp.host` konfigurationsvärdet är `smtp.office365.com`
1. Vid körning skickar du `refreshToken values` och `clientSecret` hemligheter med Cloud Manager-variablernas API enligt beskrivningen [här](/help/implementing/deploying/configuring-osgi.md#setting-values-via-api). Värdena för variablerna `SECRET_SMTP_OAUTH_REFRESH_TOKEN`  och `SECRET_SMTP_OAUTH_CLIENT_SECRET` ska definieras.

### Felsökning {#troubleshooting}

Om e-posttjänsten inte fungerar som den ska måste du i de flesta fall generera om `refreshToken` så som beskrivs ovan, skicka det nya värdet via Cloud Manager API. Det kommer att ta några minuter innan det nya värdet distribueras.
