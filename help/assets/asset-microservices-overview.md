---
title: Bearbeta resurser med hjälp av mikrotjänster för resurser
description: Bearbeta era digitala resurser med molnbaserade och skalbara mikrotjänster för bearbetning av resurser.
contentOwner: AG
feature: Asset Compute Microservices, Asset Ingestion, Asset Processing
role: Developer, Admin
exl-id: 1e069b95-a018-40ec-be01-9a74ed883b77
source-git-commit: ff06dbd86c11ff5ab56b3db85d70016ad6e9b981
workflow-type: tm+mt
source-wordcount: '837'
ht-degree: 0%

---

# Översikt över intag och hantering av tillgångar med hjälp av mikrotjänster {#asset-microservices-overview}

Adobe Experience Manager som [!DNL Cloud Service] tillhandahåller en molnbaserad metod för att använda Experience Manager-program och -funktioner. En av de viktigaste komponenterna i den nya arkitekturen är att man får in och bearbetar material med hjälp av mikrotjänster. Resursmikrotjänsterna erbjuder en skalbar och flexibel bearbetning av resurser med hjälp av molntjänster. Adobe hanterar molntjänsterna för optimal hantering av olika resurstyper och bearbetningsalternativ. De viktigaste fördelarna med molnbaserade resurstjänster är:

* Skalbar arkitektur som möjliggör smidig bearbetning för resurskrävande åtgärder.
* Effektiv indexering och textextrahering som inte påverkar Experience Manager-miljöernas prestanda.
* Minimera behovet av arbetsflöden för att hantera resursbearbetning i Experience Manager-miljön. Detta frigör resurser, minimerar belastningen på Experience Manager och ger skalbarhet.
* Förbättrad flexibilitet i bearbetningen av resurser. Potentiella problem vid hantering av atypiska filer, som skadade filer eller extremt stora filer, påverkar inte längre distributionens prestanda.
* Förenklad konfiguration av tillgångsbearbetning för administratörer.
* Installationen av Assets-bearbetningen hanteras och underhålls av Adobe för att ge bästa möjliga konfiguration för hantering av återgivningar, metadata och textrahering för olika filtyper
* Adobe filbehandlingstjänster används där det är tillämpligt, vilket ger exakt återgivning och [effektiv hantering av Adobe egna format](file-format-support.md).
* Möjlighet att konfigurera efterbehandlingsarbetsflöden för att lägga till användarspecifika åtgärder och integreringar.

Resursmikrotjänster hjälper till att undvika behovet av återgivningsverktyg och -metoder från tredje part (som [!DNL ImageMagick] och FMPEG-omkodning) och förenklar konfigurationer, samtidigt som de tillhandahåller grundläggande funktioner för vanliga filformat som standard.

## Arkitektur på hög nivå {#asset-microservices-architecture}

Ett arkitekturdiagram på hög nivå visar de viktigaste elementen när det gäller tillgångsintag, bearbetning och flöde av resurser i hela systemet.

<!-- Proposed DRAFT diagram for asset microservices overview - see section "Asset processing - high-level diagram" in the PPTX deck

https://adobe-my.sharepoint.com/personal/gklebus_adobe_com/_layouts/15/guestaccess.aspx?guestaccesstoken=jexDC5ZnepXSt6dTPciH66TzckS1BPEfdaZuSgHugL8%3D&docid=2_1ec37f0bd4cc74354b4f481cd420e07fc&rev=1&e=CdgElS
-->

![Tillgångsinmatning och bearbetning med tillgångsmikrotjänster](assets/asset-microservices-overview.png "Tillgångsinmatning och bearbetning med tillgångsmikrotjänster")

De viktigaste stegen för intag och bearbetning med hjälp av tillgångsmikrotjänster är:

* Klienter, som webbläsare eller Adobe Asset Link, skickar en överföringsbegäran till [!DNL Experience Manager] och börjar överföra binärfilen direkt till det binära molnlagringsutrymmet.
* När den direkta binära överföringen har slutförts meddelar klienten [!DNL Experience Manager].
* [!DNL Experience Manager] skickar en bearbetningsbegäran till resursens mikrotjänster. Innehållet i begäran beror på den konfiguration av bearbetningsprofiler i [!DNL Experience Manager] som anger vilka återgivningar som ska genereras.
* Resursmikrotjänsterna tar emot begäran och skickar den till en eller flera mikrotjänster baserat på begäran. Varje mikrotjänst får åtkomst till den ursprungliga binärfilen direkt från den binära molnbutiken.
* Resultaten av bearbetningen, t.ex. renderingar, lagras i det binära molnlagringsutrymmet.
* Experience Manager får ett meddelande om att bearbetningen har slutförts tillsammans med direktpekare till de genererade binärfilerna (renderingar). De genererade återgivningarna är tillgängliga i [!DNL Experience Manager] för den överförda resursen.

