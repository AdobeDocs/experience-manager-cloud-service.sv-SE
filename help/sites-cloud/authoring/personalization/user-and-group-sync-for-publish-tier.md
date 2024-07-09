---
title: Registrering, inloggning och användarprofil
description: Läs mer om registrering, inloggning, användardata och gruppsynkronisering för AEM as a Cloud Service
exl-id: a991e710-a974-419f-8709-ad86c333dbf8
solution: Experience Manager Sites
feature: Authoring, Personalization
role: User
source-git-commit: 54159c25b60277268ade16b437891f268873fecf
workflow-type: tm+mt
source-wordcount: '1340'
ht-degree: 0%

---

# Registrering, inloggning och användarprofil {#registration-login-and-userprofile}

## Introduktion {#introduction}

Webbprogram har ofta funktioner för kontohantering så att slutanvändarna kan registrera sig på en webbplats som bevarar användarinformationen, vilket gör att de kan logga in i framtiden och få en konsekvent upplevelse. I den här artikeln beskrivs följande koncept för AEM as a Cloud Service:

* Registrering
* Inloggning
* Lagra användarprofildata
* Gruppmedlemskap
* Datasynkronisering

## Registrering {#registration}

När en slutanvändare registrerar sig för ett konto i ett AEM program skapas ett användarkonto på den AEM Publish-tjänsten, vilket återspeglas på en användarresurs under `/home/users` i JCR-databasen.

Det finns två sätt att genomföra registreringen, som beskrivs nedan.

### AEM hanterad {#aem-managed-registration}

Du kan skriva en egen registreringskod som innehåller användarens användarnamn och lösenord och som skapar en användarpost i AEM som sedan kan användas för att autentisera mot vid inloggning. Följande steg används vanligtvis för att konstruera den här registreringsmekanismen:

1. Visa en anpassad AEM som samlar in registreringsinformation
1. Vid inlämningen används en korrekt etablerad tjänstanvändare för
   1. Verifiera att en befintlig användare inte redan finns, med en av API:erna för UserManager `findAuthorizables()` metoder
   1. Skapa en användarpost med någon av API:erna för UserManager `createUser()` metoder
   1. Bevara alla profildata som samlats in med det redigerbara gränssnittets `setProperty()` metoder
1. Valfria flöden, som att kräva att användaren validerar sin e-post.

**Krav:**

