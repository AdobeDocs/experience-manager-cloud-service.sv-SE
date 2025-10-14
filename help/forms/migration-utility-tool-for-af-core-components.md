---
title: Migreringsverktyg/AEM Modernize Tools för att konvertera adaptiv Forms baserad på Foundation Components till Core Component-baserade formulär
description: Lär dig installera och använda Migreringsverktyg/AEM Modernize Tools för att konvertera adaptiv Forms baserad på Foundation Components till Core Component-baserade formulär.
Keywords: Migration Utility Tool, Convert Adaptive Forms based on Foundation Components to Core Component based forms, Convert Foundation forms to Core Components forms, Using Modernizer Tool to convert Foundation Components to Core Components in forms.
role: User, Developer, Admin
features: core components
hide: true
hidefromtoc: true
exl-id: ee71a576-96a7-4c81-b3a3-1d678f010cba
feature: Adaptive Forms, Core Components
source-git-commit: 16b1e7ffa4e3812e9207bb283c63029939f7d14e
workflow-type: tm+mt
source-wordcount: '1036'
ht-degree: 0%

---

# Introduktion

<span class="preview"> Funktionen är tillgänglig under det tidiga adopterprogrammet. Du kan skriva till aem-forms-ea@adobe.com från ditt officiella e-post-id för att gå med i det tidiga adopterprogrammet och begära åtkomst till funktionen. </span>