Detta är det grundläggande flödet av tillgångsintag och bearbetning. Om den är konfigurerad kan Experience Manager även starta en anpassad arbetsflödesmodell för att utföra efterbearbetning av resursen. Du kan till exempel utföra anpassade steg som är specifika för din miljö, som att hämta information från ett företagssystem och lägga till i resursegenskaper.

Insug- och bearbetningsflödet är nyckelbegrepp för resursmikrotjänstens arkitektur för Experience Manager.

* **Direkt binär åtkomst**: Assets transporteras (och överförs) till Cloud Binary Store när den har konfigurerats för Experience Manager-miljöer, och sedan [!DNL Experience Manager] får resursmikrotjänster och slutligen klienter direktåtkomst till dem för att utföra sitt arbete. Detta minimerar belastningen på nätverk och duplicering av lagrade binärfiler
* **Extern bearbetning**: Bearbetning av resurser utförs utanför [!DNL Experience Manager]-miljön och sparar resurser (CPU, minne) för att tillhandahålla viktiga DAM-funktioner (Digital Asset Management) och stöd för interaktivt arbete med systemet för slutanvändare

## Tillgångsuppladdning med direkt binär åtkomst {#asset-upload-with-direct-binary-access}

Experience Manager-klienter, som ingår i produkterbjudandet, har som standard stöd för uppladdning med direkt binär åtkomst. Dessa inkluderar överföring via webbgränssnitt, Adobe Asset Link och skrivbordsappen [!DNL Experience Manager].

Du kan använda anpassade överföringsverktyg, som fungerar direkt med [!DNL Experience Manager] HTTP API:er. Du kan använda dessa API:er direkt eller använda och utöka följande öppen källkodsprojekt som implementerar överföringsprotokollet:

* [Överföringsbibliotek med öppen källkod](https://github.com/adobe/aem-upload)
* [Kommandoradsverktyget för öppen källkod](https://github.com/adobe/aio-cli-plugin-aem)

Mer information finns i [Överför resurser](add-assets.md).

## Lägg till efterbearbetning av anpassade resurser {#add-custom-asset-post-processing}

De flesta kunder bör få alla sina behov av tillgångsbearbetning från de konfigurerbara tillgångsmikrotjänsterna, men vissa kan behöva ytterligare bearbetning av resurser. Detta gäller särskilt om resurser behöver bearbetas baserat på information som kommer från andra system via integreringar. I sådana fall kan anpassade efterbearbetningsarbetsflöden användas.

Efterbehandlingsarbetsflöden är vanliga [!DNL Experience Manager] arbetsflödesmodeller, som skapas och hanteras i [!DNL Experience Manager] Arbetsflödesredigeraren. Kunderna kan konfigurera arbetsflödena så att de kan utföra ytterligare bearbetningssteg för en mediefil, inklusive använda tillgängliga körklara arbetsflödessteg och anpassade arbetsflöden.

Adobe Experience Manager kan konfigureras så att efterbearbetningen av arbetsflöden automatiskt startar när bearbetningen av materialet har slutförts.

<!-- TBD asgupta, Engg: Create some asset-microservices-data-flow-diagram.
-->

**Se även**

* [Översätt Assets](translate-assets.md)
* [ASSETS HTTP API](mac-api-assets.md)
* [Filformat som stöds av Assets](file-format-support.md)
* [Sök resurser](search-assets.md)
* [Anslutna resurser](use-assets-across-connected-assets-instances.md)
* [Resursrapporter](asset-reports.md)
* [Metadata-scheman](metadata-schemas.md)
* [Hämta resurser](download-assets-from-aem.md)
* [Hantera metadata](manage-metadata.md)
* [Sök efter ansikten](search-facets.md)
* [Hantera samlingar](manage-collections.md)
* [Import av massmetadata](metadata-import-export.md)
* [Publicera Assets till AEM och Dynamic Media](/help/assets/publish-assets-to-aem-and-dm.md)

>[!MORELIKETHIS]
>
>* [Komma igång med mikrotjänster för material](asset-microservices-configure-and-use.md)
>* [Filformat som stöds](file-format-support.md)
>* [Adobe Asset Link](https://helpx.adobe.com/enterprise/using/adobe-asset-link.html)
>* [[!DNL Experience Manager] skrivbordsapp](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/introduction.html)
>* [Apache Oak-dokumentation om direkt binär åtkomst](https://jackrabbit.apache.org/oak/docs/features/direct-binary-access.html)
