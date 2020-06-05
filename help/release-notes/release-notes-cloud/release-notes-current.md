---
title: Versionsinformation om Adobe Experience Manager som molntjänst för 2020.6.0
description: Versionsinformation om Experience Manager för 2020.6.0
translation-type: tm+mt
source-git-commit: c5ee964fad3e1430e7c08f0cca76aecfae8bd44f
workflow-type: tm+mt
source-wordcount: '1808'
ht-degree: 0%

---


# Versionsinformation för AEM som molntjänst 2020.6.0 {#release-notes}

I följande avsnitt beskrivs den allmänna versionsinformationen för Experience Manager som en molntjänst 2020.6.0.

## Releasedatum {#release-date}

Releasedatum för [!DNL Experience Manager] som molntjänst 2020.6.0 är 4 juni 2020.

## Nyheter i AEM Sites {#aem-sites}

Följ det här avsnittet för att lära dig mer om nyheter och uppdateringar för AEM Sites i AEM som en Cloud Service Release 2020.6.0.

### What&#39;s New {#whats-new-2020.6.0}

Version 2.9.0 av [Core Components](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) finns nu som en del av AEM Sites som inkluderar:

* Integrering mellan [Adobe Client Data Layer](https://github.com/adobe/adobe-client-data-layer) och Core Components
* Konfigurerbara HTML ID-attribut för alla komponenter
* En ny Progress Bar-komponent
* Många felkorrigeringar

### Bug Fixes {#sites-bug-fixes}

* Komponenter i layoutbehållaren visas inte när layoutbehållaren kopieras och klistras in igen på en sida.

* Korrigerat problem med storleksändring av layoutkomponent.

* Lagt till möjlighet att hantera sidor med enbart routningsvinkel och sidor med AEM/vinkeler.

### Tillgänglighet {#accessibility}

* Nu går det att lägga till berättarroller och status för huvudobjekten i dialogrutan **Skapa sida** när du navigerar i bläddringsläget med hjälp av nedpilen.

* En länk i navigeringen har lagts till så att användare kan hoppa över huvudinnehållet.

* Förbättrad skärmläsare.


## Nyheter i Foundations i AEM som molntjänst {#foundations}

AEM-projektens byggtider förbättras genom att alla referenser i AEM-projektets pom.xml tas bort från fjärrdatabasen `https://downloads.experiencecloud.adobe.com/content/maven/public`.

AEM som API Jar för molntjänster, SDK, som tidigare fanns på den platsen, finns nu i Maven Central, som är Maven standardarkiv för artefakter.

## Nyheter i Cloud Manager {#cloud-manager}

Följ det här avsnittet för att lära dig mer om vad som är nytt och uppdateringarna för Cloud Manager i AEM som en molntjänst 2020.6.0.

### What&#39;s New {#what-is-new-cloud-manager}

* En användare i rollen *Business Owner* i Cloud Manager kan nu ta bort ett sandlådeprogram från landningssidan (via snabbåtgärdsknappen på programkortet) eller inifrån programmet.

   Mer information finns i [Ta bort ett sandlådeprogram](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html) .

* En sandlådeprogramanvändare i *Business Owner* eller *Deployment Manager* -rollen i Cloud Manager kan nu ta bort sin produktions- och scenmiljö som angetts via användargränssnittet i Cloud Manager. Alternativet Ta bort finns nu både på miljökortet på sidan **Programöversikt** och på sidan **Miljö** . Om du väljer borttagningsalternativet för antingen produktion eller scen tas även det andra bort i uppsättningen.

   Mer information finns i [Ta bort ett sandlådeprogram](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html) .

* Tips på landningssidan som informerar och instruerar användaren om grundläggande navigering.

* Tips på sidan **Programöversikt** för att informera och instruera användaren om grundläggande navigering i Cloud Manager för att komma igång.

* En **LEARN** -sida är nu tillgänglig i Cloud Manager, som du når via den övre navigeringen. Den här sidan innehåller resurser som hjälper användare att lära sig mer om de mest använda arbetsflödena som är relevanta för deras roller i Cloud Manager.

* Sandlådeprogram identifieras nu med ett **sandlådemärke** som visas på programkortet på landningssidan samt bredvid programnamnet på sidan **Programöversikt** .

* En användare i rollen SysAdmin har nu tillgång till den plats i Admin Console där användarroller och behörigheter till Cloud Manager kan hanteras med ett enda klick. En **Hantera åtkomst** -knapp är nu tillgänglig på landningssidan bredvid knappen **Lägg till program** .

   Mer information finns i [SysAdmin-uppgifter](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/navigation.html#sysadmin-tasks) .

* En användare i rollen SysAdmin har nu tillgång till författarinstansen med ett klick direkt från Cloud Manager.

   Mer information finns i [Hantera åtkomst till författarinstansen](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/navigation.html#manage-access-aem) .

* Build-loggen innehåller nu en lista över identifierade artefakter, inklusive överhoppade innehållspaket.

* I steget Skapa valideras nu att alla genererade innehållspaket innehåller alla obligatoriska egenskaper - namn, grupp och version.

* Bygget verifierar nu att bygget producerade minst ett innehållspaket.

### Bug Fixes {#bug-fixes-cm}

* I vissa situationer var ikonerna i dialogrutan **Skapa program** feljusterade.

* Identifieraren för AEM-versionen visades inte konsekvent på sidan **Programöversikt** .

* När produktionsflödet konfigurerades var alternativet **Schemalagd distribution** inte synligt för vissa kunder.

### Kända fel {#known-issues-cm}

* Miljöer i ett sandlådeprogram försätts i viloläge när ingen aktivitet identifieras under en viss tid. Den här statusen visas inte i Cloud Manager. Status kan dock observeras via Developer Console. Detta kommer att åtgärdas i en kommande version.

* Länken till Developer Console direkt från Cloud Manager visar inte alternativet att avplacera/viloläge för sandlådeprogrammets miljö. För att åtgärda detta lägger du till mönstret i slutet av URL:en på Developer Console, där `#release-cm-p1234-e5678` 1234 *är program-ID och* 5678 ** är miljö-ID. Detta kommer att åtgärdas i en kommande version.

## Nyheter i [!DNL Adobe Experience Manager Assets] {#aem-assets}

<!-- 
Assets RNs are being authored and are a work in progress.
PM/EM review required before publishing.
-->

**Guidad användarupplevelse för förbättrade smarta taggar från Adobe Sensei**

Förbättrade smarta taggar gör det möjligt för organisationer att utbilda smarta taggningsmodeller för att identifiera bilder som baseras på kundspecifika företagstaggar utöver generiska smarta taggar.

I den här versionen finns det en ny, guidad användarupplevelse som hjälper dig att skapa smarta taggar för uppsättningar av kundspecifika taggar och utbilda dem med resurser, som bör kännas igen och taggas med dem i framtiden. Detta är en mer intuitiv upplevelse.
Utbilda förbättrade smarta taggar för mer intuitiv utbildning i Smarta taggar. Se [hur du smarta taggar](/help/assets/smart-tags.md) och [konfigurerar smart taggning](/help/assets/smart-tags-configuration.md).

**Stöd för konsumtion, förgranskning och leverans av 3D-material**

Organisationer kan nu lagra och använda 3D-filer i AEM Resurser. Användaren kan ladda upp, förhandsgranska och använda en mängd olika centrala 3D-filer, t.ex. .obj-, .stl-, .gltf- och .glb-filer. Med tillägg av [!DNL Dynamic Media]kan 3D-upplevelser konfigureras och levereras via agnostiska URL:er eller visningsprogram. Detta inkluderar en [!DNL Dynamic Media] 3D Experience Viewer, Sites 3D Viewer-komponent och möjligheten att leverera 3D-filer via [!DNL Dynamic Media] (AR/VR).

<!-- TBD: Add link to the DM help article, if any. -->

<!-- Hiding this as the GA is at a later date. 
TBD: Add link to the AAL help article. 

**Adobe Asset Link support for Adobe XD**

With the latest release, [!DNL Experience Manager Assets] provides support for a new [!DNL Adobe Asset Link] plug-in that is released with [!DNL Adobe XD] v29. The integration allows designers to access and use assets from [!DNL Experience Manager] in their designs, without the need to leave [!DNL Adobe XD] application.

-->

**Förbättrad tillgänglighet**

[!DNL Adobe Experience Manager Assets] är nu mer tillgängligt i enlighet med riktlinjerna för tillgängligt webbinnehåll (WCAG) v2.1. Tillgängligheten har förbättrats för följande användningsområden eller gränssnitt:

* Element, kontroller, sidor och dialogrutor i användargränssnittet är anpassade för skärmläsare.
* Element, kontroller och inmatningsfält i användargränssnittet är tillgängliga via tangentbordet.
* Ändrar färg eller kontrast på vissa gränssnittselement för att göra dem tydligare för användare med begränsad syn och utan att förstå färger. Resurser har till exempel nu rätt kontrast i stjärngraderingsikonerna på [!UICONTROL Properties] sidan och i kortvyn.

<!-- TBD: Add link to the a11y help article if created. Else add it post-GA. -->

**Andra förbättringar**

Versionen innehåller följande ytterligare förbättringar:

* Hjälpmedelsförbättringar för användargränssnittet Resurser.
* Möjlighet att bearbeta om resurser med tillgångsbearbetningsprofiler, ge användarna full kontroll över processen (kör full bearbetning av resurser, bara tillämpa en viss bearbetningsprofil och bestämma om arbetsflödet ska köras efter bearbetning).
* Sökfrågor returnerar resultat snabbare nu när den underliggande klusterinstansen har startats om bakom scenerna (den inledande sökningen kan ta längre tid i ett sådant fall tidigare).
* Sortera efter Namn när du visar resurser i listvyn i Assets-gränssnittet och i sökresultaten.
* Sortera efter&quot;Skapad&quot; (Datum) när du visar resurser i listvyn i Assets-gränssnittet och i sökresultaten.
* Stöd för konvertering av EPS-filer till bilder.

### Bug Fixes {#assets-bug-fixes}

<!-- TBD: Add enhancements above and bug fixes below.
Seek DM bug fixes if any.
Add Nui update as shared on Slack: https://git.corp.adobe.com/nui/app/releases/tag/22
-->

Förutom de nya funktionerna ovan innehåller den aktuella versionen följande förbättringar och felkorrigeringar baserat på kundfeedback för [!DNL Assets].

* För MP3-musikfiler fungerar inte den uppspelningsknapp som visas på miniatyrbilden i DAM-förhandsvisningen. (CQ-4294731)
* Pekaren placeras på kortvyn och skärmen rullas som ett resultat av (automatisk) fokus på de snabbåtgärder som är tillgängliga på kortet. (GRANITE-26895)
* För många bilder visas när du har bläddrat igenom ett stort antal sökresultat, vilket gör att webbläsaren kraschar. (GRANITE-26432)
* Indikatorerna för [!UICONTROL Options], [!UICONTROL Scope]och [!UICONTROL Workflows] förlopp på [!UICONTROL Manage Publication] sidan läses inte ut av skärmläsaren som förloppsindikatorer. I stället ser skärmläsaranvändare dessa statusindikatorer som en fliklista. (CQ-4273015)
* När du hämtar en resurs är inte nedladdningsalternativet tillgängligt om du har valt e-postalternativ och även om du har angett ett giltigt e-post-ID. (CQ-4296535)

* När du lägger till taggar på en [!UICONTROL Properties] sida i en resurs navigerar användarna i en trädstruktur med taggar. Trädstrukturen är inte tillgänglig eftersom skärmläsaranvändare inte hör något när de navigerar i den. (CQ-4272964)
* Skärmläsaren visas i dialogrutan för länkdelning när du navigerar i bläddringsläge,

   * visar tabellinformationen så snart dialogrutan har lästs in.
   * kan inte navigera till alla automatiska förslag i listan.
   * lägger inte till en berättarröst för de automatiska förslag som visas för [!UICONTROL Add Email Address/Search] kombinationsrutan. (CQ-4294232)

* Det går inte att dra med tangentbordet i NVDA-bläddringsläge i metadatarameditor. (CQ-4296326)
* I Assets-användargränssnittet är visningsinställningarna inte tillgängliga via tangentbordet. (CQ-4289038)
* Anpassade filter som sparats som smarta samlingar används inte korrekt på resurser. (CQ-4294942)
* Flera förbättringar av sökning och indexering samt felkorrigeringar för att förbättra prestandan. (CQ-4286373)
* Luminiscensförhållandet är mindre än 3:1 för de gula betygsikonerna. Det är inte användbart för användare med begränsad syn och utan att förstå färgen. Klassificeringsstjärnorna visas i avsnittet på [!UICONTROL Rating] fliken [!UICONTROL Advanced] i resursvyn [!UICONTROL Properties] eller i kortvyn (CQ-4295106)
* Listrutan för kombinationsrutan (i olika fält på olika sidor) visar nu poster som en lista med alternativ som skärmläsare kan meddela. (CQ-4294017)
* Det går inte att komma åt den nedåtriktade pilen i [!UICONTROL Timeline] med hjälp av ett tangentbord för att använda ett arbetsflöde på en resurs. (CQ-4289268)
* Det går nu att ta bort de markerade taggarna under [!UICONTROL x]fältet på [!UICONTROL Tags] fliken [!UICONTROL Basic] [!UICONTROL Properties] för skärmläsare. (CQ-4273033)
* Skrivskyddade formulärfält (t.ex. inaktiverade fält på [!UICONTROL Basic tab] resurser [!UICONTROL Properties]) kan nu fokuseras med tangentbordet. (CQ-4273031)
* Du kan nu öppna filtersidofältet med hjälp av tangentbordet. (CQ-4273018)
* Ändamålet med olika kombinationsruteelement (t.ex. fältet Bana och alternativet att öppna dialogrutan Markering på fliken Grundläggande i resursegenskaper) meddelas nu korrekt av skärmläsare. (CQ-4273016)
* [!UICONTROL Metadata Schema Editor] sidan och dess element är inte tillgängliga via tangentbordet och är inte läsvänliga för skärmläsare. (CQ-4272953)
* Det går inte att komma åt videovolymkontroller via ett tangentbord. (CQ-4272696)
* Många alternativ som kan användas i Assets-användargränssnittet visar inte fokus när du använder tangentbordet. (CQ-4272694)
* Användare av skärmläsare vet inte om raderna i listvyn är markeringsbara när de använder ett tangentbord. Informationen visas endast när musen förs över raderna. (CQ-4271824)
* Vissa formulärfält, t.ex. fälten för användarnamn och lösenord på inloggningssidan, förlitar sig bara på platshållarvärden för att ge en tillgänglig etikett. (CQ-4271716)
* Nu kan du komma åt interaktiva element i användargränssnittet, t.ex. länkar och alternativ (för sidhuvud och zoomalternativ på resurssidan, mappnavigering) via ett tangentbord. (CQ-4271412)
* Titlarna på alla bläddrade sidor på [!DNL Adobe Experience Manager] Assets är nu unika. (CQ-4271409)
