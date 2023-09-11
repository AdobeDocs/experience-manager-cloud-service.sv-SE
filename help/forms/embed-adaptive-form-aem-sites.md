---
title: Bädda in ett anpassat formulär på AEM Sites-sidan
seo-title: How to add an Adaptive Form to an AEM Sites page?
description: Du kan använda komponenten Adaptiv Forms - Embed för att bädda in adaptiv Forms på en AEM Sites-sida, så att du kan fylla i och skicka ett formulär utan att lämna AEM Sites-sidorna.
feature: Adaptive Forms
Keywords: Forms AEM Sites, Embed Form to a Sites page, Adaptive Forms AEM Sites, Embed Adaptive Forms to AEM Page, Embed Forms in an AEM Sites page
exl-id: 359b05e8-d8c1-4a77-9e70-6f6b6e668560
source-git-commit: d9dee0b5a070da6a19004c749f69c724fff9d967
workflow-type: tm+mt
source-wordcount: '2966'
ht-degree: 0%

---

# Bädda in ett anpassat formulär på en AEM webbplatssida {#embed-an-adaptive-form-to-aem-sites-page}

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/embed-adaptive-form-aem-sites.html) |
| AEM as a Cloud Service | Den här artikeln |


## Översikt {#overview}

Med AEM Forms kan formulärutvecklare smidigt bädda in Adaptiv Forms på en AEM Sites-sida eller en webbsida som ligger utanför AEM. Det inbäddade adaptiva formuläret fungerar fullt ut och användarna kan fylla i och skicka formuläret utan att behöva lämna sidan. Det hjälper användaren att hålla sig i rätt sammanhang för andra element på webbsidan och interagera samtidigt med formuläret. Detta gör att användarna enkelt kan fylla i och skicka formulär utan att behöva lämna den sida de är på. Den här integreringen är ett bekvämt sätt att återanvända adaptiva Forms som de redan har skapat.

Du kan använda AEM Page Editor för att snabbt bädda in flera formulär på dina AEM Sites-sidor. Med AEM Page Editor kan skribenter skapa sömlösa datainhämtningsupplevelser på en Sites-sida med hjälp av adaptiva Forms-komponenter, inklusive dynamiskt beteende, validering, dataintegrering, generering av dokument för post- och affärsprocessautomatisering. Du kan även använda olika funktioner på AEM Sites-sidor, som versionshantering, målgruppsanpassning, översättning och hantering av flera webbplatser.

AEM Forms tillhandahåller **[!UICONTROL Adaptive Form Container]** och **[!UICONTROL Adaptive Forms – Embed(v2)]** -komponenter. Du kan använda **[!UICONTROL Adaptive Forms – Embed(v2)]** för att lägga till ett befintligt adaptivt formulär eller skapa ett formulär med Adaptiv Forms Editor, samtidigt som **[!UICONTROL Adaptive Form Container]** för att skapa nya formulär på en Experience Fragment- eller AEM Sites-sida.

![Ett exempel på ett adaptivt formulär på en AEM Sites-sida](/help/forms/assets/adaptive-form-in-sites-page.png)

<!-- For information about embedding an Adaptive Form in an external web page, see [Embed Adaptive Form in external web page](/help/forms/using/embed-adaptive-form-external-web-page.md). 

## Why embed an Adaptive Form in AEM Sites page or AEM Experience Fragment? 

Using **[!UICONTROL Adaptive Forms – Embed(v2)]** in AEM Page Editor lets you create seamless data capture experiences within a Sites page using the power of Adaptive Forms components including dynamic behavior, validations, data integration, generate document of record and business process automation. It also lets you use various features of AEM Sites pages like, versioning, targeting, translation, and multi-site manager, enhancing the overall form creation and management experience. Let's explore some of these features:

