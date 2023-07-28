---
title: Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell versionsinformation för [!DNL Adobe Experience Manager] as a Cloud Service.
mini-toc-levels: 1
exl-id: a2d56721-502c-4f4e-9b72-5ca790df75c5
source-git-commit: 5995c416328e6f340285004ec2e723cc9279dabd
workflow-type: tm+mt
source-wordcount: '935'
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

Utgivningsdatumet [!DNL Adobe Experience Manager] som [!DNL Cloud Service] aktuell version (2023.7.0) är 27 juli 2023. Nästa version (2023.8.0) är planerad till 31 augusti 2023.

## Släpp video {#release-video}

Titta på videon med versionsöversikten för juli 2023 om du vill se en sammanfattning av funktioner som lagts till i version 2023.7.0:

>[!VIDEO](https://video.tv.adobe.com/v/3422016/?quality=12)

## [!DNL Experience Manager Sites] som [!DNL Cloud Service] {#sites}

### Nya funktioner i [!DNL Experience Manager Sites] {#sites-features}

* MSM för innehållsfragment. AEM Multisite Manager är nu tillgängligt för innehållsfragment, vilket gör att du kan skapa Live-kopior för innehållsfragment för massdistribution av innehåll. Detaljerade arvskontroller är tillgängliga ned till nivån för innehållselement och variationer.

### Nya funktioner i [!DNL Experience Manager Sites] prerelease {#prerelease-sites}

* The [Konsol för innehållsfragment](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/content-fragments/content-fragments-console.html?lang=en) Nu kan användare visa taggar och söka efter taggar som används som metadata i innehållsfragment. Användarna behöver inte längre växla till Assets UI för den här funktionen, vilket minskar behovet av sammanhangsväxling och förbättrar effektiviteten.

![Tagga i konsolen för innehållsfragment](/help/assets/content-fragments-console-tags.png)

## [!DNL Experience Manager Assets] som [!DNL Cloud Service] {#assets}

### Nya funktioner i resursvyn {#assets-view-features}

<!--

**Assign metadata form to a folder**

You can now assign metadata form to a specific folder within your Assets Essentials deployment. All assets in the folder, including assets in the sub-folders, then display properties defined in the assigned metadata form.

![assign metadata form to a folder](/help/release-notes/assets/assign-to-folder.png)

-->

**Förbättrat ramverk för artificiell intelligens för smarta taggar i bilder**

Experience Manager Assets använder nu ett förbättrat ramverk för artificiell intelligens för smarta taggar i bilder. Den här innehållsintelligensen ger bättre relevans och precision för smarta taggar som är tillgängliga för alla bildresurser vid förtäring.

**Konfigurera visning av kolumner för resurslista-vyn**

Nu kan du i Assets Essentials välja vilka kolumner som ska visas i resurslista, till exempel Status, Format, Dimensioner, Storlek.

![Konfigurera kolumner](/help/release-notes/assets/configure-columns.png)

**Sortera sökresultat baserat på relevans**

Assets Essentials sorterar nu sökresultaten baserat på relevans som standard. Du kan sortera de sökda resurserna i stigande eller fallande ordning efter `Name`, `Relevance`, `Size`, `Modified`och `Created`.


## [!DNL Experience Manager Forms] som [!DNL Cloud Service] {#forms}

### Nya funktioner i [!DNL Forms] {#new-features-available-in-forms-channel}

* [**Färdiga teman**](/help/forms/using-themes-in-core-components.md) **och mallar**: Kom igång snabbt med processen för att skapa formulär med våra färdiga OOTB-teman och mallar som är skräddarsydda för både erfarna proffs och nya formulärförfattare. Dessa välstrukturerade teman och mallar är sömlöst byggda med adaptiva Forms Core-komponenter och gör att du snabbt kan börja skapa formulär för vanliga användningsområden.

  ![Körklara mallar](/help/forms/assets/form-templates-ootb.png)

* **Reaktionskomponenter för Headless Forms**: Nu kan du förhandsgranska och anpassa Headless Adaptive Form-renderingar med React-komponenterna som medföljer. Dessa komponenter utnyttjar BEM-klasser från adaptiva Forms Core-komponenter för formatering, vilket gör det enkelt för dig att anpassa deras utseende efter dina specifika krav.

* [**Skapa adaptiv Forms med repeterbara avsnitt**](/help/forms/create-forms-repeatable-sections.md): Nu kan du [Dragspel](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/accordion.html), [guide](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/wizard.html), [Panel](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/panel-container.html)och [Vågräta flikar](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/horizontal-tabs.html) komponentbaserad Adaptiv form repeterbar för inspelning av flera dataposter.  Dessa upprepningsbara avsnitt gör att du enkelt kan ange flera datainmatningar. Det är användbart när de nödvändiga instanserna av data är okända i förväg. En formuläranvändare kan enkelt lägga till eller ta bort avsnitt, göra formulären anpassningsbara till olika datainmatningsscenarier och förenkla insamlingen av flera förekomster av samma datapost.


### Förhandsversioner av funktioner som finns i [!DNL Forms] {#pre-release-features-available-in-forms-channel}

* [**Google reCAPTCHA - företagssupport**](/help/forms/captcha-adaptive-forms.md): Använd Google reCAPTCHA Enterprise i en adaptiv form för att få bättre skydd mot bedräglig aktivitet och skräppost, vilket ger en säkrare användarupplevelse. Med avancerad riskanalys och smidig integrering kan äkta användare enkelt skicka in formulär medan bots blockeras effektivt.

  >[!VIDEO](https://video.tv.adobe.com/v/3422097/adaptive-forms-recaptcha-core-components-captcha/?quality=12&learn=on)

### Headless Adaptive Forms early adopter {#forms-early-adopter}

Använd [Headless Adaptive Forms](https://experienceleague.adobe.com/docs/experience-manager-headless-adaptive-forms/using/overview.html) så att utvecklarna kan skapa, publicera och hantera interaktiva formulär som kan öppnas och interagera med via API:er, i stället för via ett traditionellt grafiskt användargränssnitt. Headless adaptive forms help you:

* bygga högkvalitativa flerkanalsformulär på valfritt programmeringsspråk
* integrera formulär direkt i era datorprogram och mobilappar, webbplatser och chattapplikationer
* återanvända era egna gränssnittskomponenter med blankettapplikationer
* använder kraften i Adobe Experience Manager Forms

Du kan skicka ett e-postmeddelande till `aem-forms-headless@adobe.com` från ditt officiella e-post-ID till att gå med i det tidiga adopterprogrammet.

## [!DNL Experience Manager] som [!DNL Cloud Service] Foundation {#foundation}

### Actions Center {#actions-center}

Prenumerera på e-postmeddelanden som varnar dig när allvarliga incidenter inträffar och som kräver omedelbara åtgärder, och även med personaliserade rekommendationer för att optimera webbplatsen. [Actions Center](/help/operations/actions-center.md) fungerar som ett nav där du kan granska dessa varningar, t.ex. blockerade replikeringsköer eller utgångna autentiseringsuppgifter, och markera dem som lösta.

![Actions Center, bild](/help/assets/assets/actions-center.png)

### CDN och WAF Rules early adopter program {#waf-early-adopter}

Filtrera trafiken vid CDN baserat på:
* begäranrubriker och egenskaper (t.ex. IP-adress)
* trafikmönster som man vet är associerade med skadlig trafik

Är du intresserad av att testa funktionen och ge feedback? Skicka e-post till **aemcs-waf-adopter@adobe.com** från ditt officiella e-post-ID om du vill veta mer om programmet för tidig användning. Utrymmet är begränsat.

Läs mer om funktionen i artikeln [här](/help/security/cdn-and-waf-rules.md).

### Andra Foundation-ändringar {#other-foundation-changes}

* Under veckan 7 augusti returnerar AEM felkod 429 i stället för felkod 503 när begäranden om att AEM instanser överskrider en felfri nivå. [Läs mer](/help/implementing/developing/introduction/development-guidelines.md).

## Versionsinformation om underhåll {#maintenance}

Du kan hitta den senaste underhållsreleasenumerationen [här](/help/release-notes/maintenance/latest.md).

## Cloud Manager {#cloud-manager}

Du hittar en fullständig lista över månatliga utgåvor av Cloud Manager [här](/help/implementing/cloud-manager/release-notes/current.md).

## Migreringsverktyg {#migration-tools}

Du hittar en fullständig lista över versioner av migreringsverktyg [här](/help/journey-migration/release-notes/release-notes-migration-tools-current.md).
