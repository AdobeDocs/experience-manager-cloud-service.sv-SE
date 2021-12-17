---
title: GoLive
description: Lär dig hur du utför migreringen när koden och innehållet är molnklara
source-git-commit: fe0261fa9708b2250b6f5e4931100a9fc006e55d
workflow-type: tm+mt
source-wordcount: '1319'
ht-degree: 0%

---


# GoLive {#go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_prep"
>title="Go-Live-förberedelser"
>abstract="För att säkerställa en smidig och framgångsrik publicering på AEM as a Cloud Service bör du planera för frysningsperioder för kod och innehåll, testning av iterationer, innehållsuppdateringar, prestandatester, säkerhetstester med mera."

Under den här delen av resan får du lära dig att planera och utföra migreringen när både koden och innehållet är klara att flyttas över till AEM as a Cloud Service. Dessutom får du lära dig vad som är bästa praxis och kända begränsningar när du utför migreringen.

## Story hittills {#story-so-far}

I de föregående faserna av resan:

* Du lärde dig att komma igång med övergången till AEM as a Cloud Service i [Komma igång](/help/journey-migration/getting-started.md) sida.
* Fastställd om distributionen är klar att flyttas till molnet genom att läsa [Beredskapsfas](/help/journey-migration/readiness.md)
* Bekanta dig med verktygen och processen som gör koden och innehållet molnklart med [Implementeringsfas](/help/journey-migration/implementation.md).

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur du utför migreringen till AEM as a Cloud Service när du känner till de tidigare stegen under resan. Du får lära dig att utföra den inledande produktionsmigreringen samt de bästa arbetssätten att följa när du migrerar till AEM as a Cloud Service.

## Inledande produktionsmigrering {#initial-migration}

