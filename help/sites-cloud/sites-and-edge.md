---
title: AEM Sites och Edge Delivery Services
description: Förstå hur Edge Delivery Services utvidgar redigerings- och publiceringsmöjligheterna för AEM Sites för att snabba upp framtagningen av innehåll och leverera webbplatser med 100 % prestanda.
solution: Experience Manager Sites
feature: Authoring
role: User
exl-id: 7747d6f7-18e4-4713-baea-bcfa94f54934
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '618'
ht-degree: 0%

---

# AEM Sites och Edge Delivery Services {#sites-and-edge}

Förstå hur Edge Delivery Services utvidgar redigerings- och publiceringsmöjligheterna för AEM Sites för att snabba upp framtagningen av innehåll och leverera webbplatser med 100 % prestanda.

## Ökning {#overview}

Förutom all den kraft och alla funktioner i [AEM Sites as a Cloud Service](/help/sites-cloud/sites-cloud-changes.md) har som en del av den molnbaserade AEM as a Cloud Service-plattformen, har Edge Delivery Servicens ytterligare redigerings- och publiceringsmöjligheter som snabbar upp framtagningen av innehåll och levererar webbplatser med 100 % prestanda.

## Vad är Edge Delivery Services? {#what-is-edge}

Edge Delivery Servicens levererar exceptionella upplevelser som skapar engagemang och konverteringar genom att leverera slagkraftiga upplevelser som är snabba att skapa och utveckla. Det är en sammanslagen uppsättning tjänster som möjliggör en snabb utvecklingsmiljö där författare snabbt kan uppdatera och publicera och nya webbplatser snabbt lanseras. Läs mer om Edge Delivery Services i dokumentet [Översikt över Edge Delivery Services](/help/edge/overview.md).

Med Edge Delivery Services och AEM Sites as a Cloud Service kan dina projekt dra nytta av följande:

* [En ny utvecklarupplevelse](#developer-experience)
* [Ett nytt publiceringsskikt](#publish-tier)
* [Fler redigeringsalternativ](#authoring-options)

## En ny utvecklarupplevelse {#developer-experience}

En huvudfilosofi för Edge Delivery Services är *snabbhet*. Detta börjar med utvecklarupplevelsen. Om utvecklarna:

* Förstå Git-grunderna och
* Förstå grunderna i HTML, CSS och JavaScript

De kan snabbt anpassa sina egna projekt och komponenter för Edge Delivery Services på mindre än trettio minuter. Börja med att klona vårt standardprojekt på GitHub och genomför sedan bara ändringarna. Din anpassning är direkt tillgänglig!

Se dokumentet [Komma igång - Självstudiekurs för utvecklare](https://www.aem.live/developer/tutorial) om du vill veta mer om hur du utvecklar för Edge Delivery Services.

## En ny Publish-nivå {#publish-tier}

Utvecklingstiden minskar inte bara dramatiskt, utan Edge Delivery Servicens ger också blixtsnabba webbplatser.

## Ytterligare redigeringsalternativ {#authoring-options}

Edge Delivery Services gör det också snabbare att skapa innehåll genom nya redigeringsalternativ.

### Universell redigerare {#universal-editor}

Universell redigerare erbjuder en smidig redigeringsfunktion för vad-du-se-is-what-you-get (WYSIWYG) som kan användas för att skapa vilket innehåll som helst.

Läs dokumentet [WYSIWYG Content Authoring for Edge Delivery Services](/help/edge/wysiwyg-authoring/authoring.md) om du vill veta mer om hur du skapar innehåll med den universella redigeraren.

### Dokumentbaserad redigering {#document-authoring}

Med dokumentbaserad redigering kan vem som helst skapa innehåll utan någon utbildning genom att utnyttja verktyg som alla känner till: Word och Google Docs. Med dessa enkla verktyg kan Edge Delivery Servicens direkt omvandla ett Word-dokument till uppdaterat innehåll på den publicerade webbplatsen.

Mer information om hur du använder dokumentbaserad redigering finns i dokumentet [Redigering och publicering av innehåll](https://www.aem.live/docs/authoring).

## Har Edge rätt för dig? {#decision}

Adobe har sett sina kunder och deras intressenter dra stor nytta av Edge Delivery Services i projekt av alla storlekar. Därför rekommenderar Adobe att du drar nytta av Edge Delivery Services som utgångspunkt för alla nya projekt.

Det går också att distribuera en delmängd av webbplatser eller sidor på Edge Delivery medan resten ligger i den aktuella stacken. Detta rekommenderas när prestanda, organisk trafik, kundengagemang, utvecklare eller innehållshastighet behöver förbättras.

Kontakta din Adobe-representant om du inte är säker på om Edge Delivery passar dig.

### Edge Delivery och Headless då? (#headless)

Edge Delivery är ett prestandaförsprång som är fristående från serverdelen. Om du har ett anpassat huvud som React SPA rekommenderar Adobe det AEM headless-integreringsmönstret. Mer information finns i [AEM Headless-dokumentationen](/help/headless/introduction.md).

Adobe rekommenderar dock att du använder Edge Delivery som standardhuvud för att dra nytta av dess snabbhet och prestanda och för att integrera den headless delen av projektet (vanligtvis affärsapplikationen) med en headlessstrategi (t.ex. Reagera eller SPA).
