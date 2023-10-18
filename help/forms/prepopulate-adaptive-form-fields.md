---
title: Hur förifyller man adaptiva formulärfält?
description: Använda befintliga data för att förifylla fält i ett adaptivt formulär kan användarna förifylla grundläggande information i ett formulär genom att logga in med sina sociala profiler.
topic-tags: develop
exl-id: e2a87233-a0d5-48f0-b883-915fe56f105f
source-git-commit: ebb77adfc97c805383de660d238e04a2173122b7
workflow-type: tm+mt
source-wordcount: '2041'
ht-degree: 0%

---

# Förifyll adaptiva formulärfält{#prefill-adaptive-form-fields}

<span class="preview"> Adobe rekommenderar att man använder modern och utbyggbar datainhämtning [Kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) for [skapa ny Adaptive Forms](/help/forms/creating-adaptive-form-core-components.md) eller [lägga till adaptiv Forms på AEM Sites-sidor](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). De här komponenterna utgör ett betydande framsteg när det gäller att skapa adaptiva Forms-filer, vilket ger imponerande användarupplevelser. I den här artikeln beskrivs det äldre sättet att skapa Adaptiv Forms med baskomponenter. </span>

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/prepopulate-adaptive-form-fields.html) |
| AEM as a Cloud Service | Den här artikeln |

## Introduktion {#introduction}

Du kan förifylla fälten i ett adaptivt formulär med befintliga data. När en användare öppnar ett formulär är värdena för dessa fält förifyllda. Om du vill förifylla data i ett adaptivt formulär gör du användardata tillgängliga som förifylld XML/JSON i det format som följer datastrukturen för förifyllnad i Adaptive Forms.

## Struktur för förifyllda data {#the-prefill-structure}

Ett adaptivt formulär kan innehålla en blandning av bundna och obundna fält. Bundna fält är fält som dras från fliken Innehållssökare och som inte är tomma `bindRef` egenskapsvärde i dialogrutan för fältredigering. Obundna fält dras direkt från komponentwebbläsaren i Sidekick och har ett tomt värde `bindRef` värde.

Du kan förifylla både bundna och obundna fält i ett adaptivt formulär. Prefill-data innehåller avsnitten afBoundData och afUnBoundData för att förifylla både bundna och obundna fält i ett adaptivt formulär. The `afBoundData` -avsnittet innehåller förifyllda data för bundna fält och paneler. Dessa data måste vara kompatibla med det associerade formulärmodellschemat:

