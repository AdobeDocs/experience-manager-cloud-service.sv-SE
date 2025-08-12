---
title: Konfigurera CDN-autentiseringsuppgifter och autentisering
description: Lär dig hur du konfigurerar CDN-autentiseringsuppgifter och autentisering genom att deklarera regler i en konfigurationsfil som sedan distribueras med hjälp av Cloud Manager konfigurationsflöde.
feature: Dispatcher
exl-id: a5a18c41-17bf-4683-9a10-f0387762889b
role: Admin
source-git-commit: edfefb163e2d48dc9f9ad90fa68809484ce6abb0
workflow-type: tm+mt
source-wordcount: '1939'
ht-degree: 0%

---


# Konfigurera CDN-autentiseringsuppgifter och autentisering {#cdn-credentials-authentication}

CDN som tillhandahålls av Adobe har flera funktioner och tjänster, varav vissa är beroende av autentiseringsuppgifter och autentisering för att säkerställa en lämplig nivå av företagssäkerhet. Genom att deklarera regler i en konfigurationsfil som distribuerats med hjälp av Cloud Manager [config pipeline](/help/operations/config-pipeline.md) kan kunderna på ett självbetjäningssätt konfigurera följande:

* HTTP-huvudvärdet för X-AEM-Edge-Key som används av Adobe CDN för att validera begäranden som kommer från ett kundhanterat CDN.
* Den API-token som används för att rensa resurser i CDN-cachen.
* En lista över kombinationer av användarnamn och lösenord som kan få åtkomst till begränsat innehåll genom att skicka ett grundläggande autentiseringsformulär.

Var och en av dessa, inklusive konfigurationssyntaxen, beskrivs i sitt eget avsnitt nedan.

