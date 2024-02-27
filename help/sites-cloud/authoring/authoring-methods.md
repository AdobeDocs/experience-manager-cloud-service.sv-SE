---
title: Metoder för att skapa innehåll i AEM
description: Lär dig olika sätt att skapa innehåll i AEM och hur de skiljer sig åt.
feature: Authoring
source-git-commit: 85b99fc0b0eb20b24f27d06159a52d4339a3c962
workflow-type: tm+mt
source-wordcount: '554'
ht-degree: 0%

---


# Metoder för att skapa innehåll i AEM {#authoring-methods}

Lär dig olika sätt att skapa innehåll i AEM, hur de skiljer sig åt och när du kan använda det ena över det andra.

## Flexibilitet för AEM {#authoring-flexibility}

AEM as a Cloud Service har flera olika redigerare för att redigera olika typer av innehåll och stöder olika redigeringssituationer.

* [AEM Page Editor](#page-editor) - Detta är den klassiska redigeraren för framtagning av innehåll i AEM, som har testats och är betrodd för tusentals eller tusentals webbplatser.
* [AEM Content Fragment Editor](#cf-editor) - Det här är det självklara valet för att skapa headless-innehåll.
* [Universal Editor](#universal-editor) - Med det här moderna användargränssnittet kan du skapa AEM på ett innehållsmedvetet sätt och det är det första alternativet för AEM projekt som utnyttjar Edge Delivery Services.
* [Dokumentbaserad redigering](#document-based) - Om du använder Edge Delivery-tjänster kan du välja att redigera ditt innehåll som vanliga dokument som Microsoft Word eller Google Docs helt utanför AEM.

På grund av AEM integrerade och skalbara natur kan dessa metoder användas exklusivt eller i kombination med varandra beroende på projektets behov.

Kontakta systemadministratören eller projektledaren om du är osäker på vilka redigeringsalternativ som är tillgängliga för dig eller om du vill utforska nya alternativ för att skapa ditt innehåll.

## AEM Page Editor {#page-editor}

Det här är den klassiska redigeraren för att skapa innehåll i AEM, som har testats och registrerats som pålitligt för tusentals eller tusentals webbplatser.

![AEM](assets/authoring-methods-page-editor.png)

Den AEM sidredigeraren innehåller en integrerad miljö för att skapa innehåll med hjälp av ett WYSIWYG-gränssnitt (what-you-see-is-what-you-get). Dra-och-släpp fördefinierade komponenter för att skapa sidan och redigera innehållet på plats.

Mer information om AEM finns i dokumentet [AEM sidredigeraren.](/help/sites-cloud/authoring/page-editor/introduction.md)

## AEM Content Fragment Editor {#cf-editor}

AEM Content Fragment Editor är den självklara redigeraren för att skapa rubrikfritt innehåll.

![AEM Content Fragment Editor](assets/authoring-methods-cf-editor.png)

AEM Content Fragment Editor har ett tydligt gränssnitt för att skapa och hantera strukturerat innehåll, idealiskt för headless-leverans.

Mer information om AEM Content Fragment Editor finns i dokumenten [Hantera innehållsfragment](/help/sites-cloud/administering/content-fragments/managing.md) och [Skapa innehållsfragment](/help/sites-cloud/administering/content-fragments/managing.md).

>[!NOTE]
>
>The *new* Redigeraren som markeras i det här avsnittet är endast tillgänglig på Adobe Experience Manager-as a Cloud Service (AEM) online.
>
>The [*original* Innehållsfragmentsredigerare](/help/assets/content-fragments/content-fragments-variations.md) är också tillgängligt.

## Universal Editor {#universal-editor}

Universal Editor är ett modernt användargränssnitt där du kan skapa AEM på ett innehållsmedvetet sätt och det är det första alternativet för AEM projekt som utnyttjar Edge Delivery Services.

![Universell redigerare](assets/authoring-methods-ue.png)

Den universella redigeraren nås via Sites-konsolen i AEM, men har den kraft och innehållsmedvetna flexibilitet som krävs för att skapa inte bara ditt AEM utan även korrekt instrumenterat externt innehåll.

Läs mer om Universal Editor i dokumentet [Skapa innehåll med den universella redigeraren.](/help/implementing/universal-editor/authoring.md)

## Dokumentbaserad redigering {#document-based}

Om du använder Edge Delivery-tjänster kan du välja att redigera ditt innehåll som vanliga dokument som Microsoft Word eller Google Docs helt utanför AEM konsol.

![Redigera dokumentbaserat innehåll](assets/authoring-methods-document.jpg)

Med dokumentbaserad redigering kan man använda de verktyg man redan känner till och ändå dra nytta av hur snabbt och effektivt AEM Edge Delivery Services kan publicera sitt material. Dokumentbaserad redigering kräver ingen användning av AEM.

Mer information om dokumentbaserad redigering finns i dokumentet [Skapa innehåll för Edge Delivery Services.](/help/edge/authoring.md)
