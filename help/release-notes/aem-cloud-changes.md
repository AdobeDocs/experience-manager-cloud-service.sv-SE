---
title: Betydande ändringar av Adobe Experience Manager (AEM) as a Cloud Service
description: Observerbara ändringar av Adobe Experience Manager (AEM) as a Cloud Service.
exl-id: fe11d779-66cd-45aa-aa6b-c819b88d2405
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '868'
ht-degree: 7%

---

# Betydande förändringar av Adobe Experience Manager as a Cloud Service {#notable-changes-aem-cloud}

Adobe Experience Manager (AEM) Cloud Service innehåller många nya funktioner och möjligheter för att hantera dina AEM projekt. Det finns dock vissa skillnader mellan AEM Sites på plats eller i Adobe Managed Service jämfört med AEM Cloud Service. I det här dokumentet markeras de viktiga skillnaderna.

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

* [Anpassade körningslägen tillåts inte](#custom-runmodes)

* [Borttagning av replikeringsagenter och relaterade ändringar](#replication-agents)

* [Borttagning av Classic UI](#classic-ui)

* [Publish-side Delivery](#publish-side-delivery)

* [Hantering och leverans av tillgångar](#asset-handling)

## /apps och /libs kan inte ändras under körning {#apps-libs-immutable}

Allt innehåll och alla undermappar i `/apps` och `/libs` är skrivskyddad. Funktioner eller anpassad kod som förväntar sig att göra ändringar där misslyckas. Ett fel returneras som anger att sådant innehåll är skrivskyddat och att skrivåtgärden inte kunde slutföras. Detta påverkar på flera AEM områden:

* Inga ändringar i `/libs` tillåts överhuvudtaget.
   * Detta är inte en ny regel, men den har inte införts i tidigare lokala versioner av AEM.
* Övertäckningar för områden i `/libs` som fortfarande får användas inom `/apps`.
   * Sådana övertäckningar måste komma från Git via CI/CD-ledningen.
* Designinformation för statiska mallar som lagras i `/apps` kan inte redigeras via gränssnittet.
   * Du bör använda Redigerbara mallar i stället.
   * Om statiska mallar fortfarande krävs måste konfigurationsinformationen komma från Git via CI/CD-flödet.
* MSM Blueprint och anpassade MSM roll-out-konfigurationer måste installeras från Git via CI/CD-pipeline.
* I18n-översättningsändringar måste komma från Git via CI/CD-flödet.

## OSGi-paket och -konfigurationer måste behandlas som kod {#osgi}

Ändringar av OSGi-paket och -konfigurationer måste införas via CI/CD-pipeline.

* Nya eller uppdaterade OSGi-paket måste introduceras via Git via CI/CD-pipeline.
* Ändringar i OSGi-konfigurationer kan bara komma från Git via CI/CD-pipeline.

Webbkonsolen, som användes i tidigare versioner av AEM för att ändra OSGi-paket och -konfigurationer, är inte tillgänglig i AEM Cloud Service.

## Ändringar i publiceringsdatabasen tillåts inte {#changes-to-publish-repo}

Förutom ändringarna under `/home` på publiceringsnivån tillåts inte direkta ändringar i publiceringsdatabasen på AEM Cloud Service. I tidigare versioner av lokala AEM eller AEM på AMS kan kodändringar göras direkt till publiceringsdatabasen. Vissa begränsningar kan minskas på följande sätt:

* För innehåll och innehållsbaserad konfiguration: gör ändringarna i Author-instansen och publicera dem.
* För kod och konfiguration: gör ändringarna i GIT-databasen och kör CI/CD-flödet för att implementera dem.

## Anpassade körningslägen tillåts inte {#custom-runmodes}

Ytterligare eller anpassade körningslägen är inte möjliga i AEM Cloud Service. En lista över körningslägen som finns för AEM Cloud Service finns i [Distribuera till AEM as a Cloud Service](/help/implementing/deploying/overview.md#runmodes).

## Borttagning av replikeringsagenter och relaterade ändringar {#replication-agents}

I AEM Cloud Service publiceras innehåll med [Distribution av säljinnehåll](https://sling.apache.org/documentation/bundles/content-distribution.html). Replikeringsagenterna som användes i tidigare versioner av AEM används inte längre eller tillhandahålls, vilket kan påverka följande områden i befintliga AEM projekt:

* Anpassade arbetsflöden som till exempel skickar innehåll till replikeringsagenter för förhandsgranskningsservrar.
* Anpassning till replikeringsagenter för att omvandla innehåll.
* Använda omvänd replikering för att återföra innehåll från publicering till författaren.

Dessutom tas knapparna för paus och inaktivering bort från administrationskonsolen för replikeringsagenten.

## Borttagning av Classic UI {#classic-ui}

Det klassiska användargränssnittet är inte längre tillgängligt i AEM Cloud Service.

## Publish-side Delivery {#publish-side-delivery}

HTTP-acceleration inklusive CDN och trafikhantering för författar- och publiceringstjänster tillhandahålls som standard i AEM Cloud Service.

För projekt som går över från AMS eller en lokal installation rekommenderar Adobe starkt att du använder det inbyggda CDN, eftersom funktionerna i AEM Cloud Service är optimerade för det CDN som tillhandahålls.

## Hantering och leverans av tillgångar {#asset-handling}

Överföring, bearbetning och nedladdning av mediefiler är optimerade i [!DNL Experience Manager Assets] som [!DNL Cloud Service]. AEM [!DNL Assets] är nu mer effektivt, ger större skalbarhet och gör att du kan ladda upp och ned snabbare. Dessutom påverkas den befintliga anpassade koden och vissa åtgärder. För en lista över ändringar och för paritet med [!DNL Experience Manager] 6.5-funktioner, se [ändringar i [!DNL Assets]](/help/assets/assets-cloud-changes.md).
