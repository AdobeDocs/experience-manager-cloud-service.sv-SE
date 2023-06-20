---
title: ContextHub Diagnostics
description: ContextHub tillhandahåller en diagnostiksida där du kan se en översikt över ContextHub-ramverket
exl-id: c8d4e160-ea02-49f3-9e31-119445ef5a68
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# ContextHub Diagnostics {#contexthub-diagnostics}

ContextHub tillhandahåller en diagnostiksida där du kan se en översikt över ContextHub-ramverket. Öppna sidan genom att gå till `contexthub.diagnostics.html` sidan med AEM författarinstans, till exempel:

`http://<host>:<port>/conf/<site>/settings/cloudsettings/default/contexthub.diagnostics.html`

På sidan ContextHub Diagnostics (ContextHub-diagnostik) finns information om de butiker och gränssnittsmoduler som har skapats, vilka mappar i klientbiblioteket som har lästs in samt länkar till användbara sidor.

>[!NOTE]
>
>Felsökningsläget måste vara aktiverat för att diagnostikinformation ska kunna returneras, annars är diagnostiksidan tom. Se [det här dokumentet](configuring-contexthub.md#debugging-contexthub) om du vill ha mer information om hur du aktiverar felsökningsläget.

## Lager {#stores}

I avsnittet Lager visas alla ContextHub-butiker som har konfigurerats. Varje post i listan består av följande information:

* **Titel:** The [butikstyp](sample-stores.md) som butiken baseras på.
* **sökväg:** Sökvägen till databasnoden som innehåller konfigurationen.
* **resourceType:** Sökvägen till databasnoden där lagringstypen har definierats.
* **clientlibs:** Kategorierna för de klientbibliotek som läses in och som implementerar lagringstypen.

## Moduler {#modules}

I avsnittet Moduler visas alla ContextHub-gränssnittsmoduler som har konfigurerats. Varje post i listan består av följande information:

* **Titel:** The [Modultyp för användargränssnitt](sample-modules.md) som användargränssnittsmodulen baseras på.
* **sökväg:** Sökvägen till databasnoden som innehåller konfigurationen.
* **resourceType:** Sökvägen till databasnoden där gränssnittsmodultypen definieras.
* **clientlibs:** De kategorier av klientbiblioteken som är inlästa och som implementerar UI-modultypen.

## Clientlibs {#clientlibs}

I avsnittet Klientlibs visas alla [biblioteksmappar](/help/implementing/developing/introduction/clientlibs.md) som ContextHub har läst in. Klientbiblioteken kategoriseras enligt följande:

* **kernel.js:** Klientbibliotek som implementerar ContextHub-ramverket, segmentmotorn och lagringstyperna.
* **ui.js:** Klientbibliotek som implementerar gränssnittstyperna ContextHub och UI.
* **style.css:** CSS-filer som läses in från klientbibliotek.

## URL:er {#urls}

Avsnittet URL:er innehåller länkar till ContextHub-funktioner:

* **Konfigurationsredigerare:** Öppnar [Konfigurationssida för ContextHub](configuring-contexthub.md) där du kan konfigurera butiker, gränssnittslägen och gränssnittsmoduler.
* **Konfiguration av ContextHub-moduler:** Öppnar `/etc/cloudsettings/default/contexthub.config.kernel.js` -filen, som innehåller Javascript-objektrepresentationen av ContextHub-lagringskonfigurationerna.
* **Konfiguration av ContextHub-gränssnitt:** Öppnar `/etc/cloudsettings/default/contexthub.config.ui.js` -filen, som innehåller Javascript-objektrepresentationen av ContextHub-gränssnittskonfigurationerna.
* **kernel.js:** Öppnar `/etc/cloudsettings/default/contexthub.kernel.js` -filen, som innehåller källkoden för de klientbibliotek som implementerar ContextHub-ramverket, segmentmotorn och lagringstyperna.
* **ui.js:** Öppnar `/etc/cloudsettings/default/contexthub.ui.js` som innehåller källkoden för de klientbibliotek som implementerar gränssnittstyperna ContextHub och UI.
* **style.css:** Öppnar `/etc/cloudsettings/default/contexthub.styles.css` som innehåller CSS-formaten för ContextHub-gränssnittsmodulerna.
