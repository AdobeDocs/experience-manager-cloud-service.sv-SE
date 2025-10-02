---
title: Hälsoutvärdering för produktions- och scenmiljöer
description: Lär dig hur du använder Cloud Manager Health Assessment. Du kan skanna AEM-miljöer, köra och granska rapporter, visa probleminformation, exportera PDF:er och hantera tidigare körningar.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 5f9d53958076b77cd333a042003c83853594db87
workflow-type: tm+mt
source-wordcount: '1406'
ht-degree: 0%

---


# Hälsoutvärdering {#about-health-assessment}

Hälsoutvärdering är en automatisk, icke-påträngande skanning för produktions- och scenmiljöer i Cloud Manager inom AEM as a Cloud Service. Innehåll, kod och konfigurationer utvärderas för att hitta mönster som inte matchar bästa praxis, vilket förbättrar säkerheten och prestandan.

Tjänsten för hälsobedömning utför följande:

* Söker igenom miljöer och visar flaskhalsar, ineffektivitet och risker.
* Analyserar innehållsstrukturer som ritningar, live-kopior och kundkonfigurationer.
* Identifierar föråldrade beroenden, inklusive AEM SDK och tredjepartsbibliotek.
* Flaggar för problem med kodkvalitet, t.ex. felaktiga anteckningar och ineffektiva mönster.
* Ger användbar vägledning i kontrollpaneler (till exempel Åtgärdscenter).
* Driver proaktiva reparationer för att förbättra systemprestanda.

Varje körning listar problem efter allvarlighetsgrad, länkar till riktlinjer och rekommenderade korrigeringar och stöder en PDF-export av rapporten. Du kan använda vyn **Senaste rapport** för det aktuella läget och vyn **Tidigare rapporter** för att jämföra körningar.

