---
title: Utöka Multi Site Manager
description: Lär dig hur du utökar funktionerna i Multi Site Manager.
exl-id: 4b7a23c3-65d1-4784-9dea-32fcceca37d1
source-git-commit: 6bb7b2d056d501d83cf227adb239f7f40f87d0ce
workflow-type: tm+mt
source-wordcount: '2429'
ht-degree: 0%

---

# Utöka Multi Site Manager {#extending-the-multi-site-manager}

Det här dokumentet hjälper dig att förstå hur du kan utöka funktionaliteten för Multi Site Manager och omfattar följande ämnen.

* Läs mer om huvudmedlemmarna i MSM Java API
* Skapa en ny synkroniseringsåtgärd som kan användas i en utrullningskonfiguration
* Ändra standardspråk och landskoder

>[!TIP]
>
>Den här sidan är lättare att förstå i dokumentets sammanhang [Återanvända innehåll: Hanteraren för flera webbplatser.](/help/sites-cloud/administering/msm/overview.md)

>[!CAUTION]
>
>Multi Site Manager och dess API används vid utvecklingen av en webbplats och är därför endast avsedda att användas i en författarmiljö.

## Översikt över Java API {#overview-of-the-java-api}

Hantering av flera platser består av följande paket:

* [com.day.cq.wcm.msm.api](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/package-frame.html)
* [com.day.cq.wcm.msm.Commons](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/commons/package-frame.html)

