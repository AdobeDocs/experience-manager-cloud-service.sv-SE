---
title: Arbeta med riktat innehåll på flera webbplatser
description: Om ni behöver hantera riktat innehåll, t.ex. aktiviteter, upplevelser och erbjudanden mellan era webbplatser, kan ni utnyttja AEM inbyggda stöd för flera webbplatser för riktat innehåll
translation-type: tm+mt
source-git-commit: 16725342c1a14231025bbc1bafb4c97f0d7cfce8
workflow-type: tm+mt
source-wordcount: '2900'
ht-degree: 5%

---


# Arbeta med riktat innehåll på flera webbplatser {#working-with-targeted-content-in-multisites}

Om ni behöver hantera riktat innehåll, till exempel aktiviteter, upplevelser och erbjudanden mellan era webbplatser, kan ni utnyttja AEM inbyggda stöd för flera webbplatser för riktat innehåll.

>[!NOTE]
>
>Att arbeta med stöd för flera webbplatser för riktat innehåll är en avancerad funktion. Om du vill använda den här funktionen bör du känna till Multi Site Manager och Adobe Target-integreringen med AEM.
<!--
>Working with Multisite support for targeted content is an advanced feature. To use this feature, you should be familiar with [Multi Site Manager](/help/sites-administering/msm.md) and the [Adobe Target integration](/help/sites-administering/target.md) with AEM.
-->

I det här dokumentet beskrivs följande:

* En kort översikt över AEM stöd för flera webbplatser för riktat innehåll.
* Beskriver några möjliga användningsscenarier för hur du kan länka webbplatser (i ett varumärke).
* Här finns ett exempel på genomgång av hur marknadsförare använder den här funktionen.
* Detaljerade anvisningar om hur man implementerar stöd för flera webbplatser för riktat innehåll.

Om du vill ange hur dina webbplatser ska dela personaliserat innehåll måste du utföra följande steg:

