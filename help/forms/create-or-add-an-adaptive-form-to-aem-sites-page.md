---
title: Skapa eller lägga till ett anpassat formulär på AEM Sites-sidan
description: Upptäck hur du enkelt kan skapa och lägga till anpassade formulär på din AEM Sites-sida. Lär dig stegvisa tekniker och metodtips för att integrera dynamiska och anpassningsbara formulär på er webbplats och optimera era era digitala upplevelser för maximal effekt.
feature: Adaptive Forms
hide: true
hidefromtoc: true
source-git-commit: 7dc36220c1f12177037aaa79d864c1ec2209a301
workflow-type: tm+mt
source-wordcount: '1210'
ht-degree: 0%

---


# Skapa eller lägga till ett anpassat formulär på AEM Sites-sidan {#create-or-add-an-adaptive-form-to-aem-sites-page}

Med AEM Forms kan du smidigt lägga in anpassningsbara formulär på webbsidorna. På så sätt kan besökarna enkelt fylla i och skicka in formulär utan att lämna den sida de är på. På så sätt kan de enkelt hålla kontakten med andra element på webbplatsen samtidigt som de interagerar aktivt med formuläret.

Du kan utnyttja den här funktionen till fullo genom att använda följande alternativ:

* **Lägg till ett anpassat formulär:** Skapa ett helt nytt formulär från grunden och skräddarsy det specifikt efter dina behov och designönskemål.

* **Förbättra upplevelsefragment:** Nå ut bättre med formulären genom att lägga till dem i AEM Experience Fragments, vilket möjliggör smidig återanvändning på flera sidor eller webbplatser.

* **Använd godkända mallar:** Använd redan godkända mallar för att snabbt skapa blanketter som är anpassade efter företagets grafiska profil och designstandarder.

* **Lägg till befintliga formulär:** Integrera enkelt formulär som du redan har skapat på webbplatserna så att besökarna kan interagera direkt med dem.

* **Lägg till flera formulär:**  Lägg till flera formulär på en sida för att ge användarna flera alternativ baserat på deras önskemål och önskemål. Dessa kan vara en kombination av helt nya formulär från grunden och befintliga formulär.

Du kan använda AEM Sites Editor för att snabbt skapa och lägga till flera formulär på dina AEM Sites-sidor. Med AEM Sites editor kan man skapa sömlösa datainhämtningsmöjligheter på en Sites-sida med hjälp av adaptiva formulärkomponenter som dynamiskt beteende, validering, dataintegrering, generering av dokument för registrering och automatisering av affärsprocesser. Det gör det även möjligt att använda olika funktioner på AEM Sites-sidor, som versionshantering, målgruppsanpassning, översättning och hantering av flera webbplatser.

## Syfte

* Lär dig skapa ett adaptivt formulär med AEM Sites editor och Experience Fragment
* Lär dig att ställa in layout och tema för ett adaptivt formulär som lagts till på en AEM Sites-sida och
* Skapa ett adaptivt formulär med AEM Sites editor och Experience Fragment


## Överväganden {#consideration}

AEM Forms har adaptiv formulärbehållare och adaptiv Forms - inbäddningskomponenter. Du kan använda adaptiv formulärbehållare för att skapa och lägga till ett nytt formulär på en Experience Fragment- eller AEM Sites-sida, medan adaptiv Forms - Embed-komponent gör att du kan lägga till ett befintligt adaptivt formulär eller skapa ett nytt formulär med Adaptiv Forms-redigerare.

När du använder den adaptiva formulärbehållaren för att skapa eller lägga till ett formulär, översätts och lokaliseras formulären via AEM Sites översättningsflöde. För varje språk genereras en separat kopia (språkkopia) av webbplatssidan och motsvarande formulär. När en innehållsförfattare ändrar en regel i ett formulär på den överordnade sidan måste samma ändringar göras i alla språkkopior av formuläret. Med adaptiv formulärbehållare kan du även använda olika funktioner på AEM Sites-sidor, som versionshantering, målgruppsanpassning, översättning och hantering av flera webbplatser.

När du skapar eller lägger till ett formulär med komponenten Adaptiv formulärinbäddning översätts och lokaliseras formulären med hjälp av AEM Forms översättningsflöde. I det här fallet finns det ett enda formulär som du kan referera till på alla språkkopior av webbplatssidorna. Adaptiv Form-embed-komponent ger inte åtkomst till olika funktioner på AEM Sites-sidor som versionshantering, målgruppsanpassning, översättning och hantering av flera webbplatser.


## Innan du börjar {#before-you-start}

+++  Aktivera adaptiva Forms Core-komponenter för din miljö

Se till att [Adaptiva Forms Core-komponenter är aktiverade för din as a Cloud Service AEM Forms-miljö](enable-adaptive-forms-core-components.md).

+++

+++ Aktivera **[!UICONTROL Adaptive Forms Container]

Aktivera [!UICONTROL Adaptive Forms Container] utför följande steg i mallens policy:

1. Öppna AEM Sites-sidan för redigering. Om du vill öppna sidan för redigering markerar du sidan och klickar på Redigera.
1. Öppna mallen för din Sites-sida. Öppna mallen genom att gå till [!UICONTROL Page Information] ![Sidinformation](/help/forms/assets/Smock_Properties_18_N.svg) > [!UICONTROL Edit Template]. Motsvarande mall öppnas i mallredigeraren.
1. I strukturvyn klickar du på **[!UICONTROL Policy]** ![Policy](/help/forms/assets/Smock_FeedManagement_18_N.svg) -ikonen på menyraden. I **[!UICONTROL Allowed Components]** och välj **[!UICONTROL Adaptive Forms Container]**  kryssrutan under **[AEM Archetype Project Name] - Adaptiv form**.
1. Klicka på **[!UICONTROL Done]**.

