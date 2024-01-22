---
title: Konfigurera OSGi för Adobe Experience Manager as a Cloud Service
description: OSGi-konfiguration med hemliga värden och miljöspecifika värden
feature: Deploying
exl-id: f31bff80-2565-4cd8-8978-d0fd75446e15
source-git-commit: a230efaa58cb00e8a0c0e2b23f0cc07462cc658b
workflow-type: tm+mt
source-wordcount: '3269'
ht-degree: 0%

---


# Konfigurera OSGi för Adobe Experience Manager as a Cloud Service {#configuring-osgi-for-aem-as-a-cloud-service}

[OSGi](https://www.osgi.org/) är en grundläggande del i Adobe Experience Manager (AEM) teknikstack. Det används för att styra de sammansatta paketen av AEM och dess konfigurationer.

OSGi innehåller standardmallar som gör att applikationer kan byggas av små, återanvändbara och samverkansbaserade komponenter. Dessa komponenter kan sättas samman till ett program och distribueras. Detta gör det enkelt att hantera OSGi-paket eftersom de kan stoppas, installeras och startas individuellt. De inbördes beroendena hanteras automatiskt. Varje OSGi-komponent finns i ett av de olika paketen. Mer information finns i [OSGi-specifikation](https://help.eclipse.org/latest/index.jsp).

Du kan hantera konfigurationsinställningarna för OSGi-komponenter genom konfigurationsfiler som ingår i ett AEM kodprojekt.

>[!TIP]
>
>Du kan använda Cloud Manager för att konfigurera miljövariabler. Mer information finns i dokumentationen [här.](/help/implementing/cloud-manager/environment-variables.md)

## OSGi-konfigurationsfiler {#osgi-configuration-files}

Konfigurationsändringar definieras i AEM Project-kodpaket (`ui.apps`) som konfigurationsfiler (`.cfg.json`) under körningslägesspecifika konfigurationsmappar:

`/apps/example/config.<runmode>`

Formatet för OSGi-konfigurationsfiler är JSON-baserat med `.cfg.json` format som definieras av Apache Sling-projektet.

OSGi-konfigurationer har OSGi-komponenter som mål via deras PID (Persistent Identity), som är standard med OSGi-komponentens Java™-klassnamn. Om du till exempel vill tillhandahålla OSGi-konfiguration för en OSGi-tjänst som implementeras av:

`com.example.workflow.impl.ApprovalWorkflow.java`

en OSGi-konfigurationsfil definieras på:

`/apps/example/config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`

följer `cfg.json` Konfigurationsformat för OSGi.

>[!NOTE]
>
>Tidigare versioner AEM OSGi-konfigurationsfiler som stöds med olika filformat, som `.cfg`, `.config` och som XML `sling:OsgiConfig` resursdefinitioner. Dessa format har ersatts av `.cfg.json` Konfigurationsformat för OSGi.

## Upplösning för körningsläge {#runmode-resolution}

>[!TIP]
>
>AEM 6.x stöder anpassade runmodes, men det gör AEM as a Cloud Service inte. AEM as a Cloud Service stöd och [exakt uppsättning av körningslägen](./overview.md#runmodes). Alla variationer i OSGi-konfigurationer mellan AEM as a Cloud Service miljöer måste hanteras med [OSGi-konfigurationsmiljövariabler](#environment-specific-configuration-values).

Specifika OSGi-konfigurationer kan riktas mot specifika AEM genom att använda runmodes. Om du vill använda körningsläget skapar du konfigurationsmappar under `/apps/example` (där till exempel är ditt projektnamn), i formatet:

`/apps/example/config.<author|publish>.<dev|stage|prod>/`

Alla OSGi-konfigurationer i sådana mappar används om de körningslägen som definieras i konfigurationsmappens namn matchar de körningslägen som används av AEM.

Om AEM t.ex. använder författaren och utvecklaren av runmodes, kommer konfigurationsnoderna i `/apps/example/config.author/` och `/apps/example/config.author.dev/` används, medan konfigurationsnoder i `/apps/example/config.publish/` och `/apps/example/config.author.stage/` används inte.

Om flera konfigurationer för samma PID kan användas, används konfigurationen med det högsta antalet matchande körningslägen.

Regelns granularitet är på PID-nivå. Det innebär att du inte kan definiera vissa egenskaper för samma PID i `/apps/example/config.author/` och mer specifika `/apps/example/config.author.dev/` för samma PID. Konfigurationen med det högsta antalet matchande körningslägen gäller för hela PID.

>[!NOTE]
>
>A `config.preview` Konfigurationsmapp för OSGi **inte** deklareras på samma sätt som `config.publish` kan deklareras som en mapp. I stället ärver förhandsgranskningsnivån sin OSGi-konfiguration från publiceringsskiktets värden.

Vid lokal utveckling, en startparameter för körningsläge, `-r`, används för att ange OSGI-konfigurationen för runmode.

```shell
$ java -jar aem-sdk-quickstart-xxxx.x.xxx.xxxx-xxxx.jar -r publish,dev
```

### Verifiera körningslägen

AEM as a Cloud Service runmodes är väl definierade baserat på miljötyp och tjänst. Granska [fullständig lista över tillgängliga AEM as a Cloud Service körningslägen](./overview.md#runmodes).

OSGi-konfigurationsvärden som anges av körningsläget kan verifieras av:

1. Öppna AEM som en Cloud Services-miljöns [Developer Console](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html)
1. Välja vilka tjänstenivåer som ska inspekteras med __Pod__ listruta
1. Markera __Status__ tab
1. Markera __Konfigurationer__ från __Statusdump__ listruta
1. Markera __Hämta status__ knapp

I den resulterande vyn visas alla OSGi-komponentkonfigurationer för de valda nivåerna med de tillämpliga OSGi-konfigurationsvärdena. Dessa värden kan korsrefereras med OSGi-konfigurationsvärdena i AEM källkod under `/apps/example/osgiconfig/config.<runmode(s)>`.


Så här kontrollerar du att rätt OSGi-konfigurationsvärden används:

1. I Developer Console&#39;s Configuration output
1. Leta reda på `pid` representerar OSGi-konfigurationen som ska verifieras. Detta är namnet på OSGi-konfigurationsfilen i AEM källkod.
1. Inspect `properties` listan för `pid` och verifiera att nyckeln och värdena matchar OSGi-konfigurationsfilen i AEM projektkällkod för det körläge som verifieras.=


## Typer av OSGi-konfigurationsvärden {#types-of-osgi-configuration-values}

Det finns tre sorters OSGi-konfigurationsvärden som kan användas med Adobe Experience Manager as a Cloud Service.

1. **Textbundna värden**, som är värden som är hårdkodade i OSGi-konfigurationen och lagrade i Git. Till exempel:

   ```json
   {
      "connection.timeout": 1000
   }
   ```

1. **Hemliga värden**, som är värden som inte får lagras i Git av säkerhetsskäl. Till exempel:

   ```json
   {
   "api-key": "$[secret:server-api-key]"
   } 
   ```

1. **Miljöspecifika värden**, som är värden som varierar mellan utvecklingsmiljöer och därför inte kan anges korrekt i körningsläge (eftersom det finns en enda `dev` runmode i Adobe Experience Manager as a Cloud Service). Till exempel:

   ```json
   {
    "url": "$[env:server-url]"
   }
   ```

   En enskild OSGi-konfigurationsfil kan använda vilken kombination som helst av dessa konfigurationsvärdetyper tillsammans. Till exempel:

   ```json
   {
   "connection.timeout": 1000,
   "api-key": "$[secret:server-api-key]",
   "url": "$[env:server-url]"
   }
   ```

## Så här väljer du lämplig OSGi-konfigurationsvärdetyp {#how-to-choose-the-appropriate-osgi-configuration-value-type}

I det vanliga fallet för OSGi används inline OSGi-konfigurationsvärden. Miljöspecifika konfigurationer används endast för specifika användningsområden där värdet skiljer sig mellan olika utvecklingsmiljöer.

![Beslutsträd om hur du använder rätt typ av konfigurationsvärde](assets/choose-configuration-value-type_res1.png)

Miljöspecifika konfigurationer utökar de traditionella, statiskt definierade OSGi-konfigurationer som innehåller infogade värden, vilket ger möjlighet att hantera OSGi-konfigurationsvärden externt via Cloud Manager API. Det är viktigt att förstå när den vanliga och traditionella metoden för att definiera textbundna värden och lagra dem i Git ska användas, jämfört med att abstrahera värdena till miljöspecifika konfigurationer.

Följande riktlinjer beskriver när icke-hemliga och hemliga miljöspecifika konfigurationer ska användas:

### Använda interna konfigurationsvärden {#when-to-use-inline-configuration-values}

Värden för infogade konfigurationer anses vara standardmetoden och bör användas när det är möjligt. Textbundna konfigurationer ger fördelar med:

* De bevaras, med styrning och versionshistorik i Git
* Värdena är implicit knutna till koddistributioner
* De kräver inga ytterligare distributionsöverväganden eller samordning

När du definierar ett OSGi-konfigurationsvärde börjar du med infogade värden och väljer bara hemliga eller miljöspecifika konfigurationer om det behövs för användningsfallet.

### När icke-hemliga miljöspecifika konfigurationsvärden ska användas {#when-to-use-non-secret-environment-specific-configuration-values}

Använd endast miljöspecifika konfigurationer (`$[env:ENV_VAR_NAME]`) för icke-hemliga konfigurationsvärden när värdena varierar för förhandsvisningsnivån eller varierar mellan olika utvecklingsmiljöer. Detta omfattar lokala utvecklingsinstanser och alla Adobe Experience Manager as a Cloud Service utvecklingsmiljöer. Förutom för att ange unika värden för förhandsvisningsnivån bör du undvika att använda icke-hemliga miljöspecifika konfigurationer för Adobe Experience Manager as a Cloud Service Stage- eller Production-miljöer.

* Använd bara icke-hemliga miljöspecifika konfigurationer för konfigurationsvärden som skiljer sig mellan publicerings- och förhandsgranskningsskikt, eller för värden som skiljer sig åt mellan utvecklingsmiljöer, inklusive lokala utvecklingsinstanser.
* Förutom scenariot när förhandsvisningsnivån måste variera från publiceringsnivån, ska du använda standardvärdena för intern visning i OSGi-konfigurationerna för icke-hemliga värden för scenen och produktionen. I relation till detta rekommenderas inte att du använder miljöspecifika konfigurationer för att underlätta konfigurationsändringar under körning i scen- och produktionsmiljöer. Dessa ändringar bör införas via källkodshantering.

### När hemliga miljöspecifika konfigurationsvärden ska användas {#when-to-use-secret-environment-specific-configuration-values}

Adobe Experience Manager as a Cloud Service kräver användning av miljöspecifika konfigurationer (`$[secret:SECRET_VAR_NAME]`) för eventuella hemliga OSGi-konfigurationsvärden, som lösenord, privata API-nycklar eller andra värden som inte kan lagras i Git av säkerhetsskäl.

Använd hemliga miljöspecifika konfigurationer för att lagra värdet för hemligheter i alla Adobe Experience Manager as a Cloud Service-miljöer, inklusive Stage och Production.

## Skapa OSGi-konfigurationer {#creating-osgi-configurations}

Det finns två sätt att skapa OSGi-konfigurationer enligt beskrivningen nedan. Den tidigare metoden används vanligtvis för att konfigurera anpassade OSGi-komponenter som har välkända OSGi-egenskaper och -värden av utvecklaren, och den senare för AEM OSGi-komponenter.

### Skriver OSGi-konfigurationer {#writing-osgi-configurations}

JSON-formaterade OSGi-konfigurationsfiler kan skrivas för hand direkt i AEM. Detta är ofta det snabbaste sättet att skapa OSGi-konfigurationer för välkända OSGi-komponenter, och särskilt anpassade OSGi-komponenter som har utformats och utvecklats av samma utvecklare som definierar konfigurationerna. Den här metoden kan också användas för att kopiera/klistra in och uppdatera konfigurationer för samma OSGi-komponent i olika körningslägemappar.

1. Öppna `ui.apps` , leta upp eller skapa konfigurationsmappen (`/apps/.../config.<runmode>`) som är avsedd för de runmodes som den nya OSGi-konfigurationen måste ha
1. Skapa en `<PID>.cfg.json` -fil. PID är den beständiga identiteten för OSGi-komponenten. Det är vanligtvis det fullständiga klassnamnet för OSGi-komponentimplementeringen. Till exempel:
   `/apps/.../config/com.example.workflow.impl.ApprovalWorkflow.cfg.json`
I-konfigurationens fabriksfilnamn använder filnamnen `<factoryPID>-<name>.cfg.json` namnkonvention
1. Öppna den nya `.cfg.json` och definiera nyckel/värde-kombinationerna för OSGi-egenskapen och värdepar enligt följande [Konfigurationsformat för JSON OSGi](https://sling.apache.org/documentation/bundles/configuration-installer-factory.html#configuration-files-cfgjson-1).
1. Spara ändringarna i den nya `.cfg.json` fil
1. Lägg till och implementera din nya OSGi-konfigurationsfil i Git

### Generera OSGi-konfigurationer med AEM SDK QuickStart {#generating-osgi-configurations-using-the-aem-sdk-quickstart}

AEM SDK Quickstart Jars AEM Web Console kan användas för att konfigurera OSGi-komponenter och exportera OSGi-konfigurationer som JSON. Detta är användbart för att konfigurera AEM OSGi-komponenter vars OSGi-egenskaper och deras värdeformat kanske inte är väl förstådda av den utvecklare som definierar OSGi-konfigurationerna i AEM.

>[!NOTE]
>
>Konfigurationsgränssnittet för AEM-webbkonsolen skriver `.cfg.json` till databasen. Därför bör du vara medveten om det här arbetsflödet för att undvika oväntade beteenden under lokal utveckling när de AEM projektdefinierade OSGi-konfigurationerna kan skilja sig från de genererade konfigurationerna.

1. Logga in på AEM SDK Quickstart Jars AEM Web console på `https://<host>:<port>/system/console` som admin-användare
1. Navigera till **OSGi** > **Konfiguration**
1. Om du vill konfigurera letar du reda på OSGi-komponenten och väljer dess titel att redigera
   ![OSGi-konfiguration](./assets/configuring-osgi/configuration.png)
1. Redigera OSGi-konfigurationens egenskapsvärden via webbgränssnittet efter behov
1. Registrera beständig identitet (PID) på en säker plats. Detta används senare för att generera OSGi-konfigurationens JSON
1. Välj Spara
1. Navigera till OSGi > OSGi Installer Configuration Printer
1. Klistra in den PID som kopierats i steg 5, kontrollera att Serialization Format är inställt på OSGi Configurator JSON
1. Välj Skriv ut
1. OSGi-konfigurationen i JSON-format visas i avsnittet Serialiserade konfigurationsegenskaper
   ![OSGi Installer Configuration Printer](./assets/configuring-osgi/osgi-installer-configurator-printer.png)
1. Öppna `ui.apps` , leta upp eller skapa konfigurationsmappen (`/apps/.../config.<runmode>`) som är avsett för de runmodes som den nya OSGi-konfigurationen måste ha.
1. Skapa en `<PID>.cfg.json` -fil. PID är samma värde från steg 5.
1. Klistra in serialiserade konfigurationsegenskaper från steg 10 i dialogrutan `.cfg.json` -fil.
1. Spara ändringarna i den nya `.cfg.json` -fil.
1. Lägg till och implementera den nya OSGi-konfigurationsfilen i Git.


## Egenskapsformat för OSGi-konfiguration {#osgi-configuration-property-formats}

### Textbundna värden {#inline-values}

Textbundna värden formateras som namnvärdespar enligt JSON-standardsyntaxen. Till exempel:

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

Kunder bör endast använda den här tekniken för OSGi-konfigurationsegenskaper som är relaterade till deras anpassade kod. Den får inte användas för att åsidosätta Adobe-definierad OSGi-konfiguration.

>[!NOTE]
>
>Platshållare kan inte användas i [repoinit-programsatser](/help/implementing/deploying/overview.md#repoinit).

### Värden för hemlig konfiguration {#secret-configuration-values}

OSGi-konfigurationen ska tilldela en platshållare för hemligheten som ska definieras per miljö:

```
use $[secret:SECRET_VAR_NAME]
```

### Variabelnamn {#variable-naming}

Följande gäller för både miljöspecifika och hemliga konfigurationsvärden.

Variabelnamn måste följa följande regler:

* Minsta längd: 2
* Maximal längd: 100
* Måste matcha regex: `[a-zA-Z_][a-zA-Z_0-9]*`

Värdena för variablerna får inte överstiga 2 048 tecken.

>[!CAUTION]
>
>Det finns regler för användning av vissa prefix för variabelnamn:
>
>1. Variabelnamn med prefix `INTERNAL_`, `ADOBE_`, eller `CONST_` är reserverade för Adobe. Alla kundinställda variabler som börjar med dessa prefix ignoreras.
>
>1. Kunderna får inte referera till variabler som är prefix med `INTERNAL_` eller `ADOBE_` antingen.
>
>1. Miljövariabler med prefix `AEM_` definieras av produkten som publikt API som ska användas och anges av kunderna.
>   När kunderna kan använda och ange miljövariabler som börjar med prefixet `AEM_` de ska inte definiera sina egna variabler med detta prefix.

### Standardvärden {#default-values}

Följande gäller för både miljöspecifika och hemliga konfigurationsvärden.

Om inget värde har angetts per miljö ersätts inte platshållaren vid körning och den lämnas kvar på plats eftersom ingen interpolering har gjorts. Du kan undvika detta genom att ange ett standardvärde som en del av platshållaren med följande syntax:

```
$[env:ENV_VAR_NAME;default=<value>]
```

När ett standardvärde anges ersätts platshållaren antingen med det angivna värdet per-environment eller med det angivna standardvärdet.

### Lokal utveckling {#local-development}

Följande gäller för både miljöspecifika och hemliga konfigurationsvärden.

Variabler kan definieras i den lokala miljön så att de hämtas av den lokala AEM vid körning. I Linux®:

```bash
export ENV_VAR_NAME=my_value
```

Vi rekommenderar att du skriver ett enkelt basskript som anger de systemvariabler som används i konfigurationerna och kör det innan du startar AEM. verktyg som [https://direnv.net/](https://direnv.net/) hjälper till med att förenkla det här tillvägagångssättet. Beroende på vilken typ av värden det är kan de checkas in i källkodshanteringen om de kan delas mellan alla.

Värdena för hemligheter läses från filer. Därför måste en textfil med det hemliga värdet skapas för varje platshållare som använder en hemlighet.

Om `$[secret:server_password]` används, en textfil med namnet **server_password** måste skapas. Alla dessa hemliga filer måste lagras i samma katalog och ramverksegenskapen `org.apache.felix.configadmin.plugin.interpolation.secretsdir` måste konfigureras med den lokala katalogen.

>[!CAUTION]
>
>Filtillägg tillåts inte för textfilen.
>
>Därför måste textfilen namnges i ovanstående exempel **server_password** - utan filtillägg.

The `org.apache.felix.configadmin.plugin.interpolation.secretsdir` är en Sling framework-egenskap. Den här egenskapen ställs inte in i felix-konsolen (/system/console), men ställs in i den sling.properties-fil som används när systemet startas. Den här filen finns i /conf-undermappen i den extraherade JAR/install-mappen (crx-quickstart/conf).

exempel: lägg till den här raden i slutet av crx-quickstart/conf/sling.properties-filen för att konfigurera crx-quickstart/secretsdir som en hemlig mapp:

```
org.apache.felix.configadmin.plugin.interpolation.secretsdir=${sling.home}/secretsdir
```

### Författare jämfört med Publiceringskonfiguration {#author-vs-publish-configuration}

Om en OSGi-egenskap kräver olika värden för författare jämfört med publicering:

* Separat `config.author` och `config.publish` OSGi-mappar måste användas enligt beskrivningen i [Avsnittet Upplösning i körläge](#runmode-resolution).
* Det finns två alternativ för att skapa de oberoende variabelnamnen som ska användas:
   * det första alternativet som rekommenderas: i alla OSGi-mappar (som `config.author` och `config.publish`) som deklarerats för att definiera olika värden, använd samma variabelnamn. Till exempel
     `$[env:ENV_VAR_NAME;default=<value>]`, där standardvärdet motsvarar standardvärdet för den nivån (författare eller publicering). När miljövariabeln ställs in via [API för Cloud Manager](#cloud-manager-api-format-for-setting-properties) eller via en klient, differentiera mellan nivåerna med hjälp av parametern &quot;service&quot; som beskrivs i detta [API-referensdokumentation](https://developer.adobe.com/experience-cloud/cloud-manager/api-reference/). Parametern service binder variabelns värde till rätt OSGi-nivå. Det kan vara&quot;författare&quot;,&quot;publicera&quot; eller&quot;förhandsgranska&quot;.
   * det andra alternativet, som är att deklarera distinkta variabler med ett prefix som `author_<samevariablename>` och `publish_<samevariablename>`

### Konfigurationsexempel {#configuration-examples}

I exemplen nedan antar vi att det finns tre utvecklingsmiljöer förutom scen- och prodmiljöer.

**Exempel 1**

Avsikten är värdet på OSGi-egenskapen `my_var1` vara densamma för scenen och produkten, men skiljer sig åt för var och en av de tre utvecklingsmiljöerna.

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
{ "my_var1": "val", "my_var2": "abc", "my_var3": 500 }
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1" : "$[env:my_var1]" "my_var2": "abc", "my_var3": 500 }
</pre>
</td>
</tr>
</table>

**Exempel 2**

Avsikten är värdet på OSGi-egenskapen `my_var1` skiljer sig åt för scenen, produkten och för var och en av de tre utvecklingsmiljöerna. Därför måste Cloud Manager API anropas för att ange värdet för `my_var1` for each dev env.

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
{ "my_var1": "val1", "my_var2": "abc", "my_var3": 500 }
</pre>
</td>
</tr>
<tr>
<td>
config.prod
</td>
<td>
<pre>
{ "my_var1": "val2", "my_var2": "abc", "my_var3": 500 }
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1" : "$[env:my_var1]" "my_var2": "abc", "my_var3": 500 }
</pre>
</td>
</tr>
</table>

**Exempel 3**

Avsikten är värdet på OSGi-egenskapen `my_var1` vara densamma för scenen, produktionen och bara en av utvecklingsmiljöerna, men för att det ska skilja sig åt för de två andra utvecklingsmiljöerna. I det här fallet måste Cloud Manager API anropas för att ange värdet för `my_var1` för var och en av utvecklingsmiljöerna, även för utvecklingsmiljön, som bör ha samma värde som stadium och produktion. Det ärver inte det värde som angetts i mappen **config**.

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
{ "my_var1": "val1", "my_var2": "abc", "my_var3": 500 }
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1" : "$[env:my_var1]" "my_var2": "abc", "my_var3": 500 }
</pre>
</td>
</tr>
</table>

Ett annat sätt att uppnå detta är att ange ett standardvärde för ersättningstoken i mappen config.dev så att det är samma värde som i **config** mapp.

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
{ "my_var1": "val1", "my_var2": "abc", "my_var3": 500 }
</pre>
</td>
</tr>
<tr>
<td>
config.dev
</td>
<td>
<pre>
{ "my_var1": "$[env:my_var1;default=val1]" "my_var2": "abc", "my_var3": 500 }
</pre>
</td>
</tr>
</table>

## API-format för Cloud Manager för att ange egenskaper {#cloud-manager-api-format-for-setting-properties}

Se [den här sidan](https://developer.adobe.com/experience-cloud/cloud-manager/docs/) om hur API måste konfigureras.
>[!NOTE]
>
>Kontrollera att det använda Cloud Manager-API:t har tilldelats rollen &quot;Deployment Manager - Cloud Service&quot;. Andra roller kan inte köra alla kommandon nedan.

>[!TIP]
>
>Du kan också använda Cloud Manager för att konfigurera miljövariabler. Mer information finns i dokumentationen [här.](/help/implementing/cloud-manager/environment-variables.md)

### Ange värden via API {#setting-values-via-api}

Anrop av API:t distribuerar de nya variablerna och värdena till en molnmiljö, ungefär som en vanlig pipeline för kundkoddistribution. Tjänsterna för författare och publicering startas om och de nya värdena anges, vilket normalt tar några minuter.

```
PATCH /program/{programId}/environment/{environmentId}/variables
```

```json
[
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

>[!NOTE]
>Standardvariabler anges inte via API, utan i själva OSGi-egenskapen.
>
>Se [den här sidan](https://developer.adobe.com/experience-cloud/cloud-manager/api-reference/) för mer information.

### Hämta värden via API {#getting-values-via-api}

```
GET /program/{programId}/environment/{environmentId}/variables
```

Se [den här sidan](https://developer.adobe.com/experience-cloud/cloud-manager/api-reference/) för mer information.

### Ta bort värden via API {#deleting-values-via-api}

```
PATCH /program/{programId}/environment/{environmentId}/variables
```

Om du vill ta bort en variabel inkluderar du den med ett tomt värde.

Se [den här sidan](https://developer.adobe.com/experience-cloud/cloud-manager/api-reference/) för mer information.

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

>[!NOTE]
>
>Se [den här sidan](https://github.com/adobe/aio-cli-plugin-cloudmanager#aio-cloudmanagerset-environment-variables-environmentid) om du vill ha mer information om hur du konfigurerar värden med plugin-programmet Cloud Manager för Adobe I/O CLI.

### Antal variabler {#number-of-variables}

Upp till 200 variabler per miljö kan deklareras.

## Distributionsöverväganden för Hemliga och miljöspecifika konfigurationsvärden {#deployment-considerations-for-secret-and-environment-specific-configuration-values}

Eftersom de hemliga och miljöspecifika konfigurationsvärdena finns utanför Git, och därför inte ingår i de formella distributionsmekanismerna för Adobe Experience Manager as a Cloud Service, bör kunden hantera, styra och integrera dem i Adobe Experience Manager as a Cloud Service distributionsprocess.

Som nämnts ovan distribueras de nya variablerna och värdena till Cloud-miljöer när API anropas, på samma sätt som en vanlig pipeline för kundkoddistribution. Tjänsterna för författare och publicering startas om och de nya värdena anges, vilket normalt tar några minuter. Kvalitetsgates och tester som körs av Cloud Manager under en vanlig koddistribution utförs inte under den här processen.

Normalt anropar kunderna API för att ange miljövariabler innan de distribuerar kod som är beroende av dem i Cloud Manager. I vissa fall kanske du vill ändra en befintlig variabel efter att koden redan har distribuerats.

>[!NOTE]
>
>API:t kanske inte fungerar när en pipeline används, antingen en AEM eller en kunddistribution, beroende på vilken del av slutpipeline som körs vid den tidpunkten. Felsvaret kommer att ange att begäran inte lyckades, men det kommer inte att ange den specifika orsaken.

Det kan finnas scenarier där en schemalagd kundkoddistribution förlitar sig på befintliga variabler för att ha nya värden, vilket inte är lämpligt med den aktuella koden. Om detta är ett problem bör variabla ändringar göras på ett additivt sätt. Det gör du genom att skapa nya variabelnamn i stället för att bara ändra värdet för gamla variabler så att gammal kod aldrig refererar till det nya värdet. När den nya kundreleasen ser stabil ut kan man välja att ta bort de äldre värdena.

Eftersom variabelns värden inte är versionshanterade kan en återställning av koden få den att referera till nyare värden som orsakar problem. Här skulle även den tidigare nämnda additiva variabelstrategin vara till hjälp.

Den här additiva variabelstrategin är också användbar för scenarier där, om kod från flera dagar tidigare behövde omdistribueras, variabelnamnen och värdena som den refererar till fortfarande är intakta. Detta bygger på en strategi där kunden väntar några dagar innan de tar bort de äldre variablerna, annars har den äldre koden inte rätt variabler att referera till.
