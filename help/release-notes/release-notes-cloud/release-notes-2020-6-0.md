---
title: Adobe Experience Manager som Cloud Service Release Notes for 2020.6.0
description: Versionsinformation om Experience Manager för 2020.6.0
translation-type: tm+mt
source-git-commit: c3922be7da1e76fee51e2ae2f59f16e260727001
workflow-type: tm+mt
source-wordcount: '1931'
ht-degree: 0%

---


# Versionsinformation för AEM som Cloud Service 2020.6.0 {#release-notes}

På den här sidan beskrivs den allmänna versionsinformationen för Experience Manager som Cloud Service 2020.6.0.

## Releasedatum {#release-date}

Releasedatum för [!DNL Experience Manager] Cloud Service 2020.6.0 är 4 juni 2020.

## Nyheter i AEM Sites {#aem-sites}

Följ det här avsnittet för att lära dig mer om nyheter och uppdateringar för AEM Sites i AEM som en Cloud Service version 2020.6.0.

### Nyheter {#whats-new-2020.6.0}

Version 2.9.0 av [Core Components](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html) finns nu som en del av AEM Sites, inklusive:

* Integrering mellan [Adobe-klientdatalagret](https://github.com/adobe/adobe-client-data-layer) och kärnkomponenterna
* Konfigurerbara HTML ID-attribut för alla komponenter
* En ny Progress Bar-komponent
* Många felkorrigeringar

### Bug Fixes {#sites-bug-fixes}

* Komponenter i layoutbehållaren visas inte när layoutbehållaren kopieras och klistras in igen på en sida.

* Korrigerat problem med storleksändring av layoutkomponent.

* Lagt till möjlighet att hantera endast sidor med routningsvinkel och AEM/vinkelsidor.

### Tillgänglighet {#accessibility}

* Nu går det att lägga till berättarroller och status för huvudobjekten i dialogrutan **Skapa sida** när du navigerar i bläddringsläget med hjälp av nedpilen.

* En länk i navigeringen har lagts till så att användare kan hoppa över huvudinnehållet.

* Förbättrad skärmläsare.

## What&#39;s New in Foundations in AEM as a Cloud Service {#foundations}

AEM projekttider förbättras genom att alla referenser i det AEM projektets pom.xml tas bort från fjärrdatabasen `https://downloads.experiencecloud.adobe.com/content/maven/public`.

AEM som en Cloud Service-SDK API Jar, som tidigare var värd på den platsen, finns nu i Maven Central, som är Maven standarddatabas för artefakter.

## Nyheter i Cloud Manager {#cloud-manager}

Följ det här avsnittet för att lära dig mer om nyheter och uppdateringar för Cloud Manager i AEM som en Cloud Service-version 2020.6.0.

### Nyheter {#what-is-new-cloud-manager}

* En användare i rollen *Business Owner* i Cloud Manager kan nu ta bort ett sandlådeprogram från landningssidan (via snabbåtgärdsknappen på programkortet) eller inifrån programmet.

   Mer information finns i [Ta bort ett sandlådeprogram](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html) .

* En sandlådeprogramanvändare i *Business Owner* eller *Deployment Manager* -rollen i Cloud Manager kan nu ta bort sin produktions- och scenmiljö som angetts via användargränssnittet i Cloud Manager. Alternativet Ta bort finns nu både på miljökortet på sidan **Programöversikt** och på sidan **Miljö** . Om du väljer borttagningsalternativet för antingen produktion eller scen tas även det andra bort i uppsättningen.

   Mer information finns i [Ta bort ett sandlådeprogram](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html) .

* Tips på landningssidan som informerar och instruerar användaren om grundläggande navigering.

* Tips på sidan **Programöversikt** för att informera och instruera användaren om grundläggande navigering i Cloud Manager för att komma igång.

* En **LEARN** -sida är nu tillgänglig i Cloud Manager, som du når via den övre navigeringen. Den här sidan innehåller resurser som hjälper användare att lära sig mer om de mest använda arbetsflödena som är relevanta för deras roller i Cloud Manager.

* Sandlådeprogram identifieras nu med ett **sandlådemärke** som visas på programkortet på landningssidan samt bredvid programnamnet på sidan **Programöversikt** .

* En användare i rollen SysAdmin har nu tillgång till den plats i Admin Console där användarroller eller behörigheter till Cloud Manager kan hanteras med ett enda klick. En **Hantera åtkomst** -knapp är nu tillgänglig på landningssidan bredvid knappen **Lägg till program** .

   Mer information finns i [SysAdmin-uppgifter](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/navigation.html#sysadmin-tasks) .

* En användare i rollen SysAdmin har nu tillgång till författarinstansen med ett klick direkt från Cloud Manager.

   Mer information finns i [Hantera åtkomst till författarinstansen](https://docs.adobe.com/content/help/en/experience-manager-cloud-service/onboarding/getting-access/navigation.html#manage-access-aem) .

* Build-loggen innehåller nu en lista över identifierade artefakter, inklusive överhoppade innehållspaket.

* I steget Skapa valideras nu att alla genererade innehållspaket innehåller alla obligatoriska egenskaper - namn, grupp och version.

* Bygget verifierar nu att bygget producerade minst ett innehållspaket.

### Bug Fixes {#bug-fixes-cm}

* I vissa situationer var ikonerna i dialogrutan **Skapa program** feljusterade.

* Den AEM releaseidentifieraren visades inte konsekvent på sidan **Programöversikt** .

* När produktionsflödet konfigurerades var alternativet **Schemalagd distribution** inte synligt för vissa kunder.

### Kända fel {#known-issues-cm}

* Miljöer i ett sandlådeprogram försätts i viloläge när ingen aktivitet identifieras under en viss tid. Den här statusen visas inte i Cloud Manager. Status kan dock observeras via Developer Console. Detta kommer att åtgärdas i en kommande version.

* Länken till Developer Console direkt från Cloud Manager visar inte alternativet att avplacera/viloläge för sandlådeprogrammets miljö. För att åtgärda detta lägger du till mönstret i slutet av URL:en på Developer Console, där `#release-cm-p1234-e5678` 1234 *är program-ID och* 5678 ** är miljö-ID. Detta kommer att åtgärdas i en kommande version.

## Nyheter i [!DNL Adobe Experience Manager Assets] {#aem-assets}

**Guided User Experience for Enhanced Smart Tags från Adobe Sensei**

Förbättrade smarta taggar gör det möjligt för organisationer att utbilda smarta taggningsmodeller för att identifiera bilder som baseras på kundspecifika företagstaggar utöver generiska smarta taggar.

I den här versionen finns det en ny, guidad användarupplevelse som hjälper dig att skapa smarta taggar för uppsättningar av kundspecifika taggar och utbilda dem med resurser, som bör kännas igen och taggas med dem i framtiden. Upplevelsen är nu mer intuitiv.
Utbilda förbättrade smarta taggar för mer intuitiv utbildning i Smarta taggar. Se [hur du lägger till smarta taggar i resurser](/help/assets/smart-tags.md) och [konfigurerar smart taggning](/help/assets/smart-tags-configuration.md).

**Stöd för konsumtion, förgranskning och leverans av 3D-material**

Organisationer kan nu lagra och använda 3D-filer i AEM Assets. Användaren kan ladda upp, förhandsgranska och använda olika centrala 3D-filer, inklusive OBJ-, STL-, GLTF- och GLB-filer. Dessutom [!DNL Dynamic Media]kan ni konfigurera och leverera 3D-upplevelser med hjälp av agnostiska URL:er eller visningsprogram. Detta inkluderar en [!DNL Dynamic Media] 3D Experience Viewer, Sites 3D Viewer-komponent och möjligheten att leverera 3D-filer via [!DNL Dynamic Media] (AR/VR). Se [Arbeta med 3D-resurser i Dynamic Media](/help/assets/dynamic-media/assets-3d.md).

**Stöd för Adobe Asset Link för Adobe XD**

I den senaste versionen har [!DNL Experience Manager Assets] stöd för en ny [!DNL Adobe Asset Link] plugin som släpps med [!DNL Adobe XD] v29.3. Tack vare integreringen kan designers komma åt och använda resurser från [!DNL Experience Manager] sin design, utan att behöva lämna [!DNL Adobe XD] programmet. Se [Adobe Asset Link för Adobe XD-dokumentation](https://helpx.adobe.com/enterprise/using/adobe-asset-link-for-xd.html).

I den här versionen kan kreativa användare och designers nu arbeta med resurser som hanteras i [!DNL AEM Assets] med [!DNL Adobe Asset Link] en rad olika datorprogram i Creative Cloud, inklusive [!DNL Adobe XD], [!DNL Photoshop], [!DNL Illustrator]och [!DNL InDesign].

**Förbättrad tillgänglighet**

[!DNL Adobe Experience Manager Assets] är nu mer tillgängligt i enlighet med riktlinjerna för tillgängligt webbinnehåll (WCAG) v2.1. Tillgängligheten har förbättrats för följande användningsområden eller gränssnitt:

Elementen i användargränssnittet är skärmläsarvänliga, går att komma åt via ett tangentbord och har bättre kontrast. Nedan följer en detaljerad lista över förbättringar:

* Staplarna [!UICONTROL Options], [!UICONTROL Scope]och [!UICONTROL Workflows] förloppsindikatorn på [!UICONTROL Manage Publication] sidan läses inte ut av skärmläsaren som förloppsindikator. I stället ser skärmläsaranvändare dessa statusindikatorer som en fliklista. (CQ-4273015)

* När du lägger till taggar på en [!UICONTROL Properties] sida i en resurs navigerar användarna i en trädstruktur med taggar. Trädstrukturen är inte tillgänglig eftersom skärmläsaranvändare inte hör något när de navigerar i den. (CQ-4272964)

* Skärmläsaren visas i dialogrutan för länkdelning när du navigerar i bläddringsläge,

   * Visar tabellinformationen direkt när dialogrutan läses in.
   * Det går inte att navigera till alla automatiska förslag som visas.
   * Berättar inte om de automatiska förslagen som visas för [!UICONTROL Add Email Address/Search] kombinationsrutan. (CQ-4294232)

* Sidan och dess element är nu tillgängliga via ett tangentbord och är läsvänliga för skärmläsare. [!UICONTROL Metadata Schema Editor] (CQ-4272953) Användare kan dra komponenterna med tangentbordet i NVDA-bläddringsläge. (CQ-4296326)

* I Assets-användargränssnittet är visningsinställningarna inte tillgängliga via tangentbordet. (CQ-4289038)

* Luminiscensförhållandet är mindre än 3:1 för de gula betygsikonerna. Det är inte användbart för användare med begränsad syn och utan att förstå färgen. Klassificeringsstjärnorna visas på fliken i resursvyn eller i kortvyn

* Färgen och kontrasten i vissa element i användargränssnittet uppdateras så att användare med begränsad syn eller användare utan att uppfatta färger kan särskilja dessa element i användargränssnittet. Färgen på stjärngraderingsikonerna i [!UICONTROL Rating] avsnittet på [!UICONTROL Advanced] fliken i [!UICONTROL Properties] en resurs och i kortvyn ändras för att ge rätt kontrast. (CQ-4295106)

* Skärmläsarna kan nu läsa posterna på snabbmenyn i kombinationsrutan (i olika fält på olika sidor) som en lista med alternativ. (CQ-4294017)

* Om du vill använda ett arbetsflöde på en resurs kan du få åtkomst till den med hjälp av ett tangentbord. [!UICONTROL Timeline] (CQ-4289268)

* Användare kan ta bort markerade taggar i [!UICONTROL Tags] fältet på [!UICONTROL Basic] fliken på en tillgångs [!UICONTROL Properties] sida med hjälp av `x` symbol. Skärmläsarna meddelar nu syfte och antal markerade taggar (CQ-4273033).

* De skrivskyddade formulärfälten kan fokuseras på att använda ett tangentbord. Till exempel de inaktiverade fälten på [!UICONTROL Basic] fliken på en tillgångs [!UICONTROL Properties] sida. (CQ-4273031)

* Du kan nu använda ett tangentbord till att filtrera resurser i det vänstra sidofältet. (CQ-4273018)

* Skärmläsaren meddelar syftet med olika kombinationsruteelement, t.ex. fältet Bana och alternativet att öppna dialogrutan Markering på [!UICONTROL Basic] fliken på en resurs [!UICONTROL Properties] sida. (CQ-4273016)

* Volymkontrollerna för videoklipp är tillgängliga via ett tangentbord. (CQ-4272696)

* Många alternativ som kan användas i Assets-användargränssnittet visar inte fokus när du använder tangentbordet. (CQ-4272694)

* Skärmläsaranvändare får nu reda på när raderna i listvyn kan markeras med ett tangentbord. Informationen visas när pekaren placeras på raderna. (CQ-4271824)

* Vissa formulärfält, t.ex. fälten för användarnamn och lösenord på inloggningssidan, förlitar sig på platshållarvärden för att ge en tillgänglig etikett. (CQ-4271716)

* Du kan nu komma åt interaktiva element i användargränssnittet, t.ex. länkar och alternativ som sidhuvud och zoomalternativ för resurssidan eller mappnavigering med hjälp av ett tangentbord. (CQ-4271412)

* Titlarna på alla bläddrade sidor på [!DNL Adobe Experience Manager] Assets är nu unika. (CQ-4271409)

**Andra förbättringar**

Versionen innehåller följande andra förbättringar:

* Möjlighet att bearbeta om resurser med tillgångsbearbetningsprofiler, ge användarna full kontroll över processen (kör full bearbetning av resurser, bara tillämpa en viss bearbetningsprofil och bestämma om arbetsflödet ska köras efter bearbetning).
* Sökfrågor returnerar resultat snabbare nu när den underliggande klusterinstansen har startats om bakom scenerna (den inledande sökningen kan ta längre tid i ett sådant fall tidigare).
* Sortera efter Namn när du visar resurser i listvyn i Assets-gränssnittet och i sökresultaten. Se [Sökresurser](/help/assets/search-assets.md#sort).
* Sortera efter&quot;Skapad&quot; (Datum) när du visar resurser i listvyn i Assets-gränssnittet och i sökresultaten. Se [Sökresurser](/help/assets/search-assets.md#sort).
* Stöd för att konvertera EPS-filer till bilder med hjälp av objektmikrotjänster.

### Bug Fixes {#assets-bug-fixes}

Förutom de nya funktionerna ovan innehåller den aktuella versionen följande felkorrigeringar som baseras på kundfeedback för [!DNL Assets].

* För MP3-musikfiler fungerar inte den uppspelningsknapp som visas på miniatyrbilden i DAM-förhandsvisningen. (CQ-4294731)
* Pekaren placeras på kortvyn och skärmen rullas som ett resultat av (automatisk) fokus på de snabbåtgärder som är tillgängliga på kortet. (GRANITE-26895)
* För många bilder visas när du har bläddrat igenom många sökresultat vilket gör att webbläsaren kraschar. (GRANITE-26432)
* När du hämtar en resurs är inte nedladdningsalternativet tillgängligt om du har valt e-postalternativ och även om du har angett ett giltigt e-post-ID. (CQ-4296535)
* Anpassade filter som sparats som smarta samlingar används inte korrekt på resurser. (CQ-4294942)
* Flera förbättringar av sökning och indexering samt felkorrigeringar för att förbättra prestandan. (CQ-4286373)
* Fliken för mappegenskaper kan inte öppnas i Resurser och returnerar ett 500-fel. (CQ-4295701)
