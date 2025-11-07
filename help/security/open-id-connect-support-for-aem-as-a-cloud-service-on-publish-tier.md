---
title: Open ID Connect-stöd för AEM as a Cloud Service på publiceringsnivå
description: Lär dig hur du konfigurerar OIDC (Open ID Connect) för AEM as a Cloud Service på publiceringsnivå
feature: Security
role: Admin
exl-id: d2f30406-546c-4a2f-ba88-8046dee3e09b
source-git-commit: 2e257634313d3097db770211fe635b348ffb36cf
workflow-type: tm+mt
source-wordcount: '1469'
ht-degree: 0%

---

# Open ID Connect-stöd för AEM as a Cloud Service på publiceringsnivå {#open-id-connect-support-for-aem-as-a-cloud-service-on-publish-tier}

## Introduktion {#introduction}

När organisationer moderniserar sina digitala upplevelser blir säker och skalbar identitetshantering ett grundläggande krav. Adobe Experience Manager (AEM) Cloud Service har nu stöd för OpenID Connect (OIDC) på publiceringsnivån, vilket möjliggör smidig och standardbaserad integrering med ledande identitetsleverantörer (IdPs) som Entra ID (Azure AD), Google, Okta, Auth0, Ping Identity, ForgeRock och OIDC-stödda IDP:er.

OIDC är ett identitetslager ovanpå OAuth 2.0-protokollet som möjliggör robust användarautentisering samtidigt som utvecklarna behåller sin enkelhet. Den används ofta för B2C-scenarier (business-to-Consumer), intranät och partnerportalscenarier, där säker användarinloggning och identitetsfederationer krävs.

Fram tills nu var AEM-kunder ansvariga för att implementera sin egen anpassade inloggningslogik på publiceringsnivån, vilket ökade utvecklingstiden och innebar långsiktiga problem med underhåll och säkerhet. Med inbyggt stöd för OIDC tar AEM Cloud Service bort denna börda genom att tillhandahålla en säker, utbyggbar och Adobe-stödd autentiseringsmekanism för slutanvändare som använder publiceringsmiljöer.

Oavsett om ni levererar en personaliserad konsumentwebbplats eller en autentiserad intern portal förenklar OIDC on Publish identitetsfederation och minskar riskerna genom centraliserad identitetsstyrning. Det hjälper också organisationer att uppfylla moderna efterlevnads- och säkerhetsstandarder utan att offra flexibiliteten.

## Konfigurera AEM för OIDC-autentisering {#configure-aem-oidc-authentication}

### Förutsättningar {#prerequisits}

Vi antar att följande information är tillgänglig eller definierad:

1. Sökvägarna till det innehåll som ska skyddas i AEM-databasen
1. En identifierare för den IdP som ska konfigureras. Detta kan vara vilken sträng som helst

Information från IdP-konfigurationen:

1. Klient-ID som konfigurerats i IdP
1. Klienthemligheten som konfigurerats i IdP. Om PKCE har konfigurerats på IdP är inte klienthemligheten tillgänglig. Lagra inte värdet för oformaterad text i konfigurationsfilen. Använd en CM-hemlighet och referera till den
1. De scope som konfigurerats på IdP:n. Minst omfånget `openid` måste anges
1. Om PKCE är aktiverat på IdP
1. `callbackUrl` definieras med en av de konfigurerade sökvägar som definieras i punkt 1 och lägger till suffixet: `/j_security_check`
1. `baseUrl` som ska få åtkomst till standardfilen `.well-known`. Om den välkända URL:en till exempel är: `https://login.microsoftonline.com/53279d7a-438f-41cd-a6a0-fdb09efc8891/v2.0/.well-known/openid-configuration` är `baseUrl`: `https://login.microsoftonline.com/53279d7a-438f-41cd-a6a0-fdb09efc8891`

### Översikt över konfigurationsfilerna {#overview-of-the-configuration-files}

Nedan finns en lista över filer som behöver konfigureras:

