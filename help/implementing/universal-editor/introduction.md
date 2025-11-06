---
title: Introduktion till Universal Editor
description: Universal Editor är ett modernt visuellt redigeringsverktyg som ger er möjlighet att skapa slagkraftiga webbupplevelser.
exl-id: d4fc2384-a0f5-4a6f-9572-62749786be4c
feature: Developing
role: Admin, Developer
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 0%

---


# Introduktion till Universal Editor {#introduction}

Universal Editor är ett modernt visuellt redigeringsverktyg som ger er möjlighet att skapa slagkraftiga webbupplevelser.

## Ökning {#overview}

Universal Editor är en mångsidig visuell editor som ingår i Adobe Experience Manager Sites. Man kan redigera det man redan gjort i WYSIWYG utan att behöva ta del av en massa rubriker. Det erbjuder:

* **Direktredigering**: Författare kan redigera innehåll direkt i förhandsgranskningen, vilket eliminerar behovet av att hitta och navigera till enskilda innehållskällor.
* **Visuell redigering**: När författare gör ändringar ser de direkt hur de påverkar besökarupplevelsen, vilket minimerar friktionen.
* **Alternativ som kan upptäckas**: Alternativ med tydliga etiketter och ett intuitivt användargränssnitt gör det enkelt för författare att konfigurera metadata och skapa layouter.
* **Icke-teknisk**: Ingen specialexpertis krävs för att göra ändringar, medan företagets varumärkesriktlinjer tillämpas automatiskt, vilket underlättar skalningen av innehållsuppgifter i hela organisationen.
* **Integrering och utbyggbarhet**: Integrerat med AEM, den universella redigerarens flexibla [utökningspunkter](#extensibility), gör att alla nödvändiga verktyg kan förenas i ett enda, sammanhängande gränssnitt. Med allt från AI-baserade funktioner till anpassade tillägg som är skräddarsydda för just era affärsbehov kan teamen smidigt effektivisera arbetsflödena och enkelt förbättra produktiviteten.

Sammanfattning:

* **Författare har nytta** av den universella redigerarens flexibilitet eftersom den har stöd för samma enhetliga visuella redigering för alla former av AEM-innehåll.
* **Utvecklare** drar nytta av den universella redigerarens mångsidighet eftersom den stöder en sann frikoppling av implementeringen.

Den universella redigeraren är en riktig redigerare som en tjänst och är generellt mer flexibel. Den kommer till slut att ersätta [sidredigeraren.](/help/sites-cloud/authoring/page-editor/introduction.md)

## Arkitekturer som stöds {#supported-architectures}

Universal Editor stöder följande två primära AEM-inställningar:

1. **[Edge Delivery Services](/help/edge/overview.md)**: Det här är det rekommenderade tillvägagångssättet för enkelhet, snabbare time-to-value och förbättrade prestanda.
1. **[Headless-implementeringar](/help/headless/introduction.md)**: Om du har ett headless-projekt eller specifika krav för frikopplad återgivning tillåter den universella redigeraren visuell redigering i företagsklass utan att du behöver omforma hela projektet. Den är kompatibel med praktiskt taget alla arkitekturer (SSR, CSR), webbramverk (Next.js, React, Astro osv.) och värdmodeller (&quot;ta med din egen app&quot;).

>[!TIP]
>
>Mer information om vilka arkitekturer som stöds finns i dokumentet [Universal Editor Use Case and Learning Paths](/help/implementing/universal-editor/use-cases.md).

## AEM-versioner som stöds {#aem-versions}

Universal Editor stöds av:

* AEM as a Cloud Service (version `2023.8.13099` eller senare)
* [AEM 6.5 LTS](https://experienceleague.adobe.com/sv/docs/experience-manager-65-lts/content/implementing/developing/headless/universal-editor/introduction)
   * Både lokala värdtjänster och AMS-värdtjänster stöds.
* [AEM 6.5](https://experienceleague.adobe.com/sv/docs/experience-manager-65/content/implementing/developing/headless/universal-editor/introduction)
   * Både lokala värdtjänster och AMS-värdtjänster stöds.

Den här dokumentationen används för Universal Editor med AEM as a Cloud Service.

## Funktioner {#features}

Den universella redigeraren har många funktioner som kan användas i många olika syften för effektiv innehållshantering.

* **[WYSIWYG](/help/sites-cloud/authoring/universal-editor/authoring.md)**: Utför vad-du-see-is-what-you-get-redigering av alla typer av webbinnehåll, inklusive oformaterad text, formaterad text, media och metadata.
* **[Disposition](/help/sites-cloud/authoring/universal-editor/authoring.md#editing-content)**: Skapa, redigera, ordna om, kapsla in eller ta bort innehållsblock av olika typer (titlar, knappar, tassar, avsnitt, bädda in osv.).
* **[Layout](/help/sites-cloud/authoring/universal-editor/templates.md)**: Använd sidmallar, använd visuella format och komponera layouter med block som kolumner, carousel och dragspelspaneler.
* **[Enhetssimulering](/help/sites-cloud/authoring/universal-editor/navigation.md#emulator)**: Förhandsgranska och optimera innehåll för olika besökarenheter under redigering.
* **Omnichannel**: Återanvänd både strukturerat och ostrukturerat innehåll i flera kanaler.
* **[Lokalisering](/help/sites-cloud/authoring/universal-editor/inheritance.md)**: Effektivisera arbetsflödena för översättning av innehåll och hantera effektivt översatt innehåll med Multi-Site Manager.
* **Konsekvens**: Säkerställ överensstämmelse med varumärkesriktlinjerna och bibehåll enhetligheten i allt innehåll.
* **Säkerhet**: [Använd åtkomstkontroll](/help/implementing/universal-editor/authentication.md), skydda innehållets integritet och spåra ändringar med [robust versionshantering.](/help/sites-cloud/authoring/sites-console/page-versions.md)
* **[Publicering](/help/sites-cloud/authoring/universal-editor/publishing.md)**: Integrera arbetsflöden för granskning, godkännande och publicering direkt i redigeraren.
* **Enhetlig**: Integreras fullt ut med AEM-verktyg som [Sites Console,](/help/sites-cloud/authoring/sites-console/introduction.md) [Content Fragment Editor,](/help/sites-cloud/administering/content-fragments/overview.md) och många andra, vilket ger en sammanhängande redigeringsupplevelse.

## Utbyggbarhet {#extensibility}

Den universella redigeraren har inte bara funktioner som är klara att användas direkt, utan erbjuder ett antal utbyggnadsmöjligheter.

* **Tillägg** är många och färdiga för att uppfylla krav som stöd för arbetsflöden, generering av variationer och experimenterande.
* **Med ett utökningsbart användargränssnitt** kan du skapa egna tillägg med samma underliggande ramverk som de färdiga tilläggen utnyttjar, vilket ger optimal flexibilitet att anpassa sig efter dina projektbehov.
* **Tilläggspunkter**, t.ex. block, anpassade datatyper och händelser, möjliggör smidig integrering av anpassade affärskrav utanför användargränssnittet.

>[!TIP]
>
>Mer information om den universella redigerarens utbyggbarhet finns i dokumentet [Utöka den universella redigeraren.](/help/implementing/universal-editor/extending.md)

## Universal Editor och Content Fragment Editor {#universal-editor-content-fragment-editor}

Vid första anblicken kan det verka som den universella redigeraren och Content Fragment Editor har liknande redigeringsfunktioner. Men de här redigerarna har mycket olika funktioner och de utför olika arbetsuppgifter för marknadsföringsavdelningen.

### Innehållsfragmentsredigerare {#content-fragment-editor}

En marknadsförare vill skapa innehåll utan att behöva bry sig om layouten, så att det kan återanvändas i många sammanhang av upplevelsen.

* Det underliggande jobbet är att skala innehållsstrategin.

### Universal Editor {#universal-editor}

En marknadsförare vill skapa innehåll som är skräddarsytt efter layouten i ett visst sammanhang för att leverera en exceptionell upplevelse.

* Det underliggande jobbet är att på ett övertygande sätt få kontakt med läsarna.

## Begränsningar {#limitations}

När du utforskar den universella redigeraren och fortsätter implementera den i dina egna projekt bör du tänka på följande begränsningar.

* Högst 25 AEM-resurser (Content Fragments, pages, Experience Fragments, Assets, etc.) får vara referenser som instrument på en enda sida.
* AEM as a Cloud Service, [AEM 6.5 LTS](https://experienceleague.adobe.com/sv/docs/experience-manager-65-lts/content/implementing/developing/headless/universal-editor/introduction) och [AEM 6.5](https://experienceleague.adobe.com/sv/docs/experience-manager-65/content/implementing/developing/headless/universal-editor/introduction) är de enda AEM-backends som stöds.
* Versionen `2023.8.13099` eller senare krävs för AEM as a Cloud Service.
* Innehållsförfattare måste ha sina egna Experience Cloud-konton.
* Som en del av AEM stöder den universella redigeraren [samma webbläsare som AEM.](/help/overview/supported-platforms.md)
   * Mobilversioner av dessa webbläsare stöds inte.

{{ip-allow-lists-ue}}

## Nästa steg {#next-steps}

Läs dokumentet [Universal Editor Use Case and Learning Paths](/help/implementing/universal-editor/use-cases.md) om du vill veta mer om vanliga användningsfall för Universal Editor och hitta rätt dokumentationsresurser för ditt projekt.
