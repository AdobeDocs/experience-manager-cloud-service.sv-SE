---
title: Registrering, inloggning och användarprofil
description: Läs mer om registrering, inloggning, användardata och gruppsynkronisering för AEM as a Cloud Service
exl-id: a991e710-a974-419f-8709-ad86c333dbf8
source-git-commit: 635f4c990c27a7646d97ebd08b453c71133f01b3
workflow-type: tm+mt
source-wordcount: '1168'
ht-degree: 0%

---

# Registrering, inloggning och användarprofil {#registration-login-and-userprofile}

## Introduktion {#introduction}

Webbprogram har ofta funktioner för kontohantering så att slutanvändarna kan registrera sig på en webbplats som bevarar användarinformationen, vilket gör att de kan logga in i framtiden och få en konsekvent upplevelse. I den här artikeln beskrivs följande begrepp för AEM as a Cloud Service:

* Registrering
* Inloggning
* Lagra användarprofildata
* Gruppmedlemskap
* Datasynkronisering

>[!IMPORTANT]
>
>För att de funktioner som beskrivs i den här artikeln ska fungera måste funktionen för synkronisering av användardata vara aktiverad, vilket för närvarande kräver en begäran till kundsupport som anger vilket program och vilken miljö som är lämplig. Om den inte är aktiverad sparas användarinformationen bara under en kort period (1 till 24 timmar) innan den försvinner.

## Registrering {#registration}

När en slutanvändare registrerar sig för ett konto i ett AEM skapas ett användarkonto i AEM Publish-tjänsten, vilket återspeglas på en användarresurs under `/home/users` i JCR-databasen.

Det finns två sätt att genomföra registreringen, som beskrivs nedan.

### AEM hanterad {#aem-managed-registration}

Du kan skriva en egen registreringskod som minimalt tar slutanvändarens användarnamn och lösenord och skapar en användarpost i AEM som sedan kan användas för att autentisera mot vid inloggning. Följande steg används vanligtvis för att konstruera den här registreringsmekanismen:

1. Visa en anpassad AEM som samlar in registreringsinformation
1. Vid inlämningen används en korrekt etablerad tjänstanvändare för att
   1. Verifiera att en befintlig användare inte redan finns, med en av API:erna för UserManager `findAuthorizables()` metoder
   1. Skapa en användarpost med någon av API:erna för UserManager `createUser()` metoder
   1. Bevara alla profildata som samlats in med det redigerbara gränssnittets `setProperty()` metoder
1. Valfria flöden, som att kräva att användaren validerar sin e-post.

### Extern {#external-managed-registration}

I vissa fall har registrering eller skapande av användare tidigare skett i infrastruktur utanför AEM. I så fall skapas användarposten i AEM under inloggningen.

## Inloggning {#login}

När en slutanvändare har registrerats i AEM Publish-tjänsten kan dessa användare logga in för att få autentiserad åtkomst (med hjälp av AEM autentiseringsmekanismer) och beständiga, användarspecifika data som profildata.

## Implementering {#implementation}

Inloggning kan implementeras med följande två metoder:

### AEM hanterad {#aem-managed-implementation}

Kunderna kan skriva egna komponenter. Om du vill veta mer kan du kanske börja lära dig mer om:

* The [Sling Authentication Framework](https://sling.apache.org/documentation/the-sling-engine/authentication/authentication-framework.html)
* Och fundera [fråga AEM Community Experts session](https://bit.ly/ATACEFeb15) om inloggning.

### Integrering med en identitetsleverantör {#integration-with-an-idp}

Kunder kan integrera med en IdP (identitetsleverantör) som autentiserar användaren. Integrationstekniken inkluderar SAML och OAuth/SSO, enligt beskrivningen nedan.

**SAML-BASERAT**

Kunder kan använda SAML-baserad autentisering via SAML IdP. När IdP används med AEM ansvarar IdP för att autentisera slutanvändarens inloggningsuppgifter och förmedla användarens autentisering med AEM, skapa användarposten i AEM efter behov och hantera användarens gruppmedlemskap i AEM, vilket beskrivs i SAML-försäkran.

>[!NOTE]
>
>Endast den initiala autentiseringen av användarens autentiseringsuppgifter autentiseras av IdP:en och efterföljande begäranden till AEM utförs med en cookie för AEM inloggningstoken, så länge cookien är tillgänglig.

Mer information om [SAML 2.0-autentiseringshanterare](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/authentication/saml-2-0.html).

**OAuth/SSO**

Se [Dokumentation för enkel inloggning (SSO)](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/single-sign-on.html) om du vill ha information om hur du använder AEM SSO Authentication Handler Service.

The `com.adobe.granite.auth.oauth.provider` -gränssnittet kan implementeras med valfri OAuth-leverantör.

### Anteckningssessioner och inkapslade token {#sticky-sessions-and-encapsulated-tokens}

AEM as a Cloud Service har aktiverat cookie-baserade klistersessioner, vilket ser till att slutanvändaren dirigeras till samma publiceringsnod vid varje begäran. För att öka prestanda är den inkapslade tokenfunktionen aktiverad som standard, så användarposten i databasen behöver inte refereras till vid varje begäran. Om den publiceringsnod som en slutanvändare har en tillhörighet att ersätta är användar-id-posten tillgänglig på den nya publiceringsnoden, vilket beskrivs i avsnittet Datasynkronisering nedan.

## Användarprofil {#user-profile}

Det finns olika sätt att se på beständiga data, beroende på vilken typ av data det rör sig om.

### AEM {#aem-repository}

Användarprofilinformation kan skrivas och läsas på två sätt:

* Användning på serversidan med `com.adobe.granite.security.user` Gränssnittet UserPropertiesManager som placerar data under användarens nod i `/home/users`. Se till att sidor som är unika per användare inte cachelagras.
* Klientsidan som använder ContextHub, enligt beskrivningen i [dokumentationen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/personalization/contexthub.html?lang=en#personalization).

### Datalager från tredje part {#third-party-data-stores}

Slutanvändardata kan skickas till tredjepartsleverantörer som CRM och hämtas via API:er när användaren loggar in på AEM och sparas (eller uppdateras) på AEM profilnod, och användas av AEM efter behov.

Åtkomst i realtid till tjänster från tredje part för att hämta profilattribut är möjlig, men det är viktigt att se till att detta inte i väsentlig grad påverkar behandlingen av begäranden i AEM.

## Behörigheter (stängda användargrupper) {#permissions-closed-user-groups}

Åtkomstprinciper på publiceringsnivå, som även kallas stängda användargrupper, definieras i AEM författare som [beskrivs här](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/cug.html?lang=en#applying-your-closed-user-group-to-content-pages). Om du vill begränsa vissa avsnitt eller sidor på en webbplats för vissa användare, tillämpar du de CUG-grupper som behövs med hjälp av AEM författare enligt beskrivningen här och replikerar dem till publiceringsnivån.

* Om användare loggar in genom att autentisera med en identitetsleverantör (IdP) med SAML, identifierar autentiseringshanteraren användarens gruppmedlemskap (som ska matcha användargrupperna på publiceringsnivån) och behåller kopplingen mellan användaren och gruppen via en databaspost
* Om inloggning sker utan IdP-integrering kan anpassad kod använda samma databasstrukturrelationer.

Oberoende av inloggning kan den anpassade koden också innehålla och hantera en användares gruppmedlemskap enligt organisationens unika krav.

## Datasynkronisering {#data-synchronization}

Slutanvändarna på webbplatsen förväntar sig en enhetlig upplevelse på alla webbsidesförfrågningar eller till och med när de loggar in i en annan webbläsare, även om de inte känner till dem, kommer de till olika servernoder i infrastrukturen på publiceringsnivån. AEM as a Cloud Service gör detta genom att snabbt synkronisera `/home` mapphierarki (användarprofilinformation, gruppmedlemskap osv.) över alla noder i publiceringsnivån.

Till skillnad från andra AEM lösningar använder synkronisering av användare och grupper i AEM as a Cloud Service inte en metod för att skicka meddelanden från punkt till punkt, utan implementerar i stället en strategi för att publicera prenumerationer som inte kräver någon kundkonfiguration.

>[!NOTE]
>
>Som standard är synkronisering av användarprofiler och gruppmedlemskap inte aktiverat och data kommer därför inte att synkroniseras till eller ens bli permanent beständiga på publiceringsnivån. Om du vill aktivera funktionen skickar du en begäran till kundsupport med information om rätt program och miljöer.

## Cacheöverväganden {#cache-considerations}

Autentiserade HTTP-begäranden kan vara svåra att cachelagra både i CDN och Dispatcher eftersom de kan medföra att användarspecifikt tillstånd överförs som en del av begäran. Om du av misstag cachelagrar autentiserade begäranden och skickar dem till andra begärande webbläsare kan det leda till felaktiga upplevelser eller till och med läcka skyddade data eller användardata.

Metoder för att behålla hög cache-kapacitet för förfrågningar med stöd för användarspecifika svar är bland annat:

* AEM Dispatcher Behörighetskänslig cachelagring
* Sling Dynamic Include
* AEM ContextHub