För att ovanstående logik ska fungera korrekt måste du aktivera [datasynkronisering](#data-synchronization-data-synchronization) genom att skicka en begäran till kundsupporten där det anges vilket program och vilken miljö som är lämplig.

### Extern {#external-managed-registration}

I vissa fall har registrering eller skapande av användare tidigare skett i infrastruktur utanför AEM. I så fall skapas användarposten i AEM under inloggningen.

## Inloggning {#login}

När en slutanvändare har registrerats på AEM Publish-tjänst kan dessa användare logga in för att få autentiserad åtkomst (med hjälp av AEM autentiseringsmekanismer) och beständiga, användarspecifika data som profildata.

## Implementering {#implementation}

Inloggning kan implementeras med följande två metoder:

### AEM hanterad {#aem-managed-implementation}

Kunderna kan skriva egna komponenter. Om du vill veta mer kan du kanske börja lära dig mer om:

* The [Sling Authentication Framework](https://sling.apache.org/documentation/the-sling-engine/authentication/authentication-framework.html)
* Och fundera [fråga AEM Community Experts session](https://bit.ly/ATACEFeb15) om inloggning.

**Krav:**

För att ovanstående logik ska fungera korrekt måste du aktivera [datasynkronisering](#data-synchronization-data-synchronization) genom att skicka en begäran till kundsupporten där det anges vilket program och vilken miljö som är lämplig.

### Integrering med en identitetsleverantör {#integration-with-an-idp}

Kunder kan integrera med en IdP (identitetsleverantör) som autentiserar användaren. Integrationstekniken inkluderar SAML och OAuth/SSO, enligt beskrivningen nedan.

**SAML-BASERAT**

Kunder kan använda SAML-baserad autentisering via SAML IdP. När en IdP används med AEM ansvarar IdP för att autentisera användarens inloggningsuppgifter och förmedla användarens autentisering med AEM, skapa användarposten i AEM efter behov och hantera användarens gruppmedlemskap i AEM, vilket beskrivs i SAML-försäkran.

>[!NOTE]
>
>Endast den initiala autentiseringen av användarens autentiseringsuppgifter autentiseras av IdP:en och efterföljande begäranden till AEM utförs med en cookie för AEM inloggningstoken, så länge cookien är tillgänglig.

Mer information om [SAML 2.0-autentiseringshanterare](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/authentication/saml-2-0.html).

**OAuth/SSO**

Se [Dokumentation för enkel inloggning (SSO)](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/single-sign-on.html) om du vill ha information om hur du AEM SSO-autentiseringshanterartjänsten.

The `com.adobe.granite.auth.oauth.provider` -gränssnittet kan implementeras med valfri OAuth-leverantör.

**Krav:**

Det bästa sättet är att alltid förlita sig på idP (Identity Provider) som en enda sanning när användarspecifika data lagras. Om den ytterligare användarinformationen lagras i den lokala databasen, som inte ingår i idP:n, ska du aktivera [datasynkronisering](#data-synchronization-data-synchronization) genom att skicka en begäran till kundsupporten där det anges vilket program och vilken miljö som är lämplig. Förutom [datasynkronisering](#data-synchronization-data-synchronization), när det gäller SAML-autentiseringsprovidern, se till att [dynamiskt gruppmedlemskap](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/authentication/saml-2-0) är aktiverat.

### Anteckningssessioner och inkapslade token {#sticky-sessions-and-encapsulated-tokens}

AEM as a Cloud Service möjliggör cookie-baserade klistersessioner så att slutanvändaren dirigeras till samma publiceringsnod vid varje begäran. I vissa fall, t.ex. vid användartrafik, kan den inkapslade tokenfunktionen öka prestandan så att användarposten i databasen inte behöver refereras till vid varje begäran. Om publiceringsnoden som en slutanvändare har en tillhörighet till ersätts, är användar-ID-posten tillgänglig på den nya publiceringsnoden, vilket beskrivs i [datasynkronisering](#data-synchronization-data-synchronization) nedan.

Om du vill utnyttja den inkapslade tokenfunktionen skickar du en begäran till kundsupporten där det anges vilket program och vilken miljö som är lämplig. Viktigare är att den inkapslade token inte kan aktiveras utan [datasynkronisering](#data-synchronization-data-synchronization) och måste aktiveras tillsammans. Granska därför användningsexemplet noggrant innan du aktiverar och kontrollera att funktionen är nödvändig.

## Användarprofil {#user-profile}

Det finns olika sätt att se på beständiga data, beroende på vilken typ av data det gäller.

### AEM {#aem-repository}

Information om användarprofiler kan skrivas och läsas på två sätt:

* Användning på serversidan med `com.adobe.granite.security.user` Gränssnittet UserPropertiesManager som placerar data under användarens nod i `/home/users`. Se till att sidor som är unika per användare inte cachelagras.
* Klientsidan som använder ContextHub, enligt beskrivningen i [dokumentationen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/personalization/contexthub.html#personalization).

**Krav:**

Aktivera för att beständighetslogiken för användarprofiler på serversidan ska fungera korrekt [datasynkronisering](#data-synchronization-data-synchronization) genom att skicka en begäran till kundsupporten där det anges vilket program och vilken miljö som är lämplig.

### Datalager från tredje part {#third-party-data-stores}

Slutanvändardata kan skickas till tredjepartsleverantörer som CRM och hämtas via API:er när användaren loggar in på AEM och sparas (eller uppdateras) på AEM profilnod, och användas av AEM efter behov.

Det är möjligt att få åtkomst i realtid till tredjepartstjänster för att hämta profilattribut, men det är viktigt att se till att detta inte påverkar behandlingen av förfrågningar i AEM.

**Krav:**

För att ovanstående logik ska fungera korrekt måste du aktivera [datasynkronisering](#data-synchronization-data-synchronization) genom att skicka en begäran till kundsupporten där det anges vilket program och vilken miljö som är lämplig.

## Behörigheter (stängda användargrupper) {#permissions-closed-user-groups}

Åtkomstprinciper på Publish-nivå, som även kallas för stängda användargrupper, definieras i AEM författare som [beskrivs här](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/cug.html#applying-your-closed-user-group-to-content-pages). Om du vill begränsa vissa avsnitt eller sidor på en webbplats för vissa användare, tillämpar du de CUG-grupper som behövs med hjälp av AEM författare, enligt beskrivningen här, och replikerar dem till publiceringsnivån.

* Om användare loggar in genom att autentisera med en identitetsleverantör (IdP) med SAML, identifierar autentiseringshanteraren användarens gruppmedlemskap (som ska matcha användargrupperna på publiceringsnivån) och behåller kopplingen mellan användaren och gruppen via en databaspost
* Om inloggning sker utan IdP-integrering kan anpassad kod använda samma databasstrukturrelationer.

Oberoende av inloggning kan den anpassade koden också innehålla och hantera en användares gruppmedlemskap enligt organisationens unika krav.

## Datasynkronisering {#data-synchronization}

Slutanvändarna på webbplatsen förväntar sig en enhetlig upplevelse på alla webbsidesförfrågningar eller till och med när de loggar in i en annan webbläsare, även om de inte känner till dem, kommer de till olika servernoder i infrastrukturen på publiceringsnivån. AEM as a Cloud Service uppnår detta genom att snabbt synkronisera `/home` mapphierarki (användarprofilinformation, gruppmedlemskap och så vidare) över alla noder i publiceringsnivån.

Till skillnad från andra AEM använder synkronisering av användare och gruppmedlemskap i AEM as a Cloud Service inte en metod för att skicka meddelanden från punkt till punkt, utan implementerar i stället en strategi för att publicera prenumerationer som inte kräver någon kundkonfiguration.

>[!NOTE]
>
>Som standard är synkronisering av användarprofiler och gruppmedlemskap inte aktiverat och data kommer därför inte att synkroniseras till eller ens bli permanent beständiga på publiceringsnivån. Om du vill aktivera funktionen skickar du en begäran till kundsupport med information om vilket program och vilken miljö som är lämplig.

>[!IMPORTANT]
>
>Testa implementeringen i stor skala innan du aktiverar datasynkronisering i produktionsmiljön. Beroende på användningsfallet och de data som bevaras kan det uppstå vissa problem med konsekvens och fördröjning.

## Cacheöverväganden {#cache-considerations}

Autentiserade HTTP-begäranden kan vara svåra att cachelagra både i CDN och Dispatcher eftersom de kan medföra att användarspecifikt tillstånd överförs som en del av svaret på begäran. Om du av misstag cachelagrar autentiserade begäranden och skickar dem till andra begärande webbläsare kan det leda till felaktiga upplevelser eller till och med läcka skyddade data eller användardata.

Metoder för att behålla hög cache-kapacitet för förfrågningar med stöd för användarspecifika svar är bland annat:

* AEM Dispatcher Behörighetskänslig cachelagring
* Sling Dynamic Include
* AEM ContextHub
