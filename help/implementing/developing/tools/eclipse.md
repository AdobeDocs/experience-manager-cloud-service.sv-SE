---
title: AEM Developer Tools for Eclipse
description: Lär dig hur du använder AEM Developer Tools för Eclipse, ett Eclipse-plugin-program som bygger på Eclipse-plugin för Apache Sling.
exl-id: 7f9c0f99-e230-440a-8bc9-a0ab7465e3bf
feature: Developing
role: Admin, Architect, Developer
source-git-commit: ba42d58a4e55efdada35cc7706d736a7314ba743
workflow-type: tm+mt
source-wordcount: '1138'
ht-degree: 0%

---

# AEM Developer Tools for Eclipse{#aem-developer-tools-for-eclipse}

![Experience Manager Developer Tools for Eclipse, logotyp](assets/eclipse-logo.png)

## Ökning {#overview}

_Experience Manager Developer Tools for Eclipse_ är en Eclipse-plugin som baseras på [Eclipse-pluginen för Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html) som släppts under Apache License 2.

Den har flera funktioner som underlättar utvecklingen av AEM:

* Smidig integrering med AEM-instanser via Eclipse Server Connector
* Synkronisering för både innehåll och OSGi-paket
* Felsökningsstöd med möjlighet att byta kod under drift
* Enkel Bootstrap av AEM-projekt genom en särskild projektguide
* Enkel redigering av JCR-egenskaper

## Krav {#requirements}

Innan du använder AEM Developer Tools måste du:

