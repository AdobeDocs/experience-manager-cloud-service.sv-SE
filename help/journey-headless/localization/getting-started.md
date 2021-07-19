---
title: Kom igång med AEM headless-lokalisering
description: Lär dig hur du organiserar ditt headless-innehåll och hur AEM lokaliseringsverktyg fungerar.
source-git-commit: 22ca7c01bfddb407c119de7d9a4d105941772664
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 0%

---

# Kom igång med AEM headless Localization {#getting-started}

Lär dig hur du organiserar ditt headless-innehåll och hur AEM lokaliseringsverktyg fungerar.

## Story hittills {#story-so-far}

I det tidigare dokumentet om den AEM headless-lokaliseringsresan [Lär dig mer om headless-innehåll och hur du lokaliserar i AEM](learn-about.md) lärde du dig den grundläggande teorin om vad ett headless CMS är och du bör nu:

* Förstå de grundläggande begreppen för leverans av headless-innehåll.
* Lär dig hur AEM hanterar headless och lokalisering.

Den här artikeln bygger på dessa grundläggande funktioner så att du förstår hur AEM lagrar och hanterar headless-innehåll och hur du kan använda AEM lokaliseringsverktyg för att översätta innehållet.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur du kommer igång med lokalisering av headless-innehåll i AEM. När du har läst bör du:

* Förstå hur viktig innehållsstrukturen är för lokaliseringen.
* Förstå hur AEM lagrar headless-innehåll.
* Bekanta dig med AEM lokaliseringsverktyg.

## Krav och krav {#requirements-prerequisites}

Det finns ett antal krav innan du börjar lokalisera ditt AEM innehåll.

### Kunskap {#knowledge}

* Lokalisera innehåll för ett CMS-system
* Upplev de grundläggande funktionerna i ett storskaligt CMS-system
* Kunskap AEM grundläggande hantering
* Förståelse för översättningstjänsten som du använder
* Ha en grundläggande förståelse för innehållet som du översätter

>[!TIP]
>
>Om du inte är van vid att använda ett stort CMS-system som AEM bör du granska [Basic Handling](/help/sites-cloud/authoring/getting-started/basic-handling.md)-dokumentationen innan du fortsätter. Dokumentationen för grundläggande hantering är inte en del av resan, så gå tillbaka till den här sidan när du är klar.

### Verktyg {#tools}

* Tillgång till sandlådor för att testa översättning av ditt innehåll
* Autentiseringsuppgifter för att ansluta till den översättningstjänst du föredrar
* Bli medlem i gruppen `project-administrators` i AEM

## Strukturen är nyckeln {#content-structure}

AEM innehåll, oavsett om det är headless eller traditionella webbsidor, styrs av sin struktur. AEM ställer få krav på innehållsstrukturen, men om du tar hänsyn till innehållshierarkin som en del av projektplaneringen blir lokaliseringen mycket enklare.

>[!TIP]
>
>Planera för översättning och lokalisering i början av det headless-projektet. Arbeta nära med projektledaren och innehållsarkitekterna tidigt.
>
>En&quot;Internationalization Project Manager&quot; kan krävas som en separat person vars ansvar är att definiera vilket innehåll som ska översättas och vad som inte ska översättas och vilket översatt innehåll som ska kunna ändras av regionala eller lokala innehållsproducenter.

Skapa en plan för vilken innehållslokalisering du behöver.

* Behöver ni bara olika språk eller språk för att anpassa er till regionala särdrag?
* Behöver multimediematerial som bilder och videor vara olika för olika språkområden?

## Så här lagrar AEM Headless-innehåll {#headless-content-in-aem}

För lokaliseringsspecialisten är det inte viktigt att förstå hur AEM hanterar headless-innehåll. Att bekanta sig med grundläggande begrepp och terminologi är dock mycket användbart eftersom du senare använder AEM lokaliseringsverktyg. Det viktigaste är att ni förstår ert eget innehåll och hur det är strukturerat för att effektivt lokalisera det.

### Innehållsmodeller {#content-models}

För att headless-innehåll ska kunna levereras på ett enhetligt sätt i alla kanaler, regioner och på alla språk måste innehållet vara välstrukturerat. AEM använder innehållsmodeller för att tillämpa den här strukturen. Tänk på Innehållsmodeller som en typ av mall eller mönster för att skapa headless-innehåll. Eftersom alla projekt har sina egna behov definierar alla projekt sina egna modeller för innehållsfragment. AEM har inga fasta krav eller strukturer för sådana modeller.

Innehållsarkitekten arbetar tidigt i projektet för att definiera den här strukturen. Som tidigare rekommenderats bör du som lokaliseringsspecialist ha ett nära samarbete med innehållsarkitekten för att förstå och organisera innehållet.

Eftersom innehållsmodellerna definierar innehållsstrukturen måste du veta vilka fält i modellerna som behöver översättas. I allmänhet arbetar du med innehållsarkitekten för att definiera detta. Följ stegen nedan för att bläddra bland fälten i dina innehållsmodeller.

1. Navigera till **Verktyg** -> **Resurser** -> **Modeller för innehållsfragment**.
1. Modeller för innehållsfragment lagras vanligtvis i en mappstruktur. Tryck eller klicka på mappen för ditt projekt.
1. Modellerna listas. Tryck eller klicka på modellen för att visa informationen.
   ![Modeller för innehållsfragment](assets/content-fragment-models.png)
