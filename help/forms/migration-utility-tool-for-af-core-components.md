---
title: Migreringsverktyg för att konvertera adaptiv Forms baserat på baskomponenter till centrala komponentbaserade formulär
description: Lär dig installera och använda migreringsverktyget för att konvertera adaptiv Forms baserat på Foundation-komponenter till kärnkomponentbaserade formulär.
Keywords: Migration Utility tool, Convert Adaptive Forms based on foundation components to core component based forms, Convert Foundation forms to Core components forms, Using Modernizer tool to convert Foundation Components to Core components in forms.
role: User, Developer, Admin
features: core components
hide: true
hidefromtoc: true
source-git-commit: 494e90bd5822495f0619e8ebf55f373a26a3ffe6
workflow-type: tm+mt
source-wordcount: '897'
ht-degree: 0%

---


# Introduktion

Du kan använda migreringsverktyget för att konvertera adaptiv Forms baserat på baskomponenter till centrala komponentbaserade formulär. Du kan använda [Verktyget AEM](https://opensource.adobe.com/aem-modernize-tools/) som ett migreringsverktyg. The [Verktyg för AEM](https://opensource.adobe.com/aem-modernize-tools/) tillhandahåller en uppsättning verktyg som används för att konvertera adaptiva Forms-baserade baskomponenter till de moderna och stödda kärnkomponenterna.

## Vad är AEM verktyg för modernisering?

[Verktyg för AEM](https://opensource.adobe.com/aem-modernize-tools/) avser en uppsättning verktyg eller program som är avsedda att underlätta processen att modernisera eller uppdatera Adobe Experience Manager-projekt (AEM). De här verktygen hjälper dig vanligtvis att konvertera äldre komponenter eller funktioner i AEM till nyare, effektivare och stöds.

AEM Modernize Tools konverterar Adaptive Forms som bygger på äldre grundkomponenter till nyare grundformulär. Denna konverteringsprocess säkerställer att formulären överensstämmer med moderna standarder och funktioner, vilket kan förbättra prestanda, kompatibilitet och enkelt underhåll i AEM.

![Verktyg för AEM](/help/forms/assets/aem-modernize-tools.png)

>[!NOTE]
> 
> Vi rekommenderar att du installerar verktygen AEM modernisering på din lokala AEM. Överför de grundläggande blanketterna till de centrala komponentbaserade blanketterna. Hämta formuläret tillsammans med dess resurser. Överför sedan formuläret och dess resurser till den miljö som krävs.

## Krav för att använda AEM verktyg för modernisering

* [Konfigurera lokal utvecklingsmiljö för AEM Forms](/help/forms/setup-local-development-environment.md)
* [Möjliggör adaptiva kärnkomponenter i Forms för er miljö.](/help/forms/enable-adaptive-forms-core-components.md)

* Lägg till dina användare i [!DNL forms-users] grupp. Medlemmarna i [!DNL forms-users] gruppen har behörighet att skapa ett adaptivt formulär.

* Användare med följande roller har behörighet att installera AEM Modernisera verktyg i en AEM miljö:
   * Utvecklarroll
   * Administratörsroll En detaljerad lista över formulärspecifika användargrupper finns i [Grupper och behörigheter](forms-groups-privileges-tasks.md).

## Installera och konfigurera AEM verktyg för modernisering

Steg för att installera och konfigurera AEM verktygen:

1. [Installera AEM Modernisera verktyg i din lokala AEM Forms-miljö](#install-aem-modernize-tools)
2. [Aktivera AEM verktyg för modernisering i din lokala AEM Forms-miljö](#enable-aem-modernize-tools)

### Installera AEM Modernisera verktyg i din lokala AEM Forms-miljö {#install-aem-modernize-tools}

Så här installerar du AEM Modernisera verktyg i din lokala AEM Forms-miljö:

1. Starta den lokala AEM Author Service genom att köra följande från kommandoraden:

   `java -jar aem-author-p4502.jar`

   >[!NOTE]
   >
   > Ange administratörslösenordet som `admin`. Alla administratörslösenord är godtagbara, men du bör använda standardvärdet för lokal utveckling för att minska behovet av att konfigurera om.

1. Klona [Verktyg för AEM](https://git.corp.adobe.com/livecycle/forms-modernizer/tree/convertForms) i din lokala dator.

   ```Shell
   git clone [Path of Git repository of AEM Modernize Tools]
   ```
   Ersätt [Sökväg till Git-databasen för AEM verktyg för modernisering] med den faktiska URL:en för motsvarande Git-databas för AEM verktyg för modernisering.
När kommandot har körts har du en lokal kopia av AEM verktygskatalog på datorn.

1. Navigera till`[AEM Modernize Tools Repository]`  i ditt lokala system.
1. Kör följande kommando:

   ```Shell
       mvn clean install 
   ```
![Installationsavbildningen har slutförts](/help/forms/assets/aem-modernize-install-steps.png)

När installationen är klar blir AEM verktyg för modernisering tillgängliga för din miljö.

![Aktivera AEM verktyg för modernisering](/help/forms/assets/enable-aem-modernizer-tools.png)


### Aktivera AEM verktyg för modernisering i din lokala AEM Forms-miljö{#enable-aem-modernize-tools}

Om du vill aktivera och använda de AEM verktygen för modernisering i din AEM miljö är det viktigt att mappa reglerna för migrering av baskomponenter till kärnkomponenter:

1. Logga in på din författarinstans.
1. Navigera till `http://[host]:[port]/system/console/configMgr`
1. Sök och redigera `AEM Modernize Tools - Component Rewrite Rule Service`.
1. Lägg till `Component Rule Paths` as `/apps/forms-modernizer/rules`.
1. Klicka **Spara** för att spara ändringarna.

![Regel för AEM](/help/forms/assets/aem-modernize-tools-component-rule.png)

## Kör AEM Modernisera verktyg för att konvertera grundkomponentbaserade blanketter till kärnkomponentbaserade blanketter

1. Gå till **[!UICONTROL Tools > AEM Modernize Tools > Forms Conversion]**.

   ![Välj AEM verktyg för modernisering](/help/forms/assets/aem-modernize-tools-select.png)

1. Välj **[!UICONTROL Forms Conversion]** alternativ.

   ![Välj alternativet Forms-konvertering](/help/forms/assets/aem-modernize-forms-conversion.png)

1. Klicka **Skapa** för att skapa ett nytt jobb.

   ![AEM Modernisera verktyg Skapa jobb](/help/forms/assets/aem-modernize-tools-create-job.png)

1. Ange **[!UICONTROL Job Name]**.
1. I **[!UICONTROL Form]** kan du välja något av följande alternativ:
   * **Ingen** : Välj det här alternativet om formulärhantering inte krävs.
   * **Återställ** : Välj det här alternativet om du vill återställa formuläret till läget före den senaste konverteringen.
   * **Kopiera till mål**: Välj det här alternativet om du vill kopiera formuläret innan du utför konverteringen.
I vårt fall **Kopiera till mål** är markerat. Om **Kopiera till mål** är markerat, **[!UICONTROL Source Path]** och **[!UICONTROL Target Path]** blir synliga.

1. Ange `source folder` namnet i **[!UICONTROL Source Path]**.
1. Ange `target folder` namnet i **[!UICONTROL Target Path]**.
1. Välj **[!UICONTROL Next]**.
1. Klicka på **[!UICONTROL Add Forms]**. Alla formulär i `source folder` visas på skärmen.
1. Välj formuläret baserat på grundkomponenterna för att konvertera det till ett formulär baserat på kärnkomponenterna. Du kan också markera flera formulär.

   ![AEM Verktyg för modernisering Välj formulär](/help/forms/assets/aem-modernize-tools-select-form.png)

1. Klicka på **[!UICONTROL Select]**.
1. Klicka **[!UICONTROL Schedule Job]** för att starta konverteringsprocessen.
1. Klicka **[!UICONTROL Convert]** från **[!UICONTROL Convert Pages]** -dialogrutan.

   ![AEM Modernisera verktyg - konvertera sidor](/help/forms/assets/aem-modernize-tools-convert-form.png)

   När processens status ändras till `success`. Navigera till `target folder` för att se det konverterade formuläret.

   ![AEM har moderniserats](/help/forms/assets/aem-modernize-tools-success.png)

1. Markera det adaptiva formuläret och välj > **[!UICONTROL Properties]**. Sidan Formuläregenskaper öppnas.
   ![AEM verktygets målmapp](/help/forms/assets/aem-modernize-tools-destination-folder.png)

1. Välj **[!UICONTROL Save and Close]** om du vill spara egenskaperna för det konverterade formuläret igen.
   ![AEM modernisch Tools Adpative Form Properties](/help/forms/assets/aem-modernize-tools-af-properties.png)

Nu ser du att den adaptiva formen som bygger på grundkomponenterna omvandlas till den adaptiva formen som bygger på kärnkomponenterna.

## Att tänka på när du använder migreringsverktyget {#considerations}

* Om formuläret som bygger på grundkomponenterna innehåller anpassade funktionsregler måste du skriva om dessa regler för det konverterade formuläret baserat på kärnkomponenterna.
* Det konverterade formuläret innehåller inga regler i regelredigeraren, vilket kräver att regler för det konverterade formuläret skrivs om.
* Du måste återskapa översättningsjobbet för det konverterade formuläret.

## Bästa praxis {#best-practices}

* Formuläret som bygger på grundkomponenterna innehåller endast de komponenter som finns i de kärnkomponentbaserade komponenterna.
* Kontrollera att reglerna är formaterade i XML.


