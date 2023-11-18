---
title: Arbeta med riktat innehåll på flera webbplatser
description: Om ni behöver hantera riktat innehåll, t.ex. aktiviteter, upplevelser och erbjudanden mellan era webbplatser, kan ni utnyttja AEM inbyggda stöd för flera webbplatser för riktat innehåll
exl-id: 03d2d640-8de8-4c4c-8a1d-756bb2dc8457
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '2844'
ht-degree: 4%

---

# Arbeta med riktat innehåll på flera webbplatser {#working-with-targeted-content-in-multisites}

Om ni behöver hantera riktat innehåll, till exempel aktiviteter, upplevelser och erbjudanden mellan era webbplatser, kan ni dra nytta av AEM inbyggda stöd för flera webbplatser för riktat innehåll.

>[!NOTE]
>
>Att arbeta med stöd för flera webbplatser för riktat innehåll är en avancerad funktion. Om du vill använda den här funktionen bör du känna till [Multi Site Manager](/help/sites-cloud/administering/msm/overview.md) och [Integrering med Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md) med AEM.

I det här dokumentet beskrivs följande:

* En kort översikt över AEM stöd för flera webbplatser för riktat innehåll.
* Beskriver några möjliga användningsscenarier för hur du kan länka webbplatser (i ett varumärke).
* Här finns ett exempel på genomgång av hur marknadsförare använder den här funktionen.
* Detaljerade anvisningar om hur man implementerar stöd för flera webbplatser för riktat innehåll.

Om du vill ange hur dina webbplatser ska dela personaliserat innehåll måste du utföra följande steg:

