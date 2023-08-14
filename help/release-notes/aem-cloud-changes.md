---
title: Betydande ändringar av Adobe Experience Manager (AEM) as a Cloud Service
description: Betydande ändringar av Adobe Experience Manager (AEM) as a Cloud Service
exl-id: fe11d779-66cd-45aa-aa6b-c819b88d2405
source-git-commit: 1994b90e3876f03efa571a9ce65b9fb8b3c90ec4
workflow-type: tm+mt
source-wordcount: '846'
ht-degree: 8%

---

# Betydande ändringar av Adobe Experience Manager (AEM) as a Cloud Service {#notable-changes-aem-cloud}

AEM Cloud Service har många nya funktioner för  att administrera AEM-projekt. Det finns dock ett antal skillnader mellan AEM Sites på plats eller i Adobe Managed Service jämfört med AEM Cloud Service. I det här dokumentet markeras de viktiga skillnaderna.

>[!CONTEXTUALHELP]
>id="aem_cloud_notable_changes"
>title="Betydande ändringar i AEM as a Cloud Service"
>abstract="På den här fliken kan du visa innehåll som hjälper dig att förstå skillnaderna mellan AEM lokalt, eller i Adobe Managed Services, jämfört med AEM as a Cloud Service."
>additional-url="https://video.tv.adobe.com/v/330543" text="AEM as a Cloud Service utveckling"


>[!NOTE]
>Det här dokumentet markerar de anmärkningsvärda ändringarna av AEM som helhet. Mer information och lösningsspecifika ändringar finns i:
>
>* [En introduktion till Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md)
>* [Nyheter och skillnader](/help/overview/what-is-new-and-different.md) i Adobe Experience Manager as a Cloud Service och tidigare versioner
>* [Arkitekturen](/help/overview/architecture.md) i Adobe Experience Manager as a Cloud Service
>* [Viktiga ändringar i AEM Sites as a Cloud Service](/help/sites-cloud/sites-cloud-changes.md)
>* [Viktiga ändringar i AEM Assets as a Cloud Service](/help/assets/assets-cloud-changes.md)

De största skillnaderna finns i följande områden:

* [/apps och /libs kan inte ändras under körning](#apps-libs-immutable)

* [OSGi-paket och -konfigurationer måste behandlas som kod](#osgi)

* [Ändringar i publiceringsdatabasen tillåts inte](#changes-to-publish-repo)

* [Anpassade runmodes tillåts inte](#custom-runmodes)

* [Borttagning av replikeringsagenter och relaterade ändringar](#replication-agents)

* [Borttagning av Classic UI](#classic-ui)

* [Publish-side Delivery](#publish-side-delivery)

* [Hantering och leverans av tillgångar](#asset-handling)

## /apps och /libs kan inte ändras under körning {#apps-libs-immutable}

Allt innehåll och alla undermappar i `/apps` och `/libs` är skrivskyddad. Funktioner eller anpassad kod som förväntas göra ändringar där kommer inte att kunna göra det. Ett fel returneras som anger att sådant innehåll är skrivskyddat och att skrivåtgärden inte kunde slutföras. Detta påverkar ett antal AEM:

* Inga ändringar i `/libs` tillåts överhuvudtaget.
   * Det här är inte en ny regel, men den har inte införts i tidigare lokala versioner av AEM.
* Övertäckningar för områden i `/libs` som får övertäckas fortfarande tillåts inom `/apps`.
   * Sådana övertäckningar måste komma från Git via CI/CD-pipeline.
* Designinformation för statiska mallar som lagras i `/apps` kan inte redigeras via användargränssnittet.
   * Du bör använda Redigerbara mallar i stället.
   * Om statiska mallar fortfarande krävs måste konfigurationsinformationen komma från Git via CI/CD-flödet.
* MSM Blueprint och anpassade MSM roll-out-konfigurationer måste installeras från Git via CI/CD-pipeline.
* I18n-översättningsändringar måste komma från Git via CI/CD-pipeline.

## OSGi-paket och -konfigurationer måste behandlas som kod {#osgi}

Ändringar av OSGi-paket och -konfigurationer måste införas via CI/CD-pipeline.

* Nya eller uppdaterade OSGi-paket måste introduceras via Git via CI/CD-pipeline.
* Ändringar i OSGi-konfigurationer kan endast göras från Git via CI/CD-pipeline.

Webbkonsolen, som användes i tidigare versioner av AEM för att ändra OSGi-paket och -konfigurationer, är inte tillgänglig i AEM Cloud Service.

## Ändringar i publiceringsdatabasen tillåts inte {#changes-to-publish-repo}

Förutom ändringarna under `/home` på publiceringsnivån tillåts inte direkta ändringar i publiceringsdatabasen på AEM Cloud Service. I tidigare versioner av lokala AEM eller AEM på AMS kan kodändringar göras direkt till publiceringsdatabasen. Vissa begränsningar kan minskas på följande sätt:

* För innehåll- och innehållsbaserad konfiguration: gör ändringarna i författarinstansen och publicera dem.
* För kod och konfiguration: gör ändringarna i GIT-databasen och kör CI/CD-flödet för att köra dem.

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

## Borttagning av replikeringsagenter och relaterade ändringar {#replication-agents}

I AEM Cloud Service publiceras innehåll med [Distribution av säljinnehåll](https://sling.apache.org/documentation/bundles/content-distribution.html). Replikeringsagenterna som användes i tidigare versioner av AEM används inte längre eller tillhandahålls, vilket kan påverka följande områden i befintliga AEM projekt:

* Anpassade arbetsflöden som till exempel skickar innehåll till replikeringsagenter för förhandsgranskningsservrar.
* Anpassning till replikeringsagenter för att omvandla innehåll
* Använda omvänd replikering för att återföra innehåll från publicering till författaren

Observera dessutom att knapparna för att pausa och inaktivera har tagits bort från administrationskonsolen för replikeringsagenten.

## Borttagning av Classic UI {#classic-ui}

Det klassiska användargränssnittet är inte längre tillgängligt i AEM Cloud Service.

## Publish-side Delivery {#publish-side-delivery}

HTTP-acceleration inklusive CDN och trafikhantering för författare och publiceringstjänster tillhandahålls som standard i AEM Cloud Service.

För projektövergångar från AMS eller en lokal installation rekommenderar Adobe starkt att man utnyttjar det inbyggda CDN, eftersom funktionerna i AEM Cloud Service är optimerade för det CDN som tillhandahålls.

## Hantering och leverans av tillgångar {#asset-handling}

Överföring, bearbetning och nedladdning av mediefiler är optimerade i [!DNL Experience Manager Assets] som [!DNL Cloud Service]. [!DNL Assets] är nu mer effektivt, ger större skalbarhet och gör att du kan ladda upp och ned i mycket snabbare takt. Dessutom påverkas den befintliga anpassade koden och vissa åtgärder. För en lista över ändringar och för paritet med [!DNL Experience Manager] 6.5-funktioner, se [ändringar i [!DNL Assets]](/help/assets/assets-cloud-changes.md).
