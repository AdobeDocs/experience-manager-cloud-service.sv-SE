---
title: Hur lägger man till ett adaptivt formulär på en AEM Sites-sida?
description: Lägg smidigt in Adaptiv Forms på en AEM Sites-sida eller en webbsida som ligger utanför AEM.
feature: Adaptive Forms
role: Admin, User, Developer
Keywords: Forms AEM Sites, Embed Form to a Sites page, Adaptive Forms AEM Sites, Embed Adaptive Forms to AEM Page, Embed Forms in an AEM Sites page
exl-id: 359b05e8-d8c1-4a77-9e70-6f6b6e668560
source-git-commit: 5321fed58f66b2beabcacc2de4b7dfb2dc3754f1
workflow-type: tm+mt
source-wordcount: '2934'
ht-degree: 0%

---

# Bädda in ett anpassat formulär på en AEM webbplatssida {#embed-an-adaptive-form-to-aem-sites-page}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/embed-adaptive-form-aem-sites.html) |
| AEM as a Cloud Service | Den här artikeln |


## Ökning {#overview}

Med AEM Forms kan formulärutvecklare smidigt bädda in Adaptiv Forms på en AEM Sites-sida eller en webbsida som ligger utanför AEM. Det inbäddade adaptiva formuläret fungerar fullt ut och användarna kan fylla i och skicka formuläret utan att behöva lämna sidan. Det hjälper användaren att hålla sig i rätt sammanhang för andra element på webbsidan och interagera samtidigt med formuläret. Detta gör att användarna enkelt kan fylla i och skicka formulär utan att behöva lämna den sida de är på. Den här integreringen är ett bekvämt sätt att återanvända adaptiva Forms som de redan har skapat.

Du kan använda AEM Page Editor för att snabbt bädda in flera formulär på dina AEM Sites-sidor. Med AEM Page Editor kan skribenter skapa sömlösa datainhämtningsupplevelser på en Sites-sida med hjälp av adaptiva Forms-komponenter, inklusive dynamiskt beteende, validering, dataintegrering, generering av dokument för post- och affärsprocessautomatisering. Du kan även använda olika funktioner på AEM Sites-sidor, som versionshantering, målgruppsanpassning, översättning och hantering av flera webbplatser.

AEM Forms tillhandahåller komponenter för **[!UICONTROL Adaptive Form Container]** och **[!UICONTROL Adaptive Forms – Embed(v2)]**. Du kan använda komponenten **[!UICONTROL Adaptive Forms – Embed(v2)]** för att lägga till ett befintligt adaptivt formulär eller skapa ett formulär med Adaptiv Forms Editor, medan **[!UICONTROL Adaptive Form Container]** för att skapa ett nytt formulär på en Experience Fragment- eller AEM Sites-sida.

![Ett exempel på ett anpassat formulär på en AEM Sites-sida](/help/forms/assets/adaptive-form-in-sites-page.png)

<!-- For information about embedding an Adaptive Form in an external web page, see [Embed Adaptive Form in external web page](/help/forms/using/embed-adaptive-form-external-web-page.md). 

## Why embed an Adaptive Form in AEM Sites page or AEM Experience Fragment? 

Using **[!UICONTROL Adaptive Forms – Embed(v2)]** in AEM Page Editor lets you create seamless data capture experiences within a Sites page using the power of Adaptive Forms components including dynamic behavior, validations, data integration, generate document of record and business process automation. It also lets you use various features of AEM Sites pages like, versioning, targeting, translation, and multi-site manager, enhancing the overall form creation and management experience. Let's explore some of these features:

