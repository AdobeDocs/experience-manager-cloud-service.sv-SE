---
title: Betydande ändringar av Adobe Experience Manager (AEM) som en Cloud Service
description: Betydande ändringar av Adobe Experience Manager (AEM) som en Cloud Service
translation-type: tm+mt
source-git-commit: 515e462e942d58758a11e0a9bd3b1c3990a4dcf9
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 9%

---


# Observerbara ändringar av Adobe Experience Manager (AEM) som en Cloud Service {#notable-changes-aem-cloud}

AEM Cloud Service har många nya funktioner för  att administrera AEM-projekt. Det finns dock ett antal skillnader mellan AEM Sites på plats eller i Adobe Managed Service jämfört med AEM Cloud Service. Det här dokumentet visar de viktiga skillnaderna.

>[!NOTE]
>Det här dokumentet markerar de anmärkningsvärda ändringarna av AEM som helhet. Mer information och lösningsspecifika ändringar finns i:
>
>* [En introduktion till Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md)
>* [Nyheter och skillnader](/help/overview/what-is-new-and-different.md) i Adobe Experience Manager as a Cloud Service och tidigare versioner
>* [Arkitekturen](/help/core-concepts/architecture.md) i Adobe Experience Manager as a Cloud Service
>* [Viktiga ändringar i AEM Sites as a Cloud Service](/help/sites-cloud/sites-cloud-changes.md)
>* [Viktiga ändringar i AEM Assets as a Cloud Service](/help/assets/assets-cloud-changes.md)


De största skillnaderna finns i följande områden:

* [/apps och /libs kan inte ändras under körning](#apps-libs-immutable)

* [OSGi-paket och -inställningar måste vara databasbaserade](#osgi)

* [Ändringar i publiceringsdatabasen tillåts inte](#changes-to-publish-repo)

* [Anpassade runmodes tillåts inte](#custom-runmodes)

* [Borttagning av replikeringsagenter](#replication-agents)

* [Borttagning av Classic UI](#classic-ui)

* [Publish-side Delivery](#publish-side-delivery)

* [Hantering och leverans av tillgångar](#asset-handling)

## /apps and /libs are immutable at runtime {#apps-libs-immutable}

Allt innehåll och alla undermappar i `/apps` och `/libs` är skrivskyddade. Funktioner eller anpassad kod som förväntas göra ändringar där kommer inte att kunna göra det. Ett fel returneras om att det här innehållet är skrivskyddat och att skrivåtgärden inte kunde slutföras. Detta påverkar ett antal AEM:

* Inga ändringar i `/libs` tillåts alls.
   * Det här är inte en ny regel, men den har inte införts i tidigare lokala versioner av AEM.
* Övertäckningar för områden i `/libs` som tillåts överlappa är fortfarande tillåtna i `/apps`.
   * Sådana övertäckningar måste komma från Git via CI/CD-pipeline.
* Designinformation för statiska mallar som lagras i `/apps` kan inte redigeras via användargränssnittet.
   * Vi rekommenderar att du använder Redigerbara mallar i stället.
   * Om statiska mallar fortfarande krävs måste konfigurationsinformationen komma från Git via CI/CD-flödet.
* MSM Blueprint och anpassade MSM roll-out-konfigurationer måste installeras från Git via CI/CD-pipeline.
* I18n-översättningsändringar måste komma från Git via CI/CD-pipeline.

## OSGi-paket och -inställningar måste vara databasbaserade {#osgi}

Webbkonsolen, som användes i tidigare versioner av AEM för att ändra OSGi-inställningarna, är inte tillgänglig i AEM Cloud Service. Därför måste ändringar av OSGi införas via CI/CD-ledningen.

* Ändringar av OSGi-inställningar kan bara göras via Git-beständighet som JCR-baserade OSGi-inställningar.
* Nya eller uppdaterade OSGi-paket måste introduceras via Git som en del av CI/CD-produktionsprocessen.

## Ändringar i publiceringsdatabasen tillåts inte {#changes-to-publish-repo}

Förutom ändringar i mappen `/home` på publiceringsnivån tillåts inte direkta ändringar i publiceringsdatabasen på AEM Cloud Service. I tidigare versioner av lokala AEM eller AEM på AMS kan kodändringar göras direkt till publiceringsdatabasen. Vissa begränsningar kan minskas på följande sätt:

* För innehåll- och innehållsbaserad konfiguration: gör ändringarna i författarinstansen och publicerar dem.
* För kod och konfiguration: gör ändringarna i GIT-databasen och kör CI/CD-flödet för att implementera dem.

## Anpassade runmodes tillåts inte {#custom-runmodes}

Följande körningslägen är färdiga för AEM Cloud Service:

* `author`
* `publish`
* `prod`
* `author.prod`
* `publish.prod`
* `stage`
* `author.stage`
* `publish.stage`
* `dev`
* `author.dev`
* `publish.dev`

Ytterligare eller anpassade körningslägen är inte möjliga i AEM Cloud Service.

## Borttagning av replikeringsagenter {#replication-agents}

I AEM Cloud Service publiceras innehåll med [Sling Content Distribution](https://sling.apache.org/documentation/bundles/content-distribution.html). Replikeringsagenterna som användes i tidigare versioner av AEM används inte längre eller tillhandahålls, vilket kan påverka följande områden i befintliga AEM projekt:

* Anpassade arbetsflöden som till exempel skickar innehåll till replikeringsagenter för förhandsgranskningsservrar.
* Anpassning till replikeringsagenter för att omvandla innehåll
* Använda omvänd replikering för att återföra innehåll från publicering till författaren

## Ta bort det klassiska användargränssnittet {#classic-ui}

Det klassiska användargränssnittet är inte längre tillgängligt i AEM Cloud Service.

## Publiceringssidleverans {#publish-side-delivery}

HTTP-acceleration inklusive CDN och trafikhantering för författar- och publiceringstjänster tillhandahålls som standard i AEM Cloud Service.

För projektövergångar från AMS eller en lokal installation rekommenderar Adobe starkt att man utnyttjar det inbyggda CDN, eftersom funktioner i AEM Cloud Service är optimerade för det CDN som tillhandahålls.

## Resurshantering och leverans {#asset-handling}

Överföring, hantering och nedladdning av resurser har optimerats i Assets som en Cloud Service för att bli effektivare och möjliggöra bättre skalning och snabbare uppladdningar och nedladdningar. Detta kan dock påverka en del befintlig anpassad kod.

* Standardarbetsflödet **DAM-resursuppdatering** i tidigare versioner av AEM är inte längre tillgängligt.
* Webbplatskomponenter som levererar binära **utan omformning** bör använda direkt nedladdning.
   * Sling GET-servertjänsten har ändrats till att göra detta som standard.
* Webbplatskomponenter som levererar en binär **med transformering** (till exempel storleksändring via serverlet) kan fortsätta att fungera som de har.
* Resurser som kommer in via Package Manager kräver manuell ombearbetning med åtgärden **Återbearbeta resurs** i Assets-gränssnittet.