1. **OIDC-anslutning**: detta används av `OidcAuthenticationHandler` för att autentisera användarna, eller av andra komponenter för att [auktorisera åtkomst till resurser som skyddas av IdP med OAuth](https://github.com/apache/sling-org-apache-sling-auth-oauth-client)
1. **OIDC-autentiseringshanterare**: Detta är den autentiseringshanterare som används för att autentisera användare som har åtkomst till de konfigurerade sökvägarna
1. **UserInfoProcessor**: Den här komponenten bearbetar informationen som tagits emot av IdP:en. Den kan utvidgas av kunder för att implementera anpassad logik
1. [**Standardhanterare för synkronisering**](https://jackrabbit.apache.org/oak/docs/security/authentication/external/defaultusersync.html): Den här komponenten skapar användaren i databasen
1. [**ExternalLoginModule**](https://jackrabbit.apache.org/oak/docs/security/authentication/externalloginmodule.html): Den här komponenten autentiserar användaren i den lokala ekalagret.

I följande diagram visas hur de angivna konfigurationselementen är kopplade. Observera att eftersom dessa är `ServiceFactory`-komponenter kan `~uniqueid` vara vilken slumpmässig unik sträng som helst:

![OIDC-konfigurationsdiagram](/help/security/assets/oidc-diagram.png)

### Konfigurera OIDC-anslutningen {#configure-the-oidc-connection}

Först måste vi konfigurera OIDC-anslutningen. Flera OIDC-anslutningar kan konfigureras och måste ha olika namn.

1. Skapa en ny `.cfg.json`-fil som lagrar konfigurationen. Du kan till exempel använda `org.apache.sling.auth.oauth_client.impl.OidcConnectionImpl~azure.cfg.json` - suffixet **azure** måste vara en unik identifierare för anslutningen
1. Följ konfigurationsformatet i exemplet nedan:

   ```
   {
    "name":"azure",
    "scopes":[
      "openid"
    ],
    "baseUrl":"<https://login.microsoftonline.com/53279d7a-438f-41cd-a6a0-fdb09efc8891/v2.0>",
    "clientId":"5199fc45-8000-473e-ac63-989f1a78759f",
    "clientSecret":"xxxxxx"
   }
   ```

1. Konfigurera egenskaperna enligt följande:
   * **&quot;name&quot;** kan definieras av användaren
   * `baseUrl`, `clientid` och `clientSecret` är konfigurationsvärden som kommer från IdP:en.
   * Omfattningarna måste innehålla minst värdet `openid`.

### Konfigurera OIDC-autentiseringshanterare {#configure-oidc-authentication-handler}

Konfigurera nu OIDC-autentiseringshanteraren. Flera OIDC-anslutningar kan konfigureras. Var och en måste ha olika namn. Om de delar samma [OAK-externa identitetsleverantör](https://jackrabbit.apache.org/oak/docs/security/authentication/identitymanagement.html) kan de dela användare.

1. Skapa konfigurationsfilen. I det här exemplet använder vi `org.apache.sling.auth.oauth_client.impl.OidcAuthenticationHandler~azure.cfg.json`. `azure`-suffixet måste vara en unik identifierare. Se ett exempel på konfigurationsfilen nedan:

   ```
   {
     "path":"/content/tests/us/en/test-7",
     "callbackUri":"http://localhost:14503/content/tests/us/en/test-7/j_security_check",
     "pkceEnabled":false,
     "defaultConnectionName":"azure"
     "idp": "azure-idp"
   }
   ```

1. Konfigurera sedan egenskaperna enligt följande:
   * `path`: sökvägen som ska skyddas
   * `callbackUri`: Lägg till suffixet `/j_security_check` i sökvägen som ska skyddas.
   * `defaultConnectionName`: konfigurera med samma namn som definierats för OIDC-anslutningen i föregående steg+
   * `pkceEnabled`: `true` Korrekturnyckel för Kodutbyte (PKCE) i auktoriseringskodflöde
   * `idp`: namnet på [OAK-providern för extern identitet](https://jackrabbit.apache.org/oak/docs/security/authentication/identitymanagement.html). Observera att olika OAK IDP inte kan dela användare eller grupper

### Konfigurera SlingUserInfoProcessor

1. Skapa konfigurationsfilen. I det här exemplet använder vi `org.apache.sling.auth.oauth_client.impl.SlingUserInfoProcessor~azure.cfg.json`. `azure`-suffixet måste vara en unik identifierare. Se ett exempel på konfigurationsfilen nedan:

   ```
   {
      "groupsInIdToken":true,
      "groupsClaimName": "groups",
      "connection":"azure",
      "storeAccessToken": false,
      "storeRefreshToken": false
   }
   ```

1. Konfigurera sedan egenskaperna enligt följande:
   * `groupsInIdToken`: Ange som true om grupperna skickas i ID-token. Om värdet är false, eller inte anges, läses grupperna från UserInfo-slutpunkten.
   * `groupsClaimName`: Anspråkets namn innehåller de grupper som ska synkroniseras i AEM.
   * `connection`: konfigurera med samma namn som definierats för OIDC-anslutningen i föregående steg
   * `storeAccessToken`: true om åtkomsttoken måste lagras i databasen. Som standard är detta false. Ställ bara in det på true om AEM behöver komma åt resurser för användaren som lagras i externa servrar som skyddas av samma IdP.
   * `storeRefreshToken`: true om uppdateringstoken måste lagras i databasen. Som standard är detta false. Ställ bara in det på true om AEM behöver komma åt resurser för användarens räkning som lagras på externa servrar som skyddas av samma IdP och behöver uppdatera token från IdP:n.
Observera att Access Token och Refresh Token lagras krypterade med AEM huvudnyckel.


### Konfigurera synkroniseringshanteraren {#configure-the-synchronization-handler}

Minst en synkroniseringshanterare måste vara konfigurerad för att synkronisera de användare som är autentiserade i eken. Mer information finns på sidan [this](https://jackrabbit.apache.org/oak/docs/security/authentication/external/defaultusersync.html).

Skapa en fil med namnet `org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler~azure.cfg.json`. Suffixet **azure** måste vara en unik identifierare. Mer information om hur du konfigurerar egenskaperna finns i [dokumentationen för Oak användar- och gruppsynkronisering](https://jackrabbit.apache.org/oak/docs/security/authentication/external/defaultusersync.html). Du hittar en exempelkonfiguration nedan:

```
{
  "user.expirationTime":"300s",
  "user.membershipExpTime":"300s",
  "user.propertyMapping":[
    "profile/familyName=profile/familyName",
    "profile/givenName=profile/givenName",
    "rep:fullname=cn",
    "profile/email=profile/email",
    "oauth-tokens"
  ],
  "user.pathPrefix":"azure",
  "handler.name":"azure"
}
```

Nedan visas några av de mest relevanta attributen som ska konfigureras i DefaultSyncHandler. Observera att dynamiskt gruppmedlemskap alltid ska vara aktiverat i molntjänster.

| Egenskapsnamn | Anteckningar | Föreslaget värde |
|---|---|---|
| `user.expirationTime` | Varaktighet tills en synkroniserad användare går ut. Användare synkroniseras först efter förfallotiden. | 1h |
| `user.membershipExpTime` | Varaktighet tills ett synkroniserat användarmedlemskap går ut. Användarmedlemskap synkroniseras först efter förfallotiden. | 1h |
| `user.dynamicMembership` | Vi rekommenderar att du aktiverar dynamiskt gruppmedlemskap | true |
| `user.enforceDynamicMembership` | Vi rekommenderar att man aktiverar ett dynamiskt gruppmedlemskap | true |
| `group.dynamicGroups` | Vi rekommenderar att du aktiverar dynamiska grupper | true |
| user.propertyMapping | Den tillhandahållna implementeringen av `UserInfoProcessor` synkroniserar bara ett fåtal egenskaper. Den kan ändras och anpassas. | <code>&quot;profile/givenName=profile/given_name&quot;,</code><br><code>&quot;profile/familyName=profile/family_name&quot;,</code><br><code>&quot;rep:fullname=profile/name&quot;,</code><br><code>&quot;profile/email=profile/email&quot;,</code><br><code>&quot;access_token=access_token&quot;,</code><br><code>&quot;refresh_token=refresh_token&quot;</code> |
| `user.membershipNestingDepth` | Returnerar det maximala djupet för gruppkapsling när medlemsrelationer synkroniseras. Värdet 0 inaktiverar sökning efter gruppmedlemskap. Värdet 1 lägger bara till en användares direktgrupper. Det här värdet har ingen effekt vid synkronisering av enskilda grupper endast när en användares medlemskapshistorik synkroniseras. | 1 |

### Konfigurera modulen för extern inloggning {#configure-the-external-login-module}

Slutligen måste du konfigurera modulen för extern inloggning.

1. Skapa en fil med namnet `org.apache.jackrabbit.oak.spi.security.authentication.external.impl.ExternalLoginModuleFactory~azure.cfg.json`. Se exempelkonfigurationen nedan:

   ```
   {
    "sync.handlerName":"azure",
    "idp.name":"azure-idp"
   }
   ```

1. Konfigurera egenskaperna enligt följande:

   * `sync.handlerName`: namn på synkroniseringshanteraren som definierats tidigare
   * `idp.name`: OAK-identitetsleverantör har definierats i OIDC-autentiseringshanterare

### Valfritt: Implementera en anpassad UserInfoProcessor {#implement-a-custom-userinfoprocessor}

Användaren autentiseras av en ID-token och ytterligare attribut hämtas i `userInfo`-slutpunkten som är definierad för IdP. Om ytterligare icke-standardåtgärder måste utföras är en anpassad implementering av [UserInfoProcessor](https://github.com/apache/sling-org-apache-sling-auth-oauth-client/blob/master/src/main/java/org/apache/sling/auth/oauth_client/impl/SlingUserInfoProcessorImpl.java) standardimplementeringen från Sling.

## Exempel: Konfigurera OIDC-autentisering med Azure Active Directory

### Konfigurera ett nytt program i Azure Active Directory {#configure-a-new-application-in-azure-ad}

1. Skapa ett nytt program i Azure Active Directory genom att följa [Azure Active Directory-dokumentationen](https://learn.microsoft.com/en-us/power-pages/security/authentication/openid-settings#create-an-app-registration-in-azure).  Se nedan hur skärmen som visar programöversikten ska se ut:

   ![Programöversikt](/help/security/assets/odic-application-overview.png)

1. Om grupper eller programroller krävs följer du [dokumentationen](https://learn.microsoft.com/en-us/entra/external-id/customers/how-to-use-app-roles-customers) för att aktivera dem för programmet och skicka dem i ID-token. Nedan visas ett exempel på konfigurerade grupper:

![ID för OIDC-anspråkstoken](/help/security/assets/oidc-claim-id-token.png)

1. Följ de tidigare dokumenterade stegen för att skapa de konfigurationsfiler som krävs. Nedan finns ett exempel som är specifikt för Azure AD där:
   * Vi definierar namnet på oidc-anslutningen, autentiseringshanteraren och DefaultSyncHandler som: `azure`
   * Webbplatsens URL är: `www.mywebsite.com`
   * Vi skyddar sökvägen `/content/wknd/us/en/adventures`
   * Innehavaren är: `tennat-id`,
   * Klient-ID: `client-id`,
   * Hemligheten är: `secret`,
   * Grupperna skickas i ID-token i ett anspråk med namnet: `groups`

#### org.apache.sling.auth.oauth_client.impl.OidcConnectionImpl~azure.cfg.json

```
{
  "name":"azure",
  "scopes":[
    openid", "User.Read", "profile", "email
  ],
  "baseUrl":"https://login.microsoftonline.com/tenant-id/v2.0",
  "clientId":"client-id",
  "clientSecret":"secret"
}
```

#### org.apache.sling.auth.oauth_client.impl.OidcAuthenticationHandler~azure.cfg.json

```
{
  "callbackUri":"https://www.mywebsite.com/content/wknd/us/en/adventures/j_security_check",
  "path":[
    "/content/wknd/us/en/adventures"
  ],
  "idp":"azure",
  "defaultConnectionName":"azure"
}
```

#### org.apache.jackrabbit.oak.spi.security.authentication.external.impl.ExternalLoginModuleFactory~azure.cfg.json

```
{
  "sync.handlerName":"azure",
  "idp.name":"azure"
}
```

#### org.apache.jackrabbit.oak.spi.security.authentication.external.impl.DefaultSyncHandler~azure.cfg.json

```
{
  "user.expirationTime":"1s",
  "user.membershipExpTime":"1s",
  "user.propertyMapping":[
    "profile/givenName=profile/given_name",
    "profile/familyName=profile/family_name",
    "rep:fullname=profile/name",
    "profile/email=profile/email",
    "access_token=access_token",
    "refresh_token=refresh_token"
  ],
  "user.pathPrefix":"azure",
  "group.pathPrefix": "oidc",
  "user.membershipNestingDepth": "1",
  "handler.name":"azure"
}
```

#### org.apache.sling.auth.oauth_client.impl.SlingUserInfoProcessorImpl~azure.cfg.json

```
{
  "groupsInIdToken": "true",
  "storeAccessToken": "false",
  "storeRefreshToken": "false",
  "connection": "azure",
  "groupsClaimName": "groups"
}
```

### Ytterligare information om Azure AD Groups {#additional-information-about-azure-ad-groups}

Om du vill konfigurera en grupp för företagsprogrammet i Microsoft Azure Portal måste du söka i programmet på: **Enterprise Applications** och lägga till grupperna: <!-- Alexandru: this bit cound be clearer-->

![OIDC-grupptillägg](/help/security/assets/oidc-ad-additional-info.png)

Om du vill aktivera gruppanspråket i Id-token lägger du till anspråket i avsnittet **Token Configuration** i Microsoft Azure-portalen: <!-- Alexandru: this bit cound be clearer as well-->

![ID för OIDC-anspråkstoken](/help/security/assets/oidc-claim-id-token.png)

Konfigurationen för `SlingUserInfoProcessor` måste ändras på samma sätt som i exemplet nedan.

Filnamnet som måste ändras är `org.apache.sling.auth.oauth_client.impl.SlingUserInfoProcessorImpl.cfg.json`. Innehållet ska konfigureras enligt följande:

```
{
  "connection": "azure",
  "groupsInIdToken": "true",
  "storeAccessToken": "false",
  "storeRefreshToken": "false"
}
```
