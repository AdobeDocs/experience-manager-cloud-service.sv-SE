---
title: Konfigurera OSGI för AEM as a Cloud Service
description: 'OSGi-konfiguration med hemliga värden och miljöspecifika värden '
translation-type: tm+mt
source-git-commit: 24f26a5cc77158ea20a09b1f40cf3d849a70591f
workflow-type: tm+mt
source-wordcount: '2737'
ht-degree: 1%

---


# Konfigurera OSGI för AEM as a Cloud Service {#configuring-osgi-for-aem-as-a-cloud-service}

[OSG ](https://www.osgi.org/) är en viktig del i Adobe Experience Manager (AEM) teknikstack. Det används för att styra de sammansatta paketen av AEM och dess konfigurationer.

OSGi innehåller standardmallar som gör att applikationer kan byggas av små, återanvändbara och samverkande komponenter. Dessa komponenter kan sättas samman till ett program och distribueras. Detta gör det enkelt att hantera OSGi-paket eftersom de kan stoppas, installeras och startas individuellt. De inbördes beroendena hanteras automatiskt. Varje OSGi-komponent finns i ett av de olika paketen. Mer information finns i [OSGi-specifikationen](https://www.osgi.org/Specifications/HomePage).

Du kan hantera konfigurationsinställningarna för OSGi-komponenter genom konfigurationsfiler som ingår i ett AEM kodprojekt.

## OSGi-konfigurationsfiler {#osgi-configuration-files}

Konfigurationsändringar definieras i AEM Project-kodpaket (`ui.apps`) som konfigurationsfiler (`.cfg.json`) under körningsspecifika konfigurationsmappar:

`/apps/example/config.<runmode>`

Formatet på OSGi-konfigurationsfilerna är JSON-baserat med formatet `.cfg.json` som definieras av Apache Sling-projektet.

OSGi-konfigurationer har OSGi-komponenter som mål via PID (Persistent Idenity), som är standard med Java-klassnamnet för OSGi-komponenten. Om du till exempel vill tillhandahålla OSGi-konfiguration för en OSGi-tjänst som implementeras av:

`com.example.workflow.impl.ApprovalWorkflow.java`

en OSGi-konfigurationsfil definieras på:

`/apps/example/config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`

efter konfigurationsformatet cfg.json OSGi.

>[!NOTE]
>
>Tidigare versioner av AEM OSGi-konfigurationsfiler som stöds med olika filformat som .cfg., .config och som resursdefinitioner för XML-sling:OsgiConfig. Dessa format har ersatts av konfigurationsformatet cfg.json OSGi.

## Upplösning för körläge {#runmode-resolution}

Specifika OSGi-konfigurationer kan riktas mot specifika AEM genom att använda runmodes. Om du vill använda körningsläget skapar du konfigurationsmappar under `/apps/example` (där exemplet är ditt projektnamn) i formatet:

`/apps/example/config.<author|publish>.<dev|stage|prod>/`

Alla OSGi-konfigurationer i sådana mappar används om körningslägena som definieras i konfigurationsmappens namn matchar de körningslägen som används av AEM.

Om AEM t.ex. använder författare och dev för körningslägena kommer konfigurationsnoderna i `/apps/example/config.author/` och `/apps/example/config.author.dev/` att tillämpas, medan konfigurationsnoderna i `/apps/example/config.publish/` och `/apps/example/config.author.stage/` inte kommer att tillämpas.

Om flera konfigurationer för samma PID kan användas, används konfigurationen med det högsta antalet matchande körningslägen.

Regelns granularitet är på PID-nivå. Det innebär att du inte kan definiera vissa egenskaper för samma PID i `/apps/example/config.author/` och mer specifika i `/apps/example/config.author.dev/` för samma PID.  Konfigurationen med det högsta antalet matchande körningslägen gäller för hela PID.

När du utvecklar lokalt kan en startparameter för körningsläge skickas in för att ange vilken OSGI-konfiguration som ska användas i körningsläget.

## Typer av OSGi-konfigurationsvärden {#types-of-osgi-configuration-values}

Det finns tre sorters OSGi-konfigurationsvärden som kan användas med AEM som Cloud Service.

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

1. **Miljöspecifika värden**, som är värden som varierar mellan olika utvecklingsmiljöer, och som därför inte kan anges korrekt av körningsläget (eftersom det finns ett enda  `dev` körningsläge i AEM som Cloud Service). Till exempel:

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

## Välj lämplig OSGi-konfigurationsvärdetyp {#how-to-choose-the-appropriate-osgi-configuration-value-type}

I det vanliga fallet för OSGi används inline OSGi-konfigurationsvärden. Miljöspecifika konfigurationer används endast för specifika användningsområden där värdet skiljer sig mellan olika utvecklingsmiljöer.

![](assets/choose-configuration-value-type_res1.png)

Miljöspecifika konfigurationer utökar de traditionella, statiskt definierade OSGi-konfigurationer som innehåller infogade värden, vilket gör det möjligt att hantera OSGi-konfigurationsvärden externt via Cloud Manager API. Det är viktigt att förstå när den vanliga och traditionella metoden för att definiera textbundna värden och lagra dem i Git ska användas, jämfört med att abstrahera värdena till miljöspecifika konfigurationer.

Följande riktlinjer beskriver när icke-hemliga och hemliga miljöspecifika konfigurationer ska användas:

### När infogade konfigurationsvärden ska användas {#when-to-use-inline-configuration-values}

Värden för infogade konfigurationer anses vara standardmetoden och bör användas när det är möjligt. Textbundna konfigurationer ger fördelar med:

* De bevaras, med styrning och versionshistorik i Git
* Värdena är implicit knutna till koddistributioner
* De kräver inga ytterligare distributionsöverväganden eller samordning

När du definierar ett OSGi-konfigurationsvärde börjar du med infogade värden, där du bara väljer hemliga eller miljöspecifika konfigurationer om det behövs för användningsfallet.

### När icke-hemliga miljöspecifika konfigurationsvärden ska användas {#when-to-use-non-secret-environment-specific-configuration-values}

Använd bara miljöspecifika konfigurationer (`$[env:ENV_VAR_NAME]`) för icke-hemliga konfigurationsvärden när värdena varierar mellan olika utvecklingsmiljöer. Detta omfattar lokala utvecklingsinstanser och alla AEM som en Cloud Service Development-miljö. Undvik att använda icke-hemliga miljöspecifika konfigurationer för AEM som Cloud Service- eller produktionsmiljöer.

* Använd bara icke-hemliga miljöspecifika konfigurationer för konfigurationsvärden som skiljer sig åt mellan utvecklingsmiljöer, inklusive lokala utvecklingsinstanser.
* Använd i stället standardvärdena för intern användning i OSGi-konfigurationerna för icke-hemliga värden för scenen och produktionen.  I samband med detta rekommenderas inte att miljöspecifika konfigurationer används för att underlätta konfigurationsändringar under körning till scen- och produktionsmiljöer. dessa ändringar bör införas via källkodshantering.

### När hemliga miljöspecifika konfigurationsvärden ska användas {#when-to-use-secret-environment-specific-configuration-values}

AEM som en Cloud Service kräver att miljöspecifika konfigurationer (`$[secret:SECRET_VAR_NAME]`) används för alla hemliga OSGi-konfigurationsvärden, till exempel lösenord, privata API-nycklar eller andra värden som inte kan lagras i Git av säkerhetsskäl.

Använd hemliga miljöspecifika konfigurationer för att lagra värdet för hemligheter på alla AEM som en Cloud Service, inklusive scenen och produktionen.

<!-- ### Adding a New Configuration to the Repository {#adding-a-new-configuration-to-the-repository}

#### What You Need to Know {#what-you-need-to-know}

To add a new configuration to the repository you need to know the following:

1. The **Persistent Identity** (PID) of the service.

   Reference the **Configurations** field in the Web console. The name is shown in brackets after the bundle name (or in the **Configuration Information** towards the bottom of the page).

   For example, create a node `com.day.cq.wcm.core.impl.VersionManagerImpl.` to configure **AEM WCM Version Manager**.

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. Whether a specific runmode is required. Create the folder:

    * `config` - for all run modes
    * `config.author` - for the author environment
    * `config.publish` - for the publish environment
    * `config.<run-mode>` - as appropriate

1. Whether a **Configuration** or **Factory Configuration** is necessary.
1. The individual parameters to be configured; including any existing parameter definitions that will need to be recreated.

   Reference the individual parameter field in the Web console. The name is shown in brackets for each parameter.

   For example, create a property
   `versionmanager.createVersionOnActivation` to configure **Create Version on Activation**.

   ![chlimage_1-142](assets/chlimage_1-142.png)

1. Does a configuration already exist in `/libs`? To list all configurations in your instance, use the **Query** tool in CRXDE Lite to submit the following SQL query:

   `select * from sling:OsgiConfig`

   If so, this configuration can be copied to ` /apps/<yourProject>/`, then customized in the new location. -->

## Skapar OSGi-konfigurationer {#creating-sogi-configurations}

Det finns två sätt att skapa nya OSGi-konfigurationer enligt beskrivningen nedan. Den tidigare metoden används vanligtvis för att konfigurera anpassade OSGi-komponenter som har välkända OSGi-egenskaper och -värden av utvecklaren, och den senare för AEM OSGi-komponenter.

### Skriver OSGi-konfigurationer {#writing-osgi-configurations}

JSON-formaterade OSGi-konfigurationsfiler kan skrivas för hand direkt i AEM. Detta är ofta det snabbaste sättet att skapa OSGi-konfigurationer för välkända OSGi-komponenter, och särskilt anpassade OSGi-komponenter som har utformats och utvecklats av samma utvecklare som definierar konfigurationerna. Den här metoden kan även användas för att kopiera/klistra in och uppdatera konfigurationer för samma OSGi-komponent i olika körningslägemappar.

1. I din utvecklingsmiljö öppnar du `ui.apps`-projektet, letar upp eller skapar konfigurationsmappen (`/apps/.../config.<runmode>`) som är avsedd för de körningslägen som den nya OSGi-konfigurationen ska gälla för
1. Skapa en ny `<PID>.cfg.json`-fil i den här konfigurationsmappen. PID är den beständiga identiteten för OSGi-komponenten är vanligtvis OSGi-komponentimplementeringens fullständiga klassnamn. Till exempel:
   `/apps/.../config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`
Observera att namnet på OSGi-konfigurationsfabriksfilen använder  `<PID>-<factory-name>.cfg.json` namnkonventionen
1. Öppna den nya `.cfg.json`-filen och definiera nyckel/värde-kombinationerna för OSGi-egenskapen och -värdepar enligt [JSON OSGi-konfigurationsformatet](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1).
1. Spara ändringarna i den nya `.cfg.json`-filen
1. Lägg till och implementera din nya OSGi-konfigurationsfil i Git

### Generera OSGi-konfigurationer med AEM SDK QuickStart {#generating-osgi-configurations-using-the-aem-sdk-quickstart}

AEM SDK Quickstart Jars AEM Web Console kan användas för att konfigurera OSGi-komponenter och exportera OSGi-konfigurationer som JSON. Detta är användbart för att konfigurera AEM OSGi-komponenter vars OSGi-egenskaper och deras värdeformat kanske inte är väl förstådda av den utvecklare som definierar OSGi-konfigurationerna i det AEM projektet. Observera att när du använder konfigurationsgränssnittet för AEM Web Console skriver du `.cfg.json`-filer i databasen, så tänk på detta för att undvika oväntade beteenden under lokal utveckling när de AEM projektdefinierade OSGi-konfigurationerna kan skilja sig från de genererade konfigurationerna.

1. Logga in på AEM SDK Quickstart Jars AEM Web console som admin-användare
1. Navigera till OSGi > Konfiguration
1. Leta reda på OSGi-komponenten som ska konfigureras och tryck på titeln för att redigera
   ![OSGi-konfiguration](./assets/configuring-osgi/configuration.png)
1. Redigera OSGi-konfigurationens egenskapsvärden via webbgränssnittet efter behov
1. Registrera Persistent Identity (PID) på en säker plats. Den används senare för att generera OSGi-konfigurationens JSON
1. Tryck på Spara
1. Navigera till OSGi > OSGi Installer Configuration Printer
1. Klistra in den PID som kopierats i steg 5, kontrollera att Serialization Format är inställt på OSGi Configurator JSON
1. Tryck på Skriv ut,
1. OSGi-konfigurationen i JSON-format visas i avsnittet Serialiserade konfigurationsegenskaper
   ![Skrivare för OSGi-installationskonfiguration](./assets/configuring-osgi/osgi-installer-configurator-printer.png)
1. I den utvecklingsmiljö du använder öppnar du `ui.apps`-projektet, letar upp eller skapar konfigurationsmappen (`/apps/.../config.<runmode>`) som är avsedd för de körningslägen som den nya OSGi-konfigurationen ska använda.
1. Skapa en ny `<PID>.cfg.json`-fil i den här konfigurationsmappen. PID är samma värde från steg 5.
1. Klistra in serialiserade konfigurationsegenskaper från steg 10 i `.cfg.json`-filen.
1. Spara ändringarna i den nya `.cfg.json`-filen.
1. Lägg till och implementera den nya OSGi-konfigurationsfilen i Git.


## Egenskapsformat för OSGi-konfiguration {#osgi-configuration-property-formats}

### Textbundna värden {#inline-values}

Som man kan förvänta sig formateras infogade värden som namnvärdespar enligt JSON-standardsyntaxen. Till exempel:

```json
{
   "my_var1": "val",
   "my_var2": [ "abc", "def" ],
   "my_var3": 500
}
```

### Miljöspecifika konfigurationsvärden {#environment-specific-configuration-values}

OSGi-konfigurationen ska tilldela en platshållare för variabeln som ska definieras per miljö:

```
use $[env:ENV_VAR_NAME]
```

Kunder bör endast använda den här tekniken för OSGI-konfigurationsegenskaper som är relaterade till deras anpassade kod. Den ska inte användas för att åsidosätta Adobe-definierad OSGI-konfiguration.

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

Variabler kan definieras i den lokala miljön så att de hämtas av den lokala AEM vid körning. I Linux:

```bash
export ENV_VAR_NAME=my_value
```

Vi rekommenderar att du skriver ett enkelt basskript som anger de systemvariabler som används i konfigurationerna och kör det innan du startar AEM. Verktyg som [https://direnv.net/](https://direnv.net/) hjälper dig att förenkla den här metoden. Beroende på vilken typ av värden det är kan de checkas in i källkodshanteringen om de kan delas mellan alla.

Värdena för hemligheter läses från filer. Därför måste en textfil med det hemliga värdet skapas för varje platshållare som använder en hemlighet.

Om du till exempel använder `$[secret:server_password]` måste en textfil med namnet **server_password** skapas. Alla dessa hemliga filer måste lagras i samma katalog och ramverksegenskapen `org.apache.felix.configadmin.plugin.interpolation.secretsdir` måste konfigureras med den lokala katalogen.

### Författare jämfört med Publiceringskonfiguration {#author-vs-publish-configuration}

Om en OSGI-egenskap kräver olika värden för författare jämfört med publicering:

* separata mappar för `config.author` och `config.publish` OSGi ska användas, enligt beskrivningen i [Lösning i körläge](#runmode-resolution).
* oberoende variabelnamn ska användas. Vi rekommenderar att du använder ett prefix som `author_<variablename>` och `publish_<variablename>` där variabelnamnen är desamma

### Konfigurationsexempel {#configuration-examples}

I exemplen nedan antar vi att det finns tre dev-miljöer förutom scen- och prodmiljöer.

**Exempel 1**

Avsikten är att värdet för OSGI-egenskapen `my_var1` ska vara detsamma för stage och prod, men skiljer sig åt för var och en av de tre utvecklingsmiljöerna.

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
{ 
 "my_var1": "val",
 "my_var2": "abc",
 "my_var3": 500
}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ 
 "my_var1" : "$[env:my_var1]"
 "my_var2": "abc",
 "my_var3": 500
}
</pre>
</td>
</tr>
</table>

**Exempel 2**

Avsikten är att värdet för OSGI-egenskapen `my_var1` ska skilja sig åt för stage, prod och för var och en av de tre dev-miljöerna. Därför måste Cloud Manager API anropas för att ange värdet för `my_var1` för varje dev-miljö.

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
{ 
 "my_var1": "val1",
 "my_var2": "abc",
 "my_var3": 500
}
</pre>
</td>
</tr>
<tr>
<td>
config.prod
</td>
<td>
<pre>
{ 
 "my_var1": "val2",
 "my_var2": "abc",
 "my_var3": 500
}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ 
 "my_var1" : "$[env:my_var1]"
 "my_var2": "abc",
 "my_var3": 500
}
</pre>
</td>
</tr>
</table>

**Exempel 3**

Avsikten är att OSGi-egenskapen `my_var1` ska vara samma för scenen, produktionen och bara en av utvecklingsmiljöerna, men att den ska vara annorlunda för de två andra utvecklingsmiljöerna. I det här fallet måste Cloud Manager API anropas för att ange värdet `my_var1` för var och en av utvecklingsmiljöerna, inklusive för utvecklingsmiljön som ska ha samma värde som fas och produktion. Det ärver inte det värde som angetts i mappen **config**.

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
{ 
 "my_var1": "val1",
 "my_var2": "abc",
 "my_var3": 500
}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ 
 "my_var1" : "$[env:my_var1]"
 "my_var2": "abc",
 "my_var3": 500
}
</pre>
</td>
</tr>
</table>

Ett annat sätt att uppnå detta är att ange ett standardvärde för ersättningstoken i mappen config.dev så att det är samma värde som i mappen **config**.

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
{ 
 "my_var1": "val1",
 "my_var2": "abc",
 "my_var3": 500
}
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ 
 "my_var1": "$[env:my_var1;default=val1]"
 "my_var2": "abc",
 "my_var3": 500
}
</pre>
</td>
</tr>
</table>

