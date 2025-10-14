---
title: Versionsinformation för version 2023.8.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
description: Versionsinformation för version 2023.8.0 av  [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: a0ffa6cf-64ae-468c-93f4-ac6805ef907e
feature: Release Information
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1691'
ht-degree: 0%

---

# Versionsinformation 2023.8.0 för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för funktionen för 2023.8.0-versionen av [!DNL Experience Manager] as a Cloud Service.

## Releasedatum {#release-date}

Releasedatum för [!DNL Adobe Experience Manager] som aktuell funktionsrelease för [!DNL Cloud Service] (2023.8.0) är 31 augusti 2023. Nästa funktionsrelease (2023.9.0) planeras till 28 september 2023.

## Släpp video {#release-video}

Titta på videon Versionsöversikt från augusti 2023 om du vill se en sammanfattning av funktioner som lagts till i version 2023.8.0:

>[!VIDEO](https://video.tv.adobe.com/v/3423535/?quality=12)

## [!DNL Experience Manager Sites] som en [!DNL Cloud Service] {#sites}

### Nya funktioner i [!DNL Experience Manager Sites] {#sites-features}

* Med konsolen [Innehållsfragment](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html?lang=sv-SE) kan användare nu visa taggar och söka efter taggar som används som metadata i innehållsfragment. Användare behöver inte längre växla till Assets-gränssnittet för den här funktionen, vilket minskar behovet av sammanhangsväxling och förbättrar effektiviteten.

  ![Taggning i konsolen för innehållsfragment](/help/assets/content-fragments-console-tags.png)
* Den nya Content Fragment Editor är nu tillgänglig i AEM as a Cloud Service. Det ger innehållsförfattarna möjlighet att bli produktivare genom att effektivisera sina redigeringsuppgifter och minska behovet av att växla mellan olika program samtidigt som de redigerar innehåll.
  ![Ny redigerare för innehållsfragment](/help/release-notes/assets/newCFEditor.png)

Den nya redigeraren för innehållsfragment har följande fördelar som inte är tillgängliga i den ursprungliga redigeraren:
* Spara automatiskt för effektivare redigering och för att förhindra oavsiktliga redigeringsförluster.
* Hierarkisk vy av ett innehållsfragment och dess referenser med hjälp av strukturträdet för snabb navigering i ett djupt strukturerat fragment.
  ![Strukturträd i redigeraren för innehållsfragment](/help/release-notes/assets/newCFEditor_StructureTree.png)

* Inline-överföring av resurser som innehållsreferenser utan att först behöva överföra dem till resursens DAM
* Ad hoc-förhandsgranskning av den renderade upplevelsen som levereras av innehållsfragmentet för att hjälpa författare att visualisera utseendet och känslan för innehållet i klientappen
* Publicera och avpublicera innehållsfragmentet med ett klick från redigeraren
* Visa och navigera till språkkopior när du redigerar ett innehållsfragment
  ![Språkkopior i Content Fragment Editor](/help/release-notes/assets/newCFEditor_LanguageCopies.PNG)

* Visa versioner för att hjälpa till att hålla reda på tidslinjen för ett innehållsfragment

  ![Versioner i Content Fragment Editor](/help/release-notes/assets/newCFEditor_Versionhistory.PNG)

* Visa överordnade referenser som hjälper författare att förstå effekten av sina redigeringar

  ![Överordnade referenser i redigeraren för innehållsfragment](/help/release-notes/assets/newCFEditor_Parentreferences.PNG)

## [!DNL Experience Manager Assets] som en [!DNL Cloud Service] {#assets}

### Nya funktioner i vyn Assets {#assets-view-features}

<!--

**Assign metadata form to a folder**

You can now assign metadata form to a specific folder within your Assets Essentials deployment. All assets in the folder, including assets in the sub-folders, then display properties defined in the assigned metadata form.

![assign metadata form to a folder](/help/release-notes/assets/assign-to-folder.png)

-->

* **Massimportera resurser från datakällor**: Administratörer kan nu [importera ett stort antal resurser](/help/assets/bulk-import-assets-view.md) från en datakälla till AEM Assets. Administratörerna behöver inte längre överföra enskilda resurser eller mappar till AEM Assets. De datakällor som stöds för bulkimport är bland annat Azure, AWS, Google Cloud och Dropbox.

  ![Massimportera resurser från en datakälla](/help/release-notes/assets/bulk-import.png)

* **Bildredigeringsverktyg som bygger på Adobe Express**: Enkla och intuitiva [bildredigeringsverktyg som bygger på Adobe Express](/help/assets/edit-images-assets-view.md) finns tillgängliga direkt i AEM Assets för att öka återanvändningen av innehåll och snabba upp hastigheten.

  ![Bildredigering med Adobe Express](/help/release-notes/assets/edit-adobe-express.png)

* **Flexibilitet vid fästning av objekt för Min Workspace snabbåtkomst**: Möjlighet att markera och fästa objekt åt dig, för hela organisationen eller för en lista över grupper så att de visas i [snabbåtkomstavsnittet i Min Workspace](/help/assets/my-workspace-assets-view.md) baserat på ditt val.

  ![Fäst objekt för grupper](/help/release-notes/assets/pin-items-for-groups.png)

### Nya funktioner i administrationsvyn {#admin-view-features}

**Sökförbättringar**

* Administratörer kan nu [konfigurera gruppstorleken för resurser](/help/assets/search-assets.md#configure-asset-batch-size) som visas när du utför en sökning. Resurssökresultaten visas i multipler av det konfigurerade batchstorleksnumret när du rullar nedåt för att läsa in resultaten. Du kan välja mellan de tillgängliga gruppstorlekarna 200, 500 och 1 000 resurser. Om du anger ett lägre batchstorleksnummer blir sökningen snabbare.

  ![Assets batchstorlekskonfiguration](/help/release-notes/assets/assets-batch-size-configuration.png)

* Experience Manager Assets innehåller nu en ny version 9 av `damAssetLucene`-indexet. `damAssetLucene-9` ändrar beteendet för Oak Query facet-inventering till [utvärderar inte längre åtkomstkontrollen för antalet facet](/help/assets/search-assets.md) som returneras av det underliggande sökindexet, vilket ger snabbare svarstider vid sökning.

### Förhandsutgåvor av funktioner som är tillgängliga i [!DNL Experience Manager Assets] {#prerelease-features-assets}

* **Dynamic Media**: [Stöd för flera bildtexter och flerljudspår för videofilmer i Dynamic Media](/help/assets/dynamic-media/video.md#about-msma) - Nu kan du enkelt lägga till flera bildtexter och flera ljudspår i en primär video. Detta innebär att videoklippen är tillgängliga för alla mottagare världen över. Du kan anpassa en enda publicerad primär video till en global publik på flera språk och följa riktlinjer för tillgänglighet för olika geografiska regioner. Författare kan också hantera beskrivningar och ljudspår från en enda flik i användargränssnittet.

  ![Fliken Bildtexter och ljudspår på egenskapssidan för en vald videoresurs.](/help/release-notes/assets/msma-aem-cs.png)*Fliken Bildtexter och ljudspår på egenskapssidan för en vald videoresurs.*

* **Assets**: Möjlighet att välja ZIP-arkiv som hanteras i Experience Manager och [att extrahera filerna direkt till Experience Manager](/help/assets/manage-digital-assets.md#extract-zip-archives) utan att hämta dem.

  ![Fäst objekt för grupper](/help/release-notes/assets/extract-archive.png)


## [!DNL Experience Manager Forms] som en [!DNL Cloud Service] {#forms}

### Nya funktioner tillgängliga i [!DNL Forms] {#new-features-available-in-forms-channel}

* [**Företagssupport för Google reCAPTCHA**](/help/forms/captcha-adaptive-forms.md): Använd Google reCAPTCHA Enterprise i en adaptiv form för att ge förbättrat skydd mot bedräglig aktivitet och skräppost, vilket ger en säkrare användarupplevelse. Med avancerad riskanalys och smidig integrering kan äkta användare enkelt skicka in formulär medan bots blockeras effektivt.


### Förhandsutgåvor av funktioner som är tillgängliga i [!DNL Forms] {#pre-release-features-available-in-forms-channel}

* **Adobe Analytics med Experience Cloud Setup Automation för Forms**: Nu kan du aktivera Adobe Analytics med Experience Cloud Setup Automation (Installationsautomatisering för) med ett par knappar. Det gör att ni kan koppla AEM Forms as a Cloud Service till Experience Platform-taggar och Adobe Analytics för att hämta in och spåra prestandamått för era publicerade formulär.

* **Adobe Analytics rapportmall för Adaptiv Forms**: Forms as a Cloud Service tillhandahåller nu en Adobe Analytics-rapport om OOTB. Det hjälper er att förstå hur era formulär fungerar. Med hjälp av formulärnivåstatistik får du insikt i hur formuläret fungerar med flera nyckeltal (KPI) som återgivningar, besökare, inskickat material, genomsnittlig fyllnadstid. Genom att följa upp användarbeteenden och feedback kan du identifiera områden i formuläret som orsakar förvirring och vägleda förbättringar av formulärets design och funktion.

  ![Analysrapport om användarinteraktion med adaptiva formulär](/help/forms/assets/forms-analytics-report.png)

* **[Formulärfragment i adaptiv Forms baserat på kärnkomponenter](/help/forms/adaptive-form-fragments-core-components.md)**: Slipp dupliceringen, optimera det digitala lagret och förbättra samarbetet när du skapar formulär med formulärfragment. Dessa återanvändbara komponenter kan smidigt integreras i flera formulär, vilket effektiviserar skapandet av enhetliga och proffsiga formulär. Form Fragments säkerställer återanvändbarhet, standardisering och enhetlig varumärkesexponering genom funktionen&quot;change once and mirror everywhere&quot;. Upplev bättre underhålls- och effektivitetsvinster i takt med att uppdateringar som görs på ett och samma ställe sprids automatiskt i alla formulär som använder dessa fragment.

* **[Förbättrat Adobe Sign Workflow-steg](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)**: Adobe Sign Workflow-steget har förbättrats och inkluderar följande:
   * **Myndighets-ID-baserad autentisering för Adobe Sign**: Adobe Acrobat Sign myndighets-ID-baserad autentisering erbjuder ytterligare ett verifieringslager genom att göra det möjligt för användare att autentisera sin identitet med hjälp av myndighetsutfärdade ID:n (körkort, nationellt ID, pass). Genom att använda pålitliga identifieringsdokument ger den här förbättringen ytterligare tillförlitlighet i signeringsprocessen, vilket gör den idealisk för scenarier som kräver högre säkerhet, regelefterlevnad och användarvalidering.

   * **Granskningsspårning för Adobe Sign-dokument**: Använd funktionen Granskningsspårning för att få detaljerade insikter om livscykeln för dina Adobe Sign-dokument. Med granskningsspåret kan du nu föra ett omfattande register över alla åtgärder och interaktioner som rör dina dokument. Detta inkluderar information som vem som visade, redigerade eller signerade dokumentet, tillsammans med tidsstämplar för varje händelse. Den här förbättringen är avgörande för att upprätthålla regelefterlevnaden, lösa tvister och säkerställa integriteten för dina digitala avtal.

   * **Nya roller för avtalsmottagare utöver bara signeraren**: Adobe Acrobat Sign har möjlighet att expandera rollerna för avtalsmottagare utöver bara signeraren för att bättre matcha deras arbetsflödesbehov. När det här alternativet är aktiverat kan varje mottagare i ett avtal konfigureras individuellt, med signerare som standard.

* **[Protect dina dokument med API:er för Document Assurance (del av kommunikations-API:er)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: Med API:erna för Document Assurance kan du skydda känslig information genom att signera och kryptera dokumenten. Genom kryptering omvandlas innehållet i ett dokument till ett oläsligt format så att bara behöriga användare kan få åtkomst till det. Detta förstärkta skydd skyddar inte bara värdefulla data från obehöriga ögon, utan ger även sinnesro. Med signatur-API:erna kan din organisation skydda säkerheten och sekretessen för Adobe PDF-dokument som den distribuerar och tar emot. Den här tjänsten använder digitala signaturer och certifiering för att säkerställa att endast avsedda mottagare kan ändra dokument.

* **Stöd för sidantal i kommunikations-API:er**: Nu kan du, tillsammans med att hämta ditt dokument via kommunikations-API:erna, även få värdefull information om antalet sidor i dokumentet.

* **[Felhantering med anpassade felhanterare i regelredigeraren](/help/forms/add-custom-error-handler-adaptive-forms-core-components.md)**: Du kan nu anropa en anpassad funktion som svar på ett fel som returnerats av en extern tjänst och ge ett skräddarsytt svar till slutanvändarna. Du kan till exempel anropa ett anpassat arbetsflöde i serverdelen för specifika felkoder eller informera kunden om att tjänsten inte fungerar.


### Headless Adaptive Forms early adopter {#forms-early-adopter}

Använd [Headless Adaptive Forms](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html?lang=sv-SE) om du vill att utvecklarna ska kunna skapa, publicera och hantera interaktiva formulär som kan nås och interagera med via API:er, i stället för via ett traditionellt grafiskt användargränssnitt. Headless adaptive forms help you:

* bygga högkvalitativa flerkanalsformulär på valfritt programmeringsspråk
* integrera formulär direkt i era datorprogram och mobilappar, webbplatser och chattapplikationer
* återanvända era egna gränssnittskomponenter med blankettapplikationer
* använder kraften i Adobe Experience Manager Forms

Du kan skicka ett e-postmeddelande till `aem-forms-headless@adobe.com` från ditt officiella e-post-ID för att gå med i det tidiga adopterprogrammet.


## [!DNL Experience Manager] som en [!DNL Cloud Service]-grund {#foundation}

### CDN-loggar {#cdn-logs}

Ladda ned CDN-loggar från Cloud Manager, vilket är användbart för optimering av täckningsgrad och större insyn i leveransflödet. [Läs mer om &#x200B;](/help/implementing/developing/introduction/logging.md#cdn-log) CDN-loggformatet. Den här funktionen lanseras gradvis för kunderna i början av september.

### CDN och WAF Rules early adopter program {#waf-early-adopter}

Filtrera trafiken vid CDN baserat på:

* begäranrubriker och egenskaper (t.ex. IP-adress)
* trafikmönster som man vet är associerade med skadlig trafik

Är du intresserad av att testa funktionen och ge feedback? Skicka ett e-postmeddelande till **aemcs-waf-adopter@adobe.com** från ditt officiella e-post-ID om du vill veta mer om det tidiga adopterprogrammet. Utrymmet är begränsat.

Läs mer om funktionen i artikeln [här](/help/security/traffic-filter-rules-including-waf.md).


## Versionsinformation om underhåll {#maintenance}

Du hittar den senaste underhållsversionsinformationen [här](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månadsutgåvor av Cloud Manager [här](/help/implementing/cloud-manager/release-notes/current.md).

## Migreringsverktyg {#migration-tools}

Du hittar en fullständig lista över migreringsverktygen [här](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
