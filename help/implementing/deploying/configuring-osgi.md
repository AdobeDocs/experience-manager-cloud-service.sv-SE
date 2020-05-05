---
title: Konfigurera OSGi för AEM som en molntjänst
description: 'OSGi-konfiguration med hemliga värden och miljöspecifika värden '
translation-type: tm+mt
source-git-commit: c5339a74f948af4c05ecf29bddfe9c0b11722d61

---


# OSGi-konfigurationer {#osgi-configurations}

[OSGi](https://www.osgi.org/) är en grundläggande del i teknikhögen i Adobe Experience Manager (AEM). Det används för att styra de sammansatta paketen av AEM och dess konfigurationer.

OSGi innehåller standardmallar som gör att applikationer kan byggas av små, återanvändbara och samverkande komponenter. Dessa komponenter kan sättas samman till ett program och distribueras. Detta gör det enkelt att hantera OSGi-paket eftersom de kan stoppas, installeras och startas individuellt. De inbördes beroendena hanteras automatiskt. Varje OSGi-komponent finns i ett av de olika paketen. Mer information finns i [OSGi-specifikationen](https://www.osgi.org/Specifications/HomePage).

Du kan hantera konfigurationsinställningarna för OSGi-komponenter genom konfigurationsfiler som ingår i ett AEM-kodprojekt.

## OSGi-konfigurationsfiler {#osgi-configuration-files}

Konfigurationsändringar definieras i AEM-projektets kodpaket (`ui.apps`) som konfigurationsfiler (`.cfg.json`) under körningslägesspecifika konfigurationsmappar:

`/apps/example/config.<runmode>`

Formatet på OSGi-konfigurationsfilerna är JSON-baserat med det format som definieras av Apache Sling-projektet. `.cfg.json`

OSGi-konfigurationer har OSGi-komponenter som mål via PID (Persistent Idenity), som är standard med Java-klassnamnet för OSGi-komponenten. Om du till exempel vill tillhandahålla OSGi-konfiguration för en OSGi-tjänst som implementeras av:

`com.example.workflow.impl.ApprovalWorkflow.java`

en OSGi-konfigurationsfil definieras på:

`/apps/example/config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`

följer konfigurationsformatet []cfg.json OSGi (som följer konfigurationsformatetcfg.json OSGi).

> [!NOTE]
>
> Tidigare versioner av AEM-stödda OSGi-konfigurationsfiler med olika filformat som .cfg., .config och som resursdefinitioner för XML-sling:OsgiConfig. Dessa format har ersatts av konfigurationsformatet cfg.json OSGi.

## Upplösning för körningsläge {#runmode-resolution}

Specifika OSGi-konfigurationer kan riktas mot specifika AEM-instanser med hjälp av runmodes. Om du vill använda körningsläge skapar du konfigurationsmappar under `/apps/example` (där till exempel projektnamnet) i formatet:

`/apps/example/config.<author|publish>.<dev|stage|prod>/`

Alla OSGi-konfigurationer i sådana mappar används om körningslägena som definieras i konfigurationsmappens namn matchar körningslägena som används av AEM.

Om AEM till exempel använder författaren och programvaran för körningslägena kommer konfigurationsnoderna i `/apps/example/config.author/` och `/apps/example/config.author.dev/` att tillämpas, medan konfigurationsnoderna i `/apps/example/config.publish/` och `/apps/example/config.author.stage/` inte kommer att tillämpas.

Om flera konfigurationer för samma PID kan användas, används konfigurationen med det högsta antalet matchande körningslägen.

Regelns granularitet är på PID-nivå. Det innebär att du inte kan definiera vissa egenskaper för samma PID i `/apps/example/config.author/` och mer specifika i `/apps/example/config.author.dev/` för samma PID.  Konfigurationen med det högsta antalet matchande körningslägen gäller för hela PID.

Vid lokal utveckling kan en startparameter för körningsläge skickas in för att ange vilken OSGI-konfiguration som ska användas i körningsläget.

## Typer av OSGi-konfigurationsvärden {#types-of-osgi-configuration-values}

Det finns tre olika OSGi-konfigurationsvärden som kan användas med AEM som molntjänst.

1. **Textbundna värden**, som är värden som är hårdkodade i OSGi-konfigurationen och lagrade i Git. Till exempel:

   ```json
   {
      "connection.timeout": 1000
   }
   ```

1. **Hemliga värden**, som är värden som inte ska lagras i Git av säkerhetsskäl. Till exempel:

   ```json
   {
   "api-key": "$[secret:server-api-key]"
   } 
   ```

1. **Miljöspecifika värden**, som är värden som varierar mellan olika utvecklingsmiljöer, och som därför inte kan användas korrekt i körningsläge (eftersom det finns ett enda `dev` körningsläge i AEM som en molntjänst). Till exempel:

   ```json
   {
    "url": "$[env:server-url]"
   }
   ```

   Observera att en enda OSGi-konfigurationsfil kan använda vilken kombination som helst av dessa konfigurationsvärdetyper tillsammans. Till exempel:

   ```json
   {
   "connection.timeout": 1000,
   "api-key": "$[secret:server-api-key]",
   "url": "$[env:server-url]"
   }
   ```

## Så här väljer du lämplig OSGi-konfigurationsvärdetyp {#how-to-choose-the-appropriate-osgi-configuration-value-type}

I det vanliga fallet för OSGi används inline OSGi-konfigurationsvärden. Miljöspecifika konfigurationer används endast för specifika användningsområden där värdet skiljer sig mellan olika utvecklingsmiljöer.

![](assets/choose-configuration-value-type.png)

Miljöspecifika konfigurationer utökar de traditionella, statiskt definierade OSGi-konfigurationer som innehåller infogade värden, vilket gör det möjligt att hantera OSGi-konfigurationsvärden externt via Cloud Manager API. Det är viktigt att förstå när den vanliga och traditionella metoden för att definiera textbundna värden och lagra dem i Git ska användas, jämfört med att abstrahera värdena till miljöspecifika konfigurationer.

Följande riktlinjer beskriver när icke-hemliga och hemliga miljöspecifika konfigurationer ska användas:

### När infogade konfigurationsvärden ska användas {#when-to-use-inline-configuration-values}

Värden för infogade konfigurationer anses vara standardmetoden och bör användas när det är möjligt. Textbundna konfigurationer ger fördelar med:

* De bevaras, med styrning och versionshistorik i Git
* Värdena är implicit knutna till koddistributioner
* De kräver inga ytterligare distributionsöverväganden eller samordning

När du definierar ett OSGi-konfigurationsvärde börjar du med infogade värden. Om det behövs för användningsfallet väljer du bara hemliga eller miljöspecifika konfigurationer.

### När icke-hemliga miljöspecifika konfigurationsvärden ska användas {#when-to-use-non-secret-environment-specific-configuration-values}

Använd bara miljöspecifika konfigurationer (`$[env:ENV_VAR_NAME]`) för icke-hemliga konfigurationsvärden när värdena varierar mellan olika utvecklingsmiljöer. Detta inkluderar lokala utvecklingsinstanser och alla AEM-miljöer som en molntjänstutvecklingsmiljö. Undvik att använda icke-hemliga miljöspecifika konfigurationer för AEM som molntjänststadium eller produktionsmiljöer.

* Använd bara icke-hemliga miljöspecifika konfigurationer för konfigurationsvärden som skiljer sig åt mellan utvecklingsmiljöer, inklusive lokala utvecklingsinstanser.
* Använd i stället standardvärdena för intern användning i OSGi-konfigurationerna för icke-hemliga värden för scenen och produktionen.  I samband med detta rekommenderas inte att miljöspecifika konfigurationer används för att underlätta konfigurationsändringar under körning till scen- och produktionsmiljöer. dessa ändringar bör införas via källkodshantering.

### När hemliga miljöspecifika konfigurationsvärden ska användas {#when-to-use-secret-environment-specific-configuration-values}

AEM som en molntjänst kräver användning av miljöspecifika konfigurationer (`$[secret:SECRET_VAR_NAME]`) för alla hemliga OSGi-konfigurationsvärden, till exempel lösenord, privata API-nycklar eller andra värden som inte kan lagras i Git av säkerhetsskäl.

Använd hemliga miljöspecifika konfigurationer för att lagra värdet för hemligheter på alla AEM som molntjänstmiljöer, inklusive Stage och Production.

### Lägga till en ny konfiguration i databasen {#adding-a-new-configuration-to-the-repository}

#### Vad du behöver veta {#what-you-need-to-know}

Om du vill lägga till en ny konfiguration i databasen måste du känna till följande:

1. Tjänstens PID ( **Persistent Identity** ).

   Referera till fältet **Konfigurationer** i webbkonsolen. Namnet visas inom parentes efter paketnamnet (eller i **konfigurationsinformationen** längst ned på sidan).

   Skapa till exempel en nod `com.day.cq.wcm.core.impl.VersionManagerImpl.` för att konfigurera **AEM WCM Version Manager**.

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. Om ett specifikt körläge krävs. Skapa mappen:

   * `config` - för alla körningslägen
   * `config.author` - för redigeringsmiljön
   * `config.publish` - för publiceringsmiljön
   * `config.<run-mode>` - i förekommande fall

1. Anger om en **konfiguration** eller **fabrikskonfiguration** krävs.
1. De enskilda parametrar som ska konfigureras. inklusive befintliga parameterdefinitioner som behöver återskapas.

   Referera till det enskilda parameterfältet i webbkonsolen. Namnet visas inom hakparenteser för varje parameter.

   Skapa till exempel en egenskap
   `versionmanager.createVersionOnActivation` för att konfigurera **Skapa version vid aktivering**.

   ![chlimage_1-142](assets/chlimage_1-142.png)

1. Finns det redan en konfiguration i `/libs`? Om du vill visa alla konfigurationer i instansen använder du **frågeverktyget** i CRXDE Lite för att skicka följande SQL-fråga:

   `select * from sling:OsgiConfig`

   I så fall kan konfigurationen kopieras till ` /apps/<yourProject>/`och sedan anpassas på den nya platsen.

## Skapa konfigurationen i databasen {#creating-the-configuration-in-the-repository}

Så här lägger du till den nya konfigurationen i databasen:

1. Använd CRXDE Lite för att navigera till:

   ` /apps/<yourProject>`

1. Om den inte redan finns skapar du `config` mappen ( `sling:Folder`):

   * `config` - gäller för alla körlägen
   * `config.<run-mode>` - specifikt för ett visst körläge

1. Skapa en nod under den här mappen:

   * Typ: `sling:OsgiConfig`
   * Namn: Den beständiga identiteten (PID).

      t.ex. för AEM WCM Version Manager `com.day.cq.wcm.core.impl.VersionManagerImpl`
   >[!NOTE]
   >
   >När en fabrikskonfiguration läggs till `-<identifier>` i namnet.
   >
   >Som i: `org.apache.sling.commons.log.LogManager.factory.config-<identifier>`
   >
   >Där `<identifier>` ersätts av fri text som du (måste) anger för att identifiera förekomsten (du kan inte utelämna denna information); till exempel:
   >
   >`org.apache.sling.commons.log.LogManager.factory.config-MINE`

1. Skapa en egenskap på den här noden för varje parameter som du vill konfigurera:

   * Namn: parameternamnet som visas i webbkonsolen, namnet visas inom parentes i slutet av fältbeskrivningen. Till exempel för `Create Version on Activation` användning `versionmanager.createVersionOnActivation`
   * Typ: i tillämpliga fall.
   * Värde: efter behov.
   Du behöver bara skapa egenskaper för de parametrar som du vill konfigurera, andra använder fortfarande standardvärdena som angetts av AEM.

1. Spara alla ändringar.

   Ändringarna tillämpas så snart noden uppdateras genom att tjänsten startas om (som med ändringarna i webbkonsolen).

>[!CAUTION]
>
>Du får inte ändra något i `/libs` banan.

>[!CAUTION]
>
>Den fullständiga sökvägen till en konfiguration måste vara korrekt för att den ska kunna läsas vid start.


## Konfigurationsegenskapsformat i källkontroll {#configuration-property-format-in-source-control}

Att skapa en ny OSGI-konfigurationsegenskap beskrivs i avsnittet [Lägga till en ny konfiguration i databasen](#creating-the-configuration-in-the-repository) ovan. Följ de här stegen och ändra syntaxen enligt underavsnitten nedan:

### Textbundna värden {#inline-values}

Som man kan förvänta sig formateras infogade värden som namnvärdespar enligt JSON-standardsyntaxen. Till exempel:

```json
 {

 "my_var1": "val",
 "my_var2": "abc",
 "my_var3": 500

}
```

### Miljöspecifika konfigurationsvärden {#environment-specific-configuration-values}

OSGi-konfigurationen ska tilldela en platshållare för variabeln som ska definieras per miljö:

```
use $[env:ENV_VAR_NAME]
```

Kunder bör endast använda den här tekniken för OSGI-konfigurationsegenskaper som är relaterade till deras anpassade kod. den ska inte användas för att åsidosätta Adobe-definierad OSGI-konfiguration.

### Värden för hemlig konfiguration {#secret-configuration-values}

OSGi-konfigurationen ska tilldela en platshållare för hemligheten som ska definieras per miljö:

```
use $[secret:SECRET_VAR_NAME]
```

### Variabelnamn {#variable-naming}

Följande gäller för både miljöspecifika och hemliga konfigurationsvärden.

Variabelnamn ska följa följande regler:

* minsta längd: 2
* maxlängd: 100
* måste matcha regex: `[a-zA-Z_][a-zA-Z_0-9]*`

Värdena för variablerna får inte överstiga 2 048 tecken.

### Standardvärden {#default-values}

Följande gäller för både miljöspecifika och hemliga konfigurationsvärden.

Om inget värde har angetts per miljö ersätts inte platshållaren vid körning och lämnas kvar på plats eftersom ingen interpolering har gjorts. Du kan undvika detta genom att ange ett standardvärde som en del av platshållaren med följande syntax:

```
$[env:ENV_VAR_NAME;default=<value>]
```

När ett standardvärde anges ersätts platshållaren antingen med det angivna per-environment-värdet eller det angivna standardvärdet.

### Lokal utveckling {#local-development}

Följande gäller för både miljöspecifika och hemliga konfigurationsvärden.

Variabler kan definieras i den lokala miljön så att de hämtas av den lokala AEM-tillverkaren vid körning. I Linux:

```bash
export ENV_VAR_NAME=my_value
```

Vi rekommenderar att du skriver ett enkelt basskript som anger de systemvariabler som används i konfigurationerna och kör det innan du startar AEM. Verktyg som [https://direnv.net/älp](https://direnv.net/) om hur du förenklar den här metoden. Beroende på vilken typ av värden det är kan de checkas in i källkodshanteringen om de kan delas mellan alla.

Värdena för hemligheter läses från filer. Därför måste en textfil med det hemliga värdet skapas för varje platshållare som använder en hemlighet.

Om `$[secret:server_password]` används måste t.ex. en textfil med namnet **server_password** skapas. Alla dessa hemliga filer måste lagras i samma katalog och ramverksegenskapen `org.apache.felix.configadmin.plugin.interpolation.secretsdir` måste konfigureras med den lokala katalogen.

### Författare jämfört med Publiceringskonfiguration {#author-vs-publish-configuration}

Om en OSGI-egenskap kräver olika värden för författare jämfört med publicering:

* Separata `config.author` - och `config.publish` OSGi-mappar ska användas, vilket beskrivs i avsnittet [Lösning i körläge](#runmode-resolution).
* oberoende variabelnamn ska användas. Vi rekommenderar att du använder ett prefix som författare_<variablename> och publicera_<variablename> där variabelnamnen är desamma

### Konfigurationsexempel {#configuration-examples}

I exemplen nedan antar vi att det finns tre dev-miljöer förutom scen- och prodmiljöer.

**Exempel 1**

Avsikten är att värdet på OSGI-egenskapen `my_var1` ska vara detsamma för stage och prod, men skiljer sig åt för var och en av de tre utvecklingsmiljöerna.

<table>
<tr>
<td>
<b>Mapp</b>
</td>
<td>
<b>Innehåll i myfile.cfg.json</b>
</td>
</tr>
<tr>
<td>
config
</td>
<td>
<pre>
{ "my_var1": "val", "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1" : "$[env:my_var1]" "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
</table>

**Exempel 2**

Avsikten är att värdet på OSGI-egenskapen ska skilja sig åt `my_var1` för scenen, produkten och för var och en av de tre utvecklingsmiljöerna. Därför måste Cloud Manager API anropas för att ange värdet för `my_var1` varje dev-miljö.

<table>
<tr>
<td>
<b>Mapp</b>
</td>
<td>
<b>Innehåll i myfile.cfg.json</b>
</td>
</tr>
<tr>
<td>
config.stage
</td>
<td>
<pre>
{ "my_var1": "val1", "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
<tr>
<td>
config.prod
</td>
<td>
<pre>
{ "my_var1": "val2", "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1" : "$[env:my_var1]" "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
</table>

**Exempel 3**

Avsikten är att OSGi-egenskapen ska ha samma värde `my_var1` för scenen, produktionen och bara en av utvecklingsmiljöerna, men att den ska skilja sig åt för de två andra utvecklingsmiljöerna. I det här fallet måste Cloud Manager API anropas för att ange värdet för `my_var1` för var och en av utvecklingsmiljöerna, inklusive för utvecklingsmiljön som bör ha samma värde som fas och produktion. Det ärver inte det värde som angetts i mappkonfigurationen ****.

<table>
<tr>
<td>
<b>Mapp</b>
</td>
<td>
<b>Innehåll i myfile.cfg.json</b>
</td>
</tr>
<tr>
<td>
config
</td>
<td>
<pre>
{ "my_var1": "val1", "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1" : "$[env:my_var1]" "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
</table>

Ett annat sätt att uppnå detta är att ange ett standardvärde för ersättningstoken i mappen config.dev så att det har samma värde som i mappen **config** .

<table>
<tr>
<td>
<b>Mapp</b>
</td>
<td>
<b>Innehåll i myfile.cfg.json</b>
</td>
</tr>
<tr>
<td>
config
</td>
<td>
<pre>
{ "my_var1": "val1", "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1": "$[env:my_var1;default=val1]" "my_var2": "abc", "my_var3": 500}
</pre>
</td>
</tr>
</table>

## API-format för Cloud Manager för att ange egenskaper {#cloud-manager-api-format-for-setting-properties}

### Ange värden via API {#setting-values-via-api}

Anrop av API:t distribuerar de nya variablerna och värdena till en molnmiljö, ungefär som en vanlig pipeline för kundkoddistribution. Skapare- och publiceringstjänsterna startas om och de nya värdena anges, vilket normalt tar några minuter.

```
PATCH /program/{programId}/environment/{environmentId}/variables
```

```
]
        {
                "name" : "MY_VAR1",
                "value" : "plaintext value",
                "type" : "string"  <---default
        },
        {
                "name" : "MY_VAR2",
                "value" : "<secret value>",
                "type" : "secretString"
        }
]
```

Observera att standardvariabler inte ställs in via API, utan i själva OSGi-egenskapen.

Mer information finns [på den här sidan](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Environment_Variables/patchEnvironmentVariables) .

### Hämta värden via API {#getting-values-via-api}

```
GET /program/{programId}/environment/{environmentId}/variables
```

Mer information finns [på den här sidan](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Environment_Variables/getEnvironmentVariables) .

### Ta bort värden via API {#deleting-values-via-api}

```
PATCH /program/{programId}/environment/{environmentId}/variables
```

Om du vill ta bort en variabel inkluderar du den med ett tomt värde.

Mer information finns [på den här sidan](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Environment_Variables/patchEnvironmentVariables) .

### Hämta värden via kommandoraden {#getting-values-via-cli}

```bash
$ aio cloudmanager:list-environment-variables ENVIRONMENT_ID
Name     Type         Value
MY_VAR1  string       plaintext value 
MY_VAR2  secretString ****
```


### Ange värden via kommandoraden {#setting-values-via-cli}

```bash
$ aio cloudmanager:set-environment-variables ENVIRONMENT_ID --variable MY_VAR1 "plaintext value" --secret MY_VAR2 "some secret value"
```

### Ta bort värden via kommandoraden {#deleting-values-via-cli}

```bash
$ aio cloudmanager:set-environment-variables ENVIRONMENT_ID --delete MY_VAR1 MY_VAR2
```

> [!NOTE]
>
> På [den här sidan](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) finns mer information om hur du konfigurerar värden med plugin-programmet Cloud Manager för Adobe I/O CLI.

### Antal variabler {#number-of-variables}

Upp till 20 variabler kan deklareras.

## Distributionsöverväganden för Hemliga och miljöspecifika konfigurationsvärden {#deployment-considerations-for-secret-and-environment-specific-configuration-values}

Eftersom de hemliga och miljöspecifika konfigurationsvärdena finns utanför Git, och därför inte är en del av den formella AEM som en distributionsmekanism för molntjänster, bör kunden hantera, styra och integrera i AEM som en distributionsprocess för molntjänster.

Som nämnts ovan kommer anrop till API att distribuera de nya variablerna och värdena till molnmiljöer, ungefär som en vanlig pipeline för kundkoddistribution. Skapare- och publiceringstjänsterna startas om och de nya värdena anges, vilket normalt tar några minuter. Observera att de kvalitetsportar och tester som körs av Cloud Manager under en vanlig koddistribution inte utförs under den här processen.

Normalt anropar kunderna API för att ange miljövariabler innan de distribuerar kod som är beroende av dem i Cloud Manager. I vissa fall kanske du vill ändra en befintlig variabel efter att koden redan har distribuerats.

Observera att API:t kanske inte fungerar när en pipeline används, antingen en AEM-uppdatering eller en kunddistribution, beroende på vilken del av slutpipeline som körs vid den tidpunkten. Felsvaret kommer att ange att begäran inte lyckades, men det kommer inte att ange den specifika orsaken.

Det kan finnas scenarier där en schemalagd kundkoddistribution förlitar sig på befintliga variabler för att ha nya värden, vilket inte är lämpligt med den aktuella koden. Om detta ger anledning till oro bör variabla ändringar göras på ett additivt sätt. Det gör du genom att skapa nya variabelnamn i stället för att bara ändra värdet för gamla variabler så att gammal kod aldrig refererar till det nya värdet. När den nya kundreleasen ser stabil ut kan man välja att ta bort de äldre värdena.

Eftersom variabelns värden inte är versionshanterade kan en återställning av koden få den att referera till nyare värden som orsakar problem. Denna additiva variabelstrategi skulle också vara till hjälp här.

Den här additiva variabelstrategin är också användbar för scenarier där, om kod från flera dagar tidigare behövde omdistribueras, variabelnamnen och värdena som den refererar till fortfarande är intakta. Detta bygger på en strategi där kunden väntar några dagar innan de tar bort de äldre variablerna, annars har den äldre koden inte rätt variabler att referera till.