---
title: Hantera översättningsprojekt
description: Lär dig hur du skapar och hanterar både maskinöversättning och mänsklig översättning i AEM.
feature: Language Copy
role: Admin
exl-id: dc2f3958-72b5-4ae3-a224-93d8b258bc80
source-git-commit: ae500923bac34689a28b9ff0bc78586f725829de
workflow-type: tm+mt
source-wordcount: '4011'
ht-degree: 0%

---

# Hantera översättningsprojekt {#managing-translation-projects}

Med översättningsprojekt kan du hantera översättning av AEM. Ett översättningsprojekt är en typ av AEM [projekt](/help/sites-cloud/authoring/projects/overview.md) som innehåller resurser som ska översättas till andra språk. Dessa resurser är sidorna och resurserna i [språkversioner](preparation.md) som har skapats från språkinställaren.

>[!TIP]
>
>Om du inte är van vid att översätta innehåll, se [Sites Translation Journey,](/help/journey-sites/translation/overview.md) som vägleder dig genom att översätta ditt AEM Sites-innehåll med AEM kraftfulla översättningsverktyg, idealiskt för dem som saknar AEM eller översättningsupplevelse.

När resurser läggs till i ett översättningsprojekt skapas ett översättningsjobb för dem. Jobb innehåller kommandon och statusinformation som du använder för att hantera de mänskliga översättnings- och maskinöversättningsarbetsflödena som körs på resurserna.

Översättningsprojekt är långvariga objekt som definieras av språk och översättningsmetod/leverantör för att anpassas till organisationsstyrning för globalisering. De bör initieras en gång, antingen under den inledande översättningen eller manuellt, och förbli i kraft under innehålls- och översättningsuppdateringen.

Översättningsprojekt och jobb skapas med arbetsflöden för översättningsförberedelser. Dessa arbetsflöden har tre alternativ, både för inledande översättning (Skapa och översätt) och uppdateringar (Uppdatera översättning):

