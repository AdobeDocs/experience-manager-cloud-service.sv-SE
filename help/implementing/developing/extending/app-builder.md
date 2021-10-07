---
title: Utöka [!DNL Adobe Experience Manager] as a Cloud Service med Adobe Developer App Builder.
description: Utöka [!DNL Adobe Experience Manager] as a Cloud Service med Adobe Developer App Builder.
source-git-commit: d37193833d784f3f470780b8f28e53b473fd4e10
workflow-type: tm+mt
source-wordcount: '589'
ht-degree: 0%

---


# Utöka [!DNL Adobe Experience Manager] as a Cloud Service med Adobe Developer App Builder {#extend-using-app-builder}

## Vad är App Builder för AEM as a Cloud Service? {#project-firefly}

Nya Adobe Developer App Builder är ett utbyggbart ramverk för utvecklare som enkelt kan utöka AEM as a Cloud Service funktioner.

App Builder erbjuder ett enhetligt ramverk för utbyggbarhet från tredje part för att integrera och skapa anpassade upplevelser som utökar Adobe Experience Manager. Med detta kompletta ramverk för utbyggbarhet, som bygger på Adobe infrastruktur, kan utvecklare skapa anpassade mikrotjänster, utöka och integrera Adobe Experience Manager över Adobe och hela IT-stacken.

Med App Builder kan kunderna enkelt utöka Adobe Experience Manager i olika fall:

* Utbyggbarhet för mediematerial - Koppla samman externa system med Adobe-applikationer och bygg upp anpassade anslutningar eller utnyttja en serie färdiga integreringar.
* Utbyggbarhet för bastjänster - Utöka de centrala programfunktionerna genom att utöka standardbeteendet med anpassade funktioner och affärslogik.
* Utbyggbarhet för användarupplevelse - Utöka kärnupplevelsen för att uppfylla verksamhetskrav eller bygga kundspecifika digitala resurser, butiker och back-office-appar.

App Builder (tidigare kallat Project Fire) har varit tillgängligt för företagskunder och partners via vår förhandsgranskning av utvecklare sedan sommaren 2020. Den allmänna tillgängligheten (GA) för App Builder är planerad till december 2021. Vi välkomnar att utvecklare provar App Builder via vårt [testprogram](http://adobe.ly/appbuilder-trial).

>[!NOTE]
>
> För AEM 6.5-kunder som vill utnyttja App Builder går du till [Extending Adobe Experience Manager 6.5 med Adobe Developer App Builder](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/app-builder.html).

## Arkitektur {#architecture}

I stället för en färdig lösning erbjuder Adobe Developer App Builder en gemensam, konsekvent och standardiserad utvecklingsplattform för utökade Adobe Cloud-lösningar som AEM, som:

* Adobe Developer Console - För utveckling av anpassade mikrotjänster och tillägg kan utvecklare skapa och hantera projekt med tillgång till alla verktyg och API:er de behöver för att skapa plugin-program och integreringar.
* Utvecklingsverktyg - verktyg med öppen källkod, SDK:er och bibliotek som gör det möjligt för utvecklare att enkelt bygga anpassade tillägg och integreringar. Använd React Spectrum (Adobe’s UI toolkit) för att ha ett gemensamt användargränssnitt för alla Adobe-appar.
* Tjänster - I/O Runtime för värdinfrastruktur på vår serverlösa plattform och I/O Events för händelsebaserade integreringar. Vi har också färdiga funktioner för lagring av data och filer.
* Adobe Experience Cloud - Utvecklare kan skicka tillägg och integreringar som ska publiceras i Experience Cloud-organisationen. Systemadministratörer kan sedan granska, hantera och godkänna dessa tillägg. När du har publicerat dina anpassade tillägg och verktyg i App Builder finns de tillsammans med andra Adobe Experience Cloud-program.

Följande diagram visar hur ett standardprogram som är byggt på App Builder utnyttjar dessa funktioner:

![Arkitektur](/help/implementing/developing/extending/assets/firefly-architecture.jpg)

Mer information om App Builder-arkitekturen finns i [Architecture Overview](https://www.adobe.io/app-builder/docs/guides/).

## Kom igång med App Builder {#additional-resources}

Vi har skapat en serie dokumentation som hjälper dig att komma igång med App Builder:

* [App Builder - komma igång](https://www.adobe.io/app-builder/docs/getting_started/)

## Fortsätta inlärningen med dokumentation {#appbuilder-documentation}

App Builder innehåller videor och dokumentation för utvecklare, inklusive guider och referensdokumentation, som hjälper dig att börja utveckla egna program:

* [App Builder-dokumentation](https://www.adobe.io/app-builder/docs/overview/)
* [App Builder-videor](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o)

## Testa ett av exempelprogrammen {#appbuilder-codesamples}

Vill du börja utveckla? Vi har massor av exempelprogram som hjälper dig att komma igång snabbt:

* [App Builder Code Labs på Adobe Developer Website](https://www.adobe.io/app-builder/docs/resources/)

## Stöd {#support}

För utvecklarsupport rekommenderar vi att utvecklare använder vårt [Experience League-forum](https://experienceleaguecommunities.adobe.com/t5/project-firefly/ct-p/project-firefly).
