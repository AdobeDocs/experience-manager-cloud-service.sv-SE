---
title: Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: a635a727e431a73086a860249e4f42d297882298
workflow-type: tm+mt
source-wordcount: '1750'
ht-degree: 0%

---

# Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service {#release-notes}

I följande avsnitt beskrivs versionsinformationen för den aktuella (senaste) versionen av [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Härifrån kan du navigera till versionsinformation för tidigare versioner som 2021 eller 2022.
>
>Ta en titt på [Roadmap för lanseringar av Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html) om de kommande funktionsaktiviteterna för [!DNL Experience Manager] as a Cloud Service.

>[!NOTE]
>
>Se [Senaste dokumentationsuppdateringar](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/doc-updates/documentation-updates.html) för information om dokumentationsuppdateringar som inte är direkt relaterade till en release.

## Releasedatum {#release-date}

Utgivningsdatumet [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell version (2023.8.0) är 31 augusti 2023. Nästa funktionsrelease (2023.9.0) planeras till 28 september 2023.

## Släpp video {#release-video}

Titta på videon Versionsöversikt från augusti 2023 om du vill se en sammanfattning av funktioner som lagts till i version 2023.8.0:

>[!VIDEO](https://video.tv.adobe.com/v/3423535/?quality=12)

## [!DNL Experience Manager Sites] som [!DNL Cloud Service] {#sites}

### Nya funktioner i [!DNL Experience Manager Sites] {#sites-features}

* The [Konsol för innehållsfragment](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html?lang=en) Nu kan användare visa taggar och söka efter taggar som används som metadata i innehållsfragment. Användarna behöver inte längre växla till Assets UI för den här funktionen, vilket minskar behovet av sammanhangsväxling och förbättrar effektiviteten.

  ![Tagga i konsolen för innehållsfragment](/help/assets/content-fragments-console-tags.png)
* Den nya redigeraren för innehållsfragment är nu tillgänglig på AEM as a Cloud Service. Det ger innehållsförfattarna möjlighet att bli produktivare genom att effektivisera sina redigeringsuppgifter och minska behovet av att växla mellan olika program samtidigt som de redigerar innehåll.
  ![Ny redigerare för innehållsfragment](/help/release-notes/assets/newCFEditor.png)

Den nya redigeraren för innehållsfragment har följande fördelar som inte är tillgängliga i den ursprungliga redigeraren:
* Spara automatiskt för effektivare redigering och för att förhindra oavsiktliga redigeringsförluster.
* Hierarkisk vy av ett innehållsfragment och dess referenser med hjälp av strukturträdet för snabb navigering i ett djupt strukturerat fragment.
  ![Strukturträd i innehållsfragmentredigeraren](/help/release-notes/assets/newCFEditor_StructureTree.png)

* Inline-överföring av resurser som innehållsreferenser utan att först behöva överföra dem till resursens DAM
* Ad hoc-förhandsgranskning av den renderade upplevelsen som levereras av innehållsfragmentet för att hjälpa författare att visualisera utseendet och känslan för innehållet i klientappen
* Publicera och avpublicera innehållsfragmentet med ett klick från redigeraren
* Visa och navigera till språkkopior när du redigerar ett innehållsfragment
  ![Språkkopior i Content Fragment Editor](/help/release-notes/assets/newCFEditor_LanguageCopies.PNG)

* Visa versioner för att hjälpa till att hålla reda på tidslinjen för ett innehållsfragment

  ![Versioner i Content Fragment Editor](/help/release-notes/assets/newCFEditor_Versionhistory.PNG)

* Visa överordnade referenser som hjälper författare att förstå effekten av sina redigeringar

  ![Överordnade referenser i Content Fragment Editor](/help/release-notes/assets/newCFEditor_Parentreferences.PNG)

## [!DNL Experience Manager Assets] som [!DNL Cloud Service] {#assets}

### Nya funktioner i resursvyn {#assets-view-features}

<!--

**Assign metadata form to a folder**

You can now assign metadata form to a specific folder within your Assets Essentials deployment. All assets in the folder, including assets in the sub-folders, then display properties defined in the assigned metadata form.

![assign metadata form to a folder](/help/release-notes/assets/assign-to-folder.png)

-->

* **Massimportera resurser från datakällor**: Administratörer har nu [möjlighet att importera ett stort antal resurser](/help/assets/bulk-import-assets-view.md) från en datakälla till AEM Assets. Administratörerna behöver inte längre överföra enskilda resurser eller mappar till AEM Assets. De datakällor som stöds för bulkimport är bland annat Azure, AWS, Google Cloud och Dropbox.

  ![Massimportera resurser från en datakälla](/help/release-notes/assets/bulk-import.png)

* **Bildredigeringsverktyg som bygger på Adobe Express**: Enkelt och intuitivt [bildredigeringsverktyg som bygger på Adobe Express](/help/assets/edit-images-assets-view.md) som finns direkt i AEM Assets för att öka återanvändningen av innehåll och snabba upp innehållets hastighet.

  ![Bildredigering med Adobe Express](/help/release-notes/assets/edit-adobe-express.png)

* **Flexibilitet vid fästning av objekt för snabb åtkomst till arbetsytan**: Möjlighet att markera och fästa objekt åt dig, för hela organisationen eller för en lista över grupper så att de visas i [Snabb åtkomst till delen Min arbetsyta](/help/assets/my-workspace-assets-view.md) baserat på ditt val.

  ![Fäst objekt för grupper](/help/release-notes/assets/pin-items-for-groups.png)

### Nya funktioner i administrationsvyn {#admin-view-features}

**Förbättrade sökfunktioner**

* Administratörer kan nu [konfigurera batchstorleken för resurser](/help/assets/search-assets.md#configure-asset-batch-size) som visas när du utför en sökning. Resurssökresultaten visas i multipler av det konfigurerade batchstorleksnumret när du rullar nedåt för att läsa in resultaten. Du kan välja mellan de tillgängliga gruppstorlekarna 200, 500 och 1 000 resurser. Om du anger ett lägre batchstorleksnummer blir sökningen snabbare.

  ![Konfiguration av batchstorlek för resurser](/help/release-notes/assets/assets-batch-size-configuration.png)

* Experience Manager Assets har nu en ny version 9 av `damAssetLucene` index. `damAssetLucene-9` ändrar beteendet för beräkning av Oak Query-faktor till [inte längre utvärdera åtkomstkontroll för antalet fakturor](/help/assets/search-assets.md) returneras av det underliggande sökindexet, vilket ger snabbare svarstider.

### Förhandsversioner av funktioner som finns i [!DNL Experience Manager Assets] {#prerelease-features-assets}

* **Dynamic Media**: [Stöd för flera undertexter och flerljudspår för videor i Dynamic Media](/help/assets/dynamic-media/video.md#about-msma)—Nu kan du enkelt lägga till flera undertexter och flera ljudspår i en primär video. Detta innebär att videoklippen är tillgängliga för alla mottagare världen över. Du kan anpassa en enda publicerad primär video till en global publik på flera språk och följa riktlinjer för tillgänglighet för olika geografiska regioner. Författare kan också hantera undertexter och ljudspår från en enda flik i användargränssnittet.

  ![Fliken Undertexter och Ljudspår på sidan Egenskaper för en vald videoresurs.](/help/release-notes/assets/msma-aem-cs.png)*Fliken Undertexter och Ljudspår på sidan Egenskaper för en vald videoresurs.*

* **Resurser**: Möjlighet att välja ZIP-arkiv som hanteras i Experience Manager och [extrahera filerna direkt i Experience Manager](/help/assets/manage-digital-assets.md#extract-zip-archives) utan att ladda ned dem.

  ![Fäst objekt för grupper](/help/release-notes/assets/extract-archive.png)


## [!DNL Experience Manager Forms] som [!DNL Cloud Service] {#forms}

### Nya funktioner i [!DNL Forms] {#new-features-available-in-forms-channel}

* [**Google reCAPTCHA - företagssupport**](/help/forms/captcha-adaptive-forms.md): Använd Google reCAPTCHA Enterprise i en adaptiv form för att få bättre skydd mot bedräglig aktivitet och skräppost, vilket ger en säkrare användarupplevelse. Med avancerad riskanalys och smidig integrering kan äkta användare enkelt skicka in formulär medan bots blockeras effektivt.


### Förhandsversioner av funktioner som finns i [!DNL Forms] {#pre-release-features-available-in-forms-channel}

* **Adobe Analytics med Experience Cloud Setup Automation för Forms**: Nu kan du aktivera Adobe Analytics med Experience Cloud Setup Automation (Automatisering av installationsprogram) med ett par knappar. Det gör att ni kan koppla AEM Forms as a Cloud Service till Experience Platform-taggar och Adobe Analytics för att hämta in och spåra prestandamått för era publicerade formulär.

* **Adobe Analytics rapportmall för Adaptiv Forms**: Forms as a Cloud Service tillhandahåller nu en Adobe Analytics-rapport, OOTB. Det hjälper er att förstå hur era formulär fungerar. Med hjälp av formulärnivåstatistik får du insikt i hur formuläret fungerar med flera nyckeltal (KPI) som återgivningar, besökare, inskickat material, genomsnittlig fyllnadstid. Genom att följa upp användarbeteenden och feedback kan du identifiera områden i formuläret som orsakar förvirring och vägleda förbättringar av formulärets design och funktion.

  ![Analysrapport om användarinteraktion med adaptiva formulär](/help/forms/assets/forms-analytics-report.png)

* **[Form Fragment in Adaptive Forms based on Core Components](/help/forms/adaptive-form-fragments-core-components.md)**: Ta farväl av dubbelarbete, optimera det digitala arkivet och förbättra samarbetet när ni utökar upplevelsen av formulärgenereringen med formulärfragment. Dessa återanvändbara komponenter kan smidigt integreras i flera formulär, vilket effektiviserar skapandet av enhetliga och proffsiga formulär. Form Fragments säkerställer återanvändbarhet, standardisering och enhetlig varumärkesexponering genom funktionen&quot;change once and mirror everywhere&quot;. Upplev bättre underhålls- och effektivitetsvinster i takt med att uppdateringar som görs på ett och samma ställe sprids automatiskt i alla formulär som använder dessa fragment.

* **[Förbättrat arbetsflöde i Adobe Sign](/help/forms/aem-forms-workflow-step-reference.md#sign-document-step-sign-document-step)**: Adobe Sign Workflow-steget har förbättrats och innehåller följande:
   * **Myndighets-ID-baserad autentisering för Adobe Sign**: Adobe Acrobat Sign Government ID-Based Authentication erbjuder ytterligare ett verifieringslager genom att användarna kan autentisera sin identitet med hjälp av foto-ID:n (körkort, nationellt ID, pass). Genom att utnyttja pålitliga identifieringsdokument ger den här förbättringen ett extra förtroende för signeringsprocessen, vilket gör den idealisk för scenarier som kräver högre säkerhet, regelefterlevnad och användarvalidering.

   * **Granskningsspår för Adobe Sign-dokument**: Använd funktionen Granskningsspår för att få detaljerade insikter om livscykeln för dina Adobe Sign-dokument. Med granskningsspåret kan du nu föra ett omfattande register över alla åtgärder och interaktioner som rör dina dokument. Detta inkluderar information som vem som visade, redigerade eller signerade dokumentet, tillsammans med tidsstämplar för varje händelse. Den här förbättringen är avgörande för att upprätthålla regelefterlevnaden, lösa tvister och säkerställa integriteten för dina digitala avtal.

   * **Nya roller för avtalsmottagare utöver bara signeraren**: Adobe Acrobat Sign har möjlighet att utöka rollerna för avtalsmottagare utöver bara signeraren för att bättre matcha deras arbetsflödesbehov. När det här alternativet är aktiverat kan varje mottagare i ett avtal konfigureras individuellt, med signerare som standard.

* **[Protect dina dokument med Document Assurance API:er (del av kommunikations-API:er)](/help/forms/aem-forms-cloud-service-communications-introduction.md#document-assurance-doc-assurance)**: Med API:erna för Document Assurance kan du skydda känslig information genom att signera och kryptera dokumenten. Genom kryptering omvandlas innehållet i ett dokument till ett oläsligt format så att bara behöriga användare kan få åtkomst till det. Detta förstärkta skydd skyddar inte bara värdefulla data från obehöriga ögon, utan ger även sinnesro. Med signatur-API:erna kan din organisation skydda säkerheten och sekretessen för Adobe PDF-dokument som den distribuerar och tar emot. Den här tjänsten använder digitala signaturer och certifiering för att säkerställa att endast avsedda mottagare kan ändra dokument.

* **Stöd för sidantal i kommunikations-API:er**: Nu kan du, tillsammans med att hämta ditt dokument via kommunikations-API:erna, även få värdefull information om antalet sidor i dokumentet.

* **[Felhantering med anpassade felhanterare i regelredigeraren](/help/forms/add-custom-error-handler-adaptive-forms-core-components.md)**: Du kan nu anropa en anpassad funktion som svar på ett fel som returnerats av en extern tjänst och ge ett skräddarsytt svar till slutanvändarna. Du kan till exempel anropa ett anpassat arbetsflöde i serverdelen för specifika felkoder eller informera kunden om att tjänsten inte fungerar.


### Headless Adaptive Forms early adopter {#forms-early-adopter}

Använd [Headless Adaptive Forms](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) så att utvecklarna kan skapa, publicera och hantera interaktiva formulär som kan öppnas och interagera med via API:er, i stället för via ett traditionellt grafiskt användargränssnitt. Headless adaptive forms help you:

* bygga högkvalitativa flerkanalsformulär på valfritt programmeringsspråk
* integrera formulär direkt i era datorprogram och mobilappar, webbplatser och chattapplikationer
* återanvända era egna gränssnittskomponenter med blankettapplikationer
* använder kraften i Adobe Experience Manager Forms

Du kan skicka ett e-postmeddelande till `aem-forms-headless@adobe.com` från ditt officiella e-post-ID till att gå med i det tidiga adopterprogrammet.


## [!DNL Experience Manager] som [!DNL Cloud Service] Foundation {#foundation}

### CDN-loggar {#cdn-logs}

Ladda ned CDN-loggar från Cloud Manager, vilket är användbart för optimering av täckningsgrad för cache och större synlighet för innehållsleveransflödet. [Läs mer om](/help/implementing/developing/introduction/logging.md#cdn-log) CDN-loggformatet. Den här funktionen lanseras gradvis för kunderna i början av september.

### CDN och WAF Rules early adopter program {#waf-early-adopter}

Filtrera trafiken vid CDN baserat på:
* begäranrubriker och egenskaper (t.ex. IP-adress)
* trafikmönster som man vet är associerade med skadlig trafik

Är du intresserad av att testa funktionen och ge feedback? Skicka e-post till **aemcs-waf-adopter@adobe.com** från ditt officiella e-post-ID om du vill veta mer om programmet för tidig användning. Utrymmet är begränsat.

Läs mer om funktionen i artikeln [här](/help/security/cdn-and-waf-rules.md).


## Versionsinformation om underhåll {#maintenance}

Du kan hitta den senaste underhållsreleasenumerationen [här](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månatliga utgåvor av Cloud Manager [här](/help/implementing/cloud-manager/release-notes/current.md).

## Migreringsverktyg {#migration-tools}

Du hittar en fullständig lista över versioner av migreringsverktyg [här](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
