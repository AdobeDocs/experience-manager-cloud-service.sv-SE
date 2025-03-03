---
title: MSM Best Practices
description: Lär dig de bästa arbetssätten som skapats av tekniker och konsultteam på Adobe för att komma igång med AEM Multi Site Manager.
feature: Multi Site Manager
role: Admin
exl-id: 61b8ded8-3b9e-423f-85a9-7280e1a721cc
solution: Experience Manager Sites
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1414'
ht-degree: 0%

---

# MSM Best Practices {#msm-best-practices}

## Allmänt {#general}

MSM är ett konfigurerbart ramverk för automatisering av innehållsdistribution. Implementeringar omfattar ofta större delar av en webbplats och omfattar organisationer och geografiska områden. Vi rekommenderar därför att du planerar MSM-implementeringar lika noggrant som du planerar din webbplats:

* **Planera struktur och innehållsflöden** noggrant innan implementeringen startas.
* **Anpassa så mycket som behövs, men så lite som möjligt.** MSM har stöd för en hög grad av anpassning (till exempel utrullningskonfigurationer), men oftast är det bästa sättet att anpassa din webbplats prestanda, tillförlitlighet och uppgraderingsbarhet att minimera.
* Upprätta en **styrningsmodell** tidigt och utbilda användare därefter för att säkerställa framgång. En god praxis från styrningssynpunkt är att **minimera den behörighet som lokala innehållsproducenter har** för att allokera/ansluta innehåll till andra lokala användare och deras respektive Live-kopior. Detta beror på att icke-styrda, kedjade arv kan öka komplexiteten i en MSM-struktur avsevärt och påverka dess prestanda och tillförlitlighet.
* När det finns en plan för din struktur, innehållsflöden, automatisering och styrning kan du **skapa prototyper och testa systemet** noggrant innan du påbörjar en liveimplementering.
* Tänk på att **Adobe Consulting och ledande systemintegratörer** har djupgående upplevelseplanering och implementering av innehållsautomatisering med MSM, så att de kan hjälpa er att komma igång med ert MSM-projekt och under hela dess implementering.

## Live Copy-källor och layoutkonfigurationer {#live-copy-sources-and-blueprint-configurations}

