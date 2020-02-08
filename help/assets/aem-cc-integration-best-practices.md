---
title: Bästa praxis för integrering av Adobe Experience Manager och Adobe Creative Cloud
description: Bästa tillvägagångssätt för att integrera en AEM-instans med Adobe Creative Cloud för att effektivisera överföringsarbetsflöden och uppnå maximal effektivitet.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# Bästa praxis för integrering av AEM och Creative Cloud {#aem-and-creative-cloud-integration-best-practices}

Adobe Experience Manager Assets (AEM) är en DAM-lösning (Digital Asset Management) som kan integreras med Adobe Creative Cloud för att hjälpa DAM-användare att samarbeta med kreativa team och effektivisera samarbetet när innehåll skapas.

Adobe Creative Cloud ger kreativa team ett ekosystem av lösningar och tjänster som hjälper dem att skapa digitala resurser. Det omfattar program för dator och mobil, molntjänster som lagring med datorsynkronisering eller webbupplevelse, liksom marknadsplatser som Adobe Stock.

Läs vidare för att ta reda på vilka integreringar som du ska välja mellan stationär dator och företagsspecifik DAM baserat på ditt användningsfall och vilka metoder som är associerade med de sammankopplade arbetsflödena.

>[!NOTE]
>
>AEM i Creative Cloud-mappdelning är nu föråldrat och beskrivs inte längre nedan. Adobe rekommenderar nyare funktioner som Adobe Asset Link eller AEM-skrivbordsappen för att ge kreativa användare tillgång till resurserna som hanteras i AEM.

## Samarbete mellan kreatörer, marknadsförare och DAM-användare {#collaboration-need-of-creatives-marketers-and-dam-users}


| Krav | Använd skiftläge | Involverade ytor |
|---|---|---|
| Förenkla för kreatörer på datorn | Effektivisera åtkomsten till resurser från en DAM (AEM Assets) för kreatörer, eller mer allmänt för användare på datorer som arbetar med program för att skapa egna resurser. De behöver ett enkelt och enkelt sätt att upptäcka, använda (öppna), redigera och spara ändringar i AEM samt överföra nya filer. | Skrivbordet Win eller Mac. Creative Cloud-program |
| Tillhandahåll högkvalitativa, färdiga mediefiler från Adobe Stock | Marknadsförarna hjälper till att snabba upp processen för att skapa innehåll genom att hjälpa till med materialanskaffning och identifiering. Kreatörer använder det godkända materialet direkt inifrån sina kreativa verktyg. | AEM Assets; Adobe Stock Marketplace; metadatafält |
| Distribuera och dela resurser efter organisationer | Interna avdelningar/lokala kontor och externa partners, distributörer och byråer använder det godkända material som delas av huvudorganisationen. Organisationen vill säkert och smidigt dela de skapade resurserna för vidare återanvändning. | Varumärkesportal, Resursdelningskommentarer |

## Adobes lösningar för samverkan {#adobe-offerings-to-support-the-collaboration-need}

| Värdeförslag för berörda personer | Erbjudande | Involverade ytor |
|---|---|---|
| Creative-användare upptäcker resurser från AEM, öppnar och använder dem, redigerar och överför ändringar till AEM samt överför nya filer till AEM, utan att behöva lämna Creative Cloud-programmen. | [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) | Photoshop, Illustrator och InDesign |
| Affärsanvändare förenklar öppning och användning av resurser, redigering och överföring av ändringar till AEM samt överföring av nya filer till AEM från skrivbordsmiljön. De använder en allmän integrering för att öppna alla resurstyper i det inbyggda datorprogrammet, inklusive sådana som inte kommer från Adobe. | [AEM-skrivbordsapp](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html) | AEM-skrivbordsapp på Win och Mac |
| Marknadsförare och företagsanvändare upptäcker, förhandsgranskar, licensierar och sparar Adobe Stock-mediefiler från AEM. Licensierade och sparade mediefiler innehåller utvalda Adobe Stock-metadata för bättre styrning. | [Integrering av Experience Manager och Adobe Stock](aem-assets-adobe-stock.md) | AEM-webbgränssnitt |

