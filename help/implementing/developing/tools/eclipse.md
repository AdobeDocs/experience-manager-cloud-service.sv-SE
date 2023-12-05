---
title: AEM Developer Tools for Eclipse
description: Lär dig hur du använder AEM Developer Tools för Eclipse, ett Eclipse-plugin-program baserat på Eclipse-pluginprogrammet för Apache Sling.
exl-id: 7f9c0f99-e230-440a-8bc9-a0ab7465e3bf
source-git-commit: 2d4ffd5518d671a55e45a1ab6f1fc41ac021fd80
workflow-type: tm+mt
source-wordcount: '1138'
ht-degree: 0%

---

# AEM Developer Tools for Eclipse{#aem-developer-tools-for-eclipse}

![Experience Manager Developer Tools for Eclipse logo](assets/eclipse-logo.png)

## Ökning {#overview}

_Experience Manager Developer Tools for Eclipse_ är ett Eclipse-plugin-program baserat på [Eclipse-plugin för Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html) som släpps under Apache License 2.

Den har flera funktioner som gör AEM enklare:

* Smidig integrering med AEM instanser via Eclipse Server Connector
* Synkronisering för både innehåll och OSGi-paket
* Felsökningsstöd med möjlighet att byta kod under drift
* Enkelt Bootstrap i AEM projekt med hjälp av en särskild projektguide
* Enkel redigering av JCR-egenskaper

## Krav {#requirements}

Innan du använder AEM Developer Tools måste du:

