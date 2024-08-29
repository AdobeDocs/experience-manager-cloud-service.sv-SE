---
title: GoLive
description: Lär dig hur du utför migreringen när koden och innehållet är molnklara
exl-id: 10ec0b04-6836-4e26-9d4c-306cf743224e
feature: Migration
role: Admin
source-git-commit: 5b0dfb847a1769665899d6dd693a7946832fe7d1
workflow-type: tm+mt
source-wordcount: '1223'
ht-degree: 0%

---

# GoLive {#go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_prep"
>title="Go-Live-förberedelser"
>abstract="För att säkerställa en smidig och framgångsrik publicering på AEM as a Cloud Service bör du planera för frysning av kod och innehåll, testning av iterationer, innehållsuppdateringar, prestandatester, säkerhetstester med mera."

Under den här delen av resan får du lära dig att planera och utföra migreringen när både koden och innehållet är klara att flyttas över till AEM as a Cloud Service. Du får också lära dig vilka metoder och begränsningar som är bäst när du utför migreringen.

## Story hittills {#story-so-far}

I de föregående faserna av resan:

* Du lärde dig att komma igång med övergången till AEM as a Cloud Service på sidan [Komma igång](/help/journey-migration/getting-started.md).
* Kontrollerade om distributionen är klar att flyttas till molnet genom att läsa [beredskapsfasen](/help/journey-migration/readiness.md)
* Bekanta dig med verktygen och processen som gör din kod och ditt innehåll molnklart med [implementeringsfasen](/help/journey-migration/implementation.md).

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur du utför migreringen till AEM as a Cloud Service när du känner till de tidigare stegen under resan. Du lär dig hur du utför den inledande produktionsmigreringen och de bästa arbetssätten att följa när du migrerar till AEM as a Cloud Service.

## Inledande produktionsmigrering {#initial-migration}