* **Versioning:** AEM Sites pages offer [robust versioning capabilities](/help/sites-cloud/authoring/sites-console/page-versions.md), allowing you to track and manage different versions of your forms. This enables you to make changes and enhancements to forms while maintaining the ability to roll back to previous versions if needed. Versioning ensures a controlled and organized approach to form development and evolution.
* **Targeting (Integration with Adobe Target):** With AEM Sites pages targeting capabilities, you can also [personalize the form experience for different audiences](/help/sites-cloud/integrating/integrating-adobe-target.md). By using user segments and targeting criteria, you can tailor the form's content, design, or behavior to specific groups of users. This enables you to provide a personalized and relevant form experience, increasing engagement and conversion rates.
* **Translation:** AEM Sites [seamless integration with translation services](/help/sites-cloud/administering/translation/overview.md), allowing you to translate forms into multiple languages easily. This feature simplifies the localization process, ensuring that your forms are accessible to a global audience. You can manage translations efficiently within AEM translation projects, reducing time and effort required for multilingual form support. See considerations section for more information on translation.  
* **Multi-site Management and Live Copy:** AEM Sites provide robust [Multi-site Management and Live Copy capabilities](/help/sites-cloud/administering/msm/overview.md), enabling you to create and manage multiple websites within a single environment. This feature now lets you reuse forms across different sites, ensuring consistency and reducing duplication efforts. With centralized control and management, you can efficiently maintain and update forms across multiple websites.
* **Themes:** AEM Sites pages provide a framework for designing and maintaining consistent visual styles across multiple web pages. These define colors, fonts, style sheets, and other visual elements that contribute to the overall look and feel of the website. [You can use the themes designed for an AEM Sites page for an Adaptive Form, saving time and effort](/help/sites-cloud/administering/site-creation/site-themes.md#using-site-themes-using-themes). 
* **Tagging:** AEM Sites pages allow you to [assign tags or labels to a page, an asset, or other content](/help/implementing/developing/introduction/tagging-framework.md). Tags are keywords or metadata labels that provide a way to categorize and organize content based on specific criteria. You can assign one or more tags to pages, assets, or any other content items within AEM to improve search and categorize the assets. 
* **Locking and Unlocking content:** AEM Sites allow users to [control access and modifications to pages](/help/sites-cloud/authoring/page-editor/edit-content.md) within the AEM Sites environment. When a page is locked, it means that it is protected from unauthorized changes or edits by other users. Only the user who has locked the content or a designated administrator can unlock it to allow modifications. 

In addition, Adaptive Forms in AEM Page Editor use [Adaptive Forms Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=en#features). These Core Components provide a standard and easier methods to style and customize the components, identical to [AEM Sites WCM Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=en).

-->

## Hur skapar eller bäddar jag in ett anpassat formulär på AEM Sites-sidan eller i AEM Experience Fragment? {#various-options-to-create-or-embed-an-adaptive-form-in-aem-sites-page-or-aem-experience-fragment}

Du kan utnyttja den här funktionen fullt ut genom att använda följande alternativ:

* **[Skapa ett adaptivt formulär med godkända mallar och bädda in det på en AEM Sites-sida](#embed-form-using-adaptive-form-wizzard-aem-sites):** Du kan använda redan godkända mallar för att snabbt skapa och bädda in adaptiv Forms som är anpassad efter organisationens riktlinjer och designstandarder.

* **[Bädda in befintliga formulär på en AEM Sites-sida](#embed-an-adaptive-form-in-sites-editor):** Du kan enkelt integrera formulär som du redan har skapat på dina webbplatser så att besökarna kan interagera direkt med dem.

* **[Konvertera ett inbäddat anpassat formulär till Experience Fragment](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment):** Konvertera ett inbäddat anpassat formulär som lagts till på en AEM Sites-sida till ett Experience Fragment för återanvändning av formuläret på flera AEM Sites-sidor.

* **[Skapa och lägg till ett anpassat anpassat formulär på en AEM Sites-sida](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md#create-an-adaptive-form-in-sites-editor-or-experience-fragment):** Du kan använda komponenten **[!UICONTROL Adaptive Form Container]** för att skapa ett helt nytt formulär från grunden och anpassa det specifikt efter dina krav och designinställningar.

* **[Skapa och lägg till ett anpassat anpassat formulär i ett Experience Fragments](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md#create-an-adaptive-form-in-sites-editor):** Du kan utöka formulärens räckvidd genom att lägga till dem i AEM Experience Fragments, vilket möjliggör smidig återanvändning på flera sidor eller webbplatser.

* **Lägg till flera formulär på en AEM Sites-sida eller i ett Experience Fragment:** Du kan skapa eller lägga till flera adaptiva Forms på en AEM Sites-sida för att ge flera alternativ för användare baserat på deras inställningar och krav. Du kan använda AEM Page Editor för att snabbt bädda in flera formulär på dina AEM Sites-sidor. Du kan använda komponenten **[!UICONTROL Adaptive Form Container]** flera gånger för att lägga till Adaptiv Forms på en AEM Sites-sida. Du kan använda komponenten **[!UICONTROL Adaptive Forms - Embed]** flera gånger på en AEM Sites-sida, endast om alternativet **[!UICONTROL Form covers entire width of the frame]** har valts. Om alternativet **[!UICONTROL Form covers entire width of the frame]** inte är markerat stöder AEM Sites-sidan endast ett adaptivt formulär som ska finnas utan iframe. Om du vill lägga till mer adaptiv Forms med komponenten **[!UICONTROL Adaptive Forms - Embed]** väljer du alternativet **[!UICONTROL Form covers entire width of the frame]**.

## Att tänka på när du bäddar in ett anpassat formulär på en AEM Sites-sida eller AEM Experience Fragment {#consideration}

* När du skapar eller lägger till ett formulär med komponenten **[!UICONTROL Adaptive Forms – Embed(v2)]**, översätts och lokaliseras formulären med hjälp av AEM Forms översättningsflöde. I det här fallet finns det ett enda formulär som du kan referera till på alla språkkopior av webbplatssidorna. **[!UICONTROL Adaptive Forms – Embed(v2)]**-komponenten ger inte åtkomst till olika funktioner på AEM Sites-sidor, som versionshantering, målgruppsanpassning, översättning och hantering av flera webbplatser.

* När du använder **[!UICONTROL Adaptive Form Container]** för att skapa ett formulär genomgår formulären översättning och lokalisering via AEM Sites översättningsflöde. För varje språk genereras en separat kopia (språkkopia) av webbplatssidan och motsvarande formulär. När en innehållsförfattare ändrar en regel i ett formulär på den överordnade sidan måste samma ändringar göras i alla språkkopior av formuläret. I **[!UICONTROL Adaptive Form Container]** kan du även använda olika funktioner på AEM Sites-sidor, som versionshantering, målgruppsanpassning, översättning och hantering av flera webbplatser.


## Krav för att bädda in ett anpassat formulär på AEM Sites-sidan eller AEM Experience Fragment {#before-you-start-embedding-an-adaptive-form}

Innan du börjar bädda in ett nytt adaptivt formulär eller ett befintligt adaptivt formulär med **[!UICONTROL Adaptive Forms – Embed(v2)]** aktiverar du **Adaptiva Forms Core-komponenter** och lägger till **adaptiva Forms Client Libraries** på din AEM Sites-sida:

+++  Aktivera adaptiva Forms Core-komponenter för din AEM Cloud Service-miljö

Kontrollera att de [adaptiva Forms Core-komponenterna är aktiverade för din AEM Forms as a Cloud Service miljö](enable-adaptive-forms-core-components.md).

+++

+++  Lägg till adaptiva Forms-klientbibliotek på din AEM Sites-sida eller Experience Fragment

När alternativet **[!UICONTROL When form covers entire width of a page]** är markerat i dialogrutan **[!UICONTROL Form Containers]** Konfigurera och Adaptiv Forms med hjälp av kärnkomponenter används, måste klientbiblioteken inkluderas på sidan för motsvarande webbplats.

![När formuläret täcker hela bredden på en sida är det valt och adaptiva formulär med kärnkomponenter används](/help/forms/assets/overlaycorecomponent.gif)


Lägg till klientbiblioteken **CustomHeaderlibs** och **CustomFoterlibs** på din AEM Sites-sida med hjälp av distributionsflödet. Så här lägger du till klientbiblioteken:

1. Få åtkomst till och klona din [AEM Cloud Service Git-databas](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/repositories.html).
1. Öppna AEM Cloud Service Git-databasmappen i en textredigerare för en plan. Exempel: Microsoft® Visual Code.
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

1. [Kör distributionsflödet](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) för att distribuera klientbiblioteken till din AEM as a Cloud Service-miljö.

+++

+++ Aktivera **[!UICONTROL Adaptive Forms – Embed(v2)]** för din AEM Sites-sida eller Experience Fragment

Så här aktiverar du komponenten **[!UICONTROL Adaptive Forms – Embed(v2)]** i mallprincipen:

1. Öppna AEM Sites eller Experience Fragment för redigering. Om du vill öppna sidan för redigering markerar du sidan och klickar på **[!UICONTROL Edit]**.
1. Öppna mallen för webbplatserna eller sidan för Experience Fragment. Öppna mallen genom att gå till **[!UICONTROL Page Information]** ![Sidinformation](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL Edit Template]**. Motsvarande mall öppnas i mallredigeraren.
1. Klicka på ikonen **[!UICONTROL Policy]** ![Princip](/help/forms/assets/Smock_FeedManagement_18_N.svg) på menyraden i strukturvyn. I listan **[!UICONTROL Allowed Components]** och markera kryssrutan **[!UICONTROL Adaptive Forms – Embed(v2)]** under projektnamnet **[AEM Archetype ] - Adaptiv form**.
1. Klicka på **[!UICONTROL Done]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419369?quality=12&learn=on)

+++

## Bädda in ett adaptivt formulär med komponenten Adaptiv Forms - Embed(v2) {#embed-an-adaptive-form-in-sites-editor-or-experience-fragment}

Använd komponenten **[!UICONTROL Adaptive Forms - Embed(v2)]** för att skapa ett adaptivt formulär direkt i AEM Sites-redigeraren med hjälp av guiden Skapa formulär. Det resulterande formuläret sparas som en extern enhet, vilket gör att det kan återanvändas på andra webbplatssidor och fristående formulär. Du kan bädda in ett helt nytt formulär från grunden och anpassa det specifikt efter dina krav och designönskemål, direkt på en AEM Sites-sida eller i Experience Fragment. För enstaka formulär rekommenderas direktredigering på en AEM Sites-sida, medan Experience Fragments är idealiskt för formulär som måste återanvändas på flera sidor på webbplatsen.

Du kan enkelt bädda in ett nytt formulär med **[!UICONTROL Adaptive Forms - Embed(v2)]**.  Tänk dig till exempel att infoga ett nytt kontaktformulär på en AEM Sites-sida eller AEM Experience Fragment. Alla uppdateringar eller ändringar som görs i kontaktformuläret på AEM Sites-sidan eller i Experience Fragment gäller automatiskt alla sidor där det distribueras. Detta förenklar hanteringen av webbplatsens formulär, vilket ger en smidig användarupplevelse och effektiviserar hela processen.

Med **[!UICONTROL Adaptive Forms - Embed(v2)]** kan du:

* [Bädda in ett nytt formulär med Adaptive Forms Wizard på AEM Sites Page](#embed-form-using-adaptive-form-wizzard-aem-sites)
* [Bädda in ett nytt formulär med hjälp av guiden Adaptiv Forms i ett Experience Fragment](#embed-form-using-adaptive-form-wizzard-experience-fragment)
* [Bädda in ett befintligt adaptivt formulär på en AEM Sites-sida](#embed-an-adaptive-form-in-sites-editor)
* [Bädda in ett befintligt formulär i ett Experience Fragment](#embed-an-adaptive-form-in-experience-fragment)
* [Konvertera ett anpassat formulär på en AEM Sites-sida till ett Experience Fragment](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)

### Bädda in ett nytt formulär med Adaptive Forms Wizard på AEM Sites Page {#embed-form-using-adaptive-form-wizzard-aem-sites}

Steg för att bädda in nya formulär på en AEM Sites-sida är:

1. Öppna AEM Sites-sidan i redigeringsläge.
1. Dra och släpp komponenten **[!UICONTROL Adaptive Forms - Embed(v2)]** på sidan från panelen Komponentwebbläsaren.
1. Klicka på ikonen **Plus** så dirigeras du till guiden för att skapa formulär.

   ![Adaptiv Forms - Bädda in komponent](/help/forms/assets/aemformcontainer.png)

1. Skapa ett nytt adaptivt formulär från guiden **[!UICONTROL Form Creation]**.
**[!UICONTROL Asset Path]** innehåller redan sökvägen till ett skapat anpassat formulär
1. Spara inställningarna. Det adaptiva formuläret är nu inbäddat på sidan.

>[!VIDEO](https://video.tv.adobe.com/v/3419366/adaptive-form-aem-forms?quality=12&learn=on)

Sedan kan du [ange åtgärden Skicka](/help/forms/configuring-submit-actions.md) och avancerade egenskaper för ett inbäddat adaptivt formulär med hjälp av guiden Skapa formulär.


### Bädda in ett nytt formulär med hjälp av guiden Adaptiv Forms i ett Experience Fragment {#embed-form-using-adaptive-form-wizzard-experience-fragment}

Steg för att bädda in nya formulär i en Experience Fragment är:

1. Öppna Experience Fragment i redigeringsläge.
1. Dra och släpp komponenten **[!UICONTROL Adaptive Forms - Embed(v2)]** på sidan från panelen Komponentwebbläsaren.
1. Klicka på ikonen **Plus** så dirigeras du till guiden för att skapa formulär.

   ![Adaptiv Forms - Bädda in komponent](/help/forms/assets/aemformcontainer.png)

1. Skapa ett nytt adaptivt formulär från guiden **[!UICONTROL Form Creation]**.
**[!UICONTROL Asset Path]** innehåller redan sökvägen till ett skapat anpassat formulär
1. Spara inställningarna. Det adaptiva formuläret är nu inbäddat i Experience Fragment.

Sedan kan du [ange åtgärden Skicka](/help/forms/configuring-submit-actions.md) och avancerade egenskaper för ett inbäddat adaptivt formulär med hjälp av guiden Skapa formulär.

### Bädda in ett befintligt adaptivt formulär på en AEM Sites-sida {#embed-an-adaptive-form-in-sites-editor}

Med komponenten **[!UICONTROL Adaptive Forms - Embed(v2)]** kan du enkelt integrera ett befintligt adaptivt formulär på en sida i AEM Sites. Den här funktionen gör det enklare att anpassa och återanvända Adaptive Forms, vilket ger kunderna ett bekvämt sätt att återanvända redan skapade formulär. Tänk dig att du kan lägga in ett kontaktformulär på en AEM Sites-sida och slippa återskapa formuläret flera gånger.

Så här bäddar du in ett befintligt adaptivt formulär på en webbplatssida:

1. Öppna AEM Sites-sidan i redigeringsläge.
1. Dra och släpp komponenten **[!UICONTROL Adaptive Forms - Embed(v2)]** från komponentwebbläsaren till sidan Platser.
1. Markera **[!UICONTROL Adaptive Forms - Embed]**-komponenten på sidan Platser och välj ![ Egenskaper för adaptiv formulärbehållare ](/help/forms/assets/configure-icon.svg) i åtgärdsfältet. Dialogrutan **[!UICONTROL Edit Adaptive Forms - Embed(v2)]** öppnas.
1. Bläddra och välj det adaptiva formulär som ska bäddas in i **[!UICONTROL Asset Path]**.
1. Spara inställningarna. Det adaptiva formuläret är nu inbäddat på sidan.

>[!VIDEO](https://video.tv.adobe.com/v/3419368?quality=12&learn=on)

Sedan kan du [ange åtgärden Skicka](/help/forms/configuring-submit-actions.md) och avancerade egenskaper för ett inbäddat adaptivt formulär med hjälp av guiden Skapa formulär.

### Bädda in ett befintligt anpassat formulär i ett Experience Fragment {#embed-an-adaptive-form-in-experience-fragment}

Du kan också utöka formulärens tillgänglighet genom att bädda in dem i AEM Experience Fragment. Så här bäddar du in ett anpassat formulär i ett Experience Fragment:

1. Öppna ett Experience Fragment i redigeringsläge.
1. Dra och släpp komponenten **[!UICONTROL Adaptive Forms - Embed(v2)]** från komponentwebbläsaren till Experience Fragment.
1. Markera **[!UICONTROL Adaptive Forms - Embed]**-komponenten i Experience Fragment och välj ![ egenskaper för adaptiv formulärbehållare ](/help/forms/assets/configure-icon.svg) i åtgärdsfältet. Dialogrutan **[!UICONTROL Edit Adaptive Forms - Embed(v2)]** öppnas.
1. Bläddra och välj det adaptiva formulär som ska bäddas in i **[!UICONTROL Asset Path]**.
1. Spara inställningarna. Det anpassade formuläret är nu inbäddat i Experience Fragment.

Sedan kan du [ange åtgärden Skicka](/help/forms/configuring-submit-actions.md) och avancerade egenskaper för ett inbäddat adaptivt formulär med hjälp av guiden Skapa formulär.

### Konvertera ett formulär på en AEM Sites-sida till ett Experience Fragment {#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment}

Du kan konvertera ett befintligt adaptivt formulär i en webbplatssidredigerare till ett Experience Fragment för att återanvända formuläret på flera sidor eller webbplatser.

Så här konverterar du ett adaptivt formulär på en AEM Sites-sida till ett Experience Fragment:

1. Öppna AEM Sites-sidan som innehåller det adaptiva formuläret (i adaptiva Forms Container-komponenten) i redigeringsläge.
1. Öppna innehållsträdet och markera **[!UICONTROL Adaptive Forms Container]** som är värd för ditt adaptiva formulär. En AEM Sites-sida kan vara värd för flera adaptiva Forms. Välj rätt adaptiva Forms-behållare.
1. På menyraden väljer du ikonen ![Konvertera till upplevelsefragment-variationsikonen ](/help/forms/assets/Smock_FilingCabinet_18_N.svg) Konvertera till upplevelsefragment-variationsikonen.

   ![Klicka på filkabinettlogotypen för att konvertera ett adaptivt formulär på AEM Sites-sidan till ett Experience Fragment](/help/forms/assets/convert-form-in-sites-page-to-an-experience-fragment.png)

   En dialogruta visas där du kan konvertera behållaren för adaptiva formulär till ett nytt Experience Fragment eller lägga till i ett befintligt Experience Fragment.

1. I variantdialogrutan **[!UICONTROL Convert to Experience Fragment]** anger du värden för följande alternativ:

   * **Åtgärd:** Välj för att skapa en upplevelsefragment eller Lägg till i ett befintligt upplevelsefragment.
   * **Överordnad sökväg:** Ange sökvägen till den mapp där Experience Fragment ska vara värd. Alternativet är bara tillgängligt för att skapa nya Experience Fragment.
   * **Mall:** Ange sökvägen till Experience Fragment-mallen. Om du inte har någon Experience Fragment-mall [skapar du den](/help/implementing/developing/extending/experience-fragments.md). Alternativet är bara tillgängligt för att lägga till adaptiv form till ett befintligt Experience Fragment.
   * **Fragmenttitel:** Ange Experience Fragment-titel. Titeln identifierar unikt en Experience Fragment.
   * **Fragment-taggar:** Ange tagg för Experience Fragment. Taggen identifierar unikt kategorin för en Experience Fragment.

## Konfigurera egenskaper för anpassad formulärinbäddning (v2)

Du kan anpassa de avancerade inställningarna för komponenten **[!UICONTROL Adaptive Form - Embed(v2)]**. I dialogrutan **[!UICONTROL Edit Adaptive Forms - Embed]** kan du ange följande:

* **Resurssökväg**: Bläddra och välj ett anpassat formulär att bädda in. Den fylls i automatiskt om du utelämnade den från Assets webbläsare.
* **Post Submission** : Välj den åtgärd som ska utlösas när formulär skickas. Du kan visa ett tackmeddelande eller en tacksida.
   * **Visa tackmeddelande**: Skriv ett meddelande med textredigeraren som ska visas när formulär skickas. Det här alternativet är endast tillgängligt när du väljer att visa ett tackmeddelande.
   * **Visa sidan Tack**: Bläddra och markera sidan som ska visas när formulär skickas. Det här alternativet är bara tillgängligt när du väljer att visa en tacksida.
   * **Omdirigering till dig:**: Aktivera alternativet att ersätta sidan som innehåller det inbäddade adaptiva formuläret med din tacksida. Annars ersätter du tacksidan det anpassade formuläret i komponenten **[!UICONTROL Adaptive Forms - Embed(v2)]**, utan att de underliggande webbplatserna uppdateras på sidan. Det här alternativet är bara tillgängligt när du väljer att visa en tacksida.
   * **Tack**: En kort bekräftelse eller bekräftelse som visas på skärmen när ett formulär har skickats.
   * **Tack-sidan**: Bläddra och markera den sida som ska visas när formuläret har skickats.

* **Använd sidspråk**: Använd lokala inställningar på AEM Sites-sidan i stället för de anpassade formulärspråken. Det här alternativet gäller endast för Adaptiv form (Foundation).
* **Sätt fokus på formulär**: Markera för att ange fokus på det första fältet i det adaptiva formuläret. Det här alternativet gäller endast för Adaptiv form (Foundation).
* **Tema**: Välj ett tema som definierar format för komponenter i det adaptiva formuläret. Formateringen innehåller utseendeegenskaper som teckensnittsstil, bakgrundsfärg, dimensioner och justering. Det här alternativet gäller endast för Adaptiv form (Foundation).

  >[!NOTE]
  >
  > Du kan bara använda alternativen **Använd sidspråk**, **Sätt fokus på formulär** och **Tema** för Adaptivt formulär (Foundation).

* **Formuläret täcker ramens hela bredd**:
En textbunden ram (iframe) är ett HTML-element som läser in ett adaptivt formulär på en AEM Sites-sida.

   * Om kryssrutan **[!UICONTROL Form covers entire width of the frame]** är markerad upptar ett adaptivt formulär hela bredden på behållaren där det placeras. I det här fallet används ingen iframe för att återge formuläret. Layouten och designen för ett adaptivt formulär anpassas efter behållarens hela bredd så att den blir responsiv och kan justeras till olika skärmstorlekar. Med det här alternativet kan du bädda in flera adaptiva Forms-filer på en AEM Sites-sida.

     >[!NOTE]
     >
     > Om du vill bädda in flera formulär på en AEM Sites-sida markerar du kryssrutan **[!UICONTROL Form covers entire width of the frame]**.

   * Om kryssrutan **[!UICONTROL Form covers entire width of the frame]** inte är markerad täcker ett adaptivt formulär inte hela behållarens bredd. I stället används en iframe för att återge formuläret, som inte kan utökas utanför en viss bredd. Detta är användbart när ett adaptivt formulär har definierade gränser och måste finnas tillsammans med andra AEM-komponenter bredvid det i behållaren. Om det här alternativet inte är markerat tillåter det endast att en Adaptiv Forms-sida på AEM Sites-sidan bäddas in utan iframe.

     >[!NOTE]
     >
     > AEM Sites-sidan stöder endast ett adaptivt formulär utan iframe. Om du vill lägga till mer adaptiv Forms med komponenten **[!UICONTROL Adaptive Forms - Embed]** väljer du alternativet **[!UICONTROL Form covers entire width of the frame]**.

* **Höjd**: Ange behållarens höjd. Lämna det tomt om du vill ändra storlek på behållaren automatiskt.
* **CSS-klientbibliotek**: Ange sökvägen till ett CSS-klientbibliotek.

<!--
In AEM Sites page, you can add an Adaptive Form using:

* **Adaptive Forms - Embed component**
   Adaptive Forms - Embed component enables AEM Sites authors to include an existing Adaptive Form within an AEM Sites page, thereby enhancing the reusability of adaptive forms. Existing Adaptive Forms can be used standalone or embedded in the site page. This integration provides a convenient way for customers to reuse Adaptive Forms they have already created.

* **Asset browser**
  All the forms are available under Assets. You can drag-drop the form as an asset on your page.

## Prerequisites {#prerequisites}

 To embed an Adaptive Form in an AEM Sites page that uses an editable template, ensure that the AEM Form component is configured as an allowed component in the associated template. 

In case **Adaptive Forms - Embed component** is not visible in the **Component browser panel** of AEM sites page, perform the following steps as illustrated in the video.

>[!VIDEO](https://video.tv.adobe.com/v/3410544)

In case Sites page is using a static template, you need to configure it in the paragraph system of the site page. 

## Embedding an Adaptive Form {#af-component}

To embed an Adaptive Form using the **[!UICONTROL Adaptive Forms - Embed]** component:

1. Open the AEM sites page, in edit mode, in which you want to embed an Adaptive Form.
1. From the Component browser panel, drag-drop the [!UICONTROL Adaptive Forms - Embed] component on the page. Alternatively, you can search for an Adaptive Form in the Assets browser and drag-drop it onto the Sites page. You can add a new Adaptive Form or embed an existing Adaptive Form. 

   >[!NOTE]
   >
   >Multiple Adaptive Forms - Embed components on a page are not supported.

1. To create and embed a new form, on the component toolbar, select the **Create Form** icon. A window to create the form opens. 

1. Select the embedded Adaptive Forms - Embed component in the sites page, and then select ![settings_icon](assets/settings_icon.png) on the action bar. The **[!UICONTROL Edit Adaptive Forms - Embed]** dialog opens.
1. In the Edit Adaptive Forms - Embed dialog, specify the following.

    **Asset Type:** Select the type of asset to embed. 
    * **Asset Path**: Browse and select the Adaptive Form to embed. It is auto-populated if you dropped it from the Assets browser.
    * **Post Submission** : Select the action to trigger on form submission. You can choose to show a thank you message or a thank you page.
        * Show

        * **Thank You Message**: Write a message using the rich text editor to show on form submission. This option is available only when you choose to show a thank you message.
        * **Thank You Page**: Browse and select the page to display on form submission. This option is available only when you choose to show a thank you page.
           * **Redirect to thank you page**: Enable the option to replace the page containing the embedded Adaptive Form with thank you page. Otherwise, the thank you page replaces the Adaptive Form in the [!UICONTROL Adaptive Forms - Embed] component, without refreshing underlying sites the page. This option is available only when you choose to show a thank you page.
    * **Use Page Language**: Use local of the AEM Sites page instead locale of Adaptive Form.
    * **Set Focus on Form**: Select to set the focus on the first field of the Adaptive Form.
    * **Theme**: Select a theme that defines styling for components of your Adaptive Form. Styling includes appearance properties such as font style, background color, dimensions, and alignment.
    * **Form covers entire width of the frame**: If checked, iframe is not used to render the form. 
    * **Height**: Specify the height of the container. Leave it blank to automatically resize the container.
    * **CSS Client library**: Specify path to a CSS client library.

1. Save the settings. The Adaptive Form  is now embedded in the page.


AEM site also lets you create an Adaptive Form on the fly using the Adaptive Forms - Embed component. Follow the steps to create an Adaptive Form using the **Adaptive Forms - Embed component** on AEM sites page:
1. Open the AEM sites page, in edit mode, in which you want to embed an Adaptive Form.
1. From the Component browser panel, drag-drop the Adaptive Forms - Embed component on the page.
1. Click the **Plus** icon and you are redirected to the form creation wizard.

    ![Adaptive Forms - Embed Component](/help/forms/assets/aemformcontainer.png)

1. You can now embed an Adaptive Form on AEM site pages using the [!UICONTROL AEM Forms Container Component].
-->

## Publish inbäddade adaptiva formulär {#publishing-embedded-adaptive-form}

Vi ska titta på följande scenarier för publicering av ett inbäddat adaptivt formulär på AEM webbplatssida:

* Om du publicerar sidan AEM webbplatser för första gången och den innehåller ett inbäddat adaptivt formulär publicerar du webbplatssidan och den inbäddade resursen.
* Om du bara ändrade det inbäddade adaptiva formuläret på en publicerad webbplatssida publicerar du den ursprungliga resursen och ändringarna återspeglas på den publicerade webbplatssidan. Den publicerade webbplatssidan innehåller en referens till resursen och behöver inte publicera om sidan.
* Om du har ändrat webbplatssidan och det inbäddade adaptiva formuläret publicerar du om webbplatssidan och den inbäddade resursen.

## Ändra inbäddat anpassat formulär  {#modifying-embedded-adaptive-form}

Om du vill ändra någon konfiguration eller egenskap för det inbäddade adaptiva formuläret gör du något av följande.

* Öppna originalformuläret i ett adaptivt formulär i respektive redigerare och ändra dem.
* Markera det adaptiva formuläret på webbplatssidan i redigeringsläge och välj sedan **[!UICONTROL Edit in a new window]**. Det ursprungliga formuläret öppnas i redigeringsläge som du kan ändra.

>[!NOTE]
>
>De ändringar som gjorts i det ursprungliga adaptiva formuläret återspeglas automatiskt i det inbäddade formuläret. Publicera dock om det adaptiva formuläret eller webbplatsens sida så att ändringarna på den publicerade sidan återspeglas.

## God praxis {#best-practices}

Tänk på följande när du bäddar in Adaptiv Forms på AEM webbplatser:

* Sidhuvud och sidfot i det ursprungliga formuläret inkluderas inte i det inbäddade formuläret.
* Användarutkast och inskickade inbäddade formulär stöds och visas på flikarna Utkast och Skickat Forms på Forms Portal.
* Den skicka-åtgärd som är konfigurerad i det ursprungliga formuläret behålls i det inbäddade formuläret.
* Om du har konfigurerat Adobe Analytics för det ursprungliga formuläret hämtas analysdata från det inbäddade formuläret i Adobe Analytics. Den är dock inte tillgänglig i rapporten för formuläranalys.

## Se även {#see-also}

* [Skapa grundläggande komponentbaserad fristående adaptiv Forms](/help/forms/creating-adaptive-form-core-components.md)
* [Skapa grundkomponentbaserade adaptiva formulär direkt på en AEM Sites-sida](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md)
