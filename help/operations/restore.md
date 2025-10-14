---
title: Återställ innehåll i AEM as a Cloud Service
description: Lär dig hur du återställer AEM as a Cloud Service-innehåll från en säkerhetskopia med Cloud Manager.
exl-id: 921d0c5d-5c29-4614-ad4b-187b96518d1f
feature: Operations
role: Admin
source-git-commit: 3aff6beda8bcafc884c46ffdc55c530d581543e4
workflow-type: tm+mt
source-wordcount: '1359'
ht-degree: 0%

---


# Återställ innehåll i AEM as a Cloud Service {#content-restore}

Du kan återställa ditt AEM as a Cloud Service-innehåll från en säkerhetskopia med Cloud Manager.

## Ökning {#overview}

Cloud Manager självbetjäningsprocess för återställning kopierar data från Adobe systemsäkerhetskopieringar och återställer dem till den ursprungliga miljön. En återställning utförs för att returnera data som har gått förlorade, skadats eller tagits bort av misstag till det ursprungliga tillståndet.

Återställningsprocessen påverkar bara innehållet, så koden och versionen av AEM ändras inte. Du kan initiera en återställning av enskilda miljöer när som helst. (Om du behöver återställa tidigare distribuerad källkod på ett enkelt och snabbt sätt, utan att behöva starta en ny pipeline-körning, kan du använda [Återställ den tidigare distribuerade koden](/help/operations/restore-previous-code-deployed.md)).

I Cloud Manager finns det två typer av säkerhetskopior som du kan återställa innehåll från.

* **PIT (Point-In-Time):** Med det här alternativet återställs kontinuerliga säkerhetskopior som har samlats in under de senaste 24 timmarna.
* **Senaste veckan:** Den här typen återställer från systemsäkerhetskopieringar under de senaste sju dagarna, exklusive de föregående 24 timmarna.

I båda fallen ändras inte versionen av din anpassade kod och AEM-versionen.

