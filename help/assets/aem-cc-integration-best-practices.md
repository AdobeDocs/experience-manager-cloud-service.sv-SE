---
title: Bästa tillvägagångssätt att integrera med  [!DNL Adobe Creative Cloud]
description: Bästa praxis är att integrera en Experience Manager-driftsättning med Adobe Creative Cloud för att effektivisera arbetsflöden för överföring av resurser och uppnå maximal effektivitet.
contentOwner: AG
mini-toc-levels: 1
feature: Collaboration, Adobe Asset Link, Desktop App
role: User, Architect, Admin
exl-id: cbed0d62-5148-45eb-b6a0-9fd164060fdc
source-git-commit: 9c1104f449dc2ec625926925ef8c95976f1faf3d
workflow-type: tm+mt
source-wordcount: '3438'
ht-degree: 12%

---

# Bästa praxis för integrering av Adobe Experience Manager och Creative Cloud {#aem-and-creative-cloud-integration-best-practices}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/aem-cc-integration-best-practices.html?lang=en) |
| AEM as a Cloud Service | Den här artikeln |

Adobe Experience Manager Assets är en DAM-lösning (Digital Asset Management) som kan integreras med Adobe Creative Cloud för att hjälpa DAM-användare att samarbeta med kreativa team och effektivisera samarbetet när det gäller att skapa innehåll.

Adobe Creative Cloud förser kreativa team med ett ekosystem av lösningar och tjänster som hjälper dem att skapa digitala resurser. Det omfattar dator- och mobilapplikationer, molntjänster som lagring med datorsynkronisering eller webbupplevelse samt marknadsplatser som Adobe Stock.

Läs vidare för att ta reda på vilka integreringar som du ska välja mellan stationär dator och företagsspecifik DAM baserat på ditt användningsfall och vilka metoder som är associerade med de sammankopplade arbetsflödena.

>[!NOTE]
>
>Mappdelning mellan Experience Manager och Creative Cloud är nu föråldrat och beskrivs inte längre nedan. Adobe rekommenderar nyare funktioner som Adobe Asset Link eller Experience Manager för att ge kreativa användare tillgång till de resurser som hanteras i Experience Manager.

## Collaboration behov av kreatörer, marknadsförare och DAM-användare {#collaboration-need-of-creatives-marketers-and-dam-users}

| Krav | Använd skiftläge | Involverade ytor |
|---|---|---|
| Förenkla för kreatörer på datorn | Effektivisera åtkomsten till resurser från ett DAM-system ([!DNL Assets]) för kreatörer, eller mer allmänt för användare på datorer som arbetar i program för att skapa interna resurser. De behöver ett enkelt och enkelt sätt att upptäcka, använda (öppna), redigera och spara ändringar i Experience Manager samt överföra nya filer. | Windows- eller Mac-program; Creative Cloud-program |
| Tillhandahåll högkvalitativa, färdiga resurser från [!DNL Adobe Stock] | Marknadsförarna hjälper till att snabba upp processen för att skapa innehåll genom att hjälpa till med materialanskaffning och identifiering. Creative använder det godkända materialet direkt inifrån de kreativa verktygen. | [!DNL Assets]; [!DNL Adobe Stock] Marketplace; metadatafält |
| Distribuera och dela resurser efter organisationer | Interna avdelningar/lokala kontor och externa partners, distributörer och byråer använder det godkända material som delas av huvudorganisationen. Organisationen vill säkert och smidigt dela de skapade resurserna för vidare återanvändning. | [!DNL Brand Portal], [!DNL Asset Share Commons] |
| Generera fördefinierade variationer av överförda resurser automatiskt | Bearbeta material automatiskt med Adobe unika mediehanterings- och omvandlingsteknik för fördefinierade åtgärder. Skapa egen logik för att definiera egna åtgärder med API:er och tillgångsmikrotjänster. | Användargränssnittet [!DNL Assets] |

## Adobe lösningar för samverkan {#adobe-offerings-to-support-the-collaboration-need}