* Hämta och installera [Eclipse IDE for Enterprise Java™ Developers](https://www.eclipse.org/downloads/packages/).
* Konfigurera din förmörkande installation för att säkerställa att du har minst 1 GB stackminne genom att redigera konfigurationsfilen för `eclipse.ini` enligt beskrivningen i [Vanliga frågor om Eclipse.](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse%3F)

>[!NOTE]
>
>I macOS måste du högerklicka på **Eclipse.app** och sedan välja **Visa paketinnehåll** för att hitta din `eclipse.ini`**.**

## Installera AEM Developer Tools for Eclipse {#how-to-install-the-aem-developer-tools-for-eclipse}

När du har uppfyllt [kraven](#requirements) ovan kan du installera plugin-programmet på följande sätt:

1. Öppna webbplatsen [AEM Developer Tools](https://eclipse.adobe.com/).

<!-- had to update the link again - was https://eclipse.adobe.com/com.adobe.granite.ide.p2update-1.3.0.zip -->
<!-- RB: OLD URL was (https://eclipse.adobe.com/aem/dev-tools/) This URL is generating a 404 error in the experience-manager-cloud-service.en LinkCheckExl report . The website appears to be dead; no redirects at all. Clicking "Installation Link" does not do anything. Only the link "Download archive" works. The "Online Documentation" link just takes you to the AEM Docs home page. Not sure if this topic is still needed?? -->

1. Kopiera **installationslänken**.

   Du kan även hämta ett arkiv i stället för att använda installationslänken. Den här metoden tillåter offlineinstallation, men du får inga meddelanden om automatiska uppdateringar på det här sättet.

1. Öppna menyn **Hjälp** i Eclipse.
1. Klicka på **Installera ny programvara**.
1. Klicka på **Lägg till..**.
1. Ange **i fältet** Namn`AEM Developer Tools`.
1. Kopiera installations-URL:en i fältet **Plats**.
1. Klicka på **Lägg till**.
1. Kontrollera både **AEM**- och **Sling**-plugin-program.
1. Klicka på **Nästa**.
1. Klicka på **Nästa** igen i fönstret **Installationsinformation**.
1. Acceptera licensavtalen och klicka på **Slutför**.
1. Klicka på **RestartNow** för att starta om Eclipse.

## AEM Perspective {#the-aem-perspective}

I Eclipse avgör ett perspektiv vilka åtgärder och vyer som finns tillgängliga i ett fönster och aktiverar uppgiftsorienterad interaktion med resurser i Eclipse. Mer information om perspektiv finns i [Eclipse-dokumentationen](https://help.eclipse.org/latest/index.jsp).

_Experience Manager utvecklingsverktyg för Eclipse_ har ett AEM-perspektiv som ger dig full kontroll över dina AEM-projekt och instanser. Så här öppnar du AEM Perspective:

1. Välj **Fönster** > **Perspektiv** > **Öppna perspektiv** > **Annat** på Eclipse-menyraden.
1. Välj **AEM** i dialogrutan och klicka på **Öppna**.

![Perspektivet AEM i Eclipse](assets/eclipse-aem-perspective.png)

## Exempel på flermodulsprojekt {#sample-multi-module-project}

_Experience Manager Developer Tools for Eclipse_ innehåller ett exempel på ett projekt med flera moduler som hjälper dig att snabbt komma igång med projektkonfigurationen i Eclipse. Det är också en metodguide till flera AEM-funktioner. [Läs mer om projekttypen](https://github.com/adobe/aem-project-archetype).

Så här skapar du exempelprojektet:

1. Gå till avsnittet **AEM** på menyn **Arkiv** > **Nytt** > **Projekt** och välj **AEM Sample Multi-Module Project**.

   ![Exempel på AEM-projekt med flera moduler](assets/aem-sample-project.png)

1. Klicka på **Nästa**.

   >[!NOTE]
   >
   >Det här steget kan ta en stund eftersom m2eclipse måste skanna arkivtypskatalogerna.

1. Välj `com.adobe.granite.archetypes : sample-project-archetype : <highest-number>` på menyn och klicka sedan på **Nästa**.

   ![Välj arketypsversion](assets/select-archetype.png)

1. Ange följande fält för exempelprojektet:

   * **Namn**
   * **Grupp-ID**
   * **Artefakt-ID**
   * **appId** - Du kan behöva utöka alternativen för **Avancerat** för att ange det här värdet.
   * **appTitle** - Du kan behöva utöka alternativen för **Avancerat** för att ange det här värdet.
   * **Paket** - Du kan behöva utöka alternativen för **Avancerat** för att ange det här värdet.

   ![Definiera arkitekturtypsegenskaper](assets/archetype-properties.png)

1. Klicka på **Nästa**.

1. Sedan konfigurerar du en AEM-server som Eclipse ansluter till.

   Om du vill använda felsökningsfunktionen måste du ha startat AEM i felsökningsläge, vilket du kan göra genom att lägga till följande på kommandoraden:

   ```text
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![Anslut till AEM-server](assets/connect-server.png)

1. Klicka på **Slutför**. Projektstrukturen skapas.

   >[!NOTE]
   >
   >Vid en ny installation (närmare bestämt när större beroenden aldrig har laddats ned) kan du få projektet skapat med fel. I det här fallet följer du proceduren som beskrivs i [Lösa ogiltig projektdefinition](#resolving-invalid-project-definition).

## Importera befintliga projekt {#how-to-import-existing-projects}

Du kan använda funktionen **Nytt projekt** för att skapa rätt struktur för dig:

1. Följ instruktionerna för att skapa ett [exempel på ett flermodulsprojekt](#sample-multi-module-project) och du har följande projekt skapade för dig, vilket gör att du kan separera dina problem på ett bra sätt:

   * `PROJECT.ui.apps` för `/apps`- och `/etc`-innehåll
   * `PROJECT.ui.content` för `/content` som har skapats
   * `PROJECT.core` för Java™-paket (dessa blir intressanta när du vill lägga till Java™-kod)
   * `PROJECT.it.launcher` och `PROJECT.it.tests` för integreringstester

1. Ersätt innehållet i ditt `PROJECT.ui.apps`-projekt med mapparna `apps` och `etc` i ditt paket:

   1. I projektutforskarpanelen, visa `PROJECT.ui.apps` > `src` > `main` > `content` > `jcr_root` > `apps`.
   1. Högerklicka på mappen `apps` och välj **Visa i** > **Systemutforskaren**.
   1. Ta bort mapparna `apps` och `etc` som du nu ska visa och placera `apps` och `etc` mappar i innehållspaketet här.
   1. Högerklicka på projektet `PROJECT.ui.apps` i Eclipse och välj **Uppdatera**.

1. Gör sedan samma sak för `PROJECT.ui.content` och ersätt dess innehållsmapp med ett av dina paket:

   1. I projektutforskarpanelen, visa `PROJECT.ui.content` > `src` > `main` > `content` > `jcr_root` > `content`.
   1. Högerklicka på den djupare innehållsmappen och välj **Visa i** > **Systemutforskaren**.
   1. Ta bort innehållsmappen som du nu ska se och placera innehållsmappen i innehållspaketet här.
   1. Högerklicka på projektet `PROJECT.ui.content` i Eclipse och välj **Uppdatera**.

1. Nu måste du uppdatera `filter.xml`-filerna för dessa två projekt så att de motsvarar innehållet i ditt innehållspaket. Om du vill göra det öppnar du `META-INF/vault/filter.xml`-filen för ditt innehållspaket i en separat text-/kodredigerare.

   * Detta är ett exempel på hur din `filter.xml`-fil kan se ut:

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

1. När det gäller innehållet i ditt paket som delats upp i två projekt måste du också dela upp dessa filterregler i två och uppdatera `filter.xml`-filerna för de två projekten.

   1. Öppna `PROJECT.ui.apps/src/main/content/META-INF/filter.xml` i Eclipse.
   1. Ersätt innehållet i elementet `<workspaceFilter>` med reglerna i paketet som börjar med `/apps` och `/etc`
      * Till exempel:

        ```xml
        <?xml version="1.0" encoding="UTF-8"?>
        <workspaceFilter version="1.0">
           <filter root="/apps/foo"/>
           <filter root="/apps/foundation/components/bar"/>
           <filter root="/etc/designs/foo"/>
        </workspaceFilter>
        ```

   1. Öppna sedan `PROJECT.ui.content/src/main/content/META-INF/filter.xml`.
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

1. Spara alla ändringar. Nu kan du synkronisera det nya innehållet med din AEM-instans.

1. Kontrollera att anslutningen har startats på serverpanelen och starta den om den inte redan har startats.
1. Klicka på ikonen **Rensa och publicera** .

När du är klar bör du låta paketet köras på din instans, och när du sparar synkroniseras alla ändringar automatiskt till instansen.

Om du vill återskapa ett paket från ditt projekt högerklickar du på `PROJECT.ui.apps` eller `PROJECT.ui.content` och väljer **Kör som** > **Maven Install**.

Nu har du skapat en målmapp med ditt paket (som till exempel kallas `PROJECT.ui.apps-0.0.1-SNAPSHOT.zip`).

## Felsökning {#troubleshooting}

### Löser ogiltig projektdefinition {#resolving-invalid-project-definition}

Så här löser du ogiltiga beroenden och projektdefinitioner:

1. Markera alla skapade projekt.
1. Högerklicka.
1. Välj **Maven** > **Uppdatera projekt** på snabbmenyn.
1. Kontrollera **Tvinga uppdateringar av ögonblicksbild/släppningar**.
1. Klicka på **OK**.

Eclipse hämtar nödvändiga beroenden. Det här kan ta en stund.

## Mer information {#more-information}

Den officiella versionen av Apache Sling IDE-verktygen för Eclipse-webbplatsen innehåller användbar information:

* [**Apache Sling IDE-verktygen för Eclipse** Användarhandbok](https://sling.apache.org/documentation/development/ide-tooling.html) hjälper dig igenom de övergripande begreppen, serverintegrationen och distributionsfunktionerna som stöds av AEM utvecklingsverktyg.
* Avsnittet [Felsökning](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting).
* Listan [Kända fel](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues).

Följande officiella [Eclipse](https://www.eclipse.org/)-dokumentation kan hjälpa dig att konfigurera miljön:

* [Komma igång med Eclipse](https://eclipseide.org/getting-started/)
* [Eclipse Luna Help System](https://help.eclipse.org/latest/index.jsp)
* [Maven Integration (m2eclipse)](https://www.eclipse.org/m2e/)