- För Adaptiv Forms med [XFA-formulärmall](#xfa-based-af)använder du den förifyllda XML-filen som är kompatibel med XFA-mallens dataschema.
- För adaptiv Forms med [XML-schema](#xml-schema-af)använder du den förifyllda XML-filen som är kompatibel med XML-schemastrukturen.
- För adaptiv Forms med [JSON-schema](#json-schema-based-adaptive-forms)använder du JSON-prefyllnad som är kompatibel med JSON-schemat.
- För adaptiva Forms som använder FDM-schema använder du JSON-prefyllning som är kompatibel med FDM-schemat.
- För adaptiv Forms med [ingen formulärmodell](#adaptive-form-with-no-form-model), finns det inga bundna data. Varje fält är ett obundet fält och är förifyllt med den obundna XML-koden.

### Exempel på XML-struktur för förifyllning {#sample-prefill-xml-structure}

```xml
<?xml version="1.0" encoding="UTF-8"?>
<afData>
  <afBoundData>
     <employeeData>
        .
     </employeeData>
  </afBoundData>

  <afUnboundData>
    <data>
      <textbox>Hello World</textbox>
         .
         .
      <numericbox>12</numericbox>
         .
         .
    </data>
  </afUnboundData>
</afData>
```

### Exempel på JSON-struktur för förifyllning {#sample-prefill-json-structure}

```javascript
{
   "afBoundData": {
      "employeeData": { }
   },
   "afUnboundData": {
      "data": {
         "textbox": "Hello World",
         "numericbox": "12"
      }
   }
}
```

För bundna fält med samma bindref-fält eller obundna fält med samma namn fylls data som anges i XML-taggen eller JSON-objektet i alla fält. Två fält i ett formulär mappas till exempel till namnet `textbox` i förifyllda data. Om det första textrutefältet innehåller&quot;A&quot; fylls&quot;A&quot; automatiskt i den andra textrutan under körningen. Denna länkning kallas live-länkning av fält i adaptiva formulär.

### Adaptivt formulär med XFA-formulärmall {#xfa-based-af}

Strukturen för förifylld XML och inskickad XML för XFA-baserad Adaptive Forms är följande:

- **XML-struktur för förifyllning**: XML-förifyllnad för XFA-baserad adaptiv form måste vara kompatibel med XFA-formulärmallens dataschema. Om du vill förifylla obundna fält omsluter du XML-strukturen för förifyllning i `/afData/afBoundData` -tagg.

- **Skickad XML-struktur**: När ingen förifylld XML används innehåller den skickade XML-filen data för både bundna och obundna fält i `afData` wrapper-tagg. Om du använder en XML-förifyllning har den skickade XML-filen samma struktur som XML-förifyllningen. Om XML-förifyllningen börjar med `afData` -taggen har XML-utdata också samma format. Om förifyllnings-XML inte har `afData/afBoundData`wrapper och i stället startar direkt från schemats rottagg som `employeeData`börjar den inskickade XML-filen också med `employeeData` -tagg.

Prefill-Submit-Data-ContentPackage.zip

[Hämta fil](assets/prefill-submit-data-contentpackage.zip)
Exempel som innehåller förifyllda data och inlämnade data

### XML-schemabaserad Adaptiv Forms  {#xml-schema-af}

Strukturen för förifylld XML och inskickad XML för Adaptive Forms baserat på XML-schema är följande:

- **XML-struktur för förifyllning**: XML-förifyllningen måste vara kompatibel med tillhörande XML-schema. Om du vill förifylla obundna fält omsluter du XML-strukturen för förifyllning i taggen /afData/afBoundData.
- **Skickad XML-struktur**: om ingen förifylld XML används innehåller den skickade XML-filen data för både bundna och obundna fält i `afData` wrapper-tagg. Om XML-förifyllning används har den skickade XML-filen samma struktur som XML-förifyllningen. Om XML-förifyllningen börjar med `afData` -taggen har XML-utdata samma format. Om förifyllnings-XML inte har `afData/afBoundData` wrapper och i stället börja direkt från schemats rottagg som `employeeData`börjar den inskickade XML-filen också med `employeeData` -tagg.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<xs:schema targetNamespace="https://adobe.com/sample.xsd"
            xmlns="https://adobe.com/sample.xsd"
            xmlns:xs="https://www.w3.org/2001/XMLSchema">

    <xs:element name="sample" type="SampleType"/>

    <xs:complexType name="SampleType">
        <xs:sequence>
            <xs:element name="noOfProjectsAssigned" type="xs:string"/>
        </xs:sequence>
    </xs:complexType>
</xs:schema>
```

För fält vars modell är XML-schema är data förifyllda i `afBoundData` -taggen som i XML-exemplet nedan. Den kan användas för att förifylla ett adaptivt formulär med ett eller flera obundna textfält.

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
      <textbox>Ignorance is bliss :) </textbox>
    </data>
  </afUnboundData>
  <afBoundData>
    <data>
      <noOfProjectsAssigned>twelve</noOfProjectsAssigned>
    </data>
  </afBoundData>
</afData>
```

>[!NOTE]
>
>Du bör inte använda obundna fält i bundna paneler (paneler med icke-tomma paneler) `bindRef` som har skapats genom att dra komponenter från Sidekick eller fliken Datakällor). Det kan orsaka dataförlust för dessa obundna fält. Vi rekommenderar dessutom att fältnamnen är unika i hela formuläret, särskilt för obundna fält.

#### Ett exempel utan afData och afBoundData-wrapper {#an-example-without-afdata-and-afbounddata-wrapper}

```xml
<?xml version="1.0" encoding="UTF-8"?><config>
 <assignmentDetails descriptionOfAssignment="Some Science Project" durationOfAssignment="34" financeRelatedProject="1" name="Lisa" numberOfMentees="1"/>
 <assignmentDetails descriptionOfAssignment="Kidding, right?" durationOfAssignment="4" financeRelatedProject="1" name="House" numberOfMentees="3"/>
</config>
```

### JSON schemabaserad Adaptiv Forms {#json-schema-based-adaptive-forms}

För Adaptiv Forms baserat på JSON-schema beskrivs strukturen för förifyll JSON och skickad JSON nedan. Mer information finns i [Skapa adaptiv Forms med JSON-schema](adaptive-form-json-schema-form-model.md).

- **JSON-struktur för förifyllning**: JSON för förifyllning måste vara kompatibel med det associerade JSON-schemat. Alternativt kan den kapslas in i /afData/afBoundData-objektet om du även vill förifylla obundna fält.
- **Skickad JSON-struktur**: Om ingen JSON för förifyllnad används, innehåller den skickade JSON data för både bundna och obundna fält i afData-wrapper-taggen. Om JSON för förifyllning används har den inskickade JSON samma struktur som JSON för förifyllnad. Om JSON för förifyllning börjar med afData-rotobjektet har utdata-JSON samma format. Om JSON-funktionen för förifyllning inte har wrapper afData/afBoundData och i stället startar direkt från schemarotobjektet, till exempel användaren, börjar den skickade JSON-filen också med användarobjektet.

```json
{
  "id": "https://some.site.somewhere/entry-schema#",
  "$schema": "https://json-schema.org/draft-04/schema#",
  "type": "object",
  "properties": {
    "address": {
      "type": "object",
      "properties": {
        "name": {
          "type": "string"
        },
        "age": {
          "type": "integer"
        }
      }
    }
  }
}
```

För fält som använder JSON-schemamodell är data förifyllda i afBoundData-objektet, vilket visas i exemplet på JSON nedan. Den kan användas för att förifylla ett adaptivt formulär med ett eller flera obundna textfält. Nedan visas ett exempel på data med `afData/afBoundData` wrapper:

```json
{
  "afData": {
    "afUnboundData": {
      "data": { "textbox": "Ignorance is bliss :) " }
    },
    "afBoundData": {
      "data": { {
   "user": {
    "address": {
     "city": "Noida",
     "country": "India"
}}}}}}}
```

Nedan visas ett exempel utan `afData/afBoundData` wrapper:

```json
{
  "user": {
    "address": {
      "city": "Noida",
      "country": "India"
    }
  }
}
```

>[!NOTE]
>
> Använda obundna fält i bundna paneler (paneler med icke-tomma bindRef som har skapats genom att dra komponenter från Sidekick eller fliken Datakällor) **not** rekommenderas eftersom det kan orsaka dataförlust i obundna fält. Du bör ha unika fältnamn i hela formuläret, särskilt för obundna fält.
>

### Adaptiv form utan formulärmodell {#adaptive-form-with-no-form-model}

För Adaptive Forms utan någon formulärmodell finns data för alla fält under `<data>` tagg för `<afUnboundData> tag`.

Observera även följande:

XML-taggarna för användardata som skickas för olika fält genereras med fältnamnet. Därför måste fältnamnen vara unika.

```xml
<?xml version="1.0" encoding="UTF-8"?><afData>
  <afUnboundData>
    <data>
      <radiobutton>2</radiobutton>
      <repeatable_panel_no_form_model>
        <numericbox>12</numericbox>
      </repeatable_panel_no_form_model>
      <repeatable_panel_no_form_model>
        <numericbox>21</numericbox>
      </repeatable_panel_no_form_model>
      <checkbox>2</checkbox>
      <textbox>Nopes</textbox>
    </data>
  </afUnboundData>
  <afBoundData/>
</afData>
```

## Konfigurerar förifyllningstjänst {#configuring-prefill-service-using-configuration-manager}

Använd `alloweddataFileLocations` egenskapen för **Standardkonfiguration för förifyllningstjänst** för att ange platsen för datafilerna eller en region (reguljärt uttryck) för datafilernas platser.

I följande JSON-fil visas ett exempel:

```JSON
  {
  "alloweddataFileLocations": "`file:///C:/Users/public/Document/Prefill/.*`"
  }
```

Så här anger du värden för en konfiguration: [Generera OSGi-konfigurationer med AEM SDK](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart) och [distribuera konfigurationen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) till din Cloud Service.

>[!NOTE]
>
> - Som standard är förifyllning tillåtet via crx-filer för alla typer av adaptiva Forms (XSD, XDP, JSON, FDM och utan formulärmodellbaserad). Förifyll tillåts bara med JSON- och XML-filer.
> - CRX-protokollet hanterar förfylld datasäkerhet och är därför tillåtet som standard. Förifyllnad via andra protokoll med generisk regex kan orsaka sårbarhet. I konfigurationen anger du en säker URL-konfiguration för att skydda dina data.

## Det nyfikna fallet med repeterbara paneler {#the-curious-case-of-repeatable-panels}

Vanligtvis skapas bundna (formulärschema) och obundna fält i samma adaptiva form, men följande undantag görs om bindningen är repeterbar:

- Obundna upprepningsbara paneler stöds inte för Adaptive Forms med XFA-formulärmallen, XSD-, JSON-schemat eller FDM-schemat.
- Använd inte obundna fält i bundna repeterbara paneler.

>[!NOTE]
>
> Som tumregel ska du inte blanda bundna och obundna fält om de korsas i data som fylls i av slutanvändaren i obundna fält. Om det är möjligt bör du ändra schemat eller XFA-formulärmallen och lägga till en post för obundna fält, så att den också blir bunden och dess data är tillgängliga som andra fält i skickade data.

## Protokoll som stöds för förifyllning av användardata {#supported-protocols-for-prefilling-user-data}

Adaptiv Forms kan förifyllas med användardata i förifyllda dataformat via följande protokoll när den konfigureras med giltig regex:

### crx:// {#the-crx-protocol}

```javascript
http
https://`servername`/content/forms/af/xml.html?wcmmode=disabled&dataRef=crx:///tmp/fd/af/myassets/sample.xml
```

Den angivna noden måste ha en egenskap som kallas `jcr:data` och lagra data.

### file://  {#the-file-protocol-nbsp}

```javascript
https://`servername`/content/forms/af/someAF.html?wcmmode=disabled&dataRef=file:///C:/Users/form-user/Downloads/somesamplexml.xml
```

Den refererade filen måste finnas på samma server.

### https:// {#the-http-protocol}

```javascript
https://`servername`/content/forms/af/xml.html?wcmmode=disabled&dataRef=https://servername/somesamplexmlfile.xml
```

### service:// {#the-service-protocol}

```javascript
https://`servername`/content/forms/af/abc.html?wcmmode=disabled&dataRef=service://[SERVICE_NAME]/[IDENTIFIER]
```

- SERVICE_NAME refererar till namnet på OSGI-förifyllningstjänsten. Se [Skapa och köra en förifyllningstjänst](prepopulate-adaptive-form-fields.md#create-and-run-a-prefill-service).
- IDENTIFIER avser alla metadata som krävs av OSGI-förifyllningstjänsten för att hämta förifyllda data. En identifierare för den inloggade användaren är ett exempel på metadata som kan användas.

>[!NOTE]
>
> Det går inte att skicka autentiseringsparametrar.

### Ställer in dataattribut i slingRequest {#setting-data-attribute-in-slingrequest}

Du kan också ange `data` attribute in `slingRequest`, där `data` -attribut är en sträng som innehåller XML eller JSON, vilket visas i exempelkoden nedan (Exempel är för XML):

```javascript
<%
           String dataXML="<afData>" +
                            "<afUnboundData>" +
                                "<data>" +
                                    "<first_name>"+ "Tyler" + "</first_name>" +
                                    "<last_name>"+ "Durden " + "</last_name>" +
                                    "<gender>"+ "Male" + "</gender>" +
                                    "<location>"+ "Texas" + "</location>" +
                                    "</data>" +
                            "</afUnboundData>" +
                        "</afData>";
        slingRequest.setAttribute("data", dataXML);
%>
```

Du kan skriva en enkel XML- eller JSON-sträng som innehåller alla data och ange den i slingRequest. Detta kan enkelt göras i JSP-återgivningsfilen för alla komponenter som du vill inkludera på sidan där du kan ange dataattributet slingRequest.

Om du till exempel vill ha en särskild design för sidan med en viss typ av sidhuvud. För att uppnå detta kan du skriva en egen `header.jsp`som du kan ta med i sidkomponenten och ange `data` -attribut.

Ett annat bra exempel är ett användningsexempel där du vill fylla i data i förväg via sociala konton som Facebook, Twitter eller LinkedIn. I det här fallet kan du inkludera en enkel JSP i `header.jsp`, som hämtar data från användarkontot och ställer in data-parametern.

prefill-page component.zip

[Hämta fil](assets/prefill-page-component.zip)
Exempel på prefill.jsp i sidkomponent

## [!DNL AEM Forms] anpassad förifyllningstjänst {#aem-forms-custom-prefill-service}

Du kan använda en anpassad förifyllningstjänst för scenarierna, där du hela tiden läser data från en fördefinierad källa. Förifyllningstjänsten läser data från definierade datakällor och fyller i fälten i det adaptiva formuläret i förväg med innehållet i datafilen för förifyllnad. Det hjälper dig även att permanent koppla förfyllda data till ett adaptivt formulär.

### Skapa och köra en förifyllningstjänst {#create-and-run-a-prefill-service}

Förifyllningstjänsten är en OSGi-tjänst och paketeras via OSGi-paketet. Du skapar OSGi-paketet, överför det och installerar det i [!DNL AEM Forms] paket. Innan du börjar skapa paketet:

- [Ladda ned [!DNL AEM Forms] Klient-SDK](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)
- Hämta mallpaketet

- Placera datafilen (förifyllda data) i crx-databasen. Du kan placera filen på valfri plats i mappen \contents i crx-database.

[Hämta fil](assets/prefill-sumbit-xmlsandcontentpackage.zip)

#### Skapa en förifyllningstjänst {#create-a-prefill-service}

Mallpaketet (exempelpaketet för förifyllningstjänsten) innehåller exempel på implementering av [!DNL AEM Forms] förifyllningstjänst. Öppna mallpaketet i en kodredigerare. Öppna till exempel mallprojektet i Eclipse för redigering. När du har öppnat mallpaketet i en kodredigerare gör du följande för att skapa tjänsten.

1. Öppna src\main\java\com\adobe\test\Prefill.java för redigering.
1. I koden anger du värdet:

   - `nodePath:` Nodsökvägsvariabeln som pekar på platsen för crx-databasen innehåller sökvägen till datafilen (prefill). Till exempel /content/prefilldata.xml
   - `label:` Etikettparametern anger tjänstens visningsnamn. Exempel: Standardtjänst för förifyllnad

1. Spara och stäng `Prefill.java` -fil.
1. Lägg till `AEM Forms Client SDK` till byggsökvägen för standardprojektet.
1. Kompilera projektet och skapa .jar-filen för paketet.

#### Starta och använda förifyllningstjänsten {#start-and-use-the-prefill-service}

Om du vill starta förifyllningstjänsten överför du JAR-filen till [!DNL AEM Forms] Webbkonsol och aktivera tjänsten. Nu börjar tjänsten visas i Adaptive Forms Editor. Så här associerar du en förifyllningstjänst till ett adaptivt formulär:

1. Öppna det adaptiva formuläret i Forms Editor och öppna egenskapspanelen för formulärbehållaren.
1. Gå till egenskapskonsolen [!DNL AEM Forms] container > Basic > Prefill Service.
1. Välj standardtjänsten för förifyllnad och klicka på **[!UICONTROL Save]**. Tjänsten är kopplad till formuläret.

<!-- ## Prepopulate data at client {#prefill-at-client}

When you prefill an Adaptive Form, the [!DNL AEM Forms] server merges data with an Adaptive Form and delivers the filled form to you. By default, the data merge action takes place at the server.

You can configure the [!DNL AEM Forms] server to perform the data merge action at the client instead of the server. It significantly reduces the time required to prefill and render Adaptive Forms. By default, the feature is disabled. You can enable it from the Configuration Manager or command line.

* To enable or disable from configuration manager:
  1. Open AEM Configuration Manager.
  1. Locate and open the Adaptive Form and Interactive Communication Web Channel Configuration
  1. Enable the Configuration.af.clientside.datamerge.enabled.name option
* To enable or disable from the command line:
  * To enable, run the following cURL command:
    `curl -u admin:admin -X POST -d apply=true \ -d propertylist=af.clientside.datamerge.enabled \ -d af.clientside.datamerge.enabled=true \ http://${crx.host}:${crx.port}/system/console/configMgr/Adaptive%20Form%20and%20Interactive%20Communication%20Web%20Channel%20Configuration`

  * To disable, run the following cURL command:
    `curl -u admin:admin -X POST -d apply=true \ -d propertylist=af.clientside.datamerge.enabled \ -d af.clientside.datamerge.enabled=false \ http://${crx.host}:${crx.port}/system/console/configMgr/Adaptive%20Form%20and%20Interactive%20Communication%20Web%20Channel%20Configuration`

   To take full advantage of the prepopulate data at client option, update your prefill service to return [FileAttachmentMap](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/forms/common/service/PrefillData.html) and [CustomContext](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/forms/common/service/PrefillData.html) -->