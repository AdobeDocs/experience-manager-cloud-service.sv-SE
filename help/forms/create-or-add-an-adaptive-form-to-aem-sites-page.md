---
title: Hur lägger man till ett adaptivt formulär på en AEM Sites-sida?
description: Upptäck hur du skapar eller lägger till ett anpassat formulär på din AEM Sites-sida. Lär dig även fördelarna och olika sätt att integrera formulär på din webbplats.
feature: Adaptive Forms, Foundation Components, Page Editor, Authoring
Keywords: AF in Sites editor, af in aem sites, aem sites af, add af to a sites page, af aem sites, af sites, create af in a sites page, adaptive form in aem sites, forms aem sites, add form to a sites page, adaptive forms aem sites, add adaptive forms to aem page, create forms in an aem sites page
exl-id: a1846c5d-7b0f-4f48-9d15-96b2a8836a9d
source-git-commit: eaab351460363b83c7d3667e048235506cc71c41
workflow-type: tm+mt
source-wordcount: '3088'
ht-degree: 0%

---

# Lägga till ett anpassat formulär på en AEM Sites-sida eller ett Experience Fragment {#create-or-add-an-adaptive-form-to-aem-sites-page}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/create-or-add-an-adaptive-form-to-aem-sites-page.html) |
| AEM as a Cloud Service | Den här artikeln |

## Ökning {#overview}

Med AEM Forms kan du enkelt lägga till ett formulär på din AEM Sites-sida. På så sätt kan besökarna enkelt fylla i och skicka in formulär utan att lämna den sida de är på. På så sätt kan de enkelt hålla kontakten med andra element på webbplatsen samtidigt som de interagerar aktivt med formuläret.

Du kan använda AEM Page Editor för att snabbt skapa och lägga till flera formulär på dina AEM Sites-sidor. Med AEM Page Editor kan skribenter skapa smidiga datainhämtningsupplevelser på en webbplatssida med hjälp av adaptiva formulärkomponenter som dynamiskt beteende, validering, dataintegrering, generering av registerdokument och automatisering av affärsprocesser. Du kan även använda olika funktioner på AEM Sites-sidor, som versionshantering, målgruppsanpassning, översättning och hantering av flera webbplatser.

AEM Forms Cloud Service har adaptiv formulärbehållare och adaptiv Forms - inbäddningskomponenter. Du kan använda adaptiv formulärbehållare för att skapa ett formulär på en AEM Sites-sida eller i ett Experience Fragment, medan adaptiv Forms - Embed-komponent gör att du kan lägga till ett befintligt adaptivt formulär eller skapa ett formulär med Adaptiv Forms Editor.

![Ett exempel på ett adaptivt formulär på en AEM Sites-sida](/help/forms/assets/adaptive-form-in-sites-page.png)

## Varför använda adaptiva Forms Core-komponenter för att skapa ett adaptivt formulär på AEM Sites-sidor eller i Experience Fragment?

Om du tidigare har skapat adaptiva Forms Foundation-komponenter eller enkla HTML-baserade formulär för dina webbplatser rekommenderar Adobe att du använder adaptiva Forms Core-komponenter för att skapa ett adaptivt formulär på AEM Sites-sidor eller i Experience Fragment. Här kan ni använda olika funktioner på AEM Sites-sidor, som versionshantering, målgruppsanpassning, översättning och hantering av flera webbplatser, vilket förbättrar den övergripande upplevelsen av att skapa och hantera formulär för Adaptiv Forms. Låt oss utforska några av dessa funktioner:

* **Versionshantering:** Erbjudande om AEM Sites-sidor [robust versionshantering](/help/sites-cloud/authoring/features/page-versions.md), så att du kan spåra och hantera olika versioner av formulären. På så sätt kan du göra ändringar och förbättringar i formulär samtidigt som du behåller möjligheten att vid behov gå tillbaka till tidigare versioner. Versionshantering säkerställer ett kontrollerat och organiserat tillvägagångssätt för blankettutveckling och -utveckling.
* **Målinriktning (integrering med Adobe Target):** Med målgruppsfunktionerna i AEM Sites kan man också [personalisera formulärupplevelsen för olika målgrupper](/help/sites-cloud/integrating/integration-adobe-target-ims.md). Genom att använda användarsegment och kriterier för målinriktning kan du anpassa formulärets innehåll, design eller beteende till specifika användargrupper. På så sätt kan ni leverera en personaliserad och relevant formulärupplevelse, vilket ökar engagemanget och konverteringsgraden.
* **Översättning:** AEM Sites [smidig integrering med översättningstjänster](/help/sites-cloud/administering/translation/overview.md)så att du enkelt kan översätta formulär till flera språk. Den här funktionen förenklar lokaliseringsprocessen och säkerställer att formulären är tillgängliga för en global publik. Ni kan hantera översättningar effektivt i AEM översättningsprojekt, vilket minskar den tid och det arbete som krävs för stöd av flerspråkiga formulär. Mer information om översättning finns i avsnittet med överväganden.
* **Hantering av flera webbplatser och Live Copy:** AEM Sites ger robusta [Funktioner för hantering av flera webbplatser och Live Copy](/help/sites-cloud/administering/msm/overview.md), vilket gör att du kan skapa och hantera flera webbplatser i en och samma miljö. Med den här funktionen kan du nu återanvända formulär på olika webbplatser, vilket ger enhetlighet och minskar dubbelarbetet. Med centraliserad kontroll och hantering kan ni effektivt hantera och uppdatera formulär på flera webbplatser.
* **Teman:** På AEM Sites-sidor finns ett ramverk för att utforma och underhålla enhetliga visuella format för flera webbsidor. Dessa definierar färger, teckensnitt, formatmallar och andra visuella element som bidrar till webbplatsens allmänna utseende och känsla. [Du kan använda teman som är utformade för en AEM Sites-sida för ett adaptivt formulär, vilket sparar både tid och arbete](/help/sites-cloud/administering/site-creation/site-themes.md#using-site-themes-using-themes).
* **Taggning:** På AEM Sites sidor kan du [tilldela taggar eller etiketter till en sida, en resurs eller annat innehåll](/help/implementing/developing/introduction/tagging-framework.md). Taggar är nyckelord eller metadataetiketter som gör det möjligt att kategorisera och ordna innehåll baserat på specifika kriterier. Du kan tilldela en eller flera taggar till sidor, resurser eller andra innehållsobjekt i AEM för att förbättra sökningen och kategorisera resurserna.
* **Låsa och låsa upp innehåll:** AEM Sites tillåter användare att [styra åtkomst till och ändringar av sidor](/help/sites-cloud/authoring/fundamentals/editing-content.md) i AEM Sites. När en sida är låst innebär det att den skyddas från obehöriga ändringar och redigeringar av andra användare. Endast den användare som har låst innehållet eller en utsedd administratör kan låsa upp det för att tillåta ändringar.

Dessutom används AEM adaptiva Forms i sidredigeraren [Adaptiva Forms Core-komponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html#features). Dessa kärnkomponenter har en standard och enklare metoder för att formatera och anpassa komponenterna, som är identiska med [AEM Sites WCM-komponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html).


## Hur skapar eller lägger man till ett anpassat formulär på AEM Sites-sidan eller AEM Experience Fragment? {#various-options-to-creat-or-add-an-adaptive-form-in-aem-sites-page-or-aem-experience-fragment}

Du kan utnyttja den här funktionen till fullo genom att använda följande alternativ:

* **[Skapa och lägga till ett anpassat anpassat formulär på en AEM Sites-sida](#create-an-adaptive-form-in-sites-editor-or-experience-fragment):** Du kan använda komponenten Adaptiv formulärbehållare för att skapa ett helt nytt formulär från grunden och anpassa det specifikt efter dina behov och designönskemål.

* **[Skapa och lägga till ett anpassat anpassat formulär i ett Experience Fragments](#create-an-adaptive-form-in-sites-editor):** Ni kan utöka räckvidden för era formulär genom att lägga till dem i AEM Experience Fragments, vilket möjliggör smidig återanvändning på flera sidor eller webbplatser.

* **[Konvertera ett anpassat formulär till Experience Fragment](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment):** Konvertera ett anpassat formulär som lagts till på en AEM Sites-sida till ett Experience Fragment för återanvändning av formuläret på flera AEM Sites-sidor.

* **[Skapa och lägg till formulär baserade på godkända mallar på en AEM Sites-sida:](/help/forms/embed-adaptive-form-aem-sites.md#embed-form-using-adaptive-form-wizzard-aem-sites)** Du kan använda redan godkända mallar för att snabbt skapa adaptiva Forms som är anpassade efter organisationens riktlinjer och designstandarder. Alternativet är bara tillgängligt för Adaptiv Forms som har skapats med Adaptiv Forms Editor eller Adaptiv Forms - Bädda in komponent.

* **[Lägga till befintliga formulär på en AEM Sites-sida:](/help/forms/embed-adaptive-form-aem-sites.md#embed-an-adaptive-form-in-sites-editor)** Ni kan enkelt integrera formulär som ni redan har skapat på era webbplatser, så att besökarna kan interagera direkt med dem. Alternativet är bara tillgängligt för Adaptiv Forms som har skapats med Adaptiv Forms Editor eller Adaptiv Forms - Bädda in komponent.


* **Lägga till flera formulär på en AEM Sites-sida eller Experience Fragment:**  Du kan skapa eller lägga till flera adaptiva Forms-filer på en AEM Sites-sida för att ge flera alternativ beroende på användarens önskemål och önskemål. Dessa kan vara en kombination av helt nya formulär från grunden och befintliga formulär. Du kan använda **[!UICONTROL Adaptive Form Container]** flera gånger för att lägga till Adaptiv Forms på en AEM Sites-sida. Du kan använda **[!UICONTROL Adaptive Forms - Embed]** flera gånger på en AEM Sites-sida, endast om **[!UICONTROL Form covers entire width of the frame]** är markerat. Om **[!UICONTROL Form covers entire width of the frame]** om alternativet inte är markerat stöder AEM Sites-sidan endast ett adaptivt formulär som ska finnas utan iframe. Lägga till mer adaptiv Forms med **[!UICONTROL Adaptive Forms - Embed]** komponent, markera **[!UICONTROL Form covers entire width of the frame]** alternativ.

## Att tänka på när du skapar ett adaptivt formulär på en AEM Sites-sida eller AEM Experience Fragment {#consideration}

* När du använder den adaptiva formulärbehållaren för att skapa eller lägga till ett formulär, översätts och lokaliseras formulären via AEM Sites översättningsflöde. För varje språk genereras en separat kopia (språkkopia) av webbplatssidan och motsvarande formulär. När en innehållsförfattare ändrar en regel i ett formulär på den överordnade sidan måste samma ändringar göras i alla språkkopior av formuläret. Med adaptiv formulärbehållare kan du även använda olika funktioner på AEM Sites-sidor, som versionshantering, målgruppsanpassning, översättning och hantering av flera webbplatser.

* När du skapar eller lägger till ett formulär med komponenten Adaptiv formulärinbäddning översätts och lokaliseras formulären med hjälp av AEM Forms översättningsflöde. I det här fallet finns det ett enda formulär som du kan referera till på alla språkkopior av webbplatssidorna. Adaptiv Form-embed-komponent ger inte åtkomst till olika funktioner på AEM Sites-sidor som versionshantering, målgruppsanpassning, översättning och hantering av flera webbplatser.


## Krav för att skapa eller lägga till ett adaptivt formulär på AEM Sites-sidan eller AEM Experience Fragment {#before-you-start-creating-an-adaptive-form}

Innan du börjar skapa eller skapa ett adaptivt formulär ska du aktivera adaptiva Forms Core-komponenter och lägga till adaptiva Forms Client Libraries på din AEM Sites-sida:

+++  Aktivera adaptiva Forms Core-komponenter för din AEM Cloud Service-miljö

Se till att [Adaptiva Forms Core-komponenter är aktiverade för din as a Cloud Service AEM Forms-miljö](enable-adaptive-forms-core-components.md).

+++

+++  Lägg till adaptiva Forms-klientbibliotek på din AEM Sites-sida eller Experience Fragment

Om du vill aktivera alla funktioner för den adaptiva Forms-behållarkomponenten lägger du till klientbiblioteken CustomHeaderlibs och CustomFoterlibs på din AEM Sites-sida via distributionsflödet. Så här lägger du till biblioteken:

1. Få åtkomst till och klona dina [AEM Cloud Service Git-databas](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/repositories.html).
1. Öppna AEM Cloud Service Git-databasmappen i en textredigerare för en plan. Exempel: Microsoft Visual Code.
1. Öppna `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\page\customheaderlibs.html` och lägg till följande kod i filen:

   ```
       //Customheaderlibs.html
   
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
       </sly> 
   ```

1. Öppna `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\page\customfooterlibs.html` och lägg till följande kod i filen:

   ```
       //customfooterlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
       </sly> 
   ```

1. Öppna `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\xfpage\customheaderlibs.html` och lägg till följande kod i filen:

   ```
       //Customheaderlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
       </sly> 
   ```

1. Öppna `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\xfpage\customfooterlibs.html` och lägg till följande kod i filen:

   ```
       //customfooterlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
       </sly> 
   ```

1. [Kör distributionsflödet](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) för att distribuera klientbiblioteken till din AEM as a Cloud Service miljö.

+++

+++ Aktivera anpassad Forms-behållare för din AEM Sites-sida eller Experience Fragment

Aktivera [!UICONTROL Adaptive Forms Container] utför följande steg i mallens policy:

1. Öppna AEM Sites eller Experience Fragment för redigering. Om du vill öppna sidan för redigering markerar du sidan och klickar på Redigera.
1. Öppna mallen för webbplatserna eller sidan för Experience Fragment. Öppna mallen genom att gå till [!UICONTROL Page Information] ![Sidinformation](/help/forms/assets/Smock_Properties_18_N.svg) > [!UICONTROL Edit Template]. Motsvarande mall öppnas i mallredigeraren.
1. I strukturvyn klickar du på **[!UICONTROL Policy]** ![Policy](/help/forms/assets/Smock_FeedManagement_18_N.svg) -ikonen på menyraden. I **[!UICONTROL Allowed Components]** och välj **[!UICONTROL Adaptive Forms Container]**  kryssrutan under **[AEM Archetype Project Name] - Adaptiv form**.
1. Klicka på **[!UICONTROL Done]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419370?quality=12&learn=on)

+++

## Skapa ett adaptivt formulär {#create-an-adaptive-form-in-sites-editor-or-experience-fragment}

Du kan skapa ett helt nytt formulär från grunden och anpassa det specifikt efter dina krav och designönskemål, direkt på en AEM Sites-sida eller i Experience Fragment. För enstaka formulär rekommenderar vi direktredigering till en AEM Sites-sida, medan Experience Fragments är idealiskt för formulär som behöver återanvändas på flera sidor på webbplatsen.

* [Skapa ett formulär på en AEM Sites-sida](#create-an-adaptive-form-in-sites-editor)
* [Skapa ett formulär i ett Experience Fragment](#create-an-adaptive-form-in-experience-fragment)
* [Konvertera ett anpassat formulär på en AEM Sites-sida till ett Experience Fragment](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)

### Skapa ett formulär på en AEM Sites-sida {#create-an-adaptive-form-in-sites-editor}

Du kan använda komponenten Adaptiv formulärbehållare AEM sidredigeraren för att skapa ett anpassat formulär. Med komponenten kan du skapa ett formulär genom att dra och släppa formulärkomponenterna. Formulärkomponenterna är baserade på kärnkomponenter. Du kan enkelt anpassa dessa efter organisationens behov.

>[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

Så här skapar du ett adaptivt formulär på en webbplatssida:

1. Öppna AEM Sites-sidan i redigeringsläge.
1. Dra och släpp **[!UICONTROL Adaptive Forms Container]** -komponenten från komponentwebbläsaren till sidan Platser. Det skapar ett blanksteg på sidan för formuläret. Du kan använda layoutläget för att ändra storleken på behållarutrymmet.
1. Dra och släpp adaptiva kärnkomponenter i formulär till behållarutrymmet för att skapa formuläret.
1. Lägg till knappen Skicka.

Nästa steg [ange åtgärden Skicka](#configure-submit-action-for-form) och avancerade egenskaper.

### Skapa ett formulär i ett Experience Fragment {#create-an-adaptive-form-in-experience-fragment}

Ni kan utöka räckvidden för era formulär genom att lägga till dem i AEM Experience Fragments, vilket möjliggör smidig återanvändning på flera sidor eller webbplatser. Du kan till exempel inkludera ett formulär för anmälan av nyhetsbrev i ett Experience Fragment. På så sätt kan du enkelt återanvända fragmentet på flera sidor på webbplatsen, vilket eliminerar behovet av att återskapa formuläret upprepade gånger. Alla uppdateringar eller ändringar som görs i formuläret för anmälan av nyhetsbrev i Experience Fragment sprids automatiskt till alla sidor där det används. Detta effektiviserar processen och ger en smidig användarupplevelse samtidigt som det förenklar hanteringen av webbplatsens formulär.

Så här skapar du ett anpassat formulär i ett Experience Fragment:

1. Öppna ett Experience Fragment.
1. Dra och släpp **[!UICONTROL Adaptive Forms Container]** -komponenten från komponentwebbläsaren till Experience Fragment.
1. Dra och släpp adaptiva kärnkomponenter i formulär till behållarutrymmet i Experience Fragment för att skapa formuläret.
1. Lägg till knappen Skicka.

Nästa steg [ange åtgärden Skicka](#configure-submit-action-for-form) och avancerade egenskaper.

### Konvertera ett formulär på en AEM Sites-sida till ett Experience Fragment {#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment}

Du kan konvertera ett befintligt adaptivt formulär i en webbplatssidredigerare till ett Experience Fragment för att återanvända formuläret på flera sidor eller webbplatser.

Så här konverterar du ett adaptivt formulär på en AEM Sites-sida till ett Experience Fragment:

1. Öppna AEM Sites-sidan som innehåller det adaptiva formuläret (i adaptiva Forms Container-komponenten) i redigeringsläge.
1. Öppna innehållsträdet och välj **[!UICONTROL Adaptive Forms Container]** som är värd för din adaptiva form. En AEM Sites-sida kan vara värd för flera adaptiva Forms. Välj rätt adaptiva Forms-behållare.
1. På menyraden väljer du ![Ikonen Konvertera till upplevelsefragment](/help/forms/assets/Smock_FilingCabinet_18_N.svg) Konvertera till Experience Fragment-variationsikon.
   ![Klicka på filkabinettlogotypen för att konvertera ett adaptivt formulär på AEM Sites-sidan till ett Experience Fragment](/help/forms/assets/convert-form-in-sites-page-to-an-experience-fragment.png)

   En dialogruta visas om du vill konvertera behållaren för det adaptiva formuläret till ett nytt Experience Fragment eller lägga till i ett befintligt Experience Fragment
1. I dialogrutan Konvertera till Experience Fragment-variation anger du värden för följande alternativ:

   * **Åtgärd:** Välj det här alternativet om du vill skapa ett Experience Fragment eller Lägg till i ett befintligt Experience Fragment.
   * **Överordnad sökväg:** Ange sökvägen till den mapp där Experience Fragment ska vara värd. Alternativet är bara tillgängligt för att skapa ett Experience Fragment.
   * **Mall:** Ange sökvägen till Experience Fragment-mallen. Om du inte har någon Experience Fragment-mall [skapa](/help/implementing/developing/extending/experience-fragments.md). Alternativet är bara tillgängligt för att lägga till adaptiv form till ett befintligt Experience Fragment.
   * **Fragmenttitel:** Ange Experience Fragment-titel. Titeln identifierar en Experience Fragment unikt


## Konfigurera åtgärden Skicka för ett formulär på AEM Sites-sidan eller i referensfragmentet {#configure-submit-action-for-form}

Med en Skicka-åtgärd kan du välja målet för data som har hämtats via ett anpassat formulär. Den aktiveras när en användare klickar på knappen Skicka på ett anpassat formulär. Anpassade formulär innehåller några av de åtgärder som har vidtagits för att skicka in. Du kan också utöka en standardåtgärd för att skicka för att skapa en egen anpassad åtgärd. Så här konfigurerar du en Skicka-åtgärd för formuläret:

1. Öppna AEM Page Editor eller Experience Fragment som innehåller det adaptiva formuläret.
1. Öppna innehållsträdet och välj **[!UICONTROL Adaptive Forms Container]** som är värd för din adaptiva form. En AEM Sites-sida kan vara värd för flera adaptiva Forms. Välj rätt adaptiva Forms-behållare.
1. Klicka på egenskaperna för den adaptiva formulärbehållaren ![Egenskaper för adaptiv formulärbehållare](/help/forms/assets/configure-icon.svg) -ikon. Dialogrutan Adaptiv formulärbehållare där du kan konfigurera skicka-åtgärder öppnas.
   ![Klicka på ikonen Bläddra för att öppna dialogrutan Adaptiv formulärbehållare och konfigurera åtgärden Skicka för ett adaptivt formulär](/help/forms/assets/adaptive-forms-container.png)
1. Välj och konfigurera en Skicka-åtgärd utifrån dina krav. Mer information om Skicka åtgärder finns i [Inlämningsåtgärd för anpassat formulär](/help/forms/configuring-submit-actions.md)


## Konfigurera ett schema eller en formulärdatamodell för ett formulär på en AEM Sites-sida eller i ett Experience Fragment {#configure-schema-or-data-model-for-form}

Du kan använda formulärdatamodellen för att ansluta ett formulär till en datakälla för att skicka och ta emot data baserat på användaråtgärder. Du kan också ansluta ett formulär till ett JSON-schema för att ta emot skickade data i ett fördefinierat format. Beroende på vad som krävs kan du ansluta formuläret till ett JSON-schema eller en formulärdatamodell:

* [Skapa ett JSON-schema och överför det till din miljö](/help/forms/adaptive-form-json-schema-form-model.md)  eller
* [Skapa en formulärdatamodell](/help/forms/create-form-data-models.md)

Så här konfigurerar du ett JSON-schema eller en formulärdatamodell för formuläret:

1. Öppna AEM Page Editor eller Experience Fragment som innehåller det adaptiva formuläret.
1. Öppna innehållsträdet och välj **[!UICONTROL Adaptive Forms Container]** som är värd för din adaptiva form. En AEM Sites-sida kan vara värd för flera adaptiva Forms. Välj rätt adaptiva Forms-behållare.
1. Klicka på egenskaperna för den adaptiva formulärbehållaren ![Egenskaper för adaptiv formulärbehållare](/help/forms/assets/configure-icon.svg) -ikon. Dialogrutan Adaptiv formulärbehållare öppnas för att konfigurera datamodeller.
   ![Klicka på skiftnyckelsikonen för att konfigurera datamodeller för det adaptiva formuläret](/help/forms/assets/form-data-model-adaptive-forms-container.png)
1. Välj och konfigurera ett JSON-schema eller en formulärdatamodell utifrån dina behov. Mer information om Skicka åtgärder finns i [Inlämningsåtgärd för anpassat formulär](/help/forms/configuring-submit-actions.md).

   * När du väljer **[!UICONTROL Form Model]** -alternativ, använd **[!UICONTROL Select Form Data Model]** för att välja en förkonfigurerad formulärdatamodell.
   * När du väljer **[!UICONTROL Schema]** -alternativ, använd **[!UICONTROL Schema]** för att välja ett JSON-schema för formuläret.

1. Klicka på **[!UICONTROL Done]**.

## Konfigurera en förifyllningstjänst för ett formulär på AEM Sites-sidan eller i Experience Fragment {#configure-prefill-service-for-form}

Du kan använda förifyllningstjänsten för att autofylla fält i ett adaptivt formulär med befintliga data. När en användare öppnar ett formulär är värdena för dessa fält förifyllda. Du kan:

* [Skapa en anpassad förifyllningstjänst](/help/forms/prepopulate-adaptive-form-fields.md)
* [Använd förifyllningstjänsten för formulärdatamodell](#fdm-prefill-service)

### Använd förifyllningstjänsten för formulärdatamodell för att fylla i fält i ett formulär i förväg på en AEM Sites-sida eller i ett Expert Fragment {#fdm-prefill-service}

Du kan använda förifyllningstjänsten för formulärdatamodell för att fylla i fält i ett adaptivt formulär på en AEM Sites-sida eller i ett Experience Fragment med hjälp av en formulärdatamodell eller en anpassad förifyllningstjänst. Tjänsten för förifyllnad av formulärdatamodell använder [Hämta tjänst för konfigurerad formulärdatamodell](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services) för att hämta data. Så här använder du förifyllningstjänsten för formulärdatamodell för ett adaptivt formulär:

1. Öppna AEM Page Editor eller Experience Fragment som innehåller det adaptiva formuläret.
1. Öppna innehållsträdet och välj **[!UICONTROL Adaptive Forms Container]** som är värd för din adaptiva form. En AEM Sites-sida kan vara värd för flera adaptiva Forms. Välj rätt adaptiva Forms-behållare.
1. Klicka på egenskaperna för den adaptiva formulärbehållaren ![Egenskaper för adaptiv formulärbehållare](/help/forms/assets/configure-icon.svg) -ikon. Dialogrutan Adaptiv formulärbehållare öppnas för att konfigurera datamodeller.
   ![Klicka på ikonen för skiftläge för att öppna dialogrutan Adaptiv formulärbehållare och konfigurera förifyllningstjänsten för det adaptiva formuläret](/help/forms/assets/adaptive-forms-container.png)
1. Välj en formulärdatamodell. Öppna **[!UICONTROL Basic]** -fliken. I förifyllningstjänsten väljer du **[!UICONTROL Form Data Model Prefill Service]**.
1. Klicka på **[!UICONTROL Done]**. Ditt adaptiva formulär har nu konfigurerats för att använda förifyllning av formulärdatamodell. Nu kan du använda [regelredigerare](rule-editor.md) om du vill skapa regler för förifyllning av formulärfält.


## Dirigera om användaren till en sida eller visa ett tackmeddelande när formuläret skickas

När du skickar ett formulär kan du dirigera om användaren till en annan webbsida eller ett meddelande. Så här omdirigerar du användaren eller konfigurerar tackmeddelandet:

1. Öppna AEM Page Editor eller Experience Fragment som innehåller det adaptiva formuläret.
1. Öppna innehållsträdet och välj **[!UICONTROL Adaptive Forms Container]** som är värd för din adaptiva form. En AEM Sites-sida kan vara värd för flera adaptiva Forms. Välj rätt adaptiva Forms-behållare.

1. Öppna **[!UICONTROL Submission]** -fliken.

   * Om du vill konfigurera en omdirigerings-URL för alternativet Skicka väljer du **[!UICONTROL Redirect to URL]** och bläddra och markera en AEM Sites-sida, eller ange en URL-adress för en extern sida.
   * Om du vill konfigurera ett anpassat meddelande eller ett tackmeddelande väljer du alternativet Skicka i **[!UICONTROL Show Message]** och skriv ett meddelande i **[!UICONTROL Message content]** box. Det är en RTF-ruta som du kan använda helskärmsalternativet för att visa alla tillgängliga RTF-objekt.


<!--
## See next

* [Create style or themes for your forms](using-themes-in-core-components.md)
* [Add dynamic behavior to forms using the rule editor](rule-editor.md)
* [Set layout of forms for different screen sizes and device types](/help/sites-cloud/authoring/features/responsive-layout.md)

-->

## Se även {#see-also}

{{see-also}}
* [Lägga till dynamiskt beteende i formulär med regelredigeraren](rule-editor.md)
* [Ange formulärlayout för olika skärmstorlekar och enhetstyper](/help/sites-cloud/authoring/features/responsive-layout.md)


