---
title: Hur lägger man till ett adaptivt formulär på en AEM Sites-sida?
description: Upptäck hur du skapar eller lägger till ett anpassat formulär på din AEM Sites-sida. Lär dig även fördelarna och olika sätt att integrera formulär på din webbplats.
feature: Adaptive Forms, Foundation Components
Keywords: AF in Sites editor, af in aem sites, aem sites af, add af to a sites page, af aem sites, af sites, create af in a sites page, adaptive form in aem sites, forms aem sites, add form to a sites page, adaptive forms aem sites, add adaptive forms to aem page, create forms in an aem sites page
exl-id: a1846c5d-7b0f-4f48-9d15-96b2a8836a9d
role: User, Developer
source-git-commit: 5b55a280c5b445d366c7bf189b54b51e961f6ec2
workflow-type: tm+mt
source-wordcount: '3206'
ht-degree: 0%

---

# Lägga till ett anpassat formulär på en AEM Sites-sida eller ett Experience Fragment {#create-or-add-an-adaptive-form-to-aem-sites-page}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/create-or-add-an-adaptive-form-to-aem-sites-page.html?lang=sv-SE) |
| AEM as a Cloud Service | Den här artikeln |

## Ökning {#overview}

Med AEM Forms kan du enkelt lägga till ett formulär på din AEM Sites-sida. På så sätt kan besökarna enkelt fylla i och skicka in formulär utan att lämna den sida de är på. På så sätt kan de enkelt hålla kontakten med andra element på webbplatsen samtidigt som de interagerar aktivt med formuläret.

Du kan använda AEM Page Editor för att snabbt skapa och lägga till flera formulär på dina AEM Sites-sidor. Med AEM Page Editor kan man skapa sömlösa datainhämtningsmöjligheter på en webbsida med hjälp av adaptiva formulärkomponenter som dynamiskt beteende, validering, dataintegrering, generering av urkunder och automatisering av affärsprocesser. Du kan även använda olika funktioner på AEM Sites-sidor, som versionshantering, målgruppsanpassning, översättning och hantering av flera webbplatser.

AEM Forms Cloud Service har adaptiv formulärbehållare och adaptiv Forms - inbäddningskomponenter. Du kan använda adaptiv formulärbehållare för att skapa ett formulär på en AEM Sites-sida eller i ett Experience Fragment, medan adaptiv Forms - Embed-komponent gör att du kan lägga till ett befintligt adaptivt formulär eller skapa ett formulär med Adaptiv Forms Editor.

![Ett exempel på ett anpassat formulär på en AEM Sites-sida](/help/forms/assets/adaptive-form-in-sites-page.png)

## Varför använda adaptiva Forms Core-komponenter för att skapa ett adaptivt formulär på AEM Sites-sidor eller i Experience Fragment?

Om du tidigare har skapat adaptiva Forms Foundation-komponenter eller rena HTML-baserade formulär för dina webbplatser rekommenderar Adobe att du använder adaptiva Forms Core-komponenter för att skapa ett adaptivt formulär på AEM Sites eller i Experience Fragment. Här kan ni använda olika funktioner på AEM Sites-sidor, som versionshantering, målgruppsanpassning, översättning och hantering av flera webbplatser, vilket förbättrar den övergripande upplevelsen av att skapa och hantera formulär för Adaptiv Forms. Låt oss utforska några av dessa funktioner:

