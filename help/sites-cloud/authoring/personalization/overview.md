---
title: Personalisering och målgruppsanpassning av innehåll
description: Lär dig hur AEM kan skapa personaliserat innehåll
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8
workflow-type: tm+mt
source-wordcount: '518'
ht-degree: 0%

---


# Personalisering och målanpassning av innehåll {#personalization}

## Personalisering och målanpassning av innehåll {#personalization-and-content-targeting}

AEM tillhandahåller ett ramverk med verktyg för att skapa riktat innehåll och presentera personaliserade upplevelser.

## Målläge {#targeting-mode}

[Skapa riktat ](/help/sites-cloud/authoring/personalization/targeted-content.md) innehåll med målinriktningsläget AEM. Målinriktningsläget och Target-komponenten tillhandahåller verktyg för att skapa innehåll för upplevelserna av era marknadsföringsaktiviteter.

## Aktiviteter {#activities}

Verksamheter definierar och organiserar era era marknadsföringssatsningar. Verksamheterna omfattar de målgrupper som ni riktar in er på och den tidsperiod under vilken målgruppsanpassningen tillämpas.

Produktkatalogen kan t.ex. innehålla lärare som fokuserar på säsongsprodukter. Sommarsportsaktiviteten definierar de marknadsföringssegment som lärarna siktar på under sommarmånaderna.

Aktiviteter identifierar också [målmotorn](#targeting-engine) som dina sidor använder.

Använd [aktivitetskonsolen](/help/sites-cloud/authoring/personalization/activities.md) för att skapa och hantera aktiviteter för dina varumärken. Du kan också skapa aktiviteter när du [redigerar riktat innehåll](/help/sites-cloud/authoring/personalization/targeted-content.md).

## Upplevelser {#experiences}

För varje aktivitet definierar ni en eller flera upplevelser som identifierar målgrupperna som ni riktar in er mot. AEM gör det möjligt att styra innehållet som omfattar varje upplevelse.

Målgrupperna bygger på marknadsföringssegment som skapats i AEM eller Adobe Target. När en besökare öppnar en webbsida avgör sidlogiken vilken målgrupp de tillhör och visar det innehåll som du har skapat för den målgruppen.

En aktivitet definierar till exempel upplevelser för två olika målgrupper: kvinnor över 30 år och kvinnor under 30 år. Kvinnornas sida på en webbplats kan visa olika produkter för varje upplevelse.

Ni definierar upplevelser för en aktivitet. Du kan använda [aktivitetskonsolen](/help/sites-cloud/authoring/personalization/activities.md#adding-editing-an-activity-using-the-activities-console) eller [Målläge](/help/sites-cloud/authoring/personalization/targeted-content.md#adding-and-removing-experiences-using-targeting-mode) för att lägga till upplevelser i en aktivitet.

## Erbjudanden {#offers}

Ett erbjudande är innehåll som visas på en plats på en sida för en upplevelse. Använd olika erbjudanden för olika upplevelser för att maximera innehållets effektivitet för era målgrupper.

Kvinnans sida på en exempelwebbplats kan t.ex. använda erbjudanden som den suddgummibild som visas högst upp på sidan. Ett annat erbjudande används som teaser för upplevelsen kvinna över 30 och för kvinna under 30.

Använd [Erbjudandekonsolen](/help/sites-cloud/authoring/personalization/offers.md) för att skapa erbjudanden som du kan använda i flera olika upplevelser. Skapa engångserbjudanden eller lägg till erbjudanden från ett erbjudandebibliotek när [du skapar riktat innehåll](/help/sites-cloud/authoring/personalization/targeted-content.md).

## Målmotor {#targeting-engine}

Målmotorn är den mekanism som driver logiken för riktat innehåll. [Aktiviteter ](/help/sites-cloud/authoring/personalization/activities.md) är konfigurerade att använda en av två målmotorer som är tillgängliga: AEM och Adobe Target.

### AEM {#aem}

AEM har en inbyggd motor för målinriktning som bearbetar sidförfrågningar och avgör vilket innehåll som ska visas. När ni använder den AEM målgruppsmotorn begränsas ni till att använda segment som skapas i AEM för att definiera målgrupperna för era upplevelser.

### Adobe Target {#adobe-target}

Adobe Target målgruppsmotor spårar information som samlats in från sidbesök i Adobe Target.

* När ni använder den här målgruppsmotorn använder ni de segment ni importerar från Adobe Target för att definiera målgrupperna för era upplevelser.
* Aktiviteter som använder Adobe Target-motorn är [synkroniserade med Target](/help/sites-cloud/authoring/personalization/activities.md#synchronizing-activities-with-adobe-target).

Du kan använda den här motorn när du har integrerat med Adobe Target. <!--You can use this engine when you have [integrated with Adobe Target](/help/sites-administering/opt-in.md).-->
