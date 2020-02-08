---
title: Introduktion till arkitekturen för Adobe Experience Manager som en molntjänst
description: 'Introduktion till arkitekturen för Adobe Experience Manager som en molntjänst. '
translation-type: tm+mt
source-git-commit: 5a846d34ee094e7d2f7fc71dbeef65f3fa58e86c

---


# En introduktion till arkitekturen för Adobe Experience Manager som en molntjänst {#an-introduction-to-the-architecture-adobe-experience-manager-as-a-cloud-service}

Adobe Experience Manager (AEM) som molntjänst har resulterat i förändringar i arkitekturen.

## Skalning {#scaling}

AEM som molntjänst har nu:

* En dynamisk arkitektur med ett varierande antal AEM-bilder.

![Dynamisk](assets/concepts-01.png "arkitekturDynamisk arkitektur")

Arkitekturen:

* Skalas baserat på den *faktiska* trafiken och den *faktiska* aktiviteten.

* Har enskilda instanser som bara körs vid behov.

* Använder modulära program.

* Har ett författarkluster som standard; På så sätt undviker du driftavbrott för underhållsåtgärder.

Detta möjliggör autoskalning för olika användningsmönster:

![Automatisk skalning för olika](assets/concepts-02.png "användningsmönsterAutomatisk skalning för olika användningsmönster")

För att uppnå detta skapas alla instanser av AEM som en molntjänst som har samma standardstorleksegenskaper som antalet noder, allokerat minne och allokerad datorkapacitet.

AEM som molntjänst baseras på en orkestrationsmotor som

* Övervakar tjänstens tillstånd kontinuerligt.

* Skalar dynamiskt var och en av tjänstinstanserna efter de faktiska behoven. både skalning uppåt och nedåt.

Detta:

* Gäller för antalet noder, mängden minne och den allokerade processorkapaciteten på varje nod.

* Tillåter AEM som molntjänst att anpassa dina trafikmönster när de ändras.

Skalningen av tjänstens klientinstanser kan vara automatisk eller manuell på de två axlarna:

* Lodrätt: allokerat minne och processorkapacitet kan skalas upp eller ned för ett fast antal noder.

* Vågrät: antalet noder för en viss tjänst kan ökas eller minskas.

## Miljö {#environments}