## API-format för Cloud Manager för att ange egenskaper {#cloud-manager-api-format-for-setting-properties}

Se [den här sidan](https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html#!AdobeDocs/cloudmanager-api-docs/master/create-api-integration.md) om hur API:t måste konfigureras.
>[!NOTE]
>
>Kontrollera att det använda Cloud Manager-API:t har tilldelats rollen &quot;Deployment Manager - Cloud Service&quot;. Andra roller kan inte köra alla kommandon nedan.

### Ange värden via API {#setting-values-via-api}

Anrop av API:t distribuerar de nya variablerna och värdena till en molnmiljö, ungefär som en vanlig pipeline för kundkoddistribution. Tjänsterna för författare och publicering kommer att startas om och de nya värdena anges, vilket normalt tar några minuter.

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

Mer information finns på [den här sidan](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Environment_Variables/patchEnvironmentVariables).

### Hämta värden via API {#getting-values-via-api}

```
GET /program/{programId}/environment/{environmentId}/variables
```

Mer information finns på [den här sidan](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Environment_Variables/getEnvironmentVariables).

### Tar bort värden via API {#deleting-values-via-api}

```
PATCH /program/{programId}/environment/{environmentId}/variables
```

Om du vill ta bort en variabel inkluderar du den med ett tomt värde.

Mer information finns på [den här sidan](https://www.adobe.io/apis/experiencecloud/cloud-manager/api-reference.html#/Environment_Variables/patchEnvironmentVariables).

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

### Tar bort värden via kommandoraden {#deleting-values-via-cli}

```bash
$ aio cloudmanager:set-environment-variables ENVIRONMENT_ID --delete MY_VAR1 MY_VAR2
```

>[!NOTE]
>
>På [den här sidan](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) finns mer information om hur du konfigurerar värden med Cloud Manager-pluginprogrammet för Adobe I/O CLI.

### Antal variabler {#number-of-variables}

Upp till 200 variabler per miljö kan deklareras.

## Distributionsöverväganden för sekretess- och miljöspecifika konfigurationsvärden {#deployment-considerations-for-secret-and-environment-specific-configuration-values}

Eftersom de hemliga och miljöspecifika konfigurationsvärdena finns utanför Git, och därför inte är en del av det formella AEM som en distributionsmekanism för Cloud Service, bör kunden hantera, styra och integrera i AEM som en distributionsprocess för Cloud Service.

Som nämnts ovan kommer anrop till API att distribuera de nya variablerna och värdena till molnmiljöer, ungefär som en vanlig pipeline för kundkoddistribution. Tjänsterna för författare och publicering kommer att startas om och de nya värdena anges, vilket normalt tar några minuter. Observera att de kvalitetsportar och tester som körs av Cloud Manager under en vanlig koddistribution inte utförs under den här processen.

Normalt anropar kunderna API för att ange miljövariabler innan de distribuerar kod som är beroende av dem i Cloud Manager. I vissa fall kanske du vill ändra en befintlig variabel efter att koden redan har distribuerats.

Observera att API:t kanske inte fungerar när en pipeline används, antingen en AEM eller en kunddistribution, beroende på vilken del av end to end-pipeline som körs vid den tidpunkten. Felsvaret kommer att ange att begäran inte lyckades, men det kommer inte att ange den specifika orsaken.

Det kan finnas scenarier där en schemalagd kundkoddistribution förlitar sig på befintliga variabler för att ha nya värden, vilket inte är lämpligt med den aktuella koden. Om detta ger anledning till oro bör variabla ändringar göras på ett additivt sätt. Det gör du genom att skapa nya variabelnamn i stället för att bara ändra värdet för gamla variabler så att gammal kod aldrig refererar till det nya värdet. När den nya kundreleasen ser stabil ut kan man välja att ta bort de äldre värdena.

Eftersom variabelns värden inte är versionshanterade kan en återställning av koden få den att referera till nyare värden som orsakar problem. Denna additiva variabelstrategi skulle också vara till hjälp här.

Den här additiva variabelstrategin är också användbar för scenarier där, om kod från flera dagar tidigare behövde omdistribueras, variabelnamnen och värdena som den refererar till fortfarande är intakta. Detta bygger på en strategi där kunden väntar några dagar innan de tar bort de äldre variablerna, annars har den äldre koden inte rätt variabler att referera till.