Det finns ett avsnitt om hur du [roterar nycklar](#rotating-secrets), vilket är en bra säkerhetspraxis.

>[!NOTE]
> Hemligheter som definieras som miljövariabler bör betraktas som oföränderliga. I stället för att ändra deras värde bör du skapa en ny hemlighet med ett nytt namn och en referens till hemligheten i konfigurationen. Om du inte gör det kommer hemligheterna att uppdateras på ett otillförlitligt sätt.

>[!WARNING]
>Ta inte bort de miljövariabler som refereras i CDN-konfigurationen. Detta kan orsaka fel vid uppdatering av CDN-konfigurationen (till exempel uppdatering av regler eller anpassade domäner och certifikat).

## Kundhanterat CDN HTTP-huvudvärde {#CDN-HTTP-value}

Så som beskrivs på [CDN-sidan i AEM as a Cloud Service](/help/implementing/dispatcher/cdn.md#point-to-point-CDN) kan kunderna välja att dirigera trafik genom sitt eget CDN, som kallas kundens CDN (kallas ibland även BYOCDN).

Som en del av konfigurationen måste Adobe CDN och kundens CDN komma överens om ett värde för HTTP-huvudet `X-AEM-Edge-Key`. Värdet anges för varje begäran hos Customer CDN, innan det dirigeras till Adobe CDN, som sedan validerar att värdet är som förväntat, så att det kan lita på andra HTTP-huvuden, inklusive de som hjälper till att dirigera begäran till rätt AEM-ursprung.

Värdet *X-AEM-Edge-Key* refereras av egenskaperna `edgeKey1` och `edgeKey2` i en fil med namnet `cdn.yaml` eller liknande, någonstans under en `config` -mapp på översta nivån. Läs [Använda konfigurationsförlopp](/help/operations/config-pipeline.md#folder-structure) om du vill ha mer information om mappstrukturen och hur du distribuerar konfigurationen.  Syntaxen beskrivs i exemplet nedan.

Mer felsökningsinformation och vanliga fel finns i [Vanliga fel](/help/implementing/dispatcher/cdn.md#common-errors).

>[!WARNING]
>Direktåtkomst utan korrekt X-AEM-Edge-Key nekas för alla begäranden som matchar villkoret (i exemplet nedan betyder det alla begäranden till publiceringsnivån). Om du behöver införa autentisering gradvis läser du avsnittet [Migrera säkert för att minska risken för blockerad trafik](#migrating-safely).

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

Mer information finns i [Konfigurera och distribuera CDN-regel för HTTP-huvudvalidering](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/content-delivery/custom-domain-names-with-customer-managed-cdn#configure-and-deploy-http-header-validation-cdn-rule).

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

Om webbplatsen redan är aktiv bör du vara försiktig när du migrerar till kundhanterad CDN eftersom en felkonfiguration kan blockera allmän trafik. Detta beror på att endast begäranden med det förväntade X-AEM-Edge-Key-huvudvärdet accepteras av Adobe CDN. Ett tillvägagångssätt rekommenderas när ytterligare ett villkor tillfälligt inkluderas i autentiseringsregeln, vilket gör att den blockerar begäran endast om en testrubrik ingår eller om en sökväg matchar:

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

```
    - name: edge-auth-rule
        when:
          allOf:
            - { reqProperty: tier, equals: "publish" }
            - { reqProperty: path, like: "/test*" }
        action:
          type: authenticate
          authenticator: edge-auth
```

Följande `curl`-begärandemönster kan användas:

```
curl https://publish-p<PROGRAM_ID>-e<ENV-ID>.adobeaemcloud.com -H "X-Forwarded-Host: example.com" -H "X-AEM-Edge-Key: <CONFIGURED_EDGE_KEY>" -H "x-edge-test: test"
```

När testningen är klar kan det ytterligare villkoret tas bort och konfigurationen distribueras på nytt.

### Migreringsprocess om Adobe Support tidigare genererade värdet `X-AEM-Edge-Key` för HTTP Header {#migrating-legacy}

>[!NOTE]
>Innan du fortsätter med migreringen ska du schemalägga en testmigrering på scenmiljön för att verifiera strategin.

>[!WARNING]
> Ändra inte nyckeln i det kundhanterade CDN förrän steg 4.

Processen för integrering med ett kundhanterat CDN involverade tidigare kunder som begärde ett HTTP Header-värde för X-AEM-Edge-Key från Adobe Support i stället för att själva definiera värdet. Om du vill migrera till den nya självbetjäningsmetoden där du definierar egna kantnyckelvärden följer du de här stegen för att säkerställa en smidig övergång utan driftavbrott:

1. Konfigurera CDN-konfigurationen med både de nya (kundgenererade) och gamla (Adobe-genererade) hemligheter som anges som `edgeKey1` och `edgeKey2`. Det här är en variation av dokumentationen [som roterar hemligheter](/help/implementing/dispatcher/cdn-credentials-authentication.md#rotating-secrets).

2. Distribuera hemligheterna och den självbetjänande CDN-konfigurationen. Nu ska den gamla Adobe-definierade hemligheten förbli det X-AEM-Edge-Key-värde som skickas av kundhanterad CDN.

3. Kontakta Adobe Support och be Adobe växla över för att använda självbetjäningskonfigurationen och ange att du redan har distribuerat den.

4. När Adobe har bekräftat att den har utfört den åtgärden konfigurerar du det kundhanterade CDN så att det använder den nya, kunddefinierade nyckeln för HTTP Header-värdet `X-AEM-Edge-Key`.

5. Ta bort den gamla nyckeln från CDN-konfigurationen och distribuera konfigurationsflödet igen.

>[!WARNING]
>Om du inte har återställningen med båda nycklarna konfigurerade samtidigt kan det leda till driftstopp under migreringen.

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

Skydda vissa innehållsresurser genom att öppna en enkel dialogruta för autentisering som kräver ett användarnamn och lösenord. Den här funktionen är främst avsedd för enkla autentiseringssituationer, som granskning av innehåll av intressenter i företag, i stället för som en fullständig lösning för slutanvändares åtkomsträttigheter.

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
      * användare - användarens namn.
      * password - dess värde måste referera till en [Cloud Manager-miljövariabel av hemlig typ](/help/operations/config-pipeline.md#secret-env-vars), med **Alla** markerat som tjänstfält.
* Regler: Här kan du deklarera vilka autentiserare som ska användas och vilka resurser som ska skyddas. Varje regel innehåller:
   * name - en beskrivande sträng
   * when - ett villkor som bestämmer när regeln ska utvärderas, enligt syntaxen i artikeln [Traffic Filter Rules](/help/security/traffic-filter-rules-including-waf.md) . Vanligtvis innehåller det en jämförelse av publiceringsnivån eller specifika sökvägar.
   * action - måste ange &quot;authenticate&quot;, med den avsedda autentiseraren refererad, som är basautentisering för detta scenario

>[!NOTE]
>
>Lösenorden måste konfigureras som [hemlig typ av Cloud Manager-miljövariabler](/help/operations/config-pipeline.md#secret-env-vars), innan konfigurationen som refererar till den distribueras.

## Rotera hemligheter {#rotating-secrets}

Det är en god säkerhetspraxis att ändra inloggningsuppgifter regelbundet. Kom ihåg att miljövariabler inte ska ändras direkt, utan i stället skapa en ny hemlighet och referera till det nya namnet i konfigurationen.

Det här användningsexemplet visas nedan med hjälp av en kantnyckel, men samma strategi kan även användas för tömningsnycklar.

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

När hemligheter som anges i begärandehuvuden roteras, t.ex. för autentisering mot en serverdel, bör du rotera i två steg för att säkerställa att rubrikvärdet byts utan tillfälliga luckor.

1. Inledande konfiguration före rotationen. I det här läget skickas den gamla nyckeln till backend-objektet.

   ```
   requestTransformations:
     rules:
       - name: set-api-key-header
         actions:
           - type: set
             reqHeader: x-api-key
             value ${{API_KEY_1}}
   ```

1. Introducera den nya nyckeln `API_KEY_2` genom att ange samma rubrik två gånger (den nya nyckeln ska anges efter den gamla nyckeln). När du har distribuerat detta visas den nya nyckeln i serverdelen.

   ```
   requestTransformations:
     rules:
       - name: set-api-key-header
         actions:
           - type: set
             reqHeader: x-api-key
             value ${{API_KEY_1}}
           - type: set
             reqHeader: x-api-key
             value ${{API_KEY_2}}
   ```

1. Ta bort den gamla nyckeln `API_KEY_1` från konfigurationen. När du har distribuerat detta ser du den nya nyckeln i serverdelen och det är säkert att ta bort den gamla nyckelns miljövariabel.


   ```
   requestTransformations:
     rules:
       - name: set-api-key-header
         actions:
           - type: set
             reqHeader: x-api-key
             value ${{API_KEY_2}}
   ```


