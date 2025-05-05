---
title: Hur skapar man en anpassad inskickningsåtgärd för ett anpassat formulär baserat på kärnkomponenterna?
description: Lär dig hur du skapar en anpassad Skicka-åtgärd för en anpassad Forms för att bearbeta data innan du skickar in dem med den anpassade skicka-åtgärden.
feature: Adaptive Forms, Core Components
role: User, Developer
level: Intermediate
source-git-commit: b703d4c0b0bb25ecc57e5335b672069f7ad2199d
workflow-type: tm+mt
source-wordcount: '1078'
ht-degree: 0%

---


# Skapa en anpassad sändningsåtgärd för adaptiva Forms (kärnkomponenter)

Med en skicka-åtgärd kan användarna välja mål för de data som hämtas från ett formulär och definiera ytterligare funktioner som ska utföras när formulär skickas. AEM har stöd för flera [färdiga åtgärder (OTB)](/help/forms/configure-submit-actions-core-components.md), t.ex. att skicka ett e-postmeddelande eller spara data till SharePoint eller OneDrive.

Du kan också skapa en anpassad skickaåtgärd för att lägga till funktioner som inte ingår i de [färdiga alternativen](/help/forms/configure-submit-actions-core-components.md#select-and-configure-a-submit-action-for-an-adaptive-form-select-and-configure-submit-action). Integrera till exempel formulärdata med ett program från en annan leverantör eller utlösa ett personanpassat SMS-meddelande baserat på användarens indata.

<!-- ![Custom Submit Image](/help/forms/assets/custom-submit-action-hero-image.png)
-->

## Krav

Innan du börjar skapa din första anpassade sändningsåtgärd för Adaptive Forms ska du kontrollera att du har följande:

* **Vanlig textredigerare (IDE)**: En integrerad utvecklingsmiljö (IDE), som Microsoft Visual Studio Code, har avancerade funktioner för enklare redigering, även om en vanlig textredigerare kan fungera.

* **Git**: Det här versionskontrollsystemet krävs för att hantera kodändringar. Om du inte har det installerat hämtar du det från https://git-scm.com.

## Skapa din första anpassade skickaåtgärd för formulär

I bilden nedan visas stegen för att skapa en anpassad skickaåtgärd för ett anpassat formulär:

![Anpassat arbetsflöde för skickaåtgärd](/help/forms/assets/custom-submit-action-workflow.png){width=50%, height-50%}

### Klona AEM as a Cloud Service Git-databasen.

1. Öppna kommandoraden och välj en katalog där AEM as a Cloud Service-databasen ska lagras, t.ex. `/cloud-service-repository/`.

1. Kör följande kommando för att klona databasen:

   ```
   git clone https://git.cloudmanager.adobe.com/<organization-name>/<app-id>/
   ```

   **Var hittar du den här informationen?**

   Stegvisa instruktioner om hur du hittar dessa uppgifter finns i Adobe Experience League-artikeln [Accessing Git](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=sv-SE#accessing-git).

   **Projektet är klart!**

   När kommandot har slutförts visas en ny mapp som har skapats i din lokala katalog. Den här mappen namnges efter ditt program (till exempel app-id). Den här mappen innehåller alla filer och all kod som hämtats från din AEM as a Cloud Service Git-databas. Du kan hitta `<appid>` för ditt AEM projekt i filen `archetype.properties`.

   ![Egenskaper för arkitekttyp](/help/forms/assets/custom-submit-action-archetype-app-id.png)

   I hela den här guiden ser vi den här mappen som `[AEMaaCS project directory]`.

## Lägg till ny skickaåtgärd

1. Öppna databasmappen i en redigerare.

   ![Klonad databas](/help/forms/assets/custom-submit-action-clone-repo.png)

1. Navigera till följande katalog i din `[AEMaaCS project directory]`:

   ```
   /ui.apps/src/main/content/jcr_root/apps/<app-id>/
   ```

   **Viktigt**: Ersätt `<app-id>` med ditt faktiska program-ID.

1. Skapa en ny mapp för din anpassade sändningsåtgärd och ge den ett namn du väljer. Ge till exempel mappen namnet `customsubmitaction`.

   ![Skapa en anpassad mapp för sändningsåtgärder](/help/forms/assets/custom-submit-action-create-folder.png)

1. Navigera till den tillagda anpassade åtgärdskatalogen för skicka.

   Navigera till följande sökväg i din `[AEMaaCS project directory]`:

   `/ui.apps/src/main/content/jcr_root/apps/<app-id>/customsubmitaction/`

   `Important`: Ersätt &lt;app-id> med ditt faktiska program-ID.

1. Skapa ny konfigurationsfil.
Skapa en ny fil med namnet `.content.xml` i mappen `customsubmitaction`.

   ![Skapa konfigurationsfil](/help/forms/assets/custom-submit-action-create-config-folder.png)

1. Öppna den här filen och klistra in följande innehåll och ersätt `[customsubmitaction]` med namnet på din sändningsåtgärd

   ```
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:jcr="http://www.jcp.org/jcr/1.0" xmlns:sling="http://sling.apache.org/jcr/sling/1.0"
   jcr:description="[customsubmitaction]"
   jcr:primaryType="sling:Folder"
   
   guideComponentType="fd/af/components/guidesubmittype"
   guideDataModel="basic,xfa,xsd"
   submitService="[customsubmitaction]"/>
   ```

   Ersätt till exempel `[customsubmitaction]` med ditt anpassade namn på åtgärden Skicka som `Custom Submit Action`.

   ![Skapa anpassad konfigurationsfil för skickaåtgärd](/help/forms/assets/custom-submit-action-config-file.png)

   >[!NOTE]
   >
   > Kom ihåg namnet på [anpassad inskickning], eftersom samma namn visas i listrutan `Submit action` när du redigerar ett formulär.


**Inkludera den nya mappen i`filter.xml`**

1. Navigera till filen `/ui.apps/src/main/content/META-INF/vault/filter.xml` i [AEMaaCS-projektkatalogen].

1. Öppna filen och lägg till följande rad i slutet:

   ```
   <filter root="/apps/<app-id>/[customsubmitaction-folder]"/>
   ```

   Lägg till exempel till följande kodrad för att lägga till mappen `customsubmitaction` i filen `filter.xml`:

   ```
   <filter root="/apps/wknd/customsubmitaction"/>
   ```

   ![Lägg till skapade mappar i filter.xml](/help/forms/assets/custom-submit-action-filter-xml.png)

1. Spara ändringarna.

### Implementera tjänsten för den tillagda skicka-åtgärden.

1. Navigera till följande katalog i din `[AEMaaCS project directory]`:
   `/core/src/main/java/com/<app-id>/core/service/`
   `Important`: Ersätt &lt;app-id> med ditt faktiska program-ID.
1. Skapa en ny Java-fil för att implementera tjänsten för den tillagda sändningsåtgärden. Lägg till exempel till en ny Java-fil som `CustomSubmitService.java`.

   ![Anpassad mapp för överföringsåtgärd](/help/forms/assets/custom-submit-action-custom-submit-folder.png)

1. Öppna den här filen och lägg till koden för den anpassade implementeringen av åtgärden skicka.

   Java-koden nedan är till exempel en OSGi-tjänst som hanterar formuläröverföringen genom att logga skickade data och returnerar statusen `OK`. Lägg till följande kod i filen `CustomSubmitService.java`:

   ```
   package com.wknd.core.service;
   
   import com.adobe.aemds.guide.model.FormSubmitInfo;
   import com.adobe.aemds.guide.service.FormSubmitActionService;
   import java.util.HashMap;
   import java.util.Map;
   import org.osgi.service.component.annotations.Component;
   import org.slf4j.Logger;
   import org.slf4j.LoggerFactory;
   
       @Component(
       service = FormSubmitActionService.class,
       immediate = true
           )
       public class CustomSubmitService implements FormSubmitActionService {
   
       private static final String serviceName = "Custom Submit Action";
   
       private static Logger log = LoggerFactory.getLogger(CustomSubmitService.class);
   
       @Override
       public String getServiceName() {
       return serviceName;
       }
   
       @Override
       public Map<String, Object> submit(FormSubmitInfo formSubmitInfo) {
       String data = formSubmitInfo.getData();
       log.info("Using custom submit action service, [data] --> " + data);
       Map<String, Object> result = new HashMap<>();
       result.put("status", "OK");
       return result;
        }
       }
   ```

   ![Anpassad skickaåtgärd ](/help/forms/assets/custom-submit-action-service.png)

1. Spara ändringarna.

### Distribuera koden.

**Distribuera kod för lokal utvecklingsmiljö**

* Distribuera AEM as a Cloud Service, `[AEMaaCS project directory]`, till din lokala utvecklingsmiljö för att testa den nya skicka-åtgärden på din lokala dator. Så här distribuerar du till din lokala utvecklingsmiljö:

   1. Kontrollera att den lokala utvecklingsmiljön är igång och körs. Om du inte redan har konfigurerat en lokal utvecklingsmiljö läser du i guiden [Konfigurera en lokal utvecklingsmiljö för AEM Forms](/help/forms/setup-local-development-environment.md).

   1. Öppna terminalfönstret eller kommandotolken.

   1. Navigera till `[AEMaaCS project directory]`.

   1. Kör följande kommando:

      ```
      mvn -PautoInstallPackage clean install
      ```

      ![Lokal distribution](/help/forms/assets/custom-submit-action-local-deployment.png)

**Distribuera koden för Cloud Servicen**

* Distribuera AEM as a Cloud Service, `[AEMaaCS project directory]`, till din Cloud Service. Så här distribuerar du till din Cloud Service:

   1. Genomför ändringarna:

      När du har lagt till den nya anpassade konfigurationen för åtgärden Skicka verkställer du ändringarna med ett tydligt Git-meddelande. (Exempel:&quot;En ny anpassad sändningsåtgärd har lagts till&quot;).

   1. Distribuera den uppdaterade koden:

      Utlös en distribution av koden via den [befintliga pipelinen för hela stacken](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=sv-SE#setup-pipeline). Den genererar och distribuerar automatiskt den uppdaterade koden med det nya stödet för åtgärden Skicka.

      Om du inte redan har konfigurerat en pipeline kan du läsa guiden [Konfigurera en pipeline för AEM Forms as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/onboarding/journey/developers.html?lang=sv-SE#setup-pipeline).

      ![Molndistribution](/help/forms/assets/custom-submit-action-cloud-deployment.png)

      **Hur bekräftar jag installationen?**

      När projektet har skapats visas den anpassade åtgärden för att skicka i listrutan `Submit action` när du redigerar ett formulär.

      ![Listruta för anpassad sändningsåtgärd](/help/forms/assets/custom-submit-action-drop-down-list.png)

  Miljön är nu klar att använda den nya anpassade skicka-åtgärden när du redigerar ett formulär.

### Förhandsgranska ett anpassat formulär med en nyligen tillagd åtgärd för att skicka

1. Logga in på din AEM Forms as a Cloud Service-instans.
1. Gå till **Forms** > **Forms och dokument**.

   ![Forms och dokument](/help/forms/assets/custom-submit-action-fnd.png)

1. Markera ett anpassat formulär och klicka på **Redigera**. Formuläret öppnas i redigeringsläge.

   ![Redigera formulär](/help/forms/assets/custom-submit-action-edit-af.png)

1. Öppna innehållsläsaren och markera komponenten **[!UICONTROL Guide Container]** i det adaptiva formuläret.
1. Klicka på ikonen för egenskaper för stödlinjebehållaren ![Egenskaper för stödlinje](/help/forms/assets/configure-icon.svg) . Dialogrutan Adaptiv formulärbehållare öppnas.
1. Klicka på fliken **[!UICONTROL Submission]**.
1. Välj åtgärden Skicka i listrutan **[!UICONTROL Submit Action]**. Välj till exempel åtgärden Skicka som `Custom Submit Action`.

   ![Anpassat skickningsformulär](/help/forms/assets/custom-submit-action-select-submit-action.png)

1. Fyll i formuläret och skicka det.

   ![Skicka formulär](/help/forms/assets/custom-submit-action-submit-form.png)

   ![Tack](/help/forms/assets/custom-submit-action-thankyou-msg.png)

   När formuläret har skickats kan du kontrollera **Adobe Experience Manager Web Console-konfigurationen** för att verifiera åtgärden för den anpassade skicka-åtgärden i den lokala utvecklingsmiljön.
1. Gå till `http://<host>:<port>/system/console/configMgr`.

1. Gå till **Adobe Experience Manager Web Console Log Support** på `http://<host>:<port>/system/console/slinglog`.

   ![ConfigMgr](/help/forms/assets/custom-submit-action-sling-log.png)

1. Klicka på alternativet `logs/error.log`.
   ![Öppna fel.loggfil](/help/forms/assets/custom-submit-action-error-log.png)

1. Öppna filen `error.log` för att se att data har lagts till i den.

   ![error.log-fil](/help/forms/assets/custom-submit-action-form-data-display.png)

   >[!NOTE]
   >
   > Om du vill visa felloggar i AEM as a Cloud Service-miljön kan du använda Splunk.

<!--
## Best practices

 * It is recommended to use the OSGi service approach for creating a custom submit action, as it is faster than the AEM servlet approach. 

## Next steps
-->

## Relaterade artiklar

{{af-submit-action}}

<!-- The [Adaptive Forms Core Components](https://github.com/adobe/aem-core-forms-components) repository includes a sample folder, `customsubmission/logsubmit`, to simplify the process of adding new custom submit actions. It also provides the Java service implementation for the `logsubmit` custom submit action, named `CustomAFSubmitService`.java. These resources are available on GitHub. -->