Den här artikeln fokuserar främst på de två första aspekterna av samarbetsbehovet. Distribution och anskaffning av resurser i stor skala omnämns kortfattat som ett användningsexempel. Överväg Adobe Brand Portal eller Assets Share Commons för sådana behov. Alternativa lösningar som [AEM Assets Brand Portal](https://helpx.adobe.com/experience-manager/brand-portal/user-guide.html), lösningar som kan byggas baserat på komponenterna [Asset Share Commons](https://adobe-marketing-cloud.github.io/asset-share-commons/) , [Link Share](share-assets.md)och [AEM Assets-webbgränssnittet](/help/assets/manage-digital-assets.md) bör granskas utifrån specifika krav.

![Creative Cloud-anslutningar för AEM: Bestäm vilka funktioner som ska användas](assets/creative-connections-aem.png)

Bestäm vilka funktioner som ska användas

### Mappning av användningsfall och Adobe-lösningar {#mapping-of-use-cases-and-adobe-solutions}

| Använd skiftläge | Adobe Asset Link | AEM-skrivbordsapp | Anmärkningar eller alternativa metoder |
|----------------------------------------------------------|-----------------------------------------------------------------------------------|--------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| Upptäck - bläddra bland AEM-mappar | Ja | AEM Web UI + skrivbordsåtgärder | När du bläddrar i nätverksresursen ska du inaktivera miniatyrbilderna för att undvika att hämta binära filer med resurser. |
| Upptäck - få tillgång till AEM-samlingar | Ja | AEM Web UI + skrivbordsåtgärder |  |
| Upptäck - sök efter resurser från AEM | Ja | AEM Web UI + skrivbordsåtgärder |  |
| Använd - öppen resurs | Ja | Ja - för alla appar | [Öppna från webbgränssnittet](/help/assets/manage-digital-assets.md#previewing-assets) eller från Finder |
| Använd - placera resurser från AEM i ett dokument | Ja - inbäddning | Ja - länkning eller inbäddning | AEM-skrivbordsappen ger åtkomst till resurser som filer i det lokala filsystemet. De här länkarna i de ursprungliga programmen representeras av lokala sökvägar. |
| Redigera - öppna för redigering | Ja - utcheckningsåtgärd | Ja - Öppna åtgärd (i nätverksresursen) | [Checka ut i AAL](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) sparar resursen i användarens Creative Cloud-lagringskonto (synkroniserat med Creative Cloud-programmet) som standard. |
| Redigera - pågående arbete utanför AEM | Ja - Tillgängliga resurser i användarens Creative Cloud-lagringskonto synkroniserat med skrivbordet. | Ja |  |
| Redigera - ladda upp ändringar | Ja - [incheckningsåtgärd](https://helpx.adobe.com/enterprise/using/manage-assets-using-adobe-asset-link.html) med valfri kommentar | Ja |  |
| Överför - en fil | Ja - överför aktuellt aktivt dokument | Ja | [Överför via webbgränssnitt](/help/assets/manage-digital-assets.md#uploading-assets) |
| Överför - flera filer/hierarkiska mappstrukturer | Nej | Ja | [Ladda upp via webbgränssnitt](/help/assets/manage-digital-assets.md#uploading-assets); Anpassade skript eller verktyg |
| Diverse - användare och inloggning | Creative Cloud-användare som är inloggad på Creative Cloud-datorprogrammet blir igenkända (SSO) | AEM-användare/inloggning | Användare av båda lösningarna räknas av mot AEM-användarkvoten. |
| Diverse - nätverk och åtkomst | Kräver åtkomst från användarens skrivbord till AEM-distribution via nätverk | Kräver åtkomst från användarens skrivbord till AEM-distribution via nätverk | Adobe Asset Link delar inte nätverksproxymiljö. |


<!-- Removing this row from table as migration guide is not yet final.
| Misc - Migrate large number of assets | No | No | [Migration Guide](/help/assets/assets-migration-guide.md) |
-->

För att stödja användningsexemplen på resursfördelning bör andra lösningar beaktas:

* [AEM Assets Brand Portal](https://helpx.adobe.com/experience-manager/brand-portal/user-guide.html) för ett konfigurerbart SaaS-tillägg i AEM Assets för publicering av resurser.

* Anpassade lösningar skapas baserat på kodbasen [Resursdelningskommentarer](https://adobe-marketing-cloud.github.io/asset-share-commons/) .
* AEM [link share](/help/assets/share-assets.md) to share assets ad hoc using links.
* [AEM Assets-webbgränssnittet](/help/assets/manage-digital-assets.md) med områden för externa parter som skyddas av AEM Access Control-installationen och med nödvändiga IT-/nätverkskonfigurationsjusteringar, vilket ger dessa externa användare tillgång till AEM.

## Viktiga begrepp och användningsområden {#key-concepts-and-use-cases}

### Ordlista med vanliga termer {#glossary-of-common-terms}

* **** Work-in-progress eller creative work-in-progress (PIP): En fas i en tillgångs livscykel där en resurs genomgår flera ändringar och vanligtvis inte är redo att delas med fler team.
* **** Kreativa resurser: Resurser som är klara att delas med ett större team, eller som har valts ut/godkänts av det kreativa teamet för att delas med marknadsförings- eller LOB-team.

* **** Godkännanden av tillgångar: Godkännandeprocessen som körs för resurser som redan har överförts till DAM, som vanligtvis omfattar varumärkesgodkännanden, juridiska godkännanden och så vidare.
* **** Slutlig tillgång: En resurs som har genomgått alla godkännanden/metadatataggar och är klar att användas av teamet. En sådan resurs lagras i DAM och görs tillgänglig för alla (eller alla intresserade) användare. Den kan användas i marknadsföringskanaler eller av kreativa team för att skapa design.

* **** Mindre uppdatering/ändring av resurs: En snabb och liten förändring av en digital resurs. Det görs ofta som svar på en begäran om retuschering eller mindre redigering, granskning av resurser eller godkännande (t.ex. omplacering, ändring av textstorlek, justering av mättnad/intensitet, färg osv.).
* **** Uppdatering/ändring av större tillgångar: En förändring av en digital resurs som kräver mycket arbete och ibland måste göras under en längre tidsperiod. Det innehåller vanligtvis flera ändringar. Resursen måste sparas flera gånger medan den uppdateras. Viktiga resursuppdateringar gör att resursen går in i ett Pågående arbete-stadium.
* **** DAM: Digital resurshantering. I det här dokumentet är det synonymt med AEM Experience Manager Assets, om inget annat anges.
* **** Kreativ användare: En kreatör som skapar digitalt material med Creative Cloud-program och -tjänster. I vissa fall är en kreativ användare medlem i ett kreativt team som kanske använder Creative Cloud, men som inte skapar digitala resurser (som en creative director eller creative team manager).
* **** DAM-användare: En typisk användare av ett DAM-system. Beroende på organisationen kan en DAM-användare vara en marknadsföringsanvändare eller en icke-marknadsföringsanvändare, till exempel en kontors- (LOB) användare, bibliotekarie, säljare osv.

### Att tänka på när du använder AEM och Creative Cloud-integrering {#considerations-when-using-aem-and-creative-cloud-integration}

<!--incomplete and TBD: 

* DA2.0 best practices: See troubleshooting.md
* Stock integration: See ?
* AAL: See ?
* BP: See ?

-->

Detta är en kort sammanfattning av de effektivaste strategierna för AEM- och Creative Cloud-integrering. Läs resten av det här dokumentet för att få en mer detaljerad förståelse för dessa.

* **** För kreativa användare: arbete i Photoshop, InDesign eller Illustrator: Adobe Asset Link ger den bästa användarupplevelsen, inklusive ren hantering av pågående arbeten för resurser som checkats ut från AEM
* **** För att förenkla åtkomsten till resurser från skrivbordet för alla generiska filformat eller program: använd AEM-skrivbordsapp
* **** Förstå varför och när resurser ska lagras i DAM: Uppdateringar som ska göras tillgängliga för hela teamet i organisationen
* **** Lägg märke till mängden resurser som delas: Om ni använder mediedistribution kan det vara de viktigaste aspekterna för styrning och säkerhet. Överväg att använda verktyg som är byggda för att göra detta i stor skala, som varumärkesportalen.
* **** Förstå tillgångarnas livscykel: Ta reda på hur resurser hanteras i organisationen av olika team
* **** Hantera ofta sparade resurser med stor omsorg: Adobe Asset Link tar hand om det åt dig med PS, AI, ID. För andra program ska du inte utföra pågående uppgifter i mappad/delad mapp såvida du inte behöver alla ändringar i DAM

### Åtkomst till Adobe Stock-resurser från AEM Assets {#access-to-adobe-stock-assets-from-aem-assets}

[AEM- och Adobe Stock-integrering](/help/assets/aem-assets-adobe-stock.md) ger AEM-användare möjlighet att söka, förhandsgranska, licensiera och spara resurser från Adobe Stock i AEM. Licensierade och sparade Adobe Stock-mediefiler har valt Stock-metadata som kan användas för att söka efter dem med extra filter.

Några viktiga punkter om den här integreringen:

* När resurser från Adobe Stock sparas till AEM blir de ett vanligt AEM Resurser, med binärfiler sparade i AEM-databasen. Vissa metadata som är relaterade till Adobe Stock sparas för resursen i AEM, annars ser importen ut på samma sätt som för andra filer. Om till exempel smarta taggar är aktiva läggs taggarna till i de här resurserna när de sparas.
* Resursen som sparas till AEM är en kopia, inte en länk tillbaka till Adobe Stock.

**Arbeta med resurser som sparats från Adobe Stock till AEM i Creative Cloud**. Den här integreringen är oberoende av Adobe Asset Link, men Adobe Asset Link känner igen dessa resurser som sparats från Stock på det sättet och visar ytterligare metadata och Stock-ikoner för dessa resurser i Adobe Asset Link-tilläggsgränssnittet i Photoshop, Illustrator eller InDesign. Filerna är tillgängliga för att bläddra, öppna och så vidare, eftersom de är vanliga AEM-resurser när de sparas i AEM.
Creative-användare som arbetar i Creative Cloud-program med Adobe Asset Link-tillägget närvarande kan, förutom att ha tillgång till redan licensierade mediefiler från Adobe Stock till AEM, även använda Creative Cloud Libraries-panelen för att söka efter, förhandsgranska och licensiera Adobe Stock-mediefiler.
Resurser från Adobe Stock som licensierats och sparats i AEM blir tillgängliga för de större team som har tillgång till AEM Assets-distributionen, medan kreatörer som licensierar resurser från Adobe Stock via Creative Cloud Libraries-panelen gör dem tillgängliga endast som standard i sina Creative Cloud-konton.

## Lagra resurser i ett resurshanteringssystem {#about-storing-assets-in-a-dam}

För att skapa ett effektivt arbetsflöde mellan kreatörer och marknadsförare/branschspecifika team (LOB) och välja de bästa supportfunktionerna är det viktigt att förstå när och varför resurser lagras i DAM.

### Varför resurser lagras i DAM {#why-assets-are-stored-in-dam}

Genom att lagra resurser i DAM blir de enkelt tillgängliga och sökbara. Det ser till att resurserna kan utnyttjas av många användare i organisationen eller ekosystemet, bland annat partners, kunder och så vidare.

De flesta organisationer väljer att endast lagra resurser som är relevanta för marknadsförings-/LOB-processerna längre fram i kedjan (publicera till kanaler som webbkanal via AEM Sites eller andra kanaler som hanteras av Adobe Experience Cloud - Marketing Cloud, Advertising Cloud, och som mäts av Analytics Cloud, som tillhandahålls användare/partner och så vidare). Dessutom lagrar organisationer resurser som kan bli föremål för en gransknings-/godkännandeprocess i DAM. På så sätt lagrar DAM de flesta resurser som har stora chanser att utnyttjas och undviker att lagra inaktiva resurser.

Lagring av resurser är också beroende av tekniska aspekter och resursutnyttjande. DAM tillhandahåller ytterligare tjänster runt lagrade resurser, inklusive extrahering av metadata, versionshantering, generering av förhandsgranskning/omkodning, hantering av referenser och tillägg av åtkomstkontrollsinformation. Dessa tjänster kräver extra tid och infrastrukturresurser.

Det är ofta inte önskvärt att lagra alla resurser och uppdateringar. Om till exempel uppdateringar av specifika resurser har dålig kvalitet och förbrukar för mycket resurser, kanske resurserna inte lagras i DAM.

#### När resurser lagras i DAM {#when-assets-are-stored-in-dam}

Kreativa team (och organisationer) är vanligtvis inte intresserade av att lagra resurser i varje skede av resursens livscykel. De undviker till exempel att lagra resurser i följande fall:

* Resurser som ännu inte färdigställts eller som är föremål för experimenterande
* Resurser som inte godkänns i granskningsprocessen
* Jämfört med den aktuella resursen har teamet bättre kandidater att representera sitt arbete för externa team

Vanligtvis lagras följande klassresurser i DAM:

* Tillgångar som har nått en viss löptid och anses vara klara att delas
* Resurser som har valts ut i förväg av det kreativa teamet
* Specifika resursformat som kan användas eller begäras av marknadsföring, beroende på ett specifikt kontrakt eller avtal (t.ex. JPG-filer som konverterats från RAW-filer, TIFF-filer/bilder från PSD-original)

#### När uppdateringar av resurser lagras i DAM {#when-updates-to-assets-are-stored-in-dam}

I regel ska endast uppdateringar av resurser som är relevanta för den bredare uppsättningen DAM-användare lagras i DAM. Det ser till att användare (marknadsföringsfunktioner och liknande funktioner) bara ser relevanta versioner på tidslinjen för DAM-resurser.

Vanligtvis ändras relaterade till viktiga milstolpar i resursens livscykel. Den initiala marknadsföringsfärdiga resursen eller en officiell uppdatering som baseras på begäran/granskning som tillhandahålls av det kreativa teamet bör till exempel lagras och versionshanteras i DAM.

Det kreativa teamets uppdatering för granskning av marknadsföringsteamet efter en begäran om ändring av befintligt material i DAM är ett exempel på en relevant uppdatering. Den ska lagras och versionshanteras i DAM för vidare referens eller för att återgå till den tidigare versionen.

Nedan följer exempel på uppdateringar som vanligtvis inte är relevanta:

* Tidiga versioner av mediefiler som överförts innan de är klara för marknadsföringsgranskning
* Vanliga kreativa förändringar av resursen i den pågående arbetsfasen innan kreatörer och marknadsförare bestämmer sig för att resursen är klar

### Användaråtkomst till DAM {#user-access-to-dam}

AEM Assets stöder två typer av användare baserat på deras åtkomst till AEM Assets-distributionen. Vanligtvis har användare i företagsnätverket (brandväggen) direktåtkomst till DAM. Andra användare utanför företagsnätverket skulle inte ha direkt åtkomst. Användartypen avgör vilka integreringar som kan användas ur teknisk synpunkt.

#### Kreativa användare med direkt åtkomst till DAM {#creative-users-with-direct-access-to-dam}

Vanligtvis har interna kreativa team, byråer/kreatörer som är anställda på det interna nätverket tillgång till DAM-instansen, inklusive AEM-inloggning. AEM och nätverksinfrastruktur kan konfigureras för att ge direktåtkomst till externa parter - vanligen betrodda organisationer som byråer som arbetar för en kund - för att få åtkomst till AEM via nätverket, till exempel via VPN eller IP-vitlista.

I sådana fall ger Adobe Asset Link eller AEM-skrivbordsappen enkel åtkomst till det slutliga/godkända materialet och gör att du kan spara kreativa resurser på DAM.

#### Kreativa användare utan åtkomst till DAM {#creative-users-without-access-to-dam}

Externa byråer och frilansare som inte har direkt åtkomst till DAM-instansen kan behöva åtkomst till godkända resurser eller lägga till sina nya designer i DAM.

Använd följande strategier för att ge tillgång till slutliga/godkända mediefiler:

* Använd skrivbordsappen om Asset Link inte fungerar.
* Använd [AEM Assets Brand Portal](https://helpx.adobe.com/experience-manager/brand-portal/user-guide.html) för säker distribution av material till externa partners
* Använd en anpassad implementering av en distributions- och källportal baserad på [resursdelningskommentarer](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* Använd åtkomstkontrollen som konfigurerats i AEM och nödvändig nätverksinfrastruktur (till exempel vitlista för VPN och IP) för att ge externa parter åtkomst till ett dedikerat innehållsområde i din DAM. De kan använda AEM Web UI för att hämta resurser och överföra nytt innehåll till din DAM.

#### Pågående arbete med resurser från AEM {#work-in-progress-on-assets-from-aem}

Som beskrivs i det här dokumentet rekommenderar vi att du utför större uppdateringar av resurser, ibland kallat pågående arbete, utan att ha alla redigeringar sparade i den lokala filen överförda till AEM som ändringar. Detta snabbar upp arbetet för en stationär användare, begränsar den nätverksbandbredd som används och håller resursernas tidslinje ren och fokuserad på kontrollerade, viktiga uppdateringar.

Adobe Asset Link har ett bra stöd för detta:

* När användare i Photoshop, InDesign eller Illustrator tänker redigera en fil utför de en utcheckningsåtgärd på den angivna resursen
* Resursen hämtas i bakgrunden, läggs till användare Creative Cloud-kontot synkroniserat med disken av Creative Cloud-datorprogrammet och utcheckningsflaggan aktiveras i AEM på resursen för att minimera redigeringskonflikter
* Därifrån arbetar användaren i en fil som lagras lokalt på den synkroniserade platsen och kan fortsätta att arbeta och spara nödvändiga ändringar med den frekvens som behövs
* Eftersom resursen finns på Creative Cloud-kontot är den dessutom tillgänglig på andra enheter som användaren kan ha (till exempel kan öppnas eller redigeras i en dedikerad Creative Cloud-mobilapp) och kan delas med andra Creative Cloud-användare i samarbetssyfte.
* När den kreativa användaren är klar med ändringarna kan han/hon utföra en incheckningsåtgärd för filen i sitt Creative Cloud-program, med en valfri kommentar. Motsvarande resurs i AEM versionshanteras och uppdateras till med den nya binärfilen. AEM-användare som marknadsförare eller LOB-användare har tillgång till större förändringar av tillgångar, eller milstolpar, via tidslinjen för AEM-resurser.

AEM-skrivbordsappen ger en nätverksresurs för resurser som öppnas i det ursprungliga programmet. Som standard överförs alla ändringar som görs lokalt till AEM automatiskt efter en kort stund. Med en sådan konfiguration överförs frekventa besparingar under den pågående arbetsfasen till AEM och versionshantering, vilket skapar en stor mängd nätverkstrafik och potentiella skalbarhetsproblem - för att inte tala om onödiga versioner i AEM.

Det rekommenderade sättet här är att använda ett alternativ i AEM-skrivbordsappen för att inaktivera automatiska uppdateringar och överföra ändringar av resurser till AEM manuellt, med hjälp av åtgärden för överföring av ändringar i programmets resursstatusgränssnitt.

#### Massöverföring till DAM {#bulk-upload-to-dam}

Du kan behöva överföra ett större antal filer till DAM samtidigt i vissa scenarier, till exempel:

* Överföra resultat från fotoprojekt eller större projekt
* Överföra material från reklambyråer
* Överför markerade resurser från en större uppsättning om markeringen görs utanför DAM

Observera att den här beskrivningen avser att överföra filer operativt (till exempel varje vecka eller med varje fotografering), som en normal del av datoranvändarens arbetsflöde. Stora resursmigreringar beskrivs inte här.

Du kan använda följande överföringsfunktioner:

* Om du vill överföra stora/hierarkiska mappar i grupp använder du AEM-datorprogrammet som har funktioner för [mappöverföring](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app.html#bulkupload) . Du kan också överföra hierarkiska mappstrukturer. Resurserna överförs i bakgrunden och är därför inte knutna till en webbläsarsession
* Om du vill överföra några filer från en enda mapp drar du filerna direkt till webbgränssnittet eller använder alternativet Skapa i webbgränssnittet för AEM Resurser.
* Beroende på vilka affärskrav du har kan du även använda en anpassad överförare.

#### Hantera digitala resurser direkt från datorn {#managing-digital-assets-directly-from-desktop}

Om du använder Network File Shares för att hantera digitala resurser kan du se att bara den nätverksresurs som är mappad av AEM-skrivbordsappen används som ett praktiskt alternativ. När du övergår från filresurser i nätverk innehåller AEM-webbgränssnittet en omfattande uppsättning funktioner för hantering av digitala resurser, som går mycket längre än vad som är möjligt på en nätverksresurs (sökning, samlingar, metadata, samarbete, förhandsvisningar och så vidare), och AEM-datorprogrammet är en praktisk länk för att ansluta DAM-databasen på serversidan med datorarbetet.

Undvik att använda AEM-datorprogrammet för att hantera resurser direkt i nätverksresursen för AEM Assets. Undvik till exempel att använda AEM-skrivbordsappen för att flytta/kopiera flera filer. Använd i stället webbgränssnittet för AEM Resurser för att dra mappar från Finder/Explorer till nätverksresursen eller använd funktionen för överföring av AEM Resursmapp.

<!-- 
#### Asset migration {#asset-migration}

To plan and execute asset migrations from existing system to a new system or migration of large volume of assets stored on servers, see the [Migration Guide](/help/assets/assets-migration-guide.md). AEM desktop app and AEM to Creative Cloud integrations do not support such migrations. Due to the large volumes of assets to be ingested, and additional requirements around metadata mapping, transformation, and ingestion, migrations should be handled using different tools and approaches.
-->