1. [Skapa nytt projekt](#creating-translation-projects-using-the-references-panel)
1. [Lägg till i befintligt projekt](#adding-pages-to-a-translation-project)
1. [Endast innehållsstruktur](#creating-the-structure-of-a-language-copy)

AEM identifierar om ett översättningsprojekt skapas för den inledande översättningen av innehåll eller för att uppdatera redan översatta språkkopior. När du skapar ett översättningsprojekt för en sida och anger vilka språkkopior du översätter för, identifierar AEM om källsidan redan finns i målspråkskopiorna:

* **Språkkopian innehåller inte sidan:** AEM behandlar denna situation som den inledande översättningen. Sidan kopieras omedelbart till språkkopian och inkluderas i projektet. När den översatta sidan importeras till AEM kopieras AEM den direkt till språkkopian.
* **Språkkopian innehåller redan sidan:** AEM behandlar den här situationen som en uppdaterad översättning. En startsida skapas och en kopia av sidan läggs till i startprogrammet och ingår i projektet. Med det här programmet kan du granska uppdaterade översättningar innan du implementerar dem i språkkopian:

   * När den översatta sidan importeras till AEM, skrivs sidan över vid start.
   * Den översatta sidan skriver bara över språkkopian när startsidan höjs.

Till exempel `/content/wknd/fr` språkrot skapas för den franska översättningen av `/content/wknd/en` huvudspråk. Det finns inga andra sidor i den franska språkversionen.

* Ett översättningsprojekt skapas för `/content/wknd/en/products` sida och alla underordnade sidor, med den franska språkkopian som mål. Eftersom språkkopian inte innehåller `/content/wknd/fr/products` AEM kopierar omedelbart `/content/wknd/en/products` och alla underordnade sidor till den franska språkkopian. Kopiorna ingår också i översättningsprojektet.
* Ett översättningsprojekt skapas för `/content/wknd/en` sida och alla underordnade sidor, med den franska språkkopian som mål. Eftersom språkkopian innehåller den sida som motsvarar `/content/wknd/en` (språkroten), AEM kopierar `/content/wknd/en` och alla underordnade sidor och lägger till dem i en programstart. Kopiorna ingår också i översättningsprojektet.

## Översättning från webbplatskonsolen {#performing-initial-translations-and-updating-existing-translations}

Översättningsprojekt kan skapas eller uppdateras direkt från webbplatskonsolen.

### Skapa översättningsprojekt med referenspanelen {#creating-translation-projects-using-the-references-panel}

Skapa översättningsprojekt så att du kan köra och hantera arbetsflödet för översättning av resurserna i din språkinställning. När du skapar projekt anger du sidan i den språkmall som du översätter och de språkkopior som du utför översättningen för:

* Molnkonfigurationen för översättningsintegreringsramverket som är associerat med den valda sidan avgör många egenskaper för översättningsprojekten, till exempel översättningsarbetsflödet som ska användas.
* Ett projekt skapas för varje vald språkkopia.
* En kopia av den valda sidan och associerade resurser skapas och läggs till i varje projekt. Dessa kopior skickas senare till översättningsleverantören för översättning.

Du kan ange att de underordnade sidorna för den markerade sidan också ska vara markerade. I det här fallet läggs kopior av de underordnade sidorna också till i varje projekt så att de översätts. När underordnade sidor är kopplade till olika konfigurationer för översättningsintegreringsramverk skapar AEM ytterligare projekt.

Du kan också [skapa översättningsprojekt manuellt](#creating-a-translation-project-using-the-projects-console).

>[!NOTE]
>
>Om du vill skapa ett projekt måste ditt konto vara medlem i `project-administrators` grupp.

### Initiala översättningar och uppdatering av översättningar {#initial-and-updating}

Referenspanelen anger om du uppdaterar befintliga språkkopior eller skapar den första versionen av språkkopiorna. När det finns en språkkopia för den valda sidan visas fliken Uppdatera språkkopior för att ge åtkomst till projektrelaterade kommandon.

![Uppdatera språkkopior](../assets/update-language-copies.png)

Efter översättning kan du [granska översättningen](#reviewing-and-promoting-updated-content) innan språkkopian skrivs över med den. Om det inte finns någon språkkopia för den valda sidan visas fliken Skapa och översätt för att ge åtkomst till projektrelaterade kommandon.

![Skapa och översätta](../assets/create-and-translate.png)

### Skapa översättningsprojekt för en ny språkkopia {#create-translation-projects-for-a-new-language-copy}

1. Använd webbplatskonsolen för att välja sidan som du lägger till i översättningsprojekt.

1. Öppna verktygsfältet **Referenser** järnväg.

   ![Referenser](../assets/references.png)

1. Välj **Språkkopior** och välj sedan de språkkopior som du översätter källsidorna för.
1. Välj **Skapa och översätta** och konfigurera översättningsjobbet:

   * Använd **Språk** för att välja en språkkopia som du vill översätta. Välj ytterligare språk efter behov. De språk som visas i listan motsvarar [språktrötter som du har skapat](preparation.md#creating-a-language-root).
      * Om du väljer flera språk skapas ett projekt med ett översättningsjobb för varje språk.
   * Om du vill översätta den markerade sidan och alla underordnade sidor väljer du **Markera alla undersidor**. Om du bara vill översätta den markerade sidan avmarkerar du alternativet.
   * För **Projekt**, markera **Skapa översättningsprojekt**.
   * Valfritt för **Projektmall** väljer du ett projekt som användarroller och behörigheter ska ärvas från.
   * I **Titel** skriv ett namn för projektet.

   ![Skapa översättningsprojekt](../assets/create-translation-project.png)

1. Välj **Skapa**.

### Skapa översättningsprojekt för en befintlig språkkopia {#create-translation-projects-for-an-existing-language-copy}

1. Använd webbplatskonsolen för att välja sidan som du lägger till i översättningsprojekten.

1. Öppna verktygsfältet **Referenser** järnväg.

   ![Referenser](../assets/references.png)

1. Välj **Språkkopior** och välj sedan de språkkopior som du översätter källsidorna för.
1. Välj **Uppdatera språkkopior** och konfigurera översättningsjobbet:

   * Om du vill översätta den markerade sidan och alla underordnade sidor väljer du **Markera alla undersidor**. Om du bara vill översätta den markerade sidan avmarkerar du alternativet.
   * För **Projekt**, markera **Skapa översättningsprojekt**.
   * Valfritt för **Projektmall** väljer du ett projekt som användarroller och behörigheter ska ärvas från.
   * I **Titel** skriv ett namn för projektet.

   ![Skapa projekt för att uppdatera språkkopior](../assets/create-update-language-copies-project.png)

1. Välj **Skapa**.

### Lägga till sidor i ett översättningsprojekt {#adding-pages-to-a-translation-project}

När du har skapat ett översättningsprojekt kan du använda **Resurs** för att lägga till sidor i projektet. Det är praktiskt att lägga till sidor när du inkluderar sidor från olika grenar i samma projekt.

När du lägger till sidor i ett översättningsprojekt inkluderas sidorna i ett nytt översättningsjobb. Du kan också [lägga till sidor i ett befintligt jobb](#adding-pages-assets-to-a-translation-job).

När du lägger till sidor i ett projekt läggs kopior av sidorna till i en programstart när det behövs för att undvika att befintliga språkkopior skrivs över. (Se [Skapa översättningsprojekt för befintliga språkkopior](#performing-initial-translations-and-updating-existing-translations).)

1. Använd webbplatskonsolen för att välja sidan som du lägger till i översättningsprojektet.

1. Öppna verktygsfältet **Referenser** järnväg.

   ![Referenser](../assets/references.png)

1. Välj **Språkkopior** och välj sedan de språkkopior som du översätter källsidorna för.

   ![Uppdatera språkkopior från referensfältet](../assets/update-language-copies-references.png)

1. Välj **Uppdatera språkkopior** och konfigurera sedan egenskaperna:

   * Om du vill översätta den markerade sidan och alla underordnade sidor väljer du **Markera alla undersidor**. Om du bara vill översätta den markerade sidan avmarkerar du alternativet.
   * För **Projekt**, markera **Lägg till i befintligt översättningsprojekt**.
   * Välj projektet i **Befintligt översättningsprojekt**.

   >[!NOTE]
   >
   >Målspråket som anges i översättningsprojektet ska matcha sökvägen för språkkopian enligt referenspunkterna.

1. Välj **Uppdatera**.

### Skapa strukturen för en språkkopia {#creating-the-structure-of-a-language-copy}

Det går bara att skapa strukturen för språkkopian, så att du kan kopiera innehåll och strukturella ändringar i språkinställningen till (oöversatta) språkkopior. Detta har ingenting med översättningsjobb eller -projekt att göra. Du kan använda detta för att synkronisera dina språkmallsidor, även utan översättning.

Fyll i din språkkopia så att den innehåller innehåll från huvudspråket som du översätter. Innan du fyller i din språkkopia måste du ha [skapade språkroten](preparation.md#creating-a-language-root) av språkversionen.

1. Använd webbplatskonsolen för att välja språkroten för huvudspråket som du använder som källa.
1. Öppna referenslisten genom att klicka eller trycka **Referenser** i verktygsfältet.

   ![Referenser](../assets/references.png)

1. Välj **Språkkopior** och välj sedan de språkkopior som du vill fylla i.

   ![Välj språkkopior](../assets/language-copy-structure-select.png)

1. Välj **Uppdatera språkkopior** för att visa översättningsverktygen och konfigurera egenskaperna:

   * Välj **Markera alla undersidor** alternativ.
   * För **Projekt**, markera **Skapa endast struktur**.

   ![Endast struktur](../assets/language-copy-structure-only.png)

1. Välj **Uppdatera**.

### Uppdaterar översättningsminne {#updating-translation-memory}

Manuella redigeringar av översatt innehåll kan synkroniseras tillbaka till översättningshanteringssystemet (TMS) för att utbilda översättningsminnet.

1. När du har uppdaterat textinnehåll på en översatt sida i webbplatskonsolen väljer du **Uppdatera översättningsminne**.
1. I en listvy visas en jämförelse sida vid sida av källan och översättningen för alla textkomponenter som redigerades. Välj vilka översättningsuppdateringar som ska synkroniseras med översättningsminnet och välj **Uppdatera minne**.

![Jämför ändringar av översättningsminne](../assets/update-translation-memory-compare.png)

AEM uppdaterar översättningen av de befintliga strängarna i översättningsminnet för den konfigurerade TMS:en.

* Åtgärden uppdaterar översättningen av befintliga strängar i översättningsminnet för den konfigurerade TMS:en.
* Det skapar inte nya översättningsjobb.
* Det skickar översättningarna tillbaka till TMS via AEM översättnings-API (se nedan).

Så här använder du funktionen:

* En TMS måste konfigureras för användning med AEM.
* Kopplingen måste implementera metoden [`storeTranslation`](https://developer.adobe.com/experience-manager/reference-materials/cloud-service/javadoc/com/adobe/granite/translation/api/TranslationService.html).
   * Koden i den här metoden avgör vad som händer med uppdateringsbegäran för översättningsminnet.
   * Det AEM översättningsramverket skickar strängvärdepar (original och uppdaterad översättning) tillbaka till TMS via den här metodimplementeringen.

Uppdateringarna av översättningsminnet kan fångas upp och skickas till en anpassad destination, i de fall där ett tillverkarspecifikt översättningsminne används.

### Kontrollera översättningsstatus för en sida {#check-translation-status}

En egenskap kan väljas i listvyn i webbplatskonsolen som visar om en sida har översatts, är i översättning eller ännu inte har översatts.

1. I platskonsolen växlar du till [listvy](/help/sites-cloud/authoring/basic-handling.md#viewing-and-selecting-resources).
1. Välj, **Visa inställningar** i listrutan.
1. I dialogrutan markerar du **Översatt** egenskap och välj **Uppdatera**.

Platskonsolen visar nu **Översatt** kolumn som visar översättningsstatusen för de listade sidorna.

![Översättningsstatus i listvyn](../assets/translation-status-list-view.png)

## Hantera översättningsprojekt från projektkonsolen

Många översättningsuppgifter och avancerade alternativ finns i projektkonsolen.

### Om projektkonsolen

Översättningsprojekt i AEM använder standarden [AEM projektkonsol](/help/sites-cloud/authoring/projects/overview.md). Om du inte är van vid AEM kan du läsa den dokumentationen.

Som alla andra projekt består ett översättningsprojekt av plattor som ger en översikt över projektuppgifterna.

![Översättningsprojekt](../assets/translation-project.png)

* **Sammanfattning** - En översikt över projektet
* **Uppgifter** - en eller flera översättningsuppgifter
* **Team** - Användare som samarbetar i översättningsprojektet
* **Uppgifter** - Objekt som måste fyllas i som en del av översättningsarbetet

Använd kommandona och ellipsknapparna längst upp och längst ned på plattorna (respektive) för att komma åt kontroller och alternativ för de olika plattorna.

![Knappen Kommandon](../assets/context.png)

![Ellipsknapp](../assets/ellipsis.png)

### Skapa ett översättningsprojekt med projektkonsolen {#creating-a-translation-project-using-the-projects-console}

Du kan skapa ett översättningsprojekt manuellt om du föredrar att använda projektkonsolen i stället för platskonsolen.

>[!NOTE]
>
>Om du vill skapa ett projekt måste ditt konto vara medlem i `project-administrators` grupp.

När du skapar ett översättningsprojekt manuellt måste du ange värden för följande översättningsrelaterade egenskaper utöver de [grundläggande egenskaper](/help/sites-cloud/authoring/projects/managing.md#creating-a-project):

* **Namn:** Projektnamn
* **Källspråk:** Källinnehållets språk
* **Målspråk:** Det eller de språk som innehållet översätts till
   * Om du väljer flera språk skapas ett jobb för varje språk i projektet.
* **Översättningsmetod:** Välj **Översättning av människor** för att ange att översättningen ska utföras manuellt.

1. I verktygsfältet i projektkonsolen väljer du **Skapa**.
1. Välj **Översättningsprojekt** mall och välj sedan **Nästa**.
1. Ange värden för **Grundläggande** egenskapsfliken.
1. Välj **Avancerat** och ange värden för översättningsrelaterade egenskaper.
1. Välj **Skapa**. I bekräftelserutan väljer du **Klar** för att gå tillbaka till projektkonsolen, eller välj **Öppna projekt** för att öppna och börja hantera projektet.

### Lägga till sidor och resurser i ett översättningsjobb {#adding-pages-assets-to-a-translation-job}

Du kan lägga till sidor, resurser eller taggar i översättningsjobbet för översättningsprojektet. Så här lägger du till sidor eller resurser:

1. Markera ellipsen längst ned i översättningsjobbpanelen i översättningsprojektet.

   ![Översättningsjobbpanel](../assets/translation-job.png)

1. Välj **Lägg till** i verktygsfältet och sedan markera **Resurser/sidor**.

   ![Lägga till sidor](../assets/add-to-project.png)

1. I det modala fönstret markerar du det översta objektet i grenen som du vill lägga till och markerar sedan bockmarkeringsikonen. Flerval är aktiverat i det här fönstret.

   ![Markera sidor](../assets/select-pages.png)

1. Du kan också välja sökikonen för att enkelt söka efter sidor eller resurser som du vill lägga till i översättningsjobbet.

   ![Sök efter innehåll](../assets/search-for-content.png)

1. När du har valt **Välj**. Dina sidor och/eller resurser läggs till i översättningsjobbet.

>[!TIP]
>
>Den här metoden lägger till sidor/resurser och deras underordnade sidor i projektet. Välj **Resurs/sida (utan underordnade)** om du bara vill lägga till de överordnade.

### Lägga till taggar i ett översättningsjobb {#adding-tags-to-a-translation-job}

Du kan lägga till taggar i ett översättningsprojekt som liknar [hur du lägger till resurser och sidor i ett projekt](#adding-pages-assets-to-a-translation-job). Välj bara **Taggar** under **Lägg till** sedan följer du samma steg.

### Visa information om översättningsprojekt {#seeing-translation-project-details}

Översättningsprojektegenskaperna är tillgängliga via ellipsknappen i sammanfattningsrutan för projektet. Förutom generiska [projektinformation](/help/sites-cloud/authoring/projects/overview.md#project-info), innehåller översättningsprojektegenskaperna översättningsspecifika.

I översättningsprojektet väljer du ellipsen längst ned i rutan Översättningssammanfattning. De flesta projektspecifika egenskaper finns på **Avancerat** -fliken.

* **Källspråk:** Språket för de sidor som översätts
* **Målspråk:** Det eller de språk som sidorna översätts till
* **Molnkonfiguration:** Molnkonfigurationen för översättningstjänstkopplingen som används för projektet
* **Översättningsmetod:** Översättningsarbetsflödet **Översättning av människor** eller **Maskinöversättning**
* **Översättningsprovider:** Översättningstjänstleverantören som utför översättningen
* **Innehållskategori:** (Maskinöversättning) Innehållskategorin som används för översättning
* **Autentiseringsuppgifter för översättningsprovider:** Autentiseringsuppgifterna för att logga in på providern
* **Befordra översättningsstarter automatiskt:** Efter att ha tagit emot översatt innehåll befordras översättningsöppningar automatiskt
   * **Ta bort start efter befordran:** Om översättningsstarter befordras automatiskt tar du bort starten efter beställningen
* **Godkänn översättningar automatiskt:** När översatt innehåll har tagits emot godkänns översättningsjobb automatiskt
* **Upprepa översättning:** Konfigurera återkommande körning av ett översättningsprojekt genom att välja den frekvens som projektet automatiskt skapar och kör översättningsjobb

När ett projekt skapas med referenslinjen för en sida, konfigureras dessa egenskaper automatiskt baserat på källsidans egenskaper.

![Översättningsprojektsegenskaper](../assets/translation-project-properties.png)

### Övervaka status för ett översättningsjobb {#monitoring-the-status-of-a-translation-job}

Översättningsjobbpanelen i ett översättningsprojekt anger status för ett översättningsjobb och antalet sidor och resurser i jobbet.

![Översättningsjobb](../assets/translation-job.png)

I följande tabell beskrivs varje status som ett jobb eller ett objekt i jobbet kan ha:

| Status | Beskrivning |
|---|---|
| **Utkast** | Översättningsjobbet har inte startats. Översättningsjobb finns i **Utkast** när de skapas. |
| **Skickat** | Filer i översättningsjobbet har den här statusen när de har skickats till översättningstjänsten. Den här statusen kan inträffa efter **Begär omfång** kommandot eller **Starta** kommandot är utfärdat. |
| **Begärt omfång** | Filerna i jobbet har skickats till översättningsleverantören för omfång för det mänskliga översättningsarbetsflödet. Den här statusen visas efter **Begär omfång** kommandot är utfärdat. |
| **Omfånget har slutförts** | Leverantören har omfattat översättningsjobbet. |
| **Bekräftat för översättning** | Projektägaren har accepterat omfattningen. Den här statusen anger att översättningsleverantören ska börja översätta filerna i jobbet. |
| **Översättning pågår** | För ett jobb är översättningen av en eller flera filer i jobbet inte slutförd än. För ett objekt i jobbet översätts objektet. |
| **Översatt** | För ett jobb är översättningen av alla filer i jobbet slutförd. För ett objekt i jobbet översätts objektet. |
| **Klar för granskning** | Objektet i jobbet översätts och filen har importerats till AEM. |
| **Complete** | Projektägaren har angett att översättningskontraktet är slutfört. |
| **Avbryt** | Anger att översättningsleverantören ska sluta arbeta med ett översättningsjobb. |
| **Feluppdatering** | Ett fel uppstod när filer överfördes mellan AEM och översättningstjänsten. |
| **Okänt läge** | Ett okänt fel har inträffat. |

Om du vill se status för varje fil i jobbet väljer du ellipsen längst ned i rutan.

### Ange förfallodatum för översättningsjobb {#setting-the-due-date-of-translation-jobs}

Ange det datum före vilket översättningsleverantören måste returnera översatta filer. Inställningen av förfallodatumet fungerar bara korrekt när översättningsleverantören som du använder har stöd för den här funktionen.

1. Markera ellipsen längst ned i översättningssammanfattningsrutan.

   ![Översättningssammanfattningsruta](../assets/translation-summary-tile.png)

1. På **Grundläggande** använder du datumväljaren på fliken **Förfallodatum** för att välja förfallodatum.

   ![Översättningsprojektsegenskaper](../assets/translation-project-properties-basic.png)

1. Välj **Spara och stäng**.

### Omfång för ett översättningsjobb {#scoping-a-translation-job}

Använd ett översättningsjobb för att få en uppskattning av översättningskostnaden från din översättningstjänstleverantör. När du omsluter ett jobb skickas källfiler till översättningsleverantören som jämför texten med deras pool med lagrade översättningar (översättningsminne). Vanligtvis är omfattningen antalet ord som måste översättas.

Kontakta översättningsleverantören om du vill ha mer information om omfångsresultat.

>[!NOTE]
>
>Omfattningen är valfri och gäller endast för mänsklig översättning. Du kan starta ett översättningsjobb utan omfång.

När du omsluter ett översättningsjobb är jobbets status **Begärt omfång**. När översättningsleverantören returnerar omfånget ändras statusen till **Omfånget har slutförts**. När omfånget är klart kan du använda **Visa omfång** för att granska omfångsresultaten.

Omfånget fungerar bara korrekt när den översättningsleverantör som du använder har stöd för den här funktionen.

1. Öppna översättningsprojektet i projektkonsolen.
1. På översättningsjobbets titel väljer du kommandomenyn och sedan **Begär omfång**.
1. När jobbstatusen ändras till **Omfånget har slutförts** väljer du kommandomenyn och väljer **Visa omfång**.

### Startar översättningsjobb {#starting-translation-jobs}

Starta ett översättningsjobb för att översätta källsidorna till målspråket. Översättningen utförs enligt egenskapsvärdena för översättningssammanfattningsrutan.

Du kan starta ett enskilt jobb inifrån projektet.

1. Öppna översättningsprojektet i projektkonsolen.
1. På översättningsjobbpanelen väljer du kommandomenyn och sedan **Starta**.
1. I åtgärdsdialogrutan som bekräftar översättningens början väljer du **Stäng**.

När du har startat översättningsjobbet visas översättningen i **Pågår** status.

Du kan också starta alla översättningsjobb för ett projekt.

1. Välj översättningsprojektet i projektkonsolen.
1. I verktygsfältet markerar du **Starta översättningsjobb**.
1. Granska listan över jobb som har startats i dialogrutan och bekräfta sedan med **Starta** eller avbryta med **Avbryt**.

### Avbryta ett översättningsjobb {#canceling-a-translation-job}

Avbryt ett översättningsjobb om du vill stoppa översättningsprocessen och förhindra att översättningsleverantören utför fler översättningar. Du kan avbryta ett jobb när jobbet har **Bekräftat för översättning** eller **Översättning pågår** status.

1. Öppna översättningsprojektet i projektkonsolen.
1. På översättningsjobbpanelen väljer du kommandomenyn och sedan **Avbryt**.
1. I åtgärdsdialogrutan som bekräftar att översättningen har avbrutits väljer du **OK**.

### Acceptera och ignorera arbetsflöde {#accept-reject-workflow}

När innehållet kommer tillbaka efter översättning och är i **Klar för granskning** kan du gå in i översättningsjobbet och acceptera/avvisa innehåll.

Om du väljer **Avvisa översättning** kan du lägga till en kommentar.

Om du avvisar innehåll skickas det tillbaka till översättningsleverantören där de kan se kommentaren.

### Slutföra och arkivera översättningsjobb {#completing-and-archiving-translation-jobs}

Slutför ett översättningsjobb när du har granskat de översatta filerna från leverantören.

1. Öppna översättningsprojektet i projektkonsolen.
1. På översättningsjobbpanelen väljer du kommandomenyn och sedan **Complete**.
1. Jobbet har nu statusen **Complete**.

För mänskliga översättningsarbetsflöden anger en översättning för leverantören att översättningsavtalet har uppfyllts och att de bör spara översättningen till sitt översättningsminne.

Arkivera ett översättningsjobb när det är klart och du behöver inte längre se jobbstatusinformation.

1. Öppna översättningsprojektet i projektkonsolen.
1. På översättningsjobbpanelen väljer du kommandomenyn och sedan **Arkiv**.

När du arkiverar jobbet tas översättningsjobbpanelen bort från projektet.

## Granska och använda översatt innehåll {#reviewing-and-promoting-updated-content}

Du kan använda webbplatskonsolen för att granska innehåll, jämföra språkkopior och aktivera innehållet.

### Befordra uppdaterat innehåll {#promoting-updated-content}

När innehåll översätts för en befintlig språkkopia granskar du översättningarna, gör ändringar om det behövs och höjer sedan översättningarna så att de flyttas till språkkopian. Du kan granska översatta filer när översättningsjobbet visar **Klar för granskning** status.

![Jobbet är klart för granskning](../assets/job-ready-for-review.png)

1. Markera sidan i språkmallen och välj **Referenser** väljer **Språkkopior**.
1. Välj den språkkopia som ska granskas.

   ![Språkkopia klar för granskning](../assets/language-copy-ready-for-review.png)

1. Välj **Starta** för att visa startrelaterade kommandon.

   ![Startar](../assets/language-copy-launch.png)

1. Om du vill öppna startkopian av sidan för att granska och redigera innehållet klickar du på **Öppna sida**.
1. När du har granskat innehållet och gjort de ändringar som krävs befordrar du en startkopia genom att klicka **Befordra**.
1. På **Promote Launch** sida, ange vilka sidor som ska befordras och markera sedan **Befordra**.

### Jämför språkkopior {#comparing-language-copies}

Så här jämför du språkkopior med språkinställningen:

1. Gå till den språkkopia som du vill jämföra i webbplatskonsolen.
1. Öppna [Referensspår](/help/sites-cloud/authoring/basic-handling.md#references).
1. Under **Kopior** rubrikmarkera **Språkkopior.**
1. Välj en språkversion och sedan kan du antingen klicka **Jämför med mallsida** eller **Jämför med föregående** om tillämpligt.

   ![Jämför språkkopior](../assets/language-copy-compare.png)

1. De två sidorna (start och källa) öppnas sida vid sida.
   * Mer information om hur du använder den här funktionen finns i [Sidskillnader](/help/sites-cloud/authoring/sites-console/page-diff.md).

## Flytta eller byta namn på en källsida {#move-source}

Om en redan översatt källsida måste [ändrat namn eller flyttat](/help/sites-cloud/authoring/sites-console/managing-pages.md#moving-or-renaming-a-page)när du översätter sidan igen efter flytten skapas en språkkopia baserad på det nya sidnamnet/den nya sidplatsen. Den gamla språkkopian som baseras på föregående namn/plats finns fortfarande kvar. Du kan förhindra detta genom att använda funktionen för att kopiera uppdateringsspråk efter flytten:

1. Flytta en sida som har en språkkopia.
1. Välj språkkopieringsroten.
1. Öppna **Referenser** -panelen.
1. Välj **Språk Kopior**.
1. Välj de målspråk som du vill uppdatera.
1. Välj **Uppdatera språkkopior**.

   ![update-language-copies](../assets/translation-move-to.png)

1. Klicka **Uppdatera**. A [Starta](/help/sites-cloud/authoring/launches/promoting.md) skapas.
1. Navigera till den önskade språkroten och markera den.
1. Använda **Referenser** panel, markera **Startar**.

   ![Promot-launch-translation](../assets/promote-launch-translation.png)

1. Klicka på Launch som skapades och klicka på **Befordra lansering**.

Nu har källsidan flyttats och tillhörande språkkopia.

## Importera och exportera översättningsjobb {#import-export}

Även om AEM erbjuder flera översättningslösningar och gränssnitt går det även att importera och exportera översättningsjobbsinformation manuellt.

### Exportera ett översättningsjobb {#exporting-a-translation-job}

Du kan hämta innehållet i ett översättningsjobb, till exempel för att skicka till en översättningsleverantör som inte är integrerad med AEM via en koppling, eller för att granska innehållet.

1. I översättningsjobbpanelens nedrullningsbara meny väljer du **Exportera**.
1. I dialogrutan väljer du **Hämta exporterad fil** och om det behövs kan du spara filen i webbläsardialogrutan.
1. I dialogrutan väljer du **Stäng**.

### Importera ett översättningsjobb {#importing-a-translation-job}

Du kan importera översatt innehåll till AEM när översättningsleverantören skickar det till dig eftersom det inte är integrerat med AEM via en koppling.

1. I översättningsjobbpanelens nedrullningsbara meny väljer du **Importera**.
1. Använd webbläsarens dialogruta för att markera filen som ska importeras.
1. I dialogrutan väljer du **Stäng**.
