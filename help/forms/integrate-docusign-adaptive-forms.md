---
title: Hur integrerar man DocuSign med ett adaptivt formulär?
description: Lär dig hur du använder DocuSign med ett adaptivt formulär för att samla in e-signaturer.
exl-id: fb2e75d6-e454-4999-a079-f663af79051f
feature: Adaptive Forms, Acrobat Sign
role: User, Developer
source-git-commit: ab84a96d0e206395063442457a61f274ad9bed23
workflow-type: tm+mt
source-wordcount: '1413'
ht-degree: 0%

---

# Använda DocuSign med ett anpassat formulär {#integrate-aem-forms-with-DocuSign}

DocuSign är en framträdande e-signaturlösning. Du kan använda det för att e-signera ett avtal. Du kan integrera DocuSign med ett anpassat formulär. Det hjälper dig att skicka ett anpassat formulär för e-signaturer till flera mottagare. Med e-signaturer kan ni

- Slut avtal från vilken enhet som helst med fullt automatiserade processer för förslag, offerter och kontrakt.
- Slutför HR-processerna snabbare och ge medarbetarna de digitala upplevelserna.
- Minska kontraktscyklerna och anlita era leverantörer snabbare.

AEM Forms as a Cloud Service innehåller en [anpassad skickaåtgärd för DocuSign](#deploy-custom-submit-action). Med åtgärden Skicka kan du skicka adaptiva formulär för e-signaturer med hjälp av API:er för DocuSign.

| Du kan också använda Adobe e-signaturlösning, Adobe Sign, för att e-signera ett anpassat formulär. AEM Forms har en mycket djupare integrering med Adobe Sign och erbjuder mycket finare kontroller som sekventiell och parallell signering, flera autentiseringsmetoder, signering i formulär och mycket mer. Mer information finns i [Använda Adobe Sign i ett anpassat formulär](working-with-adobe-sign.md). |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## Förutsättningar {#prerequisites}

Följande krävs för att integrera DocuSign med AEM Forms:

- Ett DocuSign [utvecklarkonto](https://developers.docusign.com/platform/account/)
- Ett DocuSign-program
- Autentiseringsuppgifter (klient-ID och klienthemlighet) för API-programmet för DocuSign.
- [Anpassad skickaåtgärd och molntjänst för DocuSign](https://github.com/adobe/aem-forms-docusign-sample)
- (Endast för lokal utvecklingsmiljö) [Konfigurera postdokument](setup-local-development-environment.md#docker-microservices).

## Konfigurera anpassad inskickningsåtgärd och molntjänst för DocuSign {#deploy-custom-submit-action}

AEM Forms as a Cloud Service innehåller en anpassad skickaåtgärd för DocuSign. Med åtgärden Skicka kan du skicka adaptiva formulär för e-signaturer med hjälp av API:er för DocuSign. Kod för anpassad skickaåtgärd är tillgänglig på [AEM Forms samplar offentlig Git-databas](https://github.com/adobe/aem-forms-docusign-sample). Du kan distribuera koden som den är i din AEM Forms-miljö eller anpassa den efter organisationens behov.

Utför följande steg för att konfigurera en körklar anpassad sändningsåtgärd och DocuSign Cloud Service:

1. [Klona ditt AEM Forms as a Cloud Service-projekt](setup-local-development-environment.md#forms-cloud-service-local-development-environment) eller skapa ett [!DNL Experience Manager Forms] som ett [!DNL Cloud Service]-projekt baserat på [AEM Archetype 27](https://github.com/adobe/aem-project-archetype) eller senare. Så här skapar du ett [!DNL Experience Manager Forms] som ett [!DNL Cloud Service]-projekt baserat på AEM-arkitypen:
   </br> Öppna kommandotolken och kör nedanstående kommando för att skapa ett [!DNL Experience Manager Forms] as a Cloud Service-projekt:

   ```shell
   mvn -B archetype:generate -DarchetypeGroupId=com.adobe.aem -DarchetypeArtifactId=aem-project-archetype -DarchetypeVersion=27 -DaemVersion="cloud" -DappTitle="My Site" -DappId="mysite" -DgroupId="com.mysite" -DincludeForms="y"
   ```

   Ändra även `appTitle`, `appId` och `groupId` i ovanstående kommando så att den återspeglar din miljö.

1. Klona databasen [aem-forms-samples](https://github.com/adobe/aem-forms-docusign-sample). Den här databasen innehåller anpassad skickaåtgärd för DocuSign och konfigurationsinformation för anslutning till DocuSign-servern.

1. Öppna AEM Forms as a Cloud Service-projektet som skapats i steg 1 för redigering i den utvecklingsmiljö du vill.

1. Öppna filen `[AEM Forms as a Cloud Service project]\pom.xml` för redigering och gör följande ändringar:

   1. Lägg till följande text i slutet av taggen `<properties>`:

      ```shell
      <repository.location>maven_repository</repository.location>
      ```

   1. Lägg till följande text i slutet av taggen `<repositories>`:

      ```shell
       <repository>
          <id>project-repository</id>
          <url>file://${project.basedir}/${repository.location}</url>
       </repository>
      ```

      Om det inte finns någon `<repositories>`-tagg skapar du taggen under `<properties>`-taggen.

   1. Lägg till följande text i slutet av taggen `<dependencyManagement>`:

      ```shell
       <dependency>
         <groupId>com.adobe.aemforms.samples</groupId>
         <artifactId>forms.integration.docusign.all</artifactId>
         <type>zip</type>
         <version>1.0.0</version>
       </dependency>
      ```

1. Utför följande steg i filen `all/pom.xml` som finns i Cloud Service projektmapp:

   1. Lägg till följande text i slutet av taggen `<embeddeds>`:

      ```shell
       <embedded>
          <groupId>com.adobe.aemforms.samples</groupId>
          <artifactId>forms.integration.docusign.all</artifactId>
          <type>zip</type>
          <target>/apps/moonlightprodprogram-vendor-packages/application/install</target>
       </embedded>
      ```

   1. Lägg till följande text i slutet av taggen `<dependencies>`:

      ```shell
       <dependency>
          <groupId>com.adobe.aemforms.samples</groupId>
          <artifactId>forms.integration.docusign.all</artifactId>
          <type>zip</type>
       </dependency>
      ```

1. Öppna kommandotolken och gå till `aem-forms-samples\forms-integration-docusign` (klonat i steg 3) och kör följande kommando:

   ```shell
   mvn clean install -Dinstall.dir="<AEM Forms as a Cloud Service project path>/maven_repository"
   ```

   `<AEM Forms as a Cloud Service project path>` refererar till namnet på mappen som skapades i steg 1 av den här proceduren.

1. Distribuera projektet till din lokala utvecklingsmiljö. Du kan använda följande kommando för att distribuera till den lokala utvecklingsmiljön

   `mvn -PautoInstallPackage clean install`

   När du har utfört de här stegen kan du visa en ny anpassad sändningsåtgärd, [Skicka med elektroniska DocuSign-signaturer](#enabledocusign), som är tillgänglig i listan över sändningsalternativ för ett adaptivt formulär och en [DocumentSign-molntjänstkonfiguration](#configure-docusign-with-aem-forms) i den lokala utvecklingsmiljön.

1. Kompilera och [Distribuera koden till din [!DNL AEM Forms] as a Cloud Service-miljö](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=sv-SE#customer-releases).

## Integrera [!DNL DocuSign] med [!DNL AEM Forms] {#configure-docusign-with-aem-forms}

När förutsättningarna är uppfyllda utför du följande steg för att integrera [!DNL DocuSign] med [!DNL AEM Forms] på författarinstanserna.

1. Navigera till **[!UICONTROL Tools]** ![hammer](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL DocuSign]** och välj en mapp som ska vara värd för konfigurationen.

1. På konfigurationssidan väljer du **[!UICONTROL Create]** för att skapa [!DNL DocuSign]-konfigurationen i AEM Forms.
1. På fliken **[!UICONTROL General]** på sidan **[!UICONTROL Create DocuSign Configuration]** anger du **[!UICONTROL Name]** för konfigurationen och väljer **[!UICONTROL Next]**. Du kan också ange **[!UICONTROL Title]**.

1. Kopiera URL-adressen i det aktuella webbläsarfönstret till en anteckningsruta. URL:en krävs för att konfigurera [!DNL DocuSign]-programmet med [!DNL AEM Forms] i ett senare steg.

1. Konfigurera OAuth-inställningar för programmet [!DNL DocuSign]:

   1. Öppna ett webbläsarfönster och logga in på ditt [!DNL DocuSign] [utvecklarkonto](https://admindemo.docusign.com/apps-and-keys).
   1. Öppna appen som konfigurerats för [!DNL AEM Forms].
   1. Lägg till den URL som kopierades i föregående steg i rutan **[!UICONTROL Redirect URI]** och klicka på **[!UICONTROL Save]**.
   1. Anteckna Integrering och Hemliga nycklar.

   Stegvis information om hur du konfigurerar OAuth-inställningar för ett [!DNL DocuSign]-program och hämtar nycklarna finns i [Konfigurera autentiseringsinställningar för programmets &#x200B;](https://support.docusign.com/guides/ndse-admin-guide-api-and-keys) utvecklardokumentation.

1. Gå tillbaka till sidan **[!UICONTROL Create DocuSign Configuration]**. På fliken **[!UICONTROL Settings]** anger fältet **[!UICONTROL OAuth URL]** följande standard-URL:

   `https://account-d.docusign.com/oauth/auth`

1. Ange **[!UICONTROL Client ID]** (DocuSign-integreringsnyckel) och **[!UICONTROL Client Secret]** (hemlig DocuSign-nyckel).

1. Välj **[!UICONTROL Connect to DocuSign]**. När du uppmanas att ange autentiseringsuppgifter anger du användarnamn och lösenord för kontot som används när programmet [!DNL DocuSign] skapas. När du ombeds bekräfta åtkomst för `your developer account` klickar du på **[!UICONTROL Allow Access]**. Om inloggningsuppgifterna är korrekta visas ett meddelande om att åtgärden lyckades.

1. Välj **[!UICONTROL Create]** om du vill skapa [!DNL DocuSign]-konfigurationen.

1. Markera konfigurationen och klicka på **[!UICONTROL Publish]**, markera konfigurationen och klicka på **[!UICONTROL Publish]**. Konfigurationen replikeras till motsvarande publiceringsmiljöer.

1. Upprepa alla ovanstående steg på din utvecklare, scen och produktionsinstanser (beroende på vad som återstår) för att slutföra konfigurationen av [!DNL DocuSign] med [!DNL AEM Forms] för din miljö.

Nu är din AEM Forms-miljö konfigurerad att använda DocuSign. Se till att du lägger till konfigurationsbehållaren som används för Cloud Service i alla adaptiva Forms som aktiveras för [!DNL DocuSign]. Du kan ange en konfigurationsbehållare bland egenskaperna för ett adaptivt formulär.

### Använd [!DNL DocuSign] i ett adaptivt formulär {#enabledocusign}

Du kan aktivera [!DNL DocuSign] för ett befintligt adaptivt formulär eller skapa ett [!DNL DocuSign]-aktiverat adaptivt formulär. Välj något av följande:

- [Skapa ett  [!DNL DocuSign] aktiverat anpassat formulär](#create-an-adaptive-form-for-docusign)
- [Aktivera [!DNL DocuSign] för ett befintligt anpassat formulär](#editafsign).

#### Skapa ett anpassat formulär för DocuSign {#create-an-adaptive-form-for-docusign}

Så här skapar du ett signeringsaktiverat adaptivt formulär:

1. Navigera till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.
1. Välj **[!UICONTROL Create]** och välj **[!UICONTROL Adaptive Form]**. En lista med mallar visas. Välj en mall och välj **[!UICONTROL Next]**.
1. På fliken **[!UICONTROL Basic]**:

   1. Ange **[!UICONTROL Name]** och **[!UICONTROL Title]** för det adaptiva formuläret.

   1. Välj [konfigurationsbehållaren](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) som skapades när [integrerar [!DNL DocuSign] med [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).

   Konfigurationsbehållaren innehåller de [!DNL DocuSign] molntjänster som är konfigurerade för din miljö. Dessa tjänster kan väljas i verktyget Adaptiv form.

1. Välj något av följande alternativ på fliken **[!UICONTROL Form Model]**:

   - Om du har en anpassad formulärmall och kräver ett dokument för post som är baserat på formulärmallen, markerar du alternativet **[!UICONTROL Associate form template as the Document of Record template]** och väljer en dokumentmall. När du använder alternativet visas endast de fält som är baserade på den associerade formulärmallen i de dokument som skickas för signering. Alla fält i det adaptiva formuläret visas inte.

   - Om du inte har någon anpassad formulärmall väljer du alternativet **[!UICONTROL Generate Document of Record]**. När du använder alternativet visas alla fält i det adaptiva formuläret i det dokument som skickas för signering.

1. Välj **[!UICONTROL Create]**. Ett signeringsaktiverat anpassat formulär skapas. Du kan lägga till dina [!DNL DocuSign]-fält i formuläret och skicka det för signering.
1. Öppna det adaptiva formuläret i redigeringsläge. Markera **[!UICONTROL Content]** på fliken **[!UICONTROL Form Container]** och välj ![Konfigurera](assets/configure-icon.svg).

1. I avsnittet **[!UICONTROL Submission]** väljer du **[!UICONTROL Submit with DocuSign electronic signatures]** i listrutan **[!UICONTROL Submit Action]**.

1. I avsnittet **[!UICONTROL Action Configuration]** väljer du **[!UICONTROL Add]** om du vill lägga till en mottagare och ange mottagarens e-postadress. Välj **[!UICONTROL Add]** igen om du vill lägga till fler mottagare.

1. Ange ämnet för e-postmeddelandet i fältet **[!UICONTROL Email Subject]**. Välj **Inkludera bifogade filer** om du vill inkludera bifogade filer i e-postmeddelandet.

1. Välj ![Spara](assets/save_icon.svg) om du vill spara egenskaperna.

#### Aktivera [!DNL DocuSign] för ett anpassat formulär {#editafsign}

Så här använder du [!DNL DocuSign] i ett befintligt adaptivt formulär:

1. Navigera till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.
1. Markera det adaptiva formuläret och välj **[!UICONTROL Properties]**.
1. På fliken **[!UICONTROL Basic]** väljer du den [konfigurationsbehållare](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) som skapades när [!DNL DocuSign] integrerades med [!DNL AEM Forms].
1. Välj något av följande alternativ på fliken **[!UICONTROL Form Model]**:

   - Om du har en anpassad formulärmall och kräver ett dokument för post som är baserat på formulärmallen, markerar du alternativet **[!UICONTROL Associate form template as the Document of Record template]** och väljer en dokumentmall. När du använder alternativet visas endast de fält som är baserade på den associerade formulärmallen i de dokument som skickas för signering. Alla fält i det adaptiva formuläret visas inte.

   - Om du inte har någon anpassad formulärmall väljer du alternativet **[!UICONTROL Generate Document of Record]**. När du använder alternativet visas alla fält i det adaptiva formuläret i det dokument som skickas för signering.

1. Välj **[!UICONTROL Save & Close]**. Det adaptiva formuläret har aktiverats för [!DNL DocuSign]. Nu kan du lägga till dina [!DNL DocuSign]-fält i formuläret och skicka det för signering.

1. Öppna det adaptiva formuläret i redigeringsläge. Markera **[!UICONTROL Content]** på fliken **[!UICONTROL Form Container]** och välj ![Konfigurera](assets/configure-icon.svg).

1. I avsnittet **[!UICONTROL Submission]** väljer du **[!UICONTROL Submit with DocuSign electronic signatures]** i listrutan **[!UICONTROL Submit Action]**.

1. I avsnittet **[!UICONTROL Action Configuration]** väljer du **[!UICONTROL Add]** om du vill lägga till en mottagare och ange mottagarens e-postadress. Välj **[!UICONTROL Add]** igen om du vill lägga till fler mottagare.

1. Ange ämnet för e-postmeddelandet i fältet **[!UICONTROL Email Subject]**. Välj **Inkludera bifogade filer** om du vill inkludera bifogade filer i e-postmeddelandet.

1. Välj ![Spara](assets/save_icon.svg) om du vill spara egenskaperna.