>[!VIDEO](https://video.tv.adobe.com/v/3419370?quality=12&learn=on)

+++


+++  Lägg till adaptiva Forms Client Libraries på din AEM Sites-sida

Om du vill aktivera alla funktioner för den adaptiva Forms-behållarkomponenten lägger du till klientbiblioteken CustomHeaderlibs och CustomFoterlibs på din AEM Sites-sida via distributionsflödet. Så här lägger du till biblioteken:

1. Få åtkomst till och klona dina [AEM Cloud Service Git-databas](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/content/managing-code/repositories.html).
1. Öppna AEM Cloud Service Git-databasmappen i en textredigerare för en plan. Exempel: Microsoft Visual Code.
1. Öppna `ui.apps/src/main/content/jcr_root/apps/[your-project]/components/page/.content.xml` fil för redigering och notera värdet för `sling:resourceSuperType`. Anteckna till exempel värdet nedåt `core/wcm/components/page/v3/page`.


   ![försäljningsresurs](/help/forms/assets/slingresource.png)

1. Navigera till `  ui.apps\src\main\content\jcr_root\apps\[your-project]\components\page\` `ui.apps/src/main/content/jcr_root/apps` och skapa en mappstruktur som är identisk med det värde som noterades i föregående steg. Om värdet till exempel liknar det i föregående steg är den sista nodstrukturen `ui.apps/src/main/content/jcr_root/apps/core/wcm/components/page/v3/page`

   ![övertäckningsstruktur](/help/forms/assets/overlaystructure.png)

1. Skapa `customheaderlibs.html` och `customfooterlibs.html` filer i nodstrukturen som skapades i föregående steg och lägg till följande innehåll i filerna:

   ```
        //Customheaderlibs.html
        <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
        <sly data-sly-call="${clientlib.css @ categories='core.forms.components.runtime.all'}"/>
        </sly> 
   
        //customfooterlibs.html
        <sly data-sly-use.clientlib="core/wcm/components/commons/v1/templates/clientlib.html">
        <sly data-sly-test="${!wcmmode.edit}" data-sly-call="${clientlib.js @ categories='core.forms.components.runtime.all', async=true}"/>
        </sly> 
   ```

1. [Kör distributionsflödet](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/sites/administering/site-creation/enable-front-end-pipeline.html) för att distribuera klientbiblioteken till din AEM as a Cloud Service miljö.

+++

## Skapa ett adaptivt formulär {#create-an-adaptive-form-in-sites-editor-or-experience-fragment}

Du kan skapa ett helt nytt formulär från grunden och anpassa det specifikt efter dina krav och designönskemål, direkt på en AEM webbplatssida eller i Experience Fragment. För enstaka formulär rekommenderas direktredigering till en AEM webbplats, medan Experience Fragments är idealiskt för formulär som behöver återanvändas på flera sidor på webbplatsen.

* [Skapa ett formulär på en AEM Sites-sida](#create-an-adaptive-form-in-sites-editor)
* [Skapa ett formulär i ett Experience Fragment](#create-an-adaptive-form-in-experience-fragment)

### Skapa ett formulär på en AEM Sites-sida {#create-an-adaptive-form-in-sites-editor}

Du kan använda komponenten Adaptiv formulärbehållare i AEM Sites Editor för att skapa ett anpassat formulär. Med komponenten kan du skapa ett formulär genom att dra och släppa formulärkomponenterna. Formulärkomponenterna är baserade på kärnkomponenter. Du kan enkelt anpassa dessa efter organisationens behov.

>[!VIDEO](https://video.tv.adobe.com/v/3419284?quality=12&learn=on)

Så här skapar du ett adaptivt formulär på en webbplatssida:

1. Öppna AEM Sites-sidan i redigeringsläge.
1. Dra och släpp **[!UICONTROL Adaptive Forms Container]** från komponentwebbläsaren till sidan Platser. Det skapar ett blanksteg på sidan för formuläret. Du kan använda layoutläget för att ändra storleken på behållarutrymmet.
1. Dra och släpp adaptiva kärnkomponenter i formulär till behållarutrymmet för att skapa formuläret.
1. Lägg till knappen Skicka.

Sedan ställer du in åtgärden Skicka och avancerade egenskaper.

### Skapa ett formulär i ett Experience Fragment {#create-an-adaptive-form-in-experience-fragment}

Ni kan utöka räckvidden för era formulär genom att lägga till dem i AEM Experience Fragments, vilket möjliggör smidig återanvändning på flera sidor eller webbplatser. Du kan till exempel inkludera ett formulär för anmälan av nyhetsbrev i ett Experience Fragment. På så sätt kan du enkelt återanvända fragmentet på flera sidor på webbplatsen, vilket eliminerar behovet av att återskapa formuläret upprepade gånger. Alla uppdateringar eller ändringar som görs i formuläret för anmälan av nyhetsbrev i Experience Fragment sprids automatiskt till alla sidor där det används. Detta effektiviserar processen och ger en smidig användarupplevelse samtidigt som det förenklar hanteringen av webbplatsens formulär.

Så här skapar du ett anpassat formulär i ett Experience Fragment:

## Ändra layout för ett anpassat formulär {#change-layout-of-an-adaptive-form}

På AEM Sites-sidan använder du [Layoutläge](/help/sites-cloud/authoring/features/responsive-layout.md) om du vill ändra storlek på en komponent för adaptiv formulärbehållare som lagts till på en AEM Sites-sida.
