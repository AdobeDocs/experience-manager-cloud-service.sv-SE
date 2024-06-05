---
title: Översätta innehåll
description: Använd översättningskopplingen och reglerna för att översätta innehållet.
index: true
hide: false
hidefromtoc: false
exl-id: b8ab2525-3f15-4844-866c-da47bfc7518c
solution: Experience Manager Sites
feature: Translation
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '2526'
ht-degree: 0%

---

# Översätta innehåll {#translate-content}

Använd översättningskopplingen och reglerna för att översätta innehållet.

## Story hittills {#story-so-far}

I det föregående dokumentet om AEM Sites översättningsresa [Konfigurera översättningsregler](translation-rules.md) du lärde dig att använda AEM översättningsregler för att identifiera översättningsinnehåll. Nu bör du:

* Förstå vad översättningsreglerna gör.
* Ange egna översättningsregler.

Nu när du har konfigurerat dina regler för koppling och översättning tar den här artikeln dig igenom nästa steg när du översätter ditt AEM Sites-innehåll.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur du använder AEM översättningsprojekt tillsammans med kopplingen och dina översättningsregler för att översätta innehåll. När du har läst det här dokumentet bör du:

* Förstå vad ett översättningsprojekt är.
* Skapa nya översättningsprojekt.
* Använd översättningsprojekt för att översätta ditt AEM Sites-innehåll.

## Skapa ett översättningsprojekt {#creating-translation-project}

Med översättningsprojekt kan du hantera översättning av AEM. Ett översättningsprojekt samlar det innehåll som ska översättas på en plats för att få en central bild av översättningsarbetet.

När innehåll läggs till i ett översättningsprojekt skapas ett översättningsjobb för det. Jobb innehåller kommandon och statusinformation som du använder för att hantera de mänskliga översättnings- och maskinöversättningsarbetsflödena som körs på resurserna.

Översättningsprojekt kan skapas på två sätt:

1. Välj språkroten för innehållet och låt AEM automatiskt skapa översättningsprojektet baserat på innehållssökvägen.
1. Skapa ett tomt projekt och välj manuellt det innehåll som ska läggas till i översättningsprojektet

Båda metoderna är vanligtvis bara olika beroende på vilken person som utför översättningen:

* Översättningsprojektledaren (TPM) behöver ofta flexibiliteten att manuellt välja innehåll till översättningsprojektet.
* Om innehållsägaren också ansvarar för översättning är det ofta enklare att låta AEM automatiskt skapa projektet baserat på den valda innehållssökvägen.

Båda metoderna beskrivs i följande avsnitt.

### Skapa ett översättningsprojekt automatiskt baserat på innehållssökväg {#automatically-creating}

För rättighetsinnehavare som också ansvarar för översättning är det ofta enklare att AEM automatiskt skapa översättningsprojektet. Så här skapar AEM automatiskt ett översättningsprojekt baserat på din innehållssökväg:

1. Navigera till **Navigering** > **Webbplatser** och välj projekt.
1. Leta reda på projektets språkrot. Om du t.ex. har språkroten engelska `/content/<your-project>/en`.
   * Före den första översättningen är de andra språkmapparna tomma platshållare. Dessa skapas vanligtvis av innehållsarkitekten.
1. Leta reda på projektets språkrot.
1. Markera spårväljaren och visa **Referenser** -panelen.
1. Välj **Språkkopior**.
1. Kontrollera **Språkkopior** kryssrutan.
1. Expandera avsnittet **Uppdatera språkkopior** längst ned på referenspanelen.
1. I **Projekt** nedrullningsbar lista, välja **Skapa översättningsprojekt**.
1. Ange en lämplig titel för översättningsprojektet.
1. Välj **Uppdatera**.

![Skapa ett översättningsprojekt](assets/create-translation-project.png)

Du får ett meddelande om att projektet har skapats.