| Värdeförslag för berörda personer | Adobe | Involverade ytor |
|---|---|---|
| Creative-användare upptäcker resurser från [!DNL Experience Manager], öppnar och använder dem, redigerar och överför ändringar till [!DNL Experience Manager] och överför nya filer till [!DNL Experience Manager], utan att lämna sin [!DNL Creative Cloud]-app. | [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html) | Photoshop, Illustrator och InDesign. |
| Affärsanvändare förenklar öppning och användning av resurser, redigering och överföring av ändringar till [!DNL Experience Manager] samt överföring av nya filer till [!DNL Experience Manager] från skrivbordsmiljön. De använder en allmän integrering för att öppna alla resurstyper i det inbyggda datorprogrammet, inklusive sådana som inte är från Adobe. | [[!DNL Experience Manager] skrivbordsapp](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html) | Experience Manager datorprogram på Win och Mac |
| Marknadsförare och affärsanvändare upptäcker, förhandsgranskar, licensierar och sparar Adobe Stock-resurser och hanterar dem inifrån Experience Manager. Licensierade och sparade mediefiler innehåller utvalda Adobe Stock-metadata för bättre styrning. | [Integrering med Experience Manager och Adobe Stock](aem-assets-adobe-stock.md) | Webbgränssnittet [!DNL Experience Manager] |
| Förbättra samarbetet mellan designers och marknadsförare av digitala produkter. Låt designers använda digitalt material i design- och trådramsmodeller på Adobe XD Canvas. | [[!DNL Adobe Asset Link] for [!DNL Adobe XD]](https://helpx.adobe.com/enterprise/using/adobe-asset-link-for-xd.html) | [!DNL Adobe XD] |
| Marknadsförarna kan automatiskt skapa variationer och derivat baserade på överförda tillgångar och fördefinierade åtgärder som skapats med anpassning. Använd den här automatiseringen för att förbättra innehållets hastighet och minska den manuella ansträngningen. | [Automatisering av innehåll](/help/assets/cc-api-integration.md) | Webbgränssnittet [!DNL Experience Manager Assets] |

Den här artikeln fokuserar främst på de två första aspekterna av samarbetsbehovet. Distribution och anskaffning av resurser i stor skala omnämns kortfattat som ett användningsexempel. Överväg Adobes varumärkesportal eller Assets Share Commons för sådana behov. Alternativa lösningar som [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html), lösningar som kan byggas baserat på [Resursdelningskomponenter](https://opensource.adobe.com/asset-share-commons/), [Länkdelning](share-assets.md), med [Experience Manager Assets webbgränssnitt](/help/assets/manage-digital-assets.md) bör granskas utifrån specifika krav.

![Creative Cloud-anslutningar för Experience Manager: Avgör vilka funktioner som ska användas](assets/creative-connections-aem.png)

Bestäm vilka funktioner som ska användas

### Mappning av användningsfall och Adobe-lösningar {#mapping-of-use-cases-and-adobe-solutions}

| Använd skiftläge | Adobe Asset Link | Experience Manager datorprogram | Anmärkningar eller alternativa metoder |
|----------------------------------------------------------|-----------------------------------------------------------------------------------|--------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|
| Upptäck - bläddra bland mappar | Ja | Experience Manager Web UI + skrivbordsåtgärder | När du bläddrar i nätverksresursen ska du inaktivera miniatyrbilderna för att undvika att hämta binära filer med resurser. |
| Upptäck - få tillgång till samlingar | Ja | Experience Manager Web UI + skrivbordsåtgärder |  |
| Upptäck - sök efter resurser | Ja | Experience Manager Web UI + skrivbordsåtgärder |  |
| Använd - öppen resurs | Ja | Ja - för alla appar | [Öppna från webbgränssnittet](/help/assets/manage-digital-assets.md#previewing-assets) eller från Finder |
| Använd - placera resurser från Experience Manager i ett dokument | Ja - inbäddning | Ja - länkning eller inbäddning | Experience Manager datorprogram ger åtkomst till resurser som filer i det lokala filsystemet. De här länkarna i de ursprungliga programmen representeras av lokala sökvägar. |
| Redigera - öppna för redigering | Ja - utcheckningsåtgärd | Ja - Öppna åtgärd (i nätverksresursen) | [Utcheckning i AAL](https://helpx.adobe.com/se/enterprise/using/manage-assets-using-adobe-asset-link.html) sparar resursen i användarens Creative Cloud-lagringskonto (synkroniserat med Creative Cloud-appen) som standard. |
| Redigera - pågående arbete utanför Experience Manager | Ja - Tillgångar som är tillgängliga i användarens Creative Cloud-lagringskonto synkroniserade med skrivbordet. | Ja |  |
| Redigera - ladda upp ändringar | Ja - [Incheckningsåtgärd](https://helpx.adobe.com/se/enterprise/using/manage-assets-using-adobe-asset-link.html) med valfri kommentar | Ja |  |
| Överför - en fil | Ja - överför aktuellt aktivt dokument | Ja | [Överför via webbgränssnitt](/help/assets/manage-digital-assets.md#uploading-assets) |
| Överför - flera filer/hierarkiska mappstrukturer | Nej | Ja | [Överför via webbgränssnitt](/help/assets/manage-digital-assets.md#uploading-assets); Anpassade skript eller verktyg |
| Diverse - användare och inloggning | Creative Cloud-användare som är inloggad på Creative Cloud datorprogram blir igenkända (SSO) | Experience Manager-användare / inloggning | Användare av båda lösningarna räknas av mot Experience Manager användarkvot. |
| Diverse - nätverk och åtkomst | Kräver åtkomst från användarens skrivbord till Experience Manager via nätverket | Kräver åtkomst från användarens skrivbord till Experience Manager via nätverket | Adobe Asset Link delar inte nätverksproxymiljö. |


<!-- Removing this row from table as migration guide is not yet final.
| Misc - Migrate large number of assets | No | No | [Migration Guide](/help/assets/assets-migration-guide.md) |
-->

Ta hänsyn till följande alternativ om du vill stödja användningsexempel för resursfördelning:

* [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) för ett konfigurerbart tillägg till Assets för publicering av resurser.

* Anpassade lösningar skapas baserat på kodbasen [Resursdelningskommandon](https://opensource.adobe.com/asset-share-commons/).
* Experience Manager [link share](/help/assets/share-assets.md) om du vill dela resurser på begäran med hjälp av länkar.
* [Assets webbgränssnitt](/help/assets/manage-digital-assets.md) med områden för externa parter som skyddas av Experience Manager Access Control-installationen och med nödvändiga IT-/nätverkskonfigurationsjusteringar, vilket ger dessa externa användare åtkomst till Experience Manager.

## Viktiga begrepp och användningsområden {#key-concepts-and-use-cases}

### Ordlista med vanliga termer {#glossary-of-common-terms}

* **Pågående arbeten eller pågående designarbeten (WIP):** En fas i en resurs livscykel där den genomgår flera ändringar och oftast inte är redo att delas med större team.
* **Designresurser:** Resurser som är klara att delas med ett större team eller som har valts ut/godkänts av designteamet för att delas med marknadsförings- eller affärsområdesteam.

* **Godkännanden av resurser:** Godkännandeprocessen som körs för resurser som redan har överförts till DAM, som vanligtvis omfattar varumärkesgodkännanden, juridiska godkännanden och så vidare.
* **Slutlig resurs:** En resurs som har genomgått alla godkännanden och all metadatataggning och är klar att användas av teamet. En sådan resurs lagras i DAM och är tillgänglig för alla (intresserade) användare. Den kan användas i marknadsföringskanaler eller av designteam för att skapa material.

* **Mindre uppdatering/ändring av resurs:** En snabb och liten ändring av en digital resurs. Ändringarna är ofta retuscheringar, smärre redigeringar, resursgranskningar eller godkännanden (t.ex. omplacering, ändring av textstorlek, justering av mättnad/intensitet eller färg).
* **Större uppdatering/ändring av resurs:** En arbetskrävande ändring av en digital resurs, som ibland tar lång tid att genomföra. Den omfattar vanligtvis flera ändringar. Resursen måste sparas flera gånger medan den uppdateras. Större resursuppdateringar medför oftast att resursen får statusen pågående arbete.
* **DAM:** Digitalt resurshanteringssystem. I det här dokumentet är det synonymt med Experience Manager Assets, om inget annat anges.
* **Designanvändare:** En kreatör som skapar digitalt material med Creative Cloud-program och -tjänster. I vissa fall är designanvändaren medlem i ett designteam och kan använda Creative Cloud, men skapar inte digitala resurser (som en designchef eller designteamschef).
* **DAM-användare:** En typisk användare av ett DAM-system. Beroende på organisationen kan en DAM-användare vara en marknadsföringsanvändare eller en icke-marknadsföringsanvändare, till exempel en LOB-användare (Line-of-Business), bibliotekarie, säljare osv.

### Att tänka på vid användning av Experience Manager- och Creative Cloud-integration {#considerations-when-using-aem-and-creative-cloud-integration}

<!--incomplete and TBD: 

* DA2.0 best practices: See troubleshooting.md
* Stock integration: See ?
* AAL: See ?
* BP: See ?

-->

Här följer en kort sammanfattning av de effektivaste strategierna för Experience Manager och Creative Cloud Integration. Läs resten av det här dokumentet för att få en mer detaljerad förståelse för dessa.

* **För kreativa användare som arbetar i Photoshop, InDesign eller Illustrator:** Adobe Asset Link ger den bästa användarupplevelsen, inklusive ren hantering av pågående arbeten på resurser som checkats ut från Experience Manager
* **Använd Experience Manager-datorprogrammet för att förenkla åtkomst till resurser från skrivbordet för alla generiska filformat eller program:**
* **Förstå varför och när resurser ska lagras i DAM:** Uppdateringar som ska göras tillgängliga för hela teamet i organisationen
* **Tänk på mängden resurser som delas:** Om ni använder mediedistribution kan styrning och säkerhet vara de viktigaste aspekterna. Överväg att använda verktyg som är byggda för att göra detta i stor skala, som varumärkesportalen.
* **Förstå resursers livscykel:** Ta reda på hur resurser hanteras i organisationen av olika team
* **Var försiktig med ofta sparade resurser:** Adobe Asset Link tar hand om det med PS, AI och ID. För andra program ska du inte utföra pågående uppgifter i mappad/delad mapp såvida du inte behöver alla ändringar i DAM

### Tillgång till Adobe Stock-material från Experience Manager Assets {#access-to-adobe-stock-assets-from-aem-assets}

Integreringen av [Experience Manager och Adobe Stock](/help/assets/aem-assets-adobe-stock.md) ger Experience Manager-användare möjlighet att söka efter, förhandsgranska, licensiera och spara resurser från Adobe Stock i Experience Manager. Licensierade och sparade Adobe Stock-resurser har valt Stock-metadata som kan användas för att söka efter dem med extra filter.

Några viktiga punkter om den här integreringen:

* När resurser från Adobe Stock sparas till Experience Manager blir de ett vanligt Experience Manager Assets med binära lager sparade i Experience Manager-databasen. Vissa metadata som är relaterade till Adobe Stock sparas för resursen i Experience Manager, i annat fall ser det ut som för andra filer. Om till exempel smarta taggar är aktiva läggs taggarna till i de här resurserna när de sparas.
* Resursen som sparas till Experience Manager är en kopia, inte en länk tillbaka till Adobe Stock.

**Arbeta med resurser som sparats från Adobe Stock till Experience Manager i Creative Cloud**. Den här integreringen är oberoende av Adobe Asset Link, men Adobe Asset Link känner igen dessa resurser som sparats från Stock på det sättet och visar ytterligare metadata och Stock-ikoner för dessa resurser i Adobe Asset Link-tilläggets gränssnitt i Photoshop, Illustrator eller InDesign. Filerna är tillgängliga för att bläddra, öppna och så vidare, eftersom de är vanliga Experience Manager-resurser när de sparas i Experience Manager.
Creative-användare som arbetar i Creative Cloud-program med Adobe Asset Link kan, förutom att ha tillgång till redan licensierade mediefiler från Adobe Stock till Experience Manager, även använda Creative Cloud Libraries-panelen för att söka efter, förhandsgranska och licensiera Adobe Stock-mediefiler.
Assets från Adobe Stock som licensierats och sparats i Experience Manager blir tillgängliga för de större team som har tillgång till Experience Manager Assets-distributionen, medan kreatörer som licensierar mediefiler från Adobe Stock via Creative Cloud Libraries-panelen endast gör dem tillgängliga för sig själva som standard på sitt Creative Cloud-konto.

## Lagra resurser i ett resurshanteringssystem {#about-storing-assets-in-a-dam}

För att skapa ett effektivt arbetsflöde mellan kreatörer och marknadsförare/branschspecifika team (LOB) och välja de bästa supportfunktionerna är det viktigt att förstå när och varför resurser lagras i DAM.

### Varför resurser lagras i DAM {#why-assets-are-stored-in-dam}

Genom att lagra resurser i DAM blir de enkelt tillgängliga och sökbara. Det ser till att resurserna kan användas av många användare i organisationen eller ekosystemet, bland annat partners, kunder och så vidare.

De flesta organisationer väljer att endast lagra resurser som är relevanta för marknadsförings-/LOB-processerna längre fram i kedjan (publicera till kanaler som webbkanaler via Experience Manager Sites eller andra kanaler som tillhandahålls av Adobe Experience Cloud - Marketing Cloud, Advertising Cloud och mäts av Analytics Cloud, som tillhandahåller till användare/partner osv.). Dessutom lagrar organisationer resurser som kan bli föremål för en gransknings-/godkännandeprocess i DAM. På så sätt lagrar DAM mest resurser som har stora chanser att användas och undviker att lagra inaktiva resurser.

Lagring av resurser är också beroende av tekniska aspekter och resursanvändning. DAM tillhandahåller ytterligare tjänster runt lagrade resurser, inklusive extrahering av metadata, versionshantering, generering av förhandsgranskning/omkodning, hantering av referenser och tillägg av åtkomstkontrollsinformation. Dessa tjänster kräver extra tid och infrastrukturresurser.

Det är ofta inte önskvärt att lagra alla resurser och uppdateringar. Om till exempel uppdateringar av specifika resurser har dålig kvalitet och förbrukar för mycket resurser, kanske resurserna inte lagras i DAM.

#### När resurser lagras i DAM {#when-assets-are-stored-in-dam}

Creative team (och organisationer) är vanligtvis inte intresserade av att lagra resurser i varje skede av resursens livscykel. De undviker till exempel att lagra resurser i följande fall:

* Assets som ännu inte är klara eller som är föremål för experimenterande
* Assets som inte klarar granskningsprocessen
* Jämfört med den aktuella resursen har teamet bättre kandidater att representera sitt arbete för externa team

Vanligtvis lagras följande klassresurser i DAM:

* Assets som nått en viss mognad och anses vara redo att delas
* Assets som har förvalts av det kreativa teamet
* Specifika resursformat som kan användas eller begäras av marknadsföring, beroende på ett specifikt kontrakt eller avtal (t.ex. JPG-filer som konverterats från RAW-filer, TIFF-filer/bilder från PSD-original)

#### När resursuppdateringar lagras i DAM {#when-updates-to-assets-are-stored-in-dam}

I regel ska endast uppdateringar av resurser som är relevanta för den bredare uppsättningen DAM-användare lagras i DAM. Det ser till att användare (marknadsföringsfunktioner och liknande funktioner) bara kan se relevanta versioner på tidslinjen för DAM-resurser.

Vanligtvis ändras relaterade till viktiga milstolpar i resursens livscykel. Den initiala marknadsföringsfärdiga resursen eller en officiell uppdatering som baseras på begäran/granskning som tillhandahålls av det kreativa teamet bör till exempel lagras och versionshanteras i DAM.

Det kreativa teamets uppdatering för granskning av marknadsföringsteamet efter en begäran om ändring av befintligt material i DAM är ett exempel på en relevant uppdatering. Den ska lagras och versionshanteras i DAM för vidare referens eller för att återgå till den tidigare versionen.

Nedan följer exempel på uppdateringar som vanligtvis inte är relevanta:

* Tidiga versioner av mediefiler som överförts innan de är klara för marknadsföringsgranskning
* Vanliga kreativa förändringar av resursen i den pågående arbetsfasen innan kreatörer och marknadsförare bestämmer sig för att resursen är klar

### Användaråtkomst till DAM {#user-access-to-dam}

Experience Manager Assets stöder två typer av användare baserat på deras åtkomst till Experience Manager Assets-distributionen. Vanligtvis har användare i företagsnätverket (brandväggen) direktåtkomst till DAM. Andra användare utanför företagsnätverket skulle inte ha direkt åtkomst. Användartypen avgör vilka integreringar som kan användas ur teknisk synpunkt.

#### Creative-användare med direktåtkomst till DAM {#creative-users-with-direct-access-to-dam}

Vanligtvis har interna kreativa team, byråer/kreatörer som är anställda på det interna nätverket tillgång till DAM-instansen, inklusive Experience Manager-inloggning. Experience Manager och nätverksinfrastruktur kan konfigureras för att ge direktåtkomst till externa parter - vanligen betrodda organisationer som byråer som arbetar för en kund - för att få åtkomst till Experience Manager via nätverk, till exempel via VPN eller IP tillåtelselista.

I sådana fall ger Adobe Asset Link eller Experience Manager datorprogram enkel åtkomst till det slutliga/godkända materialet och gör att du kan spara kreativa resurser på DAM.

#### Creative-användare utan åtkomst till DAM {#creative-users-without-access-to-dam}

Externa byråer och frilansare som inte har direkt åtkomst till DAM-instansen kan behöva åtkomst till godkända resurser eller lägga till sina nya designer i DAM.

Använd följande strategier för att ge tillgång till slutliga/godkända mediefiler:

* Använd skrivbordsappen om Asset Link inte fungerar.
* Använd [Experience Manager Assets Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html) för säker distribution av resurser till externa partner
* Använd en anpassad implementering av en distributions- och källportal baserad på [Resursdelningskommentarer](https://adobe-marketing-cloud.github.io/asset-share-commons/)
* Använd den åtkomstkontroll som har konfigurerats i Experience Manager och nödvändig nätverksinfrastruktur (till exempel VPN och IP) för att ge externa parter åtkomst till ett dedikerat innehållsområde i din DAM. De kan använda Experience Manager Web UI för att hämta resurser och överföra nytt innehåll till din DAM.

#### Pågående arbete med resurser från Experience Manager {#work-in-progress-on-assets-from-aem}

Som beskrivs i det här dokumentet rekommenderar vi att du utför större uppdateringar av resurser, ibland kallat pågående arbete, utan att ha alla redigeringar sparade i den lokala filen överförda till Experience Manager som ändringar. Detta snabbar upp arbetet för en stationär användare, begränsar den nätverksbandbredd som används och håller resursernas tidslinje ren och fokuserad på kontrollerade, viktiga uppdateringar.

Adobe Asset Link har ett bra stöd för detta:

* När användare i Photoshop, InDesign eller Illustrator vill redigera en fil utför de en utcheckningsåtgärd för den aktuella resursen
* Resursen hämtas i bakgrunden, läggs till användare Creative Cloud-kontot synkroniserat med disken via Creative Cloud datorprogram och utcheckningsflaggan aktiveras i Experience Manager för att minimera redigeringskonflikter
* Därifrån arbetar användaren i en fil som lagras lokalt på den synkroniserade platsen och kan fortsätta att arbeta och spara nödvändiga ändringar med den frekvens som behövs
* Eftersom resursen finns på Creative Cloud-kontot är den också tillgänglig på andra enheter som användaren kan ha (till exempel kan öppnas eller redigeras i en dedikerad Creative Cloud-mobilapp) och kan delas med andra Creative Cloud-användare i samarbetssyfte.
* När den kreativa användaren är klar med ändringarna kan han/hon utföra en incheckningsåtgärd för filen i sitt Creative Cloud-program, med en valfri kommentar. Motsvarande resurs i Experience Manager versionshanteras och uppdateras till med den nya binärfilen. Experience Manager-användare som marknadsförare eller LOB-användare har tillgång till större förändringar av tillgångar, eller milstolpar, via Experience Manager tidslinjegränssnitt för mediefiler.

Experience Manager skrivbordsapp har en nätverksresurs för resurser som öppnas i det ursprungliga programmet. Som standard överförs alla ändringar som görs lokalt till Experience Manager automatiskt efter en kort stund. Med en sådan konfiguration överförs ofta sparande under den pågående arbetsfasen till Experience Manager och versionsindelas, vilket skapar en stor mängd nätverkstrafik och potentiella skalbarhetsproblem - för att inte tala om onödiga versioner i Experience Manager.

Det rekommenderade sättet här är att använda ett alternativ i Experience Manager-datorprogrammet för att inaktivera automatiska uppdateringar och överföra ändringar av resurser till Experience Manager manuellt, med hjälp av åtgärden för överföring av ändringar i programmets resursstatusgränssnitt.

#### Massöverföring till DAM {#bulk-upload-to-dam}

Du kan behöva överföra ett större antal filer till DAM samtidigt i vissa scenarier, till exempel:

* Överföra resultat från fotoprojekt eller större projekt
* Överföra material från reklambyråer
* Överför markerade resurser från en större uppsättning om markeringen görs utanför DAM

Den här beskrivningen avser att överföra filer operativt (till exempel varje vecka eller med varje fotografering), som en normal del av datoranvändarens arbetsflöde. Stora resursmigreringar beskrivs inte här.

Du kan använda följande överföringsfunktioner:

* Om du vill överföra stora/hierarkiska mappar samtidigt använder du Experience Manager-datorprogrammet som har [mappöverföringsfunktioner](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#bulk-upload-assets). Du kan också överföra hierarkiska mappstrukturer. Assets överförs i bakgrunden och är därför inte knutet till någon webbläsarsession
* Om du vill överföra några filer från en enda mapp drar du filerna direkt till webbgränssnittet eller använder alternativet Skapa i Experience Manager Assets webbgränssnitt.
* Beroende på vilka affärskrav du har kan du även använda en anpassad överförare.

#### Hantera digitala resurser direkt från datorn {#managing-digital-assets-directly-from-desktop}

Om du använder Network File Shares för att hantera digitala resurser kan du se att bara den nätverksresurs som är mappad av Experience Manager-datorprogrammet används som ett praktiskt alternativ. När du övergår från filresurser i nätverk har Experience Manager webbgränssnitt en mängd funktioner för hantering av digitala resurser som går mycket längre än vad som är möjligt på en nätverksresurs (sökning, samlingar, metadata, samarbete, förhandsvisningar och så vidare), och Experience Manager datorprogram erbjuder en praktisk länk för att ansluta DAM-databasen på serversidan med datorarbetet.

Undvik att använda Experience Manager datorprogram för att hantera mediefiler direkt i Experience Manager Assets nätverksresurs. Undvik till exempel att använda Experience Manager datorprogram för att flytta/kopiera flera filer. Använd i stället Experience Manager Assets webbgränssnitt för att dra mappar från Finder/Utforskaren till nätverksresursen eller använd funktionen Experience Manager Assets mappöverföring.

**Se även**

* [Översätt Assets](translate-assets.md)
* [ASSETS HTTP API](mac-api-assets.md)
* [Filformat som stöds av Assets](file-format-support.md)
* [Sök resurser](search-assets.md)
* [Anslutna resurser](use-assets-across-connected-assets-instances.md)
* [Resursrapporter](asset-reports.md)
* [Metadata-scheman](metadata-schemas.md)
* [Hämta resurser](download-assets-from-aem.md)
* [Hantera metadata](manage-metadata.md)
* [Sök efter ansikten](search-facets.md)
* [Hantera samlingar](manage-collections.md)
* [Import av massmetadata](metadata-import-export.md)
* [Publicera Assets till AEM och Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)