>[!NOTE]
>
> Mer information finns i [Distribuera - Körningslägen](/help/implementing/deploying/overview.md#runmodes)

AEM som molntjänst är tillgängligt som enskilda instanser där varje instans representerar en komplett AEM-miljö. Det finns fyra typer av miljöer som är tillgängliga med AEM som molntjänst:

* **Produktionsmiljö**: är värd för de ansökningar som riktar sig till yrkesverksamma.

* **Scenmiljö**: är alltid kopplad till en enda produktionsmiljö i en 1:1-relation. Scenmiljön används för olika prestanda- och kvalitetstester innan ändringar i programmet överförs till produktionsmiljön.

* **Utvecklingsmiljö**: ger utvecklare möjlighet att implementera AEM-program under samma körningsförhållanden som scen- och produktionsmiljöerna.

* **Demonstrationsmiljö**: kan användas för utvärdering, demonstration, prototyper och utbildningsändamål.

Utvecklings- och demonstrationsmiljöerna kallas ofta för *icke-produktionsmiljöer* .

## Program {#programs}

Alla nya AEM-projekt är alltid bundna till exakt en specifik kodbas, där du kan lagra både konfiguration och anpassad kod för ditt projekt. Den här informationen lagras i en koddatabas som du kan nå via de vanliga Git-klienterna när nya program skapas.

Ett AEM-program är den behållare som innehåller:

|  Programelement |  Nummer |
|--- |--- |
| Koddatabas (Git) |  1 |
| Originalbild (platser eller resurser) |  1 |
| Scen- och produktionsmiljöuppsättning (1:1) | 0 eller 1 |
| Icke-produktionsmiljöer (utveckling eller demonstration) | 0 till N |
| Pipeline för varje miljö | 0 eller 1 |

Två typer av program är inledningsvis tillgängliga för AEM som molntjänst:

* AEM Cloud Sites Service

* AEM Cloud Assets Service

Båda dessa ger tillgång till ett antal funktioner. Författarnivån innehåller alla Sites- och Assets-funktioner för alla program, men Assets-programmen har som standard ingen publiceringsnivå.

## Runtime Architecture {#runtime-architecture}

Det finns olika huvudkomponenter i den nya arkitekturen:

<!--- needs reworking -->

![AEM som en molntjänst - Runtime](assets/concepts-03.png "ArchitectureAEM som en molntjänst - Runtime Architecture")

* För AEM Sites som en molntjänst:

   * Det finns fortfarande ett koncept för ett redigeringsskikt och ett publiceringsskikt för varje miljö (på en hög nivå).

   * Författarnivån består av två eller flera noder i ett enda författarkluster. Den skalas automatiskt beroende på redigeringsaktiviteten.

      * Innehållsförfattare/skapare loggar in på AEM-författarnivå för att skapa, redigera och hantera innehåll.

      * Inloggning på författarnivå hanteras av Adobe Identity Management Services (IMS).

      * Integrering och bearbetning av resurser använder en dedikerad resurshanteringstjänst.
   * Publiceringsnivån består av två eller flera noder i en enda publiceringsgrupp: de kan fungera oberoende av varandra. Varje nod består av en AEM-utgivare och en webbserver utrustad med modulen AEM Dispatcher. Den skalas automatiskt efter behov av platstrafik.

      * Slutanvändare, eller besökare på webbplatsen, via AEM Publish Service.


* För AEM Assets som en molntjänst:

   * Arkitekturen innehåller endast en redigeringsmiljö.

* Både författarnivån och publiceringsnivån läser och behåller innehåll från/till en innehållslagringstjänst.

   * Publiceringsnivån läser bara innehåll från det beständiga lagret.

   * Författarnivån läser och skriver innehåll från och till det beständiga lagret.

   * BLOB-lagringen delas mellan publicerings- och författarnivå. filer *flyttas* inte.

   * När innehåll godkänns från författarnivån är detta en indikation på att det kan aktiveras och därför skickas till publiceringsskiktets beständiga lager. Detta sker via replikeringstjänsten, en pipeline för mellanvara. Detta tillvägagångssätt tar emot det nya innehållet, där de enskilda publiceringstjänstnoderna prenumererar på det innehåll som skickas till pipeline.

      >[!NOTE]
      >
      >For more details see [Replication](/help/operations/replication.md).

   * Utvecklare och administratörer hanterar AEM som en molntjänst genom att använda en CI/CD-tjänst (Continuous Integration/Continuous Delivery) som är tillgänglig via [Cloud Manager](/help/overview/what-is-new-and-different.md#cloud-manager). Detta inkluderar kod- och konfigurationsdistributioner med Cloud Managers CI/CD-pipeline. Allt som rör övervakning, underhåll och felsökning (till exempel loggfiler) visas för kunder i Cloud Manager.

   * Åtkomst till författar- och publiceringsnivåer sker alltid via en belastningsutjämnare. Detta är alltid uppdaterat med de aktiva noderna i varje lager.

   * För publiceringsnivån är en CDN-tjänst (Continuous Delivery Network) också tillgänglig som första startpunkt.

* För demonstrationsinstanser av AEM som en molntjänst förenklas arkitekturen till en enda författarnod. Därför presenterar den inte alla egenskaper hos standardutvecklingsmiljö, stadium eller produktionsmiljö. Det innebär också att det kan finnas vissa driftavbrott och att det inte finns stöd för säkerhetskopierings-/återställningsåtgärder.

## Driftsättningsarkitektur {#deployment-architecture}

Cloud Manager hanterar alla uppdateringar av AEM-instanserna som en molntjänst. Det är obligatoriskt, det enda sättet att bygga, testa och distribuera kundapplikationen, till både författaren och publiceringsnivån. Uppdateringarna kan aktiveras av Adobe när en ny version av AEM Cloud-tjänsten är klar, eller av kunden när en ny version av programmet är klar.

Tekniskt sett genomförs detta på grund av konceptet med en driftsättningspipeline som är kopplad till varje miljö i ett program. När en pipeline för Cloud Manager körs skapas en ny version av kundprogrammet, både för författaren och publiceringsskikten. Detta uppnås genom att kombinera de senaste kundpaketen med den senaste Adobe-bilden som baslinje. När de nya bilderna har byggts och testats automatiserar Cloud Manager helt klippet till den senaste versionen av bilden genom att uppdatera alla tjänstnoder med ett rullande uppdateringsmönster. Detta medför inga driftavbrott för författaren eller publiceringstjänsten.

<!--- needs reworking -->

![AEM som en molntjänst -](assets/concepts-04.png "distributionsarkitekturAEM som en molntjänst - distributionsarkitektur")

## Innehållsdistribution {#content-distribution}

Adobe Experience Manager som molntjänst har ändrat det sätt på vilket publiceringsinnehåll fungerar. Med AEM som molntjänst används inte längre replikeringsramverket från tidigare versioner av AEM för att publicera sidor (flytta ändringar från författarinstans till publiceringsinstanser).

AEM som molntjänst använder nu funktionen för [delning av innehållsdistribution](https://sling.apache.org/documentation/bundles/content-distribution.html) för att flytta rätt innehåll. Detta använder en pipeline-tjänst som körs på Adobe I/O, som ligger utanför AEM-miljön.

Installationen är automatiserad, inklusive automatisk självkonfigurering när publiceringsnoder läggs till, tas bort eller återanvänds under körning.

En enda begäran om publicering eller avpublicering kan innehålla flera resurser, men returnerar en enda status som gäller för alla. det fungerar för alla resurser i AEM Publish Service, eller misslyckas för alla. Detta garanterar att resurserna i AEM Publish Service aldrig kommer att vara i ett inkonsekvent läge.

**Arkitekturdiagram för innehållsdistribution på hög nivå**

![Arkitekturdiagram](assets/architecture-diagram.png "för innehållsdistribution på hög nivåArkitektur för innehållsdistribution")

## Viktiga händelser {#key-evolutions}

Den nya arkitekturen för AEM som en molntjänst introducerar några grundläggande förändringar och innovationer jämfört med tidigare generationer:

* Alla filer (blobs) överförs direkt och hanteras från ett molndatalager. Den associerade strömmen med bitar går aldrig igenom JVM för tjänsterna AEM Author och Publish. Därför kan noderna för AEM-författaren och publiceringstjänsterna bli mindre och mer kompatibla med förväntningarna på snabb autoskalning. För dem som arbetar med affärsverksamhet ger detta en snabbare upplevelse när de laddar upp och ned bilder, video osv.

* Alla åtgärder som består av publicerat innehåll omfattar nu en pipeline som följer ett prenumerationsmönster. Publicerat innehåll skickas till olika köer i pipeline, som alla noder i publiceringstjänsten prenumererar på. Därför behöver författarnivån inte vara medveten om antalet noder i publiceringstjänsten. Detta möjliggör snabb autoskalning av publiceringsnivån.

* Konceptet med en gyllene mästare introducerades för att automatisera publiceringsnodernas livscykel. Den gyllene mallsidan är en specialiserad publiceringsnod som ingen slutanvändare har åtkomst till och som alla noder i publiceringstjänsten skapas från. Underhållsåtgärder som komprimering utförs på innehållsarkivet som är kopplat till den gyllene mallen. Publiceringsnoderna återvinns dagligen och kräver inget rutinunderhåll. tidigare krävde sådant underhåll driftavbrott, särskilt för författarinstansen.

* Arkitekturen separerar programinnehållet helt från programkoden och konfigurationen. All kod och konfiguration är praktiskt taget oföränderlig och inbäddad i basbilden som används för att skapa de olika noderna i författaren och publiceringstjänsterna. Det innebär att det finns en absolut garanti för att varje nod är identisk och att ändringar i kod och konfiguration bara kan göras globalt genom att köra en Cloud Manager-pipeline.
