---
title: SPA-modellroutning
description: För enkelsidiga program i AEM ansvarar appen för routningen. I det här dokumentet beskrivs routningsmekanismen, kontraktet och tillgängliga alternativ.
exl-id: 1186b64e-11f8-43a6-bc75-450c4d7587ec
feature: Developing
role: Admin, Architect, Developer
index: false
source-git-commit: 7a9d947761b0473f5ddac3c4d19dfe5bed5b97fe
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---


# SPA-modellroutning{#spa-model-routing}

För enkelsidiga program i AEM ansvarar appen för routningen. I det här dokumentet beskrivs routningsmekanismen, kontraktet och tillgängliga alternativ.

{{ue-over-spa}}

## Projektdirigering {#project-routing}

Appen äger routningen och implementeras sedan av projektutvecklarna. I det här dokumentet beskrivs routningen som är specifik för den modell som returneras av AEM-servern. Sidmodellens datastruktur visar den underliggande resursens URL. Det främsta projektet kan använda vilket anpassat bibliotek eller tredjepartsbibliotek som helst som tillhandahåller routningsfunktioner. När en väg förväntar sig ett fragment av modellen kan ett anrop till funktionen `PageModelManager.getData()` göras. När en modellväg har ändrats måste en händelse aktiveras för att varna avlyssningsbibliotek som t.ex. Page Editor.

## Arkitektur {#architecture}

En detaljerad beskrivning finns i avsnittet [PageModelManager](blueprint.md#pagemodelmanager) i SPA-designdokumentet.

## ModelRouter {#modelrouter}

`ModelRouter` - när den är aktiverad - kapslar in API-funktionerna `pushState` och `replaceState` i HTML5 för historik för att garantera att ett visst modellfragment är förhämtat och tillgängligt. Därefter meddelas den registrerade frontkomponenten om att modellen har ändrats.

## Manuell kontra automatisk modellroutning {#manual-vs-automatic-model-routing}

`ModelRouter` automatiserar hämtning av fragment av modellen. Men som alla automatiserade verktyg har de begränsningar som behövs. Vid behov kan `ModelRouter` inaktiveras eller konfigureras för att ignorera sökvägar med hjälp av metaegenskaper (se avsnittet Metaegenskaper i [ SPA Page Component ](page-component.md) -dokumentet). Utvecklare på klientsidan kan sedan implementera sitt eget modellroutningslager genom att begära att `PageModelManager` läser in ett givet fragment av modellen med funktionen `getData()`.

>[!CAUTION]
>
>Den aktuella versionen av `ModelRouter` stöder endast användning av URL:er som pekar mot den faktiska resurssökvägen för Sling Model-startpunkter. Det stöder inte användning av Vanity-URL:er eller alias.

## Routningskontrakt {#routing-contract}

Den aktuella implementeringen baseras på antagandet att SPA-projektet använder historik-API:t HTML5 för routning till de olika programsidorna.

### Konfiguration {#configuration}

`ModelRouter` stöder begreppet modellroutning när det lyssnar efter `pushState` - och `replaceState` -anrop för att hämta modellfragment i förväg. Internt aktiveras `PageModelManager` för att läsa in modellen som motsvarar en angiven URL och en `cq-pagemodel-route-changed` -händelse som andra moduler kan lyssna på utlöses.

Som standard aktiveras det här beteendet automatiskt. Om du vill inaktivera den bör SPA återge följande metaegenskap:

```
<meta property="cq:pagemodel_router" content="disabled"\>
```

Varje väg i SPA ska motsvara en tillgänglig resurs i AEM (till exempel `/content/mysite/mypage"`) eftersom `PageModelManager` automatiskt försöker läsa in motsvarande sidmodell när flödet har valts. Även om det behövs kan SPA även definiera ett &quot;blockeringslista&quot; av vägar som ska ignoreras av `PageModelManager`:

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
