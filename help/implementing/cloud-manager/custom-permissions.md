---
title: Anpassade behörigheter
description: Lär dig hur du kan använda anpassade behörigheter för att skapa nya anpassade behörighetsprofiler med konfigureringsbara behörigheter för att begränsa åtkomst till program, pipelines och miljöer för användare av Cloud Managers.
source-git-commit: 928a3f0d8ee98e211aa03ad3d0fd83b780e98bbc
workflow-type: tm+mt
source-wordcount: '1509'
ht-degree: 1%

---


# Anpassade behörigheter {#custom-permissions}

Lär dig hur du kan använda anpassade behörigheter för att skapa nya anpassade behörighetsprofiler med konfigureringsbara behörigheter för att begränsa åtkomst till program, pipelines och miljöer för användare av Cloud Managers.

>[!NOTE]
>
>Den här funktionen är bara tillgänglig för [det tidiga adopteringsprogrammet.](/help/implementing/cloud-manager/release-notes/current.md#early-adoption)

## Introduktion {#introduction}

Cloud Manager har en uppsättning fördefinierade roller som styr åtkomsten till olika funktioner i molnhanteraren:

* Business Owner
* Program Manager
* Deployment Manager
* Developer

Med anpassade behörigheter kan användare skapa nya anpassade behörighetsprofiler med konfigurerbara behörigheter för att begränsa åtkomst för molnhanterare till program, rörledningar och miljöer.

>[!TIP]
>
>Mer information om fördefinierade roller finns i dokumentet [AEM as a Cloud Service team och produktprofiler.](/help/onboarding/aem-cs-team-product-profiles.md)

## Använda anpassade behörigheter {#using}

För att skapa och använda egna behörigheter krävs tre steg:

1. [Skapa en ny produktprofil.](#create)
1. [Tilldela anpassade behörigheter till den nya produktprofilen.](#assign-permissions)
1. [Tilldela användare till den nya produktprofilen.](#assign-users)

I det här avsnittet beskrivs de här stegen. Det kan vara praktiskt att använda [Villkor](#terms) och [Konfigurerbara behörigheter](#configurable-permissions) när du skapar egna behörigheter.

>[!NOTE]
>
>Du måste ha produktadministratörsbehörighet i Admin Console för Adobe Experience Manager as a Cloud Service för att kunna skapa nya profiler och hantera behörigheter för Cloud Manager.

### Skapa en ny produktprofil {#create}

Du måste först skapa en ny produktprofil innan du kan tilldela anpassade behörigheter.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/)

1. På landningssidan för Cloud Manager trycker eller klickar du på **Hantera åtkomst** knapp

![Knappen Hantera åtkomst](assets/manage-access.png)

1. Du omdirigeras till **Produkter** på Admin Console, där du kan hantera användare och behörigheter för molnhanteraren. Tryck eller klicka på Admin Console **Ny profil** -knappen.

![Ny profil, knapp](assets/admin-console-new-profile.png)

1. Ange allmän information om profilen.

   * **Produktprofilnamn** - Ett beskrivande namn för profilen
   * **Visningsnamn** - Ett förkortat namn som visas i användargränssnittet (alternativ)
   * **Beskrivning** - En informativ beskrivning av profilen som förklarar dess syfte (valfritt)
   * **Meddela användare via e-post** - När du väljer det här alternativet meddelas användare via e-post när de läggs till eller tas bort från profilen.

1. Tryck eller klicka **Spara** när det är klart.

Den nya produktprofilen sparas och visas i listan över produktprofiler på Admin Console.

### Tilldela anpassade behörigheter till profil {#assign-permissions}

Nu när du har en ny produktprofil kan du tilldela den anpassade behörigheter.

1. Tryck eller klicka på namnet på Admin Console [en ny produktprofil som du just har skapat.](#create)

1. I det fönster som öppnas väljer du **Behörigheter** om du vill visa en lista med redigerbara behörigheter.

   ![Redigerbara behörigheter](assets/permissions-tab.png)

1. Tryck eller klicka på **Redigera** länk till en behörighet att redigera den.

1. The **Redigera behörigheter** öppnas.
   * Den behörighet du valde i föregående steg är markerad i den vänstra kolumnen.
   * Behörighetsobjekten som är tillgängliga för tilldelning av behörigheten finns i den mellersta kolumnen med etiketten **Tillgänglig behörighet** Objekt.
   * De tilldelade behörighetsobjekten finns i den högra kolumnen med etiketten **Behörighetsobjekt som ingår**.

   ![Redigera behörighetsobjekt](assets/edit-permission-items.png)

1. Tryck eller klicka på plustecknet (`+`) bredvid behörighetsobjektet för att lägga till det i kolumnen **Behörighetsobjekt som ingår**.

   * Tryck eller klicka på `i` -ikon bredvid ett behörighetsobjekt om du vill veta mer om det.

1. Tryck eller klicka på **Lägg till alla** längst upp på **Tillgängliga behörigheter** för att lägga till alla behörigheter.

1. Om profilen alltid ska ha alla behörighetsobjekt bör du använda **Inkludera automatiskt** alternativ.

   * **På** - Alla aktuella behörighetsobjekt och framtida behörighetsobjekt flyttas till Inkluderade behörighetsobjekt och tillämpas därefter när de sparas.
   * **Av** - Alla behörighetsobjekt flyttas tillbaka till tillgängliga behörighetsobjekt och när de sparas används de i enlighet med detta.

1. Tryck eller klicka **Spara** när du har definierat behörighetsobjekten för den nya produktprofilen.

Din nya produktprofil sparas nu med anpassade behörigheter.

### Tilldela användare till anpassade behörigheter {#assign-users}

Nu kan du tilldela användare till den nya produktprofilen som du skapade med anpassade behörigheter.

1. Tryck eller klicka på namnet på Admin Console [ny produktprofil som du just har tilldelat anpassade behörigheter till.](#assign-permissions)

1. I det fönster som öppnas väljer du **Användare** -fliken.

1. Tryck eller klicka på **Lägg till användare** och tilldela användare till din nya produktprofil med anpassade behörigheter.

Se avsnittet **Lägga till användare och användargrupper i en produktprofil** av dokumentet [Hantera produktprofiler för företagsanvändare](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html) för mer information om hur du använder Admin Console.

## Konfigurerbara behörigheter {#configurable-permissions}

Följande behörigheter är tillgängliga för att skapa anpassade profiler.

| Behörighet | Beskrivning |
|---|---|
| Skapa program | Tillåt användare att skapa ett nytt program |
| Programåtkomst | Ge användarna åtkomst till program |
| Programredigering | Tillåt användare att redigera program |
| Miljöskapande | Tillåt användare att skapa en ny miljö |
| Miljöredigering | Tillåt användare att uppdatera och redigera miljöer |
| Miljöloggar Läs | Tillåt användare att läsa miljöloggar |
| Skapa pipeline | Tillåt användare att skapa nya rörledningar |
| Ta bort pipeline | Tillåt användare att ta bort rörledningar |
| Redigera pipeline | Tillåt användare att redigera rörledningar |
| Godkänn/avvisa produktionsdistributioner | Tillåt användare att godkänna eller avvisa ett produktionsdistributionssteg |
| Avbryt körning av pipeline | Tillåt användare att avbryta pipeline-körningar |
| Körningsstart för pipeline | Tillåt användare att starta en ny pipeline-körning |
| Åsidosätt/avvisa viktiga måttfel | Tillåt användare att åsidosätta/ignorera viktiga mätfel |
| Produktionsdistributionsschema | Tillåt användare att schemalägga ett produktionsdistributionssteg |
| Datainformationsåtkomst | Tillåt användare att komma åt databasinformation och generera lösenord för åtkomst |

### Behörigheter på organisationsnivå {#organization-level}

Behörigheter på organisationsnivå avser behörigheter som alltid ges i alla program i en organisation.

Följande behörigheter är behörigheter på organisationsnivå:

* **Skapa program** - Med den här behörigheten kan användare skapa ett nytt program i organisationen.
* **Datainformationsåtkomst** Behörigheten på innehavar-/organisationsnivå ger användarna möjlighet att generera användarnamn, lösenord och databas-URL för åtkomst och att bidra till kundprojekt.
   * Användarnamn och lösenord för databasåtkomst är gemensamma för alla rapporter i organisationen, men databasens URL är unik för varje program.
   * Se dokumentet [Åtkomst till databaser](/help/implementing/cloud-manager/managing-code/accessing-repos.md) för mer information.

## Villkor {#terms}

Följande termer används för att skapa och hantera anpassade behörigheter och fördefinierade roller.

| Term | Beskrivning |
|---|---|
| Fördefinierade behörigheter | Fördefinierade roller som **Företagsägare**, **Distributionshanteraren**, osv. för att styra olika funktioner i Cloud Manager. Mer information om fördefinierade roller finns i dokumentet [AEM as a Cloud Service team och produktprofiler.](/help/onboarding/aem-cs-team-product-profiles.md) |
| Anpassade behörigheter | Funktioner i Cloud Manager som gör att användare kan skapa behörighetsprofiler för att definiera roller som styr funktioner som stöds i Cloud Manager |
| Produktprofil | Skapat i Admin Console för att hantera konfigurerbara behörigheter som gäller för användare som ingår i behörighetsprofilen |
| Konfigurerbar behörighet | Cloud Manager-behörigheter som kan konfigureras i behörighetsprofilen |
| Behörighetsobjekt | Ett program, en miljö eller en pipeline-resurs som en behörighet kan tillämpas på |

Behörighetsobjekt avser det område där behörigheten ska tillämpas. Vanligtvis är det något av följande.

| Typ av behörighetsobjekt | Exempel | Beskrivning |
|---|---|---|
| Organisation | organisation:företagA | Alla tillämpliga resurser i en organisation. En resurs kan vara ett program, en miljö eller en pipeline. Om användaren lägger till en organisation för någon behörighet får även alla nya resurser i den organisationen den behörigheten. |
| Program | Program A | Alla tillämpliga resurser i ett program |
| Miljö | Program A: miljö | Tillämpligt på en viss miljö |
| Pipeline | Program A: Pipeline | Gäller för en viss rörledning |

## Begränsningar {#limitations}

Tänk på följande begränsningar när du använder anpassade behörigheter.

* Profilen för anpassade behörigheter listar även AMS-program, -miljöer och -pipelines när behörigheter konfigureras.
* Resurser som program, miljö, pipeline osv. som skapats i Cloud Manager kan ta upp till två minuter att visa i Admin Console för behörighetskonfiguration.
* I sällsynta fall där anpassade behörighetstjänster inte svarar är fördefinierade profiler fortfarande tillgängliga och användare i fördefinierade profiler fortfarande har lämplig åtkomst.

## Vanliga frågor {#faq}

### Vilka behörighetsprofiler är fördefinierade behörighetsprofiler?

* Business Owner
* Program Manager
* Deployment Manager
* Developer

Mer information om fördefinierade roller finns i dokumentet [AEM as a Cloud Service team och produktprofiler.](/help/onboarding/aem-cs-team-product-profiles.md)

### Vad händer med fördefinierade behörighetsprofiler med introduktion till anpassade profiler?

Standardproduktprofiler och molnhanterarroller fungerar fortfarande på samma sätt som tidigare.

### Kan jag redigera fördefinierade behörighetsprofiler?

Nej, standardprofiler kan inte redigeras. Du kan inte lägga till eller ta bort behörigheter i standardbehörighetsprofilen. Du kan bara lägga till eller ta bort användare från fördefinierade profiler.

### Ska jag ta bort fördefinierade behörighetsprofiler eftersom anpassade profiler nu är tillgängliga?

Fördefinierade behörighetsprofiler får inte tas bort från Admin Console.

### Kan jag lägga till användare i flera behörighetsprofiler?

Ja, en användare kan ingå i flera profiler, inklusive fördefinierade och anpassade behörighetsprofiler. När en användare tilldelas till flera profiler blir de kombinerade behörigheterna från alla tilldelade behörighetsprofiler tillgängliga för den användaren.

### Vad händer om en användare har behörighet att redigera en miljö/pipeline men inte har åtkomst till ett program som innehåller miljön/pipeline?

I det här fallet kan användaren inte komma åt miljön eller pipeline om han/hon inte har **Programåtkomst** behörigheter som innehåller miljön eller pipeline.
