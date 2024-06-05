---
title: OAuth2-stöd för e-posttjänsten
description: OAuth2-stöd för e-posttjänsten i Adobe Experience Manager som en molntjänst.
exl-id: 93e7db8b-a8bf-4cc7-b7f0-cda481916ae9
feature: Security
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '679'
ht-degree: 0%

---


# OAuth2-stöd för e-posttjänsten {#oauth2-support-for-the-mail-service}

AEM as a Cloud Service erbjuder OAuth2-stöd för den integrerade e-posttjänsten så att organisationer kan följa e-postkraven.

Du kan konfigurera OAuth för flera e-postleverantörer. Nedan finns stegvisa instruktioner för hur du konfigurerar AEM Mail Service för att autentisera via OAuth2 med Microsoft® Office 365 Outlook. Andra leverantörer kan konfigureras på liknande sätt.

Mer information om AEM as a Cloud Service Mail Service finns i [Skickar e-post](/help/implementing/developing/introduction/development-guidelines.md#sending-email).

## Microsoft® Outlook {#microsoft-outlook}

1. Gå till [https://portal.azure.com/](https://portal.azure.com/) och logga in.
1. Sök efter **Azure Active Directory** i sökfältet och klicka på resultatet. Du kan även bläddra direkt till [https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview)
1. Klicka **Appregistrering** > **Ny registrering**.

   ![Starta appregistreringsprocessen](assets/oauth-outlook1.png)

1. Fyll i informationen enligt dina krav och klicka sedan **Registrera**.
1. Gå till den skapade appen och välj **API-behörigheter**.
1. Klicka **Lägg till behörighet** > **Diagrambehörighet** > **Delegerade behörigheter**.
1. Välj behörigheter nedan för din app och klicka sedan på **Lägg till behörighet**:

   >[!NOTE]
   >
   >Behörighetskonfigurationen kan förändras över tid. Arbeta med Microsoft® om dessa inte fungerar som förväntat.

   * `https://outlook.office.com/SMTP.Send`
   * `openid`
   * `offline_access`
   * `email`
   * `profile`
1. Gå till **Autentisering** > **Lägg till en plattform** > **Webb** och i **Omdirigerings-URL** lägger du till nedanstående URL:er - en med och en utan snedstreck:
   * `http://localhost/`
   * `http://localhost`
1. Tryck **Konfigurera** efter att du lagt till varje URL-adress och konfigurerat inställningarna enligt dina önskemål.
1. Nästa, gå till **Certifikat och hemligheter**, klicka **Ny klienthemlighet** och följ stegen på skärmen för att skapa en hemlighet. Observera denna hemlighet för senare bruk.
1. Tryck **Ökning** i den vänstra rutan och kopiera värdena för **Program-ID (klient)** och **Katalog-ID (klientorganisation)** för senare bruk.

Använd följande information för att konfigurera OAuth2 för e-posttjänsten på AEM sida:

* Autentiserings-URL:en, som skapas med klient-ID:t. Den har följande formulär: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/authorize`
* Token-URL, som skapas med klient-ID. Den har följande formulär: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* Uppdaterings-URL:en som skapas med klient-ID:t. Den har följande formulär: `https://login.microsoftonline.com/<tenantID>/oauth2/v2.0/token`
* Klient-ID
* Klienthemlighet

### Genererar uppdateringstoken {#generating-the-refresh-token}

Generera sedan uppdateringstoken, som är en del av OSGi-konfigurationen i ett efterföljande steg, genom att göra följande:

1. Öppna följande URL i webbläsaren när du har ersatt den `clientID` och `tenantID` med specifika värden för ditt konto:

   ```
   https://login.microsoftonline.com/%3ctenantID%3e/oauth2/v2.0/authorize?client_id=%3cclientId%3e&response_type=code&redirect_uri=http://localhost&response_mode=query&scope=https://outlook.office.com/SMTP.Send%20email%20openid%20profile%20offline_access&state=12345`
   ```

1. Tillåt tillstånd när du blir tillfrågad.
1. URL:en dirigeras om till en ny plats, som har följande format:

   ```
   http://localhost/?code=<code>&state=12345&session_state=4f984c6b-cc1f-47b9-81b2-66522ea83f81#`
   ```

1. Kopiera värdet för `<code>` i exemplet ovan.
1. Använd följande cURL-kommando för att hämta refreshToken. Ersätt tenantID, clientID och clientSecret med värdena för ditt konto och värdet för `<code>`:

   ```
   curl --location --request POST 'https://login.microsoftonline.com/<tenantId>/oauth2/v2.0/token' \
   --header 'Content-Type: application/x-www-form-urlencoded' \
   --header 'Cookie: buid=0.ARgAep0nU49DzUGmoP2wnvyIkcQjsx26HEpOnvHS0akqXQgYAAA.AQABAAEAAAD--DLA3VO7QrddgJg7Wevry9XPJSKbGVlPt5NWYxLtTl3K1W0LwHXelrffApUo_K02kFrkvmGm94rfBT94t25Zq4bCd5IM3yFOjWb3V22yDM7-rl112sLzbBQBRCL3QAAgAA; esctx=AQABAAAAAAD--DLA3VO7QrddgJg7Wevr4a8wBjYcNbBXRievdTOd15caaeAsQdXeBAQA3tjVQaxmrOXFGkKaE7HBzsJrzA-ci4RRpor-opoo5gpGLh3pj_iMZuqegQPEb1V5sUVQV8_DUEbBv5YFV2eczS5EAhLBAwAd1mHx6jYOL8LwZNDFvd2-MhVXwPd6iKPigSuBxMogAA; x-ms-gateway-slice=estsfd; stsservicecookie=estsfd; fpc=Auv6lTuyAP1FuOOCfj9w0U_5vR5dAQAAALDXP9gOAAAAwIpkkQEAAACT2T_YDgAAAA' \
   --data-urlencode 'client_id=<clientID>' \
   --data-urlencode 'scope=https://outlook.office.com/SMTP.Send https://graph.microsoft.com/Mail.Read https://graph.microsoft.com/Mail.Send https://graph.microsoft.com/User.Read email openid profile offline_access' \
   --data-urlencode 'redirect_uri=http://localhost' \
   --data-urlencode 'grant_type=authorization_code' \
   --data-urlencode 'client_secret=<clientSecret>' \
   --data-urlencode 'code=<code>'
   ```

1. Notera refreshToken och accessToken.

### Validerar token {#validating-the-tokens}

Innan du fortsätter att konfigurera OAuth på AEM-sidan måste du verifiera både accessToken och refreshToken med proceduren nedan:

1. Generera accessToken med hjälp av den refreshToken som skapades i föregående procedur genom att använda följande uttryck och ersätta värdena för `<client_id>`,`<client_secret>`och `<refreshToken>`:

   ```
   curl --location --request POST 'https://login.microsoftonline.com/<tenetId>/oauth2/v2.0/token' \
   --header 'Content-Type: application/x-www-form-urlencoded' \
   --header 'Cookie: buid=0.ARgAep0nU49DzUGmoP2wnvyIkcQjsx26HEpOnvHS0akqXQgYAAA.AQABAAEAAAD--DLA3VO7QrddgJg7Wevry9XPJSKbGVlPt5NWYxLtTl3K1W0LwHXelrffApUo_K02kFrkvmGm94rfBT94t25Zq4bCd5IM3yFOjWb3V22yDM7-rl112sLzbBQBRCL3QAAgAA; esctx=AQABAAAAAAD--DLA3VO7QrddgJg7Wevr4a8wBjYcNbBXRievdTOd15caaeAsQdXeBAQA3tjVQaxmrOXFGkKaE7HBzsJrzA-ci4RRpor-opoo5gpGLh3pj_iMZuqegQPEb1V5sUVQV8_DUEbBv5YFV2eczS5EAhLBAwAd1mHx6jYOL8LwZNDFvd2-MhVXwPd6iKPigSuBxMogAA; x-ms-gateway-slice=estsfd; stsservicecookie=estsfd; fpc=Auv6lTuyAP1FuOOCfj9w0U_IezHLAQAAAPeNSdgOAAAA' \
   --data-urlencode 'client_id=<client_id>' \
   --data-urlencode 'scope=https://outlook.office.com/SMTP.Send https://graph.microsoft.com/Mail.Read https://graph.microsoft.com/Mail.Send https://graph.microsoft.com/User.Read email openid profile offline_access' \
   --data-urlencode 'redirect_uri=http://localhost' \
   --data-urlencode 'grant_type=refresh_token' \
   --data-urlencode 'client_secret=<client_secret>' \
   --data-urlencode 'refresh_token=<refreshToken>'
   ```

1. Skicka ett e-postmeddelande med accessToken så att du kan se om det fungerar som det ska.

>[!NOTE]
>
> Du kan hämta Postman API-samlingen från [den här platsen](https://learn.microsoft.com/en-us/entra/identity-platform/v2-oauth2-auth-code-flow).
>
> Se MSFT OAuth-dokumentationen [här](https://learn.microsoft.com/en-us/exchange/client-developer/legacy-protocols/how-to-authenticate-an-imap-pop-smtp-application-by-using-oauth) för mer information.

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
       authCodeRedirectUrl: "http://localhost",
       refreshUrl: "<Refresh token Url>",
       refreshToken: "$[secret:SECRET_SMTP_OAUTH_REFRESH_TOKEN]"
   }
   ```

1. Fyll i `authUrl`, `tokenUrl`och `refreshURL` genom att konstruera dem enligt beskrivningen i föregående avsnitt.
1. Lägg till följande scope i konfigurationen:

   >[!NOTE]
   >
   >Omfattningar kan utvecklas över tid. Arbeta med Microsoft® om dessa inte fungerar som förväntat.

   * `https://outlook.office.com/SMTP.Send`
   * `openid`
   * `offline_access`
   * `email`
   * `profile`
1. Skapa en OSGI-egenskapsfil `called com.day.cq.mailer.DefaultMailService.cfg.json`
under `/apps/<my-project>/osgiconfig/config` med syntaxen nedan. The `smtp.host` och `smtp.port` värdena visar avancerad nätverkskonfiguration, vilket beskrivs i [Självstudiekurs om e-posttjänst](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/networking/examples/email-service).

   ```
   {
    "smtp.host": "$[env:AEM_PROXY_HOST;default=proxy.tunnel]",
    "smtp.user": "<user account that logged into get the oauth tokens>",
    "smtp.password": "value not used",
    "smtp.port": 30465,
    "from.address": "<from address used for sending>",
    "smtp.ssl": false,
    "smtp.starttls": true,
    "smtp.requiretls": true,
    "debug.email": false,
    "oauth.flow": true
   }
   ```

1. För Outlook gäller följande: `smtp.host` konfigurationsvärdet är `smtp.office365.com`
1. Vid körning skickas `refreshToken values` och `clientSecret` hemligheter med Cloud Manager-variablernas API enligt beskrivningen [här](/help/implementing/deploying/configuring-osgi.md#setting-values-via-api) eller genom att använda [Cloud Manager för att lägga till variabler.](/help/implementing/cloud-manager/environment-variables.md) Variabelvärdena `SECRET_SMTP_OAUTH_REFRESH_TOKEN`  och `SECRET_SMTP_OAUTH_CLIENT_SECRET` ska definieras.

### Felsökning {#troubleshooting}

Om e-posttjänsten inte fungerar som den ska måste du generera om `refreshToken` så som beskrivs ovan, skicka det nya värdet via Cloud Manager API. Det tar några minuter innan det nya värdet distribueras.
