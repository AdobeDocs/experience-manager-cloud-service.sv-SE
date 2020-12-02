---
title: ContextHub Diagnostics
description: ContextHub tillhandahåller en diagnostiksida där du kan se en översikt över ContextHub-ramverket
translation-type: tm+mt
source-git-commit: 1c518830f0bc9d9c7e6b11bebd6c0abd668ce040
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---


# ContextHub Diagnostics {#contexthub-diagnostics}

ContextHub tillhandahåller en diagnostiksida där du kan se en översikt över ContextHub-ramverket. Öppna sidan genom att gå till sidan `contexthub.diagnostics.html` i AEM författarinstans, till exempel:

`http://<host>:<port>/conf/<site>/settings/cloudsettings/default/contexthub.diagnostics.html`

På sidan ContextHub Diagnostics (ContextHub-diagnostik) finns information om de butiker och gränssnittsmoduler som har skapats, vilka mappar i klientbiblioteket som har lästs in samt länkar till användbara sidor.

>[!NOTE]
>
>Felsökningsläget måste vara aktiverat för att diagnostikinformation ska kunna returneras, annars är diagnostiksidan tom. Mer information om hur du aktiverar felsökningsläget finns i [det här dokumentet](configuring-contexthub.md#debugging-contexthub).

## Lagrar {#stores}

I avsnittet Lager visas alla ContextHub-butiker som har konfigurerats. Varje post i listan består av följande information:

* **Titel:** Den  [butikstyp ](sample-stores.md) som butiken baseras på.
* **sökväg:** Sökvägen till databasnoden som innehåller konfigurationen.
* **resourceType:** Sökvägen till databasnoden där lagringstypen definieras.
* **clientlibs:** De kategorier i klientbiblioteken som är inlästa och som implementerar lagringstypen.

## Moduler {#modules}

I avsnittet Moduler visas alla ContextHub-gränssnittsmoduler som har konfigurerats. Varje post i listan består av följande information:

* **Titel:** Den  [gränssnittsmodul-](sample-modules.md) typ som gränssnittsmodulen baseras på.
* **sökväg:** Sökvägen till databasnoden som innehåller konfigurationen.
* **resourceType:** Sökvägen till databasnoden där gränssnittsmodultypen definieras.
* **clientlibs:** De kategorier i klientbiblioteken som är inlästa som implementerar gränssnittsmodultypen.

## Clientlibs {#clientlibs}

I Clientlibs-avsnittet visas alla [klientbiblioteksmappar](/help/implementing/developing/introduction/clientlibs.md) som ContextHub har läst in. Klientbiblioteken kategoriseras enligt följande:

* **kernel.js:** Klientbibliotek som implementerar ContextHub-ramverket, segmentmotorn och lagringstyperna.
* **ui.js:** Klientbibliotek som implementerar gränssnittstyperna ContextHub och UI.
* **style.css:** CSS-filer som läses in från klientbibliotek.

## URL:er {#urls}

Avsnittet URL:er innehåller länkar till ContextHub-funktioner:

* **Konfigurationsredigerare:** Öppnar  [konfigurationssidan för ContextHub, där du kan ](configuring-contexthub.md) konfigurera arkiv, gränssnittslägen och gränssnittsmoduler.
* **Konfiguration av ContextHub-moduler:** Öppnar  `/etc/cloudsettings/default/contexthub.config.kernel.js` filen som innehåller JavaScript-objektrepresentationen av ContextHub-lagringskonfigurationerna.
* **Konfiguration av ContextHub-gränssnitt:** Öppnar  `/etc/cloudsettings/default/contexthub.config.ui.js` filen som innehåller JavaScript-objektrepresentationen av ContextHub-gränssnittskonfigurationerna.
* **kernel.js:** Öppnar  `/etc/cloudsettings/default/contexthub.kernel.js` filen som innehåller källkoden för klientbiblioteken som implementerar ContextHub-ramverket, segmentmotorn och lagertyperna.
* **ui.js:** Öppnar  `/etc/cloudsettings/default/contexthub.ui.js` filen som innehåller källkoden för klientbiblioteken som implementerar gränssnitts- och gränssnittsmodultyperna för ContextHub.
* **style.css:** Öppnar  `/etc/cloudsettings/default/contexthub.styles.css` filen som innehåller CSS-formaten för ContextHub-gränssnittsmodulerna och UI.
