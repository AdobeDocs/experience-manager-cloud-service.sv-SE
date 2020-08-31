---
title: SPA-modellroutning
description: För enkelsidiga program i AEM ansvarar appen för routningen. I det här dokumentet beskrivs routningsmekanismen, kontraktet och tillgängliga alternativ.
translation-type: tm+mt
source-git-commit: c075bcc415b68ba0deaeca61d6d179bd7263ca5f
workflow-type: tm+mt
source-wordcount: '441'
ht-degree: 0%

---


# SPA-modellroutning{#spa-model-routing}

För enkelsidiga program i AEM ansvarar appen för routningen. I det här dokumentet beskrivs routningsmekanismen, kontraktet och tillgängliga alternativ.

## Projektdirigering {#project-routing}

Appen äger routningen och implementeras sedan av projektutvecklarna. Det här dokumentet beskriver routningen som är specifik för den modell som returneras av AEM. Sidmodellens datastruktur visar den underliggande resursens URL. Det främsta projektet kan använda vilket anpassat bibliotek eller tredjepartsbibliotek som helst som tillhandahåller routningsfunktioner. När en väg förväntar sig ett fragment av modellen kan ett anrop till `PageModelManager.getData()` funktionen göras. När en modellväg har ändrats måste en händelse aktiveras för att varna avlyssningsbibliotek som t.ex. Page Editor.

## Arkitektur {#architecture}

En detaljerad beskrivning finns i avsnittet [PageModelManager](blueprint.md#pagemodelmanager) i SPA-designdokumentet.

## ModelRouter {#modelrouter}

När `ModelRouter` det här alternativet är aktiverat kapslar det in API-funktioner för HTML5-historik `pushState` och `replaceState` för att garantera att ett visst modellfragment är förhämtat och tillgängligt. Därefter meddelas den registrerade frontkomponenten om att modellen har ändrats.

## Manuell kontra automatisk modellroutning {#manual-vs-automatic-model-routing}

Funktionen `ModelRouter` automatiserar hämtning av fragment av modellen. Men som alla automatiserade verktyg har de begränsningar. Vid behov `ModelRouter` kan sökvägarna inaktiveras eller konfigureras så att de ignoreras med metaegenskaper (se avsnittet Metaegenskaper i [SPA Page Component](page-component.md) -dokumentet). Utvecklare kan sedan implementera sitt eget modellroutningslager genom att begära `PageModelManager` att ett visst fragment av modellen ska läsas in med `getData()` funktionen.

>[!CAUTION]
>
>Den aktuella versionen av det `ModelRouter` enda stödet för användning av URL:er som pekar på den faktiska resurssökvägen för Sling Model-startpunkter. Det stöder inte användning av Vanity-URL:er eller alias.

## Routningskontrakt {#routing-contract}

Den aktuella implementeringen baseras på antagandet att SPA-projektet använder API:t för HTML5-historik för routning till de olika programsidorna.

### Konfiguration {#configuration}

Den `ModelRouter` stöder begreppet modellroutning när den lyssnar efter `pushState` och `replaceState` anropar för att hämta modellfragment i förväg. Internt aktiveras en funktion för `PageModelManager` att läsa in den modell som motsvarar en viss URL och utlöser en `cq-pagemodel-route-changed` händelse som andra moduler kan lyssna på.

Som standard aktiveras det här beteendet automatiskt. Om du vill inaktivera den bör SPA återge följande metaegenskap:

```
<meta property="cq:pagemodel_router" content="disable"\>
```

Observera att alla vägar i SPA bör motsvara en tillgänglig resurs i AEM (t.ex. &quot; `/content/mysite/mypage"`) eftersom `PageModelManager` automatiskt försöker läsa in motsvarande sidmodell när flödet har valts. Även om det vid behov kan SPA även definiera ett &quot;blockeringslista&quot; på rutter som ska ignoreras av `PageModelManager`följande:

```
<meta property="cq:pagemodel_route_filters" content="route/not/found,^(.*)(?:exclude/path)(.*)"/>
```
