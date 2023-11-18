---
title: Versionsinformation om Adobe Experience Manager as a Cloud Service 2020.6.0
description: "[!DNL Adobe Experience Manager] as a Cloud Service Release Notes for 2020.6.0."
exl-id: fd6ebe2b-6d98-498c-a45d-b9a9c34e6be7
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1908'
ht-degree: 0%

---

# Versionsinformation för AEM as a Cloud Service 2020.6.0 {#release-notes}

På den här sidan finns en översikt över den allmänna versionsinformationen för Experience Manager as a Cloud Service 2020.6.0.

## Releasedatum {#release-date}

Utgivningsdatum för [!DNL Experience Manager] as a Cloud Service 2020.6.0 är 4 juni 2020.

## Nyheter i AEM Sites {#aem-sites}

Följ det här avsnittet för att lära dig mer om nyheter och uppdateringar för AEM Sites i AEM as a Cloud Service Release 2020.6.0.

### Nyheter {#whats-new-2020.6.0}

Version 2.9.0 av [Kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) ingår nu som en del av AEM Sites:

* Integration mellan [Adobe-klientdatalager](https://github.com/adobe/adobe-client-data-layer) och kärnkomponenterna
* Konfigurerbara HTML ID-attribut för alla komponenter
* En ny Progress Bar-komponent
* Många felkorrigeringar

### Felkorrigeringar {#sites-bug-fixes}

* Komponenter i layoutbehållaren visas inte när layoutbehållaren kopieras och klistras in igen på en sida.

* Korrigerat problem med storleksändring av layoutkomponent.

* Lagt till möjlighet att hantera endast Angular- och AEM/Angular-sidor.

### Tillgänglighet {#accessibility}

* Berättarrollen och läget är nu möjliga för de masterobjekt som finns i **Skapa sida** när du navigerar i bläddringsläget med hjälp av nedpilen.

* En länk i navigeringen har lagts till så att användare kan hoppa över huvudinnehållet.

* Förbättrad skärmläsare.

## What&#39;s New in Foundations in AEM as a Cloud Service {#foundations}

AEM projektbyggtider förbättras genom att alla referenser i det AEM projektets pom.xml tas bort från fjärrdatabasen `https://downloads.experiencecloud.adobe.com/content/maven/public`.

Den AEM as a Cloud Service SDK API Jar, som tidigare fanns på den platsen, finns nu i Maven Central, som är Maven standarddatabas för artefakter.

## Nyheter i Cloud Manager {#cloud-manager}

Följ det här avsnittet för att lära dig mer om nyheter och uppdateringar för Cloud Manager i AEM as a Cloud Service Release 2020.6.0.

### Nyheter {#what-is-new-cloud-manager}

* En användare i *Företagsägare* rollen i Cloud Manager kan nu ta bort ett sandlådeprogram från landningssidan (via snabbåtgärdsknappen på programkortet) eller inifrån programmet.

  Se [Ta bort ett sandlådeprogram](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html) för mer information.

* En användare av sandlådeprogrammet i *Företagsägare* eller *Distributionshanteraren* rollen i Cloud Manager kan nu ta bort sin produktionsmiljö och scenmiljö som angetts via användargränssnittet i Cloud Manager. Alternativet Ta bort är nu tillgängligt både från miljökortet på **Programöversikt** sidan och **Miljö** sida. Om du väljer borttagningsalternativet för antingen produktion eller scen tas även det andra bort i uppsättningen.

  Se [Ta bort ett sandlådeprogram](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/cloud-service-programs/creating-a-program.html) för mer information.

* Tips på landningssidan som informerar och instruerar användaren om grundläggande navigering.

* Tips på **Programöversikt** för att informera och instruera användaren om grundläggande navigering i Cloud Manager för att komma igång.

* A **LÄR DIG** sidan är nu tillgänglig i Cloud Manager via den övre navigeringen. Den här sidan innehåller resurser som hjälper användare att lära sig mer om de mest använda arbetsflödena som är relevanta för deras roller som tilldelats i Cloud Manager.

* Sandlådeprogram identifieras nu med en **Sandbox** emblem som visas på programkortet på landningssidan och bredvid programnamnet i **Programöversikt** sida.

* En användare i rollen SysAdmin har nu tillgång till den plats i Admin Console där användarroller eller behörigheter till Cloud Manager kan hanteras med ett enda klick. A **Hantera åtkomst** finns nu på landningssidan intill **Lägg till program** -knappen.

  Se [SysAdmin-uppgifter](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html#sysadmin-tasks) för mer information.

* En användare i rollen SysAdmin har nu tillgång till författarinstansen med ett klick direkt från Cloud Manager.

  Se [Hantera åtkomst till författarinstansen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/navigation.html#manage-access-aem) för mer information.

* Build-loggen innehåller nu en lista över identifierade artefakter, inklusive överhoppade innehållspaket.

* I steget Skapa valideras nu att alla genererade innehållspaket innehåller alla obligatoriska egenskaper - namn, grupp och version.

* Bygg-steget verifierar nu att bygget producerade minst ett innehållspaket.

### Felkorrigeringar {#bug-fixes-cm}

* I vissa situationer visas ikonerna i **Skapa program** dialogrutan var feljusterad.

* Den AEM releaseidentifieraren visades inte konsekvent på **Programöversikt** sida.

* När produktionsflödet konfigureras visas **Schemalagd distribution** för vissa kunder.

### Kända fel {#known-issues-cm}

* Miljöer i ett sandlådeprogram försätts i viloläge när ingen aktivitet identifieras under en viss tid. Den här statusen visas inte i Cloud Manager. Status kan dock observeras via Developer Console. Detta kommer att åtgärdas i en kommande version.

* Länken till Developer Console direkt från Cloud Manager visar inte alternativet att avplacera/viloläge för sandlådeprogrammets miljö. För att åtgärda detta lägger du till mönstret en gång på Developer Console `#release-cm-p1234-e5678` till slutet av URL:en, där *1234* är program-ID och *5678* är miljö-ID. Detta kommer att åtgärdas i en kommande version.

## Nyheter i [!DNL Adobe Experience Manager Assets] {#aem-assets}

**Guided User Experience for Enhanced Smart Tags från Adobe Sensei**

Förbättrade smarta taggar gör det möjligt för organisationer att utbilda smarta taggningsmodeller för att identifiera bilder som baseras på kundspecifika företagstaggar utöver generiska smarta taggar.

I den här versionen finns det en ny, guidad användarupplevelse som hjälper dig att skapa smarta taggar för uppsättningar av kundspecifika taggar och utbilda dem med resurser, som bör kännas igen och taggas med dem i framtiden. Upplevelsen är nu mer intuitiv.
Utbilda förbättrade smarta taggar för mer intuitiv utbildning i Smarta taggar. Se [hur du lägger till smarta taggar i resurser](/help/assets/smart-tags.md).

**Stöd för konsumtion, förgranskning och leverans av 3D-material**

Organisationer kan nu lagra och använda 3D-filer i AEM Assets. Användaren kan ladda upp, förhandsgranska och använda olika centrala 3D-filer, inklusive OBJ-, STL-, GLTF- och GLB-filer. Med tillägget [!DNL Dynamic Media]kan du konfigurera och leverera 3D-upplevelser med hjälp av agnostiska URL:er eller visningsprogram. Detta inkluderar en [!DNL Dynamic Media] 3D Experience Viewer, Sites 3D Viewer-komponent och möjlighet att leverera 3D-filer via [!DNL Dynamic Media] (AR/VR). Se [Arbeta med 3D-resurser i Dynamic Media](/help/assets/dynamic-media/assets-3d.md).

**Stöd för Adobe Asset Link för Adobe XD**

Med den senaste versionen [!DNL Experience Manager Assets] har stöd för en ny [!DNL Adobe Asset Link] plugin-program som släpps med [!DNL Adobe XD] v29.3. Integrationen gör att designers kan komma åt och använda resurser från [!DNL Experience Manager] i sin design, utan att behöva lämna [!DNL Adobe XD] program. Se [Adobe Asset Link för Adobe XD-dokumentation](https://helpx.adobe.com/enterprise/using/adobe-asset-link-for-xd.html).

I den här versionen kan kreativa användare och designers nu arbeta med resurser som hanteras i [!DNL AEM Assets] använda [!DNL Adobe Asset Link] i en rad datorprogram från Creative Cloud, inklusive [!DNL Adobe XD], [!DNL Photoshop], [!DNL Illustrator]och [!DNL InDesign].

**Förbättringar av hjälpmedel**

[!DNL Adobe Experience Manager Assets] är nu mer tillgängligt i enlighet med riktlinjerna för tillgängligt webbinnehåll (WCAG) v2.1. Tillgängligheten har förbättrats för följande användningsområden eller gränssnitt:

Elementen i användargränssnittet är skärmläsarvänliga, går att komma åt via ett tangentbord och har bättre kontrast. Nedan följer en detaljerad lista över förbättringar:

* The [!UICONTROL Options], [!UICONTROL Scope]och [!UICONTROL Workflows] förloppsindikator [!UICONTROL Manage Publication] sidan läses inte ut av skärmläsaren som förloppsindikator. I stället ser skärmläsaranvändare dessa statusindikatorer som en fliklista. (CQ-4273015)

* När du lägger till taggar i [!UICONTROL Properties] på en tillgångs sida navigerar användarna i en trädstruktur med taggar. Trädstrukturen är inte tillgänglig eftersom skärmläsaranvändare inte hör något när de navigerar i den. (CQ-4272964)

* Skärmläsaren visas i dialogrutan för länkdelning när du navigerar i bläddringsläge,

   * Visar tabellinformationen direkt när dialogrutan läses in.
   * Det går inte att navigera till alla automatiska förslag som visas.
   * Berättar inte om de automatiska förslag som visas för [!UICONTROL Add Email Address/Search] kombinationsruta. (CQ-4294232)

* The [!UICONTROL Metadata Schema Editor] sidan och dess element är nu tillgängliga via ett tangentbord och är skärmläsarvänliga. (CQ-4272953) Användare kan dra komponenterna med tangentbordet i NVDA-bläddringsläge. (CQ-4296326)

* I Assets-användargränssnittet är visningsinställningarna inte tillgängliga via tangentbordet. (CQ-4289038)

* Luminiscensförhållandet är mindre än 3:1 för de gula betygsikonerna. Det är inte användbart för användare med begränsad syn och utan att förstå färgen. Klassificeringsstjärnorna visas på fliken i resursvyn eller i kortvyn

* Färgen och kontrasten i vissa element i användargränssnittet uppdateras så att användare med begränsad syn eller användare utan att uppfatta färger kan särskilja dessa element i användargränssnittet. Färgen på stjärngraderingsikonerna i [!UICONTROL Rating] avsnitt i [!UICONTROL Advanced] i [!UICONTROL Properties] för en resurs och i kortvyn ändras för att uppnå lämplig kontrast. (CQ-4295106)

* Skärmläsarna kan nu läsa posterna på snabbmenyn i kombinationsrutan (i olika fält på olika sidor) som en lista med alternativ. (CQ-4294017)

* Om du vill använda ett arbetsflöde på en resurs trycker du på nedpilen i dialogrutan [!UICONTROL Timeline] kan nås via ett tangentbord. (CQ-4289268)

* Användare kan ta bort markerade taggar i [!UICONTROL Tags] fält i [!UICONTROL Basic] fliken för en resurs [!UICONTROL Properties] sida använda `x` symbol. Skärmläsarna meddelar nu syfte och antal markerade taggar (CQ-4273033).

* De skrivskyddade formulärfälten kan fokuseras på att använda ett tangentbord. De inaktiverade fälten på [!UICONTROL Basic] på en resurs [!UICONTROL Properties] sida. (CQ-4273031)

* Du kan nu använda ett tangentbord till att filtrera resurser i det vänstra sidofältet. (CQ-4273018)

* Skärmläsaren meddelar syftet med olika kombinationsruteelement, t.ex. fältet Bana och alternativet att öppna dialogrutan Markering i [!UICONTROL Basic] fliken för en resurs [!UICONTROL Properties] sida. (CQ-4273016)

* Volymkontrollerna för videoklipp är tillgängliga via ett tangentbord. (CQ-4272696)

* Många alternativ som kan användas i Assets-användargränssnittet visar inte fokus när du använder tangentbordet. (CQ-4272694)

* Skärmläsaranvändare får nu reda på när raderna i listvyn kan markeras med ett tangentbord. Informationen visas när pekaren placeras på raderna. (CQ-4271824)

* Vissa formulärfält, t.ex. fälten för användarnamn och lösenord på inloggningssidan, förlitar sig på platshållarvärden för att ge en tillgänglig etikett. (CQ-4271716)

* Du kan nu komma åt interaktiva element i användargränssnittet, t.ex. länkar och alternativ som sidhuvud och zoomalternativ för resurssidan eller mappnavigering med hjälp av ett tangentbord. (CQ-4271412)

* Titlar på alla bläddrade sidor på [!DNL Adobe Experience Manager] Resurserna är nu unika. (CQ-4271409)

**Andra förbättringar**

Versionen innehåller följande andra förbättringar:

* Möjlighet att bearbeta om resurser med tillgångsbearbetningsprofiler, ge användarna full kontroll över processen (kör full bearbetning av resurser, bara tillämpa en viss bearbetningsprofil och bestämma om arbetsflödet ska köras efter bearbetning).
* Sökfrågor returnerar resultat snabbare nu när den underliggande klusterinstansen har startats om bakom scenerna (den inledande sökningen kan ta längre tid i ett sådant fall tidigare).
* Sortera efter Namn när du visar resurser i listvyn i Assets-gränssnittet och i sökresultaten. Se [sökresurser](/help/assets/search-assets.md#sort).
* Sortera efter&quot;Skapat&quot; (Datum) när du visar resurser i listvyn i Assets-gränssnittet och i sökresultaten. Se [sökresurser](/help/assets/search-assets.md#sort).
* Stöd för konvertering av EPS-filer till bilder med hjälp av objektmikrotjänster.

### Felkorrigeringar {#assets-bug-fixes}

Förutom de nya funktionerna ovan innehåller den aktuella versionen följande felkorrigeringar som baseras på kundens feedback för [!DNL Assets].

* För MP3-musikfiler fungerar inte den uppspelningsknapp som visas på miniatyrbilden i DAM-förhandsvisningen. (CQ-4294731)
* Pekaren placeras på kortvyn och skärmen rullas som ett resultat av (automatisk) fokus på de snabbåtgärder som är tillgängliga på kortet. (GRANITE-26895)
* För många bilder visas när du har bläddrat igenom många sökresultat, vilket leder till att webbläsaren kraschar. (GRANITE-26432)
* När du hämtar en resurs är inte nedladdningsalternativet tillgängligt om du har valt e-postalternativ och även om du har angett ett giltigt e-post-ID. (CQ-4296535)
* Anpassade filter som sparats som smarta samlingar används inte korrekt på resurser. (CQ-4294942)
* Flera förbättringar av sökning och indexering samt felkorrigeringar för att förbättra prestandan. (CQ-4286373)
* Fliken för mappegenskaper kan inte öppnas i Resurser och returnerar ett 500-fel. (CQ-4295701)
