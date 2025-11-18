---
title: Återställ innehåll i AEM som en molntjänst
description: Lär dig hur du återställer ditt innehåll från AEM as a Cloud Service från backup med Cloud Manager.
exl-id: 921d0c5d-5c29-4614-ad4b-187b96518d1f
feature: Operations
role: Admin
source-git-commit: e6bd71cc56db766fcbab3a925baabb5901c97ee8
workflow-type: tm+mt
source-wordcount: '1610'
ht-degree: 0%

---


# Återställ innehåll i AEM som en molntjänst {#content-restore}

Du kan återställa ditt AEM som molntjänstinnehåll från backup med Cloud Manager.



Cloud Managers självbetjäningsåterställningsprocess kopierar data från Adobes systembackuper och återställer dem till dess ursprungliga miljö. En återställning utförs för att återställa data som har förlorats, skadats eller av misstag raderats till sitt ursprungliga tillstånd.

Återställningsprocessen påverkar endast innehåll, och lämnar din kod och version av AEM oförändrade. Du kan när som helst starta en återställningsoperation av enskilda miljöer.

Om du behöver återställa tidigare distribuerad källkod på ett enkelt och snabbt sätt, utan att behöva starta en ny pipeline-exekvering, kan du använda [Återställ den tidigare distribuerade](/help/operations/restore-previous-code-deployed.md) koden.

Cloud Manager erbjuder två typer av säkerhetskopior från vilka du kan återställa innehåll.

* **Point-In-Time (PIT):** Detta alternativ återställer kontinuerliga säkerhetskopior som tagits under de senaste 24 timmarna.
* **Förra veckan:** Denna typ återställer från systembackuper de senaste sju dagarna, exklusive de senaste 24 timmarna.

I båda fallen förblir versionen av din anpassade kod och AEM-versionen oförändrade.

>[!TIP]
>
>Det är också möjligt att återställa säkerhetskopior [med hjälp av det publika API:et](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/).

>[!WARNING]
>
>* Denna funktion bör endast användas när det finns allvarliga problem med antingen kod eller innehåll.
>* Att återställa en backup tar bort all data som lagts till efter den backupen. Scenografin återgår också till sin tidigare version.
>* Innan du påbörjar en innehållsåterställning, överväg andra selektiva alternativ för innehållsåterställning.

## Alternativ för selektiv innehållsåterställning {#selective-options}

Innan du återställer till en fullständig innehållsåterställning, överväg dessa alternativ för att enklare återställa ditt innehåll.

* Om ett paket för den borttagna sökvägen finns tillgängligt, installera paketet igen med [Package Manager](/help/implementing/developing/tools/package-manager.md).
* Om den borttagna sökvägen var en sida i Sites, använd [funktionen](/help/sites-cloud/authoring/sites-console/page-versions.md) Återställ träd.
* Om den raderade sökvägen var en mapp för tillgångar och originalfilerna är tillgängliga, ladda upp dem igen via [tillgångskonsolen](/help/assets/add-assets.md).
* Om det borttagna innehållet var tillgångar, överväg [att återställa tidigare versioner av tillgångarna](/help/assets/manage-digital-assets.md).

Om inget av ovanstående alternativ fungerar och innehållet i den borttagna sökvägen är betydelsefullt, utför en innehållsåterställning som beskrivs i följande avsnitt.

## Skapa användarroll {#user-role}

Som standard har ingen användare behörighet att utföra innehållsåterställningar i utvecklings-, produktions- eller staging-miljöer. För att delegera denna behörighet till specifika användare eller grupper, använd följande allmänna steg.

1. Skapa en produktprofil med ett uttrycksfullt namn som syftar på innehållsåterställning.
1. Ge behörighet för **programåtkomst** på det nödvändiga programmet.
1. Ge behörigheten **Environment Restore Create** på den nödvändiga miljön eller alla miljöer i programmet, beroende på ditt användningsfall.
1. Tilldela användare till den profilen.

För detaljer om hantering av behörigheter, se [Anpassade behörigheter](/help/implementing/cloud-manager/custom-permissions.md).

## Återställ innehållet i en miljö {#restoring-content}

