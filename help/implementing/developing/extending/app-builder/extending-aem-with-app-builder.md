---
title: Utöka [!DNL Adobe Experience Manager] as a Cloud Service med Adobe Developer App Builder.
description: Utöka [!DNL Adobe Experience Manager] as a Cloud Service med Adobe Developer App Builder.
exl-id: 50d82745-5deb-4bfa-961b-714842403601
source-git-commit: 7260649eaab303ba5bab55ccbe02395dc8159949
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 0%

---

# Utöka [!DNL Adobe Experience Manager] as a Cloud Service med Adobe Developer App Builder {#extend-using-app-builder}

## Vad är App Builder för AEM as a Cloud Service? {#project-appbuilder}

Nya Adobe Developer App Builder är ett utbyggbart ramverk för utvecklare som enkelt kan utöka funktioner på AEM as a Cloud Service.

App Builder erbjuder ett enhetligt ramverk för utbyggbarhet från tredje part för att integrera och skapa anpassade upplevelser som utökar Adobe Experience Manager. Med detta kompletta ramverk för utbyggbarhet, som bygger på Adobe infrastruktur, kan utvecklare skapa anpassade mikrotjänster, utöka och integrera Adobe Experience Manager över Adobe-lösningar och hela IT-stacken.

Med App Builder kan kunderna enkelt utöka Adobe Experience Manager i olika fall:

* Utbyggbarhet för mellanvara - Koppla samman externa system med Adobe-program och skapa anpassade anslutningar eller använd en serie färdiga integreringar.
* Utbyggbarhet för bastjänster - Utöka de centrala programfunktionerna genom att utöka standardbeteendet med anpassade funktioner och affärslogik.
* Utbyggbarhet för användarupplevelse - Utöka kärnupplevelsen för att uppfylla verksamhetskrav eller bygga kundspecifika digitala resurser, butiker och back-office-appar.

App Builder har varit tillgängligt för företagskunder och partners via Adobe Developer Preview sedan sommaren 2020. Den allmänna tillgängligheten (GA) för App Builder är planerad till december 2021. Adobe välkomnar utvecklare att testa App Builder via [testprogram](https://developer.adobe.com/app-builder/trial/).

>[!NOTE]
>
> AEM 6.5-kunder som vill använda App Builder finns på [Utöka Adobe Experience Manager 6.5 med Adobe Developer App Builder](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/app-builder.html).

## Arkitektur {#architecture}

I stället för en färdig lösning erbjuder Adobe Developer App Builder en gemensam, enhetlig och standardiserad utvecklingsplattform för utökade Adobe Cloud-lösningar som AEM som:

* Adobe Developer Console - För utveckling av anpassade mikrotjänster och tillägg kan utvecklare skapa och hantera projekt med tillgång till alla verktyg och API:er som behövs för att skapa plugin-program och integreringar.
* Utvecklingsverktyg - verktyg med öppen källkod, SDK:er och bibliotek som gör det möjligt för utvecklare att enkelt bygga anpassade tillägg och integreringar. Använd React Spectrum (Adobe UI) så att du får ett gemensamt användargränssnitt för alla Adobe-program.
* Tjänster - I/O Runtime för hosting av infrastruktur på Adobe serverless-plattformen och I/O Events för händelsebaserade integreringar. Adobe har också färdiga funktioner för lagring av data och filer.
* Adobe Experience Cloud - Utvecklare kan skicka tillägg och integreringar som ska publiceras i Experience Cloud-organisationen. Systemadministratörer kan sedan granska, hantera och godkänna dessa tillägg. När du har publicerat dina anpassade tillägg och verktyg i App Builder finns de tillsammans med andra Adobe Experience Cloud-program.

Följande diagram visar hur ett standardprogram som är byggt på App Builder använder dessa funktioner:

![Arkitektur](/help/implementing/developing/extending/assets/appbuilder-architecture.jpg)

Mer information om App Builder-arkitekturen finns i [Arkitektur - översikt](https://developer.adobe.com/app-builder/docs/guides/).

## Kom igång med App Builder {#additional-resources}

Adobe har skapat dokumentationen Komma igång så att du kan komma igång med App Builder:

* [App Builder - komma igång](https://developer.adobe.com/app-builder/docs/getting_started/)

## Fortsätta inlärningen med dokumentation {#appbuilder-documentation}

App Builder innehåller videor och dokumentation för utvecklare, inklusive guider och referensdokumentation, som hjälper dig att börja utveckla egna program:

* [App Builder-dokumentation](https://developer.adobe.com/app-builder/docs/overview/)
* [App Builder-videor](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o)

## Testa ett av exempelprogrammen {#appbuilder-codesamples}

Vill du börja utveckla? Adobe har många exempelprogram som hjälper dig att komma igång snabbt:

* [App Builder Code Labs på Adobe Developer webbplats](https://developer.adobe.com/app-builder/docs/resources/)