1. [Skapa ett nytt område](#creating-new-areas) eller [skapa ett område som en live-kopia](#creating-new-areas). Ett område innehåller alla aktiviteter som är tillgängliga för en *area* på sidan, d.v.s. den plats på sidan där komponenten är avsedd. När du skapar ett nytt område skapas ett tomt område, medan du kan ärva innehåll över webbplatsstrukturer genom att skapa ett område som en live-kopia.

1. [Länka webbplatsen eller sidan](#linking-sites-to-an-area) till ett område.

Du kan när som helst göra uppehåll i eller återställa arv. Om du inte vill göra uppehåll i arv kan du dessutom skapa lokala upplevelser. Som standard används mallområdet för alla sidor, såvida du inte anger något annat.

## Introduktion till stöd för flera webbplatser för riktat innehåll {#introduction-to-multisite-support-for-targeted-content}

Stöd för flera webbplatser för riktat innehåll finns tillgängligt direkt och du kan överföra riktat innehåll från huvudsidan som du hanterar via MSM till en lokal live-kopia eller hantera globala och lokala ändringar av sådant innehåll.

Du hanterar det här i en **Område**. Områden avgränsar riktat innehåll (aktiviteter, upplevelser och erbjudanden) som används på olika webbplatser och tillhandahåller en MSM-baserad mekanism för att skapa och hantera arvet av riktat innehåll tillsammans med webbplatsarv. Detta förhindrar att du behöver återskapa riktat innehåll på ärvda webbplatser.

I ett område överförs endast aktiviteter som är kopplade till det området till aktiva kopior. Som standard är mallområdet markerat. När du har skapat ytterligare områden kan du länka dessa till dina webbplatser eller sidor för att ange vilket målinnehåll som skickas.

En webbplats eller en live-kopia länkar till ett område som innehåller de aktiviteter som behöver vara tillgängliga på den webbplatsen eller live-kopian. Som standard länkar webbplatsen eller den aktiva kopian till mallområdet, men du kan länka andra områden förutom mallområdena bra.

>[!NOTE]
>
>Du bör vara medveten om följande när du använder stöd för flera webbplatser för riktat innehåll:
>
>* När du använder utrullningar eller live-kopior krävs en MSM-licens.
>* När du synkroniserar med Adobe Target krävs en Adobe Target-licens.
>

## Användningsexempel {#use-cases}

Du kan konfigurera stöd för flera webbplatser för riktat innehåll på flera olika sätt, beroende på hur det används. I det här avsnittet beskrivs hur detta teoretiskt skulle fungera med ett varumärke. Dessutom har [Exempel: Målinrikta innehåll baserat på geografi](#example-targeting-content-based-on-geography)kan ni se ett verkligt program för att målinrikta innehåll på flera webbplatser.

Målinriktat innehåll kapslas in i så kallade områden, som definierar omfånget för webbplatser eller sidor. Dessa områden definieras på varumärkesnivå. Ett varumärke kan innehålla flera områden. Områden kan vara åtskilda mellan varumärken. Även om ett varumärke bara innehåller huvudområdet och därför delas av alla varumärken, kan ett annat varumärke innehålla flera varumärken (till exempel per region). Varumärken behöver därför inte spegla de olika områdena mellan dem.

Med stöd för flera webbplatser för riktat innehåll kan du till exempel ha två (eller fler) webbplatser med **en** varumärke som har något av följande:

* Ett helt *distinkt* uppsättning med målinnehåll - redigering av målinnehåll i det ena påverkar inte det andra. Webbplatser som länkar till olika områden läser och skriver till sina egna konfigurerade områden. Till exempel:
   * Plats A-länkar till område X
   * Plats B-länkar till område Y
* A *delad* uppsättning med riktat innehåll - Redigering i en påverkar båda platserna direkt. Du kan konfigurera detta genom att låta två webbplatser referera till samma område. Webbplatser som länkar till samma område delar målinnehållet i det här området. Till exempel:
   * Plats A-länkar till område X
   * Plats B-länkar till område X
* En distinkt uppsättning målinriktat innehåll *ärvd* från en annan webbplats via MSM - Innehållet kan enkelt publiceras från masterversion till livekopia. Till exempel:
   * Plats A-länkar till område X
   * Site B-länkar till Area Y (som är en live-kopia av Area X)

Du skulle också kunna ha **flera** varumärken som används på en plats, vilket kan vara mer komplext än det här exemplet.

![Exempel på multisite](/help/sites-cloud/authoring/assets/multisite-example.png)

>[!NOTE]
>
>Mer teknisk information om den här funktionen finns i [Hur hantering av flera webbplatser för riktat innehåll är strukturerad](/help/sites-cloud/authoring/personalization/multisite-structure.md).

## Exempel: Målinrikta innehåll baserat på geografi {#example-targeting-content-based-on-geography}

Genom att använda flera webbplatser för riktat innehåll kan ni dela, rulla ut eller isolera personaliserat innehåll. För att bättre illustrera hur den här funktionen används bör du överväga ett scenario där du vill styra hur riktat innehåll introduceras baserat på geografi, som i följande scenario:

Det finns fyra versioner av samma webbplats baserat på geografisk placering:

* The **Amerikas förenta stater** -platsen finns i det övre vänstra hörnet och är huvudwebbplatsen. I det här exemplet är det öppet i målläge.
* De tre andra versionerna av den här webbplatsen är **Kanada**, **Storbritannien** och **Australien**, som alla är live-kopior. De här platserna är öppna i förhandsgranskningsläge.

![Multisiteversioner](/help/sites-cloud/authoring/assets/multisite-versions.png)

Varje webbplats delar personligt innehåll i geografiska regioner:

* Kanada delar huvudområdet med USA.
* Storbritannien är kopplat till det europeiska området och ärver från huvudområdet.
* Australien har sitt eget personaliserade innehåll eftersom det ligger på södra halvklotet och eftersom säsongsprodukter inte skulle gälla.

![Multisitediagram](/help/sites-cloud/authoring/assets/multisite-diagram.png)

På det norra halvklotet har vi skapat en vinteraktivitet, men i den manliga publiken vill marknadsföraren i Nordamerika ha en annan bild för vintern, så han eller hon ändrar den på USA:s webbplats.

![Amerikas förenta stater](/help/sites-cloud/authoring/assets/multisite-us.png)

När du har uppdaterat fliken ändras den kanadensiska webbplatsen till den nya bilden utan att vi behöver göra något. Det gör det eftersom det delar huvudområdet med USA. I Storbritannien och Australien ändras inte bilden.

![Ändra versioner](/help/sites-cloud/authoring/assets/multisite-us-change.png)

Marknadsföraren vill sprida dessa ändringar till den europeiska regionen och [lanserar live-kopian](/help/sites-cloud/administering/msm/creating-live-copies.md) genom att trycka eller klicka **Utrullningssida**. När du har uppdaterat fliken får den nya bilden på den brittiska webbplatsen när det europeiska området ärver från huvudområdet (efter utrullning).

![Rolling live copy](/help/sites-cloud/authoring/assets/multisite-roll-out.png)

Bilden på Australiens webbplats ändras inte, vilket är det önskade beteendet, eftersom det är sommar i Australien och marknadsföraren inte vill ändra det innehållet. Australiens webbplats ändras inte eftersom den inte delar ett område med någon annan region och inte heller är den en live-kopia av en annan region. Marknadsföraren behöver aldrig oroa sig för att den australiska webbplatsens riktade innehåll skrivs över.

För Storbritannien, vars område är en live-kopia av huvudområdet, kan du dessutom se arvsstatusen med den gröna indikatorn bredvid aktivitetsnamnet. Om en aktivitet ärvs kan du inte ändra den om du inte gör uppehåll i eller frigör den.

Du kan när som helst göra uppehåll i arvet eller helt koppla loss arvet. Du kan också alltid lägga till lokala upplevelser som bara är tillgängliga för den upplevelsen utan att avbryta arvet.

>[!NOTE]
>
>Mer teknisk information om den här funktionen finns i [Hur hantering av flera webbplatser för riktat innehåll är strukturerad](/help/sites-cloud/authoring/personalization/multisite-structure.md).

### Skapa ett nytt område jämfört med att skapa ett nytt område som livecopy {#creating-a-new-area-versus-creating-a-new-area-as-livecopy}

I AEM kan du skapa ett nytt område eller skapa nya områden som livecopy. När du skapar ett nytt område grupperas aktiviteter och allt som hör till dessa aktiviteter, som erbjudanden, upplevelser och så vidare. Du skapar ett område när du antingen vill skapa en helt distinkt uppsättning målinnehåll eller vill dela en uppsättning målinnehåll.

Om du har skapat arv via MSM mellan de två platserna kanske du vill ärva aktiviteterna. I det här fallet skapar du ett område som en live-kopia, där Y är en live-kopia av X och därför även ärver alla aktiviteter.

>[!NOTE]
>
>Standardutrullningen aktiverar efterföljande rullningar av målinnehållet när en sida är en Live-kopia som länkar till ett område som själv är en Live-kopia av området som är länkat till sidans plan.

I följande diagram finns fyra platser där två delar huvudområdet (och alla aktiviteter som ingår i det området), en plats som har ett område som är en live-kopia av ett område, så att den delar med sig av aktiviteterna vid utrullning, och en sida som är helt separat (och därför kräver ett område för sina aktiviteter).

![Diagramdetalj](/help/sites-cloud/authoring/assets/multisite-diagram-detail.png)

För att uppnå detta i AEM gör du följande:

* Plats A länkar till mallområdet - inget område behöver skapas. Mallområde är markerat som standard i AEM. Delningsaktiviteter för webbplats A och B osv.
* Plats B länkar till mallområdet - inget område behöver skapas. Mallområde är markerat som standard i AEM. Delningsaktiviteter för webbplats A och B osv.
* Site C-länkar till Inherited Area, som är en live-kopia av mallområdet - Skapa område som Live-kopia där du skapar en live-kopia baserad på mallområdet. Det ärvda området ärver aktiviteter från huvudområdet vid utrullning.
* Plats D länkar till sitt eget isolerade område - Skapa område där du skapar ett helt nytt område utan aktiviteter ännu. Det isolerade området kommer inte att dela aktiviteter med någon annan plats.

## Skapa nya områden {#creating-new-areas}

Områden kan omfatta aktiviteter och erbjudanden. När du har skapat ett område i någon av dem (till exempel aktiviteter), har du även det tillgängliga området i den andra (till exempel erbjudanden).

>[!NOTE]
>
>Standardområdet som kallas mallområde komprimeras som standard när du väljer namnet på ett varumärke **tills** du skapar ett annat område. När du sedan väljer ett varumärke på konsolen **Aktivitet** eller **Erbjudanden** visas konsolen **Område**.

Så här skapar du ett område:

1. Navigera till **Personalisering** > **Aktiviteter** eller **Erbjudanden** och sedan till ert varumärke.
1. Välj **Skapa område**.

   ![Skapa område](/help/sites-cloud/authoring/assets/multisite-create-area.png)

1. Klicka på **Område** ikon och klicka **Nästa**.
1. I **Titel** anger du ett namn för det nya området. Du kan också välja taggar.
1. Välj **Skapa**.

   AEM omdirigeras till varumärkesfönstret, där alla områden som skapas listas. Om det finns ett annat område förutom mallområdet kan du skapa områden direkt i varumärkeskonsolen.

   ![Skapa](/help/sites-cloud/authoring/assets/multisite-create.png)

## Skapa områden som live-kopior {#creating-areas-as-live-copies}

Du skapar ett område som en live-kopia för att ärva målinnehållet i olika webbplatsstrukturer.

Så här skapar du ett område som en livecopy:

1. Navigera till **Personalisering** > **Aktiviteter** eller **Erbjudanden** och sedan till ert varumärke.
1. Välj **Skapa område som Live Copy**.

   ![Skapa område som live-kopia](/help/sites-cloud/authoring/assets/multisite-area-as-livecopy.png)

1. Markera området som du vill göra en live-kopia av och klicka på **Nästa**.

   ![Skapa live copy](/help/sites-cloud/authoring/assets/multisite-livecopy.png)

1. I fältet **Namn** anger du ett namn för live-kopian. Som standard inkluderas undersidor. Exkludera dem genom att markera kryssrutan **Uteslut undersidor**.

   ![Skapa live copy](/help/sites-cloud/authoring/assets/multisite-create-livecopy.png)

1. I **Utrullningskonfigurationer** väljer du lämplig konfiguration.

   Se [Installerade utrullningskonfigurationer](/help/sites-cloud/administering/msm/live-copy-sync-config.md#installed-and-custom-rollout-configurations) för beskrivningar av varje alternativ.

   Se [Skapa och synkronisera Live-kopior](/help/sites-cloud/administering/msm/creating-live-copies.md) för mer information om live-kopior.

   >[!NOTE]
   >
   >När en sida förs ut till en Live-kopia och området som är konfigurerat för sidan Blå utskrift också är skissen för området som är konfigurerat för sidans Live-kopia, är LiveAction **personalizationContentRollout** utlöser en synkron subRollout, som är en del av **Standardkonfiguration för utrullning**.

1. Välj **Skapa**.

   AEM omdirigeras till varumärkesfönstret, där alla områden som skapas listas. Om det finns ett annat område förutom mallområdet kan du skapa områden direkt från varumärkesfönstret.

   ![Skapa område](/help/sites-cloud/authoring/assets/multisite-create-2.png)

## Länka webbplatser till ett område {#linking-sites-to-an-area}

Du kan länka områden till antingen sidor eller till en plats. Områden ärvs av alla undersidor såvida inte dessa sidor överlappas av en mappning på en undersida. I allmänhet länkar du dock på webbplatsnivå.

När du länkar är bara de aktiviteter, upplevelser och erbjudanden från det valda området tillgängliga. Detta förhindrar oavsiktlig blandning av oberoende hanterat innehåll. Om inget annat område är konfigurerat används huvudområdet för varje varumärke.

>[!NOTE]
>
>Sidor eller platser som refererar till samma område använder *samma* gemensamma aktiviteter, upplevelser och erbjudanden. Om du redigerar en aktivitet, en upplevelse eller ett erbjudande som delas av flera webbplatser påverkas alla webbplatser.

Så här länkar du en plats till ett område:

1. Navigera till den webbplats (eller sida) som du vill länka till ett område.
1. Markera webbplatsen eller sidan och välj **Visa egenskaper**.
1. Välj **Personalisering** -fliken.
1. I **Varumärke** väljer du det varumärke som du vill länka området till. När du har valt varumärket finns tillgängliga områden på **Områdesreferens** -menyn.

   ![Länka platser](/help/sites-cloud/authoring/assets/multisite-english.png)

1. Markera området på menyn **Områdesreferens** nedrullningsbar meny och välj **Spara**.

   ![Områdesreferens](/help/sites-cloud/authoring/assets/multisite-area-reference.png)

## Koppla loss live-kopia eller avbryta arv av riktat innehåll {#detaching-live-copy-or-suspending-inheritance-of-targeted-content}

Du kan antingen göra uppehåll i eller koppla från arv av riktat innehåll. Du gör uppehåll i eller frigör live-kopian per aktivitet. Du kanske vill ändra upplevelserna i din aktivitet, men om aktiviteten fortfarande är länkad till en ärvd kopia kan du inte ändra upplevelsen eller någon av aktivitetens egenskaper.

Om du gör uppehåll i den aktiva kopian avbryts arvet tillfälligt, men i framtiden kan du återställa arv. Arv bryts permanent när du kopplar loss den aktiva kopian.

Du gör uppehåll i eller frigör arvet av målinnehåll genom att återställa det i en aktivitet. Om en sida eller webbplats länkar till ett område som är en Live-kopia, kan du visa en aktivitets arvsstatus.

En aktivitet som ärver från en annan plats markeras som grön bredvid aktivitetsnamnet. Ett uppehåll i arv har markerats som rött och en lokalt skapad aktivitet har ingen ikon.

>[!NOTE]
>
>* Du kan bara göra uppehåll i eller koppla loss live-kopior i en aktivitet.
>* Du behöver inte göra uppehåll i eller koppla loss live-kopior för att utöka en ärvd aktivitet. Du kan alltid skapa **new** lokala upplevelser och erbjudanden för den aktiviteten. Om du vill ändra en befintlig aktivitet måste du göra uppehåll i arv.
>

### Avbryter arv {#suspending-inheritance}

Så här gör du uppehåll i eller frånkoppling av arv av riktat innehåll i en aktivitet:

1. Navigera till sidan där du vill koppla loss eller göra uppehåll i arv och markera **Målinriktning** i listrutan Läge.
1. Om sidan är länkad till ett område som är en live-kopia ser du arvsstatusen. Välj **Börja målinrikta**.
1. Gör något av följande om du vill göra uppehåll i en aktivitet:

   1. Välj ett element i aktiviteten, t.ex. målgruppen. AEM visar automatiskt en bekräftelseruta för att pausa Live Copy. (Du kan göra uppehåll i live-kopieringen genom att trycka eller klicka på ett element under målprocessen.)
   1. Välj **Skjut upp Live Copy** i listrutan i verktygsfältet.

   ![Skjut upp live-kopia](/help/sites-cloud/authoring/assets/multisite-suspend-livecopy.png)

1. Välj **Gör uppehåll** för att pausa aktiviteten. Avbrutna aktiviteter markeras med rött.

   ![Pausad live-kopia](/help/sites-cloud/authoring/assets/multisite-suspended.png)

### Brytande arv {#breaking-inheritance}

Så här bryter du arv av riktat innehåll i en aktivitet:

1. Navigera till sidan där du vill koppla loss den aktiva kopian från mallen och markera **Målinriktning** i listrutan Läge.
1. Om sidan är länkad till ett område som är en live-kopia ser du arvsstatusen. Välj **Börja målinrikta**.
1. Välj **Koppla loss live-kopia** i listrutan i verktygsfältet. AEM bekräftar att du vill koppla loss live-kopian.
1. Välj **Koppla loss** för att frigöra den aktiva kopian från aktiviteten. När den har kopplats loss visas inte längre listrutan för arv. Aktiviteten är nu en lokal aktivitet.

   ![Lokal aktivitet](/help/sites-cloud/authoring/assets/multisite-winter.png)

## Återställa arv av riktat innehåll {#restoring-inheritance-of-targeted-content}

Om du har inaktiverat arv av riktat innehåll i en aktivitet kan du återställa det när som helst. Om du har kopplat loss den aktiva kopian kan du inte återställa arvet.

Så här återställer du arv av riktat innehåll i en aktivitet:

1. Navigera till sidan där du vill återställa arv och markera **Målinriktning** i listrutan Läge.
1. Välj **Börja målinrikta**.
1. Välj **Återuppta live-kopia** i listrutan i verktygsfältet.

   ![Återupptar live-kopia](/help/sites-cloud/authoring/assets/multisite-resume.png)

1. Välj **Återuppta** för att bekräfta att du vill återuppta arv av live-kopior. Alla ändringar som gjorts i den aktuella aktiviteten går förlorade om du återupptar arvet.

## Ta bort områden {#deleting-areas}

När du tar bort ett område tar du bort alla aktiviteter i det området. AEM varnar dig innan du kan ta bort ett område. Om du tar bort ett område som en webbplats är kopplad till, kommer mappningen för det här varumärket automatiskt att ändras till huvudområdet.

Så här tar du bort ett område:

1. Navigera till **Personalisering** > **Verksamhet** eller **Erbjudanden** och därefter ert varumärke.
1. Markera ikonen bredvid det område du vill ta bort.
1. Välj **Ta bort** och bekräfta att du vill ta bort området.