* **Versioning:** AEM Sites pages offer [robust versioning capabilities](/help/sites-cloud/authoring/features/page-versions.md), allowing you to track and manage different versions of your forms. This enables you to make changes and enhancements to forms while maintaining the ability to roll back to previous versions if needed. Versioning ensures a controlled and organized approach to form development and evolution.
* **Targeting (Integration with Adobe Target):** With AEM Sites pages targeting capabilities, you can also [personalize the form experience for different audiences](/help/sites-cloud/integrating/integration-adobe-target-ims.md). By leveraging user segments and targeting criteria, you can tailor the form's content, design, or behavior to specific groups of users. This enables you to provide a personalized and relevant form experience, increasing engagement and conversion rates.
* **Translation:** AEM Sites [seamless integration with translation services](/help/sites-cloud/administering/translation/overview.md), allowing you to translate forms into multiple languages easily. This feature simplifies the localization process, ensuring that your forms are accessible to a global audience. You can manage translations efficiently within AEM translation projects, reducing time and effort required for multilingual form support. See considerations section for more information on translation.  
* **Multi-site Management and Live Copy:** AEM Sites provide robust [Multi-site Management and Live Copy capabilities](/help/sites-cloud/administering/msm/overview.md), enabling you to create and manage multiple websites within a single environment. This feature now lets you reuse forms across different sites, ensuring consistency and reducing duplication efforts. With centralized control and management, you can efficiently maintain and update forms across multiple websites.
* **Themes:** AEM Sites pages provide a framework for designing and maintaining consistent visual styles across multiple web pages. These define colors, fonts, style sheets, and other visual elements that contribute to the overall look and feel of the website. [You can use the themes designed for an AEM Sites page for an Adaptive Form, saving time and effort](/help/sites-cloud/administering/site-creation/site-themes.md#using-site-themes-using-themes). 
* **Tagging:** AEM Sites pages allow you to [assign tags or labels to a page, an asset, or other content](/help/implementing/developing/introduction/tagging-framework.md). Tags are keywords or metadata labels that provide a way to categorize and organize content based on specific criteria. You can assign one or more tags to pages, assets, or any other content items within AEM to improve search and categorize the assets. 
* **Locking and Unlocking content:** AEM Sites allow users to [control access and modifications to pages](/help/sites-cloud/authoring/fundamentals/editing-content.md) within the AEM Sites environment. When a page is locked, it means that it is protected from unauthorized changes or edits by other users. Only the user who has locked the content or a designated administrator can unlock it to allow modifications. 

In addition, Adaptive Forms in AEM Page Editor use [Adaptive Forms Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=en#features). These Core Components provide a standard and easier methods to style and customize the components, identical to [AEM Sites WCM Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=en).

-->

## Hur skapar eller bäddar jag in ett anpassat formulär på AEM Sites-sidan eller i AEM Experience Fragment? {#various-options-to-create-or-embed-an-adaptive-form-in-aem-sites-page-or-aem-experience-fragment}

Du kan utnyttja den här funktionen fullt ut genom att använda följande alternativ:

* **[Skapa ett adaptivt formulär med godkända mallar och bädda in det på en AEM Sites-sida](#embed-form-using-adaptive-form-wizzard-aem-sites):** Ni kan använda redan godkända mallar för att snabbt skapa och bädda in adaptiva Forms som är anpassade efter företagets riktlinjer och designstandarder.

* **[Bädda in befintliga formulär på en AEM Sites-sida](#embed-an-adaptive-form-in-sites-editor):** Ni kan enkelt integrera formulär som ni redan har skapat på era webbplatser, så att besökarna kan interagera direkt med dem.

* **[Konvertera ett inbäddat anpassat formulär till Experience Fragment](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment):** Konvertera ett inbäddat adaptivt formulär som lagts till på en AEM Sites-sida till ett Experience Fragment för återanvändning av formuläret på flera AEM Sites-sidor.

* **[Skapa och lägga till ett anpassat anpassat formulär på en AEM Sites-sida](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md#create-an-adaptive-form-in-sites-editor-or-experience-fragment):** Du kan använda **[!UICONTROL Adaptive Form Container]** för att skapa ett helt nytt formulär från grunden och skräddarsy det specifikt efter dina behov och designönskemål.

* **[Skapa och lägga till ett anpassat anpassat formulär i ett Experience Fragments](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md#create-an-adaptive-form-in-sites-editor):** Ni kan utöka räckvidden för era formulär genom att lägga till dem i AEM Experience Fragments, vilket möjliggör smidig återanvändning på flera sidor eller webbplatser.

* **Lägga till flera formulär på en AEM Sites-sida eller Experience Fragment:**  Du kan skapa eller lägga till flera adaptiva Forms-filer på en AEM Sites-sida för att ge flera alternativ beroende på användarens önskemål och önskemål. Du kan använda AEM Page Editor för att snabbt bädda in flera formulär på dina AEM Sites-sidor. Du kan använda **[!UICONTROL Adaptive Form Container]** flera gånger för att lägga till Adaptiv Forms på en AEM Sites-sida. Du kan använda **[!UICONTROL Adaptive Forms - Embed]** flera gånger på en AEM Sites-sida, endast om **[!UICONTROL Form covers entire width of the frame]** är markerat. Om **[!UICONTROL Form covers entire width of the frame]** om alternativet inte är markerat stöder AEM Sites-sidan endast ett adaptivt formulär som ska finnas utan iframe. Lägga till mer adaptiv Forms med **[!UICONTROL Adaptive Forms - Embed]** komponent, markera **[!UICONTROL Form covers entire width of the frame]** alternativ.

## Att tänka på när du bäddar in ett anpassat formulär på en AEM Sites-sida eller AEM Experience Fragment {#consideration}

* När du skapar eller lägger till ett formulär med **[!UICONTROL Adaptive Forms – Embed(v2)]** kan formulären översättas och lokaliseras med hjälp av AEM Forms översättningsflöde. I det här fallet finns det ett enda formulär som du kan referera till på alla språkkopior av webbplatssidorna. **[!UICONTROL Adaptive Forms – Embed(v2)]** -komponenten ger inte åtkomst till olika funktioner på AEM Sites-sidor som versionshantering, målgruppsanpassning, översättning och hantering av flera webbplatser.

* När du använder **[!UICONTROL Adaptive Form Container]** om du vill skapa ett formulär, översätts och lokaliseras formulären via AEM Sites översättningsflöde. För varje språk genereras en separat kopia (språkkopia) av webbplatssidan och motsvarande formulär. När en innehållsförfattare ändrar en regel i ett formulär på den överordnade sidan måste samma ändringar göras i alla språkkopior av formuläret. **[!UICONTROL Adaptive Form Container]** Med kan du också använda olika funktioner på AEM Sites-sidor, som versionshantering, målgruppsanpassning, översättning och hantering av flera webbplatser.


## Krav för att bädda in ett anpassat formulär på AEM Sites-sidan eller AEM Experience Fragment {#before-you-start-embedding-an-adaptive-form}

Innan du börjar bädda in ett nytt adaptivt formulär eller ett befintligt adaptivt formulär med **[!UICONTROL Adaptive Forms – Embed(v2)]**, aktivera **Adaptiva Forms Core-komponenter** och lägga till **Adaptiva Forms-klientbibliotek** till din AEM Sites-sida:

+++  Aktivera adaptiva Forms Core-komponenter för din AEM Cloud Service-miljö

Se till att [Adaptiva Forms Core-komponenter är aktiverade för din as a Cloud Service AEM Forms-miljö](enable-adaptive-forms-core-components.md).

+++

+++  Lägg till adaptiva Forms-klientbibliotek på din AEM Sites-sida eller Experience Fragment

När **[!UICONTROL When form covers entire width of a page]** alternativet är markerat i **[!UICONTROL Form Containers]** dialogrutan Konfigurera och Adaptiv Forms med Core Components används. Klientbiblioteken måste inkluderas på sidan för motsvarande webbplats.

![När formuläret täcker hela sidbredden är markerat och adaptiva formulär med kärnkomponenter används](/help/forms/assets/overlaycorecomponent.gif)


Lägg till **CustomerHeaderlibs** och **CustomFoterlibs** klientbibliotek till din AEM Sites-sida via distributionsflödet. Så här lägger du till klientbiblioteken:

1. Få åtkomst till och klona dina [AEM Cloud Service Git-databas](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/repositories.html).
1. Öppna AEM Cloud Service Git-databasmappen i en textredigerare för en plan. Exempel: Microsoft® Visual Code.
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

+++ Aktivera **[!UICONTROL Adaptive Forms – Embed(v2)]** för din AEM Sites-sida eller Experience Fragment

Aktivera **[!UICONTROL Adaptive Forms – Embed(v2)]** utför följande steg i mallens policy:

1. Öppna AEM Sites eller Experience Fragment för redigering. Om du vill öppna sidan för redigering markerar du sidan och klickar på **[!UICONTROL Edit]**.
1. Öppna mallen för webbplatserna eller sidan för Experience Fragment. Öppna mallen genom att gå till **[!UICONTROL Page Information]** ![Sidinformation](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL Edit Template]**. Motsvarande mall öppnas i mallredigeraren.
1. I strukturvyn klickar du på **[!UICONTROL Policy]** ![Policy](/help/forms/assets/Smock_FeedManagement_18_N.svg) -ikonen på menyraden. I **[!UICONTROL Allowed Components]** och välj **[!UICONTROL Adaptive Forms – Embed(v2)]**  kryssrutan under **[AEM Archetype Project Name] - Adaptiv form**.
1. Klicka på **[!UICONTROL Done]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419369?quality=12&learn=on)

+++

## Bädda in ett adaptivt formulär med komponenten Adaptiv Forms - Embed(v2) {#embed-an-adaptive-form-in-sites-editor-or-experience-fragment}

Använd **[!UICONTROL Adaptive Forms - Embed(v2)]** för att skapa ett adaptivt formulär direkt i AEM Sites-redigeraren med hjälp av guiden Skapa formulär. Det resulterande formuläret sparas som en extern enhet, vilket gör att det kan återanvändas på andra webbplatssidor och fristående formulär. Du kan bädda in ett helt nytt formulär från grunden och anpassa det specifikt efter dina krav och designönskemål, direkt på en AEM Sites-sida eller i Experience Fragment. För enstaka formulär rekommenderas direktredigering på en AEM Sites-sida, medan Experience Fragments är idealiskt för formulär som måste återanvändas på flera sidor på webbplatsen.

Du kan enkelt bädda in ett nytt formulär med **[!UICONTROL Adaptive Forms - Embed(v2)]**.  Tänk dig till exempel att infoga ett nytt kontaktformulär på en AEM Sites-sida eller AEM Experience Fragment. Alla uppdateringar eller ändringar som görs i kontaktformuläret på AEM Sites-sidan eller i Experience Fragment gäller automatiskt alla sidor där det distribueras. Detta förenklar hanteringen av webbplatsens formulär, vilket ger en smidig användarupplevelse och effektiviserar hela processen.

Använda **[!UICONTROL Adaptive Forms - Embed(v2)]** kan du:

* [Bädda in ett nytt formulär med Adaptive Forms Wizard på AEM Sites Page](#embed-form-using-adaptive-form-wizzard-aem-sites)
* [Bädda in ett nytt formulär med hjälp av guiden Adaptiv Forms i ett Experience Fragment](#embed-form-using-adaptive-form-wizzard-experience-fragment)
* [Bädda in ett befintligt adaptivt formulär på en AEM Sites-sida](#embed-an-adaptive-form-in-sites-editor)
* [Bädda in ett befintligt formulär i ett Experience Fragment](#embed-an-adaptive-form-in-experience-fragment)
* [Konvertera ett anpassat formulär på en AEM Sites-sida till ett Experience Fragment](#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment)

### Bädda in ett nytt formulär med Adaptive Forms Wizard på AEM Sites Page {#embed-form-using-adaptive-form-wizzard-aem-sites}

Steg för att bädda in nya formulär på en AEM Sites-sida är:

1. Öppna AEM Sites-sidan i redigeringsläge.
1. Dra och släpp komponentens **[!UICONTROL Adaptive Forms - Embed(v2)]** på sidan.
1. Klicka på **Plus** och du omdirigeras till guiden för att skapa formulär.

   ![Adaptiv Forms - Bädda in komponent](/help/forms/assets/aemformcontainer.png)

1. Skapa ett nytt adaptivt formulär från **[!UICONTROL Form Creation]** guide.
The **[!UICONTROL Asset Path]** innehåller redan sökvägen till ett skapat adaptivt formulär
1. Spara inställningarna. Det adaptiva formuläret är nu inbäddat på sidan.

>[!VIDEO](https://video.tv.adobe.com/v/3419366/adaptive-form-aem-forms?quality=12&learn=on)

Nu kan du [ange åtgärden Skicka](/help/forms/configuring-submit-actions.md) och avancerade egenskaper för inbäddade adaptiva formulär med hjälp av guiden Skapa formulär.


### Bädda in ett nytt formulär med hjälp av guiden Adaptiv Forms i ett Experience Fragment {#embed-form-using-adaptive-form-wizzard-experience-fragment}

Steg för att bädda in nya formulär i en Experience Fragment är:

1. Öppna Experience Fragment i redigeringsläge.
1. Dra och släpp komponentens **[!UICONTROL Adaptive Forms - Embed(v2)]** på sidan.
1. Klicka på **Plus** och du omdirigeras till guiden för att skapa formulär.

   ![Adaptiv Forms - Bädda in komponent](/help/forms/assets/aemformcontainer.png)

1. Skapa ett nytt adaptivt formulär från **[!UICONTROL Form Creation]** guide.
The **[!UICONTROL Asset Path]** innehåller redan sökvägen till ett skapat adaptivt formulär
1. Spara inställningarna. Det adaptiva formuläret är nu inbäddat i Experience Fragment.

Nu kan du [ange åtgärden Skicka](/help/forms/configuring-submit-actions.md) och avancerade egenskaper för inbäddade adaptiva formulär med hjälp av guiden Skapa formulär.

### Bädda in ett befintligt adaptivt formulär på en AEM Sites-sida {#embed-an-adaptive-form-in-sites-editor}

Med **[!UICONTROL Adaptive Forms - Embed(v2)]** kan du enkelt integrera ett befintligt adaptivt formulär på en sida i AEM Sites. Den här funktionen gör det enklare att anpassa och återanvända Adaptive Forms, vilket ger kunderna ett bekvämt sätt att återanvända redan skapade formulär. Tänk dig att du kan lägga in ett kontaktformulär på en AEM Sites-sida och slippa återskapa formuläret flera gånger.

Så här bäddar du in ett befintligt adaptivt formulär på en webbplatssida:

1. Öppna AEM Sites-sidan i redigeringsläge.
1. Dra och släpp **[!UICONTROL Adaptive Forms - Embed(v2)]** -komponenten från komponentwebbläsaren till sidan Platser.
1. Tryck på **[!UICONTROL Adaptive Forms - Embed]** på sidan Platser och tryck på ![Egenskaper för adaptiv formulärbehållare](/help/forms/assets/configure-icon.svg) i åtgärdsfältet. The **[!UICONTROL Edit Adaptive Forms - Embed(v2)]** öppnas.
1. Bläddra och välj det adaptiva formulär som ska bäddas in i **[!UICONTROL Asset Path]**.
1. Spara inställningarna. Det adaptiva formuläret är nu inbäddat på sidan.

>[!VIDEO](https://video.tv.adobe.com/v/3419368?quality=12&learn=on)

Nu kan du [ange åtgärden Skicka](/help/forms/configuring-submit-actions.md) och avancerade egenskaper för inbäddade adaptiva formulär med hjälp av guiden Skapa formulär.

### Bädda in ett befintligt anpassat formulär i ett Experience Fragment {#embed-an-adaptive-form-in-experience-fragment}

Du kan också utöka formulärens tillgänglighet genom att bädda in dem i AEM Experience Fragment. Så här bäddar du in ett anpassat formulär i ett Experience Fragment:

1. Öppna ett Experience Fragment i redigeringsläge.
1. Dra och släpp **[!UICONTROL Adaptive Forms - Embed(v2)]** -komponenten från komponentwebbläsaren till Experience Fragment.
1. Tryck på **[!UICONTROL Adaptive Forms - Embed]** i Experience Fragment och tryck på ![Egenskaper för adaptiv formulärbehållare](/help/forms/assets/configure-icon.svg) i åtgärdsfältet. The **[!UICONTROL Edit Adaptive Forms - Embed(v2)]** öppnas.
1. Bläddra och välj det adaptiva formulär som ska bäddas in i **[!UICONTROL Asset Path]**.
1. Spara inställningarna. Det anpassade formuläret är nu inbäddat i Experience Fragment.

Nu kan du [ange åtgärden Skicka](/help/forms/configuring-submit-actions.md) och avancerade egenskaper för inbäddade adaptiva formulär med hjälp av guiden Skapa formulär.

### Konvertera ett formulär på en AEM Sites-sida till ett Experience Fragment {#convert-an-adaptive-form-in-sites-page-to-an-experience-fragment}

Du kan konvertera ett befintligt adaptivt formulär i en webbplatssidredigerare till ett Experience Fragment för att återanvända formuläret på flera sidor eller webbplatser.

Så här konverterar du ett adaptivt formulär på en AEM Sites-sida till ett Experience Fragment:

1. Öppna AEM Sites-sidan som innehåller det adaptiva formuläret (i adaptiva Forms Container-komponenten) i redigeringsläge.
1. Öppna innehållsträdet och välj **[!UICONTROL Adaptive Forms Container]** som är värd för din adaptiva form. En AEM Sites-sida kan vara värd för flera adaptiva Forms. Välj rätt adaptiva Forms-behållare.
1. På menyraden väljer du ![Ikon för att konvertera till upplevelsefragmentvariationer](/help/forms/assets/Smock_FilingCabinet_18_N.svg) Konvertera till Experience Fragment-variationsikon.

   ![Klicka på filkabinettlogotypen för att konvertera ett adaptivt formulär på AEM Sites-sidan till ett Experience Fragment](/help/forms/assets/convert-form-in-sites-page-to-an-experience-fragment.png)

   En dialogruta visas där du kan konvertera behållaren för adaptiva formulär till ett nytt Experience Fragment eller lägga till i ett befintligt Experience Fragment.

1. På **[!UICONTROL Convert to Experience Fragment]** i variantdialogrutan anger du värden för följande alternativ:

   * **Åtgärd:** Välj det här alternativet om du vill skapa ett Experience Fragment eller Lägg till i ett befintligt Experience Fragment.
   * **Överordnad sökväg:** Ange sökvägen till den mapp där Experience Fragment ska vara värd. Alternativet är bara tillgängligt för att skapa nya Experience Fragment.
   * **Mall:** Ange sökvägen till Experience Fragment-mallen. Om du inte har någon Experience Fragment-mall [skapa](/help/implementing/developing/extending/experience-fragments.md). Alternativet är bara tillgängligt för att lägga till adaptiv form till ett befintligt Experience Fragment.
   * **Fragmenttitel:** Ange Experience Fragment-titel. Titeln identifierar unikt en Experience Fragment.
   * **Fragment-taggar:** Ange tagg för Experience Fragment. Taggen identifierar unikt kategorin för en Experience Fragment.

## Konfigurera egenskaper för anpassad formulärinbäddning (v2)

Du kan anpassa de avancerade inställningarna för **[!UICONTROL Adaptive Form - Embed(v2)]** -komponenten. I **[!UICONTROL Edit Adaptive Forms - Embed]** kan du ange följande:

* **Resurssökväg**: Bläddra och välj ett anpassat formulär som ska bäddas in. Den fylls i automatiskt om du släppte den från Assets-webbläsaren.
* **Efterbeställning** : Välj den åtgärd som ska utlösas när formulär skickas. Du kan visa ett tackmeddelande eller en tacksida.
   * **Visa tackmeddelande**: Skriv ett meddelande med textredigeraren som ska visas när formulär skickas. Det här alternativet är endast tillgängligt när du väljer att visa ett tackmeddelande.
   * **Visa tacksida**: Bläddra och välj den sida som ska visas när formuläret skickas. Det här alternativet är bara tillgängligt när du väljer att visa en tacksida.
   * **Omdirigering till dig som tackar dig**: Aktivera alternativet att ersätta sidan som innehåller det inbäddade adaptiva formuläret med tacksidan. I annat fall ersätter tack-sidan det adaptiva formuläret i dialogrutan **[!UICONTROL Adaptive Forms - Embed(v2)]** utan att uppdatera underliggande webbplatser på sidan. Det här alternativet är bara tillgängligt när du väljer att visa en tacksida.
   * **Thankyou Message**: Kortfattad bekräftelse eller bekräftelse som visas på skärmen när ett formulär har skickats.
   * **Thankyou Page**: Bläddra och markera den sida som ska visas när formuläret har skickats.

* **Använd sidspråk**: Använd lokala sidor på AEM Sites-sidan i stället för anpassade formulär. Det här alternativet gäller endast för Adaptiv form (Foundation).
* **Sätt fokus på formulär**: Välj det här alternativet om du vill fokusera på det första fältet i det adaptiva formuläret. Det här alternativet gäller endast för Adaptiv form (Foundation).
* **Tema**: Välj ett tema som definierar formatering för komponenter i det adaptiva formuläret. Formateringen innehåller utseendeegenskaper som teckensnittsstil, bakgrundsfärg, dimensioner och justering. Det här alternativet gäller endast för Adaptiv form (Foundation).

  >[!NOTE]
  >
  > Du kan använda **Använd sidspråk**, **Sätt fokus på formulär** och **Tema** endast för Adaptiv form (Foundation).

* **Formuläret täcker ramens hela bredd**: En textbunden bildruta (iframe) är ett HTML-element som läser in ett adaptivt formulär på en AEM Sites-sida.

   * Om **[!UICONTROL Form covers entire width of the frame]** om kryssrutan är markerad upptar ett adaptivt formulär hela bredden på den behållare som det är placerat i. I det här fallet används ingen iframe för att återge formuläret. Layouten och designen för ett adaptivt formulär anpassas efter behållarens hela bredd så att den blir responsiv och kan justeras till olika skärmstorlekar. Med det här alternativet kan du bädda in flera adaptiva Forms-filer på en AEM Sites-sida.

     >[!NOTE]
     >
     > Om du vill bädda in flera formulär på en AEM Sites-sida väljer du **[!UICONTROL Form covers entire width of the frame]** kryssrutan.

   * Om **[!UICONTROL Form covers entire width of the frame]** inte är markerad, ett anpassat formulär täcker inte hela behållarens bredd. I stället används en iframe för att återge formuläret, som inte kan utökas utanför en viss bredd. Detta är användbart när ett adaptivt formulär har definierade gränser och behöver finnas tillsammans med andra AEM komponenter bredvid det i behållaren. Om det här alternativet inte är markerat tillåter det endast att en Adaptiv Forms-sida på AEM Sites-sidan bäddas in utan iframe.

     >[!NOTE]
     >
     > AEM Sites-sidan stöder endast ett adaptivt formulär utan iframe. Lägga till mer adaptiv Forms med **[!UICONTROL Adaptive Forms - Embed]** komponent, markera **[!UICONTROL Form covers entire width of the frame]** alternativ.

* **Höjd**: Ange behållarens höjd. Lämna det tomt om du vill ändra storlek på behållaren automatiskt.
* **CSS-klientbibliotek**: Ange sökväg till ett CSS-klientbibliotek.

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

1. To create and embed a new form, on the component toolbar, tap the **Create Form** icon. A window to create the form opens. 

1. Tap the embedded Adaptive Forms - Embed component in the sites page, and then tap ![settings_icon](assets/settings_icon.png) on the action bar. The **[!UICONTROL Edit Adaptive Forms - Embed]** dialog opens.
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

## Publicera inbäddat adaptivt formulär {#publishing-embedded-adaptive-form}

Vi ska titta på följande scenarier för publicering av ett inbäddat adaptivt formulär på AEM webbplatssida:

* Om du publicerar sidan AEM webbplatser för första gången och den innehåller ett inbäddat adaptivt formulär publicerar du webbplatssidan och den inbäddade resursen.
* Om du bara ändrade det inbäddade adaptiva formuläret på en publicerad webbplatssida publicerar du den ursprungliga resursen och ändringarna återspeglas på den publicerade webbplatssidan. Den publicerade webbplatssidan innehåller en referens till resursen och behöver inte publicera om sidan.
* Om du har ändrat webbplatssidan och det inbäddade adaptiva formuläret publicerar du om webbplatssidan och den inbäddade resursen.

## Ändra inbäddat anpassat formulär  {#modifying-embedded-adaptive-form}

Om du vill ändra någon konfiguration eller egenskap för det inbäddade adaptiva formuläret gör du något av följande.

* Öppna originalformuläret i ett adaptivt formulär i respektive redigerare och ändra dem.
* Tryck på det adaptiva formuläret på webbplatssidan i redigeringsläge och tryck sedan på **[!UICONTROL Edit in a new window]**. Det ursprungliga formuläret öppnas i redigeringsläge som du kan ändra.

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
