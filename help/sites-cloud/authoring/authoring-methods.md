---
title: Metoder för att skapa innehåll i AEM
description: Lär dig olika sätt att skapa innehåll i AEM och hur de skiljer sig åt.
feature: Authoring
exl-id: ef482843-451b-474e-a8d0-d0bfcc17221b
solution: Experience Manager Sites
role: User
source-git-commit: 7ad9a959592f1e8cebbcad9a67d280d5b2119866
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 0%

---

# Metoder för att skapa innehåll i AEM {#authoring-methods}

Lär dig olika sätt att skapa innehåll i AEM, hur de skiljer sig åt och när du kan använda det ena över det andra.

## AEM redigeringsflexibilitet {#authoring-flexibility}

AEM as a Cloud Service erbjuder flera olika redigeringsprogram för att redigera olika typer av innehåll och har stöd för olika redigeringsanvändningsområden.

* [WYSIWYG-redigering med sidredigeraren](#page-editor) - Sidredigeraren är den klassiska redigeraren för att skapa innehåll i AEM, har testats och är tillförlitlig för tusentals webbplatser.
* [WYSIWYG-redigering med den universella redigeraren](#universal-editor) - Den universella redigeraren är ett modernt användargränssnitt där du kan AEM innehåll på ett innehållsmedvetet sätt och som är tillgängligt för AEM projekt som utnyttjar Edge Delivery Services.
* [Dokumentbaserad redigering](#document-based) - Om du använder Edge Delivery-tjänster kan du välja att redigera ditt innehåll som vanliga dokument som Microsoft Word eller Google Docs helt utanför AEM.
* [AEM Content Fragment Editor](#cf-editor) - Det här är den valfria redigeraren för att skapa rubrikfritt innehåll.

På grund av AEM integrerade och skalbara natur kan dessa metoder användas exklusivt eller i kombination med varandra beroende på projektets behov.

Kontakta systemadministratören eller projektledaren om du är osäker på vilka redigeringsalternativ som är tillgängliga för dig eller om du vill utforska nya alternativ för att skapa ditt innehåll.

## WYSIWYG-redigering med sidredigeraren {#page-editor}

Det här är den klassiska redigeraren för att skapa innehåll i AEM, som har testats och registrerats som pålitligt för tusentals eller tusentals webbplatser.

![AEM sidredigeraren](assets/authoring-methods-page-editor.png)

Den AEM sidredigeraren innehåller en integrerad miljö för att skapa innehåll med hjälp av ett WYSIWYG-gränssnitt (what-you-see-is-what-you-get). Dra-och-släpp fördefinierade komponenter för att skapa sidan och redigera innehållet på plats.

Mer information om AEM finns i dokumentet [AEM Page Editor.](/help/sites-cloud/authoring/page-editor/introduction.md)

## WYSIWYG-redigering med den universella redigeraren {#universal-editor}

Universal Editor är ett modernt användargränssnitt där du kan skapa AEM på ett innehållsmedvetet sätt och det är det första alternativet för AEM projekt som utnyttjar Edge Delivery Services.

![Den universella redigeraren](assets/authoring-methods-ue.png)

Den universella redigeraren nås via Sites-konsolen i AEM, men har den kraft och innehållsmedvetna flexibilitet som krävs för att skapa inte bara ditt AEM utan även korrekt instrumenterat externt innehåll.

Mer information om den universella redigeraren finns i dokumentet [Skapa innehåll med den universella redigeraren.](/help/sites-cloud/authoring/universal-editor/authoring.md)

## Dokumentbaserad redigering  {#document-based}

Om du använder Edge Delivery tjänster kan du välja att redigera ditt innehåll som konventionella dokument, som Microsoft Word eller Google Docs, helt utanför [AEM **Sites** -konsolen.](/help/sites-cloud/authoring/sites-console/introduction.md)

![Redigerar dokumentbaserat innehåll](assets/authoring-methods-document.jpg)

Med dokumentbaserad redigering kan man använda de verktyg man redan känner till och ändå dra nytta av hur snabbt och effektivt AEM Edge Delivery Services kan publicera sitt material. Dokumentbaserad redigering kräver ingen användning av AEM.

Mer information om dokumentbaserad redigering finns i dokumentet [Redigering och publicering av innehåll.](/help/edge/docs/authoring.md)

## AEM Content Fragment Editor {#cf-editor}

AEM Content Fragment Editor är den självklara redigeraren för att skapa rubrikfritt innehåll.

![AEM Content Fragment Editor](assets/authoring-methods-cf-editor.png)

AEM Content Fragment Editor har ett tydligt gränssnitt för att skapa och hantera strukturerat innehåll, idealiskt för headless-leverans.

Mer information om AEM Content Fragment Editor finns i dokumenten [Hantera innehållsfragment](/help/sites-cloud/administering/content-fragments/managing.md) och [Skapa innehållsfragment](/help/sites-cloud/administering/content-fragments/managing.md).

>[!NOTE]
>
>Redigeraren *new* som markeras i det här avsnittet är inte tillgänglig vid lokal utveckling för AEM as a Cloud Service.
>
>[*Originalredigeraren* för innehållsfragment](/help/assets/content-fragments/content-fragments-variations.md) är också tillgänglig.