>[!NOTE]
>
>Det antas att den nödvändiga språkstrukturen för översättningsspråken redan har skapats som en del av [definition av innehållsstrukturen.](getting-started.md#content-structure) Detta bör göras i samarbete med innehållsarkitekten.
>
>Om språkmapparna inte skapas i förväg kommer du inte att kunna skapa språkkopior enligt beskrivningen i föregående steg.

### Skapa ett översättningsprojekt manuellt genom att välja ditt innehåll {#manually-creating}

För översättningsprojektledare är det ofta nödvändigt att manuellt välja specifikt innehåll som ska inkluderas i ett översättningsprojekt. Om du vill skapa ett sådant manuellt översättningsprojekt måste du börja med att skapa ett tomt projekt och sedan välja det innehåll som ska läggas till i det.

1. Navigera till **Navigering** > **Projekt**.
1. Välj **Skapa** > **Mapp** för att skapa en mapp för dina projekt.
   * Detta är valfritt, men användbart om du vill organisera översättningsarbetet.
1. I **Skapa projekt** fönster, lägga till **Titel** för mappen och välj **Skapa**.

   ![Skapa projektmapp](assets/create-project-folder.png)

1. Markera mappen som du vill öppna.
1. I den nya projektmappen väljer du **Skapa** > **Projekt**.
1. Projekten bygger på mallar. Välj **Översättningsprojekt** mall för att markera den och sedan välja **Nästa**.

   ![Välj översättningsprojektmall](assets/select-translation-project-template.png)

1. På **Grundläggande** anger du ett namn för det nya projektet.

   ![Grundläggande projektflik](assets/project-basic-tab.png)

1. På **Avancerat** -fliken använder du **Målspråk** för att välja vilka språk ditt innehåll ska översättas till. Välj **Skapa**.

   ![Avancerad flik i projekt](assets/project-advanced-tab.png)

1. Välj **Öppna** i bekräftelsedialogrutan.

   ![Bekräftelsedialogruta för projekt](assets/project-confirmation-dialog.png)

Projektet har skapats, men innehåller inget innehåll att översätta. I nästa avsnitt beskrivs hur projektet är strukturerat och hur du lägger till innehåll.

## Använda ett översättningsprojekt {#using-translation-project}

Översättningsprojekt är utformade för att samla allt innehåll och alla uppgifter som hör till en översättningssatsning på ett och samma ställe så att översättningen blir enkel och enkel att hantera.

Så här visar du översättningsprojektet:

1. Navigera till **Navigering** > **Projekt**.
1. Välj det projekt som skapades i föregående avsnitt (antingen [Skapa ett översättningsprojekt automatiskt baserat på innehållssökväg](#automatically-creating) eller [Skapa ett översättningsprojekt manuellt genom att välja ditt innehåll](#manually-creating) beroende på din situation).

![Översättningsprojekt](assets/translation-project.png)

Projektet är uppdelat i flera kort.

* **Sammanfattning** - Det här kortet visar grundläggande rubrikinformation för projektet inklusive ägare, språk och översättningsleverantör.
* **Översättningsjobb** - Kortet eller korten ger en översikt över det faktiska översättningsjobbet inklusive status, antal resurser och så vidare. Vanligtvis finns det ett jobb per språk med ISO-2-språkkoden tillagd till jobbnamnet.
   * När [automatiskt skapa översättningsjobb,](#automatically-creating) AEM skapar jobben asynkront och kanske inte visas direkt i projektet.
* **Team** - Det här kortet visar vilka användare som samarbetar i det här översättningsprojektet. Den här resan täcker inte det här ämnet.
* **Uppgifter** - Ytterligare uppgifter som är kopplade till översättning av innehåll som att göra objekt eller arbetsflödesobjekt. Den här resan täcker inte det här ämnet.

En ändring av projektinställningarna är användbar för att bättre förstå översättningsflödet i AEM. Det här steget krävs inte för produktionsöversättningar, men underlättar förståelsen av processen.

1. På **Sammanfattning** markerar du ellipsknappen längst ned på kortet.
1. På **Avancerat** -flik, avmarkera alternativet **Ta bort start efter erbjudande**.

   ![Ta bort startdatum efter erbjudandealternativ](assets/delete-launch-option.png)

1. Välj **Spara och stäng**.

Nu kan du börja använda ditt översättningsprojekt. Hur du använder ett översättningsprojekt beror på hur det skapades: antingen automatiskt AEM eller manuellt.

### Använda ett automatiskt skapat översättningsprojekt {#using-automatic-project}

När du automatiskt skapar översättningsprojektet utvärderar AEM innehållet under den sökväg du valde baserat på översättningsreglerna som du tidigare definierade. Utifrån utvärderingen extraheras det innehåll som kräver översättning till ett nytt översättningsprojekt.

Om du vill se detaljerna i innehållet som ingår i det här projektet:

1. Markera ellipsknappen längst ned i **Översättningsjobb** kort.
1. The **Översättningsjobb** visas alla objekt i jobbet.

   ![Information om översättningsjobb](assets/translation-job-detail.png)

1. Markera en rad om du vill se detaljerna på den raden, och tänk på att en rad kan representera flera innehållsobjekt som ska översättas.
1. Markera kryssrutan för val för ett radobjekt om du vill se ytterligare alternativ, t.ex. alternativet att ta bort det från jobbet eller visa det i platskonsolen.

   ![Alternativ för översättningsjobb](assets/translation-job-options.png)

Översättningsjobbets innehåll startar vanligtvis i **Utkast** enligt **Läge** kolumn i **Översättningsjobb** -fönstret.

Om du vill starta översättningsjobbet går du tillbaka till översättningsprojektöversikten och väljer knappen för nedstapeln längst upp i **Översättningsjobb** och välj **Starta**.

![Starta översättningsjobb](assets/start-translation-job.png)

AEM kommunicerar nu med din översättningskonfiguration och koppling för att skicka innehållet till översättningstjänsten. Du kan visa översättningens förlopp genom att gå tillbaka till **Översättningsjobb** och visa **Läge** kolumn för posterna.

![Översättningsjobbet har godkänts](assets/translation-job-approved.png)

Maskinöversättningar returneras automatiskt med statusen **Godkänd**. Översättning till människor möjliggör mer interaktion, men ligger utanför den här resan.

>[!TIP]
>
>Det kan ta en stund att bearbeta ett översättningsjobb och du kan se att dina översättningsobjekt flyttas från läget **Utkast** till **Översättning pågår** till **Klar för granskning** innan de kommer till **Godkänd** tillstånd. Detta förväntas.

>[!NOTE]
>
>Om du inte inaktiverade projektalternativet **Ta bort start efter erbjudande** as [som beskrivs i föregående avsnitt,](#using-translation-project) översatta objekt visas med **Borttagen** tillstånd. Detta är normalt eftersom AEM automatiskt tar bort översättningsposterna när de översatta objekten kommer fram. De översatta objekten har importerats som språkkopior, men bara översättningsposterna har tagits bort eftersom de inte längre behövs.
>
>Oroa dig inte om det här är oklart. Det här är ingående detaljer om hur AEM fungerar och påverkar inte din förståelse av resan. Om du vill lära dig mer om hur AEM bearbetar översättningar finns mer information i [ytterligare resurser](#additional-resources) i slutet av artikeln.

### Använda ett manuellt skapat översättningsprojekt {#using-manual-project}

När du skapar ett översättningsprojekt manuellt skapar AEM de nödvändiga jobben, men väljer inte automatiskt något innehåll som ska inkluderas i dessa jobb. Detta ger översättningsprojektledaren flexibilitet att välja och välja vilket innehåll som ska översättas.

Så här lägger du till innehåll i ett översättningsjobb:

1. Markera ellipsknappen längst ned på en av **Översättningsjobb** kort.
1. Se till att jobbet inte innehåller något innehåll. Välj **Lägg till** överst i fönstret och sedan **Resurser/sidor** i listrutan.

   ![Tomt översättningsjobb](assets/empty-translation-job.png)

1. En sökvägsläsare öppnas där du kan välja specifikt vilket innehåll som ska läggas till. Leta reda på innehållet och välj det.

   ![Sökvägsläsare](assets/path-browser.png)

1. Välj **Välj** för att lägga till det markerade innehållet i jobbet.
1. I **Översätt** anger du att du vill **Skapa språkkopia**.

   ![Skapa språkkopia](assets/translate-copy-master.png)

1. Innehållet ingår nu i jobbet.

   ![Innehåll som lagts till i översättningsjobb](assets/content-added.png)

1. Markera kryssrutan för val för ett radobjekt om du vill se ytterligare alternativ, t.ex. alternativet att ta bort det från jobbet eller visa det i platskonsolen.

   ![Alternativ för översättningsjobb](assets/translation-job-options.png)

1. Upprepa de här stegen för att inkludera allt nödvändigt innehåll i jobbet.

>[!TIP]
>
>Sökvägsläsaren är ett kraftfullt verktyg med vilket du kan söka efter, filtrera och navigera i innehållet. Välj **Endast innehåll/filter** för att växla sidopanelen och visa avancerade filter som **Ändringsdatum** eller **Översättningsstatus**.
>
>Du kan läsa mer om sökvägsläsaren i [ytterligare resursavsnitt.](#additional-resources)

Du kan använda de föregående stegen för att lägga till nödvändigt innehåll till alla språk (jobb) för projektet. När du har markerat allt innehåll kan du starta översättningen.

Översättningsjobbets innehåll startar vanligtvis i **Utkast** enligt **Läge** kolumn i **Översättningsjobb** -fönstret.

Om du vill starta översättningsjobbet går du tillbaka till översättningsprojektöversikten och väljer knappen för nedstapeln längst upp i **Översättningsjobb** och välj **Starta**.

![Starta översättningsjobb](assets/start-translation-job.png)

AEM kommunicerar nu med din översättningskonfiguration och koppling för att skicka innehållet till översättningstjänsten. Du kan visa översättningens förlopp genom att gå tillbaka till **Översättningsjobb** och visa **Läge** kolumn för posterna.

![Översättningsjobbet har godkänts](assets/translation-job-approved.png)

Maskinöversättningar returneras automatiskt med statusen **Godkänd**. Översättning till människor möjliggör mer interaktion, men ligger utanför den här resan.

>[!TIP]
>
>Det kan ta en stund att bearbeta ett översättningsjobb och du kan se att dina översättningsobjekt flyttas från läget **Utkast** till **Översättning pågår** till **Klar för granskning** innan de kommer till **Godkänd** tillstånd. Detta förväntas.

>[!NOTE]
>
>Om du inte inaktiverade projektalternativet **Ta bort start efter erbjudande** as [som beskrivs i föregående avsnitt,](#using-translation-project) översatta objekt visas med **Borttagen** tillstånd. Detta är normalt eftersom AEM automatiskt tar bort översättningsposterna när de översatta objekten kommer fram. De översatta objekten har importerats som språkkopior, men bara översättningsposterna har tagits bort eftersom de inte längre behövs.
>
>Oroa dig inte om det här är oklart. Det här är ingående detaljer om hur AEM fungerar och påverkar inte din förståelse av resan. Om du vill lära dig mer om hur AEM bearbetar översättningar finns mer information i [ytterligare resurser](#additional-resources) i slutet av artikeln.

## Granskning av översatt innehåll {#reviewing}

[Som tidigare visats](#using-translation-project) maskinöversatt innehåll flödas tillbaka till AEM med statusen **Godkänd** Eftersom antagandet är att maskinöversättning används krävs ingen mänsklig åtgärd. Det går dock fortfarande att granska det översatta innehållet.

Gå bara till det slutförda översättningsjobbet och markera ett radobjekt genom att trycka eller klicka i kryssrutan. Ikonen **Förhandsgranska på platser** visas i verktygsfältet.

![Visa på webbplatser](assets/reveal-in-sites.png)

Välj den ikonen om du vill öppna det översatta innehållet i konsolen och visa information om det översatta innehållet.

![En översatt sida](assets/translated-page.png)

Du kan ändra det översatta innehållet ytterligare, förutsatt att du har rätt behörighet, men att redigera innehåll ligger utanför den här kundresan. Se [Ytterligare resurser](#additional-resources) i slutet av det här dokumentet om du vill ha mer information om det här avsnittet.

Projektets syfte är att samla alla resurser som hör till en översättning på ett och samma ställe för enkel åtkomst och en tydlig översikt. Men som du kan se genom att visa detaljerna för ett översatt objekt, flödar översättningarna i sig tillbaka till webbplatsmappen för översättningsspråket. I det här exemplet är mappen

```text
/content/<your-project>/es
```

Om du navigerar till den här mappen via **Navigering** > **Webbplatser** ser du det översatta innehållet.

![Mappstruktur för översatt innehåll](assets/translated-sites-content.png)

AEM översättningsramverk tar emot översättningarna från översättningskopplingen och skapar sedan automatiskt innehållsstrukturen baserat på språkroten och med hjälp av översättningarna från kopplingen.

Det är viktigt att förstå att detta innehåll inte publiceras och därför inte är tillgängligt för konsumtion. Du lär dig mer om den här strukturen för författarpublicering och hur du publicerar vårt översatta innehåll i nästa steg av översättningsresan.

## Översättning av människor {#human-translation}

Om översättningstjänsten tillhandahåller mänsklig översättning erbjuder granskningsprocessen fler alternativ. Översättningar kommer till exempel tillbaka i projektet med statusen **Utkast** och måste granskas och godkännas eller avvisas manuellt.

Översättning till människor ligger utanför den här lokaliseringsresan. Se [Ytterligare resurser](#additional-resources) i slutet av det här dokumentet om du vill ha mer information om det här avsnittet. Förutom de ytterligare godkännandealternativen är arbetsflödet för mänskliga översättningar detsamma som maskinöversättningar som beskrivs under den här resan.

## What&#39;s Next {#what-is-next}

Nu när du är klar med den här delen av AEM Sites översättningsresa ska du:

* Förstå vad ett översättningsprojekt är.
* Skapa nya översättningsprojekt.
* Använd översättningsprojekt för att översätta innehållet.

Bygg vidare på den här kunskapen och fortsätt din översättning till AEM Sites genom att granska nästa gång dokumentet [Publicera översatt innehåll](publish-content.md) där du lär dig hur du publicerar översatt innehåll och hur du uppdaterar översättningarna när rotinnehållet för ditt språk ändras.

## Ytterligare resurser {#additional-resources}

Vi rekommenderar att du går vidare till nästa del av översättningsresan genom att granska dokumentet [Publicera översatt innehåll,](publish-content.md) Nedan följer ytterligare, valfria resurser som fördjupar sig i några koncept som nämns i det här dokumentet, men som inte behöver fortsätta på resan.

* [Hantera översättningsprojekt](/help/sites-cloud/administering/translation/managing-projects.md) - Läs mer om översättningsprojekt och andra funktioner som arbetsflöden för översättning och flerspråkiga projekt.
* [Redigeringsmiljö och -verktyg](/help/sites-cloud/authoring/path-selection.md#path-selection) - AEM innehåller olika sätt att ordna och redigera ditt innehåll, bland annat en robust sökvägsläsare.