1. [Skapa ett nytt område](#creating-new-areas) eller [skapa ett nytt område som live-kopia](#creating-new-areas). Ett område omfattar alla aktiviteter som är tillgängliga för ett *område* på sidan. d.v.s. den plats på sidan där komponenten är avsedd. När du skapar ett nytt område skapas ett tomt område, medan du kan ärva innehåll i olika webbplatsstrukturer genom att skapa ett nytt område som en dynamisk kopia.

1. [Länka webbplatsen eller sidan](#linking-sites-to-an-area) till ett område.

Du kan när som helst göra uppehåll i eller återställa arv. Om du inte vill göra uppehåll i arv kan du dessutom skapa lokala upplevelser. Som standard används det Överordnad området på alla sidor, såvida du inte anger något annat.

## Introduktion till stöd för flera webbplatser för riktat innehåll {#introduction-to-multisite-support-for-targeted-content}

Stöd för flera webbplatser för riktat innehåll är tillgängligt direkt och gör att du kan överföra riktat innehåll från den överordnad sidan som du hanterar via MSM till en lokal live-kopia eller hantera globala och lokala ändringar av sådant innehåll.

Du hanterar det här i ett **område**. Områden avgränsar riktat innehåll (aktiviteter, upplevelser och erbjudanden) som används på olika webbplatser och tillhandahåller en MSM-baserad mekanism för att skapa och hantera arvet av riktat innehåll tillsammans med webbplatsarv. Detta förhindrar att du behöver återskapa riktat innehåll på ärvda webbplatser, vilket krävdes i AEM före 6.2.

I ett område överförs endast aktiviteter som är kopplade till det området till aktiva kopior. Som standard är det Överordnad området markerat. När du har skapat ytterligare områden kan du länka dessa till dina webbplatser eller sidor för att ange vilket målinnehåll som skickas.

En webbplats eller en live-kopia länkar till ett område som innehåller de aktiviteter som behöver vara tillgängliga på den webbplatsen eller live-kopian. Som standard länkar webbplatsen eller den aktiva kopian till det överordnad området, men du kan länka andra områden förutom de överordnad områdena bra.

>[!NOTE]
>
>Du bör vara medveten om följande när du använder stöd för flera webbplatser för riktat innehåll:
>
>* När du använder utrullningar eller live-kopior krävs en MSM-licens.
>* När du synkroniserar med Adobe Target krävs en Adobe Target-licens.

>



## Användningsexempel {#use-cases}

Du kan konfigurera stöd för flera webbplatser för riktat innehåll på flera olika sätt, beroende på hur det används. I det här avsnittet beskrivs hur detta teoretiskt skulle fungera med ett varumärke. Dessutom, i [exemplet: Med innehåll baserat på geografisk](#example-targeting-content-based-on-geography)inriktning kan ni se en verklighetstrogen applikation som inriktar sig på innehåll på flera webbplatser.

Målinriktat innehåll kapslas in i så kallade områden, som definierar omfånget för webbplatser eller sidor. Dessa områden definieras på varumärkesnivå. Ett varumärke kan innehålla flera områden. Områden kan vara åtskilda mellan varumärken. Ett varumärke kan innehålla det överordnad området och delas därför över alla varumärken, men ett annat varumärke kan innehålla flera varumärken (till exempel per region). Varumärken behöver därför inte spegla de olika områdena mellan dem.

Med stöd för flera webbplatser för riktat innehåll kan du till exempel ha två (eller fler) webbplatser med **ett** varumärke som har något av följande:

* En helt *distinkt* uppsättning målinnehåll - redigering av målinnehåll i det ena påverkar inte det andra. Webbplatser som länkar till olika områden läser och skriver till sina egna konfigurerade områden. Till exempel:
   * Plats A-länkar till område X
   * Plats B-länkar till område Y
* En *gemensam* uppsättning målinriktat innehåll - redigering i ett har en direkt effekt på båda webbplatserna. Du kan konfigurera detta genom att låta två platser referera till samma område. Webbplatser som länkar till samma område delar målinnehållet i det här området. Till exempel:
   * Plats A-länkar till område X
   * Plats B-länkar till område X
* En distinkt uppsättning målinriktat innehåll som *ärvs* från en annan webbplats via MSM - innehållet kan introduceras individuellt från överordnad till live-text. Till exempel:
   * Plats A-länkar till område X
   * Site B-länkar till Area Y (som är en live-kopia av Area X)

Du kan också ha **flera** varumärken som används på en plats, vilket kan vara mer komplext än i det här exemplet.

![Exempel på multisite](/help/sites-cloud/authoring/assets/multisite-example.png)

>[!NOTE]
>
>Mer teknisk information om den här funktionen finns i [How Multisite Management for Targeted Content is Structured](/help/sites-cloud/authoring/personalization/multisite-structure.md).

## Exempel: Rikta innehåll baserat på geografi {#example-targeting-content-based-on-geography}

Genom att använda flera webbplatser för riktat innehåll kan ni dela, rulla ut eller isolera personaliserat innehåll. För att bättre illustrera hur den här funktionen används bör du överväga ett scenario där du vill styra hur riktat innehåll introduceras baserat på geografi, som i följande scenario:

Det finns fyra versioner av samma webbplats baserat på geografisk placering:

* Den **amerikanska** webbplatsen ligger i det övre vänstra hörnet och är den överordnad webbplatsen. I det här exemplet är det öppet i målläge.
* De tre andra versionerna av denna webbplats är **Kanada**, **Storbritannien** och **Australien**, som alla är live-kopior. Dessa webbplatser är öppna i förhandsgranskningsläge.

![Flera versioner](/help/sites-cloud/authoring/assets/multisite-versions.png)

Varje webbplats delar personligt innehåll i geografiska regioner:

* Kanada delar det överordnad området med USA.
* Storbritannien är kopplat till det europeiska området och ärver från det överordnad området.
* Australien har sitt eget personaliserade innehåll eftersom det ligger på södra halvklotet och eftersom säsongsprodukter inte skulle gälla.

![Multisitediagram](/help/sites-cloud/authoring/assets/multisite-diagram.png)

På det norra halvklotet har vi skapat en vinteraktivitet, men i den manliga publiken vill marknadsföraren i Nordamerika ha en annan bild för vintern, så han eller hon ändrar den på USA:s webbplats.

![Amerikas förenta stater](/help/sites-cloud/authoring/assets/multisite-us.png)

När du har uppdaterat fliken ändras den kanadensiska webbplatsen till den nya bilden utan att vi behöver göra något. Den gör det eftersom den delar det överordnad området med USA. I Storbritannien och Australien ändras inte bilden.

![Ändra versioner](/help/sites-cloud/authoring/assets/multisite-us-change.png)

Marknadsföraren vill sprida dessa ändringar till den europeiska regionen och lansera den aktiva kopian genom att trycka eller klicka på **utrullningssidan**. När du har uppdaterat fliken får den nya bilden på den brittiska webbplatsen när det europeiska området ärver från det överordnad området (efter utrullning). <!--The marketer would like to roll out these changes to the European region and [rolls out the live copy](/help/sites-administering/msm-livecopy.md) by tapping or clicking **Rollout Page**. After refreshing the tab, the Great Britain site has the new image as the Europe area inherits from the master area (after rollout).-->

![Rolling live copy](/help/sites-cloud/authoring/assets/multisite-roll-out.png)

Bilden på Australiens webbplats ändras inte, vilket är det önskade beteendet, eftersom det är sommar i Australien och marknadsföraren inte vill ändra det innehållet. Australiens webbplats ändras inte eftersom den inte delar ett område med någon annan region och inte heller är den en live-kopia av en annan region. Marknadsföraren behöver aldrig oroa sig för att den australiska webbplatsens riktade innehåll skrivs över.

För Storbritannien, vars område är en live-kopia av det överordnad området, ser du dessutom arvsstatus med den gröna indikatorn bredvid aktivitetsnamnet. Om en aktivitet ärvs kan du inte ändra den om du inte gör uppehåll i eller frigör den.

Du kan när som helst göra uppehåll i arvet eller helt koppla loss arvet. Du kan också alltid lägga till lokala upplevelser som bara är tillgängliga för den upplevelsen utan att avbryta arvet.

>[!NOTE]
>
>Mer teknisk information om den här funktionen finns i [How Multisite Management for Targeted Content is Structured](/help/sites-cloud/authoring/personalization/multisite-structure.md).

### Skapa ett nytt område jämfört med att skapa ett nytt område som livecopy {#creating-a-new-area-versus-creating-a-new-area-as-livecopy}

I AEM kan du skapa ett nytt område eller skapa nya områden som livecopy. När du skapar ett nytt område grupperas aktiviteter och allt som hör till dessa aktiviteter, som erbjudanden, upplevelser och så vidare. Du skapar ett nytt område när du antingen vill skapa en helt distinkt uppsättning målinnehåll eller vill dela en uppsättning målinnehåll.

Om du har skapat arv via MSM mellan de två platserna kanske du vill ärva aktiviteterna. I det här fallet skapar du ett nytt område som en live-kopia, där Y är en live-kopia av X och därför även ärver alla aktiviteter.

>[!NOTE]
>
>Standardutrullningen aktiverar efterföljande rullningar av målinnehållet när en sida är en Live-kopia som länkar till ett område som själv är en Live-kopia av området som är länkat till sidans plan.

I följande diagram finns fyra platser där två delar det överordnad området (och alla aktiviteter som ingår i det området), en plats som har ett område som är en live-kopia av ett område, så att den delar på verksamheten vid utrullning, och en sida som är helt separat (och därför kräver ett område för sina aktiviteter).

![Diagramdetalj](/help/sites-cloud/authoring/assets/multisite-diagram-detail.png)

För att uppnå detta i AEM gör du följande:

* Plats A länkar till det Överordnad området - inget områdesskapande behövs. Överordnad område markeras som standard i AEM. Delningsaktiviteter för webbplats A och B osv.
* Plats B länkar till det Överordnad området - inget områdesskapande behövs. Överordnad område markeras som standard i AEM. Delningsaktiviteter för webbplats A och B osv.
* Site C-länkar till Inherited Area, som är en live-kopia av det Överordnad området - Skapa område som Live-kopia där du skapar en live-kopia baserad på det Överordnad området. Det ärvda området ärver aktiviteter från det Överordnad området vid utrullning.
* Plats D länkar till sitt eget isolerade område - Skapa område där du skapar ett helt nytt område utan aktiviteter ännu. Det isolerade området kommer inte att dela aktiviteter med någon annan plats.

## Skapa nya områden {#creating-new-areas}

Områden kan omfatta aktiviteter och erbjudanden. När du har skapat ett område i någon av dem (till exempel aktiviteter), har du även det tillgängliga området i den andra (till exempel erbjudanden).

>[!NOTE]
>
>Standardområdet som kallas masterområde komprimeras som standard när du trycker eller klickar på namnet på ett varumärke **tills** du skapar ett annat område. När du sedan väljer ett varumärke på konsolen **Aktivitet** eller **Erbjudanden** visas konsolen **Område**.

Så här skapar du ett nytt område:

1. Navigera till **Personalisering** > **Aktiviteter** eller **Erbjudanden** och sedan till ert varumärke.
1. Tryck eller klicka på **Skapa område**.

   ![Skapa område](/help/sites-cloud/authoring/assets/multisite-create-area.png)

1. Klicka på ikonen **Område** och klicka på **Nästa**.
1. I fältet **Titel** anger du ett namn för det nya området. Du kan också välja taggar.
1. Tryck eller klicka på **Skapa**.

   AEM omdirigeras till varumärkesfönstret, där alla områden som skapas listas. Om det finns ett annat område förutom det Överordnad området kan du skapa områden direkt i varumärkeskonsolen.

   ![Skapa](/help/sites-cloud/authoring/assets/multisite-create.png)

## Skapa områden som live-kopior {#creating-areas-as-live-copies}

Du skapar ett område som en live-kopia för att ärva målinnehållet i olika webbplatsstrukturer.

Så här skapar du ett område som en livecopy:

1. Navigera till **Personalisering** > **Aktiviteter** eller **Erbjudanden** och sedan till ert varumärke.
1. Tryck eller klicka på **Skapa område som Live-kopia**.

   ![Skapa område som live-kopia](/help/sites-cloud/authoring/assets/multisite-area-as-livecopy.png)

1. Markera området som du vill göra en live-kopia av och klicka på **Nästa**.

   ![Skapa live copy](/help/sites-cloud/authoring/assets/multisite-livecopy.png)

1. I fältet **Namn** anger du ett namn för live-kopian. Som standard inkluderas undersidor. Exkludera dem genom att markera kryssrutan **Uteslut undersidor**.

   ![Skapa live copy](/help/sites-cloud/authoring/assets/multisite-create-livecopy.png)

1. Välj lämplig konfiguration i listrutan **utrullningskonfigurationer** .

   Se Installerade utrullningskonfigurationer för beskrivningar av varje alternativ. <!--See [Installed Rollout Configurations](/help/sites-administering/msm-sync.md#installed-rollout-configurations) for descriptions of each option.-->

   Mer information om live-kopior finns i Skapa och synkronisera live-kopior. <!--See [Creating and Synchronizing Live Copies](/help/sites-administering/msm-livecopy.md) for more information on live copies.-->

   >[!NOTE]
   >
   >När en sida rullas ut till en Live Copy och området som är konfigurerat för sidan Blueprint också är utkast för området som är konfigurerat för sidans Live Copy, utlöser LiveAction **personalizationContentRollout** en synkron subRollout, som är en del av **standardkonfigurationen**.

1. Tryck eller klicka på **Skapa**.

   AEM omdirigeras till varumärkesfönstret, där alla områden som skapas listas. Om det finns ett annat område förutom det Överordnad området kan du skapa områden direkt från varumärkesfönstret.

   ![Skapa område](/help/sites-cloud/authoring/assets/multisite-create-2.png)

## Länka webbplatser till ett område {#linking-sites-to-an-area}

Du kan länka områden till antingen sidor eller till en plats. Områden ärvs av alla undersidor såvida inte dessa sidor överlappas av en mappning på en undersida. I allmänhet länkar du dock på webbplatsnivå.

När du länkar är bara de aktiviteter, upplevelser och erbjudanden från det valda området tillgängliga. Detta förhindrar oavsiktlig blandning av oberoende hanterat innehåll. Om inget annat område är konfigurerat används det överordnad området för varje varumärke.

>[!NOTE]
>
>Sidor eller webbplatser som refererar till samma område använder *samma* gemensamma uppsättning aktiviteter, upplevelser och erbjudanden. Om du redigerar en aktivitet, en upplevelse eller ett erbjudande som delas av flera webbplatser påverkas alla webbplatser.

Så här länkar du en plats till ett område:

1. Navigera till den webbplats (eller sida) som du vill länka till ett område.
1. Markera webbplatsen eller sidan och tryck eller klicka på **Visa egenskaper**.
1. Tryck eller klicka på fliken **Personalisering** .
1. På menyn **Varumärke** väljer du det varumärke som du vill länka området till. När du har valt varumärket är tillgängliga områden tillgängliga på menyn **Områdesreferens** .

   ![Länka platser](/help/sites-cloud/authoring/assets/multisite-english.png)

1. Markera området i listrutan **Områdesreferens** och tryck eller klicka på **Spara**.

   ![Områdesreferens](/help/sites-cloud/authoring/assets/multisite-area-reference.png)

## Koppla loss live-kopia eller avbryta arv av riktat innehåll {#detaching-live-copy-or-suspending-inheritance-of-targeted-content}

Du kan antingen göra uppehåll i eller koppla från arv av riktat innehåll. Du gör uppehåll i eller frigör live-kopian per aktivitet. Du kanske vill ändra upplevelserna i din aktivitet, men om aktiviteten fortfarande är länkad till en ärvd kopia kan du inte ändra upplevelsen eller någon av aktivitetens egenskaper.

Om du gör uppehåll i den aktiva kopian avbryts arvet tillfälligt, men i framtiden kan du återställa arv. Arv bryts permanent när du kopplar loss den aktiva kopian.

Du gör uppehåll i eller frigör arvet av målinnehåll genom att återställa det i en aktivitet. Om en sida eller webbplats länkar till ett område som är en Live-kopia, kan du visa en aktivitets arvsstatus.

En aktivitet som ärver från en annan plats markeras som grön bredvid aktivitetsnamnet. Ett uppehåll i arv har markerats som rött och en lokalt skapad aktivitet har ingen ikon.

>[!NOTE]
>
>* Du kan bara göra uppehåll i eller koppla loss live-kopior i en aktivitet.
>* Du behöver inte göra uppehåll i eller koppla loss live-kopior för att utöka en ärvd aktivitet. Ni kan alltid skapa **nya** lokala upplevelser och erbjudanden för den aktiviteten. Om du vill ändra en befintlig aktivitet måste du göra uppehåll i arv.

>



### Avbryter arv {#suspending-inheritance}

Så här gör du uppehåll i eller frånkoppling av arv av riktat innehåll i en aktivitet:

1. Navigera till sidan där du vill koppla loss eller göra uppehåll i arv och tryck eller klicka på **Mål** i listrutan Läge.
1. Om sidan är länkad till ett område som är en live-kopia ser du arvsstatusen. Tryck eller klicka på **Start Targeting**.
1. Gör något av följande om du vill göra uppehåll i en aktivitet:

   1. Välj ett element i aktiviteten, till exempel målgruppen. AEM visar automatiskt en bekräftelseruta för att pausa Live Copy. (Du kan göra uppehåll i live-kopieringen genom att trycka eller klicka på ett element under målprocessen.)
   1. Select **Suspend Live Copy** from the drop-down menu in the toolbar.

   ![Skjut upp live-kopia](/help/sites-cloud/authoring/assets/multisite-suspend-livecopy.png)

1. Tryck eller klicka på **Gör uppehåll** för att pausa aktiviteten. Avbrutna aktiviteter markeras med rött.

   ![Pausad live-kopia](/help/sites-cloud/authoring/assets/multisite-suspended.png)

### Brytande arv {#breaking-inheritance}

Så här bryter du arv av riktat innehåll i en aktivitet:

1. Navigera till den sida där du vill koppla loss den aktiva kopian från överordnad och tryck eller klicka på **Riktning** i listrutan Läge.
1. Om sidan är länkad till ett område som är en live-kopia ser du arvsstatusen. Tryck eller klicka på **Start Targeting**.
1. Välj **Koppla loss live-kopia** i listrutan i verktygsfältet. AEM bekräftar att du vill koppla loss live-kopian.
1. Tryck eller klicka på **Koppla loss** för att koppla loss live-kopian från aktiviteten. När den har kopplats loss visas inte längre listrutan för arv. Aktiviteten är nu en lokal aktivitet.

   ![Lokal aktivitet](/help/sites-cloud/authoring/assets/multisite-winter.png)

## Återställa arv av riktat innehåll {#restoring-inheritance-of-targeted-content}

Om du har inaktiverat arv av riktat innehåll i en aktivitet kan du återställa det när som helst. Om du har kopplat loss den aktiva kopian kan du inte återställa arvet.

Så här återställer du arv av riktat innehåll i en aktivitet:

1. Navigera till sidan där du vill återställa arv och tryck eller klicka på **Mål** i listrutan Läge.
1. Tryck eller klicka på **Start Targeting**.
1. Välj **Återuppta live-kopia** i listrutan i verktygsfältet.

   ![Återupptar live-kopia](/help/sites-cloud/authoring/assets/multisite-resume.png)

1. Tryck eller klicka på **Återuppta** för att bekräfta att du vill återuppta arv av live-kopia. Alla ändringar som gjorts i den aktuella aktiviteten går förlorade om du återupptar arvet.

## Ta bort områden {#deleting-areas}

När du tar bort ett område tar du bort alla aktiviteter i det området. AEM varnar dig innan du kan ta bort ett område. Om du tar bort ett område som en webbplats är kopplad till, kommer mappningen för det här varumärket automatiskt att ändras till det överordnad området.

Så här tar du bort ett område:

1. Navigate to **Personalization** > **Activities** or **Offers** and then your brand.
1. Tryck eller klicka på ikonen bredvid det område du vill ta bort.
1. Tryck eller klicka på **Ta bort** och bekräfta att du vill ta bort området.