Innan du kan utföra produktionsmigreringen följer du stegen för implementering och korrektur av migrering som beskrivs i avsnittet [Strategi för innehållsmigrering och tidslinje](/help/journey-migration/implementation.md##strategy-timeline) i [implementeringsfasen](/help/journey-migration/implementation.md).

* Starta migreringen från produktionen baserat på den erfarenhet du fick under AEM as a Cloud Service-scenmigreringen som gjordes på kloner:
   * Författare/Författare
   * Publish-Publish

* Validera det innehåll som har infogats i både AEM as a Cloud Service författare- och publiceringsskikt.
* Instruera innehållsredigeringsteamet att undvika att flytta innehåll på både källa och mål tills det är fullständigt
* Nytt innehåll kan läggas till, redigeras eller tas bort, men du kan inte flytta det. Detta gäller både källa och mål.
* Registrera den [tid som tagits](/help/journey-migration/implementation.md#gathering-data) för fullständig extrahering och förtäring för att få en uppskattning av framtida tidslinjer för migrering uppifrån.
* Skapa en [migreringsplanerare](/help/journey-migration/implementation.md#migration-plan) för både författare och publicering.

## Inkrementella överkanter {#top-up}

Efter den första migreringen från produktionen måste du utföra stegvisa översikter för att se till att ditt innehåll är uppdaterat på molninstansen. Därför rekommenderar vi att du följer dessa bästa metoder:

* Samla in data om mängden innehåll. Exempel: per en vecka, två veckor eller en månad.
* Se till att planera de översta bilderna på ett sådant sätt att du undviker mer än 48 timmars extrahering och förtäring av innehåll. Detta rekommenderas så att de översta delarna av innehållet får plats i en heltalsram.
* Planera antalet toppavhopp och använd dessa uppskattningar för att planera runt Go-Live-datumet.

## Identifiera tidslinjer för att migrera kod och innehåll för frysning {#code-content-freeze}

Som tidigare nämnts måste du schemalägga en frysperiod för kod och innehåll. Använd följande frågor för att planera frysningsperioden:

* Hur länge måste jag frysa innehållsredigeringsaktiviteterna?
* Hur länge ska jag be mitt leveransteam sluta lägga till nya funktioner?

Som svar på den första frågan bör du fundera över hur lång tid det har tagit att genomföra testkörningar i icke-produktionsmiljöer. För att svara på den andra frågan behöver du ha ett nära samarbete mellan teamet som lägger till nya funktioner och teamet som omfaktoriserar koden. Målet är att se till att all kod som läggs till i den befintliga distributionen också läggs till, testas och distribueras till molntjänstgrenen. Vanligtvis innebär det att mängden fryst kod är lägre.

Dessutom måste ni planera för en frysning av innehållet när den slutliga innehållstillägget är schemalagd.

## Bästa praxis {#best-practices}

När du planerar eller utför migreringen bör du tänka på följande riktlinjer:

* Migrera från författare till författare och Publish till Publish
* Begär en produktionskloning som kan användas för att:
   * Hämta databasstatistik
   * Bevis på migrationsverksamhet
   * Förbered migreringsplanen
   * Identifiera krav på frysning av innehåll
   * Identifiera alla uppgraderingsbehov i produktionen vid migrering från produktionen

**Metodtips för verktyget Innehållsöverföring**

Se till att du kör innehållsmigreringen i produktion i stället för en klon när du publicerar. Ett bra sätt är att använda [AZCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) för den inledande migreringen och sedan köra extraheringar uppifrån ofta (t.o.m. dagligen) för att extrahera mindre segment och undvika långvarig belastning på AEM.

När du utför produktionsmigreringen bör du undvika att köra verktyget Innehållsöverföring från en klon eftersom:

* Om en kund kräver att innehållsversioner migreras under en översta migrering migreras inte versionerna när innehållsöverföringsverktyget körs från en klon. Även om klonen ofta återskapas från en live-författare återställs de kontrollpunkter som används av verktyget Innehållsöverföring för att beräkna deltarna varje gång en klon skapas.
* Eftersom en klon inte kan uppdateras som helhet måste ACL-frågepaketet användas för att paketera och installera det innehåll som läggs till eller redigeras från produktion till kloning. Problemet med den här metoden är att allt borttaget innehåll i källinstansen aldrig kommer till klonen om det inte tas bort manuellt från både källan och klonen. Detta introducerar möjligheten att det borttagna innehållet i produktionen inte tas bort på klonen och AEM as a Cloud Service.

**Optimerar inläsningen på AEM när innehållsmigreringen utförs**

Kom ihåg att belastningen på AEM är större under extraheringsfasen. Tänk på följande:

* Innehållsöverföringsverktyget är en extern Java-process som använder en JVM-heap på 4 GB
* Icke-AzCopy-versionen hämtar binärfiler, lagrar dem på ett temporärt utrymme på AEM, förbrukar disk-I/O och överför dem sedan till Azure-behållaren som förbrukar nätverksbandbredd
* [AzCopy](/help/journey-migration/content-transfer-tool/using-content-transfer-tool/handling-large-content-repositories.md) överför blober direkt från blobbarkivet till Azure-behållaren som sparar disk-I/O och nätverksbandbredd. AzCopy-versionen använder fortfarande disk- och nätverksbandbredd för att extrahera och överföra data från segmentlagret till Azure-behållaren
* Processen med verktyget Innehållsöverföring är ljusare på systemresurserna under överföringsfasen, eftersom det bara strömmar matningsloggar och det inte finns mycket belastning på källinstansen vad gäller disk-I/O eller nätverksbandbredd.

## Kända begränsningar {#known-limitations}

Ta hänsyn till att hela intaget misslyckas om någon av följande begränsningar påträffas som en del av den extraherade migreringsuppsättningen:

* En JCR-nod med ett namn som är längre än 150 tecken
* En JCR-nod som är större än 16 MB
* Om en resurs som extraheras och hämtas flyttas till en annan sökväg, antingen på källan eller på målet, före nästa iteration av migreringen.

## Resurshälsa {#asset-health}

Jämfört med avsnittet ovan misslyckas **inte** på grund av följande problem med tillgången. Vi rekommenderar dock att du vidtar lämpliga åtgärder i följande situationer:

* Alla resurser som har den ursprungliga återgivningen saknas
* Alla mappar som saknar en `jcr:content`-nod.

Båda ovanstående objekt identifieras och rapporteras i rapporten [Best Practice Analyzer](/help/journey-migration/best-practices-analyzer/overview-best-practices-analyzer.md) .

## GoLive Checklist {#Go-Live-Checklist}

Mer information finns i dokumentationen för [Go-Live Checklist](/help/journey-onboarding/go-live-checklist.md).

## What&#39;s Next {#what-is-next}

När du har förstått hur du utför migreringen till AEM as a Cloud Service kan du kontrollera sidan [Efter-Go-Live](/help/journey-migration/post-go-live.md) för att se till att instansen körs utan problem.
