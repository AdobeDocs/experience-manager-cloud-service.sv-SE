---
title: Anpassade behörigheter
description: Lär dig hur du kan använda anpassade behörigheter för att skapa anpassade behörighetsprofiler med konfigureringsbara behörigheter för att begränsa åtkomst till program, pipelines och miljöer för användare av Cloud Managers.
exl-id: 167da985-7f19-45b3-90a3-884817907da2
solution: Experience Manager
feature: Security, Developing
role: Admin, Architect, Developer
source-git-commit: 0afd74120380c9ae3d02db9fb684189c2f19648f
workflow-type: tm+mt
source-wordcount: '1490'
ht-degree: 1%

---


# Anpassade behörigheter {#custom-permissions}

Lär dig hur du kan använda anpassade behörigheter för att skapa anpassade behörighetsprofiler med konfigureringsbara behörigheter för att begränsa åtkomst till program, pipelines och miljöer för användare av Cloud Managers.

## Introduktion {#introduction}

Cloud Manager har en uppsättning fördefinierade roller som styr åtkomsten till olika funktioner i Cloud Manager:

* Business Owner
* Program Manager
* Deployment Manager
* Developer

Med anpassade behörigheter kan användare skapa anpassade behörighetsprofiler med konfigurerbara behörigheter för att begränsa åtkomst för molnhanterare till program, rörledningar och miljöer.

>[!TIP]
>
>Mer information om fördefinierade roller finns i [AEM as a Cloud Service Team och produktprofiler](/help/onboarding/aem-cs-team-product-profiles.md).

## Använda anpassade behörigheter {#using}

Om du vill skapa och använda egna behörigheter krävs det tre steg:

1. [Skapa en produktprofil](#create).
1. [Tilldela anpassade behörigheter till produktprofilen](#assign-permissions).
1. [Tilldela användare till produktprofilen](#assign-users).

I det här avsnittet beskrivs dessa steg. Det kan vara praktiskt att se avsnitten [Villkor](#terms) och [Konfigurerbara behörigheter](#configurable-permissions) när du skapar egna anpassade behörigheter.

>[!NOTE]
>
>Du måste ha produktadministratörsbehörighet i Admin Console för Adobe Experience Manager as a Cloud Service för att kunna skapa profiler och hantera behörigheter för Cloud Manager.

### Skapa en ny produktprofil {#create}

Skapa först en produktprofil som du kan tilldela anpassade behörigheter till.

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/).

1. På Cloud Manager landningssida väljer du knappen **Hantera åtkomst** .

![Knappen Hantera åtkomst](assets/manage-access.png)

1. Du omdirigeras till fliken **Produkter** i Admin Console, där du kan hantera användare och behörigheter för Cloud Manager. I Admin Console väljer du knappen **Ny profil** .

![Knappen Ny profil](assets/admin-console-new-profile.png)

1. Ange allmän information om profilen.

   * **Produktprofilnamn** - Ett beskrivande namn för profilen
   * **Visningsnamn** - Ett förkortat namn som visas i gränssnittet (alternativ)
   * **Beskrivning** - En informativ beskrivning av profilen som förklarar dess syfte (valfritt)
   * **Meddela användare via e-post** - Användare får ett e-postmeddelande när de läggs till eller tas bort från den här profilen.

1. Välj **Spara** när du är klar.

Den nya produktprofilen sparas och visas i listan över produktprofiler i Admin Console.

### Tilldela anpassade behörigheter till profil {#assign-permissions}

Nu när du har en ny produktprofil kan du tilldela den anpassade behörigheter.

1. I Admin Console väljer du namnet på den [nya produktprofilen som du skapade](#create).

1. I det fönster som öppnas väljer du fliken **Behörigheter** för att visa en lista med redigerbara behörigheter.

   ![Redigerbara behörigheter](assets/permissions-tab.png)

1. Markera länken **Redigera** för en behörighet så att du kan redigera den.

1. Fönstret **Redigera behörighet** öppnas.
   * Den behörighet du valde i föregående steg är markerad i den vänstra kolumnen.
   * Behörighetsobjekten som är tillgängliga för tilldelning för behörigheten finns i den mellersta kolumnen med namnet **Tillgänglig behörighet**.
   * De tilldelade behörighetsobjekten finns i den högra kolumnen med etiketten **Inkluderade behörighetsobjekt**.

   ![Redigera behörighetsobjekt](assets/edit-permission-items.png)

1. Markera plusikonen (`+`) bredvid behörighetsobjektet så att du kan lägga till det i kolumnen **Inkluderade behörighetsobjekt**.

   * Markera ikonen `i` bredvid ett behörighetsobjekt om du vill veta mer om det.

1. Välj knappen **Lägg till alla** längst upp i kolumnen **Tillgängliga behörigheter** så att du kan lägga till alla behörigheter.

1. Välj **Spara** när du är klar med att definiera behörighetsobjekten för den nya produktprofilen.

Din nya produktprofil sparas nu med anpassade behörigheter.

### Tilldela användare till anpassade behörigheter {#assign-users}

Nu kan du tilldela användare till den nya produktprofilen som du skapade med anpassade behörigheter.

1. I Admin Console väljer du namnet på den [nya produktprofil som du har tilldelat anpassade behörigheter till](#assign-permissions).

1. I det fönster som öppnas väljer du fliken **Användare**.

1. Välj knappen **Lägg till användare** och tilldela användare till din nya produktprofil med anpassade behörigheter.

Mer information om hur du använder Admin Console finns i avsnittet **Lägg till användare och användargrupper i en produktprofil** i dokumentet [Hantera produktprofiler för företagsanvändare](https://helpx.adobe.com/se/enterprise/using/manage-product-profiles.html).

## Konfigurerbara behörigheter {#configurable-permissions}

Följande behörigheter är tillgängliga för att skapa anpassade profiler.

| Behörighet | Beskrivning |
| --- | --- |
| Skapa program | Låt användarna skapa ett program. |
| Programåtkomst | Ge användarna tillgång till programmen. |
| Programredigering | Låt användarna redigera program. |
| Miljöskapande | Låt användarna skapa en miljö. |
| Miljöredigering | Låt användare uppdatera och redigera miljöer. |
| Miljöloggar Läs | Låt användarna läsa miljöloggar. |
| Hantera miljövariabler | Låt användare skapa/redigera/ta bort miljökonfigurationer. |
| Miljöåterställning - skapa | Låter användarna skapa en miljöåterställning. |
| Återställning av snabb utvecklingsmiljö | Låt användarna återställa RDE (Rapid Development Environment). |
| Hantera innehållskopia | Låt användarna hantera kopieringsåtgärder. |
| Skapa pipeline | Låt användarna skapa rörledningar. |
| Ta bort pipeline | Låt användarna ta bort rörledningar. |
| Redigera pipeline | Låt användarna redigera rörledningar. |
| Godkänn/avvisa produktionsdistributioner | Låt användare godkänna eller avvisa ett produktionsdistributionssteg. |
| Avbryt körning av pipeline | Låt användarna avbryta pipeline-körningar. |
| Körningsstart för pipeline | Låt användarna starta en ny pipeline-körning. |
| Åsidosätt/avvisa viktiga måttfel | Låt användare åsidosätta/ignorera viktiga mätfel. |
| Produktionsdistributionsschema | Låt användarna schemalägga ett produktionsdistributionssteg. |
| Datainformationsåtkomst | Ge användarna åtkomst till databasinformation och generera ett lösenord för åtkomst. |
| Skapa databas | Låt användarna skapa Git-databaser. |
| Radera databas | Låt användarna ta bort Git-databaser. |
| Databasredigering | Låt användarna redigera Git-databaser. |
| Generera databaskod | Låt användarna generera ett projekt av typen arkiv. |
| Domännamnshantering | Låt användare skapa, redigera och ta bort domännamn. |
| Hantera IP Tillåtelselista | Gör att användare kan skapa/redigera/ta bort IP tillåtelselista och IP tillåtelselista-bindning. |
| Hantera nätverksinfrastruktur | Låt användare skapa, redigera och ta bort nätverksinfrastruktur. |
| SSL-certifikatshantering | Låt användare skapa, redigera eller ta bort SSL-certifikat. |
| New Relic Sub Account User Manage | Låt användare läsa/redigera New Relic-underkontoanvändare. |

### Behörigheter på organisationsnivå {#organization-level}

Behörigheter på organisationsnivå avser behörigheter som alltid ges i alla program i en organisation.

Följande behörigheter är behörigheter på organisationsnivå:

* **Skapa program** - Med den här behörigheten kan användare skapa ett program i organisationen.
* **Åtkomst till databasinformation** Med den här innehavar-/organisationsnivån kan användare generera användarnamn, lösenord och databas-URL för åtkomst och bidrag till ett kundprojekt.
   * Användarnamnet och lösenordet för databasåtkomst är gemensamma för alla databaser i organisationen. Databas-URL:en är dock unik för varje program.
   * Mer information finns i [Åtkomst till databaser](/help/implementing/cloud-manager/managing-code/accessing-repos.md).

## Villkor {#terms}

Följande termer används för att skapa och hantera anpassade behörigheter och fördefinierade roller.

| Term | Beskrivning |
| --- | --- |
| Fördefinierade behörigheter | Fördefinierade roller som **Business Owner** och **Deployment Manager** som styr olika funktioner i Cloud Manager. Mer information om fördefinierade roller finns i [AEM as a Cloud Service Team och produktprofiler](/help/onboarding/aem-cs-team-product-profiles.md). |
| Anpassade behörigheter | Med funktionerna i Cloud Manager kan användare skapa behörighetsprofiler för att definiera roller som styr de funktioner som stöds i Cloud Manager. |
| Produktprofil | Skapat i Admin Console för att hantera konfigurerbara behörigheter som gäller för användare som ingår i behörighetsprofilen. |
| Konfigurerbar behörighet | Cloud Manager-behörigheter som du kan konfigurera i behörighetsprofilen. |
| Behörighetsobjekt | Ett program, en miljö eller en pipeline-resurs som en behörighet kan tillämpas på. |

Behörighetsobjekt avser det område där behörigheten tillämpas. Vanligtvis är det något av följande.

| Typ av behörighetsobjekt | Exempel | Beskrivning |
| --- | --- | --- |
| Organisation | organisation:companyA | Alla tillämpliga resurser i en organisation. En resurs kan vara ett program, en miljö eller en pipeline. Om användaren lägger till en organisation för någon behörighet har alla nya resurser i den organisationen också den behörigheten. |
| Program | Program A | Alla tillämpliga resurser i ett program. |
| Miljö | Program A: miljö | Gäller en viss miljö. |
| Pipeline | Program A: Pipeline | Gäller en viss rörledning. |

## Användningsinformation {#usage-notes}

* En anpassad behörighetsprofil visar även AMS-program, -miljöer och -pipelines när behörigheter konfigureras.
* Resurser som program, miljö och pipeline som skapats i Cloud Manager kan ta upp till två minuter att visa i Admin Console för behörighetskonfiguration.
* I sällsynta fall där en anpassad behörighetstjänst inte svarar är fördefinierade profiler fortfarande tillgängliga och användare i fördefinierade profiler fortfarande har lämplig åtkomst.

## Vanliga frågor {#faq}

### Vilka behörighetsprofiler är fördefinierade behörighetsprofiler?

* Business Owner
* Program Manager
* Deployment Manager
* Developer

Mer information om fördefinierade roller finns i [AEM as a Cloud Service Team och produktprofiler](/help/onboarding/aem-cs-team-product-profiles.md).

### Vad händer med fördefinierade behörighetsprofiler med introduktion till anpassade profiler?

Standardproduktprofiler och Cloud Manager-roller fungerar fortfarande på samma sätt som tidigare.

### Kan jag redigera fördefinierade behörighetsprofiler?

Nej, standardprofiler kan inte redigeras. Du kan inte lägga till eller ta bort behörigheter i standardbehörighetsprofilen. Du kan bara lägga till eller ta bort användare från fördefinierade profiler.

### Ska jag ta bort fördefinierade behörighetsprofiler eftersom anpassade profiler nu är tillgängliga?

Ta inte bort fördefinierade behörighetsprofiler från Admin Console.

### Kan jag lägga till användare i flera behörighetsprofiler?

Ja, en användare kan ingå i flera profiler, inklusive fördefinierade och anpassade behörighetsprofiler. När en användare tilldelas till flera profiler är de kombinerade behörigheterna från alla tilldelade behörighetsprofiler tillgängliga för den användaren.

### Vad händer om en användare har behörighet att redigera en miljö/pipeline men inte har åtkomst till ett program som innehåller miljön/pipeline?

I det här fallet kan användaren inte komma åt miljön eller pipelinen om de inte har **Programåtkomst** -behörigheten som innehåller miljön eller pipelinen.
