---
title: Databasläsare
seo-title: Repository Browser
description: Databasens webbläsare ger en skrivskyddad vy i databasen för alla miljöer på författar-, publicerings- och förhandsgranskningsnivåer.
seo-description: The repository browser provides a read-only view into the repository for all environments on author, publish, and preview tiers.
exl-id: 22473a97-8f7b-4014-b885-1233116aeda6
source-git-commit: b4d28a0c827fb07d6f731118078ecdf448e2f58b
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Databasläsare {#repository-browser}

>[!NOTE]
>
>Databasläsaren finns AEM version 6582 och senare.

>[!INFO]
>
>Du kan också titta [det här klippet](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/repository-browser.html) om du vill få en snabb videointroduktion om hur du använder Databasläsaren för att felsöka AEM as a Cloud Service.

## Introduktion {#introduction}

Databasens webbläsare är ett utvecklarverktyg som ger en skrivskyddad vy i databasen för alla miljöer med författare-, publicerings- och förhandsgranskningsnivåer. Den är utformad för att göra det enklare att se och felsöka innehållet genom att visa innehållsstrukturen.

Den är tillgänglig från Developer Console och kan användas för att bläddra i databasen för en författare eller publicera en instans för en vald miljö.

### Åtkomstkrav {#access-prerequisites}

Följande villkor måste vara uppfyllda för att du ska få tillgång till Developer Console eller Databaswebbläsaren

Så här får du åtkomst till Developer Console:

* För produktionsprogram måste användarna ha **Cloud Manager - Utvecklarroll** i Admin Console
* För sandlådeprogram är den tillgänglig för alla användare med en produktprofil som ger dem tillgång till AEM as a Cloud Service.

Så här kommer du åt Databasläsaren:

* Användarna måste ha **Cloud Manager - utvecklare** Roll i Admin Console för att visa författarinstanser och publiceringsinstanser.
* Dessutom kan användare med AEM användarprofil visa databaswebbläsaren med minimal läsåtkomst. användarens behörigheter respekteras när användaren bläddrar i databasen. Användare med AEM administratörsproduktprofil kan visa databaswebbläsaren med fullständig läsåtkomst.

Mer information om hur du ställer in användarbehörigheter finns i [Dokumentation för Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/requirements/setting-up-users-and-roles.html).

### Starta Databasläsaren {#launching-the-repository-browser}

Databaswebbläsaren kan startas genom att följa stegen nedan.

1. Klicka på de tre punkterna bredvid den miljö du vill använda i Cloud Manager och välj **Developer Console**

   ![repobrowser1](/help/implementing/developing/tools/assets/repobrowser1.png)

1. Klicka sedan på **Databasläsare** tab
1. Välj en ruta som motsvarar författare, publicering eller förhandsgranskning genom att klicka på **Pod** listruta.

   ![repobrowser2](/help/implementing/developing/tools/assets/repobrowser2.png)

1. Starta databaswebbläsaren genom att klicka på **Öppna databasläsaren** länka längre ned. Då startas webbläsaren som motsvarar en representativ instans (pod) för det valda skiktet. Då startas webbläsaren som motsvarar en representativ instans (pod) för det valda skiktet. Observera att du inte kan styra den specifika pod för den nivån som startas.

## Funktioner {#features}

### Navigera i hierarkin {#navigate-the-hierarchy}

Du kan använda den vänstra navigeringsrutan för att navigera i innehållshierarkin. Om du klickar på varje mapp eller nod visas dess underordnade objekt. Mappstrukturen återspeglar Sling Resource-trädet, som är en överordnad uppsättning till JCR-nodträdet.

![repobrowser3](/help/implementing/developing/tools/assets/repobrowser3.png)

<!-- Alexandru: temporarily commenting this out, please don't delete. 

Alternatively, you can navigate directly to a path by entering it in the **Path** field, as shown below. This will also expand its location in the content hierarcy view on the left.

![repobrowser14](/help/implementing/developing/tools/assets/repobrowser14.png)

Whenever you click a folder on the left, the Path field automatically populates with its location. This is useful for copying and pasting the value for later usage.

Additionally, when you click on a folder, the URL is dynamically modified to include the path to that folder. This allows for bookmarkable URLs.

-->

Som standard visas bara publikt innehåll, vilket innebär att vissa mappar som `/conf` eller `/home` kommer inte att synas.

För att göra platserna synliga måste du följa proceduren nedan.

1. Klicka på de tre punkterna bredvid den miljö du vill använda och välj **Hantera åtkomst**

   ![repobrowser7](/help/implementing/developing/tools/assets/repobrowser7.png)

1. Hitta din publiceringsinstans och klicka sedan på den

   ![repobrowser8](/help/implementing/developing/tools/assets/repobrowser8.png)

1. Skapa en ny produktprofil för publiceringsadministratörer. I exemplet nedan anropas den **DEV - AEM administratörer publicerar**

   ![repobrowser9](/help/implementing/developing/tools/assets/repobrowser9.png)

1. Lägg till lämpliga användare, som motsvarar vem som ska kunna navigera i den publicerade databaswebbläsaren med fullständig åtkomst, till den nya produktprofilen

   ![repobrowser10](/help/implementing/developing/tools/assets/repobrowser10.png)

1. Vänta i några minuter och öppna sedan **AEM** konsol
1. Lägg till gruppen som motsvarar den nya produktprofilen som medlem i gruppen Administratörer. Du kan göra detta genom att klicka på **Verktyg - Säkerhet - grupper på författaren** och sedan klicka på **administratörer** grupp. Lägg sedan till gruppen enligt nedan

   ![repobrowser11](/help/implementing/developing/tools/assets/repobrowser11.png)

1. Aktivera **administratörer** och nya **DEV - AEM administratörer publicerar** grupp så att de blir tillgängliga vid publicering

   ![repobrowser12](/help/implementing/developing/tools/assets/repobrowser12.png)

1. Som en bra säkerhetspraxis bör du ta bort den nya **DEV - AEM administratörer publicerar** grupp från administratörsgruppen på **författare** så att den nya gruppen isoleras för publicering

   ![repobrowser13](/help/implementing/developing/tools/assets/repobrowser13.png)

1. När du öppnar databaswebbläsaren för en publiceringsinstans visas alla mappar, inklusive `/home` och `/conf`.

### Visa JCR-egenskaper {#view-jcr-properties}

Om du klickar på en nod visas dess JCR-egenskaper till höger i navigeringsläsaren. Nedan visas ett exempel för `experience-fragments` nod.

![repobrowser4](/help/implementing/developing/tools/assets/repobrowser41.png)

### Visa innehåll {#view-content}

Du kan använda databaswebbläsaren för att visa innehåll genom att klicka på en resurs i navigeringsrutan. Då öppnas en förhandsgranskning till höger om webbläsaren, under en flik som heter efter respektive resurs.

![repobrowser6](/help/implementing/developing/tools/assets/repobrowser61.png)

Förhandsgranskning är för närvarande tillgängligt för bildtyper i listan nedan:

* apng
* avif
* gif
* jpeg
* png
* svg+xml
* webp
* bmp
* x-icon
* tiff

Och för följande textbaserade MIME-typer:

* `"text/*"`
* `'application/javascript'`
* `'application/json'`
* `'application/x-sh'`

### Hämta innehåll {#download-content}

Du kan också använda databaswebbläsaren för att hämta innehåll. I exemplet nedan kan du trycka på **ladda ned** länk för att ladda ned `jcr:data` som är associerad med den valda noden. Den här funktionen är tillgänglig för alla binära egenskaper genom att navigera till noden som innehåller egenskapsdefinitionen.

![repobrowser5](/help/implementing/developing/tools/assets/repobrowser52.png)
