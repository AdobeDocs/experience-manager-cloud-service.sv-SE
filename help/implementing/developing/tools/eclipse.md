---
title: AEM Developer Tools for Eclipse
description: AEM Developer Tools for Eclipse
translation-type: tm+mt
source-git-commit: c40d668cb6dcf5c3e2d09504b547457306a99c85
workflow-type: tm+mt
source-wordcount: '1182'
ht-degree: 1%

---


# AEM Developer Tools for Eclipse{#aem-developer-tools-for-eclipse}

![](assets/eclipse-logo.png)

## Översikt {#overview}

AEM Developer Tools for Eclipse är en Eclipse-plugin som bygger på [Eclipse-pluginen för Apache Sling](https://sling.apache.org/documentation/development/ide-tooling.html) som lanserats under Apache License 2.

Den har flera funktioner som gör AEM enklare:

* Smidig integrering med AEM instanser via Eclipse Server Connector
* Synkronisering för både innehåll och OSGi-paket
* Felsökningsstöd med möjlighet att byta kod under drift
* Enkel start av AEM projekt via en särskild projektguide
* Enkel redigering av JCR-egenskaper

## Krav {#requirements}

Innan du använder AEM Developer Tools måste du:

* Hämta och installera [Eclipse IDE för Java-utvecklare](https://www.eclipse.org/downloads/packages/)för företag.
* Konfigurera förmörkelseinstallationen för att säkerställa att du har minst 1 gigabyte stackminne genom att redigera din `eclipse.ini` konfigurationsfil enligt beskrivningen i Vanliga frågor om [Eclipse](https://wiki.eclipse.org/FAQ_How_do_I_increase_the_heap_size_available_to_Eclipse).

>[!NOTE]
>
>I macOS måste du högerklicka på **Eclipse.app** och sedan välja **Visa paketinnehåll** för att kunna hitta `eclipse.ini`**.**

## Installera AEM Developer Tools for Eclipse {#how-to-install-the-aem-developer-tools-for-eclipse}

När du har uppfyllt [kraven](#requirements) ovan kan du installera plugin-programmet på följande sätt:

1. Öppna webbplatsen [AEM utvecklingsverktyg.](https://eclipse.adobe.com/aem/dev-tools/)

1. Kopiera **installationslänken**.

   Observera att du kan hämta ett arkiv i stället för att använda installationslänken. Detta tillåter offlineinstallation men du kommer att sakna automatiska uppdateringsmeddelanden på det här sättet.

1. Öppna **Hjälp** -menyn i Eclipse.
1. Klicka på **Installera ny programvara**.
1. Click **Add...**.
1. Ange **Namn** `AEM Developer Tools`.
1. In **Location** copy the installation URL.
1. Click **Add**.
1. Kontrollera både **AEM** - och **Sling** -plugin-program.
1. Klicka på **Nästa**.
1. Klicka på **Nästa** igen i fönstret **Installationsinformation** .
1. Acceptera licensavtalen och klicka på **Slutför**.
1. Klicka på **RestartNow** för att starta om Eclipse.

## AEM {#the-aem-perspective}

I Eclipse bestämmer ett perspektiv vilka åtgärder och vyer som är tillgängliga i ett fönster och aktiverar uppgiftsorienterad interaktion med resurser i Eclipse. Mer information om perspektiv finns i dokumentationen för [Eclipse.](https://help.eclipse.org)

AEM utvecklingsverktyg för Eclipse har ett AEM perspektiv som ger dig full kontroll över dina AEM projekt och instanser. Så här öppnar du AEM perspektiv:

1. På Eclipse-menyraden väljer du **Fönster** -> **Perspektiv** -> **Öppna perspektiv** -> **Annat**.
1. Markera **AEM** i dialogrutan och klicka på **Öppna**.

![AEM i Eclipse](assets/eclipse-aem-perspective.png)

## Exempel på flermodulsprojekt {#sample-multi-module-project}

I AEM Developer Tools for Eclipse finns ett exempel på ett flermodulsprojekt som hjälper dig att snabbt komma igång med projektkonfigurationen i Eclipse, och som en praktisk guide till flera AEM funktioner. [Läs mer om Project Archetype](https://github.com/Adobe-Marketing-Cloud/aem-project-archetype).

Så här skapar du exempelprojektet:

1. På menyn **Arkiv** > **Nytt** > **Projekt** bläddrar du till **AEM** och väljer **AEM Sample Multi-Module Project**.

   ![Exempel på AEM projekt med flera moduler](assets/aem-sample-project.png)

1. Klicka på **Nästa**.

   >[!NOTE]
   >
   >Det här steget kan ta en stund eftersom m2eclipse behöver skanna arkivtypskatalogerna.

1. Välj `com.adobe.granite.archetypes : sample-project-archetype : <highest-number>` från menyn och klicka sedan på **Nästa**.

   ![Välj arkivtypsversion](assets/select-archetype.png)

1. Ange följande fält för exempelprojektet:

   * **Namn**
   * **Grupp-ID**
   * **Artefakt-ID**
   * **appId** - Du kan behöva utöka de **avancerade** alternativen för att ange det här värdet.
   * **appTitle** - Du kan behöva utöka de **avancerade** alternativen för att ange det här värdet.
   * **Paket** - Du kan behöva utöka de **avancerade** alternativen för att ange det här värdet.

   ![Definiera egenskaper för arkityp](assets/archetype-properties.png)

1. Klicka på **Nästa**.

1. Sedan konfigurerar du en AEM som Eclipse ska ansluta till.

   Om du vill använda felsökningsfunktionen måste du ha startat AEM i felsökningsläge, vilket du kan göra genom att lägga till följande på kommandoraden:

   ```text
       -nofork -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=10123
   ```

   ![Anslut till AEM server](assets/connect-server.png)

1. Click **Finish**. Projektstrukturen skapas.

   >[!NOTE]
   >
   >Vid en ny installation (närmare bestämt när större beroenden aldrig har laddats ned) kan du få projektet skapat med fel. I så fall följer du proceduren som beskrivs i [Lösa ogiltig projektdefinition](#resolving-invalid-project-definition).

## Importera befintliga projekt {#how-to-import-existing-projects}

Du kan använda funktionen **Nytt projekt** för att skapa rätt struktur för dig:

1. Följ instruktionerna för att skapa ett [exempel på ett flermodulsprojekt](#sample-multi-module-project) , så skapas följande projekt åt dig, vilket gör att du kan separera problemen på ett bra sätt:

   * `PROJECT.ui.apps` för `/apps` och `/etc` innehåll
   * `PROJECT.ui.content` som `/content` har skapats
   * `PROJECT.core` för Java-paket (dessa blir intressanta så fort du vill lägga till Java-kod)
   * `PROJECT.it.launcher` och `PROJECT.it.tests` för integrationstester

1. Ersätt innehållet i ditt `PROJECT.ui.apps` projekt med paketets `apps` och `etc` mappar:

   1. I projektutforskarpanelen, visa `PROJECT.ui.apps` > `src` > `main` > `content` > `jcr_root` > `apps`.
   1. Högerklicka på `apps` mappen och välj **Visa i** > **Systemutforskaren**.
   1. Ta bort `apps` och `etc` mappar som du nu ska se och placera `apps` - och `etc` -mapparna för ditt innehållspaket här.
   1. Högerklicka på `PROJECT.ui.apps` projektet i Eclipse och välj **Uppdatera**.

1. Gör sedan samma sak för `PROJECT.ui.content` och ersätt innehållsmappen med den i paketet:

   1. I projektutforskarpanelen, visa `PROJECT.ui.content` > `src` > `main` > `content` > `jcr_root` > `content`.
   1. Högerklicka på den djupare innehållsmappen och välj **Visa i** -> **Systemutforskaren**.
   1. Ta bort innehållsmappen som du nu ska se och placera innehållsmappen i innehållspaketet här.
   1. Högerklicka på `PROJECT.ui.content` projektet i Eclipse och välj **Uppdatera**.

1. Nu måste du uppdatera filerna `filter.xml` för dessa två projekt så att de motsvarar innehållet i ditt innehållspaket. I så fall öppnar du `META-INF/vault/filter.xml` filen för ditt innehållspaket i en separat text-/kodredigerare.

   * Detta är ett exempel på hur din `filter.xml` fil kan se ut:

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

1. När det gäller innehållet i ditt paket som delats upp i två projekt måste du också dela upp dessa filterregler i två och uppdatera filerna för de två projekten i enlighet med detta `filter.xml` .

   1. Öppna i Eclipse `PROJECT.ui.apps/src/main/content/META-INF/filter.xml`.
   1. Ersätt innehållet i `<workspaceFilter>` elementet med reglerna i paketet som börjar med `/apps` och `/etc`
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
   1. Ersätt reglerna med reglerna i det paket som börjar med `/content`.
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
1. Klicka på ikonen **Rensa och publicera** .

När du är klar bör du låta paketet köras på din instans, och när du sparar synkroniseras alla ändringar automatiskt till instansen.

Om du vill återskapa ett paket från projektet högerklickar du på `PROJECT.ui.apps` eller `PROJECT.ui.content` väljer **Kör som** -> **Maven Install**.

Nu har du en målmapp som har skapats med ditt paket (kallas t.ex. `PROJECT.ui.apps-0.0.1-SNAPSHOT.zip`).

## Felsökning {#troubleshooting}

### Löser ogiltig projektdefinition {#resolving-invalid-project-definition}

Så här löser du ogiltiga beroenden och projektdefinitioner:

1. Markera alla skapade projekt.
1. Högerklicka.
1. Välj **Maven** -> **Uppdatera projekt** på snabbmenyn.
1. Markera **Tvinga uppdateringar av ögonblicksbilder/releaser**.
1. Click **OK**.

Eclipse hämtar nödvändiga beroenden. Det här kan ta en stund.

## Mer information {#more-information}

Den officiella versionen av Apache Sling IDE-verktygen för Eclipse-webbplatsen innehåller användbar information:

* I [**Apache Sling IDE Tooling for Eclipse** User Guide](https://sling.apache.org/documentation/development/ide-tooling.html)beskrivs de övergripande begreppen, serverintegrering och distributionsfunktioner som stöds av AEM Development Tools.
* Avsnittet [Felsökning](https://sling.apache.org/documentation/development/ide-tooling.html#troubleshooting).
* Listan [Kända fel](https://sling.apache.org/documentation/development/ide-tooling.html#known-issues).

Följande officiella [Eclipse](https://eclipse.org/) -dokumentation kan hjälpa dig att konfigurera miljön:

* [Komma igång med Eclipse](https://eclipse.org/users/)
* [Hjälpsystemet Eclipse Luna](https://help.eclipse.org/luna/index.jsp)
* [Maven Integration (m2eclipse)](https://www.eclipse.org/m2e/)