Forms Conversion Utility, som ingår i sviten [AEM Modernize Tool](https://opensource.adobe.com/aem-modernize-tools/), hjälper dig att enkelt konvertera adaptiv Forms som skapats med äldre Foundation Components till formulär som utnyttjar de moderna, stödda funktionerna i Core Components.

## Vad är AEM Modernize Tools?

[AEM moderniseringsverktyg](https://opensource.adobe.com/aem-modernize-tools/) avser en uppsättning verktyg eller program som är utformade för att underlätta processen att uppdatera eller uppdatera Adobe Experience Manager (AEM)-projekt. Dessa verktyg hjälper dig vanligtvis att konvertera äldre komponenter eller funktioner inom AEM till nyare, effektivare och stöds. Forms Conversion Utility installeras under AEM Modernize Tools för att konvertera adaptiv Forms baserad på Foundation Components till Core Component-baserade formulär.

Forms Conversion Utility konverterar adaptiv Forms som är baserad på äldre Foundation-komponenter till nyare Core Component-baserade formulär. Denna konverteringsprocess säkerställer att formulären överensstämmer med moderna standarder och funktioner, vilket kan förbättra prestanda, kompatibilitet och enkel hantering i AEM-miljön.

![AEM Moderniseringsverktyg](/help/forms/assets/aem-modernize-tools.png)

>[!NOTE]
> 
>Vi rekommenderar att du installerar AEM Modernize Tools på din lokala AEM-installation. Migrera det adaptiva Forms som bygger på Foundation Components till Core Component-baserade formulär. Hämta formuläret tillsammans med dess resurser. Överför sedan formuläret och dess resurser till den miljö som krävs.

## Att tänka på när du använder AEM verktyg för modernisering {#considerations}

* Vid lyckade konverteringar tas alla regler som tillämpas på formuläret bort. Regler migreras inte automatiskt. Du bör återskapa och tillämpa dessa regler på det konverterade formuläret manuellt.
* Översättningsinställningarna som används i det ursprungliga formuläret överförs inte. Konfigurera om översättning för det konverterade formuläret.
* Om formuläret som bygger på Foundation Components innehåller skript eller anpassade funktionsregler måste du skriva om dem för det konverterade formuläret baserat på Core Components.
* Följande OOTB-grundskomponenter stöds ännu inte i Core Components och tas därför bort i den konverterade formen:

   * Adobe Sign-block
   * Diagram
   * Lista över bifogade filer
   * Fotnotsplatshållare
   * Bildval
   * Knappen Nästa
   * Knappen Föregående
   * Klottersignatur
   * Sammanfattningssteg
   * Verktygsfält

## Krav för att använda AEM Modernize Tools

* [Konfigurera lokal utvecklingsmiljö för AEM Forms](/help/forms/setup-local-development-environment.md).
* Installera den senaste versionen för att aktivera adaptiva Forms Core-komponenter för din AEM Cloud-tjänstmiljö.
* Lägg till dina användare i gruppen [!DNL forms-users]. Medlemmarna i gruppen [!DNL forms-users] har behörighet att skapa ett anpassat formulär.
* Användare med följande roller har behörighet att installera AEM Modernize Tools i en AEM-miljö:

   * Utvecklarroll
   * Administratörsroll

En detaljerad lista med formulärspecifika användargrupper finns i [Grupper och behörigheter](forms-groups-privileges-tasks.md).

## Installera och konfigurera AEM Modernize Tools

Så här installerar och konfigurerar du AEM Modernize Tools:

1. [Installera AEM Modernize Tools i din lokala AEM Forms-miljö](#install-aem-modernize-Tools)
1. [Aktivera AEM Modernize Tools för din lokala AEM Forms-miljö](#enable-aem-modernize-Tools)

### Installera AEM Modernize Tools i din lokala AEM Forms-miljö {#install-aem-modernize-Tools}

Så här installerar du AEM Modernize Tools i din lokala AEM Forms-miljö:

1. Öppna kommandotolken eller terminalen.
1. Starta den lokala AEM Author Service. Kör till exempel följande kod från för att starta den lokala AEM Author-instansen:

   `java -jar aem-author-p4502.jar`

1. Klona databasen [AEM Modernize Tool](https://github.com/adobe/forms-modernizer) i din lokala dator.

   ```Shell
   git clone [Path of Git repository of AEM Modernize Tool]
   ```

   När kommandot har utförts finns en lokal kopia av AEM Modernize Tool på datorn.

1. Navigera till `[AEM Modernize Tool Repository]` i din lokala dator.
1. Kör följande kommando:

   ```Shell
       mvn clean install 
   ```

![Installationsavbildningen &#x200B;](/help/forms/assets/aem-modernize-install-steps.png) har slutförts

När installationen är klar blir AEM verktyg för modernisering tillgängliga för din miljö.

![Aktivera verktyget AEM Migration Utility](/help/forms/assets/enable-aem-modernizer-tools.png)


### Aktivera AEM Modernize Tools för din lokala AEM Forms-miljö{#enable-aem-modernize-Tools}

Om du vill aktivera och använda AEM moderniseringsverktyg för din AEM-miljö är det viktigt att mappa reglerna för migrering av Foundation-komponenter till Core-komponenter:

1. Logga in på din författarinstans.
1. Navigera till `http://[host]:[port]/system/console/configMgr`
1. Sök efter och redigera `AEM Modernize Tools - Component Rewrite Rule Service`.
1. Lägg till `Component Rule Paths` som `/apps/forms-modernizer/rules`.
1. Klicka på **Spara** för att spara ändringarna.

![Komponentregeln AEM Modernize](/help/forms/assets/aem-modernize-tools-component-rule.png)

## Kör formulärkonverteringsverktyget för att konvertera Foundation Components-baserade formulär till Core Component-baserade formulär

1. Gå till **[!UICONTROL Tools > AEM Modernize Tools > Forms Conversion]**.

   ![Välj AEM moderniseringsverktyg](/help/forms/assets/aem-modernize-tools-select-form.png)

1. Välj alternativet **[!UICONTROL Forms Conversion]**.

   ![Välj alternativet Forms-konvertering](/help/forms/assets/aem-modernize-forms-conversion.png)

1. Klicka på **Skapa** för att skapa ett nytt jobb.

   ![AEM verktyg för modernisering - skapa jobb](/help/forms/assets/aem-modernize-tools-create-job.png)

1. Ange **[!UICONTROL Job Name]**.
1. På fliken **[!UICONTROL Form]** kan du välja något av följande alternativ:

   * **Inget** : Välj alternativet om du inte vill skapa en kopia av de Foundation Component-baserade formulären innan du påbörjar formulärkonverteringen.
   * **Återställ** : Välj alternativet att återställa formuläret till det tillstånd det hade innan formulärkonverteringen startades.
   * **Kopiera till mål**: Välj alternativet att skapa en kopia av de Foundation Component-baserade formulären innan du påbörjar formulärkonverteringen.

   I vårt fall är alternativet **Kopiera till mål** markerat. Om alternativet **Kopiera till mål** är markerat blir alternativen **[!UICONTROL Source Path]** och **[!UICONTROL Target Path]** synliga.

1. Ange namnet `source folder` i **[!UICONTROL Source Path]**.
1. Ange namnet `target folder` i **[!UICONTROL Target Path]**.
1. Välj **[!UICONTROL Next]**.
1. Klicka på **[!UICONTROL Add Forms]**. Alla formulär i `source folder` visas på skärmen.
1. Välj den adaptiva Forms som baseras på Foundation Components för att konvertera den till Core Component-baserade formulär. Du kan också markera flera formulär.

   ![AEM moderniseringsverktyg Välj formulär](/help/forms/assets/aem-modernize-tools-select-form.png)

1. Klicka på **[!UICONTROL Select]**.
1. Klicka på **[!UICONTROL Schedule Job]** för att starta konverteringsprocessen.
1. Klicka på **[!UICONTROL Convert]** i dialogrutan **[!UICONTROL Convert Pages]**.

   ![AEM verktyg för modernisering - konvertera sidor](/help/forms/assets/aem-modernize-tools-convert-form.png)

   När processens status ändras till `success`. Navigera till `target folder` för att se det konverterade formuläret.

   ![AEM Moderniseringsverktyg lyckades](/help/forms/assets/aem-modernize-tools-success.png)

1. Markera det adaptiva formuläret och välj > **[!UICONTROL Properties]**. Sidan Formuläregenskaper öppnas.

   ![Målmapp för AEM Modernize Tools](/help/forms/assets/aem-modernize-tools-destination-folder.png)

1. Välj **[!UICONTROL Save and Close]** om du vill spara egenskaperna för det konverterade formuläret igen.
   ![Anpassade formuläregenskaper för AEM Modernize Tools](/help/forms/assets/aem-modernize-tools-af-properties.png)

Nu ser du att den adaptiva formen som bygger på Foundation Components omvandlas till den adaptiva formen som bygger på Core Components.

## Bästa praxis {#best-practices}

* Kontrollera att dina Foundation Components-baserade formulär bara använder de komponenter som har motsvarande [Core Components](https://experienceleague.adobe.com/sv/docs/experience-manager-core-components/using/adaptive-forms/introduction#available-components-a-breakdown-by-component-type) tillgängliga. Om du använder Foundation Components som inte har någon motsvarande Core Component (Grundläggande komponent) konverteras inte Foundation Component (Grundläggande komponent). Därför fungerar den inte korrekt när du redigerar ett formulär
* Kontrollera att reglerna som konverterar Foundation Components till Core Components är formaterade i XML.
