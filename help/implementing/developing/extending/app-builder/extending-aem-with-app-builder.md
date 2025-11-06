---
title: Utökar [!DNL Adobe Experience Manager] as a Cloud Service med Adobe Developer App Builder.
description: Utökar [!DNL Adobe Experience Manager] as a Cloud Service med Adobe Developer App Builder.
exl-id: 50d82745-5deb-4bfa-961b-714842403601
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---

# Utöka [!DNL Adobe Experience Manager] as a Cloud Service med Adobe Developer App Builder {#extend-using-app-builder}

## Vad är App Builder för AEM as a Cloud Service? {#project-appbuilder}

Nya Adobe Developer App Builder är ett utbyggbart ramverk för utvecklare som enkelt kan utöka funktionerna i AEM as a Cloud Service.

App Builder har ett enhetligt ramverk för utbyggbarhet från tredje part för att integrera och skapa anpassade upplevelser som utökar Adobe Experience Manager. Med detta kompletta ramverk för utbyggbarhet, som bygger på Adobe infrastruktur, kan utvecklare skapa anpassade mikrotjänster, utöka och integrera Adobe Experience Manager i alla Adobe-lösningar och i resten av IT-stacken.

App Builder erbjuder ett sätt för kunder att enkelt utöka Adobe Experience Manager i olika fall:

* Utbyggbarhet för mellanvara - Koppla samman externa system med Adobe-program och skapa anpassade anslutningar eller använd en serie färdiga integreringar.
* Utbyggbarhet för bastjänster - Utöka de centrala programfunktionerna genom att utöka standardbeteendet med anpassade funktioner och affärslogik.
* Utbyggbarhet för användarupplevelse - Utöka kärnupplevelsen för att uppfylla verksamhetskrav eller bygga kundspecifika digitala resurser, butiker och back-office-appar.

>[!NOTE]
>
> För AEM 6.5-kunder som vill använda App Builder, se [Utöka Adobe Experience Manager 6.5 med Adobe Developer App Builder](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/app-builder.html).

## Arkitektur {#architecture}

Istället för en körklar lösning erbjuder Adobe Developer App Builder en gemensam, konsekvent och standardiserad utvecklingsplattform för utbyggnad av Adobe Cloud-lösningar som AEM:

* Adobe Developer Console - För utveckling av anpassade mikrotjänster och tillägg kan utvecklare skapa och hantera projekt med tillgång till alla verktyg och API:er som behövs för att skapa plugin-program och integreringar.
* Utvecklingsverktyg - verktyg med öppen källkod, SDK:er och bibliotek så att utvecklare enkelt kan skapa anpassade tillägg och integreringar. Använd React Spectrum (Adobe UI Toolkit) så att du får ett gemensamt användargränssnitt för alla Adobe-program.
* Tjänster - I/O Runtime för värdinfrastruktur på Adobe serverlösa plattform och I/O-händelser för händelsebaserade integreringar. Adobe har också färdiga funktioner för lagring av data och filer.
* Adobe Experience Cloud - Utvecklare kan skicka tillägg och integreringar som ska publiceras i sin Experience Cloud-organisation. Systemadministratörer kan sedan granska, hantera och godkänna dessa tillägg. När de publicerats kan du hitta dina anpassade App Builder-tillägg och verktyg tillsammans med andra Adobe Experience Cloud-program.

Följande diagram visar hur ett standardprogram som bygger på App Builder använder dessa funktioner:

![Arkitektur](/help/implementing/developing/extending/assets/appbuilder-architecture.jpg)

Mer information om App Builder-arkitekturen finns i [Översikt över arkitekturen.](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/architecture_overview/architecture-overview)

## Kom igång med App Builder {#additional-resources}

Adobe har skapat dokumentationen Komma igång så att du kan komma igång med App Builder:

* [App Builder Komma igång](https://developer.adobe.com/app-builder/docs/getting_started/)

## Fortsätta inlärningen med dokumentation {#appbuilder-documentation}

App Builder tillhandahåller videor och dokumentation för utvecklare, inklusive guider och referensdokumentation som hjälper dig att börja utveckla egna program:

* [App Builder-dokumentation](https://developer.adobe.com/app-builder/docs/overview/)
* [App Builder-videor](https://www.youtube.com/playlist?list=PLcVEYUqU7VRfDij-Jbjyw8S8EzW073F_o)

## Testa ett av exempelprogrammen {#appbuilder-codesamples}

Vill du börja utveckla? Adobe har massor av exempelprogram som hjälper dig att komma igång snabbt:

* [App Builder Code Labs på Adobe Developer webbplats](https://developer.adobe.com/app-builder/docs/resources/)