De huvudsakliga MSM API-objekten interagerar på följande sätt (se även avsnittet [Använda termer](/help/sites-cloud/administering/msm/overview.md#terms-used)):

![Huvudobjekt för MSM API](assets/msm-api-interaction.png)

* **`Blueprint`** - A `Blueprint` (som i [konfiguration av utkast](/help/sites-cloud/administering/msm/overview.md#source-blueprints-and-blueprint-configurations)) anger de sidor från vilka en live-kopia kan ärva innehåll.

  ![Blueprint](assets/msm-blueprint-interaction.png)

   * Användning av en ritningskonfiguration ( `Blueprint`) är valfritt, men:

      * Det gör att författaren kan använda **Utrullning** på källan för att uttryckligen skicka ändringar till live-kopior som ärver från den här källan.
      * Det gör att författaren kan använda **Skapa webbplats**, vilket gör det enkelt för användaren att välja språk och konfigurera strukturen för live-kopian.
      * Den definierar standardkonfigurationen för utrullning för alla resulterande live-kopior.

* **`LiveRelationship`** - `LiveRelationship` Anger anslutningen (relationen) mellan en resurs i livekopiegrenen och dess ekvivalenta käll-/planresurs.

   * Relationerna används vid arv och utrullning.
   * `LiveRelationship` objekt ger åtkomst (referenser) till utrullningskonfigurationer ( `RolloutConfig`), `LiveCopy`och `LiveStatus` objekt som är relaterade till relationen.

   * En live-kopia skapas till exempel i `/content/copy/us` från källan/ritningen på `/content/wknd/language-masters`. Resurserna `/content/wknd/language-masters/en/jcr:content` och `/content/copy/us/en/jcr:content` skapa en relation.

* **`LiveCopy`** - A `LiveCopy` innehåller konfigurationsinformation för relationerna (`LiveRelationship`) mellan de aktiva kopieringsresurserna och deras käll-/ritresurser.

   * Använd `LiveCopy` -klass för att komma åt sidans sökväg, sökvägen till käll-/ritningssidan, rollout-konfigurationerna och om underordnade sidor också inkluderas i `LiveCopy`.

   * A `LiveCopy` noden skapas varje gång **Skapa webbplats** eller **Skapa Live Copy** används.

* **`LiveStatus`** - `LiveStatus` objekt ger åtkomst till körningsstatus för en `LiveRelationship`. Används för att fråga synkroniseringsstatusen för en live-kopia.

* **`LiveAction`** - A `LiveAction` är en åtgärd som utförs på varje resurs som ingår i utrullningen.

   * `LiveAction`s genereras endast av `RolloutConfig`s.

* **`LiveActionFactory`** - A `LiveActionFactory` skapar `LiveAction` objekt som har `LiveAction` konfiguration. Konfigurationer lagras som resurser i databasen.

* **`RolloutConfig`** - `RolloutConfig` innehåller en lista med `LiveActions`, som ska användas när den aktiveras. The `LiveCopy` ärver `RolloutConfig` och resultatet finns i `LiveRelationship`.

   * När du konfigurerar en live-kopia för första gången används även en `RolloutConfig` (som utlöser `LiveAction`s).

## Skapa en ny synkroniseringsåtgärd {#creating-a-new-synchronization-action}

Du kan skapa anpassade synkroniseringsåtgärder som du kan använda med dina utrullningskonfigurationer. Detta kan vara användbart när [installerade åtgärder](/help/sites-cloud/administering/msm/live-copy-sync-config.md#installed-synchronization-actions) uppfyller inte dina specifika programkrav.

Skapa då två klasser:

* Ett genomförande av [`com.day.cq.wcm.msm.api.LiveAction`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/LiveAction.html) gränssnitt som utför åtgärden.
* En OSGi-komponent som implementerar [`com.day.cq.wcm.msm.api.LiveActionFactory`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html) -gränssnittet och skapar instanser av `LiveAction` class

The `LiveActionFactory` skapar instanser av `LiveAction` klass för en viss konfiguration:

* `LiveAction` -klasser innehåller följande metoder:

   * `getName` - Returnerar åtgärdens namn

      * Namnet används för att referera till åtgärden, till exempel i utrullningskonfigurationer.

   * `execute` - Utför åtgärderna

* `LiveActionFactory` -klasserna innehåller följande medlemmar:

   * `LIVE_ACTION_NAME` - Ett fält som innehåller namnet på det associerade `LiveAction`

      * Namnet måste sammanfalla med värdet som returneras av `getName` metod för `LiveAction` klassen.

   * `createAction` - Skapar en instans av `LiveAction`

      * Valfritt `Resource` -parametern kan användas för att tillhandahålla konfigurationsinformation.

   * `createsAction` - Returnerar namnet på det associerade `LiveAction`

### Åtkomst till konfigurationsnoden för LiveAction {#accessing-the-liveaction-configuration-node}

Använd `LiveAction` konfigurationsnoden i databasen för att lagra information som påverkar körningsbeteendet för `LiveAction` -instans. Den nod i databasen som lagrar `LiveAction` konfigurationen är tillgänglig för `LiveActionFactory` objekt vid körning. Därför kan du lägga till egenskaper i konfigurationsnoden och använda dem i `LiveActionFactory` vid behov.

Till exempel en `LiveAction` måste lagra namnet på den som skapat ritningen. En egenskap för konfigurationsnoden innehåller egenskapsnamnet för den planeringssida som lagrar informationen. Vid körning visas `LiveAction` hämtar egenskapsnamnet från konfigurationen och hämtar sedan egenskapsvärdet.

Parametern för [`LiveActionFactory.createAction`](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/msm/api/LiveActionFactory.html) metoden är en `Resource` -objekt. Detta `Resource` objektet representerar `cq:LiveSyncAction` nod för den här live-åtgärden i rollout-konfigurationen.

Se [Skapa en utrullningskonfiguration](/help/sites-cloud/administering/msm/live-copy-sync-config.md#creating-a-rollout-configuration) för mer information.

Som vanligt när du använder en konfigurationsnod bör du anpassa den till en `ValueMap` objekt:

```java
public LiveAction createAction(Resource resource) throws WCMException {
        ValueMap config;
        if (resource == null || resource.adaptTo(ValueMap.class) == null) {
            config = new ValueMapDecorator(Collections.<String, Object>emptyMap());
        } else {
            config = resource.adaptTo(ValueMap.class);
        }
        return new MyLiveAction(config, this);
}
```

### Åtkomst till målnoder, källnoder och LiveRelationship {#accessing-target-nodes-source-nodes-and-the-liverelationship}

Följande objekt anges som parametrar för `execute` metod för `LiveAction` objekt:

* A [`Resource`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/Resource.html) objekt som representerar källan till den aktiva kopian
* A `Resource` objekt som representerar målet för live-kopian.
* The [`LiveRelationship`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/wcm/msm/api/LiveRelationship.html) objekt för live-kopian
   * The `autoSave` värdet anger om `LiveAction` bör spara ändringar som görs i databasen
   * The `reset` värdet anger läget för återställning av utrullning.

Från dessa objekt kan du få information om `LiveCopy`. Du kan också använda `Resource` objekt att hämta `ResourceResolver`, `Session`och `Node` objekt. De här objekten är användbara för att hantera databasinnehåll:

I den första raden i följande kod är källan `Resource` källsidans objekt:

```java
ResourceResolver resolver = source.getResourceResolver();
Session session = resolver.adaptTo(javax.jcr.Session.class);
Node sourcenode = source.adaptTo(javax.jcr.Node.class);
```

>[!NOTE]
>
>The `Resource` argument kan `null` eller `Resources` objekt som inte anpassar sig till `Node` objekt, som [`NonExistingResource`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/org/apache/sling/api/resource/NonExistingResource.html) objekt.

## Skapa en ny utrullningskonfiguration {#creating-a-new-rollout-configuration}

Du kan skapa en utrullningskonfiguration om de installerade utrullningskonfigurationerna inte uppfyller dina programkrav i två steg:

* [Skapa utrullningskonfigurationen](#create-the-rollout-configuration)
* [Lägg till synkroniseringsåtgärder i utrullningskonfigurationen](#add-synchronization-actions-to-the-rollout-configuration)

Den nya utrullningskonfigurationen är sedan tillgänglig för dig när du ställer in utrullningskonfigurationer på en ritnings- eller Live copy-sida.

>[!TIP]
>
>Se även [de bästa sätten att anpassa utrullningar](/help/sites-cloud/administering/msm/best-practices.md#customizing-rollouts).

### Skapa utrullningskonfiguration {#create-the-rollout-configuration}

Så här skapar du en utrullningskonfiguration:

1. Öppna CRXDE Lite at `https://<host>:<port>/crx/de`.

1. Navigera till `/apps/msm/<your-project>/rolloutconfigs`, projektets anpassade version av `/libs/msm/wcm/rolloutconfigs`.

   * Om det här är din första konfiguration `/libs` gren måste användas som mall för att skapa den nya grenen under `/apps`.

1. Skapa en nod med följande egenskaper under den här platsen:

   * **Namn**: Nodnamnet för utrullningskonfigurationen, till exempel `contentCopy` eller `workflow`
   * **Typ**: `cq:RolloutConfig`

1. Lägg till följande egenskaper i den här noden:

   * **Namn**: `jcr:title`
     **Typ**: `String`
     **Värde**: En identifierande titel som visas i användargränssnittet

   * **Namn**: `jcr:description`
     **Typ**: `String`
     **Värde**: En valfri beskrivning.

   * **Namn**: `cq:trigger`
     **Typ**: `String`
     **Värde**: [Utlösare för utrullning](/help/sites-cloud/administering/msm/live-copy-sync-config.md#rollout-triggers) används
      * `rollout`
      * `modification`
      * `publish`
      * `deactivate`

1. Klicka **Spara alla**.

### Lägg till synkroniseringsåtgärder i utrullningskonfigurationen {#add-synchronization-actions-to-the-rollout-configuration}

Utrullningskonfigurationer lagras under [rollout configuration node](#create-the-rollout-configuration) som du har skapat under `/apps/msm/<your-project>/rolloutconfigs` nod.

Lägg till underordnade noder av typen `cq:LiveSyncAction` för att lägga till synkroniseringsåtgärder i utrullningskonfigurationen. Ordningen på synkroniseringsåtgärdsnoderna avgör i vilken ordning åtgärderna utförs.

1. I CRXDE Lite väljer du [Konfiguration av utrullning](#create-the-rollout-configuration) nod, till exempel `/apps/msm/myproject/rolloutconfigs/myrolloutconfig`.

1. Skapa en nod med följande nodegenskaper:

   * **Namn**: Synkroniseringsåtgärdens nodnamn
      * Namnet måste vara detsamma som **Åtgärdsnamn** i tabellen under [Synkroniseringsåtgärder](/help/sites-cloud/administering/msm/live-copy-sync-config.md#installed-synchronization-actions) som `contentCopy` eller `workflow`.
   * **Typ**: `cq:LiveSyncAction`

1. Lägg till och konfigurera så många noder för synkroniseringsåtgärder som du behöver.

1. Ordna om åtgärdsnoderna så att ordningen matchar den ordning i vilken du vill att de ska visas.
   * Den översta åtgärdsnoden inträffar först.

## Skapa och använda en enkel LiveActionFactory-klass {#creating-and-using-a-simple-liveactionfactory-class}

Följ anvisningarna i det här avsnittet för att utveckla en `LiveActionFactory` och använda den i en utrullningskonfiguration. Processerna använder Maven och Eclipse för att utveckla och driftsätta `LiveActionFactory`:

1. [Skapa maven-projektet](#create-the-maven-project) och importera den till Eclipse.
1. [Lägg till beroenden](#add-dependencies-to-the-pom-file) till POM-filen.
1. [Implementera `LiveActionFactory` gränssnitt](#implement-liveactionfactory) och driftsätta OSGi-paketet.
1. [Skapa utrullningskonfigurationen](#create-the-example-rollout-configuration).
1. [Skapa en live-kopia](#create-the-live-copy).

[Maven-projektet och Java-klassens källkod](https://github.com/Adobe-Marketing-Cloud/experiencemanager-java-msmrollout) är tillgängligt i den offentliga Git-databasen.

### Skapa projektet Maven {#create-the-maven-project}

Följande procedur kräver att du har lagt till `adobe-public` till din Maven-inställningsfil.

* Mer information om profilen adobe-public finns i [Hämta innehållspaketet Maven Plugin](/help/implementing/developing/tools/maven-plugin.md#obtaining-the-content-package-maven-plugin)
* Mer information om inställningarna för Maven finns i Maven [Inställningsreferens](https://maven.apache.org/settings.html).

1. Öppna en terminal- eller kommandoradssession och ändra katalogen så att den pekar på den plats där projektet ska skapas.
1. Ange följande kommando:

   ```text
   mvn archetype:generate -DarchetypeGroupId=com.day.jcr.vault -DarchetypeArtifactId=multimodule-content-package-archetype -DarchetypeVersion=1.0.0 -DarchetypeRepository=adobe-public-releases
   ```

1. Ange följande värden vid en interaktiv fråga:

   * **`groupId`**: `com.adobe.example.msm`
   * **`artifactId`**: `MyLiveActionFactory`
   * **`version`**: `1.0-SNAPSHOT`
   * **`package`**: `MyPackage`
   * **`appsFolderName`**: `myapp`
   * **`artifactName`**: `MyLiveActionFactory package`
   * **`packageGroup`**: `myPackages`

1. Starta Eclipse och [importera projektet Maven.](/help/implementing/developing/tools/eclipse.md#import-the-maven-project-into-eclipse)

### Lägg till beroenden till POM-filen {#add-dependencies-to-the-pom-file}

Lägg till beroenden så att Eclipse-kompilatorn kan referera till klasserna som används i `LiveActionFactory` kod.

1. Öppna filen i Eclipse Project Explorer `MyLiveActionFactory/pom.xml`.

1. Klicka på knappen `pom.xml` -fliken och leta upp `project/dependencyManagement/dependencies` -avsnitt.

1. Lägg till följande XML i `dependencyManagement` och spara sedan filen.

   ```xml
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-msm-api</artifactId>
     <version>5.6.2</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.api</artifactId>
     <version>2.4.3-R1488084</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-wcm-api</artifactId>
     <version>5.6.6</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.commons.json</artifactId>
     <version>2.0.6</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
     <version>5.6.4</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.jcr.jcr-wrapper</artifactId>
     <version>2.0.0</version>
     <scope>provided</scope>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
     <version>5.6.4</version>
     <scope>provided</scope>
    </dependency>
   ```

1. Öppna POM-filen för paketet från **Project Explorer** på `MyLiveActionFactory-bundle/pom.xml`.

1. Klicka på knappen `pom.xml` och leta upp avsnittet Projekt/beroenden. Lägg till följande XML i beroendeelementet och spara sedan filen:

   ```xml
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-msm-api</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.api</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq.wcm</groupId>
     <artifactId>cq-wcm-api</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.commons.json</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
    </dependency>
    <dependency>
     <groupId>org.apache.sling</groupId>
     <artifactId>org.apache.sling.jcr.jcr-wrapper</artifactId>
    </dependency>
    <dependency>
     <groupId>com.day.cq</groupId>
     <artifactId>cq-commons</artifactId>
    </dependency>
   ```

### Implementera LiveActionFactory {#implement-liveactionfactory}

Följande `LiveActionFactory` class implements a `LiveAction` som loggar meddelanden om käll- och målsidor och kopierar `cq:lastModifiedBy` från källnoden till målnoden. Den aktiva åtgärdens namn är `exampleLiveAction`.

1. I Eclipse Project Explorer högerklickar du på `MyLiveActionFactory-bundle/src/main/java/com.adobe.example.msm` paketera och klicka **Nytt** > **Klass**.

1. För **Namn**, ange `ExampleLiveActionFactory` och sedan klicka **Slutför**.

1. Öppna `ExampleLiveActionFactory.java` , ersätter innehållet med följande kod och sparar filen.

   ```java
   package com.adobe.example.msm;
   
   import java.util.Collections;
   
   import org.apache.felix.scr.annotations.Component;
   import org.apache.felix.scr.annotations.Property;
   import org.apache.felix.scr.annotations.Service;
   import org.apache.sling.api.resource.Resource;
   import org.apache.sling.api.resource.ResourceResolver;
   import org.apache.sling.api.resource.ValueMap;
   import org.apache.sling.api.wrappers.ValueMapDecorator;
   import org.apache.sling.commons.json.io.JSONWriter;
   import org.apache.sling.commons.json.JSONException;
   
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   
   import javax.jcr.Node;
   import javax.jcr.RepositoryException;
   import javax.jcr.Session;
   
   import com.day.cq.wcm.msm.api.ActionConfig;
   import com.day.cq.wcm.msm.api.LiveAction;
   import com.day.cq.wcm.msm.api.LiveActionFactory;
   import com.day.cq.wcm.msm.api.LiveRelationship;
   import com.day.cq.wcm.api.WCMException;
   
   @Component(metatype = false)
   @Service
   public class ExampleLiveActionFactory implements LiveActionFactory<LiveAction> {
    @Property(value="exampleLiveAction")
    static final String actionname = LiveActionFactory.LIVE_ACTION_NAME;
   
    public LiveAction createAction(Resource config) {
     ValueMap configs;
     /* Adapt the config resource to a ValueMap */
           if (config == null || config.adaptTo(ValueMap.class) == null) {
               configs = new ValueMapDecorator(Collections.<String, Object>emptyMap());
           } else {
               configs = config.adaptTo(ValueMap.class);
           }
   
     return new ExampleLiveAction(actionname, configs);
    }
    public String createsAction() {
     return actionname;
    }
    /************* LiveAction ****************/
    private static class ExampleLiveAction implements LiveAction {
     private String name;
     private ValueMap configs;
     private static final Logger log = LoggerFactory.getLogger(ExampleLiveAction.class);
   
     public ExampleLiveAction(String nm, ValueMap config){
      name = nm;
      configs = config;
     }
   
     public void execute(Resource source, Resource target,
       LiveRelationship liverel, boolean autoSave, boolean isResetRollout)
         throws WCMException {
   
      String lastMod = null;
   
      log.info(" *** Executing ExampleLiveAction *** ");
   
      /* Determine if the LiveAction is configured to copy the cq:lastModifiedBy property */
      if ((Boolean) configs.get("repLastModBy")){
   
       /* get the source's cq:lastModifiedBy property */
       if (source != null && source.adaptTo(Node.class) !=  null){
        ValueMap sourcevm = source.adaptTo(ValueMap.class);
        lastMod = sourcevm.get(com.day.cq.wcm.msm.api.MSMNameConstants.PN_PAGE_LAST_MOD_BY, String.class);
       }
   
       /* set the target node's la-lastModifiedBy property */
       Session session = null;
       if (target != null && target.adaptTo(Node.class) !=  null){
        ResourceResolver resolver = target.getResourceResolver();
        session = resolver.adaptTo(javax.jcr.Session.class);
        Node targetNode;
        try{
         targetNode=target.adaptTo(javax.jcr.Node.class);
         targetNode.setProperty("la-lastModifiedBy", lastMod);
         log.info(" *** Target node lastModifiedBy property updated: {} ***",lastMod);
        }catch(Exception e){
         log.error(e.getMessage());
        }
       }
       if(autoSave){
        try {
         session.save();
        } catch (Exception e) {
         try {
          session.refresh(true);
         } catch (RepositoryException e1) {
          e1.printStackTrace();
         }
         e.printStackTrace();
        }
       }
      }
     }
     public String getName() {
      return name;
     }
   
     /************* Deprecated *************/
     @Deprecated
     public void execute(ResourceResolver arg0, LiveRelationship arg1,
       ActionConfig arg2, boolean arg3) throws WCMException {
     }
     @Deprecated
     public void execute(ResourceResolver arg0, LiveRelationship arg1,
       ActionConfig arg2, boolean arg3, boolean arg4)
         throws WCMException {
     }
     @Deprecated
     public String getParameterName() {
      return null;
     }
     @Deprecated
     public String[] getPropertiesNames() {
      return null;
     }
     @Deprecated
     public int getRank() {
      return 0;
     }
     @Deprecated
     public String getTitle() {
      return null;
     }
     @Deprecated
     public void write(JSONWriter arg0) throws JSONException {
     }
    }
   }
   ```

1. Ändra katalogen till `MyLiveActionFactory` katalogen (Maven project directory). Ange sedan följande kommando:

   ```shell
   mvn -PautoInstallPackage clean install
   ```

1. AEM `error.log` filen ska ange att paketet har startats, vilket visas i loggarna på `https://<host>:<port>/system/console/status-slinglogs`.

   ```text
   13.08.2013 14:34:55.450 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent RESOLVED
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTING
   13.08.2013 14:34:55.451 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle BundleEvent STARTED
   13.08.2013 14:34:55.453 *INFO* [OsgiInstallerImpl] com.adobe.example.msm.MyLiveActionFactory-bundle Service [com.adobe.example.msm.ExampleLiveActionFactory,2188] ServiceEvent REGISTERED
   13.08.2013 14:34:55.454 *INFO* [OsgiInstallerImpl] org.apache.sling.audit.osgi.installer Started bundle com.adobe.example.msm.MyLiveActionFactory-bundle [316]
   ```

### Skapa exempelkonfigurationen {#create-the-example-rollout-configuration}

Skapa den MSM-utrullningskonfiguration som använder `LiveActionFactory` som du har skapat:

1. Skapa och konfigurera en [Konfiguration av utrullning med standardproceduren](/help/sites-cloud/administering/msm/live-copy-sync-config.md#creating-a-rollout-configuration) med egenskaperna:

   * **Titel**: Exempel på utrullningskonfiguration
   * **Namn**: exampleLoutconfig
   * **cq:trigger**: `publish`

### Lägg till Live-åtgärden i exempelkonfigurationen för utrullning {#add-the-live-action-to-the-example-rollout-configuration}

Konfigurera den utrullningskonfiguration som du skapade i föregående procedur så att den använder `ExampleLiveActionFactory` klassen.

1. Öppna CRXDE Lite.

1. Skapa följande nod under `/apps/msm/rolloutconfigs/examplerolloutconfig/jcr:content`:

   * **Namn**: `exampleLiveAction`
   * **Typ**: `cq:LiveSyncAction`

1. Klicka **Spara alla**.

1. Välj `exampleLiveAction` nod och lägg till en egenskap som ska anges för `ExampleLiveAction` klassen som `cq:LastModifiedBy` ska replikeras från källan till målnoden.

   * **Namn**: `repLastModBy`
   * **Typ**: `Boolean`
   * **Värde**: `true`

1. Klicka **Spara alla**.

### Skapa Live Copy {#create-the-live-copy}

[Skapa en live-kopia](/help/sites-cloud/administering/msm/creating-live-copies.md#creating-a-live-copy-of-a-page) på den engelska/Products-grenen på WKND-referenswebbplatsen med din rollout-konfiguration:

* **Källa**: `/content/wknd/language-masters/en/products`

* **Konfiguration av utrullning**: Exempel på utrullningskonfiguration

Aktivera **Produkter** (på engelska) sidan av källgrenen och observera loggmeddelandena som `LiveAction` klassen genererar:

```xml
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***ExampleLiveAction has been executed.***
16.08.2013 10:53:33.055 *INFO* [Thread-444535] com.adobe.example.msm.ExampleLiveActionFactory$ExampleLiveAction  ***Target node lastModifiedBy property updated: admin ***
```

## Ändra språknamn och standardländer {#changing-language-names-and-default-countries}

AEM använder en standarduppsättning med språk- och landskoder.

* Standardspråkkoden är den gemena tvåbokstavskoden enligt ISO-639-1.
* Standardlandskoden är den gemena eller versala tvåbokstavskoden enligt ISO 3166.

MSM använder en lagrad lista med språk- och landskoder för att fastställa namnet på landet som är associerat med namnet på språkversionen av sidan. Du kan ändra följande delar av listan om det behövs:

* Språktitlar
* Landsnamn
* Standardländer för språk (för koder som `en`, `de`, bland annat)

Språklistan sparas under `/libs/wcm/core/resources/languages` nod. Varje underordnad nod representerar ett språk eller ett språkområde:

* Nodnamnet är språkkoden (till exempel `en` eller `de`) eller koden för språk_land (till exempel `en_us` eller `de_ch`).

* The `language` -egenskapen för noden lagrar det fullständiga namnet på kodspråket.
* The `country` -egenskapen för noden lagrar det fullständiga namnet på landet för koden.
* När nodnamnet bara består av en språkkod (till exempel `en`), egenskapen country är `*`och ytterligare `defaultCountry` -egenskapen lagrar koden för det språkområde som ska användas för att ange landet.

![Språkdefinition](assets/msm-language-manager.png)

Så här ändrar du språk:

1. Öppna CRXDE Lite.
1. Välj `/apps` mapp och klicka på **Skapa** sedan **Skapa mapp.**

1. Namnge den nya mappen `wcm`.

1. Upprepa föregående steg för att skapa `/apps/wcm/core` mappträd. Skapa en nod av typen `sling:Folder` in `core` anropad `resources`.

1. Högerklicka på `/libs/wcm/core/resources/languages` och klicka på **Kopiera**.
1. Högerklicka på `/apps/wcm/core/resources` mapp och klicka på **Klistra in**. Ändra de underordnade noderna efter behov.
1. Klicka **Spara alla**.
1. Klicka **verktyg**, **Operationer** sedan **Webbkonsol**. Klicka från den här konsolen **OSGi** sedan **Konfiguration**.
1. Leta reda på och klicka **Day CQ WCM Language Manager** och ändra värdet för **Språklista** till `/apps/wcm/core/resources/languages`och sedan klicka **Spara**.

   ![Day CQ WCM Language Manager](assets/msm-language-manager.png)

## Konfigurera MSM-lås på sidegenskaper {#configuring-msm-locks-on-page-properties}

När du skapar en anpassad sidegenskap kan du behöva fundera på om den nya egenskapen ska kunna rullas ut till alla live-kopior.

Om till exempel två nya sidegenskaper läggs till:

* E-postadress:

   * Den här egendomen behöver inte lanseras eftersom den kommer att vara olika i varje land (eller varumärke osv.).

* Visuell huvudstil:

   * Projektkravet är att den här egenskapen ska rullas ut eftersom den (vanligtvis) är gemensam för alla länder (eller varumärken osv.).

Då måste du se till att:

* E-postadress:

   * Utesluts från de utrullade egenskaperna.
   * Se [Konfigurera Live Copy-synkronisering](/help/sites-cloud/administering/msm/live-copy-sync-config.md#excluding-properties-and-node-types-from-synchronization) för mer information.

* Visuell huvudstil:

   * Se till att du inte får redigera den här egenskapen om inte arvet avbryts.
   * Se även till att du sedan kan återskapa arv. Detta styrs genom att klicka på kedjelänkarna/brutna kedjor som växlar för att ange anslutningsstatus.

Anger om en sidegenskap ska rullas ut och därför styrs arvet av egenskapen dialog, under förutsättning att arvet avbryts/återställs vid redigering:

* `cq-msm-lockable`

   * Då skapas kedjelänkssymbolen i dialogrutan.
   * Detta tillåter bara redigering om arvet avbryts (kedjelänken bryts).
   * Detta gäller endast den första underordnade nivån för resursen
      * **Typ**: `String`
      * **Värde**: Innehåller namnet på den aktuella egendomen och är jämförbart med värdet på egendomen `name`
         * Se till exempel
           `/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title`

När `cq-msm-lockable` har definierats, om kedjan bryts/stängs kommer den att interagera med MSM på följande sätt:

* Om värdet för `cq-msm-lockable` är:

   * **Relativ** (till exempel `myProperty` eller `./myProperty`)

      * Om kedjan bryts läggs egenskapen till och tas bort från `cq:propertyInheritanceCancelled`.

   * **Absolut** (till exempel `/image`)

      * Om kedjan bryts avbryts arvet genom att det läggs till `cq:LiveSyncCancelled` blanda till `./image` och inställning `cq:isCancelledForChildren` till `true`.

      * Om du stänger kedjan återställs arvet.

>[!NOTE]
>
>`cq-msm-lockable` används på den första underordnade nivån för resursen som ska redigeras och den fungerar inte på något djupare nivåöverordnat objekt, oavsett om värdet är definierat som absolut eller relativ.

>[!NOTE]
>
>När du återaktiverar arv synkroniseras inte egenskapen för live-kopieringssidan automatiskt med egenskapen source. Du kan begära en synkronisering manuellt om det behövs.
