---
title: Konfigurera CDN-autentiseringsuppgifter och autentisering
description: Lär dig hur du konfigurerar CDN-autentiseringsuppgifter och autentisering genom att deklarera regler i en konfigurationsfil som sedan distribueras med hjälp av Cloud Manager konfigurationsflöde.
feature: Dispatcher
exl-id: a5a18c41-17bf-4683-9a10-f0387762889b
role: Admin
source-git-commit: c31441baa6952d92be4446f9035591b784091324
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Konfigurera CDN-autentiseringsuppgifter och autentisering {#cdn-credentials-authentication}

CDN som tillhandahålls av Adobe har flera funktioner och tjänster, varav vissa förlitar sig på autentiseringsuppgifter och autentisering för att säkerställa en lämplig nivå av företagssäkerhet. Genom att deklarera regler i en konfigurationsfil som distribuerats med hjälp av Cloud Manager [config-pipeline kan ](/help/operations/config-pipeline.md)-kunder konfigurera följande på ett självbetjäningssätt:

* HTTP-huvudvärdet X-AEM-Edge-Key som används av Adobe CDN för att validera begäranden som kommer från ett kundhanterat CDN.
* Den API-token som används för att rensa resurser i CDN-cachen.
* En lista över kombinationer av användarnamn och lösenord som kan få åtkomst till begränsat innehåll genom att skicka ett grundläggande autentiseringsformulär.

Var och en av dessa, inklusive konfigurationssyntaxen, beskrivs i sitt eget avsnitt nedan.

Det finns ett avsnitt om hur du [roterar nycklar](#rotating-secrets), vilket är en bra säkerhetspraxis.

## Kundhanterat CDN HTTP-huvudvärde {#CDN-HTTP-value}

Så som beskrivs på [CDN-sidan i AEM as a Cloud Service](/help/implementing/dispatcher/cdn.md#point-to-point-CDN) kan kunderna välja att dirigera trafik genom sitt eget CDN, som kallas kundens CDN (kallas ibland även BYOCDN).

Som en del av konfigurationen måste Adobe CDN och kundens CDN komma överens om ett värde för HTTP-huvudet `X-AEM-Edge-Key`. Värdet anges för varje begäran, på kundens CDN, innan det dirigeras till Adobe CDN, som sedan validerar att värdet är som förväntat, så att det kan lita på andra HTTP-huvuden, inklusive de som hjälper till att dirigera begäran till rätt AEM.

Värdet *X-AEM-Edge-Key* refereras av egenskaperna `edgeKey1` och `edgeKey2` i en fil med namnet `cdn.yaml` eller liknande, någonstans under en `config`-mapp på översta nivån. Läs [Använda konfigurationsförlopp](/help/operations/config-pipeline.md#folder-structure) om du vill ha mer information om mappstrukturen och hur du distribuerar konfigurationen.

Syntaxen beskrivs nedan:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  authentication:
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

Se [Använda konfigurationsförlopp](/help/operations/config-pipeline.md#common-syntax) för en beskrivning av egenskaperna ovanför noden `data`. Egenskapsvärdet `kind` ska vara *CDN* och egenskapen `version` ska vara `1`.

Ytterligare egenskaper är:

* `Data`-nod som innehåller en underordnad `authentication`-nod.
* Under `authentication`, en `authenticators`-nod och en `rules`-nod, som båda är arrayer.
* Autentiserare: Gör att du kan deklarera en typ av token eller autentiseringsuppgifter, som i det här fallet är en edge-nyckel. Den innehåller följande egenskaper:
   * name - en beskrivande sträng.
   * type - måste vara `edge`.
   * edgeKey1 - värdet för *X-AEM-Edge-Key* som måste referera till en [Cloud Manager-miljövariabel av hemlig typ](/help/operations/config-pipeline.md#secret-env-vars). Välj Alla för fältet Tjänst används. Vi rekommenderar att värdet (till exempel `${{CDN_EDGEKEY_052824}}`) återspeglar den dag det lades till.
   * edgeKey2 - används för att rotera hemligheter, vilket beskrivs i avsnittet [roterande hemligheter](#rotating-secrets) nedan. Definiera den på liknande sätt som edgeKey1. Minst en av `edgeKey1` och `edgeKey2` måste deklareras.
<!--   * OnFailure - defines the action, either `log` or `block`, when a request doesn't match either `edgeKey1` or `edgeKey2`. For `log`, request processing will continue, while `block` will serve a 403 error. The `log` value is useful when testing a new token on a live site since you can first confirm that the CDN is correctly accepting the new token before changing to `block` mode; it also reduces the chance of lost connectivity between the customer CDN and the Adobe CDN, as a result of an incorrect configuration. -->
* Regler: Gör att du kan deklarera vilka autentiserare som ska användas och om det är för publicerings- och/eller förhandsgranskningsnivån.  Den innehåller följande uppgifter:
   * name - en beskrivande sträng.
   * when - ett villkor som bestämmer när regeln ska utvärderas, enligt syntaxen i artikeln [Traffic Filter Rules](/help/security/traffic-filter-rules-including-waf.md) . Vanligtvis innehåller det en jämförelse av den aktuella nivån (till exempel publicera) så att all livtrafik valideras som routning via kundens CDN.
   * action - måste ange &quot;authenticate&quot; med referens till den avsedda autentiseraren.

>[!NOTE]
>Edge-nyckeln måste konfigureras som en [hemlig Cloud Manager-miljövariabel](/help/operations/config-pipeline.md#secret-env-vars) innan konfigurationen som refererar till den distribueras. Vi rekommenderar att du använder en unik slumpmässig nyckel på minst 32 byte. Det kryptografiska biblioteket Open SSL kan till exempel generera en slumpmässig nyckel genom att köra kommandot `openssl rand -hex 32`.

### Migrera säkert för att minska risken för blockerad trafik {#migrating-safely}

Om webbplatsen redan är aktiv bör du vara försiktig när du migrerar till kundhanterad CDN eftersom en felkonfiguration kan blockera allmän trafik. Detta beror på att endast begäranden med det förväntade X-AEM-Edge-Key-huvudvärdet accepteras av Adobe CDN. Ett tillvägagångssätt rekommenderas när ett ytterligare villkor tillfälligt inkluderas i autentiseringsregeln, vilket gör att den bara utvärderar begäran om en testrubrik ingår:

```
    - name: edge-auth-rule
        when:
          allOf:  
            - { reqProperty: tier, equals: "publish" }
            - { reqHeader: x-edge-test, equals: "test" }
        action:
          type: authenticate
          authenticator: edge-auth
```

Följande `curl`-begärandemönster kan användas:

```
curl https://publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com -H "X-Forwarded-Host: example.com" -H "X-AEM-Edge-Key: <CONFIGURED_EDGE_KEY>" -H "x-edge-test: test"
```

När testningen är klar kan det ytterligare villkoret tas bort och konfigurationen distribueras på nytt.

## Rensa API-token {#purge-API-token}

Kunder kan [rensa CDN-cachen](/help/implementing/dispatcher/cdn-cache-purge.md) genom att använda en deklarerad rensnings-API-token. Token har deklarerats i en fil med namnet `cdn.yaml` eller liknande, någonstans under en `config`-mapp på översta nivån. Läs [Använda konfigurationsförlopp](/help/operations/config-pipeline.md#folder-structure) om du vill ha mer information om mappstrukturen och hur du distribuerar konfigurationen.

Syntaxen beskrivs nedan:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  authentication:
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

Se [Använda konfigurationsförlopp](/help/operations/config-pipeline.md#common-syntax) för en beskrivning av egenskaperna ovanför noden `data`. Egenskapsvärdet `kind` ska vara *CDN* och egenskapen `version` ska vara `1`.

Ytterligare egenskaper är:

* `data`-nod som innehåller en underordnad `authentication`-nod.
* Under `authentication`, en `authenticators`-nod och en `rules`-nod, som båda är arrayer.
* Autentiserare: Gör att du kan deklarera en typ av token eller autentiseringsuppgifter, som i det här fallet är en rensningsnyckel. Den innehåller följande egenskaper:
   * name - en beskrivande sträng.
   * type - måste tömmas.
   * purgeKey1 - dess värde måste referera till en [Cloud Manager-miljövariabel av hemlig typ](/help/operations/config-pipeline.md#secret-env-vars). Välj Alla för fältet Tjänst används. Vi rekommenderar att värdet (till exempel `${{CDN_PURGEKEY_031224}}`) återspeglar den dag det lades till.
   * purgeKey2 - används för att rotera hemligheter, vilket beskrivs i avsnittet [roterande hemligheter](#rotating-secrets) nedan. Minst en av `purgeKey1` och `purgeKey2` måste deklareras.
* Regler: Gör att du kan deklarera vilka autentiserare som ska användas och om det är för publicerings- och/eller förhandsgranskningsnivån.  Den innehåller följande uppgifter:
   * name - en beskrivande sträng
   * when - ett villkor som bestämmer när regeln ska utvärderas, enligt syntaxen i artikeln [Traffic Filter Rules](/help/security/traffic-filter-rules-including-waf.md) . Vanligtvis innehåller det en jämförelse av den aktuella nivån (till exempel publicera).
   * action - måste ange &quot;authenticate&quot; med referens till den avsedda autentiseraren.

>[!NOTE]
>Töm nyckel måste konfigureras som en [hemlig typ av Cloud Manager-miljövariabel](/help/operations/config-pipeline.md#secret-env-vars) innan konfigurationen som refererar till den distribueras. Vi rekommenderar att du använder en unik slumpmässig nyckel med en längd på minst 32 byte. Open SSL-kryptografibiblioteket kan till exempel generera en slumpmässig nyckel genom att köra kommandot openssl rand -hex 32

Du kan referera till [en självstudie](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/caching/how-to/purge-cache) som fokuserar på att konfigurera rensningsnycklar och utföra rensning av CDN-cache.

## Grundläggande autentisering {#basic-auth}

Protect vissa innehållsresurser genom att öppna en enkel autentiseringsdialogruta som kräver användarnamn och lösenord. Den här funktionen är främst avsedd för enkla autentiseringssituationer, som granskning av innehåll av intressenter i företag, i stället för som en fullständig lösning för slutanvändares åtkomsträttigheter.

Slutanvändaren får en grundläggande autentiseringsdialogruta som ser ut så här:

![basicauth-dialog](/help/implementing/dispatcher/assets/basic-auth-dialog.png)


Syntaxen är följande:

```
kind: "CDN"
version: "1"
metadata:
  envTypes: ["dev"]
data:
  authentication:
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

Se [Använda konfigurationsförlopp](/help/operations/config-pipeline.md#common-syntax) för en beskrivning av egenskaperna ovanför noden `data`. Egenskapsvärdet `kind` ska vara *CDN* och egenskapen `version` ska vara `1`.

Dessutom innehåller syntaxen:

* en `data`-nod som innehåller en `authentication`-nod.
* Under `authentication`, en `authenticators`-nod och en `rules`-nod, som båda är arrayer.
* Autentiserare: i det här scenariot deklarerar du en grundläggande autentiserare med följande struktur:
   * name - en beskrivande sträng
   * type - måste vara `basic`
   * en array med upp till 10 autentiseringsuppgifter, som vart och ett innehåller följande namn/värde-par, som slutanvändarna kan ange i den grundläggande autentiseringsdialogrutan:
      * användare - namnet på användaren
      * password - dess värde måste referera till en [Cloud Manager-miljövariabel av hemlig typ](/help/operations/config-pipeline.md#secret-env-vars), med **Alla** markerat som tjänstfält.
* Regler: Här kan du deklarera vilka autentiserare som ska användas och vilka resurser som ska skyddas. Varje regel innehåller:
   * name - en beskrivande sträng
   * when - ett villkor som bestämmer när regeln ska utvärderas, enligt syntaxen i artikeln [Traffic Filter Rules](/help/security/traffic-filter-rules-including-waf.md) . Vanligtvis innehåller det en jämförelse av publiceringsnivån eller specifika sökvägar.
   * action - måste ange &quot;authenticate&quot;, med den avsedda autentiseraren refererad, som är basautentisering för detta scenario

>[!NOTE]
>Lösenorden måste konfigureras som [hemlig typ av Cloud Manager-miljövariabler](/help/operations/config-pipeline.md#secret-env-vars), innan konfigurationen som refererar till den distribueras.

## Rotera hemligheter {#rotating-secrets}

1. Det är god säkerhetspraxis att emellanåt ändra autentiseringsuppgifter. Detta kan åstadkommas enligt exemplet nedan med hjälp av en kantnyckel, även om samma strategi används för tömningsnycklar.

1. Till att börja med har bara `edgeKey1` definierats, i det här fallet refererat till `${{CDN_EDGEKEY_052824}}`, vilket som en rekommenderad konvention, visar datumet då det skapades.

   ```
   authentication:
     authenticators:
       - name: edge-auth
         type: edge
         edgeKey1: ${{CDN_EDGEKEY_052824}}
   ```
1. När det är dags att rotera nyckeln skapar du en ny Cloud Manager-hemlighet, till exempel `${{CDN_EDGEKEY_041425}}`.
1. I konfigurationen refererar du till den från `edgeKey2` och distribuerar den.

   ```
   authentication:
     authenticators:
       - name: edge-auth
         type: edge
         edgeKey1: ${{CDN_EDGEKEY_052824}}
         edgeKey2: ${{CDN_EDGEKEY_041425}}
   ```

1. När du är säker på att den gamla kantnyckeln inte längre används tar du bort den genom att ta bort `edgeKey1` från konfigurationen.

   ```
   authentication:
     authenticators:
       - name: edge-auth
         type: edge
         edgeKey2: ${{CDN_EDGEKEY_041425}}
   ```
1. Ta bort den gamla hemliga referensen (`${{CDN_EDGEKEY_052824}}`) från Cloud Manager och distribuera.

1. När du är redo för nästa rotation följer du samma procedur, men den här gången lägger du till `edgeKey1` i konfigurationen och refererar till en ny Cloud Manager-miljöhemlighet med namnet, till exempel, `${{CDN_EDGEKEY_031426}}`.

   ```
   authentication:
     authenticators:
       - name: edge-auth
         type: edge
         edgeKey2: ${{CDN_EDGEKEY_041425}}
         edgeKey1: ${{CDN_EDGEKEY_031426}}
   ```
