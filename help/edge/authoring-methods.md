---
title: Välja en redigeringsmetod
description: Lär dig viktiga saker när du bestämmer hur du ska skapa ditt innehåll i AEM så att du kan fatta det bästa beslutet för dina innehållsförfattare.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: a75e7051-e5ec-4d2a-848a-a66989e2f30b
index: false
hide: true
hidefromtoc: true
source-git-commit: e57610e4c5e498ddfdbaa0ba39c9197ecfb5d177
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---

# Välja en redigeringsmetod {#authoring-methods}

Lär dig viktiga saker när du bestämmer hur du ska skapa ditt innehåll i AEM så att du kan fatta det bästa beslutet för dina innehållsförfattare.

## Översikt över överväganden {#overview}

AEM flexibla hantering säkerställer att alla redigeringsbehov täcks oavsett om du väljer dokumentbaserad redigering eller WYSIWYG-redigering. Tänk på följande när du börjar.

* **Involvera alltid innehållsförfattarna i beslutet.** - Dina innehållsförfattare är dina experter och deras insikter är viktiga.
* **Flera redigeringsmetoder kan implementeras.** - Även om Adobe rekommenderar att du börjar med enkel och komplex lagerhantering vid behov, kan flera redigeringsmetoder fungera tillsammans i ett projekt.
* **Du kan alltid ändra redigeringsmetod efter hand.** - Oavsett vad du bestämmer dig för är du inte låst. Att byta från en metod till en annan är enkelt med hjälp av Adobe automatiska migreringsverktyg.
* **Du får inte bestämma dig före implementeringen, utan som en del av implementeringen.** - AEM är en enhetlig produkt, så detta viktiga beslut behöver inte ingå i avtalsförhandlingarna. När du köper AEM får du alla. Detta är snarare ett beslut under genomförandet.

Adobe kan hjälpa dig att avgöra vilken metod (eller vilka metoder) som bäst passar dina behov som en del av implementeringen.

## En storlek passar inte alla {#one-size}

Alla implementeringar av AEM har sina egna arbetsflöden och mål. Ett projekt kan omfatta en enkel redigeringsmodell med innehållsförfattare som ansvarar för sina egna publikationer. En annan kan ha ett komplext nätverk av medverkande och godkännanden.

![Olika redigeringsarbetsflöden](assets/authoring-workflows.png)

Olika projekt kan ha olika (och flera) användningsområden.

![Användningsexempel](assets/use-cases.png)

Adobe förstår detta och erbjuder därför inte en lösning som passar alla. AEM är den enda lösning som erbjuder olika strategier för innehållsleverans och innehållsframtagning efter dina behov.

För att fastställa det bästa tillvägagångssättet måste du överväga fyra alternativ.

1. [Har du en inställning för innehållsleverans?](#content-delivery)
1. [Har du någon inställning för innehållsredigering?](#content-authoring)
1. [Vad har du för projektmål?](#project-goals)
1. [Vilka redigeringsutmaningar står du inför idag?](#authoring-challenges)

## Inställningar för innehållsleverans {#content-delivery}

Det första du bör tänka på är hur du vill leverera ditt innehåll. Edge Delivery Services erbjuder blixtsnabba sajter, men du kanske fokuserar på headless-leverans. Följande beslutsträd kan hjälpa dig att överväga dina alternativ.

![Beslutsträd för innehållsleverans](assets/content-delivery-decision-tree.png)

Detta kan hjälpa dig att avgöra om du behöver:

* [AEM som headless CMS](/help/headless/introduction.md) med Content Fragment Editor och/eller Universal Editor.
* AEM Edge Delivery Services med [dokumentbaserad redigering](/help/edge/docs/authoring.md) eller [WYSIWYG med den universella redigeraren](/help/edge/wysiwyg-authoring/authoring.md).

## Inställningar för innehållsredigering {#content-authoring}

Du bör tänka på hur du vill skapa ditt innehåll. Följande beslutsträd kan hjälpa dig att överväga dina alternativ.

![Beslutsträd för innehållsredigering](assets/content-authoring-decision-tree.png)

Detta kan hjälpa dig att avgöra om du behöver:

* AEM Edge Delivery Services med den [dokumentbaserade redigeringen](/help/edge/docs/authoring.md).
* [WYSIWYG-redigering med Universal Editor](/help/edge/wysiwyg-authoring/authoring.md).

## Projektmål {#project-goals}

Hur ser framgångarna ut för dig? Hur definierar man framgången för projektet?

* Du kanske behöver kunna ge fler personer möjlighet att skapa innehåll, men du vill undvika utbildning i en ny verktygsuppsättning. (Tänk dokumentbaserad redigering.)
* Du kanske behöver öka mängden innehåll du genererar. (Tänk dokumentbaserad redigering.)
* Du kanske behöver fokusera på den visuella innehållslayouten, men minimera behovet av att kunna koda. (Tänk dig WYSIWYG.)

Tydliga projektmål i början av implementeringen hjälper er att fatta ett välgrundat beslut om er utvecklingsmetod.

## Redigeringsproblem {#authoring-challenges}

Ta till sist hänsyn till de specifika utmaningar du står inför idag när du skapar ditt innehåll.

* Du kanske råkar ut för duplicerat arbete med innehåll som skapats utanför CMS, som sedan måste importeras eller kopieras och klistras in. (Tänk dokumentbaserad redigering.)
* Du kanske behöver korta ned tiden för skribenter i utbildning om hur man använder CMS. (Tänk dokumentbaserad redigering.)
* Dina författare kanske ofta behöver redigera den visuella layouten för ditt innehåll, vilket kräver konstant utvecklarstöd. (Tänk dig WYSIWYG.)
