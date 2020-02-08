---
title: Handbok för resursmigrering
description: Beskriver hur du hämtar resurser till AEM, använder metadata, genererar återgivningar och aktiverar dem för att publicera instanser.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# Handbok för resursmigrering {#assets-migration-guide}

När du migrerar resurser till AEM finns det flera steg att tänka på. Extrahering av resurser och metadata från det aktuella hemmet ligger utanför det här dokumentets omfång eftersom det varierar mycket mellan implementeringar, men i det här dokumentet beskrivs hur du överför dessa resurser till AEM, använder deras metadata, genererar återgivningar och aktiverar dem för publiceringsinstanser.

## Förutsättningar {#prerequisites}

Granska och implementera riktlinjerna för prestandajustering innan du faktiskt utför något av stegen i den här metoden. Många av stegen, som att konfigurera maximalt antal samtidiga jobb, förbättrar i hög grad serverns stabilitet och prestanda vid inläsning. Andra steg, som att konfigurera ett fildatalager, är mycket svårare att utföra efter att systemet har lästs in med resurser.

>[!NOTE]
>
>Följande verktyg för resursmigrering ingår inte i AEM och stöds inte av Adobe Support:
>
>* ACS AEM Tools Tag Maker
>* ACS AEM Tools CSV Asset Importer
>* ACS Commons - massarbetsflödeshanterare
>* Snabbåtgärdshanteraren för ACS-kommandon
>* Syntetiskt arbetsflöde
>
>
Programvaran är öppen källkod och täcks av [Apache v2-licensen](https://adobe-consulting-services.github.io/pages/license.html). Om du vill ställa en fråga eller rapportera ett problem går du till respektive [GitHub Issues för ACS AEM Tools](https://github.com/Adobe-Consulting-Services/acs-aem-commons/issues) och [ACS AEM Commons](https://github.com/Adobe-Consulting-Services/acs-aem-tools/issues).

## Migrerar till AEM {#migrating-to-aem}

Att migrera resurser till AEM kräver flera steg och bör ses som en process i flera steg. Flyttningsfaserna är följande:

1. Inaktivera arbetsflöden.
1. Läs in taggar.
1. Ingest assets.
1. Bearbeta återgivningar.
1. Aktivera resurser.
1. Aktivera arbetsflöden.

![chlimage_1-223](assets/chlimage_1-223.png)

### Inaktivera arbetsflöden {#disabling-workflows}

Innan du startar din migrering ska du inaktivera dina startprogram för arbetsflödet DAM Update Asset. Det är bäst att importera alla resurser till systemet och sedan köra arbetsflödena gruppvis. Om du redan är aktiv under migreringen kan du schemalägga att dessa aktiviteter körs på ledig tid.

### Läser in taggar {#loading-tags}

Du kanske redan har en tagg-taxonomi på plats som du tillämpar på dina bilder. Verktyg som CSV-resursimporteraren och AEM:s stöd för metadataprofiler kan automatisera processen att lägga till taggar i resurser, men taggarna måste läsas in i systemet. Med [ACS AEM Tools Tag Maker](https://adobe-consulting-services.github.io/acs-aem-tools/features/tag-maker/index.html) -funktionen kan du fylla i taggar med hjälp av ett Microsoft Excel-kalkylblad som är inläst i systemet.

### Inkommande resurser {#ingesting-assets}

Prestanda och stabilitet är viktiga frågor när du ska hämta in resurser i systemet. Eftersom du läser in en stor mängd data i systemet bör du se till att systemet fungerar så bra som möjligt för att minimera tidsåtgången och undvika att överbelasta systemet, vilket kan leda till att systemet kraschar, särskilt i system som redan är i produktion.

Det finns två sätt att läsa in resurser i systemet: en push-baserad metod med HTTP eller en pull-baserad metod med JCR-API:erna.

#### Tryck via HTTP {#pushing-through-http}

Adobes Managed Services-team använder ett verktyg som kallas Glutton för att läsa in data i kundmiljöer. Glutton är ett litet Java-program som läser in alla resurser från en katalog till en annan katalog i en AEM-instans. I stället för Glutton kan du också använda verktyg som Perl-skript för att publicera resurserna i databasen.

Det finns två nackdelar med att använda metoden att gå igenom https:

1. Resurserna måste överföras via HTTP till servern. Detta kräver en hel del extraarbete och är tidskrävande, vilket gör att det tar längre tid att utföra migreringen.
1. Om du har taggar och anpassade metadata som måste användas för resurserna, kräver den här metoden en andra anpassad process som du måste köra för att använda dessa metadata för resurserna när de har importerats.

Det andra sättet att importera resurser är att hämta resurser från det lokala filsystemet. Om du inte kan få en extern enhet eller nätverksresurs monterad på servern för att utföra en pull-baserad metod är det bästa alternativet att publicera resurserna via HTTP.

#### Pulling från det lokala filsystemet {#pulling-from-the-local-filesystem}

CSV-resursimporteraren [för](https://adobe-consulting-services.github.io/acs-aem-tools/features/csv-asset-importer/index.html) ACS AEM-verktyg hämtar resurser från filsystemet och metadata för resurser från en CSV-fil för resursimporten. API:t för AEM Asset Manager används för att importera resurserna till systemet och tillämpa de konfigurerade metadataegenskaperna. Resurser monteras helst på servern via en nätverksfilmontering eller via en extern enhet.

Eftersom resurser inte behöver överföras via ett nätverk förbättras prestandan avsevärt, och den här metoden anses generellt vara det mest effektiva sättet att läsa in resurser i databasen. Eftersom verktyget har stöd för metadatainmatning kan du dessutom importera alla resurser och metadata i ett enda steg i stället för att skapa ett andra steg för att använda metadata med hjälp av ett separat verktyg.

### Bearbetar återgivningar {#processing-renditions}

När du har läst in resurserna i systemet måste du bearbeta dem via arbetsflödet DAM Update Asset för att extrahera metadata och generera renderingar. Innan du utför det här steget måste du duplicera och ändra arbetsflödet för DAM-uppdatering av resurser efter dina behov. Det färdiga arbetsflödet innehåller många steg som kanske inte behövs, till exempel Scene7 PTIFF-generering eller InDesign-serverintegrering.

När du har konfigurerat arbetsflödet efter dina behov finns det två alternativ:

1. Det enklaste sättet är [ACS Commons massarbetsflödeshanterare](https://adobe-consulting-services.github.io/acs-aem-commons/features/bulk-workflow-manager.html). Med det här verktyget kan du köra en fråga och bearbeta resultatet av frågan via ett arbetsflöde. Det finns även alternativ för att ange gruppstorlekar.
1. Du kan använda [ACS Commons Fast Action Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) tillsammans med [syntetiska arbetsflöden](https://adobe-consulting-services.github.io/acs-aem-commons/features/synthetic-workflow.html). Även om det här arbetssättet är mycket mer involverat kan du ta bort de allmänna kostnaderna för AEM-arbetsflödesmotorn samtidigt som du optimerar användningen av serverresurser. Dessutom förbättrar Fast Action Manager prestanda ytterligare genom att dynamiskt övervaka serverresurser och begränsa belastningen på systemet. Exempel på skript finns på funktionssidan ACS Commons.

### Aktivera resurser {#activating-assets}

För distributioner som har en publiceringsnivå måste du aktivera resurserna i publiceringsgruppen. Även om Adobe rekommenderar att du kör mer än en publiceringsinstans är det mest effektivt att replikera alla resurser till en publiceringsinstans och sedan klona den instansen. När du aktiverar ett stort antal resurser kan du behöva ingripa efter att ha aktiverat ett träd. Därför: När aktiveringar utlöses läggs objekt till i kön för att skicka jobb/händelser. När storleken på den här kön börjar bli över cirka 40 000 objekt tar det dramatiskt lång tid att bearbeta. När storleken på den här kön överstiger 100 000 objekt börjar systemstabiliteten försämras.

Du kan lösa det här problemet genom att använda [Snabb Action Manager](https://adobe-consulting-services.github.io/acs-aem-commons/features/fast-action-manager.html) för att hantera resursreplikering. Detta fungerar utan att använda Sling-köerna, vilket sänker overheadkostnaderna samtidigt som arbetsbelastningen begränsas för att förhindra att servern blir överbelastad. Ett exempel på hur du använder FAM för att hantera replikering visas på funktionens dokumentationssida.

Andra alternativ för att hämta resurser till publiceringsgruppen är bland annat att använda [vlt-rcp](https://jackrabbit.apache.org/filevault/rcp.html) eller [ekrun](https://github.com/apache/jackrabbit-oak/tree/trunk/oak-run), som tillhandahålls som verktyg som en del av Jackrabbit. Ett annat alternativ är att använda ett verktyg med öppen källkod för din AEM-infrastruktur som kallas [Grabbit](https://github.com/TWCable/grabbit), som sägs ha snabbare prestanda än vad VLT.

För någon av dessa metoder är caveat att resurserna i författarinstansen inte visas som aktiverade. Om du vill hantera flaggning av dessa resurser med rätt aktiveringsstatus måste du också köra ett skript som markerar resurserna som aktiverade.

>[!NOTE]
>
>Adobe underhåller eller stöder inte Grabbit.

### Kloning Publish {#cloning-publish}

När resurserna har aktiverats kan du klona publiceringsinstansen och skapa så många kopior som behövs för distributionen. Det är ganska enkelt att klona en server, men det finns några viktiga steg att komma ihåg. Så här klonar du publiceringen:

1. Säkerhetskopiera källinstansen och datalagret.
1. Återställ säkerhetskopian av instansen och datalagret till målplatsen. Följande steg hänvisar alla till den nya instansen.
1. Gör en filsystemssökning under **crx-quickstart/launchpad/felix** för **sling.id**. Ta bort den här filen.
1. Under rotsökvägen för datalagret letar du reda på och tar bort alla **databas-XXX** -filer.
1. Redigera **crx-quickstart/install/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config** och **crx-quickstart/launchpad/config/org/apache/jackrabbit/oak/plugins/blob/datastore/FileDataStore.config** för att peka på platsen för datalagret i den nya miljön.
1. Starta miljön.
1. Uppdatera konfigurationen för alla replikeringsagenter på författaren/författarna så att de pekar på rätt publiceringsinstanser eller push-agenter för dispatcher på den nya instansen för att peka på rätt dispatchers för den nya miljön.

### Aktivera arbetsflöden {#enabling-workflows}

När migreringen är klar bör startarna för DAM Update Asset-arbetsflödena återaktiveras för att stödja generering av återgivningar och metadataextrahering för den dagliga systemanvändningen.

## Migrera mellan AEM-instanser {#migrating-between-aem-instances}

Även om det inte är nästan lika vanligt behöver du ibland migrera stora mängder data från en AEM-instans till en annan. När du till exempel utför en AEM-uppgradering uppgraderar du maskinvaran eller migrerar till ett nytt datacenter, till exempel med en AMS-migrering.

I det här fallet är dina resurser redan ifyllda med metadata och återgivningar har redan genererats. Du kan helt enkelt fokusera på att flytta resurser från en instans till en annan. När du migrerar mellan AEM-instanser utför du följande steg:

1. Inaktivera arbetsflöden.

   Eftersom du migrerar återgivningar tillsammans med våra resurser, vill du inaktivera arbetsflödesstarterna för DAM Update Asset.

1. Migrera taggar.

   Eftersom du redan har taggar inlästa i AEM-källinstansen kan du skapa dem i ett innehållspaket och installera paketet på målinstansen.

1. Migrera resurser.

   Det finns två verktyg som rekommenderas för att flytta resurser från en AEM-instans till en annan:

   * **Med Vault Remote Copy**, eller vlt rcp, kan du använda VLT i ett nätverk. Du kan ange en käll- och målkatalog och hämta alla databasdata från en instans och läsa in dem i en annan. Vlt rcp finns på [https://jackrabbit.apache.org/filevault/rcp.html](https://jackrabbit.apache.org/filevault/rcp.html)
   * **Grabbit** är ett verktyg för innehållssynkronisering med öppen källkod som utvecklats av Time Warner Cable för deras AEM-implementering. Eftersom den använder kontinuerliga dataströmmar har den en lägre fördröjning jämfört med vlt rcp och kräver en hastighetsförbättring på två till tio gånger snabbare än vlt rcp. Grabbit har även stöd för synkronisering av deltainnehåll, vilket gör att det kan synkronisera ändringar efter att en första migreringspass har slutförts.

1. Aktivera resurser.

   Följ instruktionerna för [aktivering av resurser](#activating-assets) som dokumenterats för den första migreringen till AEM.

1. Klona publiceringen.

   Precis som med en ny migrering är det effektivare att läsa in en publiceringsinstans och klona den än att aktivera innehållet på båda noderna. Se [Klona publicering.](#cloning-publish)

1. Aktivera arbetsflöden.

   När du är klar med migreringen kan du aktivera startfunktionerna för arbetsflödena för DAM Update Asset för att stödja generering av återgivningar och extrahering av metadata för den dagliga systemanvändningen.

