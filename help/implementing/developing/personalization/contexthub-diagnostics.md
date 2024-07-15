---
title: ContextHub Diagnostics
description: ContextHub tillhandahåller en diagnostiksida där du kan se en översikt över ContextHub-ramverket
exl-id: c8d4e160-ea02-49f3-9e31-119445ef5a68
feature: Developing, Personalization
role: Admin, Architect, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 0%

---

# ContextHub Diagnostics {#contexthub-diagnostics}

ContextHub tillhandahåller en diagnostiksida där du kan se en översikt över ContextHub-ramverket. Öppna sidan genom att gå till sidan `contexthub.diagnostics.html` i AEM författarinstans, till exempel:

`http://<host>:<port>/conf/<site>/settings/cloudsettings/default/contexthub.diagnostics.html`

På sidan ContextHub Diagnostics (ContextHub-diagnostik) finns information om de butiker och gränssnittsmoduler som har skapats, vilka mappar i klientbiblioteket som har lästs in samt länkar till användbara sidor.

>[!NOTE]
>
>Felsökningsläget måste vara aktiverat för att diagnostikinformation ska kunna returneras, annars är diagnostiksidan tom. Mer information om hur du aktiverar felsökningsläget finns i [det här dokumentet](configuring-contexthub.md#debugging-contexthub).

## Lager {#stores}

I avsnittet Lager visas alla ContextHub-butiker som har konfigurerats. Varje post i listan består av följande information:

* **Titel:** [Butikstypen](sample-stores.md) som butiken baseras på.
* **sökväg:** Sökvägen till databasnoden som innehåller konfigurationen.
* **resourceType:** Sökvägen till databasnoden där lagringstypen definieras.
* **clientlibs:** De kategorier i klientbiblioteken som är inlästa och som implementerar lagringstypen.

## Moduler {#modules}

I avsnittet Moduler visas alla ContextHub-gränssnittsmoduler som har konfigurerats. Varje post i listan består av följande information:

* **Titel:** Den [UI-modultyp](sample-modules.md) som UI-modulen baseras på.
* **sökväg:** Sökvägen till databasnoden som innehåller konfigurationen.
* **resourceType:** Sökvägen till databasnoden där gränssnittsmodultypen definieras.
* **clientlibs:** Kategorierna för klientbiblioteken som är inlästa och som implementerar UI-modultypen.

## Clientlibs {#clientlibs}

I Clientlibs-avsnittet visas alla t[klientbiblioteksmappar](/help/implementing/developing/introduction/clientlibs.md) som ContextHub har läst in. Klientbiblioteken kategoriseras enligt följande:

* **kernel.js:** Klientbibliotek som implementerar ContextHub-ramverket, segmentmotorn och lagringstyperna.
* **ui.js:** Klientbibliotek som implementerar gränssnittstyperna ContextHub och UI.
* **style.css:** CSS-filer som läses in från klientbibliotek.

## URL:er {#urls}

Avsnittet URL:er innehåller länkar till ContextHub-funktioner:

* **Konfigurationsredigeraren:** Öppnar [konfigurationssidan för ContextHub](configuring-contexthub.md) där du kan konfigurera arkiv, gränssnittslägen och gränssnittsmoduler.
* **Konfiguration av ContextHub-moduler:** Öppnar filen `/etc/cloudsettings/default/contexthub.config.kernel.js` som innehåller JavaScript-objektrepresentationen av ContextHub-lagringskonfigurationerna.
* **Konfiguration av ContextHub-gränssnitt:** Öppnar filen `/etc/cloudsettings/default/contexthub.config.ui.js` som innehåller JavaScript-objektrepresentationen av ContextHub-gränssnittskonfigurationerna.
* **kernel.js:** Öppnar filen `/etc/cloudsettings/default/contexthub.kernel.js` som innehåller källkoden för de klientbibliotek som implementerar ContextHub-ramverket, segmentmotorn och lagringstyperna.
* **ui.js:** Öppnar filen `/etc/cloudsettings/default/contexthub.ui.js` som innehåller källkoden för de klientbibliotek som implementerar gränssnittstyperna ContextHub och UI.
* **style.css:** Öppnar filen `/etc/cloudsettings/default/contexthub.styles.css` som innehåller CSS-formaten för ContextHub-gränssnittsmodulerna och UI.