Innan du kan utföra produktionsmigreringen följer du stegen för implementering och korrektur av migrering i [Strategi för innehållsmigrering och tidslinje](/help/journey-migration/implementation.md##strategy-timeline) i [Implementeringsfas](/help/journey-migration/implementation.md).

* Starta migreringen från produktionen baserat på den erfarenhet du fick under den AEM as a Cloud Service migreringen av scenen som utfördes på kloner:
   * Författare/Författare
   * Publish-Publish

* Validera det innehåll som är inkapslat i både den AEM as a Cloud Service författaren och publiceringsnivån.
* Instruera innehållsredigeringsteamet att undvika att flytta innehåll på både källa och mål tills det är fullständigt
* Nytt innehåll kan läggas till, redigeras eller tas bort, men du kan inte flytta det. Detta gäller både källa och mål.
* Spela in [tid](/help/journey-migration/implementation.md#gathering-data) för fullständig extrahering och förtäring för att få en uppskattning av framtida tidslinjer för migrering uppifrån och ned.
* Skapa en [migreringsplanering](/help/journey-migration/implementation.md#migration-plan) för både författare och publicering.

## Inkrementella överkanter {#top-up}

Efter den första migreringen från produktionen måste du utföra stegvisa översikter för att se till att ditt innehåll är uppdaterat på molninstansen. Därför rekommenderar vi att du följer dessa bästa metoder:

* Samla in data om mängden innehåll. Till exempel: en vecka, två veckor eller en månad.
* Se till att planera de översta bilderna på ett sådant sätt att du undviker mer än 48 timmars extrahering och förtäring av innehåll. Detta rekommenderas så att de översta delarna av innehållet får plats i en helg.
* Planera antalet toppavhopp och använd dessa uppskattningar för att planera runt Go-Live-datumet.

## Identifiera tidslinjer för att migrera kod och innehåll för frysning {#code-content-freeze}

Som tidigare nämnts måste du schemalägga en frysperiod för kod och innehåll. Använd följande frågor för att planera frysningsperioden:

* Hur länge måste jag frysa redigeringsaktiviteterna?
* Hur länge ska jag be mitt leveransteam sluta lägga till nya funktioner?

Som svar på den första frågan bör du fundera över hur lång tid det har tagit att genomföra testkörningar i icke-produktionsmiljöer. För att svara på den andra frågan behöver du ha ett nära samarbete mellan teamet som lägger till nya funktioner och teamet som omstrukturerar koden. Målet bör vara att se till att all kod som läggs till i den befintliga distributionen också läggs till, testas och distribueras till molntjänstgrenen. I allmänhet innebär detta att mängden fryst kod blir lägre.

Dessutom måste du planera för en frysning av innehållet när den slutliga innehållsuppdateringen är schemalagd.

## Bästa praxis {#best-practices}

När du planerar eller utför migreringen bör du tänka på följande riktlinjer:

* Migrera från författare till författare och publicera till publicera
* Begär en produktionskloning som kan användas för att:
   * Hämta databasstatistik
   * Bevis på migrationsverksamhet
   * Förbered migreringsplanen
   * Identifiera krav på frysning av innehåll
   * Identifiera alla uppgraderingsbehov i produktionen vid migrering från produktionen

**Metodtips för verktyget Innehållsöverföring**

Se till att du kör innehållsmigreringen i produktion i stället för en klon när du publicerar. Ett bra sätt är att använda [AZCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) för den initiala migreringen och kör sedan extraheringar uppifrån ofta (t.o.m. dagligen) för att extrahera mindre bitar och undvika långvarig belastning på AEM.

När du utför produktionsmigreringen bör du undvika att köra verktyget Innehållsöverföring från en klon eftersom:

* Om en kund kräver att innehållsversioner migreras under en översta migrering migreras inte versionerna när innehållsöverföringsverktyget körs från en klon. Även om klonen ofta återskapas från en live-författare återställs de kontrollpunkter som ska användas av verktyget Innehållsöverföring för att beräkna deltarna varje gång en klon skapas.
* Eftersom en klon inte kan uppdateras som helhet måste ACL-frågepaketet användas för att paketera och installera det innehåll som läggs till eller redigeras från produktion till kloning. Problemet med den här metoden är att allt borttaget innehåll i källinstansen aldrig kommer till klonen om det inte tas bort manuellt från både källan och klonen. Detta introducerar möjligheten att det borttagna innehållet i produktionen inte tas bort på klonen och AEM as a Cloud Service.

**Optimera belastningen på AEM när innehållsmigreringen utförs**

Kom ihåg att belastningen på AEM blir större under extraheringsfasen. Du bör vara medveten om att

* Innehållsöverföringsverktyget är en extern Java-process som använder en JVM-heap på 4 GB
* Icke-AzCopy-versionen hämtar binärfiler, lagrar dem på ett temporärt utrymme på AEM, förbrukar disk-I/O och överför dem sedan till Azure-behållaren som förbrukar nätverksbandbredd
* [AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) överför blobbar direkt från blobbarkivet till Azure-behållaren som sparar disk-I/O och nätverksbandbredd. AzCopy-versionen använder fortfarande disk- och nätverksbandbredd för att extrahera och överföra data från segmentlagret till Azure-behållaren
* Processen med verktyget Innehållsöverföring är ljusare på systemresurserna under överföringsfasen, eftersom det bara strömmar matningsloggar och det inte finns mycket belastning på källinstansen vad gäller disk-I/O eller nätverksbandbredd.

## Kända begränsningar {#known-limitations}

Ta hänsyn till att hela intaget misslyckas om någon av följande begränsningar påträffas som en del av den extraherade migreringsuppsättningen:

* En JCR-nod med ett namn som är längre än 150 tecken
* En JCR-nod som är större än 16 MB
* Alla användare/grupper med `rep:AuthorizableID` som redan finns på AEM as a Cloud Service
* Om en resurs som extraheras och hämtas flyttas till en annan sökväg, antingen på källan eller på målet, före nästa iteration av migreringen.

## Resurshälsa {#asset-health}

Jämfört med avsnittet ovanför intaget **inte** misslyckas på grund av följande problem med tillgångar. Vi rekommenderar dock att du vidtar lämpliga åtgärder i följande situationer:

* Alla resurser som har den ursprungliga återgivningen saknas
* Alla mappar som saknas `jcr:content` nod

Båda ovanstående poster identifieras och rapporteras i [Best Practice Analyzer](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md) rapport.

## GoLive Checklist {#Go-Live-Checklist}

Granska listan över aktiviteter nedan för att säkerställa att du kan genomföra en smidig och framgångsrik migrering:

* Schemalägg en frysperiod för kod och innehåll. Se även [Tidslinjer för Kod- och Content Freeze för migrering](#code-content-freeze).
* Utför den slutliga innehållsuppsättningen
* Slutföra testiterationer
* Köra prestanda- och säkerhetstester
* Kom igång och utföra migreringen på produktionsinstansen

Du kan alltid referera till listan om du behöver kalibrera om dina uppgifter när du utför migreringen.

## What&#39;s Next {#what-is-next}

När du förstår hur du utför migreringen till AEM as a Cloud Service kan du kontrollera [Post-Go-Live](/help/journey-migration/post-go-live.md) sida för att få instansen att löpa smidigt.