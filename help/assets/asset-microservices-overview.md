---
title: Se hur Assets microservices kan bearbeta dina digitala resurser i molnet
description: Bearbeta era digitala resurser med molnbaserade och skalbara mikrotjänster för bearbetning av resurser.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0686acbc61b3902c6c926eaa6424828db0a6421a

---


# Översikt över intag och hantering av tillgångar med hjälp av mikrotjänster {#asset-microservices-overview}

<!--
First half of content at https://git.corp.adobe.com/aklimets/project-nui/blob/master/docs/Project-Nui-Asset-Compute-Service.md is useful for this article.
TBD: Post-GA we will provide detailed information at \help\assets\asset-microservices-configure-and-use.md. However, for GA, all information is added, in short, in this article.
-->

Adobe Experience Manager som molntjänst är en molnbaserad metod för att utnyttja Experience Manager-program och -funktioner. En av de viktigaste komponenterna i den nya arkitekturen är att man får in och bearbetar material med hjälp av mikrotjänster. Resursmikrotjänsterna erbjuder en skalbar och flexibel bearbetning av resurser med hjälp av molntjänster. Adobe hanterar molntjänsterna för optimal hantering av olika resurstyper och bearbetningsalternativ. De viktigaste fördelarna med molnbaserade resurstjänster är:

* Skalbar arkitektur som möjliggör smidig bearbetning för resurskrävande åtgärder.
* Effektiv indexering och textextrahering som inte påverkar prestandan i Experience Manager-miljöerna.
* Minimera behovet av arbetsflöden för att hantera resursbearbetning i Experience Manager-miljön. Detta frigör resurser, minimerar belastningen på Experience Manager och ger skalbarhet.
* Förbättrad flexibilitet i bearbetningen av resurser. Potentiella problem vid hantering av atypiska filer, som skadade filer eller extremt stora filer, påverkar inte längre distributionens prestanda.
* Förenklad konfiguration av tillgångsbearbetning för administratörer.
* Resurshanteringsinställningarna hanteras och underhålls av Adobe för att ge bästa möjliga konfiguration för hantering av återgivningar, metadata och textredigering för olika filtyper
* Adobes filbehandlingstjänster används där det är tillämpligt, vilket ger exakt återgivning och [effektiv hantering av Adobes egna format](file-format-support.md).
* Möjlighet att konfigurera efterbehandlingsarbetsflöden för att lägga till användarspecifika åtgärder och integreringar.

Resursmikrotjänster hjälper till att undvika behovet av verktyg och metoder för återgivning från tredje part (som ImageMagick och FMPEG-omkodning) och förenklar konfigurationer, samtidigt som de ger körklara funktioner för vanliga filtyper.

## Arkitektur på hög nivå {#asset-microservices-architecture}

Ett arkitekturdiagram på hög nivå visar de viktigaste elementen när det gäller tillgångsintag, bearbetning och flöde av resurser i hela systemet.

<!-- Proposed DRAFT diagram for asset microservices overview - see section "Asset processing - high-level diagram" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![Tillgång till och hantering av tillgångar med](assets/asset-microservices-overview.png "mikrotjänsterTillgång och hantering av tillgångar med mikrotjänster")

De viktigaste stegen för intag och bearbetning med hjälp av tillgångsmikrotjänster är:

* Klienter, som webbläsare eller Adobe Asset Link, skickar en överföringsbegäran till Experience Manager och börjar överföra binärfilen direkt till det binära molnlagringsutrymmet.
* När den direkta binära överföringen har slutförts meddelar klienten Experience Manager.
* Experience Manager skickar en bearbetningsbegäran till resursens mikrotjänster. Innehållet i begäran beror på vilken bearbetningsprofilskonfiguration i Experience Manager som anger vilka återgivningar som ska genereras.
* Resurserna för mikrotjänster tar emot begäran och skickar den till en eller flera mikrotjänster baserat på begäran. Varje mikrotjänst får åtkomst till den ursprungliga binärfilen direkt från den binära molnbutiken.
* Resultaten av bearbetningen, t.ex. renderingar, lagras i det binära molnlagringsutrymmet.
* Experience Manager meddelas om att bearbetningen är klar tillsammans med direktpekare till de genererade binärfilerna (återgivningar). De genererade återgivningarna är tillgängliga i Experience Manager för den överförda resursen.

Detta är det grundläggande flödet av tillgångsintag och bearbetning. Om den är konfigurerad kan Experience Manager även starta en anpassad arbetsflödesmodell för att utföra efterbearbetning av resursen. Du kan till exempel utföra anpassade steg som är specifika för din miljö, som att hämta information från ett företagssystem och lägga till i resursegenskaper.

Intag och bearbetningsflöde är viktiga begrepp i resursens mikrotjänstarkitektur för Experience Manager.

* **Direkt binär åtkomst**: Resurser transporteras (och överförs) till molnbinärarkivet när de har konfigurerats för Experience Manager-miljöer, och sedan får AEM, Assets microservices och slutligen klienterna direktåtkomst för att utföra sitt arbete. Detta minimerar belastningen på nätverk och duplicering av lagrade binärfiler
* **Extern bearbetning**: Bearbetning av resurser görs utanför AEM-miljön och sparar resurser (CPU, minne) för att tillhandahålla viktiga funktioner för hantering av digitala resurser samt stöd för interaktivt arbete med systemet för slutanvändare

## Tillgångsuppladdning med direkt binär åtkomst {#asset-upload-with-direct-binary-access}

Experience Manager-klienter, som ingår i ett produkterbjudande, har som standard stöd för överföring med direkt binär åtkomst. Dessa inkluderar överföring via webbgränssnitt, Adobe Asset Link och AEM-datorprogrammet.

Du kan använda anpassade överföringsverktyg, som fungerar direkt med AEM HTTP API:er. Du kan använda dessa API:er direkt eller använda och utöka följande öppen källkodsprojekt som implementerar överföringsprotokollet:

* [Överföringsbibliotek med öppen källkod](https://github.com/adobe/aem-upload)
* [Kommandoradsverktyg med öppen källkod](https://github.com/adobe/aio-cli-plugin-aem)

Mer information finns i [Överföra resurser](add-assets.md).

## Lägg till efterbearbetning av anpassade resurser {#add-custom-asset-post-processing}

De flesta kunder bör få alla sina behov av tillgångsbearbetning från de konfigurerbara tillgångsmikrotjänsterna, men vissa kan behöva ytterligare bearbetning av resurser. Detta gäller särskilt om resurser behöver bearbetas baserat på information som kommer från andra system via integreringar. I sådana fall kan anpassade efterbearbetningsarbetsflöden användas.

Efterbehandlingsarbetsflöden är vanliga arbetsflödesmodeller för AEM, som skapas och hanteras i AEM Workflow Editor. Kunderna kan konfigurera arbetsflödena så att de kan utföra ytterligare bearbetningssteg för en mediefil, inklusive använda tillgängliga körklara arbetsflödessteg och anpassade arbetsflöden.

Adobe Experience Manager kan konfigureras så att efterbearbetningen av arbetsflöden automatiskt startar när bearbetningen av resurser har slutförts.

<!-- TBD asgupta, Engg: Create some asset-microservices-data-flow-diagram.
-->

>[!MORELIKETHIS]
>
>* [Komma igång med mikrotjänster för material](asset-microservices-configure-and-use.md)
>* [Filformat som stöds](file-format-support.md)
>* [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)
>* [AEM-skrivbordsapp](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/introduction.html)
>* [Apache Oak-dokumentation om direkt binär åtkomst](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html)

