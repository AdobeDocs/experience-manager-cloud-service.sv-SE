---
title: Page Editor och Universal Editor
description: Sidredigeraren stöds fortfarande av Adobe, men den universella redigeraren ger dig fler möjligheter till dina nya projekt.
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 9fdc24600c9dd4ebf6a3d12462eb9bd387815360
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 0%

---


# Page Editor och Universal Editor {#page-editor-universal-editor}

Sidredigeraren stöds fortfarande av Adobe, men den universella redigeraren ger dig fler möjligheter till dina nya projekt.

## Bakgrund {#background}

Adobe introducerade den [universella redigeraren](/help/implementing/universal-editor/introduction.md) 2024 som en smidig redigerare som använder en modern Javascript-baserad utvecklingsmetod. Universell redigerare är Adobe vision för en smidig och utbyggbar visuell redigeringsupplevelse.

Med tanke på [sidredigerarens](/help/sites-cloud/authoring/page-editor/introduction.md)omfattande funktionsuppsättning och otaliga projekt som investerar i den över AEM långa historia fortsätter Adobe att ge fullt stöd åt sidredigeraren, men innovationen kommer att inriktas på den universella redigeraren.

## Rekommendation {#recommendation}

Även om det går snabbt att förminska finns det ett funktionsavstånd mellan Universal Editor och Page Editor ([en funktionsjämförelse finns i nästa avsnitt](#feature-comparison)).

Som tumregel:

* **Nya projekt** bör använda den universella redigeraren som standard.
* **Befintliga projekt** bör fortsätta använda sidredigeraren och använda den universella redigeraren när du startar Edge Delivery eller Headless.

**Vilken redigerare du väljer bör styras helt av det enskilda projektets behov.**

## Funktionsjämförelse {#feature-comparison}

Eftersom luckan mellan de två redigerarna ständigt krymper bör du läsa versionsinformationen för [den universella redigeraren](/help/release-notes/universal-editor/current.md) för att få den senaste utvecklingen.

### Leverans {#delivery}

|  | Page Editor | Anteckningar | Universal Editor | Anteckningar |
|---|---|---|---|---|
| [Klassisk AEM-leverans](/help/sites-cloud/authoring/author-publish.md) | [!BADGE Tillgänglig]{type=Positive} | Rekommenderas för användning med kärnkomponenter | [!BADGE Inte tillgänglig]{type=Negative} | Klassiska AEM-sidor är ofta beroende av flera funktioner som är svåra att kopiera som de är med den universella redigeraren. |
| [Edge Delivery](/help/edge/overview.md) | [!BADGE Inte tillgänglig]{type=Negative} |  | [!BADGE Tillgänglig]{type=Positive} |  |
| [Headless Delivery](/help/headless/introduction.md) | [!BADGE Delvis tillgänglig]{type=Caution} | Endast med [SPA-redigeraren,](/help/implementing/developing/hybrid/introduction.md) som [är inaktuellt](/help/implementing/developing/hybrid/spa-editor-deprecation.md) till förmån för den universella redigeraren | [!BADGE Tillgänglig]{type=Positive} | Med Universell redigerare kan utvecklare ta med sig ett eget webbprogram utan att införa några specifika ramverkskrav eller implementeringsbegränsningar. |

### Persistence {#persistence}

|  | Page Editor | Anteckning | Universal Editor | Anteckningar |
|---|---|---|---|---|
| Redigera sidkomponenter | [!BADGE Tillgänglig]{type=Positive} |  | [!BADGE Tillgänglig]{type=Positive} |  |
| Redigera [innehållsfragment](/help/assets/content-fragments/content-fragments.md) | [!BADGE Inte tillgänglig]{type=Negative} |  | [!BADGE Tillgänglig]{type=Positive} | Inkludera infogning av nya och sortering av fragment |

### Funktioner {#capabilities}

|  | Page Editor | Anteckning | Universal Editor | Anteckningar |
|---|---|---|---|---|
| Sidmallar | [!BADGE Tillgänglig]{type=Positive} |  | [!BADGE Tillgänglig]{type=Positive} | Universal Editor känner inte av vilket mallsystem som används. Det typiska implementeringsmönstret prioriterar dock mallar som definierats av utvecklare, eftersom moderna frontend-verktyg gör det mycket enklare för utvecklare att definiera och underhålla malllogik direkt i koden. |
| WYSIWYG Editing | [!BADGE Tillgängligt]{type=Positive} Begränsat till sidor |  | [!BADGE Tillgänglig]{type=Positive} | Stödsidor och innehållsfragment |
| [Generera variationer](/help/generative-ai/generate-variations.md) | [!BADGE Inte tillgänglig]{type=Negative} |  | [!BADGE Tillgänglig]{type=Positive} | [Tillgängligt som tillägg](/help/implementing/universal-editor/extending.md) |
| Infoga nytt block | [!BADGE Tillgänglig]{type=Positive} |  | [!BADGE Tillgänglig]{type=Positive} |  |
| Ordna om block | [!BADGE Tillgänglig]{type=Positive} | Möjligt med dra-och-släpp i sitt sammanhang, men inte i sidopanelen i trädvyn | [!BADGE Tillgänglig]{type=Positive} | Möjligt via dra-och-släpp i sidopanelen &quot;Trädvy&quot;, men inte i sitt sammanhang (planerat) |
| Klipp ut/kopiera/klistra in block | [!BADGE Tillgänglig]{type=Positive} |  | [!BADGE Inte tillgänglig]{type=Negative} | Planerad |
| Använd format | [!BADGE Tillgänglig]{type=Positive} | Format kan användas på komponenter med [Style System.](/help/sites-cloud/authoring/page-editor/style-system.md) | [!BADGE Tillgänglig]{type=Positive} | Du kan använda format med vanliga komponentegenskaper (eller Content Fragment). Samma formatväljare är inte tillgänglig i Universal Editor, men om du använder en flervalswidget kan du uppnå ett mycket liknande användargränssnitt. |
| Använd layout | [!BADGE Tillgänglig]{type=Positive} | Webbplatser måste implementera [AEM responsiva stödraster](/help/implementing/developing/introduction/responsive-design.md) för att författare ska kunna ändra storlek på komponenter över tre fördefinierade brytpunkter. | [!BADGE Tillgänglig]{type=Positive} | Layouter kan användas med vanliga komponentegenskaper (eller Content Fragment), men det responsiva stödrastret stöds inte. |
| Ångra-Gör om | [!BADGE Tillgänglig]{type=Positive} |  | [!BADGE Inte tillgänglig]{type=Negative} | Planerad |
| Publicera (även för förhandsgranskning) | [!BADGE Tillgänglig]{type=Positive} |  | [!BADGE Tillgänglig]{type=Positive} |  |
| [Starta arbetsflöde](/help/sites-cloud/authoring/workflows/overview.md) | [!BADGE Tillgänglig]{type=Positive} |  | [!BADGE Tillgänglig]{type=Positive} | Tillgängligt som tillägg |
| Kommentarer | [!BADGE Tillgänglig]{type=Positive} | Använda [anteckningar](/help/sites-cloud/authoring/page-editor/annotations.md) | [!BADGE Inte tillgänglig]{type=Negative} | Planerad |
| Integrering med Workfront | [!BADGE Inte tillgänglig]{type=Negative} |  | [!BADGE Tillgänglig]{type=Positive} | Tillgängligt som tillägg |
| [MSM och startprogram](/help/sites-cloud/administering/msm-and-translation.md) | [!BADGE Tillgänglig]{type=Positive} |  | [!BADGE Tillgänglig]{type=Positive} | Tillgängligt för sidor som tillägg |
| Experimentera och personalisera | [!BADGE Tillgänglig]{type=Positive} | Använder [målläge](/help/sites-cloud/authoring/personalization/targeted-content.md) | [!BADGE Tillgänglig]{type=Positive} | Finns som tillägg för Edge Delivery Services |
| Innehållsträd | [!BADGE Tillgänglig]{type=Positive} |  | [!BADGE Tillgänglig]{type=Positive} | Det går även att ändra ordning i trädet |
| Enhetssimulering | [!BADGE Tillgänglig]{type=Positive} | [Konfigurerade enheter kan simuleras,](/help/sites-cloud/administering/responsive-layout.md), men användaren kan inte ange några olika skärmdimensioner att simulera manuellt. | [!BADGE Tillgänglig]{type=Positive} | [Alla skärmdimensioner som ska simuleras kan anges manuellt,](/help/sites-cloud/authoring/universal-editor/navigation.md#emulator), men standardbrytpunkter kan inte konfigureras. |
| [Sidlåsning](/help/sites-cloud/authoring/sites-console/managing-pages.md) | [!BADGE Tillgänglig]{type=Positive} |  | [!BADGE Tillgänglig]{type=Positive} | Respterar låsstatus som angetts i Sites Console med tillägg för att låsa/låsa upp sidor från redigeraren |
| [Sidegenskaper](/help/sites-cloud/authoring/sites-console/page-properties.md) | [!BADGE Tillgänglig]{type=Positive} |  | [!BADGE Tillgänglig]{type=Positive} | Tillgängligt från Webbplatsadministratör, med tillägg för att även komma åt egenskaper för sidor från redigeraren |
| Egenskaper för flera fält | [!BADGE Tillgänglig]{type=Positive} |  | [!BADGE Inte tillgänglig]{type=Negative} | Planerad |
| [Fjärr-DAM](/help/assets/dynamic-media-open-apis-overview.md) | [!BADGE Tillgänglig]{type=Positive} |  | [!BADGE Tillgänglig]{type=Positive} |  |
| [Sidversionshantering](/help/sites-cloud/authoring/sites-console/page-versions.md) | [!BADGE Tillgänglig]{type=Positive} |  | [!BADGE Tillgänglig]{type=Positive} |  |
| [TimeWarp](/help/sites-cloud/authoring/sites-console/page-versions.md#timewarp) och [Diff-vy](/help/sites-cloud/authoring/sites-console/page-diff.md) | [!BADGE Tillgänglig]{type=Positive} |  | [!BADGE Inte tillgänglig]{type=Negative} | Planerad |
| Visa i administratör | [!BADGE Tillgänglig]{type=Positive} |  | [!BADGE Tillgänglig]{type=Positive} | Tillgängligt som tillägg för sidor |
| Visa sidstatus | [!BADGE Tillgänglig]{type=Positive} |  | [!BADGE Inte tillgänglig]{type=Negative} | Finns i webbplatskonsolen |
| Utbyggbarhet | [!BADGE Tillgänglig]{type=Positive} | Som AEM-övertäckningar | [!BADGE Tillgänglig]{type=Positive} | Som tydligt definierade tilläggspunkter med App Builder och mycket liten AEM-specifik kunskap |

## Använda den universella redigeraren {#adopt-ue}

Den universella redigeraren har många fördelar och är därför en utmärkt lösning för nya projekt.

* **Visuell redigering:** Precis som för sidredigeraren kan författare redigera innehåll direkt i förhandsgranskningen och omedelbart se hur ändringarna påverkar besökarupplevelsen.
* **Framtidsgranskning:** AEM färdplan prioriterar den universella redigeraren som visuell redigerare. Genom att använda det får du tillgång till de senaste innovationerna och förbättringarna.
* **Förenklad integrering:** Det krävs ingen AEM-specifik SDK för att använda den universella redigeraren, vilket reducerar tilllåsning av högtalarsystem.
* **Använd din egen app:** Den universella redigeraren har stöd för alla webbramverk och -arkitekturer, vilket gör att du kan börja använda programmet utan att behöva göra en komplex omfaktorisering.
* **Utbyggbarhet:** Den universella redigeraren drar nytta av ett robust [tilläggsramverk,](/help/implementing/universal-editor/extending.md) inklusive integreringar med GenAI, Workfront med flera.

### Migrera till Universal Editor {#migrate-ue}

Det finns ingen direkt migreringssökväg från sidredigeraren till den universella redigeraren. Detta beror på de två teknikernas grundläggande skillnader.

* Den universella redigeraren återinför inte funktioner som mallredigeraren, formatsystemet eller det responsiva stödrastret.
   * De här användningsområdena kan nu hanteras effektivare med tunn frontend-CSS och Javascript i Edge Delivery Services eller headless-projekt.
* Eftersom den universella redigeraren är en redigerare som en tjänst kan den inte tillåta att implementerare injicerar CSS eller JS i komponentdialogrutorna.
   * Detta förhindrar automatisk konvertering av komponentdialogrutor från sidredigeraren.
   * Detta påverkar många områden i dialogrutorna, t.ex. anpassade widgetar, fältvalidering, visa/dölj regler och mallbaserade anpassningar.
      * Dessa funktioner är fortfarande möjliga, men i Universell redigerare löses de genom konfiguration i stället för att JavaScript distribueras i dialogrutor.

Medan Universell redigerare tekniskt kan aktivera redigering för klassiska AEM-sidor (t.ex. skapade med Core Components), är dessa webbplatser vanligtvis beroende av flera funktioner som är specifika för sidredigeraren, t.ex. Style System, Responsive Grid, Editable Templates och anpassad JavaScript i dialogrutor.

Eftersom den universella redigeraren följer ett mer strömlinjeformat, modernt arbetssätt som inte har stöd för dessa äldre funktioner, behöver du omfaktorisera om du migrerar sådana webbplatser. Därför bör **du bara migrera sidredigeringswebbplatser till den universella redigeraren för projekt som övergår till Edge Delivery Services.**
