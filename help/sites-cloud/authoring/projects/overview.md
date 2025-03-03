---
title: Projekt
description: Med projekt kan du gruppera resurser i en enhet vars gemensamma, delade miljö gör det enkelt att hantera dina projekt
exl-id: c5f3331e-637f-4816-be83-faf2df59bd5f
solution: Experience Manager Sites
feature: Authoring
role: User
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1253'
ht-degree: 7%

---

# Projekt {#projects}

Med projekt kan du gruppera resurser i en enhet. En gemensam, delad miljö gör det enkelt att hantera projekt. De typer av resurser som du kan associera med ett projekt kallas för Plattor i AEM. Rutorna kan innehålla projekt- och teaminformation, resurser, arbetsflöden och andra typer av information, vilket beskrivs i detalj i [Projektrutor](#project-tiles).

>[!CAUTION]
>
>För användare i projekt som vill se andra användare/grupper när de använder projektfunktioner som att skapa projekt, skapa uppgifter/arbetsflöden, se och hantera team, måste dessa användare ha läsåtkomst på `/home/users` och `/home/groups`. Det enklaste sättet att implementera detta är att ge gruppen **projects-users** läsåtkomst till `/home/users` och `/home/groups`.

Som användare kan du göra följande:

* Skapa projekt
* Koppla innehåll- och resursmappar till ett projekt
* Ta bort projekt
* Ta bort innehållslänkar från projekt

Se följande ytterligare ämnen:

* [Hantera projekt](/help/sites-cloud/authoring/projects/managing.md)
* [Arbeta med uppgifter](/help/sites-cloud/authoring/projects/tasks.md)
* [Arbeta med projektarbetsflöden](/help/sites-cloud/authoring/projects/workflows.md)

## Projektkonsol {#projects-console}

Projektkonsolen är den plats där du får åtkomst till och hanterar dina projekt i AEM.

![Projektkonsolen](/help/sites-cloud/authoring/assets/projects-console.png)

* Välj **Tidslinje** och sedan ett projekt för att visa tidslinjen.
* Välj **Markera** om du vill aktivera markeringsläget.
* Klicka på **Skapa** för att lägga till projekt.
* Med **Växla aktiva projekt** kan du växla mellan alla projekt och endast de som är aktiva.
* Med **Visa statistikvy** kan du visa projektstatistik för slutförda uppgifter.

## Projektpaneler {#project-tiles}

Med Projekt kan du koppla olika typer av information till dina projekt. Dessa kallas **plattor**. Var och en av plattorna och vilken typ av information de innehåller beskrivs i detta avsnitt.

Du kan associera följande rutor med ditt projekt. Var och en av dem beskrivs i följande avsnitt:

* Assets och resurssamlingar
* Erfarenheter
* Länkar
* Projektinformation
* Team
* Landningssidor
* E-post
* Arbetsflöden
* Launches
* Uppgifter

### Assets {#assets}

I rutan **Assets** kan du samla alla resurser som du använder för ett visst projekt.

![Assets-panel](/help/sites-cloud/authoring/assets/projects-assets-tile.png)

Du överför resurser direkt i rutan. Du kan dessutom skapa bilduppsättningar, snurruppsättningar eller blandade medieuppsättningar om du har Dynamic Media-tillägget.

![Bilduppsättning](/help/sites-cloud/authoring/assets/projects-image-sets.png)

### Resurssamlingar {#asset-collections}

På liknande sätt som resurser kan du lägga till [resurssamlingar](/help/assets/manage-collections.md) direkt i ditt projekt. Du definierar samlingar i Assets.

![Resurssamling](/help/sites-cloud/authoring/assets/projects-asset-collections.png)

Lägg till en samling genom att klicka på **Lägg till samling** och välja önskad samling i listan.

### Erfarenheter {#experiences}

Med rutan **Erfarenheter** kan du lägga till en mobilapp, en webbplats eller en publikation i projektet.

![Erfarenheter](/help/sites-cloud/authoring/assets/project-experiences.png)

Ikonerna anger vilken typ av upplevelse som visas: webbplats, mobilapp eller publikation. Lägg till upplevelser genom att trycka på eller klicka på nedåtpilen och knacka på **Lägg till upplevelse** och välja typ av upplevelse.

![Lägg till en upplevelse](/help/sites-cloud/authoring/assets/projects-add-experience.png)

Välj sökväg för miniatyrbilderna och ändra miniatyrbilden för upplevelsen om det är tillämpligt. Erfarenheter grupperas tillsammans i rutan **Erfarenheter**.

### Länkar {#links}

På länkpanelen kan du koppla externa länkar till ditt projekt.

![Länkar](/help/sites-cloud/authoring/assets/project-links.png)

Du kan namnge länken med ett lättkänt namn och ändra miniatyrbilden.

![Lägg till länk](/help/sites-cloud/authoring/assets/projects-add-link.png)

### Projektinformation {#project-info}

Panelen Projektinformation innehåller allmän information om projektet, inklusive en beskrivning, projektstatus (inaktiv eller aktiv), ett förfallodatum och medlemmar. Dessutom kan du lägga till en projektminiatyr, som visas på huvudprojektsidan.

![Projektinformation](/help/sites-cloud/authoring/assets/project-info.png)

Teammedlemmar kan tilldelas och tas bort från den här panelen (eller få sina roller ändrade) och teampanelen.

![Lägg till teammedlemmar i projektet](/help/sites-cloud/authoring/assets/projects-add-team.png)

### Översättningsjobb {#translation-job}

Översättningsjobbrutan är där du startar en översättning och även där du ser statusen för dina översättningar. Mer information om hur du konfigurerar översättningen finns i [Skapa översättningsprojekt](/help/assets/translate-assets.md).

![Översättningsjobb](/help/sites-cloud/authoring/assets/projects-translation-job.png)

Klicka på ellipsen längst ned på **översättningsjobbkortet** för att visa resurserna i översättningsarbetsflödet. I översättningsjobblistan visas även poster för metadata och taggar för resurser. Dessa poster anger att metadata och taggar för resurserna också översätts.

![Information om översättningsjobb](/help/sites-cloud/authoring/assets/projects-translation-job-detail.png)

### Team {#team}

I den här rutan kan du ange medlemmarna i projektteamet. När du redigerar kan du ange namnet på teammedlemmen och tilldela användarrollen.

![Teampanel](/help/sites-cloud/authoring/assets/projects-team-tile.png)

Du kan lägga till och ta bort teammedlemmar från teamet. Dessutom kan du redigera den [användarroll](#user-roles-in-a-project) som tilldelats teammedlemmen.

![Lägg till team från listan](/help/sites-cloud/authoring/assets/projects-add-team-list.png)

### Arbetsflöden {#workflows}

Du kan tilldela ditt projekt för att följa vissa arbetsflöden. Om några arbetsflöden körs visas deras status i rutan **Arbetsflöden** i Projekt.

![Arbetsflöden](/help/sites-cloud/authoring/assets/project-workflows.png)

Du kan tilldela ditt projekt för att följa vissa arbetsflöden. Beroende på vilket projekt du väljer finns olika arbetsflöden tillgängliga.

Dessa beskrivs i [Arbeta med projektarbetsflöden](/help/sites-cloud/authoring/projects/workflows.md).

### Launches {#launches}

I rutan Launches (Starta) visas alla starter som har begärts med ett [begärandestartarbetsflöde](/help/sites-cloud/authoring/projects/workflows.md).

![Startar](/help/sites-cloud/authoring/assets/project-launches.png)

### Uppgifter {#tasks}

Med uppgifter kan du övervaka status för projektrelaterade uppgifter, inklusive arbetsflöden. Uppgifter beskrivs mer ingående i [Arbeta med uppgifter](/help/sites-cloud/authoring/projects/tasks.md).

![Uppgifter](/help/sites-cloud/authoring/assets/projects-tasks.png)

## Projektmallar {#project-templates}

AEM levereras med tre olika mallar:

* Ett enkelt projekt - Ett referensexempel för projekt som inte passar in i andra kategorier (en&quot;catch-all&quot;). Det innehåller tre grundläggande roller (ägare, redigerare och observatörer) och fyra arbetsflöden (projektgodkännande, begäranstart, begäranstartsida och e-postbegäran).
* Ett medieprojekt - Ett referensexempelprojekt för medierelaterade aktiviteter. Det innehåller flera medierelaterade projektroller (fotografer, redigerare, copywriters, designers, Owners och Observers). Det begär också arbetsflöde för kopiering för att begära och granska text.
* Ett [översättningsprojekt](/help/sites-cloud/administering/translation/overview.md) - Ett referensexempel för hantering av översättningsrelaterade aktiviteter. Det innehåller tre grundläggande roller (ägare, redigerare och observatörer). Det innehåller två arbetsflöden som du kommer åt i användargränssnittet för arbetsflöden.

Beroende på vilken mall du väljer har du olika alternativ tillgängliga, särskilt när det gäller användarroller och arbetsflöden.

## Användarroller i ett projekt {#user-roles-in-a-project}

De olika användarrollerna anges i en projektmall och används av två primära orsaker:

1. Behörigheter. Användarrollerna tillhör en av de tre kategorierna: observatör, redigerare, ägare. En fotograf eller en copywriter har till exempel samma behörighet som en redigerare. Behörigheterna avgör vad en användare kan göra med innehållet i ett projekt.
1. Arbetsflöden. Arbetsflödena avgör vem som tilldelas uppgifter i ett projekt. Uppgifterna kan associeras med en projektroll. En uppgift kan till exempel tilldelas fotografer så att alla gruppmedlemmar som har rollen fotograf får uppgiften.

Alla projekt har stöd för följande standardroller så att du kan administrera säkerhet och kontrollbehörigheter:

| Roll | Beskrivning | Behörigheter | Gruppmedlemskap |
|---|---|---|---|
| Observer | En användare i den här rollen kan visa projektinformation, inklusive projektstatus. | Skrivskyddade behörigheter i ett projekt | `workflow-users` grupp |
| Redigerare | En användare med den här rollen kan överföra och redigera innehållet i ett projekt. | Läs- och skrivbehörighet för ett projekt, associerade metadata och relaterade resurser, behörighet att överföra en tagningslista och granska och godkänna resurser, skrivbehörighet för /etc/commerce, ändra behörighet för ett specifikt projekt | arbetsflödesgrupp |
| Ägare | En användare med den här rollen kan initiera ett projekt. En ägare kan skapa ett projekt, initiera arbete i ett projekt och även flytta godkända resurser till produktionsmappen. Även om alla andra uppgifter i projektet kan visas och utföras av ägaren. | Skrivbehörighet för `/etc/commerce` | `dam-users`-grupp (för att kunna skapa ett projekt) projekt-administratörsgrupp (för att kunna skapa ett projekt och flytta resurser) |

>[!NOTE]
>
>När du skapar projektet och lägger till användare för de olika rollerna skapas grupper som är kopplade till projektet automatiskt för att hantera associerade behörigheter. Ett projekt med namnet Myproject skulle till exempel ha tre grupper, **Myproject Owners**, **Myproject Editors** och **Myproject Observers**. Om projektet tas bort tas de grupperna dock inte bort automatiskt. En administratör måste ta bort grupperna manuellt i **Verktyg** > **Dokumentskydd** > **Grupper**.
