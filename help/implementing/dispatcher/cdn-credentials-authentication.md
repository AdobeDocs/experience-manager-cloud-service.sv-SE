---
title: Konfigurera CDN-autentiseringsuppgifter och autentisering
description: Lär dig hur du konfigurerar CDN-inloggningsuppgifter och autentisering genom att deklarera regler i en konfigurationsfil som sedan distribueras med hjälp av Cloud Manager Configuration Pipeline.
feature: Dispatcher
exl-id: a5a18c41-17bf-4683-9a10-f0387762889b
role: Admin
source-git-commit: 73d0a4a73a3e97a91b2276c86d3ed1324de8c361
workflow-type: tm+mt
source-wordcount: '1400'
ht-degree: 0%

---

# Konfigurera CDN-autentiseringsuppgifter och autentisering {#cdn-credentials-authentication}

>[!NOTE]
>Den här funktionen är ännu inte allmänt tillgänglig. Om du vill gå med i programmet för tidig adopter skickar du e-post `aemcs-cdn-config-adopter@adobe.com`.

CDN som tillhandahålls av Adobe har flera funktioner och tjänster, varav vissa förlitar sig på autentiseringsuppgifter och autentisering för att säkerställa en lämplig nivå av företagssäkerhet. Genom att deklarera regler i en konfigurationsfil som distribuerats med [Konfigurationspipeline för Cloud Manager](/help/implementing/cloud-manager/configuring-pipelines/introduction-ci-cd-pipelines.md#config-deployment-pipeline)kan man via självbetjäning konfigurera följande:

* Det HTTP-huvudvärde som används av CDN i Adobe för att validera begäranden från ett kundhanterat CDN.
* Den API-token som används för att rensa resurser i CDN-cachen.
* En lista över kombinationer av användarnamn och lösenord som kan få åtkomst till begränsat innehåll genom att skicka ett grundläggande autentiseringsformulär.


Var och en av dessa, inklusive konfigurationssyntaxen, beskrivs i sitt eget avsnitt nedan. The [Vanliga inställningar](#common-setup) -avsnittet illustrerar de inställningar som är gemensamma för både och distributionen. Slutligen finns det ett avsnitt om hur man [rotera tangenter](#rotating-secrets), vilket anses vara en god säkerhetspraxis.

## Kundhanterat CDN HTTP-huvudvärde {#CDN-HTTP-value}

Enligt beskrivningen i [CDN på AEM as a Cloud Service](/help/implementing/dispatcher/cdn.md#point-to-point-CDN) kan kunderna välja att dirigera trafik genom sitt eget CDN, som kallas kundens CDN (kallas ibland även BYOCDN).

Som en del av installationen måste CDN och kundens CDN komma överens om ett värde för `X-AEM-Edge-Key` HTTP-huvud. Värdet anges för varje begäran, på kundens CDN, innan det dirigeras till Adobe CDN, som sedan validerar att värdet är som förväntat, så att det kan lita på andra HTTP-huvuden, inklusive de som hjälper till att dirigera begäran till rätt AEM.

The `X-AEM-Edge-Key` värdet deklareras med syntaxen nedan, med de faktiska värdena som refereras av egenskaperna edgeKey1 och edgeKey2. Se [Vanliga inställningar](#common-setup) för att lära dig hur du distribuerar konfigurationen.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  experimental_authentication:
    authenticators:
      - name: edge-auth
        type: edge
        edgeKey1: ${{CDN_EDGEKEY_052824}}
        edgeKey2: ${{CDN_EDGEKEY_041425}}
    rules:
      - name: edge-auth-rule
        when: { reqProperty: tier, equals: "publish" }
        action:
          type: authenticate
          authenticator: edge-auth
```

Syntaxen för `X-AEM-Edge-Key` Värdet innehåller:

* Typ, version och metadata.
* Datanod som innehåller ett underordnat objekt `experimental_authentication` nod (det experimentella prefixet tas bort när funktionen släpps).
* Under `experimental_authentication`, en `authenticators` nod och en `rules` nod, som båda är arrayer.
* Autentiserare: Gör att du kan deklarera en typ av token eller autentiseringsuppgifter, som i det här fallet är en edge-nyckel. Den innehåller följande egenskaper:
   * name - en beskrivande sträng.
   * type - måste vara `edge`.
   * edgeKey1 - värdet på *X-AEM-edge-key*, som måste referera till en hemlig token, som inte ska lagras i Git, utan snarare deklareras som en [Miljövariabel för Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) av typen hemlighet. Välj Alla för fältet Tjänst används. Vi rekommenderar att värdet (till exempel`${{CDN_EDGEKEY_052824}}`) återspeglar den dag då det lades till.
   * edgeKey2 - används för att rotera hemligheter, som beskrivs i [rotera avsnittet med hemligheter](#rotating-secrets) nedan. Definiera den på liknande sätt som edgeKey1. Minst en av `edgeKey1` och `edgeKey2` måste deklareras.
<!--   * OnFailure - defines the action, either `log` or `block`, when a request doesn't match either `edgeKey1` or `edgeKey2`. For `log`, request processing will continue, while `block` will serve a 403 error. The `log` value is useful when testing a new token on a live site since you can first confirm that the CDN is correctly accepting the new token before changing to `block` mode; it also reduces the chance of lost connectivity between the customer CDN and the Adobe CDN, as a result of an incorrect configuration. -->
* Regler: Gör att du kan deklarera vilka autentiserare som ska användas och om det är för publicerings- och/eller förhandsgranskningsnivån.  Den innehåller följande uppgifter:
   * name - en beskrivande sträng.
   * when - ett villkor som bestämmer när regeln ska utvärderas, enligt syntaxen i [Trafikfilterregler](/help/security/traffic-filter-rules-including-waf.md) artikel. Vanligtvis innehåller det en jämförelse av den aktuella nivån (till exempel publicera) så att all livtrafik valideras som routning via kundens CDN.
   * action - måste ange &quot;authenticate&quot; med referens till den avsedda autentiseraren.

>[!NOTE]
>Kantnyckeln måste konfigureras som en [Miljövariabel för Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) variabel av typen `secret` (med *Alla* väljs för Tillämpad tjänst), innan konfigurationen som refererar till den distribueras.

## Rensa API-token {#purge-API-token}

Kunderna kan [rensa CDN-cachen](/help/implementing/dispatcher/cdn-cache-purge.md) genom att använda en deklarerad rensnings-API-token. Token deklareras med syntaxen nedan.  Se [Vanliga inställningar](#common-setup) för att lära dig hur du distribuerar det.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  experimental_authentication:
    authenticators:
       - name: purge-auth
         type: purge
         purgeKey1: ${{CDN_PURGEKEY_031224}}
         purgeKey2: ${{CDN_PURGEKEY_021225}}
    rules:
       - name: purge-auth-rule
         when: { reqProperty: tier, equals: "publish" }
         action:
           type: authenticate
           authenticator: purge-auth
```

Syntaxen innehåller:

* typ, version och metadata.
* datanod som innehåller en underordnad `experimental_authentication` nod (det experimentella prefixet tas bort när funktionen släpps).
* Under `experimental_authentication`, en `authenticators` nod och en `rules` nod, som båda är arrayer.
* Autentiserare: Gör att du kan deklarera en typ av token eller autentiseringsuppgifter, som i det här fallet är en rensningsnyckel. Den innehåller följande egenskaper:
   * name - en beskrivande sträng.
   * type - måste tömmas.
   * purgeKey1 - dess värde måste referera till en hemlig token, som inte ska lagras i git, utan deklareras som [Miljövariabler för Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) av typen `secret`.
   * Välj Alla för fältet Tjänst används. Vi rekommenderar att värdet (till exempel `${{CDN_PURGEKEY_031224}}`) återspeglar den dag då det lades till.
   * purgeKey2 - används för att rotera hemligheter, vilket beskrivs i [rotera avsnittet med hemligheter](#rotating-secrets) nedan. Minst en av `purgeKey1` och `purgeKey2` måste deklareras.
* Regler: Gör att du kan deklarera vilka autentiserare som ska användas och om det är för publicerings- och/eller förhandsgranskningsnivån.  Den innehåller följande uppgifter:
   * name - en beskrivande sträng
   * when - ett villkor som bestämmer när regeln ska utvärderas, enligt syntaxen i [Trafikfilterregler](/help/security/traffic-filter-rules-including-waf.md) artikel. Vanligtvis innehåller det en jämförelse av den aktuella nivån (till exempel publicera).
   * action - måste ange &quot;authenticate&quot; med referens till den avsedda autentiseraren.

>[!NOTE]
>Kantnyckeln måste konfigureras som en [Miljövariabel för Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) variabel av typen `secret`innan konfigurationen som refererar till den distribueras.

## Grundläggande autentisering {#basic-auth}

Protect vissa innehållsresurser genom att öppna en enkel autentiseringsdialogruta som kräver användarnamn och lösenord. Den här funktionen är främst avsedd för enkla autentiseringssituationer, som granskning av innehåll av intressenter i företag, i stället för som en fullständig lösning för slutanvändares åtkomsträttigheter.

Slutanvändaren får en grundläggande autentiseringsdialogruta som ser ut så här:

![basicauth-dialog](/help/implementing/dispatcher/assets/basic-auth-dialog.png)


Syntaxen deklareras enligt beskrivningen nedan. Se [Vanliga inställningar](#common-setup) nedan om du vill ha information om hur du distribuerar den.

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  experimental_authentication:
    authenticators:
       - name: my-basic-authenticator
         type: basic
         credentials:
           - user: johndoe
             password: ${{JOHN_DOE_PASSWORD}}
           - user: janedoe
             password: ${{JANE_DOE_PASSWORD}}
    rules:
       - name: basic-auth-rule
         when: { reqProperty: path, like: "/summercampaign" }
         action:
           type: authenticate
           authenticator: my-basic-authenticator
```

Syntaxen innehåller:

* typ, version och metadata.
* en datanod som innehåller `experimental_authentication` nod (det experimentella prefixet tas bort när funktionen släpps).
* Under `experimental_authentication`, en `authenticators` nod och en `rules` nod, som båda är arrayer.
* Autentiserare: i det här scenariot deklarerar du en grundläggande autentiserare med följande struktur:
   * name - en beskrivande sträng
   * type - måste vara `basic`
   * en array med autentiseringsuppgifter, som vart och ett innehåller följande namn/värde-par, som slutanvändarna kan ange i den grundläggande autentiseringsdialogrutan:
      * användare - namnet på användaren
      * password - dess värde måste referera till en hemlig token, som inte ska lagras i Git, utan istället deklareras som Cloud Manager Environment Variables av typen secrets (med **Alla** markerat som tjänstfält)
* Regler: Här kan du deklarera vilka autentiserare som ska användas och vilka resurser som ska skyddas. Varje regel innehåller:
   * name - en beskrivande sträng
   * when - ett villkor som bestämmer när regeln ska utvärderas, enligt syntaxen i [Trafikfilterregler](/help/security/traffic-filter-rules-including-waf.md) artikel. Vanligtvis innehåller det en jämförelse av publiceringsnivån eller specifika sökvägar.
   * action - måste ange &quot;authenticate&quot;, med den avsedda autentiseraren refererad, som är basautentisering för detta scenario

>[!NOTE]
>Kantnyckeln måste konfigureras som en [Miljövariabel för Cloud Manager](/help/implementing/cloud-manager/environment-variables.md) variabel av typen `secret`innan konfigurationen som refererar till den distribueras.

## Vanliga inställningar {#common-setup}

Alla autentiserare konfigureras enligt följande:

* Skapa först följande mapp- och filstruktur i den översta mappen i Git-projektet:

```
config/
     cdn.yaml
```

* För det andra `cdn.yaml` konfigurationsfilen ska innehålla de noder som beskrivs i exemplen nedan. The `kind` egenskapen ska anges till `CDN` och versionen bör anges till schemaversionen, som för närvarande är `1`. Metadatanoden har en envTypes-egenskap som anger på vilka miljötyper (dev, stage, prod) som den här konfigurationen ska utvärderas.

* Skapa en riktad distributionsprocess i Cloud Manager. Se [konfigurera produktionspipelines](/help/implementing/cloud-manager/configuring-pipelines/configuring-production-pipelines.md) och [konfigurera icke-produktionsrörledningar](/help/implementing/cloud-manager/configuring-pipelines/configuring-non-production-pipelines.md).

Observera att:

* De lokala lagringsplatserna stöder för närvarande inte konfigurationsflödet.
* Du kan använda `yq` för att lokalt validera YAML-formateringen i konfigurationsfilen (till exempel `yq cdn.yaml`).

## Rotera hemligheter {#rotating-secrets}

Det är god säkerhetspraxis att emellanåt ändra autentiseringsuppgifter. Detta kan åstadkommas enligt exemplet nedan med hjälp av en kantnyckel, även om samma strategi används för tömningsnycklar.

* Initialt bara `edgeKey1` har definierats, i detta fall refereras till som `${{CDN_EDGEKEY_052824}}`, vilket som en rekommenderad konvention återspeglar datumet då den skapades.

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey1: ${{CDN_EDGEKEY_052824}}
```

* När det är dags att rotera nyckeln skapar du en ny Cloud Manager-hemlighet, till exempel `${{CDN_EDGEKEY_041425}}`.
* I konfigurationen refererar du till den från `edgeKey2` och driftsätta.

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey1: ${{CDN_EDGEKEY_052824}}
      edgeKey2: ${{CDN_EDGEKEY_041425}}
```

* När du är säker på att den gamla kantnyckeln inte längre används tar du bort den genom att ta bort `edgeKey1` från konfigurationen.

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey2: ${{CDN_EDGEKEY_041425}}
```

* Ta bort den gamla hemliga referensen (`${{CDN_EDGEKEY_052824}}`) från Cloud Manager och distribuera.
* När du är klar för nästa rotation följer du samma procedur, men den här gången lägger du till `edgeKey1` till konfigurationen, med referens till en ny Cloud Manager-miljöhemlighet med namnet, till exempel `${{CDN_EDGEKEY_031426}}`.

```
experimental_authentication:
  authenticators:
    - name: edge-auth
      type: edge
      edgeKey2: ${{CDN_EDGEKEY_041425}}
      edgeKey1: ${{CDN_EDGEKEY_031426}}
```