>[!NOTE]
>
>En användare måste ha [lämpliga behörigheter](#user-role) för att initiera en återställningsoperation.

**För att återställa innehållet i en miljö:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj rätt organisation.

1. Klicka på programmet där du vill initiera en återställning.

1. Lista alla miljöer för programmet genom att göra någon av följande:

   * Från vänstermenyn, under **Tjänster, klicka på** Dataikon![&#x200B; &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg)Miljöer **&#x200B;**.

     ![Fliken Miljöer](assets/environments-1.png)

   * Från vänstermenyn, under **Program, klicka på**&#x200B;Översikt **, och från** Miljökortet **, klicka** på Arbetsflödesikonen![&#x200B; &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg)Visa allt **&#x200B;**.

     ![Visa alla-alternativet](assets/environments-2.png)

     >[!NOTE]
     >
     >Miljökortet **&#x200B;**&#x200B;listar endast tre miljöer. Klicka på **Visa alla** på kortet för att se *alla* miljöer i programmet.

1. I tabellen Miljöer, till höger om en miljö vars innehåll du vill återställa, klicka på ![Fler-ikonen eller ellipsmenyikonen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg), och sedan på **Återställ innehåll**.

   ![Återställ innehåll-alternativet från ellipsmenyn](/help/operations/assets/environments-ellipsis-menu.png)

1. På fliken **Återställ innehåll** på miljöns sida, i **rullgardinsmenyn Tid att återställa** , välj tidsramen för återställningen.

   ![Återställ innehåll-fliken i en miljö](/help/operations/assets/environments-content-restore-tab.png)

   * Om du väljer **Senaste 24 timmar**, i det intilliggande **tidsfältet** , ange exakt tid inom de senaste 24 timmarna för återställning.
   * Om du väljer **Förra veckan**, i det intilliggande **Dagfältet** , välj ett datum inom de senaste sju dagarna, exklusive de senaste 24 timmarna.

1. När du har valt ett datum eller angett en tid **visar avsnittet Tillgängliga** säkerhetskopior nedan en lista över tillgängliga säkerhetskopior som kan återställas

1. Klicka på ![Info-ikonen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) bredvid en backup för att se dess kodversion och AEM-release, och väg sedan återställningseffekten innan du väljer en backup (se [Välj rätt backup](#choosing-backup)).

   ![Backup-information](assets/backup-info.png)

   Tidsstämpeln som visas för återställningsalternativen baseras på datorns användarens tidszon.

1. I höger ände av raden som representerar den backup du vill återställa, klicka på ![Rotera CCW fetstil, eller återställ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_RotateCCWBold_18_N.svg) för att starta återställningsprocessen.

1. Granska detaljerna i **dialogrutan Återställ innehåll** och klicka sedan på **Återställ.**

   ![Bekräfta återställning](assets/backup-restore.png)

Säkerhetskopieringsprocessen initieras. Du kan se dess status i **[listan Återställ aktivitet](#restore-activity)** . Tiden som krävs för att en återställningsoperation ska slutföras beror på storleken och profilen på det innehåll som återställs.

När återställningen slutförs framgångsrikt gör miljön följande:

* Kör samma kod och AEM-release som vid starttillfället för återställningsoperationen.
* Den har samma innehåll som fanns tillgängligt vid tidsstämpeln för den valda ögonblicksbilden, med indexen ombyggda för att matcha den aktuella koden.

## Välj rätt backup {#choosing-backup}

Cloud Managers självbetjäningsåterställningsprocess återställer endast innehåll till AEM. Av denna anledning måste du noggrant överväga kodändringar som gjordes mellan din önskade återställningspunkt och nuvarande tid. Gå igenom commithistoriken mellan det aktuella commit-ID:t och det som återställs.

Det finns flera scenarier.

* Den anpassade miljökoden och återställningen finns på samma repository och samma branch.
* Miljöns anpassade kod och återställningen delar ett repository, använder en separat gren och kommer från en gemensam commit.
* Den anpassade miljökoden och återställningen finns i olika repositorier.
   * I detta fall visas inget commit-ID.
   * Adobe rekommenderar starkt att du klonar båda repositorierna och använder ett differentierat verktyg för att jämföra grenarna.

Tänk också på att en återställning kan göra att dina produktions- och stagingmiljöer hamnar ur synk. Du är ansvarig för konsekvenserna av att återställa innehållet.

## Återställningsaktivitet {#restore-activity}

Listan för **återställningsaktiviteter** visar statusen för de tio senaste återställningsförfrågningarna, inklusive eventuella aktiva återställningsoperationer.

![Återställningsaktivitet](assets/backup-activity.png)

Genom att klicka på ![Informationsikonen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) för en backup kan du ladda ner loggar för den backupen och granska koddetaljerna, inklusive skillnaderna mellan snapshoten och data i det ögonblick återställningen initierades.

## Extern backup {#offsite-backup}

Regelbundna säkerhetskopior täcker risken för oavsiktliga raderingar eller tekniska fel inom AEM Cloud Services, men ytterligare risker kan uppstå vid ett regions fel. Utöver tillgänglighet är den största risken vid sådana regionavbrott förlust av data.

AEM som molntjänst minskar denna risk för alla AEM-produktionsmiljöer. Det vill säga, den kopierar kontinuerligt allt AEM-innehåll till en avlägsen region. Denna process gör innehållet tillgängligt för återhämtning i tre månader. Denna funktion kallas en offsite-backup.

AEM Service Reliability Engineering återställer staging- och produktionsmiljöer för AEM Cloud Service från externa säkerhetskopior under dataregionavbrott.

## Principer för kartläggning av dataregioner {#data-region-mapping-principles}

Adobe följer en uppsättning interna riktlinjer för att bestämma dataregionkartläggningar för **AEM som molntjänst**. Dessa riktlinjer är utformade för att stödja operativ effektivitet, säkerställa efterlevnad av regionala regulatoriska krav och ge en konsekvent kundupplevelse över globala marknader.

### Transparens för regionkartläggning {#region-mapping-transparency}

Adobe offentliggör inte detaljerad kartläggning från region till region.\
Om kunder har specifika eller berättigade frågor om regional distribution, dataresidens eller efterlevnadsimplikationer rekommenderas det att kontakta Adobe direkt via officiell support eller kontokanaler.

### Kärnprinciper för kartläggning av dataregioner {#core-principles}

När Adobe bestämmer en lämplig dataregionkartläggning tillämpar de flera prioriterade kriterier:

1. **Lämna inte den globala regionen**\
   Utplaceringarna finns kvar inom en av de stora globala regionerna: **APAC,**&#x200B;**EMEA** och **Amerika.**

2. **Lämna inte kontinenten**\
   Där det är möjligt förblir datareplikering och failover på samma kontinent.

3. **Lämna inte landet**\
   Om det är tekniskt möjligt stannar data inom samma nationella gränser.

### Hanteringsundantag {#handling-exceptions}

När ovanstående kriterier inte kan uppfyllas på grund av tekniska eller infrastrukturella begränsningar, gör Adobe ytterligare överväganden:

* **Europaspecifik riktlinje**\
  Reserv- eller sekundära regioner bör inte ligga i länder utanför EU.\
  (Omvänt—att använda ett EU-land som backup för ett icke-EU-primärval—kan vara acceptabelt om det inte finns något bättre alternativ för samma land.)

* **Undvik vissa regioner**\
  Regioner med restriktiva datapolicys eller ökad regulatorisk risk bör undvikas som backup- eller failover-platser.

Om kunder behöver förtydliganden eller har krav på efterlevnad rekommenderar Adobe att man kontaktar Adobes kontoteam eller supportorganisation för vägledning anpassad till deras specifika situation.

## Begränsningar {#limitations}

Användningen av självbetjäningsåterställningsmekanismen omfattas av följande begränsningar.

* Återställningsoperationer är begränsade till sju dagar, vilket innebär att det inte är möjligt att återställa en ögonblicksbild som är äldre än sju dagar.
* Maximalt tio lyckade återställningar tillåts i alla miljöer i ett program per kalendermånad.
* Efter miljöskapandet tar det sex timmar innan den första säkerhetskopian skapas. Tills denna snapshot skapas kan ingen återställning utföras i miljön.
* En återställningsoperation initieras inte om det finns en fullstack- eller webbnivåkonfigurationspipeline som för närvarande körs för miljön.
* En återställning kan inte initieras om en annan återställning redan körs i samma miljö.
* I sällsynta fall, på grund av 24-timmars/sju dagars gränsen för backuper, kan den valda backupen bli otillgänglig på grund av en fördröjning mellan när den valdes och när återställningen initieras.
* Data från raderade miljöer går permanent förlorad och kan inte återställas.
