---
title: Vad har ändrats mellan AEM 6.5 Forms och AEM Cloud Services
description: 'Använder du Experience Manager Forms och vill uppgradera till Adobe Experience Manager Forms as a Cloud Service? Lär dig de mest framträdande förändringarna innan du uppgraderar eller migrerar till Cloud Servicen.  '
contentOwner: khsingh
exl-id: 46fcc1b4-8fd5-40e1-b0fc-d2bc9df3802e
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '1211'
ht-degree: 2%

---

# Betydande förändringar för befintliga Adobe Experience Manager Forms-användare  {#notable-changes-for-existing-AEM-Forms-users}

Adobe Experience Manager Forms as a Cloud Service förändrar de befintliga funktionerna avsevärt jämfört med Adobe Experience Manager FormsOn-Premise och [!DNL Adobe-Managed Service] miljöer. De viktigaste skillnaderna anges nedan:

* Tjänsten tillhandahåller en lokal och molnbaserad utvecklingsmiljö. Du kan använda en [lokal utvecklingsmiljö](setup-local-development-environment.md) för att utveckla och testa din egen kod, komponenter, mallar, teman, adaptiva Forms och andra resurser innan du distribuerar dessa resurser till en molnmiljö. Det snabbar upp utvecklingsprocessen.
* [!DNL AEM] när Cloud Servicen levereras med ett inbyggt CDN. Dess huvudsakliga syfte är att minska latensen genom att leverera tillgängligt innehåll från CDN-noder nära webbläsaren. Det är helt managerat och konfigurerat för optimal prestanda i AEM-program.
* En molnbaserad miljö har ingen webbkonsol (konfigurationshanterare). Du kan använda [[!DNL AEM Forms] as a Cloud Service SDK för att generera konfigurationer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#generating-osgi-configurations-using-the-aem-sdk-quickstart) och CI/CD-överföring till [distribuera konfigurationen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#deployment-process) till din Cloud Service.

* URL-konventionen för lokaliserade adaptiva Forms har nu stöd för att ange nationella inställningar i URL:en. Ny URL-konvention möjliggör cachelagring av lokaliserade formulär på en Dispatcher eller CDN. I Cloud Service-miljön använder du URL-formatet `http://host:port/content/forms/af/<afName>.<locale>.html` begära en lokaliserad version av ett adaptivt formulär i stället för `http://host:port/content/forms/af/afName.html?afAcceptLang=<locale>`. Adobe rekommenderar att du använder Dispatcher eller CDN-cachning. Det förbättrar återgivningshastigheten för förfyllda formulär.
* I förifyllningstjänsten sammanfogas data med ett adaptivt formulär på en klient. Det hjälper till att förbättra tiden som krävs för att förifylla ett adaptivt formulär. Du kan alltid konfigurera så att kopplingsåtgärden körs på Adobe Experience Manager FormsServer.
* E-poststöd är som standard bara för HTTP- och HTTP-protokoll. [Kontakta supportteamet](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#sending-email) för att aktivera portar för att skicka e-post och för att aktivera SMTP-protokoll för din miljö.
* Adobe Experience Manager Forms as a Cloud Service innehåller många nya funktioner och möjligheter i dina AEM projekt. Det krävs dock vissa förändringar i Adobe Experience Manager Maven-projekten för att de ska vara kompatibla med AEM Cloud Service. På en hög nivå kräver AEM att innehåll och kod skiljs åt i diskreta delpaket för att se skillnaden mellan muterbart och oföränderligt innehåll. Använd [Databasmodernisering](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/refactoring-tools/repo-modernizer.html) för att strukturera om befintliga projektpaket genom att separera innehåll och kod i separata paket som är kompatibla med den projektstruktur som har definierats för Adobe Experience Manager as a Cloud Service.

<!--  If your Cloud Configuration contains a secret (password), create a separate Cloud Configuration for every Author instance (Developer, Stage, and Production). If a Cloud Configuration is also required on Publish instances, publish/replicate a separate Cloud Configuration for every Publish instance (Developer, Stage, and Production). 

* When you create a Cloud Configuration that contains a secret, each Cloud Service instance (Developer, Stage, and Production) uses its own encryption key to encrypt the password before storing it. So, manually create such Cloud Configuration for every Cloud Service instance (Developer, Stage, and Production). Also, do not store secrets used in a Cloud Configuration to your Cloud Manager Git repository.

* Use [!DNL Cloud Manager] [APIs to convert and provide your passwords as secrets](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#setting-values-via-api). Do not store plain text password or secrets on your environments. -->

* Användning av miljöspecifika konfigurationer för hemliga OSGi-konfigurationsvärden, som lösenord, privata API-nycklar eller andra värden. Dessa kan inte lagras i Git av säkerhetsskäl. [Använd hemliga miljöspecifika konfigurationer för att lagra värdet för hemligheter i alla Adobe Experience Manager as a Cloud Service-miljöer, inklusive scenen och produktionen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/deploying/configuring-osgi.html?lang=en#when-to-use-secret-environment-specific-configuration-values).

En omfattande lista över förändringar i Adobe Experience Manager as a Cloud Service finns på [Vad är nytt och vad är annorlunda?](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/overview/what-is-new-and-different.html).

<!-- ## Feature comparison {#comparison}

[!DNL AEM Forms] as a Cloud Service and Experience Manager 6.5 Forms share a common set of features: Adaptive Forms, data integration, integration with [!DNL Adobe Sign], themes, templates, and forms management interface are identical. You can easily port your existing Adaptive Forms from an Experience Manager 6.5 Forms or an earlier version to [!DNL AEM Forms] as a Cloud Service.

### Features of AEM 6.5 Forms and [!DNL AEM Forms] as a Cloud Service {#feature-comparison}

The following table lists the major features of Experience Manager 6.5 Forms and provides information about whether the feature is partially or fully supported in [!DNL AEM Forms] as a Cloud Service, with a link to more information about the feature. The table also lists extra features available in [!DNL AEM Forms] as a Cloud Service.


| Feature/Capability | AEM 6.5 Forms | [!DNL AEM Forms] as a Cloud Service |
| - | - | - |
| Adaptive Forms | &#x2611; | &#x2611; |
| Data Integration | &#x2611; | &#x2611;(With some changes) |
| Automated Forms Conversion Service | &#x2611; | &#x2611; |
| Integration with Adobe Sign | &#x2611; | &#x2611;(With some changes) |
| Themes and Templates | &#x2611; | &#x2611; ([With some changes](themes.md#difference-in-themes))|
| Rule editor | &#x2611; | &#x2611; (With some changes) |
| Forms Portal | &#x2611; | --- |
| Integration with Adobe Analytics | &#x2611; | &#x2612; |
| Document Security | &#x2611; | &#x2612; | -->

<!-- ## New features {#comparison} -->



## Viktiga förbättringar {#whats-new}

<!-- [!DNL AEM Forms] as a Cloud Service offers benefits like auto-scaling, cost-effectiveness, zero downtime for upgrades, and cloud-native development environment and more. The list does not stop here. The following features are are start and are available only for [!DNL AEM Forms] as a Cloud Service: -->

Följande funktioner och förbättringar är endast tillgängliga på [!DNL AEM Forms] as a Cloud Service:

**Förbättrad redigerare för visuell regel**
Tjänsten ger en härdad [Visuell regelredigerare](rule-editor.md#visual-rule-editor). Tjänsten har lagt till följande funktioner i redigeraren för visuell regel som hjälper dig att skriva kapabla regler:

* [Nya inskickningshändelser](working-with-adobe-sign.md#available-operator-types-and-events-in-rule-editor): `Navigation`, `Step Completion`, `Successful Submission`och `Error`

* [Ny datatyp `scope`](rule-editor.md#custom-functions). Du kan använda `scope` datatypen i en anpassad funktion för att skicka hela omfånget för ett formulär.

* Möjlighet att använda [@this för att ange en JSDoc i en anpassad funktion](rule-editor.md#custom-functions). Den tillåter anrop av en anpassad funktion genom att använda @this i en aktiv komponent.

* Möjlighet att lägga till villkor för egenskapsbaserade regler.

**Kärnkomponenter**
The [Kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=en) är en uppsättning standardiserade WCM-komponenter (Web Content Management) för AEM som snabbar upp utvecklingstiden och minskar underhållskostnaderna. [!DNL AEM Forms] as a Cloud Service stöd **[!UICONTROL AEM Forms Container]** Kärnkomponent. Du kan använda komponenten för att bädda in ett adaptivt formulär på en AEM Sites-sida.

**AEM Archetype for Forms as a Cloud Service**
[AEM](https://github.com/adobe/aem-project-archetype/releases/tag/aem-project-archetype-27) hjälper dig att börja utveckla för [!DNL AEM Forms] as a Cloud Service. Du kan använda Arketype version 27 eller senare för att skapa en projektmall som är kompatibel med [!DNL AEM Forms] as a Cloud Service miljö. Arketypen innehåller även några exempelteman och mallar som hjälper dig att komma igång snabbt.

**Säkert och förbättrat informationsflöde mellan formulär och signering**
[Adaptiv integrering med Forms och Adobe Sign](working-with-adobe-sign.md) på Cloud Servicen ger samtidig inlämning av data och signeringsaktivitet. Det gör det möjligt att skicka in formulär oberoende av signeringsstatus, vilket gör det möjligt att skicka in formulär snabbare. Dessutom sparas inga data i Cloud Service som gör signeringsprocessen supersäker.

**Best Practices Analyzer och migreringsverktyg**
Best Practices Analyzer ger en bedömning av din nuvarande AEM. Kör verktyget före [migrera till Forms as a Cloud Service](migrate-to-forms-as-a-cloud-service.md). Här utvärderas beredskapen för att gå över från en befintlig Adobe Experience Manager (AEM)-distribution till AEM as a Cloud Service.

Tjänsten tillhandahåller även [förbättrad migreringsupplevelse](migrate-to-forms-as-a-cloud-service.md) för att du enkelt ska kunna migrera från [!DNL AEM 6.4 Forms] och [!DNL AEM 6.5 Forms] till [!DNL AEM Forms] as a Cloud Service.

**Snabbare formuläråtergivning och snabbare valideringar på serversidan**
Tjänsten använder CDN och Dispatcher-cachning för att leverera snabbare renderingar och serversidevalidering för Adaptive Forms.

**Förbättrad CAPTCHA**
Nu kan du [validera CAPTCHA](captcha-adaptive-forms.md) antingen när det gäller inlämning av anpassade blanketter eller affärslogik. Du kan också lägga till villkor för att validera CAPTCHA på en användaråtgärd och visa eller dölja CAPTCHA-komponenten i ett anpassat formulär baserat på regler.

CAPTCHA-komponenten har en färdig integrering med Google reCAPTCHA. Om det behövs kan du även konfigurera fler CAPTCHA-tjänster för komponenten.

**Flera överordnad sidor för arkivhandlingar**
Nu kan du använda olika överordnad sidor för varje sida i ett dokument och styra placeringen av en adaptiv formulärpanel i ett dokument med sidnumreringsalternativ.

**Lägg till kolumner i rubrikfria tabeller**
Du kan lägga till och ta bort kolumner i tabeller utan rubriker. Dolda rubriker läggs till i sådana tabeller så att du lättare kan lägga till och ta bort kolumner. Dessa rubriker visas vid redigering men döljs i det publicerade formuläret. Tabeller utan rubriker finns oftast i Adaptive Forms som skapats med tjänsten Automated forms conversion.

**Förbättrade Skicka-åtgärder**
Du kan använda [Skicka e-post](configuring-submit-actions.md#send-email#send-email) Skicka åtgärd för att skicka ett dokument med post (DoR) PDF som en bifogad fil.

**Gruppera e-post för arbetsflöde**
Du kan välja att [skicka e-postmeddelanden](aem-forms-workflow-step-reference.md#assign-task-step) från steget Tilldela uppgift till en person eller grupp.

**Förbättrat steg för Anropa formulärdatamodell**
Du kan nu ange sökvägen till mappen för alternativet Relativt till nyttolast för indatatjänstargumenten i steget Anropa formulärdatamodell. Det hjälper dig att mappa en fil som finns i den angivna mappen till tjänstargumentet utan att ange det exakta filnamnet.

**Förbättrad läsbarhet i översättningsfiler**
På Forms-as a Cloud Service har läsordningen för fälten och panelerna i ett adaptivt formulär och meddelandetangenterna för motsvarande översättningsfiler (.XLIFF-filer) en liknande struktur. Det förbättrar den manuella översättningshastigheten.

<!-- ## Feature comparison {#feature-comparison}

[!DNL AEM Forms] as a Cloud Service and [!DNL AEM 6.5 Forms] share some features like Adaptive Forms, Data Integration, and Forms Portal. You can easily port your existing Adaptive Forms from an [!DNL AEM 6.5 Forms] or an earlier version to [!DNL AEM Forms] as a Cloud Service.

### Features of [!DNL AEM 6.5 Forms] and [!DNL AEM Forms] as a Cloud Service {#aem-6.5-vs-aem-forms-as-a-cloud-service}

The following table lists the major features of [!DNL AEM 6.5 Forms] and provides information about the features coming soon to [!DNL AEM Forms] as a Cloud Service:

| Feature/Capability | AEM 6.5 Forms  | [!DNL AEM Forms] as a Cloud Service |
|---|---|---|
| Cloud-native architecture | &#x2612; | &#x2611;  |
| Auto-scaling based on load | &#x2612; | &#x2611;  |
| Zero downtime for upgrades | &#x2612; | &#x2611;  |
| Feature roll-out frequency | Quarterly | Agile*  |
| CDN (content delivery network) included | &#x2612; | &#x2611;  |
| Topologies optimized for maximum resilience and efficiency | &#x2612; | &#x2611;  |
| Cloud-native development environment | &#x2612; | &#x2611;  |
| Self-Service via Cloud Manager | &#x2612; | &#x2611;  |
| Automated upgrades with Continuous Integration and Continuous Delivery (CI/CD)| &#x2611; | &#x2611;  |
| Adaptive Forms | &#x2611; | &#x2611; |
| Data Integration | &#x2611; | &#x2611; |
| Automated Forms Conversion Service | &#x2611; | &#x2611; |
| Integration with [!DNL Adobe Sign] | &#x2611; | &#x2611; |
| Integration with [!DNL AEM Sites] | &#x2611; | &#x2611; |
| Enhanced Visual Rule editor | &#x2612; | &#x2611; |
| Forms Portal | &#x2611; | Coming Soon |
| Integration with [!DNL Adobe Analytics] | &#x2611; | Coming Soon |
| Integration with [!DNL Adobe Target] | &#x2611; | Coming Soon |
| Document Security | &#x2611; | &#x2612; |

`*` New features every month and bug fix updates on daily basis.

For a comprehensive list of changes in AEM as a Cloud Service, See [What is New and What is Different](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/overview/what-is-new-and-different.html) and [Notable changes in [!DNL AEM Forms] as a Cloud Service](notable-changes.md) -->