1. **Modellredigeraren för innehållsfragment** öppnas.
   1. Den vänstra kolumnen innehåller modellens fält. Den här kolumnen intresserar oss.
   1. Den högra kolumnen innehåller de fält som kan läggas till i modellen. Den här kolumnen kan vi ignorera.
      ![Modellredigerare för innehållsfragment](assets/content-fragment-model-editor.png)
1. Tryck eller klicka på ett av modellens fält. AEM markerar det och detaljerna för det fältet visas i den högra kolumnen.
   ![Information om Modellredigerare för innehållsfragment](assets/content-fragment-model-editor-detail.png)

Observera fältet **Egenskapsnamn** för alla fält som måste översättas. Du behöver den här informationen för nästa steg i resan.

### Innehållsfragment {#content-fragments}

Innehållsmodellerna används av innehållsförfattarna för att skapa det faktiska rubrikfria innehållet. Innehållsförfattare väljer vilken modell de vill basera sitt innehåll på och skapar sedan innehållsfragment. Innehållsfragment är förekomster av modellerna och representerar faktiskt innehåll som ska levereras utan krångel.

Om Innehållsmodellerna är mönstren för innehållet, är innehållsfragmenten det faktiska innehållet baserat på dessa mönster.

Innehållsfragment hanteras som resurser i AEM som en del av DAM (Digital Asset Management). Detta är viktigt eftersom alla kommer att finnas under sökvägen `/content/dam`.

## Rekommenderad innehållsstruktur {#recommended-structure}

Som vi tidigare har rekommenderat arbetar du med din innehållsarkitekt för att fastställa lämplig innehållsstruktur för ditt eget projekt. Följande är dock en beprövad, enkel och intuitiv struktur som är mycket effektiv.

Definiera en basmapp för projektet under `/content/dam`.

```text
/content/dam/<your-project>
```

Språket som ditt innehåll skrivs på kallas för språkrot. I vårt exempel är det engelska och det bör vara under den här vägen.

```text
/content/dam/<your-project>/en
```

Allt projektinnehåll som kan behöva lokaliseras ska placeras under det överordnad språket.

```text
/content/dam/<your-project>/en/<your-project-content>
```

Lokaliseringar ska skapas som jämställda mappar bredvid språkroten. Tyska skulle till exempel ha följande sökväg.

```text
/content/dam/<your-project>/de
```

Den slutliga strukturen kan se ut ungefär så här.

```text
/content
    |- dam
        |- your-project
            |- en
                |- some
                |- exciting
                |- headless
                |- content
            |- de
            |- fr
            |- it
            |- ...
        |- another-project
        |- ...
```

## AEM {#localization-tools}

Nu när du förstår vad innehållsfragment är och hur viktig innehållsstrukturen är kan vi titta på hur vi lokaliserar innehållet. Lokaliseringsverktygen i AEM är mycket kraftfulla, men enkla att förstå på en hög nivå.

* **Translation Connector**  - Kopplingen är länken mellan AEM och den översättningstjänst som du använder.
* **Översättningsregler**  - Regler definierar vilket innehåll under särskilda sökvägar som ska översättas.
* **Översättningsprojekt**  - Översättningsprojekt samlar ihop innehåll som ska hanteras som en enda översättningsåtgärd och spårar översättningens förlopp, interagerar med kopplingen för att överföra innehållet som ska översättas och få tillbaka det från översättningstjänsten.

Vanligtvis behöver du bara konfigurera anslutningen en gång för din instans och regler per headless-projekt. Sedan använder ni översättningsprojekt för att lokalisera innehållet och hålla översättningarna uppdaterade kontinuerligt.

## What&#39;s Next {#what-is-next}

Nu när du är klar med den här delen av den headless lokaliseringsresan bör du:

* Förstå hur viktig innehållsstrukturen är för lokaliseringen.
* Förstå hur AEM lagrar headless-innehåll.
* Bekanta dig med AEM lokaliseringsverktyg.

Bygg vidare på den här kunskapen och fortsätt din AEM headless-lokaliseringsresa genom att nästa gång du granskar dokumentet [Konfigurera översättningskopplingen](configure-connector.md) där du får lära dig hur du ansluter AEM till en översättningstjänst.|

## Ytterligare resurser {#additional-resources}

Vi rekommenderar att du går vidare till nästa del av den headless-baserade lokaliseringsresan genom att granska dokumentet [Konfigurera översättningskopplingen](configure-connector.md), men följande är ytterligare, valfria resurser som gör en djupdykning i vissa koncept som nämns i det här dokumentet, men de behöver inte fortsätta på den headless-resan.

* [AEM grundläggande hantering](/help/sites-cloud/authoring/getting-started/basic-handling.md)  - Lär dig grunderna i AEM gränssnitt för att enkelt navigera och utföra viktiga uppgifter som att hitta ditt innehåll.
* [Identifiera innehåll som ska översättas](/help/sites-cloud/administering/translation/rules.md)  - Lär dig hur översättningsregler identifierar innehåll som behöver översättas.
* [Configuring the Translation Integration Framework](/help/sites-cloud/administering/translation/integration-framework.md)  - Lär dig hur du konfigurerar översättningsintegreringsramverket för integrering med översättningstjänster från tredje part.
* [Hantera översättningsprojekt](/help/sites-cloud/administering/translation/managing-projects.md)  - Lär dig hur du skapar och hanterar både maskinöversättning och mänskliga översättningsprojekt i AEM.