Kom ihåg att en Live-kopia kan skapas med [vanliga sidor](creating-live-copies.md#creating-a-live-copy-of-a-page) eller en [plantryckskonfiguration](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration). Båda är giltiga användningsfall.

Ytterligare fördelar med att använda en ritkonfiguration är att de:

* Tillåt författaren att använda alternativet **Rollout** för en ritning för att uttryckligen skicka ändringar till Live-kopior som ärver från den här ritningen.
* Tillåt författaren att använda **Skapa plats** för att enkelt välja språk och konfigurera strukturen för Live-kopian.
* Definiera en standardkonfiguration för utrullning för Live-kopior som har en relation till ritningen.

Om det inte finns någon referens till en ritningskonfiguration kan rollouts bara initieras från själva Live-kopiorna, vilket i huvudsak leder till att innehållet hämtas från källan.

När du skapar en webbplats med Live Copy är det fördelaktigt att skapa designkonfigurationer för att säkerställa att hela MSM-funktionsuppsättningen är tillgänglig.

>[!NOTE]
>
>CUG-filer på fliken Behörigheter kan inte rullas ut till Live-kopior från utkast. Planera runt den här regeln när du konfigurerar Live Copy.

## Komponenter- och behållarsynkronisering {#components-and-container-synchronization}

I allmänhet gäller följande som utrullningsregel i MSM för synkronisering av komponenter:

* Komponenter introduceras med synkronisering av alla resurser som ingår i planen.
* Behållare synkroniserar bara den aktuella resursen.

Detta innebär att komponenterna behandlas som en sammanställning och att själva komponenten och alla dess underordnade komponenter i en utrullning ersätts med de i ritningarna. Det innebär att om en resurs läggs till lokalt i en sådan komponent, försvinner den till innehållet i ritningen vid utrullning.

För att ge stöd åt kapsling av komponenter så att lokalt tillagda komponenter bibehålls i en utrullning måste komponenten deklareras som en behållare.

>[!NOTE]
>
>Lägg till egenskapen `cq:isContainer` i komponenten för att ange den som en behållare.

## Skapa webbplats {#create-site}

Observera att AEM har två metoder för att skapa Live-kopior:

* När [skapar en Live-kopia](creating-live-copies.md#creating-a-live-copy-of-a-page) - Detta kan betraktas som ett mer allmänt tillvägagångssätt, vilket gör att du kan skapa Live-kopior från vilken sida som helst. Innehållsstrukturen i en Live-kopia matchar källan exakt.

* När [skapar en plats](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) - Detta är ett mer specialiserat tillvägagångssätt, främst för att skapa webbplatser med en flerspråkig struktur.

Tänk på följande när du skapar en plats:

* Om du vill skapa en plats behöver du en [plantryckskonfiguration](creating-live-copies.md#managing-blueprint-configurations).
* Om du vill att språksökvägar ska kunna väljas på en ny plats måste motsvarande språkrörelser finnas i planen (källa).
* När en [ny webbplats har skapats som en Live-kopia](creating-live-copies.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) (med **Skapa** och sedan **Plats**) är de två första nivåerna i den här Live-kopian *grund*. Sidans underordnade hör inte till live-relationen, men en utrullning kommer ändå att gå ned om en live-relation som matchar utlösaren hittas.

Det är praktiskt att undvika:

* Lägga till språk manuellt i utkastet (under den första nivån).
* Om du lägger till innehåll manuellt direkt under språkroten, eftersom det inte leder till att det nya innehållet överförs automatiskt till Live Copy vid utrullning.

## MSM och flerspråkiga webbplatser {#msm-and-multilingual-websites}

MSM kan hjälpa till att skapa flerspråkiga webbplatser på två sätt:

Tänk på följande när du skapar språkmallar:

* Även om själva MSM **inte tillhandahåller innehållsöversättning** kan den integreras med översättningsanslutningar från tredje part som gör det. Observera följande:
   * Med MSM kan du avbryta arv på sid- och/eller komponentnivå. Detta förhindrar att översatt innehåll (från en Live-kopia, med ännu inte översatt innehåll från en ritning) skrivs över vid nästa utrullning.
      * Vissa översättningsanslutningar från tredje part automatiserar hanteringen av MSM-arv.
      * Kontakta översättningstjänsten för mer information.
      * Ett annat sätt att skapa och översätta språkmallsidor är att använda språkkopior tillsammans med AEM färdiga integrationsramverk för översättning.

Mer information finns i [Översätta innehåll för flerspråkiga platser](/help/sites-cloud/administering/translation/overview.md) och [Bästa praxis för översättning](/help/sites-cloud/administering/translation/best-practices.md).

## Strukturändringar och utrullningar {#structure-changes-and-rollouts}

Ändringar av innehållsstrukturen i ett utkast-/källträd återspeglas på olika sätt i en Live-kopia. Detta beror på ändringstypen:

* **Om du skapar** nya sidor i en plan skapas motsvarande sidor i Live-kopior efter utrullning med standardkonfigurationen.
* **Om du tar bort** sidor i en plan kommer motsvarande sidor att tas bort från Live-kopior efter utrullning med standardkonfiguration.
* **Om du flyttar** sidor i en plan kommer **inte** att resultera i att motsvarande sidor flyttas i Live-kopior efter utrullning med standardkonfiguration:
   * Orsaken till detta är att en sidflyttning implicit inkluderar en sidborttagning. Detta kan potentiellt leda till oväntat beteende vid publicering, eftersom borttagning av sidor på författaren automatiskt inaktiverar motsvarande innehåll vid publicering. Detta kan också ha en extra effekt på relaterade objekt som länkar, bokmärken och andra.
      * Innehållsarv på respektive Live Copy-sidor uppdateras för att återspegla den nya platsen för deras källor i planen.
      * Om du vill att en sida ska flyttas från en plan till Live-kopior bör du överväga [sidflyttningen ].(#page-move)

### Sidflyttning - bästa praxis {#page-move}

Tänk på följande när du funderar på att flytta sidor i en Live-kopia.

>[!NOTE]
>
>Följande fungerar bara med utlösaren [Vid utrullning](live-copy-sync-config.md#rollout-triggers).

1. Skapa en anpassad utrullningskonfiguration.
   * Den nya konfigurationen måste innehålla åtgärden `PageMoveAction`.
   * Lägg inte till andra åtgärder i den här konfigurationen.
1. Placera den nya konfigurationen.
   * Om du vill flytta sidan helt och hållet och ta bort respektive sidor på den gamla platsen i Live Copy:
      * Placera den skapade konfigurationen före standardkonfigurationen för utrullning. Standardkonfigurationen för utrullning hanterar borttagning av sidor på deras gamla platser.
      * Så här flyttar du sidan samtidigt som du behåller sidorna på de gamla platserna i Live-kopior (duplicerar i stort sett innehållet):
         * Placera den skapade konfigurationen efter standardkonfigurationen för utrullning. Detta säkerställer att inget innehåll tas bort i Live Copy eller inaktiveras från publicering.

## Anpassa utrullningar {#customizing-rollouts}

MSM-utrullningskonfigurationer är mycket anpassningsbara. Automatisering av utrullningar kan få stora konsekvenser. Som en god vana bör du planera mycket noggrant innan du deltar i följande aktiviteter:

* Automatiserar rollout som med [onModify-utlösare](#onmodify)
* Anpassar [nodtyper/egenskaper](#node-types-properties)
* Starta efterföljande arbetsflöden
* Aktivera innehåll som en del av utrullningar

### onModify {#onmodify}

När du använder [rollout-utlösaren](live-copy-sync-config.md#rollout-triggers) `onModify` bör du tänka på följande:

* Automatisering av rollouter med `onModify` utlösare kan ha en negativ inverkan på redigeringsprestanda eftersom de utlöser rollout efter varje sidändring.
* Resultatet av utrullningen kan skilja sig från det förväntade:
   * Du kan inte ange ordningen för ändringshändelserna som skapas.
   * Den händelsebaserade arkitekturen kan inte garantera sekvensen för de händelser som skickas till utrullningshanteraren.
* Om en sådan utrullningskonfiguration används kan konflikter uppstå om samma resurs uppdateras samtidigt.

Du bör därför bara använda `onModify`-utlösare om fördelarna med automatisk utrullning är större än eventuella prestandaproblem.

### Nodtyper/egenskaper {#node-types-properties}

Förutom att anpassa utrullningsåtgärder kan MSM även anpassa nodegenskaper som introduceras. Med konfigurationen [MSM OSGi kan du undanta nodtyperna ](live-copy-sync-config.md#excluding-properties-and-node-types-from-synchronization) från kopiering från källan till Live Copy.

## Ytterligare information {#further-information}

Mer information om MSM och Live Copy finns i följande artiklar.

* [Skapa och synkronisera Live-kopior](creating-live-copies.md)
* [Översiktskonsol för Live Copy](live-copy-overview.md)
* [Konfigurera Live Copy-synkronisering](live-copy-sync-config.md)
* [MSM-utrullningskonflikter](rollout-conflicts.md)
