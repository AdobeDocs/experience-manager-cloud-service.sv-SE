---
title: Hur integrerar man DocuSign med ett adaptivt formulär?
description: Lär dig hur du använder DocuSign med ett adaptivt formulär för att samla in e-signaturer.
exl-id: fb2e75d6-e454-4999-a079-f663af79051f
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '1413'
ht-degree: 0%

---

# Använda DocuSign med ett anpassat formulär {#integrate-aem-forms-with-DocuSign}

DocuSign är en framträdande e-signaturlösning. Du kan använda det för att e-signera ett avtal. Du kan integrera DocuSign med ett anpassat formulär. Det hjälper dig att skicka ett anpassat formulär för e-signaturer till flera mottagare. Med e-signaturer kan ni

- Slut avtal från vilken enhet som helst med fullt automatiserade processer för förslag, offerter och kontrakt.
- Slutför HR-processerna snabbare och ge medarbetarna de digitala upplevelserna.
- Minska kontraktscyklerna och anlita era leverantörer snabbare.

AEM Forms as a Cloud Service har en [anpassad skickaåtgärd för DocuSign](#deploy-custom-submit-action). Med åtgärden Skicka kan du skicka adaptiva formulär för e-signaturer med hjälp av API:er för DocuSign.

| Du kan också använda Adobe signaturlösning, Adobe Sign, för att e-signera ett anpassat formulär. AEM Forms har en mycket djupare integrering med Adobe Sign och ger mycket finare kontroller som sekventiell och parallell signering, flera autentiseringsmetoder, signering i formulär med mera. Mer information finns i [Använda Adobe Sign i en adaptiv form](working-with-adobe-sign.md). |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

## Förutsättningar {#prerequisites}

Följande krävs för att integrera DocuSign med AEM Forms:

- En DocuSign [utvecklarkonto](https://developers.docusign.com/platform/account/)
- Ett DocuSign-program
- Autentiseringsuppgifter (klient-ID och klienthemlighet) för API-programmet för DocuSign.
- [Anpassad inskickningsåtgärd och molntjänst för DocuSign](https://github.com/adobe/aem-forms-docusign-sample)
- (Endast för lokal utvecklingsmiljö) [Konfigurera postdokument](setup-local-development-environment.md#docker-microservices).

## Konfigurera anpassad inskickningsåtgärd och molntjänst för DocuSign {#deploy-custom-submit-action}

AEM Forms as a Cloud Service innehåller en anpassad skickaåtgärd för DocuSign. Med åtgärden Skicka kan du skicka adaptiva formulär för e-signaturer med hjälp av API:er för DocuSign. Kod för anpassad skickaåtgärd är tillgänglig på [AEM Forms samplar offentlig Git-databas](https://github.com/adobe/aem-forms-docusign-sample). Du kan distribuera koden som den är i din AEM Forms-miljö eller anpassa den efter organisationens behov.

Utför följande steg för att konfigurera en körklar anpassad sändningsåtgärd och DocuSign-Cloud Service:

1. [Klona ditt as a Cloud Service AEM Forms-projekt](setup-local-development-environment.md#forms-cloud-service-local-development-environment) eller skapa [!DNL Experience Manager Forms] som [!DNL Cloud Service] projekt baserat på [AEM 27](https://github.com/adobe/aem-project-archetype) eller senare. Skapa en [!DNL Experience Manager Forms] som [!DNL Cloud Service] projekt baserat på AEM Archetype:
   </br> Öppna kommandotolken och kör nedanstående kommando för att skapa en [!DNL Experience Manager Forms] as a Cloud Service projekt:

   ```shell
   mvn -B archetype:generate -DarchetypeGroupId=com.adobe.aem -DarchetypeArtifactId=aem-project-archetype -DarchetypeVersion=27 -DaemVersion="cloud" -DappTitle="My Site" -DappId="mysite" -DgroupId="com.mysite" -DincludeForms="y"
   ```

   Ändra också `appTitle`, `appId`och `groupId`, i ovanstående kommando för att återspegla din miljö.

1. Klona [aem-forms-samples](https://github.com/adobe/aem-forms-docusign-sample) databas. Den här databasen innehåller anpassad skickaåtgärd för DocuSign och konfigurationsinformation för anslutning till DocuSign-servern.

1. Öppna AEM Forms as a Cloud Service projekt som skapats i steg 1 för redigering i den utvecklingsmiljö du vill.

1. Öppna `[AEM Forms as a Cloud Service project]\pom.xml` -fil för redigering och gör följande ändringar:

   1. Lägg till följande text i slutet av `<properties>` tagg:

      ```shell
      <repository.location>maven_repository</repository.location>
      ```

   1. Lägg till följande text i slutet av `<repositories>` tagg:

      ```shell
       <repository>
          <id>project-repository</id>
          <url>file://${project.basedir}/${repository.location}</url>
       </repository>
      ```

      Om det inte finns något `<repositories>` skapar du taggen under -taggen `<properties>` -tagg.

   1. Lägg till följande text i slutet av `<dependencyManagement>` tagg:

      ```shell
       <dependency>
         <groupId>com.adobe.aemforms.samples</groupId>
         <artifactId>forms.integration.docusign.all</artifactId>
         <type>zip</type>
         <version>1.0.0</version>
       </dependency>
      ```

1. Utför följande steg i `all/pom.xml` -fil finns i Cloud Servicens projektmapp:

   1. Lägg till följande text i slutet av `<embeddeds>` tagg:

      ```shell
       <embedded>
          <groupId>com.adobe.aemforms.samples</groupId>
          <artifactId>forms.integration.docusign.all</artifactId>
          <type>zip</type>
          <target>/apps/moonlightprodprogram-vendor-packages/application/install</target>
       </embedded>
      ```

   1. Lägg till följande text i slutet av `<dependencies>` tagg:

      ```shell
       <dependency>
          <groupId>com.adobe.aemforms.samples</groupId>
          <artifactId>forms.integration.docusign.all</artifactId>
          <type>zip</type>
       </dependency>
      ```

1. Öppna kommandotolken och navigera till `aem-forms-samples\forms-integration-docusign` (klonat i steg 3) och kör följande kommando:

   ```shell
   mvn clean install -Dinstall.dir="<AEM Forms as a Cloud Service project path>/maven_repository"
   ```

   `<AEM Forms as a Cloud Service project path>` refererar till namnet på mappen som skapades i steg 1 i den här proceduren.

1. Distribuera projektet till din lokala utvecklingsmiljö. Du kan använda följande kommando för att distribuera till den lokala utvecklingsmiljön

   `mvn -PautoInstallPackage clean install`

   När du har utfört de här stegen kan du visa en ny anpassad skicka-åtgärd [Skicka med elektroniska signaturer i DocuSign](#enabledocusign) finns i listan med alternativ för att skicka in formulär med adaptiv form och en [DokSign-molntjänstkonfiguration](#configure-docusign-with-aem-forms) i den lokala utvecklingsmiljön.

1. Kompilera och [Distribuera koden till [!DNL AEM Forms] as a Cloud Service miljö](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/overview.html?lang=en#customer-releases).

## Integrera [!DNL DocuSign] med [!DNL AEM Forms] {#configure-docusign-with-aem-forms}

Utför följande steg för att integrera [!DNL DocuSign] med [!DNL AEM Forms] på Author-instanserna.

1. Navigera till **[!UICONTROL Tools]** ![hammare](assets/hammer.png) > **[!UICONTROL Cloud Services]** > **[!UICONTROL DocuSign]** och välj en mapp som ska vara värd för konfigurationen.

1. Välj på konfigurationssidan **[!UICONTROL Create]** att skapa [!DNL DocuSign] i AEM Forms.
1. I **[!UICONTROL General]** -fliken i **[!UICONTROL Create DocuSign Configuration]** sida, ange en **[!UICONTROL Name]** för konfigurationen och välj **[!UICONTROL Next]**. Du kan också ange en **[!UICONTROL Title]**.

1. Kopiera URL-adressen i det aktuella webbläsarfönstret till en anteckningsruta. URL:en krävs för att konfigurera [!DNL DocuSign] program med [!DNL AEM Forms] i ett senare steg.

1. Konfigurera OAuth-inställningar för [!DNL DocuSign] program:

   1. Öppna ett webbläsarfönster och logga in på [!DNL DocuSign] [utvecklarkonto](https://admindemo.docusign.com/apps-and-keys).
   1. Öppna programmet som konfigurerats för [!DNL AEM Forms].
   1. I **[!UICONTROL Redirect URI]** lägger du till den URL som kopierades i föregående steg och klickar på **[!UICONTROL Save]**.
   1. Anteckna Integrering och Hemliga nycklar.

   Om du vill ha stegvis information om hur du konfigurerar OAuth-inställningar för en [!DNL DocuSign] program och hämta nycklarna, se [Konfigurera autentiseringsinställningar för programmet](https://support.docusign.com/guides/ndse-admin-guide-api-and-keys) dokumentation för utvecklare.

1. Gå tillbaka till **[!UICONTROL Create DocuSign Configuration]** sida. I **[!UICONTROL Settings]** -fliken, **[!UICONTROL OAuth URL]** I fältet anges följande standard-URL:

   `https://account-d.docusign.com/oauth/auth`

1. Ange **[!UICONTROL Client ID]** (DocuSign-integreringsnyckel) och **[!UICONTROL Client Secret]** (Hemlig nyckel för DocuSign).

1. Välj **[!UICONTROL Connect to DocuSign]**. Ange användarnamn och lösenord för kontot som används när du skapar inloggningsuppgifter [!DNL DocuSign] program. När du ombeds att bekräfta åtkomsten för `your developer account`, klicka **[!UICONTROL Allow Access]**. Om inloggningsuppgifterna är korrekta visas ett meddelande om att åtgärden lyckades.

1. Välj **[!UICONTROL Create]** för att skapa [!DNL DocuSign] konfiguration.

1. Välj konfigurationen och klicka på **[!UICONTROL Publish]**, markera konfigurationen och klicka på **[!UICONTROL Publish]**. Konfigurationen replikeras till motsvarande publiceringsmiljöer.

1. Upprepa alla ovanstående steg på utvecklaren, scenen och produktionsinstanserna (beroende på vad som återstår) för att slutföra konfigurationen [!DNL DocuSign] med [!DNL AEM Forms] för din miljö.

Nu är din AEM Forms-miljö konfigurerad att använda DocuSign. Se till att du lägger till konfigurationsbehållaren som används för Cloud Servicen i alla adaptiva Forms som aktiveras för [!DNL DocuSign]. Du kan ange en konfigurationsbehållare bland egenskaperna för ett adaptivt formulär.

### Använd [!DNL DocuSign] i adaptiv form {#enabledocusign}

Du kan aktivera [!DNL DocuSign] för ett befintligt adaptivt formulär eller skapa ett [!DNL DocuSign] aktiverad adaptiv form. Välj något av följande:

- [Skapa en [!DNL DocuSign] aktiverat adaptivt format](#create-an-adaptive-form-for-docusign)
- [Aktivera [!DNL DocuSign] för ett befintligt adaptivt formulär](#editafsign).

#### Skapa ett anpassat formulär för DocuSign {#create-an-adaptive-form-for-docusign}

Så här skapar du ett signeringsaktiverat adaptivt formulär:

1. Navigera till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.
1. Välj **[!UICONTROL Create]** och markera **[!UICONTROL Adaptive Form]**. En lista med mallar visas. Välj en mall och välj **[!UICONTROL Next]**.
1. I **[!UICONTROL Basic]** tab:

   1. Ange **[!UICONTROL Name]** och **[!UICONTROL Title]** för den adaptiva formen.

   1. Välj [konfigurationsbehållare](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) skapad [integrering [!DNL DocuSign] med [!DNL AEM Forms]](adobe-sign-integration-adaptive-forms.md).

   Konfigurationsbehållaren innehåller [!DNL DocuSign] Cloud Service som konfigurerats för din miljö. Dessa tjänster kan väljas i redigeraren för adaptiva formulär.

1. I **[!UICONTROL Form Model]** väljer du något av följande alternativ:

   - Om du har en anpassad formulärmall och kräver ett postdokument som är baserat på formulärmallen väljer du **[!UICONTROL Associate form template as the Document of Record template]** och välj en dokumentmall. När du använder alternativet visas endast de fält som är baserade på den associerade formulärmallen i de dokument som skickas för signering. Alla fält i det adaptiva formuläret visas inte.

   - Om du inte har någon anpassad formulärmall väljer du **[!UICONTROL Generate Document of Record]** alternativ. När du använder alternativet visas alla fält i det adaptiva formuläret i det dokument som skickas för signering.

1. Välj **[!UICONTROL Create.]** Ett signeringsaktiverat anpassat formulär skapas. Du kan lägga till [!DNL DocuSign] fält till formuläret och skicka det för signering.
1. Öppna det adaptiva formuläret i redigeringsläge. I **[!UICONTROL Content]** väljer du **[!UICONTROL Form Container]** och markera ![Konfigurera](assets/configure-icon.svg).

1. I **[!UICONTROL Submission]** avsnitt, markera **[!UICONTROL Submit with DocuSign electronic signatures]** från **[!UICONTROL Submit Action]** listruta.

1. I **[!UICONTROL Action Configuration]** avsnitt, markera **[!UICONTROL Add]** om du vill lägga till en mottagare och ange mottagarens e-postadress. Välj **[!UICONTROL Add]** igen om du vill lägga till fler mottagare.

1. Ange ämnet för e-postmeddelandet i **[!UICONTROL Email Subject]** fält. Välj **Inkludera bifogade filer** om du vill inkludera bilagor i e-postmeddelandet.

1. Välj ![Spara](assets/save_icon.svg) för att spara egenskaperna.

#### Aktivera [!DNL DocuSign] för ett adaptivt formulär {#editafsign}

Används [!DNL DocuSign] i en befintlig adaptiv form:

1. Navigera till **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.
1. Markera det adaptiva formuläret och välj **[!UICONTROL Properties]**.
1. I **[!UICONTROL Basic]** väljer du [konfigurationsbehållare](adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) skapad vid integrering [!DNL DocuSign] med [!DNL AEM Forms].
1. I **[!UICONTROL Form Model]** väljer du något av följande alternativ:

   - Om du har en anpassad formulärmall och kräver ett postdokument som är baserat på formulärmallen väljer du **[!UICONTROL Associate form template as the Document of Record template]** och välj en dokumentmall. När du använder alternativet visas endast de fält som är baserade på den associerade formulärmallen i de dokument som skickas för signering. Alla fält i det adaptiva formuläret visas inte.

   - Om du inte har någon anpassad formulärmall väljer du **[!UICONTROL Generate Document of Record]** alternativ. När du använder alternativet visas alla fält i det adaptiva formuläret i det dokument som skickas för signering.

1. Välj **[!UICONTROL Save & Close]**. Det adaptiva formuläret är aktiverat för [!DNL DocuSign]. Nu kan du lägga till [!DNL DocuSign] fält till formuläret och skicka det för signering.

1. Öppna det adaptiva formuläret i redigeringsläge. I **[!UICONTROL Content]** väljer du **[!UICONTROL Form Container]** och markera ![Konfigurera](assets/configure-icon.svg).

1. I **[!UICONTROL Submission]** avsnitt, markera **[!UICONTROL Submit with DocuSign electronic signatures]** från **[!UICONTROL Submit Action]** listruta.

1. I **[!UICONTROL Action Configuration]** avsnitt, markera **[!UICONTROL Add]** om du vill lägga till en mottagare och ange mottagarens e-postadress. Välj **[!UICONTROL Add]** igen om du vill lägga till fler mottagare.

1. Ange ämnet för e-postmeddelandet i **[!UICONTROL Email Subject]** fält. Välj **Inkludera bifogade filer** om du vill inkludera bilagor i e-postmeddelandet.

1. Välj ![Spara](assets/save_icon.svg) för att spara egenskaperna.
