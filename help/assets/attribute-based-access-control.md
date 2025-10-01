---
title: Attributbaserad åtkomstkontroll
description: Lär dig hur du aktiverar attributbaserad åtkomstkontroll för att definiera metadatabaserade regler för att definiera åtkomstnivån för resurser som är tillgängliga i Content Hub
role: Admin
exl-id: 05f54b05-40b8-4a6c-af8f-5c3f7a2089d4
source-git-commit: 82630f69399c077dc5c8ca40e7552cd479ea5bc5
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 0%

---

# Attributbaserad åtkomstkontroll {#attribute-based-access-control}

Med den attributbaserade åtkomstkontrollen (ABAC) kan Content Hub-administratörer definiera metadatabaserade regler för att definiera åtkomstnivån för resurser som är tillgängliga i Content Hub.

Administratörer för en organisation definierar regler för användargrupper, som mappas till ett grupp-ID. Regler är en blandning av [logiska operatorer och jämförelseoperatorer](#supported-rule-constructs) och administratörer kan definiera så många regler som behövs för att hantera resursåtkomst inom Content Hub.

Reglerna baseras på metadata och om villkoren som definieras i regeln matchar metadata för resursen visas resursen för användargruppen. Content Hub skannar metadata för resursen inklusive anpassade metadata för alla resurser som är tillgängliga i **Alla Assets** och **Samlingar** för att visa resultaten för användargrupper.

Till exempel TILLÅT åtkomst till användargruppen med grupp-ID = 1011 när metadata för resursen matchar&quot;Brand = Brand X&quot; OCH&quot;Region = EMEA ELLER Nord- och Sydamerika&quot;. Content Hub visar endast dessa resurser för användargruppen med ID = 1011 där Brand = `Brand X` och Region = `EMEA` eller `Americas`.

Några av fördelarna med attributbaserad åtkomstkontroll är:

* Eliminerar beroendet av mappstrukturen för behörigheter

* Tillåter administratörer att överföra resurser och retroaktivt fastställa behörighetsstrukturer

* Minskar antalet dubbletter - förbättrar materialets integritet. Dubbletter behövs i mappbaserade behörigheter när samma resurser delas med olika grupper.

## Hur aktiverar jag attributbaserad åtkomstkontroll? {#enable-attribute-based-access-control}

Från och med nu kan du inte skapa attributbaserade åtkomstkontrollsregler på egen hand med Content Hub användargränssnitt.

Klicka på **Hämta kalkylblad** om du vill hämta och definiera regler i ett kalkylblad. Skapa en Adobe supportanmälan och förse Adobe med de regler som finns definierade i kalkylbladet.

[!BADGE Hämta kalkylblad]{type=Informative url="https://helpx.adobe.com/content/dam/help/en/experience-manager/aem-assets/ABAC_Get_Started_Template.xlsx"}


Definiera regler i kalkylbladet med hjälp av riktlinjerna i den här artikeln.

<!--

>[!IMPORTANT]
>
> After defining the rules, navigate to the **Validation Errors** tab of the spreadsheet and click **Run ABAC Validations**. **All validations passed** message confirms that you can provide the defined rules to Adobe.

-->

## Exempel: Attributbaserad åtkomstkontroll {#example-metadata-based-rules}

För att stödja en storskalig marknadsföring behöver olika teammedlemmar i olika regioner och varumärken tillgång till digitalt material. Varje personlighet har ett specifikt omfång baserat på region och varumärke. ABAC tillämpar dessa regler automatiskt via metadata för resurser. I följande tabell visas de olika persontyperna för det här användningsfallet och de regler som tillämpas:

| Persona | Roll | Rollbeskrivning | Grupp-ID | ABAC-regel |
|---------------------|----------------|-----------------|------------|------------|
| John | EMEA Marketing Lead | Övervakar marknadsföringen av alla varumärken inom EMEA. Behöver tillgång till godkänt material för alla varumärken som är avsedda för EMEA: s marknader. | group-emea-marketing | region = &quot;EMEA&quot; |
| Mike | APAC Marketing Lead | Övervakar marknadsföringen för alla varumärken i APAC. Behöver tillgång till godkända mediefiler för alla varumärken som är avsedda för APAC-marknader. | gruppmarknadsföring | region = &quot;APAC&quot; |
| Sophie | Brand X Manager (EMEA) | Hanterar varumärkes X-identitet inom EMEA. Behöver bara se Brand X-godkänt innehåll som är anpassat till EMEA: s marknader. | group-emea-brandx | region = &quot;EMEA&quot; &amp;&amp; varumärke = &quot;varumärke X&quot; |
| Tom | Y-hanterare för varumärke (APAC) | Hanterar varumärkets Y-identitet i APAC. Behöver bara se innehåll som är godkänt av Brand Y och som är anpassat för APAC-marknader. | group-apac-brandy | region = &quot;APAC&quot; &amp;&amp; varumärke = &quot;varumärke Y&quot; |

Med dessa regler kan Content Hub-administratörer:

* **Detaljerad, regelbaserad åtkomst**: Användare ser bara de resurser som är relevanta för deras region och varumärke - inga manuella behörighetstilldelningar.

* **Sömlöst globalt samarbete**: Regionala team och varumärkesteam arbetade parallellt utan åtkomstkonflikter.

* **Skalbara och framtidssäkra behörigheter**: När nya regioner eller varumärken läggs till kan regler uppdateras baserat på metadata.

>[!IMPORTANT]
>
> Som standard nekas alla andra användargrupper åtkomst, som inte har angetts med några regler i [kalkylbladet](#enable-attribute-based-access-control). Om en användare inte är en del av någon grupp för vilken ABAC-regler har definierats, kan de inte komma åt några resurser. Om du vill att vissa användare ska ha tillgång till alla resurser (till exempel administratörer), måste en grupp med ett grupp-ID anges i kalkylbladet med den information som den här gruppen behöver ha tillgång till alla resurser och Adobe konfigurerar den åt dig.


## Regelkonstruktioner som stöds {#supported-rule-constructs}

* **Logiska operatorer**:
   * AND: Alla villkor måste vara sanna
   * OR: Minst ett villkor måste vara sant
* **Jämförelseoperatorer**:
   * Lika med (=): Kontrollerar om ett användar- eller resursattribut matchar ett värde
   * Inte lika med (!=): Kontrollerar om ett användar- eller resursattribut inte matchar ett värde

När metadatafält för resurser innehåller arrayer (till exempel flera regioner eller taggar) refererar `Equals` till `contains` logic och `Not Equals` refererar till `does not contain` logic.

Detta gör att du kan skriva enkla och uttrycksfulla regler, som: ALLOW if region = emea AND assetType != prototype AND-taggar != Konfidentiellt.

## Riktlinjer {#guidelines-attribute-based-access-control}

* ABAC-regler gäller endast för tillgångar som godkänts för Content Hub. Mer information finns i [Godkänn Assets för Content Hub](/help/assets/approve-assets-content-hub.md).

* Ge inte DENY-regler, utan konvertera alltid DENY till ALLOW-regel. `ALLOW if region = <user-region> DENY if assetType = prototype AND confidential = yes` kan till exempel konverteras till `ALLOW if region = <user-region> AND (assetType != prototype OR confidential != yes)`.

* ABAC-regler tillämpas på användargrupper med hjälp av IMS-grupp-ID, som är tillgängligt i Admin Console.


* Du kan ange [Godkännandemål](/help/assets/approve-assets-content-hub.md#set-approval-target) för resurser med hjälp av AEM as a Cloud Service författarmiljö. ABAC-regler tillämpas på resurser som godkänts med Godkännandemål = `Content Hub`, eftersom Godkännandemål = `Delivery` är tillgängligt för resurser som är tillgängliga för `Delivery` + `Content Hub`. Assets som har markerats som Godkännandemål = `Delivery` är synliga för alla i innehållsnavet.

* Se till att metadatamappningarna som används i ABAC-regler är korrekt definierade och tillgängliga i AEM. Ange fullständig sökväg till metadatamatcheman i AEM som definierar egenskaper som refereras i ABAC-regler. Du kan också skapa en testmapp med några exempelresurser med metadatavärden som matchar ABAC-villkoren. Detta hjälper till att verifiera regelbeteende och utvärdera åtkomsten korrekt.

* Fånga regelns affärsmetod i kommentarer, oavsett om villkoret är korrekt skrivet, eftersom metoden hjälper oss att validera och korrigera logiken, om det behövs.

* Licensen för PDF-filer som är inställda för DRM måste vara synliga för alla, så att användarna kan se dem när de hämtar resursen med licens.