* **Versionshantering:** På AEM Sites-sidor finns [robusta versionshanteringsfunktioner](/help/sites-cloud/authoring/sites-console/page-versions.md) som gör att du kan spåra och hantera olika versioner av dina formulär. På så sätt kan du göra ändringar och förbättringar i formulär samtidigt som du behåller möjligheten att vid behov gå tillbaka till tidigare versioner. Versionshantering säkerställer ett kontrollerat och organiserat tillvägagångssätt för blankettutveckling och -utveckling.
* **Målgruppsanpassning (integrering med Adobe Target):** Med funktioner för målgruppsanpassning för AEM Sites-sidor kan du även [anpassa formulärupplevelsen för olika målgrupper](/help/sites-cloud/integrating/integrating-adobe-target.md). Genom att använda användarsegment och kriterier för målinriktning kan du anpassa formulärets innehåll, design eller beteende till specifika användargrupper. På så sätt kan ni leverera en personaliserad och relevant formulärupplevelse, vilket ökar engagemanget och konverteringsgraden.
* **Översättning:** AEM Sites [sömlös integration med översättningstjänster](/help/sites-cloud/administering/translation/overview.md) så att du enkelt kan översätta formulär till flera språk. Den här funktionen förenklar lokaliseringsprocessen och säkerställer att formulären är tillgängliga för en global publik. Ni kan hantera översättningar effektivt i AEM översättningsprojekt, vilket minskar den tid och det arbete som krävs för flerspråkigt formulärstöd. Mer information om översättning finns i avsnittet med överväganden.
* **Hantering av flera webbplatser och Live Copy:** AEM Sites har effektiva [funktioner för hantering av flera webbplatser och Live Copy](/help/sites-cloud/administering/msm/overview.md), vilket gör att du kan skapa och hantera flera webbplatser i en och samma miljö. Med den här funktionen kan du nu återanvända formulär på olika webbplatser, vilket ger enhetlighet och minskar dubbelarbetet. Med centraliserad kontroll och hantering kan ni effektivt hantera och uppdatera formulär på flera webbplatser.
* **Teman:** På AEM Sites-sidor finns ett ramverk för att utforma och underhålla enhetliga visuella format på flera webbsidor. Dessa definierar färger, teckensnitt, formatmallar och andra visuella element som bidrar till webbplatsens allmänna utseende och känsla. [Du kan använda teman som är utformade för en AEM Sites-sida för ett adaptivt formulär, vilket sparar tid och arbete](/help/sites-cloud/administering/site-creation/site-themes.md#using-site-themes-using-themes).
* **Taggning:** På AEM Sites-sidor kan du [tilldela taggar eller etiketter till en sida, en resurs eller annat innehåll](/help/implementing/developing/introduction/tagging-framework.md). Taggar är nyckelord eller metadataetiketter som gör det möjligt att kategorisera och ordna innehåll baserat på specifika kriterier. Du kan tilldela en eller flera taggar till sidor, resurser eller andra innehållsobjekt i AEM för att förbättra sökningen och kategorisera resurserna.
* **Låsa och låsa upp innehåll:** Med AEM Sites kan användare [styra åtkomst och ändringar av sidor](/help/sites-cloud/authoring/page-editor/edit-content.md) i AEM Sites-miljön. När en sida är låst innebär det att den skyddas från obehöriga ändringar och redigeringar av andra användare. Endast den användare som har låst innehållet eller en utsedd administratör kan låsa upp det för att tillåta ändringar.

Dessutom använder Adaptiv Forms i AEM sidredigerare [adaptiva Forms Core-komponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=sv-SE#features). Dessa kärnkomponenter tillhandahåller en standard och enklare metod för att formatera och anpassa komponenterna, som är identisk med [AEM Sites WCM-komponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=sv-SE).


## Hur skapar eller lägger man till ett adaptivt formulär på AEM Sites-sidan eller i AEM Experience Fragment? {#various-options-to-creat-or-add-an-adaptive-form-in-aem-sites-page-or-aem-experience-fragment}

Du kan utnyttja den här funktionen till fullo genom att använda följande alternativ:

* **[Skapa och lägg till ett anpassat anpassat formulär på en AEM Sites-sida](#create-an-adaptive-form-in-sites-editor-or-experience-fragment):** Du kan använda komponenten Adaptiv formulärbehållare för att skapa ett helt nytt formulär från grunden och anpassa det specifikt efter dina behov och designönskemål.

* **[Skapa och lägg till ett anpassat anpassat formulär i ett Experience Fragments](#create-an-adaptive-form-in-sites-editor):** Du kan utöka formulärens räckvidd genom att lägga till dem i AEM Experience Fragments, vilket möjliggör smidig återanvändning på flera sidor eller webbplatser.

* **[Konvertera ett anpassat formulär till Experience Fragment](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment):** Konvertera ett anpassat formulär som lagts till på en AEM Sites-sida till ett Experience Fragment för återanvändning av formuläret på flera AEM Sites-sidor.

* **[Skapa och lägg till formulär baserade på godkända mallar på en AEM Sites-sida:](/help/forms/embed-adaptive-form-aem-sites.md#embed-form-using-adaptive-form-wizzard-aem-sites)** Du kan använda redan godkända mallar för att snabbt skapa adaptiv Forms som är anpassad efter organisationens riktlinjer för varumärken och designstandarder. Alternativet är bara tillgängligt för Adaptiv Forms som har skapats med Adaptiv Forms Editor eller Adaptiv Forms - Bädda in komponent.

* **[Lägg till befintliga formulär på en AEM Sites-sida:](/help/forms/embed-adaptive-form-aem-sites.md#embed-an-adaptive-form-in-sites-editor)** Du kan enkelt integrera formulär som du redan har skapat på dina webbplatser så att besökarna kan interagera med dem direkt. Alternativet är bara tillgängligt för Adaptiv Forms som har skapats med Adaptiv Forms Editor eller Adaptiv Forms - Bädda in komponent.


* **Lägg till flera formulär på en AEM Sites-sida eller i ett Experience Fragment:** Du kan skapa eller lägga till flera adaptiva Forms på en AEM Sites-sida för att ge flera alternativ för användare baserat på deras inställningar och krav. Dessa kan vara en kombination av helt nya formulär från grunden och befintliga formulär. Du kan använda komponenten **[!UICONTROL Adaptive Form Container]** flera gånger för att lägga till Adaptiv Forms på en AEM Sites-sida. Du kan använda komponenten **[!UICONTROL Adaptive Forms - Embed]** flera gånger på en AEM Sites-sida, endast om alternativet **[!UICONTROL Form covers entire width of the frame]** har valts. Om alternativet **[!UICONTROL Form covers entire width of the frame]** inte är markerat stöder AEM Sites-sidan endast ett adaptivt formulär som ska finnas utan iframe. Om du vill lägga till mer adaptiv Forms med komponenten **[!UICONTROL Adaptive Forms - Embed]** väljer du alternativet **[!UICONTROL Form covers entire width of the frame]**.

## Att tänka på när du skapar ett adaptivt formulär på en AEM Sites-sida eller i AEM Experience Fragment {#consideration}

* När du använder den adaptiva formulärbehållaren för att skapa eller lägga till ett formulär, översätts och lokaliseras formulären via AEM Sites översättningsflöde. För varje språk genereras en separat kopia (språkkopia) av webbplatssidan och motsvarande formulär. När en innehållsförfattare ändrar en regel i ett formulär på den överordnade sidan måste samma ändringar göras i alla språkkopior av formuläret. Med adaptiv formulärbehållare kan du även använda olika funktioner på AEM Sites-sidor, som versionshantering, målgruppsanpassning, översättning och hantering av flera webbplatser.

* När du skapar eller lägger till ett formulär med komponenten Adaptiv formulärinbäddning översätts och lokaliseras formulären med hjälp av AEM Forms översättningsflöde. I det här fallet finns det ett enda formulär som du kan referera till på alla språkkopior av webbplatssidorna. Adaptiv Form-embed-komponent ger inte åtkomst till olika funktioner på AEM Sites-sidor som versionshantering, målgruppsanpassning, översättning och hantering av flera webbplatser.


## Krav för att skapa eller lägga till ett adaptivt formulär på AEM Sites-sidan eller AEM Experience Fragment {#before-you-start-creating-an-adaptive-form}

Innan du börjar skapa eller skapa ett adaptivt formulär lägger du till adaptiva Forms Client Libraries på din AEM Sites-sida:


### Lägg till adaptiva Forms Client Libraries på din AEM Sites-sida eller i din Experience

**Fall 1: Använda komponenter för separata webbplatser**

Om du vill aktivera alla funktioner för den adaptiva Forms-behållarkomponenten lägger du till klientbiblioteken CustomHeaderlibs och CustomFoterlibs på din AEM Sites-sida via distributionsflödet. Så här lägger du till biblioteken:

1. Få åtkomst till och klona din [AEM Cloud Service Git-databas](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/repositories.html?lang=sv-SE).
1. Öppna mappen AEM Cloud Service Git-databas i en textredigerare för en plan. Exempel: Microsoft Visual Code.
1. Öppna filen `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\page\customheaderlibs.html` och lägg till följande kod i filen:

   ```
       //Customheaderlibs.html
   
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
       </sly> 
   ```

1. Öppna filen `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\page\customfooterlibs.html` och lägg till följande kod i filen:

   ```
       //customfooterlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
       </sly> 
   ```

1. Öppna filen `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\xfpage\customheaderlibs.html` och lägg till följande kod i filen:

   ```
       //Customheaderlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
       </sly> 
   ```

1. Öppna filen `ui.apps\src\main\content\jcr_root\apps\[your-project]\components\xfpage\customfooterlibs.html` och lägg till följande kod i filen:

   ```
       //customfooterlibs.html
       <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
       <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
       </sly> 
   ```

1. [Kör distributionsflödet](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html?lang=sv-SE) för att distribuera klientbiblioteken till din AEM as a Cloud Service-miljö.

>[!NOTE]
>
> Maskinkoda klientbiblioteket för anpassade funktioner endast när det krävs för alla formulär. För bibliotek som skiljer sig åt beroende på formulärtyp lägger du till dem via mallsidans profiler, vilket förklaras i nästa avsnitt.

**Fall 2: Använda sidkomponenten för samma platser**

Inkludera runtime client-biblioteken eller anpassade funktionsbibliotek i mallens sidprofil som används för att skapa sidor med formulär.

1. Öppna AEM Sites eller Experience Fragment för redigering. Om du vill öppna sidan för redigering markerar du sidan och klickar på **[!UICONTROL Edit]**.
2. Öppna mallen för webbplatserna eller sidan för Experience Fragment. Öppna mallen genom att gå till **[!UICONTROL Page Information]** ![Sidinformation](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL Edit Template]**. Motsvarande mall öppnas i mallredigeraren.
3. Gå till avsnittet **[!UICONTROL Page Information]** ![Sidinformation](/help/forms/assets/Smock_Properties_18_N.svg) i mallen och välj alternativet **[!UICONTROL Page Policy]**. Då öppnas egenskaperna för AEM Sites-mallen, där du kan definiera anpassade funktioner eller klientbibliotek för körningsmiljön.
4. Klicka på knappen **[!UICONTROL Add]** på fliken **[!UICONTROL Properties]** om du vill lägga till nya anpassade funktionsbibliotek eller körningsbibliotek.
5. Klicka på **[Klar]**.

>[!VIDEO](https://video.tv.adobe.com/v/3476178?quality=12&learn=on)

### Aktivera anpassad Forms-behållare för din AEM Sites-sida eller Experience Fragment

Så här aktiverar du komponenten [!UICONTROL Adaptive Forms Container] i mallprincipen:

1. Öppna AEM Sites eller Experience Fragment för redigering. Om du vill öppna sidan för redigering markerar du sidan och klickar på Redigera.
1. Öppna mallen för webbplatserna eller sidan för Experience Fragment. Öppna mallen genom att gå till [!UICONTROL Page Information] ![Sidinformation](/help/forms/assets/Smock_Properties_18_N.svg) > [!UICONTROL Edit Template]. Motsvarande mall öppnas i mallredigeraren.
1. Klicka på ikonen **[!UICONTROL Policy]** ![Princip](/help/forms/assets/Smock_FeedManagement_18_N.svg) på menyraden i strukturvyn. I listan **[!UICONTROL Allowed Components]** och markera kryssrutan **[!UICONTROL Adaptive Forms Container]** under **[Projektnamn för AEM-arkityp] - anpassat formulär**.
1. Klicka på **[!UICONTROL Done]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419370?quality=12&learn=on)

## Skapa ett adaptivt formulär {#create-an-adaptive-form-in-sites-editor-or-experience-fragment}

Du kan skapa ett helt nytt formulär från grunden och anpassa det specifikt efter dina krav och designönskemål, direkt på en AEM Sites-sida eller i Experience Fragment. För enstaka formulär rekommenderar vi direktredigering till en AEM Sites-sida, medan Experience Fragments är idealiskt för formulär som behöver återanvändas på flera sidor på webbplatsen.

* [Skapa ett formulär på en AEM Sites-sida](#create-an-adaptive-form-in-sites-editor)
* [Skapa ett formulär i ett Experience Fragment](#create-an-adaptive-form-in-experience-fragment)
* [Konvertera ett anpassat formulär på en AEM Sites-sida till ett Experience Fragment](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)

### Skapa ett formulär på en AEM Sites-sida {#create-an-adaptive-form-in-sites-editor}

Du kan använda komponenten Adaptiv formulärbehållare i AEM Page Editor för att skapa ett anpassat formulär. Med komponenten kan du skapa ett formulär genom att dra och släppa formulärkomponenterna. Formulärkomponenterna är baserade på kärnkomponenter. Du kan enkelt anpassa dessa efter organisationens behov.

>[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

Så här skapar du ett adaptivt formulär på en webbplatssida:

1. Öppna AEM Sites-sidan i redigeringsläge.
1. Dra och släpp komponenten **[!UICONTROL Adaptive Forms Container]** från komponentwebbläsaren till sidan Platser. Det skapar ett blanksteg på sidan för formuläret. Du kan använda layoutläget för att ändra storleken på behållarutrymmet.
1. Dra och släpp adaptiva kärnkomponenter i formulär till behållarutrymmet för att skapa formuläret.
1. Lägg till knappen Skicka.

Sedan [ställer du in åtgärden Skicka](#configure-submit-action-for-form) och avancerade egenskaper.

### Skapa ett formulär i ett Experience Fragment {#create-an-adaptive-form-in-experience-fragment}

Ni kan utöka räckvidden för era formulär genom att lägga till dem i AEM Experience Fragments, så att ni kan återanvända dem på flera sidor eller webbplatser. Du kan till exempel inkludera ett formulär för anmälan av nyhetsbrev i ett Experience Fragment. På så sätt kan du enkelt återanvända fragmentet på flera sidor på webbplatsen, vilket eliminerar behovet av att återskapa formuläret upprepade gånger. Alla uppdateringar eller ändringar som görs i formuläret för anmälan av nyhetsbrev i Experience Fragment sprids automatiskt till alla sidor där det används. Detta effektiviserar processen och ger en smidig användarupplevelse samtidigt som det förenklar hanteringen av webbplatsens formulär.

Så här skapar du ett anpassat formulär i ett Experience Fragment:

1. Öppna ett Experience Fragment.
1. Dra och släpp komponenten **[!UICONTROL Adaptive Forms Container]** från komponentwebbläsaren till Experience Fragment.
1. Dra och släpp adaptiva kärnkomponenter i formulär till behållarutrymmet i Experience Fragment för att skapa formuläret.
1. Lägg till knappen Skicka.

Sedan [ställer du in åtgärden Skicka](#configure-submit-action-for-form) och avancerade egenskaper.

### Konvertera ett formulär på en AEM Sites-sida till ett Experience Fragment {#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment}

Du kan konvertera ett befintligt adaptivt formulär i en webbplatssidredigerare till ett Experience Fragment för att återanvända formuläret på flera sidor eller webbplatser.

Så här konverterar du ett adaptivt formulär på en AEM Sites-sida till ett Experience Fragment:

1. Öppna AEM Sites-sidan som innehåller det adaptiva formuläret (i adaptiva Forms Container-komponenten) i redigeringsläge.
1. Öppna innehållsträdet och markera **[!UICONTROL Adaptive Forms Container]** som är värd för ditt adaptiva formulär. En AEM Sites-sida kan vara värd för flera adaptiva Forms. Välj rätt adaptiva Forms-behållare.
1. Välj ikonen ![Konvertera till upplevelsefragment](/help/forms/assets/Smock_FilingCabinet_18_N.svg) Konvertera till upplevelsefragment på menyraden.
   ![Klicka på filkabinettlogotypen för att konvertera ett adaptivt formulär på AEM Sites-sidan till ett Experience Fragment](/help/forms/assets/convert-form-in-sites-page-to-an-experience-fragment.png)

   En dialogruta visas om du vill konvertera behållaren för det adaptiva formuläret till ett nytt Experience Fragment eller lägga till i ett befintligt Experience Fragment
1. I dialogrutan Konvertera till Experience Fragment-variation anger du värden för följande alternativ:

   * **Åtgärd:** Välj för att skapa en upplevelsefragment eller Lägg till i ett befintligt upplevelsefragment.
   * **Överordnad sökväg:** Ange sökvägen till den mapp där Experience Fragment ska vara värd. Alternativet är bara tillgängligt för att skapa ett Experience Fragment.
   * **Mall:** Ange sökvägen till Experience Fragment-mallen. Om du inte har någon Experience Fragment-mall [skapar du den](/help/implementing/developing/extending/experience-fragments.md). Alternativet är bara tillgängligt för att lägga till adaptiv form till ett befintligt Experience Fragment.
   * **Fragmenttitel:** Ange Experience Fragment-titel. Titeln identifierar en Experience Fragment unikt


## Konfigurera åtgärden Skicka för ett formulär på AEM Sites-sidan eller i referensfragmentet {#configure-submit-action-for-form}

Med en Skicka-åtgärd kan du välja målet för data som har hämtats via ett anpassat formulär. Den aktiveras när en användare klickar på knappen Skicka på ett anpassat formulär. Anpassade formulär innehåller några av de åtgärder som har vidtagits för att skicka in. Du kan också utöka en standardåtgärd för att skicka för att skapa en egen anpassad åtgärd. Så här konfigurerar du en Skicka-åtgärd för formuläret:

1. Öppna AEM Page Editor eller Experience Fragment som innehåller det adaptiva formuläret.
1. Öppna innehållsträdet och markera **[!UICONTROL Adaptive Forms Container]** som är värd för ditt adaptiva formulär. En AEM Sites-sida kan vara värd för flera adaptiva Forms. Välj rätt adaptiva Forms-behållare.
1. Klicka på ikonen för den adaptiva formulärbehållaren ![Egenskaper för den adaptiva formulärbehållaren](/help/forms/assets/configure-icon.svg) . Dialogrutan Adaptiv formulärbehållare där du kan konfigurera skicka-åtgärder öppnas.
   ![Klicka på skiftnyckelsikonen för att öppna dialogrutan Adaptiv formulärbehållare och konfigurera åtgärden Skicka för ett adaptivt formulär](/help/forms/assets/adaptive-forms-container.png)
1. Välj och konfigurera en Skicka-åtgärd utifrån dina krav. Mer information om Skicka-åtgärder finns i [Åtgärden Skicka anpassat formulär](/help/forms/configuring-submit-actions.md)


## Konfigurera ett schema eller en formulärdatamodell (FDM) för ett formulär på en AEM Sites-sida eller i ett Experience Fragment {#configure-schema-or-data-model-for-form}

Du kan använda formulärdatamodellen (FDM) för att ansluta ett formulär till en Data Source för att skicka och ta emot data baserat på användaråtgärder. Du kan också ansluta ett formulär till ett JSON-schema för att ta emot skickade data i ett fördefinierat format. Beroende på behovet kan du ansluta formuläret till ett JSON-schema eller en formulärdatamodell (FDM):

* [Skapa ett JSON-schema och överför det till din miljö](/help/forms/adaptive-form-json-schema-form-model.md) eller
* [Skapa en formulärdatamodell (FDM)](/help/forms/create-form-data-models.md)

Så här konfigurerar du ett JSON-schema eller en formulärdatamodell (FDM) för formuläret:

1. Öppna AEM Page Editor eller Experience Fragment som innehåller det adaptiva formuläret.
1. Öppna innehållsträdet och markera **[!UICONTROL Adaptive Forms Container]** som är värd för ditt adaptiva formulär. En AEM Sites-sida kan vara värd för flera adaptiva Forms. Välj rätt adaptiva Forms-behållare.
1. Klicka på ikonen för den adaptiva formulärbehållaren ![Egenskaper för den adaptiva formulärbehållaren](/help/forms/assets/configure-icon.svg) . Dialogrutan Adaptiv formulärbehållare öppnas för att konfigurera datamodeller.
   ![Klicka på skiftnyckelsikonen för att konfigurera datamodeller för det adaptiva formuläret](/help/forms/assets/form-data-model-adaptive-forms-container.png)
1. Välj och konfigurera ett JSON-schema eller en formulärdatamodell (FDM) utifrån dina behov. Mer information om Skicka åtgärder finns i [Åtgärden Skicka anpassat formulär](/help/forms/configuring-submit-actions.md).

   * När du väljer alternativet **[!UICONTROL Form Model]** använder du alternativet **[!UICONTROL Select Form Data Model]** för att välja en förkonfigurerad formulärdatamodell (FDM).
   * När du väljer alternativet **[!UICONTROL Schema]** använder du alternativet **[!UICONTROL Schema]** för att välja ett JSON-schema för formuläret.

1. Klicka på **[!UICONTROL Done]**.

## Konfigurera en förifyllningstjänst för ett formulär på AEM Sites-sidan eller i Experience Fragment {#configure-prefill-service-for-form}

Du kan använda förifyllningstjänsten för att autofylla fält i ett adaptivt formulär med befintliga data. När en användare öppnar ett formulär är värdena för dessa fält förifyllda. Du kan:

* [Skapa en anpassad förifyllningstjänst](/help/forms/prepopulate-adaptive-form-fields.md)
* [Använd förifyllningstjänsten för formulärdatamodell](#fdm-prefill-service)

### Använd förifyllningstjänsten för formulärdatamodell för att fylla i fält i ett formulär i förväg på en AEM Sites-sida eller i ett Expert Fragment {#fdm-prefill-service}

Du kan använda förifyllningstjänsten för formulärdatamodell för att fylla i fält i ett adaptivt formulär på en AEM Sites-sida eller i ett Experience Fragment med hjälp av en formulärdatamodell eller en anpassad förifyllningstjänst. Tjänsten för förifyllning av formulärdatamodell använder tjänsten [Hämta tjänst för den konfigurerade formulärdatamodellen](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services) för att hämta data. Så här använder du förifyllningstjänsten för formulärdatamodell för ett adaptivt formulär:

1. Öppna AEM Page Editor eller Experience Fragment som innehåller det adaptiva formuläret.
1. Öppna innehållsträdet och markera **[!UICONTROL Adaptive Forms Container]** som är värd för ditt adaptiva formulär. En AEM Sites-sida kan vara värd för flera adaptiva Forms. Välj rätt adaptiva Forms-behållare.
1. Klicka på ikonen för den adaptiva formulärbehållaren ![Egenskaper för den adaptiva formulärbehållaren](/help/forms/assets/configure-icon.svg) . Dialogrutan Adaptiv formulärbehållare öppnas för att konfigurera datamodeller.
   ![Klicka på skiftnyckelsikonen för att öppna dialogrutan Adaptiv formulärbehållare och konfigurera förifyllningstjänsten för det adaptiva formuläret](/help/forms/assets/adaptive-forms-container.png)
1. Välj en formulärdatamodell. Öppna fliken **[!UICONTROL Basic]**. Välj **[!UICONTROL Form Data Model Prefill Service]** i förifyllningstjänsten.
1. Klicka på **[!UICONTROL Done]**. Ditt adaptiva formulär har nu konfigurerats för att använda förifyllning av formulärdatamodell. Du kan nu använda [regelredigeraren](rule-editor.md) för att skapa regler för att fylla i formulärfält i förväg.


## Dirigera om användaren till en sida eller visa ett tackmeddelande när formuläret skickas

När du skickar ett formulär kan du dirigera om användaren till en annan webbsida eller ett meddelande. Så här omdirigerar du användaren eller konfigurerar tackmeddelandet:

1. Öppna AEM Page Editor eller Experience Fragment som innehåller det adaptiva formuläret.
1. Öppna innehållsträdet och markera **[!UICONTROL Adaptive Forms Container]** som är värd för ditt adaptiva formulär. En AEM Sites-sida kan vara värd för flera adaptiva Forms. Välj rätt adaptiva Forms-behållare.

1. Öppna fliken **[!UICONTROL Submission]**.

   * Om du vill konfigurera en omdirigerings-URL, för alternativet Skicka, markerar du alternativet **[!UICONTROL Redirect to URL]** och bläddrar och väljer en AEM Sites-sida, eller anger en URL för en extern sida.
   * Om du vill konfigurera ett anpassat meddelande eller ett tackmeddelande för alternativet Skicka markerar du alternativet **[!UICONTROL Show Message]** och anger ett meddelande i rutan **[!UICONTROL Message content]**. Det är en RTF-ruta som du kan använda helskärmsalternativet för att visa alla tillgängliga RTF-objekt.