* Hämta och installera [Eclipse IDE for Enterprise Java™ Developers](https://www.eclipse.org/downloads/packages/).
* Konfigurera förmörkelseinstallationen för att säkerställa att du har minst 1 GB stackminne genom att redigera `eclipse.ini` konfigurationsfilen enligt beskrivningen i [Vanliga frågor om Eclipse](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse).

>[!NOTE]
>
>På macOS högerklickar du **Eclipse.app** och sedan markera **Visa paketinnehåll** för att hitta `eclipse.ini`**.**

## Installera AEM Developer Tools for Eclipse {#how-to-install-the-aem-developer-tools-for-eclipse}

När du har uppfyllt [krav](#requirements) ovan kan du installera plugin-programmet på följande sätt:

1. Öppna [AEM för utvecklingsverktyg](https://eclipse.adobe.com/com.adobe.granite.ide.p2update-1.3.0.zip). <!-- RB: OLD URL was (https://eclipse.adobe.com/aem/dev-tools/) This URL is generating a 404 error in the experience-manager-cloud-service.en LinkCheckExl report . The website appears to be dead; no redirects at all. Clicking "Installation Link" does not do anything. Only the link "Download archive" works. The "Online Documentation" link just takes you to the AEM Docs home page. Not sure if this topic is still needed?? -->

1. Kopiera **Installationslänk**.

   Du kan även hämta ett arkiv i stället för att använda installationslänken. Den här metoden tillåter offlineinstallation, men du får inga meddelanden om automatiska uppdateringar på det här sättet.

1. Öppna **Hjälp** -menyn.
1. Klicka **Installera ny programvara**.
1. Klicka **Lägg till...**.
1. I **Namn** fält, ange `AEM Developer Tools`.
1. I **Plats** kopierar du installations-URL:en.
1. Klicka **Lägg till**.
1. Markera båda **AEM** och **Sling** plugins.
1. Klicka på **Nästa**.
1. I **Installationsinformation** fönster, klicka **Nästa** igen.
1. Godkänn licensavtalen och klicka på **Slutför**.
1. Klicka **Starta omNow** för att starta om Eclipse.

## AEM {#the-aem-perspective}

I Eclipse avgör ett perspektiv vilka åtgärder och vyer som finns tillgängliga i ett fönster och aktiverar uppgiftsorienterad interaktion med resurser i Eclipse. Mer information om Perspektiv finns i [Eclipse-dokumentation.](https://help.eclipse.org/latest/index.jsp)

_Experience Manager Development Tools for Eclipse_ har ett AEM perspektiv som ger dig full kontroll över dina AEM projekt och instanser. Så här öppnar du AEM perspektiv:

1. Välj **Fönster** > **Perspektiv** > **Öppna perspektiv** > **Övriga**.
1. Välj **AEM** i dialogrutan och klicka på **Öppna**.

![AEM i Eclipse](assets/eclipse-aem-perspective.png)

## Exempel på flermodulsprojekt {#sample-multi-module-project}

The _Experience Manager Developer Tools for Eclipse_ innehåller ett exempel på ett projekt med flera moduler som hjälper dig att snabbt komma igång med en projektkonfiguration i Eclipse. Det är också en praktisk guide till flera AEM funktioner. [Läs mer om Project Archetype](https://github.com/adobe/aem-project-archetype).

Så här skapar du exempelprojektet:

1. I **Fil** > **Nytt** > **Projekt** -menyn, bläddra till **AEM** avsnitt och markera **Exempel på AEM-projekt med flera moduler**.

   ![Exempel på AEM-projekt med flera moduler](assets/aem-sample-project.png)

1. Klicka på **Nästa**.

   >[!NOTE]
   >
   >Det här steget kan ta en stund eftersom m2eclipse måste skanna arkivtypskatalogerna.

1. Välj `com.adobe.granite.archetypes : sample-project-archetype : <highest-number>` från menyn och sedan klicka på **Nästa**.

   ![Välj arkivtypsversion](assets/select-archetype.png)

1. Ange följande fält för exempelprojektet:

   * **Namn**
   * **Grupp-ID**
   * **Artefakt-ID**
   * **appId** - Du kan behöva utöka **Avancerat** alternativ för att ange det här värdet.
   * **appTitle** - Du kan behöva utöka **Avancerat** alternativ för att ange det här värdet.
   * **Paket** - Du kan behöva utöka **Avancerat** alternativ för att ange det här värdet.

   ![Definiera egenskaper för arkityp](assets/archetype-properties.png)

1. Klicka på **Nästa**.

1. Sedan konfigurerar du en AEM som Eclipse ska ansluta till.

   Om du vill använda felsökningsfunktionen måste du ha startat AEM i felsökningsläge, vilket du kan göra genom att lägga till följande på kommandoraden:

   ```text
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![Anslut till AEM server](assets/connect-server.png)

1. Klicka **Slutför**. Projektstrukturen skapas.

   >[!NOTE]
   >
   >Vid en ny installation (närmare bestämt när större beroenden aldrig har laddats ned) kan du få projektet skapat med fel. I så fall följer du det förfarande som beskrivs i [Löser ogiltig projektdefinition](#resolving-invalid-project-definition).

## Importera befintliga projekt {#how-to-import-existing-projects}

Du kan använda **Nytt projekt** för att skapa rätt struktur för dig:

1. Följ instruktionerna för att skapa en [Exempel på flermodulsprojekt](#sample-multi-module-project) och du har skapat följande projekt åt dig, som gör det möjligt att frilägga problemen på ett bra sätt:

   * `PROJECT.ui.apps` for `/apps` och `/etc` innehåll
   * `PROJECT.ui.content` for `/content` som är skapad
   * `PROJECT.core` för Java™-paket (dessa blir intressanta när du vill lägga till Java™-kod)
   * `PROJECT.it.launcher` och `PROJECT.it.tests` för integreringstester

1. Ersätta innehållet i `PROJECT.ui.apps` projektet med `apps` och `etc` mappar i ditt paket:

   1. I projektutforskarpanelen, visa `PROJECT.ui.apps` > `src` > `main` > `content` > `jcr_root` > `apps`.
   1. Högerklicka på `apps` mapp och välj **Visa i** > **Systemutforskaren**.
   1. Ta bort `apps` och `etc` mappar som du nu ska visa och placera här `apps` och `etc` mappar med ditt innehållspaket.
   1. Högerklicka på `PROJECT.ui.apps` projekt och välj **Uppdatera**.

1. Gör sedan samma sak med `PROJECT.ui.content` och ersätta innehållsmappen med ett av dina paket:

   1. I projektutforskarpanelen, visa `PROJECT.ui.content` > `src` > `main` > `content` > `jcr_root` > `content`.
   1. Högerklicka på den djupare innehållsmappen och välj **Visa i** > **Systemutforskaren**.
   1. Ta bort innehållsmappen som du nu ska se och placera innehållsmappen i innehållspaketet här.
   1. Högerklicka på `PROJECT.ui.content` projekt och välj **Uppdatera**.

1. Nu måste du uppdatera `filter.xml` filer i dessa två projekt så att de motsvarar innehållet i ditt innehållspaket. Öppna `META-INF/vault/filter.xml` en fil med ditt innehållspaket i en separat text-/kodredigerare.

   * Detta är ett exempel på hur `filter.xml` filen kan se ut:

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <workspaceFilter version="1.0">
       <filter root="/apps/foo"/>
       <filter root="/apps/foundation/components/bar"/>
       <filter root="/etc/designs/foo"/>
       <filter root="/content/foo"/>
       <filter root="/content/dam/foo"/>
       <filter root="/content/usergenerated/content/foo"/>
   </workspaceFilter>
   ```

1. När det gäller innehållet i ditt paket som delats upp i två projekt måste du också dela upp dessa filterregler i två och uppdatera i enlighet med det `filter.xml` filer från de två projekten.

   1. Öppna i Eclipse `PROJECT.ui.apps/src/main/content/META-INF/filter.xml`.
   1. Ersätta innehållet i `<workspaceFilter>` -element med reglerna i paketet som börjar med `/apps` och `/etc`
      * Till exempel:

        ```xml
        <?xml version="1.0" encoding="UTF-8"?>
        <workspaceFilter version="1.0">
           <filter root="/apps/foo"/>
           <filter root="/apps/foundation/components/bar"/>
           <filter root="/etc/designs/foo"/>
        </workspaceFilter>
        ```

   1. Öppna `PROJECT.ui.content/src/main/content/META-INF/filter.xml`.
   1. Ersätt reglerna med reglerna i ditt paket som börjar med `/content`.
      * Till exempel:

        ```xml
        <?xml version="1.0" encoding="UTF-8"?>
        <workspaceFilter version="1.0">
           <filter root="/content/foo"/>
           <filter root="/content/dam/foo"/>
           <filter root="/content/usergenerated/content/foo"/>
        </workspaceFilter>
        ```

1. Spara alla ändringar. Nu kan du synkronisera det nya innehållet med din AEM.

1. Kontrollera att anslutningen har startats på serverpanelen och starta den om den inte redan har startats.
1. Klicka på **Rensa och publicera** -ikon.

När du är klar bör du låta paketet köras på din instans, och när du sparar synkroniseras alla ändringar automatiskt till instansen.

Om du vill återskapa ett paket från projektet högerklickar du på `PROJECT.ui.apps` eller `PROJECT.ui.content` och välja **Kör som** > **Maven Install**.

Nu har du en målmapp som skapats med ditt paket inuti (anropas till exempel `PROJECT.ui.apps-0.0.1-SNAPSHOT.zip`).

## Felsökning {#troubleshooting}

### Löser ogiltig projektdefinition {#resolving-invalid-project-definition}

Så här löser du ogiltiga beroenden och projektdefinitioner:

1. Markera alla skapade projekt.
1. Högerklicka.
1. Välj **Maven** > **Uppdatera projekt**.
1. Kontrollera **Tvinga uppdateringar av ögonblicksbild/releaser**.
1. Klicka **OK**.

Eclipse hämtar nödvändiga beroenden. Det här kan ta en stund.

## Mer information {#more-information}

Den officiella versionen av Apache Sling IDE-verktygen för Eclipse-webbplatsen innehåller användbar information:

* The [**Apache Sling IDE-verktyg för Eclipse** Användarhandbok](https://sling.apache.org/documentation/development/ide-tooling.html)I den här dokumentationen får du hjälp med de övergripande begreppen, serverintegreringen och distributionsfunktionerna som stöds av AEM utvecklingsverktyg.
* The [Felsökningsavsnitt](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting).
* The [Lista över kända fel](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues).

Följande tjänsteman [Eclipse](https://www.eclipse.org/) dokumentation kan hjälpa dig att konfigurera miljön:

* [Komma igång med Eclipse](https://www.eclipse.org/getting-started/)
* [Hjälpsystemet Eclipse Luna](https://help.eclipse.org/latest/index.jsp)
* [Maven Integration (m2eclipse)](https://www.eclipse.org/m2e/)
