---
title: Nu kommer Assets as a Cloud Service för hantering av digitala resurser i AEM
description: Nu kommer Assets as a Cloud Service för hantering av digitala resurser i AEM
exl-id: 4437f214-d058-4975-8b8f-869a12c8103b
source-git-commit: c3a528d7e903b43f6b9a18b2426a04638b086d38
workflow-type: tm+mt
source-wordcount: '5032'
ht-degree: 0%

---

# Nu kommer Assets as a Cloud Service för hantering av digitala resurser i AEM {#assets-as-cloud-service-digital-asset-management-aem}

Adobe Experience Manager Assets as a Cloud Service är en molnbaserad, Adobe PaaS-lösning som gör att företag inte bara kan utföra sina Digital Asset Management- och Dynamic Media-åtgärder snabbt och effektivt, utan även använda nästa generations smarta funktioner, som AI/ML, inifrån ett system som alltid är aktuellt, alltid tillgängligt och alltid håller på att lära sig.

Adobe erbjuder robusta DAM-lösningar (Digital Asset Management) så att ni får ut mesta möjliga av era digitala resurser. Adobe Experience Manager Assets har två separata upplevelser som använder samma molntjänstdatabas för att passa era behov. Mer information om personliga upplevelser för AEM Assets finns i [Tillgängliga personbaserade upplevelser för hantering av digitala resurser](#persona-based-experiences).

Mer information om AEM Assets Ultimate och AEM Assets Prime finns i [Assets as a Cloud Service Ultimate](/help/assets/assets-ultimate-overview.md) och [Assets as a Cloud Service Prime](/help/assets/assets-prime.md).

Några av de viktigaste funktionerna i Adobe Digital Asset Management:

![add-tags](assets/aem-assets-features-landing-page.png)


>[!BEGINTABS]

>[!TAB Resursintag]

## Tillgångsintag {#asset-ingestion}

Använd bulkimportfunktionen för att importera ett stort antal resurser direkt från en datakälla, till exempel Azure, AWS, Google Cloud, Dropbox och OneDrive, till Assets as a Cloud Service.

Du kan utföra massimportåtgärden i administrationsvyn eller vyn Assets. I Assets-vyn finns fler alternativ för datakällor jämfört med i administrationsvyn.

Förutom webbläsarens användargränssnitt har Experience Manager stöd för andra klienter på datorn. De ger också en uppladdningsupplevelse utan att du behöver gå till webbläsaren.

* Adobe Asset Link ger åtkomst till material från Experience Manager i Adobe Photoshop, Adobe Illustrator och Adobe InDesign. Du kan överföra det öppna dokumentet till Experience Manager direkt från Adobe Asset Link-användargränssnittet från dessa datorprogram.

* Experience Manager datorprogram gör det enklare att arbeta med resurser på datorn, oberoende av filtyp eller vilket program som hanterar dem. Det är användbart att överföra filer i kapslade mapphierarkier från det lokala filsystemet, eftersom webbläsaröverföring bara stöder överföring av platta fillistor.

Använd de här länkarna för att få tillgång till detaljerad dokumentation om dessa verktyg för tillgångsintag:

<table>
<td>
   <a href="/help/assets/bulk-import-assets-view.md">
   <img alt="Verktyget Massimport" src="./assets/bulk-images.jpeg" />
   </a>
   <div>
      <a href="/help/assets/bulk-import-assets-view.md">
      <strong> Använda verktyget Massimport </strong>
      </a>
   </div>
   <p>
      <em>Lär dig hur du importerar ett stort antal resurser direkt från en datakälla</em>
   </p>
</td>


<td>
   <a href="https://experienceleague.adobe.com/sv/docs/experience-manager-desktop-app/using/using">
   <img alt="Använd AEM datorprogram" src="./assets/desktop-app-upload.jpeg" />
   </a>
   <div>
      <a href="https://experienceleague.adobe.com/sv/docs/experience-manager-desktop-app/using/using">
      <strong> Använda AEM-datorprogrammet </strong>
      </a>
   </div>
   <p>
      <em>Lär dig hur du använder AEM skrivbordsapp för att överföra filer i kapslade mapphierarkier från det lokala filsystemet.</em>
   </p>
</td>
<td>
   <a href="https://helpx.adobe.com/se/enterprise/using/adobe-asset-link.html">
   <img alt="Använd Adobe Asset Link" src="./assets/adobe-asset-link.jpeg" />
   </a>
   <div>
      <a href="https://helpx.adobe.com/se/enterprise/using/adobe-asset-link.html">
      <strong> Använd Adobe Asset Link </strong>
      </a>
   </div>
   <p>
      <em>Lär dig hur du överför resurser till Experience Manager med Creative Cloud-program.</em>
   </p>
</td>
</table>

>[!TAB AI-funktioner]

**Smarta taggar**: Smarta taggar använder det artificiellt intelligenta ramverket i Adobe Sensei för att utbilda sin bildigenkänningsalgoritm i din taggstruktur och i din företagsklonomi. Den här innehållsintelligensen används sedan för att tillämpa relevanta taggar på en annan uppsättning resurser. Som standard lägger AEM automatiskt till smarta taggar i överförda resurser.

**Intelligent färgbaserad taggning och sökning**: AEM Assets använder Adobe Sensei AI-funktioner för att skilja mellan färger i en bild och tillämpa dem automatiskt som taggar vid förtäring. Dessa taggar möjliggör en förbättrad sökfunktion baserat på bildens färgkomposition.

**AI-genererade metadata**: AEM Assets använder AI för att automatiskt generera metadata, inklusive rubrik, beskrivning och nyckelord. Dessa AI-genererade fält gör metadata mer korrekta, vilket gör materialet enklare att söka, kategorisera och rekommendera. Detta tillvägagångssätt förbättrar inte bara effektiviteten genom att eliminera manuell taggning, utan garanterar också enhetlighet och skalbarhet för stora volymer digitalt innehåll.

**Byt namn på flera resurser i grupp**: [I Assets-vyn kan du byta namn på flera resurser samtidigt med hjälp av artificiell intelligens](/help/assets/bulk-rename-assets-view.md). Du kan markera flera filer samtidigt och döpa om dem alla samtidigt. Några av de exempel som visas när du byter namn på konversationer är *Ändra alla filer till &#39;min fil&#39; och lägg till ett ökande nummer* och *Prefix för filerna med 001, 002 osv. och översätt till engelska*.

<table>
<td>
   <a href="/help/assets/smart-tags.md">
   <img alt="Smarta taggar i AEM Assets" src="./assets/smart-tags-ai.jpeg" />
   </a>
   <div>
      <a href="/help/assets/smart-tags.md">
      <strong> Lägga till smarta AI-taggar i resurser </strong>
      </a>
   </div>
   <p>
      <em>Lär dig hur du använder smarta taggar automatiskt på överförda resurser.</em>
   </p>
</td>


<td>
   <a href="/help/assets/color-tag-images.md">
   <img alt="Lägg in intelligenta färgbaserade taggar" src="./assets/color-tags.jpg" />
   </a>
   <div>
      <a href="/help/assets/manage-notifications-assets-view.md">
      <strong> Lägg till intelligenta färgbaserade taggar </strong>
      </a>
   </div>
   <p>
      <em>Lär dig hur du använder färgbaserade taggar automatiskt vid förtäring.</em>
   </p>
</td>
<td>
   <a href="/help/assets/metadata-assets-view.md">
   <img alt="AI-genererade metadata" src="./assets/ai-generated-metadata-landing.jpg" />
   </a>
   <div>
      <a href="/help/assets/metadata-assets-view.md">
      <strong> AI-genererade metadata </strong>
      </a>
   </div>
   <p>
      <em>Använd AI för att generera metadata för resurser, till exempel titel och beskrivning. </em>
   </p>
</td>
</table>

**Sammanhangsbaserad sökning**: I AEM Assets kan du söka efter resurser som är tillgängliga i databasen genom att definiera textmeddelanden. Experience Manager Assets omvandlar automatiskt dessa textmeddelanden till sökfilter och visar sökresultaten. Du kan visa och ändra automatiska filter med hjälp av filterpanelen för att begränsa sökresultaten ytterligare. Några av exemplen på konversationstextprompter är *Bilder som är minst 200 pixlar höga och 100 pixlar breda med strand och klar himmel* och *Jag behöver bilder med blå himmel som är 1 500 och 2 500 pixlar höga och som har skapats den senaste månaden och som inte har gått ut och godkänts*.

**Generera resurser med Adobe Firefly i AEM**: Med AEM Assets kan du generera en resurs om sökfrågan inte returnerar några resultat, med Adobe Firefly i realtid. AEM Assets gör det även möjligt att överföra den genererade bilden till AEM Assets-databasen från AEM Assets användargränssnitt.

**Integrering med Adobe Express**: AEM Assets kan integreras direkt med Adobe Express, vilket gör att du kan komma åt resurser som lagras i AEM Assets direkt från Adobe Express användargränssnitt. Du kan också använda Adobe Firefly Artificial Intelligence i Express för att generera bilder med enkla textmeddelanden och placera dem på Express Canvas. Du kan sedan spara nytt eller redigerat innehåll i en AEM Assets-databas.

<table>
<td>
   <a href="/help/assets/search-assets-view.md#contextual-search">
   <img alt="Sammanhangsbaserad sökning" src="./assets/ai-based-search.jpg" />
   </a>
   <div>
      <a href="/help/assets/search-assets-view.md#contextual-search">
      <strong> Sammanhangsbaserad sökning </strong>
      </a>
   </div>
   <p>
      <em>Lär dig hur du söker efter resurser med enkla textmeddelanden.</em>
   </p>
</td>


<td>
   <a href="/help/assets/search-assets-view.md#search-firefly">
   <img alt="Generera resurser med Adobe Firefly" src="./assets/adobe-firefly.jpg" />
   </a>
   <div>
      <a href="/help/assets/search-assets-view.md#search-firefly">
      <strong> Generera resurser med Adobe Firefly </strong>
      </a>
   </div>
   <p>
      <em>Generera resurser i realtid med Adobe Firefly.</em>
   </p>
</td>
<td>
   <a href="/help/assets/native-integration-adobe-express.md">
   <img alt="Integrering med Adobe Express" src="./assets/content-hub-express.jpeg" />
   </a>
   <div>
      <a href="/help/assets/native-integration-adobe-express.md">
      <strong>Integrering med Adobe Express</strong>
      </a>
   </div>
   <p>
      <em>Använd Adobe Express AI-funktioner i AEM Assets användargränssnitt.</em>
   </p>
</td>
</table>

**Smart Imaging**: Smart Imaging ger ännu bättre prestanda för leverans av bildresurser genom att automatiskt optimera en bilds format och filstorlek baserat på en kunds webbläsarkapacitet. Det fungerar med befintliga bildförinställningar och använder intelligens vid leverans. Den här intelligensen minskar bildfilens storlek ytterligare baserat på webbläsarens och nätverkets anslutningshastighet.

**Smart beskärning**: En Adobe Sensei AI-funktion som automatiskt identifierar fokalpunkten i en bild eller video och beskär för att behålla den. Den fångar upp den avsedda intressepunkten oavsett skärmstorlek och eliminerar därmed långtråkiga manuella moment och levererar högkvalitativa, snabba bilder och video som ser bra ut på alla enheter och skärmar.

**AI-genererade videobeskrivningar**: AI-genererade videobeskrivningar i Adobe Dynamic Media använder artificiell intelligens för att generera bildtexter automatiskt för videoinnehåll. Den här funktionen är utformad för att förbättra tillgängligheten och användarupplevelsen genom att ge korrekta bildtexter. Bildtexter genereras från det ursprungliga ljudet, eventuella ytterligare ljudspår eller extra bildtexter finns på fliken `Captions and Audio` på sidan med videoegenskaper. Med stöd för över 60 språk kan bildtexter granskas och förhandsgranskas innan videon publiceras.
<table>
<td>
   <a href="/help/assets/dynamic-media/imaging-faq.md">
   <img alt="Smart bildbehandling" src="./assets/smart-imaging.jpg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media/imaging-faq.md">
      <strong> Smart bildbehandling </strong>
      </a>
   </div>
   <p>
      <em>Optimera bildens format och filstorlek baserat på användarens webbläsarkapacitet och nätverkshastighet.</em>
   </p>
</td>


<td>
   <a href="https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use.html">
   <img alt="Smart beskärning" src="./assets/smart-cropping.jpg" />
   </a>
   <div>
      <a href="https://experienceleague.adobe.com/en/docs/experience-manager-learn/assets/dynamic-media/images/smart-crop-feature-video-use.html">
      <strong> Smart beskärning </strong>
      </a>
   </div>
   <p>
      <em>Använd AI för att automatiskt identifiera brännpunkten i bilder och videoklipp och beskär för att behålla den</em>
   </p>
</td>
<td>
   <a href="/help/assets/dynamic-media/video.md">
   <img alt="AI-genererade videobeskrivningar" src="./assets/videos-with-captions.jpg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media/video.md">
      <strong> AI-genererade videobeskrivningar </strong>
      </a>
   </div>
   <p>
      <em>Använd artificiell intelligens för att generera bildtexter automatiskt för videoinnehåll. </em>
   </p>
</td>
</table>

>[!TAB Resursidentifiering]

## Resursidentifiering {#asset-discovery}

När du har importerat dina mediefiler till AEM Assets är det en utmaning att snabbt hitta rätt mediefiler från en sådan stor samling.

AEM Assets har funktioner som gör det enklare att hitta rätt resurs på nolltid, t.ex. AI-genererad taggning (smarta taggar), anpassade metadata och funktioner som ger en bättre sökupplevelse.

**Metadatahantering**: Metadata är den viktigaste aspekten när du startar resurshanteringsresan. Administratörerna får inte längre kontroll över metadatahanteringen när resurserna distribueras till användarna. Effektiva metadata säkerställer bättre sökning, vilket är det ultimata målet för alla DAM-verktyg.


**Metadata Forms**: Assets as a Cloud Service innehåller många standardmetadatafält som standard. Om du har ytterligare metadatabehov och behöver fler metadatafält för att lägga till företagsspecifika metadata. Med metadataformulär kan företag lägga till anpassade metadatafält på sidan Detaljer för en resurs. De företagsspecifika metadata förbättrar styrningen och identifieringen av dess resurser. Du kan skapa formulär från grunden eller återanvända ett befintligt formulär.

<table>
<td>
   <a href="/help/assets/metadata-assets-view.md">
   <img alt="Hantera metadatavy i Assets" src="./assets/manage-metadata-assets-view.jpeg" />
   </a>
   <div>
      <a href="/help/assets/metadata-assets-view.md">
      <strong>Hantera metadata i Assets-vyn </strong>
      </a>
   </div>
   <p>
      <em>Lär dig hur du hanterar metadata och metadataformulär i Assets-vyn.</em>
   </p>
</td>


<td>
   <a href="https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager-blogs/how-to-manage-metadata-before-and-after-migrating-to-aem-assets/ba-p/744298">
   <img alt="Metadatahantering, god praxis" src="./assets/metadata-best-practices.jpeg" />
   </a>
   <div>
      <a href="https://experienceleaguecommunities.adobe.com/t5/adobe-experience-manager-blogs/how-to-manage-metadata-before-and-after-migrating-to-aem-assets/ba-p/744298">
      <strong> Metadatahantering </strong>
      </a>
   </div>
   <p>
      <em>Lär dig hur du hanterar metadata före och efter att du har migrerat dina resurser till AEM.</em>
   </p>
</td>
<td>
   <a href="/help/assets/manage-metadata.md">
   <img alt="Använd Adobe Asset Link" src="./assets/metadata-management-admin-view.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-metadata.md">
      <strong> Hantera metadata i administrationsvyn </strong>
      </a>
   </div>
   <p>
      <em>Lär dig hur du hanterar metadata och metadataformulär i administratörsvyn.</em>
   </p>
</td>
</table>

**Smarta taggar**: Smarta taggar använder det artificiellt intelligenta ramverket i Adobe Sensei för att utbilda sin bildigenkänningsalgoritm i din taggstruktur och i din företagsklonomi. Den här innehållsintelligensen används sedan för att tillämpa relevanta taggar på en annan uppsättning resurser. Som standard lägger AEM automatiskt till smarta taggar i överförda resurser.

**Sök efter resurser**: När du har rätt metadata på plats kan du söka med olika operatorer, jokertecken, avancerade frågor och anpassade filter i AEM Assets.

**Sammanhangsbaserad sökning**: AEM Assets tillhandahåller också funktionen Sammanhangsbaserad sökning, som gör att du kan söka efter resurser i databasen genom att definiera textmeddelanden. Experience Manager Assets omvandlar automatiskt dessa textmeddelanden till sökfilter och visar sökresultaten. Du kan visa och ändra automatiska filter med hjälp av filterpanelen för att begränsa sökresultaten ytterligare.

<table>
<td>
   <a href="/help/assets/smart-tags.md">
   <img alt="Smarta taggar i AEM Assets" src="./assets/smart-tags-ai.jpeg" />
   </a>
   <div>
      <a href="/help/assets/smart-tags.md">
      <strong> Lägga till smarta taggar i resurser </strong>
      </a>
   </div>
   <p>
      <em>Lär dig hur du använder smarta taggar automatiskt på överförda resurser.</em>
   </p>
</td>


<td>
   <a href="/help/assets/search-assets-view.md">
   <img alt="Sök i Assets" src="./assets/search-assets-view-landing.jpeg" />
   </a>
   <div>
      <a href="/help/assets/search-assets-view.md">
      <strong> Söka efter resurser i Assets-vyn </strong>
      </a>
   </div>
   <p>
      <em>Lär dig hur du effektivt använder kontextuell sökning och andra sökfunktioner i Assets-vyn.</em>
   </p>
</td>
<td>
   <a href="/help/assets/search-best-practices.md">
   <img alt="Sök efter bästa praxis" src="./assets/search-best-practices.jpeg" />
   </a>
   <div>
      <a href="/help/assets/search-best-practices.md">
      <strong> Söka efter bästa praxis </strong>
      </a>
   </div>
   <p>
      <em>Beskriver olika scenarier som hjälper AEM-användare att utföra grundläggande till avancerad sökning.</em>
   </p>
</td>
</table>

>[!TAB Resursstyrning]

## Tillgångshantering och -styrning {#asset-management-governance}

När du har överfört dina resurser till AEM Assets och angett metadata för dem så att de blir lättare att hitta kan du utföra olika åtgärder för hantering av digitala resurser med det användarvänliga gränssnittet i Assets-vyn.

**Resurshanteringsåtgärder**: Vissa av de grundläggande åtgärderna är sök-, hämtnings-, flytt-, kopierings-, byt namn på, ta bort-, uppdatering- och redigeringsåtgärder.

Du kan också underhålla resursversioner, ange resursstatus och ange förfallodatum för tillgångar.

**Min Workspace**: Assets-vyn innehåller även en anpassningsbar arbetsyta som ger smidig åtkomst till viktiga delar av Assets användargränssnitt och den information som är mest relevant för dig. Den här sidan är en helhetslösning som ger en översikt över dina arbetsobjekt och ger snabb åtkomst till viktiga arbetsflöden.

**Content Credentials**: En annan kraftfull funktion som AEM Assets stöder är Content Credentials. Varumärken är mer oroade än någonsin över innehållets transparens, AI-exponering och förhindrande av manipulering av tillgångar. Content Authenticity Initiative (CAI) på Adobe bygger verktyg som är kompatibla med den tekniska standarden Coalition for Content Provenance and Authenticity (C2PA). Content Credentials, som är en ny typ av krypterade, manipuleringssäkra metadata, kan hjälpa tittarna att förstå innehållet och säkerställa varumärkesmaterialets integritet. De kan innehålla ett brett urval av härkomstdata som ger insikter i en digital resursers historia.

<table>
<td>
   <a href="/help/assets/manage-organize-assets-view.md">
   <img alt="Resurshanteringsaktiviteter" src="./assets/asset-management.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-organize-assets-view.md">
      <strong> Resurshanteringsåtgärder </strong>
      </a>
   </div>
   <p>
      <em>Lär dig hur du utför grundläggande och avancerade resurshanteringsåtgärder.</em>
   </p>
</td>


<td>
   <a href="/help/assets/my-workspace-assets-view.md">
   <img alt="Mt Workspace" src="./assets/my-workspace.jpeg" />
   </a>
   <div>
      <a href="/help/assets/my-workspace-assets-view.md">
      <strong>Min Workspace</strong>
      </a>
   </div>
   <p>
      <em>Lär dig hur du arbetar med Min Workspace för att snabbt komma åt nyckelområden i Assets användargränssnitt.</em>
   </p>
</td>
<td>
   <a href="/help/assets/content-credentials.md">
   <img alt="Content Credentials" src="./assets/content-credentials.jpeg" />
   </a>
   <div>
      <a href="/help/assets/content-credentials.md">
      <strong>Content Credentials</strong>
      </a>
   </div>
   <p>
      <em>Få insikter om historiken för en digital resurs med Content Credentials.</em>
   </p>
</td>
</table>

**Samlingar**: Med AEM Assets kan du också ordna dina resurser i samlingar. En samling är en uppsättning resurser, mappar eller andra samlingar i vyn Adobe Experience Manager Assets. Använd samlingar för att dela resurser mellan användare. Till skillnad från mappar kan en samling innehålla resurser från olika platser. Du kan dela flera samlingar med en användare. Varje samling innehåller referenser till resurser. Resursernas referensintegritet bevaras i alla samlingar.

**Meddelanden**: Med Assets-vymeddelanden kan du övervaka åtgärder som utförs för de resurser, mappar och samlingar som är tillgängliga i databasen. Du måste välja och prenumerera på det innehåll som meddelandena skickas till dig för. Du kan också konfigurera de kategorier som meddelanden skickas till dig för.

**Identifiera duplicerade resurser**: AEM Assets stöder även identifiering av dubblettresurser. Om en DAM-användare överför en eller flera resurser som redan finns i databasen, upptäcker Experience Manager dupliceringen och meddelar användaren.



<table>
<td>
   <a href="/help/assets/manage-collections-assets-view.md">
   <img alt="Hantera samlingar" src="./assets/manage-collections.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-collections-assets-view.md">
      <strong> Hantera samlingar </strong>
      </a>
   </div>
   <p>
      <em>Lär dig hur du organiserar dina resurser i samlingar för effektiv delning av resurser.</em>
   </p>
</td>


<td>
   <a href="/help/assets/manage-notifications-assets-view.md">
   <img alt="Ange meddelanden" src="./assets/manage-notifications.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-notifications-assets-view.md">
      <strong> Ange meddelanden </strong>
      </a>
   </div>
   <p>
      <em>Lär dig hur du ställer in meddelanden för att övervaka åtgärder som utförs på resurser, mappar eller samlingar.</em>
   </p>
</td>
<td>
   <a href="/help/assets/detect-duplicate-assets.md">
   <img alt="Identifiera duplicerade resurser" src="./assets/duplicate-assets.jpeg" />
   </a>
   <div>
      <a href="/help/assets/detect-duplicate-assets.md">
      <strong> Identifiera duplicerade resurser </strong>
      </a>
   </div>
   <p>
      <em>Identifiera duplicerade resurser som överförts till AEM Assets och meddela användarna.</em>
   </p>
</td>
</table>

>[!TAB Integrationer]

## Integrering med Adobe och andra program än Adobe {#integration-adobe-non-adode-apps}

AEM Assets kan integreras smidigt med olika Adobe- och andra program än Adobe. Här följer en sammanfattning av de tillgängliga integreringarna:

+++**Integrering med Adobe och andra program än Adobe**

* **Dynamiska media med OpenAPI-funktioner**: [Dynamiska media med OpenAPI-funktioner](/help/assets/dynamic-media-open-apis-overview.md) erbjuder en omfattande uppsättning API:er för [sökning](/help/assets/search-assets-api.md) och [leverans](/help/assets/deliver-assets-apis.md). Det gör att utvecklarna enkelt kan integrera leverans av resurser med sina program. Programmen innehåller både Adobe och tredjepartsprogram. Det har ett användargränssnitt för resursväljare i Micro FrontEnd som gör att du kan söka efter och välja godkända resurser. Väljaren kan enkelt integreras med alla program som är baserade på JavaScript ramverk som React JS, Angular JS och Vanilla JS.

* **Micro-Frontend Asset Selector**: Micro-Frontend Asset Selector har ett användargränssnitt som enkelt kan integreras med Experience Manager Assets-databasen så att du kan bläddra bland eller söka efter digitala resurser som är tillgängliga i databasen och använda dem i programutvecklingen.
Du kan integrera resursväljaren med ett Adobe- eller ett program som inte kommer från Adobe.

<table>
<td>
   <a href="/help/assets/dynamic-media-open-apis-overview.md">
   <img alt="Dynamic Media med OpenAPI-funktioner - översikt" src="./assets/dm-openapi-uses.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media-open-apis-overview.md">
      <strong> Dynamic Media med OpenAPI-funktioner - översikt </strong>
      </a>
   </div>
   <p>
      <em>Lär dig viktiga fördelar och hur du aktiverar det. </em>
   </p>
</td>


<td>
   <a href="/help/assets/restrict-assets-delivery.md">
   <img alt="Begränsa åtkomst till resurser i Experience Manager" src="./assets/restrict-assets.jpeg" />
   </a>
   <div>
      <a href="/help/assets/restrict-assets-delivery.md">
      <strong>Begränsa åtkomst till resurser i Experience Manager</strong>
      </a>
   </div>
   <p>
      <em> Konfigurera roller för att begränsa åtkomst till godkända resurser.</em>
   </p>
</td>
<td>
   <a href="/help/assets/overview-asset-selector.md">
   <img alt="Resursväljare" src="./assets/integration-asset-selector.jpeg" />
   </a>
   <div>
      <a href="/help/assets/overview-asset-selector.md">
      <strong> Micro-Frontend Asset Selector </strong>
      </a>
   </div>
   <p>
      <em>Lär dig hur du integrerar Micro-Front Asset Selector med ett Adobe- eller ett icke-Adobe-program.</em>
   </p>
</td>
</table>

+++

+++**Inbyggd integrering med Adobe-program**

* **Integrering med Adobe Workfront**: [!DNL Adobe Workfront] är ett arbetshanteringsprogram som hjälper dig att hantera hela arbetscykeln på ett och samma ställe. Integrationen mellan [!DNL Workfront] och [!DNL Adobe Experience Manager Assets] gör att organisationer kan förbättra innehållets hastighet och time-to-market genom att knyta samman arbete och hantering av digitala resurser. När man arbetar i Workfront får man tillgång till dokument och bilder.

  Adobe erbjuder att [integrera [!DNL Workfront] och [!DNL Adobe Experience Manager Assets] internt](https://experienceleague.adobe.com/docs/workfront/using/documents/wf-aem-integrations/wf-aem-essentials/aem-asset-integrations.html?lang=sv-SE).

* **Integrering med Figma**: AEM Assets kan integreras direkt med Figma, vilket gör att designers kan komma åt de resurser som lagras i AEM Assets direkt från Figma-användargränssnittet. Du kan placera innehåll som hanteras i AEM Assets på arbetsytan i Figma och sedan spara nytt eller redigerat innehåll i AEM Assets-databasen. Klicka [här](https://www.figma.com/community/plugin/1512561378275712210/adobe-experience-manager-aem-assets-connector) om du vill få åtkomst till AEM Assets Connector på Figma Community-sidan.

* **Inbyggd integrering med Adobe Express**: AEM Assets kan integreras med Adobe Express, vilket gör att du kan komma åt resurser som lagras i AEM Assets direkt från Adobe Express användargränssnitt. Du kan placera innehåll som hanteras i AEM Assets på arbetsytan Express och sedan spara nytt eller redigerat innehåll i en AEM Assets-databas.

* **Anslut AEM Assets till Creative Cloud**: Experience Manager Assets kan ansluta till ett Creative Cloud-berättigande som har etablerats till en annan IMS-organisation för att enkelt kunna använda de senaste Creative Cloud-integreringarna i AEM Assets, inklusive Express och Creative Cloud Libraries. Om era Creative Cloud-produkter och AEM Assets är avsedda för olika IMS-organisationer kan ni ansluta till en annan Creative Cloud-organisation för att kunna genomföra integrerade arbetsflöden mellan de två lösningarna.

<table>
<td>
   <a href="/help/assets/workfront-integrations.md">
   <img alt="Integrering med Adobe Workfront" src="./assets/integration-adobe-workfront.jpeg" />
   </a>
   <div>
      <a href="/help/assets/workfront-integrations.md">
      <strong>Integrering med Adobe Workfront</strong>
      </a>
   </div>
   <p>
      <em>Integrera med Adobe Workfront för att hantera hela arbetscykeln på ett och samma ställe.</em>
   </p>
</td>
<td>
   <a href="/help/assets/manage-collections-assets-view.md">
   <img alt="Integrering med Figma" src="./assets/integration-commerce.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-collections-assets-view.md">
      <strong> Integrering med Figma </strong>
      </a>
   </div>
   <p>
      <em>Få åtkomst till resurser som lagras i AEM Assets inifrån Figma-användargränssnittet</em>
   </p>
</td>
<td>
   <a href="/help/assets/native-integration-adobe-express.md">
   <img alt="Inbyggd integrering med Adobe Express" src="./assets/integration-adobe-express.jpeg" />
   </a>
   <div>
      <a href="/help/assets/native-integration-adobe-express.md">
      <strong> Inbyggd integrering med Adobe Express </strong>
      </a>
   </div>
   <p>
      <em>Placera resurser som är tillgängliga i AEM Assets på Express-arbetsytan och spara uppdaterade resurser i AEM. </em>
   </p>
</td>


</table>


* **Integrering med Adobe Journey Optimizer**: Sammanför arbetsflöden för marknadsföring och kreativitet med Adobe Experience Manager Assets. Inbyggt i Adobe Journey Optimizer ger du tillgång till Assets as a Cloud Service där du kan lagra, hantera, upptäcka och distribuera digitalt material. Det utgör en central databas med resurser som du kan använda för att fylla i dina meddelanden.

* **Integrering med Commerce**: Adobe Experience Manager (AEM) Assets Integration för Commerce kombinerar de robusta funktionerna i AEM som ett DAM-system (Digital Asset Management) med Adobe Commerce för att förbättra e-handelsupplevelsen. Dessa funktioner levereras genom att man kopplar ihop Commerce-projekt med AEM kraftfulla resurshanteringsmiljö för att erbjuda ett smidigt, skalbart och effektivt sätt att hantera och leverera material i butiker.
* **Integrera AEM Assets med dokumentbaserade redigeringsflöden för Edge Delivery Services**: När [!DNL AEM Assets] integreras med dokumentbaserade redigeringsverktyg som [!DNL Microsoft Word] eller [!DNL Google Docs] innehåller det en resursväljare i utvecklingsverktyget. Använd den här resursväljaren för att komma åt [!DNL AEM Assets] och infoga godkända resurser i ditt innehåll.
Om du redan har en [!DNL Edge Delivery Services]-webbplats kan du läsa [[!DNL AEM Assets] plugin](https://github.com/adobe-rnd/aem-assets-plugin/blob/main/README.md)-dokumentationen och lära dig hur du integrerar [!DNL AEM Assets] med ditt befintliga [!DNL AEM]-projekt.

* **Integrerar [!DNL AEM Assets] med [!DNL Universal Editor]-baserade redigeringsflöden för[!DNL Edge Delivery Services]**: Konfigurera [!DNL Universal Editor] för integrering med [!DNL AEM Assets]. Med den här integreringen kan du använda [!DNL Dynamic Media with OpenAPI capabilities] för att leverera resurser.

   * Mer information om hur du lägger till en anpassad resursväljarfunktion i [ finns i  [!DNL Edge Delivery] Konfiguration i](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#configuration-in-edge-delivery-site)Plats[!DNL Universal Editor]. Med den anpassade resursväljaren kan du infoga resurser direkt i ditt [!DNL Universal Editor]-innehåll.
   * Se [Tilläggsöversikt](https://developer.adobe.com/uix/docs/extension-manager/extension-developed-by-adobe/configurable-asset-picker/#extension-overview) om du vill veta hur du får åtkomst till [!DNL AEM Assets] och infogar resurserna när du redigerar i [!DNL Universal Editor].

<table>
<td>
   <a href="https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/content-management/combine/assets">
   <img alt="Integrering med Adobe Journey Optimizer" src="./assets/integration-figma.jpeg" />
   </a>
   <div>
      <a href="https://experienceleague.adobe.com/sv/docs/journey-optimizer/using/content-management/combine/assets">
      <strong>Integrering med Adobe Journey Optimizer</strong>
      </a>
   </div>
   <p>
      <em>Sammanför arbetsflöden för marknadsföring och kreativitet med hjälp av integrering med AJO</em>
   </p>
</td>
<td>
   <a href="https://experienceleague.adobe.com/sv/docs/commerce-admin/content-design/aem-asset-management/aem-assets-integration">
   <img alt="Integrering med Commerce" src="./assets/integration-ajo.jpeg" />
   </a>
   <div>
      <a href="https://experienceleague.adobe.com/sv/docs/commerce-admin/content-design/aem-asset-management/aem-assets-integration">
      <strong>Integrering med Commerce</strong>
      </a>
   </div>
   <p>
      <em>Integrera AEM Assets med Commerce för att förbättra e-handelsupplevelserna.</em>
   </p>
</td>
<td>
   <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md">
   <img alt="Integrera AEM Assets med EDS" src="./assets/integrate-ue-assets.jpeg" />
   </a>
   <div>
      <a href="/help/assets/integrate-aem-assets-edge-delivery-services.md">
      <strong> Integrera AEM Assets med EDS </strong>
      </a>
   </div>
   <p>
      <em>Integrera AEM Assets med dokumentbaserade och universella redigeringsbaserade redigeringsflöden.</em>
   </p>
</td>
</table>

+++

>[!TAB Resursaktivering]

## Aktivering av tillgångar {#asset-activation}

Utnyttja era digitala resurser fullt ut med AEM Assets, som använder Content Hub till Dynamic Media - inklusive kraftfulla OpenAPI-funktioner. AEM Assets erbjuder en omfattande uppsättning lösningar som utformats för att effektivisera omvandling av resurser och optimera leveransen över olika kanaler.

+++**Content Hub**

Content Hub ingår i Experience Manager Assets as a Cloud Service för att demokratisera tillgången till varumärkesinnehåll för organisationer och deras affärspartners. Fokus ligger på att distribuera resurser för aktivering i stor skala och att skapa innehållsvarianter för varumärke, vilket ger förbättrad marknadsföringsflexibilitet.

Content Hub har följande fördelar:

* **Hitta och dela alla varumärkesgodkända resurser som finns i en intuitiv portal**: AEM Assets fungerar som en enda källa till sanning och alla godkända resurser är automatiskt tillgängliga på Content Hub i en plan hierarki för att förbättra sökupplevelsen.

* **Konfigurerbart användargränssnitt**: De vanligaste egenskaperna i Content Hub, till exempel sökfilter, fält som är tillgängliga när du lägger till eller importerar resurser, resursegenskaper och banderollinnehåll för profilering, kan konfigureras av en administratör och kan enkelt konfigurera Content Hub-användargränssnittet utifrån deras behov.

* **Ge icke-kreatörer möjlighet att redigera och mixa om innehåll samtidigt som de behåller sitt varumärke**: Med Content Hub kan du skapa nytt innehåll med Adobe Express (om du har Adobe Express-rättigheter). Du kan redigera befintligt innehåll med lättanvända verktyg, producera varumärkesanpassade varianter med mallar och märkeselement och skapa nytt innehåll med de senaste GenAI-funktionerna från Adobe Firefly.

* **Få insikter om hur innehåll används i olika team**: [!DNL Content Hub] ger värdefulla insikter om resurser, vilket löser en vanlig utmaning som marknadsföringsintressenter ofta stöter på - statistik om resursanvändning som används i marknadsföringskampanjer, kanaler och olika regioner. Genom att få en tydlig förståelse för resursernas prestanda och popularitet kan ni få användbara insikter som är viktiga för att förbättra användarupplevelsen.

<table>
<td>
   <a href="/help/assets/product-overview.md">
   <img alt="Content Hub - översikt" src="./assets/content-hub-overview.jpeg" />
   </a>
   <div>
      <a href="/help/assets/product-overview.md">
      <strong> Content Hub - översikt </strong>
      </a>
   </div>
   <p>
      <em>Läs mer om Content Hub, dess viktigaste fördelar och hur du får tillgång till det. </em>
   </p>
</td>


<td>
   <a href="/help/assets/configure-content-hub-ui-options.md">
   <img alt="Konfigurera Content Hub användargränssnitt" src="./assets/content-hub-configuration.jpeg" />
   </a>
   <div>
      <a href="/help/assets/configure-content-hub-ui-options.md">
      <strong> Konfigurera Content Hub-användargränssnitt </strong>
      </a>
   </div>
   <p>
      <em>Lär dig hur du konfigurerar alternativ som är tillgängliga i Content Hub användargränssnitt.</em>
   </p>
</td>
<td>
   <a href="/help/assets/edit-images-content-hub.md">
   <img alt="Redigera med Adobe Express" src="./assets/content-hub-express.jpeg" />
   </a>
   <div>
      <a href="/help/assets/edit-images-content-hub.md">
      <strong>Redigera med Adobe Express</strong>
      </a>
   </div>
   <p>
      <em>Lär dig hur du redigerar bilder i Content Hub med Adobe Express.</em>
   </p>
</td>
</table>

+++

+++**Dynamiska media**

Med Dynamic Media kan ni leverera visuella marknadsförings- och marknadsföringsresurser on demand. Det hjälper dig också att skapa och leverera interaktiva visningsupplevelser som zoomning, 360-graders rotation och video. Dina resurser skalas dynamiskt för konsumtion på webben, mobiler och sociala webbplatser. Med hjälp av en uppsättning primära källresurser - som bilder, video och 3D - genererar och levererar Dynamic Media flera varianter av detta multimediematerial i realtid via en global, skalbar, prestandaoptimerad CDN (Content Delivery Network).

Dynamic Media har följande viktiga funktioner:

* **Smart Imaging**: Smart Imaging ger ännu bättre prestanda för leverans av bildresurser genom att automatiskt optimera en bilds format och filstorlek baserat på en kunds webbläsarkapacitet. Det fungerar med befintliga bildförinställningar och använder intelligens vid leverans. Den här intelligensen minskar bildfilens storlek ytterligare baserat på webbläsarens och nätverkets anslutningshastighet.

* **Adaptiva videouppsättningar**: En adaptiv videouppsättning grupperar versioner av samma video som är kodade med olika bithastigheter och format. Du börjar med den ursprungliga primära videon som du överför till systemet. Dynamic Media ändrar automatiskt storlek på videon, eller omkodar den till flera videor. När filmen levereras avgör den sedan på ett smart sätt vilken videoskärm, vilken kvalitet och vilket format som ska användas och skickar den till telefonen, surfplattan eller datorn.

* **Smart beskärning**: En Adobe Sensei AI-funktion som automatiskt identifierar fokalpunkten i en bild eller video och beskär för att behålla den. Den fångar upp den avsedda intressepunkten oavsett skärmstorlek och eliminerar därmed långtråkiga manuella moment och levererar högkvalitativa, snabba bilder och video som ser bra ut på alla enheter och skärmar.

* **Dynamiska mediamallar**: Skapa anpassningsbara mallar i realtid för banners och flygblad med Dynamic Media-mallar, en WYSIWYG-mallredigerare. Publicera mallen för dynamiska media och använd den i program längre fram i kedjan. En mall för dynamiska media innehåller bild- och textlager. Lägg till parametrar i bild- och textlagren i mallen och använd dynamiska medie-URL:er för att flytta och ändra storlek på lagret och uppdatera innehållet i realtid.

* **Flerljud och bildtext**: Lägg till flera bildtexter och flera ljudspår i en primär video. Detta innebär att videoklippen är tillgängliga för en global publik. Du kan anpassa en enda publicerad primär video till en global publik på flera språk och följa riktlinjer för tillgänglighet för olika geografiska regioner. Författare kan också hantera beskrivningar och ljudspår från en enda flik i användargränssnittet.

* **Stöd för dynamisk adaptiv strömning via HTTP (DASH)**: Dynamic Media har stöd för adaptiv strömning i Dynamic Media-leverans (med CMAF aktiverat), vilket ger en bättre användarupplevelse för videor. DASH är det internationella standardprotokollet för strömning av adaptiv video och är en vida spridd bransch.

* **AI-genererade videobeskrivningar**: AI-genererade videobeskrivningar i Adobe Dynamic Media använder artificiell intelligens för att generera bildtexter automatiskt för videoinnehåll. Med stöd för över 60 språk kan bildtexter granskas och förhandsgranskas innan videon publiceras.

Information om tillgängliga Dynamic Media-erbjudanden finns i [Dynamic Media Prime och Ultimate](/help/assets/dynamic-media/dm-prime-ultimate.md).



<table>
<td>
   <a href="/help/assets/dynamic-media/dynamic-media.md">
   <img alt="Arbeta med Dynamic Media" src="./assets/work-with-dynamic-media.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media/dynamic-media.md">
      <strong> Arbeta med dynamiska media </strong>
      </a>
   </div>
   <p>
      <em>Lär dig hur du levererar resurser för konsumtion på webbplatser, mobilsajter och sociala medier. </em>
   </p>
</td>


<td>
   <a href="/help/assets/dynamic-media/dm-journey-part1.md">
   <img alt="Dynamic Media Journey" src="./assets/dm-journey.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media/dm-journey-part1.md">
      <strong> Dynamic Media Journey </strong>
      </a>
   </div>
   <p>
      <em>Lär dig hur Dynamic Media ger ditt arbete värde.</em>
   </p>
</td>
<td>
   <a href="/help/assets/dynamic-media/dm-best-practices.md">
   <img alt="Anslut AEM Assets till Creative Cloud" src="./assets/dm-best-practices.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media/dm-best-practices.md">
      <strong>Bästa praxis för dynamiska media</strong>
      </a>
   </div>
   <p>
      <em>Bästa tillvägagångssätt när du arbetar med bilder, videoklipp och visningsprogram.</em>
   </p>
</td>
</table>

+++

+++**Dynamiska media med OpenAPI-funktioner**

I dagens snabba digitala värld är det avgörande att frigöra potentialen i ert varumärkes digitala resurser för att ligga steget före konkurrenterna. En helhetsbaserad lösning för digital Assets Management (DAM) underlättar materialstyrning, främjar varumärkets enhetlighet och snabbar upp innehållsleveransen samtidigt som man säkerställer varumärkets integritet och exceptionella kundupplevelser.

Dynamic Media med OpenAPI-funktioner sätter DAM i centrum för ett flexibelt och effektivt ekosystem i innehållsförsörjningskedjan för att säkerställa materialstyrning och leverans.

Dynamic Media med OpenAPI-funktioner ger följande viktiga fördelar:

* **Smidiga integreringar**: Dynamiska medier med OpenAPI-funktioner erbjuder en omfattande uppsättning API:er för sökning och leverans. Det gör att utvecklarna enkelt kan [integrera leverans av resurser med sina program](/help/assets/integrate-dynamic-media-open-apis.md). Programmen innehåller både Adobe och tredjepartsprogram. Det har ett [användargränssnitt för resursväljare i Microsoft FrontEnd](/help/assets/overview-asset-selector.md) för att söka efter och välja godkända resurser. Väljaren kan enkelt integreras med alla program som är baserade på JavaScript ramverk som React JS, Angular JS och Vanilla JS.

* **Centraliserad hantering av digitala resurser**: DAM är den enda källan till sanning för alla digitala resurser. Dina digitala resurser hanteras centralt i AEM Assets och levereras till de förbrukande programmen via referens via leverans-URL:er, utan att du behöver kopiera resurbinärfiler.

* **Realtidsuppdateringar**: Alla ändringar som görs i godkända resurser i DAM, inklusive versionsuppdateringar och metadataändringar, återspeglas automatiskt i leverans-URL:erna. Med ett kort TTL-värde (Time-to-Live) på 10 minuter konfigurerat för Dynamic Media med OpenAPI-funktioner via CDN blir uppdateringarna synliga i alla redigerings- och publiceringsgränssnitt på mindre än 10 minuter.

* **Varumärkeskonsekvens**: Endast [varumärkesgodkända resurser](/help/assets/approve-assets.md) exponeras för program längre fram i kedjan. [Varumärkesansvariga och marknadsförare har strikt kontroll över varumärkesresurser](/help/assets/restrict-assets-delivery.md). Det är bara en godkänd och den senaste versionen av resursen som är tillgänglig för användning, vilket garanterar ett enhetligt varumärke i alla kanaler och tillämpningar.

* **Webboptimerad leverans**: Digitala resurser levereras i webboptimerade format för att förbättra de digitala upplevelsernas Core Web Vitals. Detta inkluderar stöd för WebP-återgivningar för bilder, adaptiv direktuppspelning via HLS- eller DASH-protokoll för videor samt ursprungliga återgivningar för dokument.

* **Dynamisk resursomformning**: I vårt system går det att göra bildomformningar direkt med URL-parametrar som kallas bildmodifierare. [Till exempel bredd, höjd, rotering, vänd, kvalitet, beskärning, format och smart beskärning](/help/assets/deliver-assets-apis.md). Omformade renderingar genereras dynamiskt och levereras smidigt via CDN.

* **Säker leverans av resurser**: Dynamiska media med OpenAPI-funktioner ger en mekanism för kontroll över åtkomsten till dina digitala resurser. Du kan ange användarroller eller användargrupper som metadata för att skydda resurser och ange en fördefinierad tidsram under vilken [endast behöriga användare kan komma åt dessa resurser](/help/assets/restrict-assets-delivery.md). Leverans-URL:erna för skyddade tillgångar kan inte matchas för obehöriga användare under den begränsade perioden.

Information om tillgängliga Dynamic Media-erbjudanden finns i [Dynamic Media Prime och Ultimate](/help/assets/dynamic-media/dm-prime-ultimate.md).

<table>
<td>
   <a href="/help/assets/dynamic-media-open-apis-overview.md">
   <img alt="Dynamic Media med OpenAPI-funktioner - översikt" src="./assets/dm-openapi-uses.jpeg" />
   </a>
   <div>
      <a href="/help/assets/dynamic-media-open-apis-overview.md">
      <strong> Dynamic Media med OpenAPI-funktioner - översikt </strong>
      </a>
   </div>
   <p>
      <em>Lär dig viktiga fördelar och hur du aktiverar det. </em>
   </p>
</td>


<td>
   <a href="/help/assets/restrict-assets-delivery.md">
   <img alt="Begränsa åtkomst till resurser i Experience Manager" src="./assets/restrict-assets.jpeg" />
   </a>
   <div>
      <a href="/help/assets/restrict-assets-delivery.md">
      <strong>Begränsa åtkomst till resurser i Experience Manager</strong>
      </a>
   </div>
   <p>
      <em> Konfigurera roller för att begränsa åtkomst till godkända resurser.</em>
   </p>
</td>
<td>
   <a href="/help/assets/integrate-remote-approved-assets-with-sites.md">
   <img alt="Integrera fjärr-AEM Assets med AEM Sites" src="./assets/integration-aem-sites.jpeg" />
   </a>
   <div>
      <a href="/help/assets/integrate-remote-approved-assets-with-sites.md">
      <strong> Integrera AEM Assets på fjärrbasis med AEM Sites </strong>
      </a>
   </div>
   <p>
      <em>Integrera fjärr-AEM Assets med AEM Sites. </em>
   </p>
</td>
</table>

+++

>[!TAB Insikter]

## Resursinsikter {#asset-insights}

Med tillgångsrapportering kan administratörer se vilka aktiviteter Adobe Experience Manager Assets View-miljön har. Dessa data ger användbar information om hur användarna interagerar med innehållet och produkten. Alla användare har tillgång till Insikter-kontrollpanelen och de som har tilldelats administratörens produktprofil kan skapa användardefinierade rapporter.

Du kan generera olika typer av rapporter, som Överför, Hämta och Dynamic Media-leverans.

* **Insikter i Assets-vyn**: I Assets-vyn kan du visa realtidsdata för din visningsmiljö i Assets med Insikter-instrumentpanelen. Du kan visa händelsemått i realtid under de senaste 30 dagarna eller under de senaste 12 månaderna. Händelserna omfattar hämtningar, överföringar, lagringsanvändning, Vanliga sökningar, Antal tillgångar efter storlek och Antal tillgångar efter tillgångstyp.

* **Adobe Analytics-integrering i administrationsvyn**: Med funktionen Assets Insights kan du spåra användarklassificeringar och användningsstatistik för bilder som används på tredjepartswebbplatser, marknadsföringskampanjer och Adobe kreativa lösningar. Det ger insikter om bildens prestanda och popularitet. Assets Insights fångar upp användaraktivitetsinformation, t.ex. hur många gånger en bild klassificeras, klickas och hur många gånger bilden läses in på webbplatsen. Det tilldelar poäng till bilder baserat på denna statistik. Du kan använda resultat och prestandastatistik för att välja populära bilder som ska ingå i kataloger, marknadsföringskampanjer och så vidare. Man kan till och med utforma arkiverings- och licensförnyelseregler baserat på denna statistik. Om du vill att Assets Insights ska visa användningsstatistik för mediefiler måste du först konfigurera funktionen för att hämta rapportdata från Adobe Analytics.

* **Content Hub Insights**: Content Hub ger värdefull information om resurser och åtgärdar en vanlig utmaning som marknadsföringsintressenter ofta stöter på - statistik om resursanvändning som används i marknadsföringskampanjer, kanaler och olika regioner. Genom att få en tydlig förståelse för resursernas prestanda och popularitet kan ni få användbara insikter som är viktiga för att förbättra användarupplevelsen.

<table>
<td>
   <a href="/help/assets/manage-reports-assets-view.md">
   <img alt="Hantera rapporter i Assets-vyn" src="./assets/assets-insights-assets-view.jpeg" />
   </a>
   <div>
      <a href="/help/assets/manage-reports-assets-view.md">
      <strong>Hantera rapporter i Assets-vyn </strong>
      </a>
   </div>
   <p>
      <em>Ta fram insikter om viktiga framgångsmått i Assets-vyn. </em>
   </p>
</td>


<td>
   <a href="/help/assets/asset-reports.md">
   <img alt="Hantera rapporter i administratörsvyn" src="./assets/assets-insights-admin-view.jpeg" />
   </a>
   <div>
      <a href="/help/assets/asset-reports.md">
      <strong>Hantera rapporter i administratörsvyn </strong>
      </a>
   </div>
   <p>
      <em>Lär dig hur du hanterar Adobe Analytics integrerade rapporter i administratörsvyn.</em>
   </p>
</td>
<td>
   <a href="/help/assets/insights-content-hub.md">
   <img alt="Assets insikter i Content Hub" src="./assets/asset-insights-content-hub.jpeg" />
   </a>
   <div>
      <a href="/help/assets/insights-content-hub.md">
      <strong> Assets insights in Content Hub </strong>
      </a>
   </div>
   <p>
      <em>Lär dig hur du visar resursinsikter i Content Hub.</em>
   </p>
</td>
</table>

>[!ENDTABS]

## Tillgängliga personbaserade upplevelser för hantering av digitala resurser {#persona-based-experiences}

Adobe erbjuder robusta DAM-lösningar (Digital Asset Management) så att ni får ut mesta möjliga av era digitala resurser. Adobe Experience Manager Assets har två separata upplevelser som använder samma molntjänstdatabas:

* **Administratörsvy**: Det befintliga användargränssnittet i Assets as a Cloud Service. Använd administrationsvyn för alla avancerade funktioner för hantering av digitala resurser, inklusive integreringar, arbetsflöden, innehållsautomatisering, publicering med mera.

* **Assets View**: Adobe lättviktiga resurshantering för att lagra, hantera, identifiera och använda digitala resurser. Effektivt användargränssnitt med viktiga funktioner för hantering av digitala resurser. Utformad för enklare DAM-användare med fokus på överföring, metadatahantering, sökning, hämtning och delning.

![add-tags](assets/newui-overview.svg)

Användare som har åtkomst till administrationsvyn har även åtkomst till vyn Assets. Assets View har ett förenklat användargränssnitt som gör det enkelt att hantera, upptäcka och distribuera digitala resurser. Ett stort antal användare från olika funktioner, inklusive kreatörer, marknadsförare och branschgrupper, kan samarbeta om resurser och få tillgång till rätt, godkänt material när och var de behöver det. Många tillfälliga DAM-användare föredrar Assets-vyn eftersom den bara innehåller en delmängd av funktioner. Upplevelsen riktar sig till kreatörer, skrivskyddade mediekonsumenter och användare med mindre vikt-DAM.

DAM-bibliotek, utvecklare och superanvändare kan fortsätta att använda administrationsvyn eller växla mellan användargränssnitten efter behov. Du kan välja den upplevelse som fungerar bäst för din roll.

Mer information om hur du kommer åt vyn Assets och vissa av de förenklingar som den erbjuder via administratörsvyn finns i [Introduktion till vyn Assets](/help/assets/assets-view-introduction.md).
