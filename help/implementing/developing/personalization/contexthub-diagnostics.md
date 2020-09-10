---
title: ContextHub Diagnostics
description: ContextHub tillhandahåller en diagnostiksida där du kan se en översikt över ContextHub-ramverket
translation-type: tm+mt
source-git-commit: e361f24b943eff68982a37ac0dc2597f92450026
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---


# ContextHub Diagnostics {#contexthub-diagnostics}

ContextHub tillhandahåller en diagnostiksida där du kan se en översikt över ContextHub-ramverket. Om du vill öppna sidan går du till `contexthub.diagnostics.html` sidan med AEM författarinstans, till exempel:

`http://<host>:<port>/conf/<site>/settings/cloudsettings/default/contexthub.diagnostics.html`

På sidan ContextHub Diagnostics (ContextHub-diagnostik) finns information om de butiker och gränssnittsmoduler som har skapats, vilka mappar i klientbiblioteket som har lästs in samt länkar till användbara sidor.

>[!NOTE]
>
>Felsökningsläget måste vara aktiverat för att diagnostikinformation ska kunna returneras, annars är diagnostiksidan tom. I [det här dokumentet](configuring-contexthub.md#debugging-contexthub) finns mer information om hur du aktiverar felsökningsläget.

## Lager {#stores}

I avsnittet Lager visas alla ContextHub-butiker som har konfigurerats. Varje post i listan består av följande information:

* **Titel:** Den [butikstyp](sample-stores.md) som butiken baseras på.
* **sökväg:** Sökvägen till databasnoden som innehåller konfigurationen.
* **resourceType:** Sökvägen till databasnoden där lagringstypen har definierats.
* **clientlibs:** Kategorierna för de klientbibliotek som läses in och som implementerar lagringstypen.

## Moduler {#modules}

I avsnittet Moduler visas alla ContextHub-gränssnittsmoduler som har konfigurerats. Varje post i listan består av följande information:

* **Titel:** Den [UI-modultyp](sample-modules.md) som UI-modulen baseras på.
* **sökväg:** Sökvägen till databasnoden som innehåller konfigurationen.
* **resourceType:** Sökvägen till databasnoden där gränssnittsmodultypen definieras.
* **clientlibs:** De kategorier av klientbiblioteken som är inlästa och som implementerar UI-modultypen.

## Clientlibs {#clientlibs}

I Clientlibs-avsnittet visas alla klientbiblioteksmappar som ContextHub har läst in. Klientbiblioteken kategoriseras enligt följande:

* **kernel.js:** Klientbibliotek som implementerar ContextHub-ramverket, segmentmotorn och lagringstyperna.
* **ui.js:** Klientbibliotek som implementerar gränssnittstyperna ContextHub och UI.
* **style.css:** CSS-filer som läses in från klientbibliotek.

## URL:er {#urls}

Avsnittet URL:er innehåller länkar till ContextHub-funktioner:

* **Konfigurationsredigerare:** Öppnar [ContextHub Configuration-sidan](configuring-contexthub.md) där du kan konfigurera butiker, gränssnittslägen och gränssnittsmoduler.
* **Konfiguration av ContextHub-moduler:** Öppnar `/etc/cloudsettings/default/contexthub.config.kernel.js` filen som innehåller Javascript-objektrepresentationen av ContextHub-lagringskonfigurationerna.
* **Konfiguration av ContextHub-gränssnitt:** Öppnar `/etc/cloudsettings/default/contexthub.config.ui.js` filen som innehåller Javascript-objektrepresentationen av ContextHub-gränssnittskonfigurationerna.
* **kernel.js:** Öppnar `/etc/cloudsettings/default/contexthub.kernel.js` filen, som innehåller källkoden för klientbiblioteken som implementerar ContextHub-ramverket, segmentmotorn och lagringstyperna.
* **ui.js:** Öppnar `/etc/cloudsettings/default/contexthub.ui.js` filen, som innehåller källkoden för klientbiblioteken som implementerar gränssnittstyperna för ContextHub och UI.
* **style.css:** Öppnar `/etc/cloudsettings/default/contexthub.styles.css` filen som innehåller CSS-formaten för ContextHub-gränssnittsmodulerna och UI.