Se även [Hälsobedömningsmönster](#ha-patterns) för regeldefinitioner och reparationsinformation.

## Gå till sidan Hälsoutvärdering {#access-health-assessment}

1. Logga in på Cloud Manager på [experience.adobe.com](https://experience.adobe.com).
1. Klicka på **Experience Manager** i avsnittet **Snabbåtkomst**.
1. Klicka på **Cloud Manager** på den vänstra panelen.
1. Välj en organisation som du vill ha. Bilden nedan är till för illustration. Välj ditt eget organisationsnamn.

   ![Välja en organisation i Cloud Manager](/help/implementing/cloud-manager/reports/assets/ha-org.png)

1. På konsolen **Mina program** klickar du på det program som du vill visa rapporten för.

1. Gör något av följande:
   * Klicka på ikonen **Ellips eller ikonen Mer** till höger om ett miljönamn på ![miljökortet](https://spectrum.adobe.com/static/icons/ui_18/More.svg) och välj sedan **Hälsoutvärdering** på menyn.

     ![Välja Hälsoutvärdering på ellipsmenyn i miljökortet](/help/implementing/cloud-manager/reports/assets/ha-myprograms-environments-card.png)

   * På den vänstra menyn, under **Tjänster**, klickar du på ![Dataikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_Data_18_N.svg) **Miljö**. Klicka på ikonen ![Ellips eller Mer &#x200B;](https://spectrum.adobe.com/static/icons/ui_18/More.svg) till höger om ett miljönamn på sidan Miljöer och välj sedan **Hälsoutvärdering** på menyn.

     ![Välja Hälsoutvärdering på ellipsmenyn på miljösidan](/help/implementing/cloud-manager/reports/assets/ha-environments-page.png)

## Kör en ny rapport för en vald miljö {#run-report}

1. [Gå till sidan för hälsoutvärdering](#access-health-assessment).
1. Bekräfta målmiljön som du ska utvärdera i det övre högra hörnet på sidan **Hälsoutvärdering**.

   Om miljön är felaktig klickar du på ![Nedrullningsbar eller nedrullningsbar meny för att välja en annan miljö](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) och väljer rätt miljö i listan.

1. Klicka på **Kör rapport**.

   ![Klicka på knappen Generera ny rapport på sidan Hälsoutvärdering](/help/implementing/cloud-manager/reports/assets/ha-run-report.png)

   När en rapport körs för den valda miljön är **Kör rapport** inaktiverat tills den är klar.

   ![Rapport mitt under körning](/help/implementing/cloud-manager/reports/assets/ha-running-report.png)

   När rapporten är klar visas rapporten på sidan **Hälsoutvärdering** i avsnittet **Senaste rapport**.

## Visa den senaste rapporten {#view-latest-report}

* Gå till avsnittet **Senaste rapporten** på sidan **Hälsoutvärdering** för följande information:

   * Resultat från den senaste körningen.
   * Kör datum och tid.
   * Totalt antal utleveranser.
   * Viktigt om viktiga problem.
   * Åtgärder: **[Visa information](#view-report-details)** eller **[Hämta PDF](#download-pdf-report)** om alla problem.

  ![Den senaste utvärderingssidan efter genereringen av en ny rapport för en vald miljö](/help/implementing/cloud-manager/reports/assets/ha-latest-report-page.png)

### Visa den senaste rapportinformationen {#view-report-details}

* På sidan **Hälsoutvärdering** till höger om titeln **Senaste rapport** klickar du på ikonen ![Ellips eller Mer &#x200B;](https://spectrum.adobe.com/static/icons/ui_18/More.svg) och sedan på **Visa information** eller **Hämta**.

  Alternativet **Visa information** visar följande:

   * En omfattande lista med frågor.
   * Möjlighet att se resultat och felbeskrivningar.
   * Möjlighet att visa dokumentation med potentiella korrigeringar.

     ![Problembeskrivningar och hitta](/help/implementing/cloud-manager/reports/assets/ha-issue-descriptions-and-findings.png)

   * Med alternativet **Hämta** kan du hämta enskilda problemrapporter i PDF.

     ![Ladda ned PDF med rapporter om enskilda problem](/help/implementing/cloud-manager/reports/assets/ha-details-page-doc-links.png)


### Ladda ned hela PDF-rapporten {#download-pdf-report}

* Klicka på **Hämta** i det övre högra hörnet av rapportsidan.

  En ZIP-fil skapas som innehåller PDF-filer för alla problem som upptäcks i rapporten.

  ![Hämta PDF för alla problem som hittats i en rapport](/help/implementing/cloud-manager/reports/assets/ha-download-pdf.png)


## Granska tidigare rapporter {#review-past-reports}

Gå till avsnittet **Tidigare rapporter** på sidan **Hälsoutvärdering** för följande information:

* Visa information om tidigare rapporter.
* Visa varje körnings datum.
* Ladda ned en PDF för alla rapporter.
* Sortera efter datum, antal utgåvor eller miljö.

![Granska tidigare rapporter](/help/implementing/cloud-manager/reports/assets/ha-past-reports.png)

* Till höger om rubriken **Tidigare rapporter** klickar du på ![Nedrullningsbar meny eller listruta för att välja en annan miljö](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ChevronDown_18_N.svg) för att sortera tidigare rapporter efter datum.
* Klicka på ikonen ![Ellips eller Mer](https://spectrum.adobe.com/static/icons/ui_18/More.svg) till höger om en rapport och klicka sedan på **Visa information** eller **Hämta**.


## Utvärderingsmönster för hälsa {#ha-patterns}

Nedan följer en fullständig lista över de antimönster och problem som Hälsoutvärdering identifierar i AEM as a Cloud Service. Tabellen grupperar objekten i tre typer: Innehållsanalys, Kodanalys och Cloud Service Optimizer-antimönster, med en förklaring för varje.

| Mönsternamn | Kategori | Typ | Beskrivning | Effekt | Automatisk korrigering? |
| --- | --- | --- | --- | --- | --- |
| Anpassade AEM-grupper med tillägg direkt från användaren | Dokumentskydd | Innehållsanalys | Användare som läggs till direkt i AEM-grupper i stället för att lägga till IMS-grupper som medlemmar. | Behörighetshantering och säkerhetsstyrning kan bli komplicerade. [IMS-stöd](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/ims-support) | Nej |
| JCR-innehållsnod saknas på sidor | Databasstruktur | Innehållsanalys | `jcr:content`-nod saknas på sidan. | Funktionsbegränsningar i Experience Manager as a Cloud Service. [Mönsteridentifiering - ACV](https://experienceleague.adobe.com/en/docs/experience-manager-pattern-detection/table-of-contents/acv) | Nej |
| Saknad typ av delningsresurs på sidor | Databasstruktur | Innehållsanalys | `sling:resourceType` saknas på sidan. | Funktionsbegränsningar i Experience Manager as a Cloud Service. [Mönsteridentifiering - ACV](https://experienceleague.adobe.com/en/docs/experience-manager-pattern-detection/table-of-contents/acv) | Nej |
| Sidor med mycket stort nodantal | Prestanda | Innehållsanalys | Sidorna innehåller ett stort antal noder i sin struktur. | Långsam sidladdningstid och dålig användarupplevelse. [Mönsteridentifiering - PCX](https://experienceleague.adobe.com/en/docs/experience-manager-pattern-detection/table-of-contents/pcx) | Nej |
| För många arbetsflödesinstanser som körs | Prestanda | Innehållsanalys | För många arbetsflödesinstanser körs. | Total försämring av systemprestanda. [Underhållsaktiviteter](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/operations/maintenance) | Nej |
| Ej rensade slutförda arbetsflödesinstanser | Prestanda | Innehållsanalys | Äldre slutförda arbetsflödesinstanser rensas inte. | Minskad systemeffektivitet och ökade lagringskostnader. [Underhållsaktiviteter](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/operations/maintenance) | Nej |
| Användningsstatistik för innehållsfragment | Statistik | Innehållsanalys | Spårar antalet innehållsfragment som används. | Ej tillämpligt | Ej tillämpligt |
| Användningsstatistik för innehållsfragmentmodell | Statistik | Innehållsanalys | Spårar antalet innehållsfragmentmodeller som används. | Ej tillämpligt | Ej tillämpligt |
| MSM stort antal utkast | Statistik | Innehållsanalys | Spårar antalet ritningar. | Det kan göra hanteringen mer komplicerad och göra innehållsstyrningen svårare. | Ej tillämpligt |
| MSM-sidor per utkast | Statistik | Innehållsanalys | Spårar antalet sidor per plan. | Det kan göra hanteringen mer komplicerad och göra innehållsstyrningen svårare. | Ej tillämpligt |
| MSM för stora Live-kopior | Statistik | Innehållsanalys | Spårar antalet live-kopior. | Det kan leda till prestandaproblem under utrullningar och komplicera innehållssynkroniseringen. | Ej tillämpligt |
| MSM-kopior av stora volymer per utkast | Statistik | Innehållsanalys | Spårar antalet live-kopior per ritning. | Det kan leda till prestandaproblem under utrullningar och komplicera innehållssynkroniseringen. | Ej tillämpligt |
| Antal Assets | Statistik | Innehållsanalys | Spårar antalet resurser. | Ej tillämpligt | Ej tillämpligt |
| Antal platser | Statistik | Innehållsanalys | Spårar antalet webbplatser. | Ej tillämpligt | Ej tillämpligt |
| Antal Forms | Statistik | Innehållsanalys | Spårar antalet formulär. | Ej tillämpligt | Ej tillämpligt |
| Formulärfragment | Statistik | Innehållsanalys | Spårar antalet formulärfragment. | Ej tillämpligt | Ej tillämpligt |
| Interaktion | Statistik | Innehållsanalys | Spårar antalet interaktioner för formulärkommunikation. | Ej tillämpligt | Ej tillämpligt |
| FDMs | Statistik | Innehållsanalys | Spårar antalet formulärdatamodeller. | Ej tillämpligt | Ej tillämpligt |
| Inaktuella beroenden | Beroenden | Kodanalys | Framhäver föråldrade beroenden i kunddatabasen. | Inkompatibelt med nyare AEM-versioner, potentiella säkerhetsproblem. | Nej |
| AEM SDK - versionerna matchar inte | Beroenden | Kodanalys | Versioner äldre än (n-2) jämfört med Cloud Manager miljöversion. | Det kan orsaka byggfel i Cloud Manager och problem i lokala utvecklingsmiljöer. | Nej |
| Förfallet beroende av dockito-kärna | Beroenden | Kodanalys | Versioner under 4.x.x betraktas som inaktuella för AEM as a Cloud Service. | Det kan orsaka byggfel i Cloud Manager och problem i lokala utvecklingsmiljöer. | Nej |
| Anteckningar som inte stöds | Beroenden | Kodanalys | Anteckningar som inte stöds i kundens Cloud Manager-databas. | Möjliga programfel och minskad prestanda. | Nej |
| @Inmatningsanteckning i delningsmodeller | Beroenden | Kodanalys | `@Inject`-anteckningen har tagits bort. | Minskade applikationsprestanda på grund av overhead-kostnader för injektionsupplösning. | Nej |
| Utgående HTTP-begäranden | Prestanda | Antimönster för Cloud Service Optimizer | Problematisk användning i begärandekontext, hög tidsgräns eller inte avslutande anslutningar. | Systemets totala prestandaförsämring och eventuella avbrott. | Ja |
| Långsamma frågor | Prestanda | Antimönster för Cloud Service Optimizer | Långsamma frågor i kundkoden. | Försämrade systemprestanda och potentiella tidsgränser. | Ja |

### Kategorier {#ha-patterns-categories}

| Kategori | Beskrivning |
| --- | --- |
| Dokumentskydd | Mönster som rör säkerhetsrutiner, användarhantering och åtkomstkontroll. |
| Prestanda | Mönster som påverkar program- och systemprestanda. |
| Databasstruktur | Mönster som hör till JCR-databasens struktur och organisation. |
| Beroenden | Mönster som är relaterade till kodberoenden och versionshantering. |
| Statistik | Mönster som representerar användningsstatistik och mätvärden. |