>[!TIP]
>
>Det går också att återställa säkerhetskopior [med det offentliga API:t &#x200B;](https://developer.adobe.com/experience-cloud/cloud-manager/reference/api/).

>[!WARNING]
>
>* Den här funktionen bör endast användas när det finns allvarliga problem med kod eller innehåll.
>* När du återställer en säkerhetskopia tas alla data som har lagts till efter säkerhetskopieringen bort. Mellanlagring återgår också till den tidigare versionen.
>* Innan du startar en innehållsåterställning bör du överväga andra alternativ för selektiv innehållsåterställning.

## Alternativ för selektiv innehållsåterställning {#selective-options}

Innan du återställer till en fullständig innehållsåterställning bör du överväga dessa alternativ för att enklare återställa ditt innehåll.

* Om det finns ett paket för den borttagna sökvägen installerar du paketet igen med hjälp av [pakethanteraren](/help/implementing/developing/tools/package-manager.md).
* Om den borttagna sökvägen var en sida i Sites använder du funktionen [Återställ träd](/help/sites-cloud/authoring/sites-console/page-versions.md).
* Om den borttagna sökvägen var en resursmapp och de ursprungliga filerna är tillgängliga, kan du överföra dem igen via [Assets-konsolen](/help/assets/add-assets.md).
* Om det borttagna innehållet var resurser bör du överväga att [återställa tidigare versioner av resurserna](/help/assets/manage-digital-assets.md).

Om inget av ovanstående alternativ fungerar och innehållet i den borttagna banan är viktigt, utför du en innehållsåterställning enligt anvisningarna i följande avsnitt.

## Skapa användarroll {#user-role}

Som standard har ingen användare behörighet att köra innehållsåterställningar i utvecklings-, produktions- eller stagingmiljöer. Om du vill delegera den här behörigheten till specifika användare eller grupper använder du följande allmänna steg.

1. Skapa en produktprofil med ett uttrycksfullt namn som refererar till innehållsåterställning.
1. Ange behörighet för **programåtkomst** för det program som krävs.
1. Ange behörigheten **Miljöåterställning Skapa** i den miljö som krävs eller i alla miljöer i programmet, beroende på ditt användningssätt.
1. Tilldela användare till den profilen.

Mer information om hur du hanterar behörigheter finns i [Anpassade behörigheter](/help/implementing/cloud-manager/custom-permissions.md).

## Återställa innehållet i en miljö {#restoring-content}

>[!NOTE]
>
>En användare måste ha [lämplig behörighet](#user-role) för att initiera en återställningsåtgärd.

**Så här återställer du innehållet i en miljö:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. Klicka på det program som du vill starta en återställning för.

1. Visa alla miljöer för programmet genom att göra något av följande:

   * På den vänstra menyn, under **Tjänster**, klickar du på ![Dataikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **Miljö**.

     ![Fliken Miljö](assets/environments-1.png)

   * Klicka på **Översikt** under **Program** på den vänstra menyn och klicka sedan på **Arbetsflödesikonen** ![Visa alla](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Workflow_18_N.svg) på **miljökortet** .

     ![Visa alla alternativ](assets/environments-2.png)

     >[!NOTE]
     >
     >Kortet **Environment** innehåller endast tre miljöer. Klicka på **Visa alla** på kortet för att visa *alla* miljöer för programmet.

1. I miljötabellen, till höger om en miljö vars innehåll du vill återställa, klickar du på ikonen ![Mer eller Ellips &#x200B;](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) och sedan på **Återställ innehåll**.

   ![Återställ innehållsalternativ från ellipsmenyn](/help/operations/assets/environments-ellipsis-menu.png)

1. Markera tidsramen för återställningen på fliken **Återställ innehåll** på miljösidan i listrutan **Tid för återställning**.

   ![Återställa fliken Innehåll i en miljö](/help/operations/assets/environments-content-restore-tab.png)

   * Om du väljer **Senaste 24 timmarna** anger du den exakta tiden inom de senaste 24 timmarna som ska återställas i fältet **Tid** intill.
   * Om du valde **Senaste veckan** i fältet **Dag** väljer du ett datum under de senaste sju dagarna, exklusive de föregående 24 timmarna.

1. När du har valt ett datum eller angett en tidpunkt visas en lista med tillgängliga säkerhetskopior som kan återställas i avsnittet **Tillgängliga säkerhetskopior** nedan

1. Klicka på ![Informationsikonen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) bredvid en säkerhetskopia för att se kodversionen och AEM-versionen och mät sedan återställningens effekt innan du väljer en säkerhetskopia (se [Välja rätt säkerhetskopia](#choosing-backup)).

   ![Säkerhetskopieringsinformation](assets/backup-info.png)

   Tidsstämpeln som visas för återställningsalternativen baseras på datorns tidszon för användaren.

1. Klicka på ![Rotera motsols fet eller återställ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_RotateCCWBold_18_N.svg) till höger om raden som representerar den säkerhetskopia som du vill återställa för att starta återställningsprocessen.

1. Granska informationen i dialogrutan **Återställ innehåll** och klicka sedan på **Återställ**.

   ![Bekräfta återställning](assets/backup-restore.png)

Säkerhetskopieringsprocessen initieras. Du kan visa dess status i listan **[Återställ aktivitet](#restore-activity)**. Hur lång tid det tar att slutföra en återställning beror på storleken och profilen på det innehåll som återställs.

När återställningen har slutförts gör miljön följande:

* Kör samma kod och AEM som när återställningsåtgärden initierades.
* Den har samma innehåll som var tillgängligt vid tidsstämpeln för den valda ögonblicksbilden, med indexen omgjorda för att matcha den aktuella koden.

## Välj rätt säkerhetskopia {#choosing-backup}

Cloud Manager självbetjäningsåterställning återställer endast innehåll till AEM. Därför måste du noga överväga kodändringar som gjorts mellan den önskade återställningspunkten och den aktuella tidpunkten. Granska implementeringshistoriken mellan det aktuella implementerings-ID:t och det som återställs.

Det finns flera scenarier.

* Miljöns anpassade kod och återställningen finns i samma databas och samma gren.
* Miljöns egen kod och återställningen delar en databas, använder en separat gren och härstammar från en gemensam implementering.
* Miljöns anpassade kod och återställningen finns i olika databaser.
   * I det här fallet visas inget implementerings-ID.
   * Adobe rekommenderar att du klonar båda databaserna och använder ett diff-verktyg för att jämföra grenarna.

Tänk också på att en återställning kan göra att produktions- och staging-miljöerna inte synkroniseras. Du ansvarar för konsekvenserna av att återställa innehåll.

## Återställ aktivitet {#restore-activity}

I listan **Återställningsaktivitet** visas status för de tio senaste återställningsbegäranden, inklusive alla aktiva återställningsåtgärder.

![Återställ aktivitet](assets/backup-activity.png)

Genom att klicka på ![Informationsikonen](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Info_18_N.svg) för en säkerhetskopia kan du hämta loggar för den säkerhetskopian och kontrollera kodinformationen, inklusive skillnaderna mellan ögonblicksbilden och data när återställningen initierades.

## Säkerhetskopiering offline {#offsite-backup}

Regelbunden säkerhetskopiering täcker risken för oavsiktliga borttagningar eller tekniska fel i AEM Cloud Services, men ytterligare risker kan uppstå om en region slutar fungera. Förutom tillgänglighet är den största risken i sådana regionala avbrott en dataförlust.

AEM as a Cloud Service minskar denna risk för alla AEM produktionsmiljöer. Det innebär att allt AEM-innehåll fortlöpande kopieras till en fjärrregion. Den här processen gör innehållet tillgängligt för återställning i tre månader. Den här funktionen kallas säkerhetskopiering på annan plats.

AEM Service Reliable Engineering återställer staging och produktion av AEM Cloud-tjänstmiljöer från säkerhetskopiering på annan plats vid dataavbrott.

## Begränsningar {#limitations}

Användningen av mekanismen för självbetjäning av återställning omfattas av följande begränsningar.

* Återställningsåtgärderna är begränsade till sju dagar, vilket innebär att det inte går att återställa en ögonblicksbild som är äldre än sju dagar.
* Högst tio lyckade återställningar tillåts i alla miljöer i ett program per kalendermånad.
* När miljön har skapats tar det sex timmar innan den första ögonblicksbilden av säkerhetskopian skapas. Innan den här ögonblicksbilden har skapats går det inte att återställa miljön.
* Ingen återställningsåtgärd initieras om det för närvarande körs en fullständig stack- eller webbskiktskonfigurationspipeline för miljön.
* Det går inte att starta en återställning om en annan återställning redan körs i samma miljö.
* I sällsynta fall, på grund av gränsen på 24 timmar/sju dagar för säkerhetskopiering, kan den markerade säkerhetskopian bli otillgänglig på grund av en fördröjning mellan den tidpunkt då den valdes och den tidpunkt då återställningen initierades.
* Data från borttagna miljöer går förlorade permanent och kan inte återställas.
