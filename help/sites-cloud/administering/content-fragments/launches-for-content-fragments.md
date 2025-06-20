---
title: Startar för innehållsfragment
description: Lär dig hur du använder starter för innehållsfragment i Adobe Experience Manager as a Cloud Service. Med Launches kan du effektivt utveckla innehåll för en framtida release, samtidigt som du behåller dina nuvarande innehållsfragment.
feature: Content Fragments
role: User, Developer, Architect
hide: true
hidefromtoc: true
index: false
solution: Experience Manager Sites
source-git-commit: f2adbc7fd92e846c6e09e52644f45c720c04dc4e
workflow-type: tm+mt
source-wordcount: '1582'
ht-degree: 0%

---


# Startar för innehållsfragment {#launches-for-content-fragments}

I Adobe Experience Manager (AEM) as a Cloud Service kan du med Launches effektivt utveckla material för framtida releaser.

En *Launch* skapas så att du kan göra ändringar inför framtida publicering, samtidigt som du behåller det aktuella innehållet. För innehållsfragment innebär det att du redigerar två versioner samtidigt: innehåll som är publicerat och en version av innehållet som ska publiceras i framtiden. När tiden är inne kan du ersätta innehållet i de ursprungliga innehållsfragmenten och publicera de nya versionerna.

>[!NOTE]
>
>Det finns även startprogram för Sidor. De grundläggande begreppen är desamma, men det finns skillnader i hur du hanterar dem i AEM.
>
>Mer information finns i [Starta för sidor](/help/sites-cloud/authoring/launches/overview.md).

Du skapar en *Starta* och redigerar och uppdaterar sedan dina innehållsfragment i *Starta* . Om *Source*-fragmenten ändras under den här fasen kan du kopiera dem till *Launch* med *Rebase* -åtgärden. När det är klart duplicerar *Promote* startinnehållet tillbaka till källan. Du kan sedan aktivera källfragmenten, antingen manuellt eller automatiskt (beroende på fält som angetts när du skapade och redigerade starten). Du kan också ange om refererade fragment ska inkluderas i den här processen.

Exempelvis uppdateras säsongsproduktfragmenten i din onlinebutik varje kvartal så att de produkter som ingår anpassas efter den aktuella säsongen. Om du vill förbereda dig för nästa kvartalsvisa uppdatering kan du skapa en startsida med lämpliga fragment. Under hela kvartalet ackumuleras följande ändringar i startversionen:

* Redigeringar som utförs direkt på startfragmenten som förberedelse inför nästa kvartal.
* Ändrar de källinnehållsfragment som du överför till startsidorna med *Rebase*.
* Du kan också navigera i innehållet i startgrenen, lägga till eller ta bort fragment efter behov.

När nästa kvartal anländer befordrar du startsidorna så att du kan publicera källsidorna (med det uppdaterade innehållet). Du kan befordra antingen alla fragment eller bara de som du har ändrat.

![Startar översikt - Rebase och Promote](/help/sites-cloud/administering/content-fragments/assets/cf-launches-overview.png)

I det här avsnittet beskrivs hur du skapar, redigerar, hanterar, baserar, befordrar och vid behov tar bort, startar från [konsolen för innehållsfragment](/help/sites-cloud/administering/content-fragments/managing.md):

* [Öppna och visa startprogram i konsolen för innehållsfragment](#launches-in-the-content-fragment-console)
* [Skapa en Launch](#create-a-launch)
* [Redigera startinnehåll](#edit-launch-content)
* [Hantera innehåll i en Launch](#manage-content-within-a-launch)
* [Jämför start med Source](#compare-launch-to-source)
* [Basera en Launch från Source](#rebase-a-launch-from-source)
* [Promote a Launch to Source](#promote-a-launch-to-source)
* [Ta bort en start](#delete-a-launch)

## Startar i konsolen för innehållsfragment {#launches-in-the-content-fragment-console}

På fliken **Startar** i konsolen Innehållsfragment kan du skapa starter, lista alla befintliga starter, se nyckelegenskaper och vidta åtgärder för dem.

När ingen start har valts kan du [skapa en ny start](#create-a-launch).

![Öppnar fliken i konsolen](/help/sites-cloud/administering/content-fragments/assets/cf-launches-tab.png)

Välj vilken programstart du vill visa:

* verktygsfältet, med tillgängliga åtgärder
* den högra panelen med egenskaper och ytterligare åtgärder

![Starta verktygsfältet för åtgärder i konsolen](/help/sites-cloud/administering/content-fragments/assets/cf-launches-actions.png)

Med verktygsfältet kan du:

* **[Öppna start](#edit-launch-content)**
* **[Redigera källor](#manage-content-within-a-launch)**
* **[Jämför start med Source](#compare-launch-to-source)**
* **[Befordra](#promote-a-launch-to-source)**
* **[Rebase](#promote-a-launch-to-source)**
* **[Ta bort start](#delete-a-launch)**

Med den högra panelen kan du:

* Redigera **Starttitel**
* Redigera startbeskrivningen **Beskrivning**
* Uppdatera konfigurationsinformation som angavs när du [skapade starten](#create-a-launch):

   * **Inkludera referenser**: Skapa Launch med, eller utan, inklusive refererade innehållsfragment. Som standard inkluderas refererade fragment.

      * Refererade fragment påverkas också när du [lägger till eller tar bort fragment från start](#manage-content-within-a-launch) i ett senare skede.

     >[!NOTE]
     >
     >Se [Information om inkluderade referenser](#details-concerning-included-references)

   * **Publiceringsklar**. Om du aktiverar den här växeln publiceras fragmenten automatiskt när starten befordras till källan.

* Definiera också:

   * **Befordra datum** och tid: Om [starten ska befordras automatiskt](#promote-automatically)

## Skapa en Launch {#create-a-launch}

Så här skapar du en start:

1. Navigera till konsolen Innehållsfragment.

1. Öppna fliken **Startar**.

1. Välj **Skapa start**.

1. Navigera till rätt mapp och välj de fragment som ska inkluderas i starten:

   ![Välj innehållsfragment för ny start](/help/sites-cloud/administering/content-fragments/assets/cf-launches-create-select-cfs.png)

1. Välj **Nästa**.

1. Ange information för att konfigurera starten:

   * **Titel**
   * **Beskrivning**
   * **Inkludera referenser**: Skapa starten med, eller utan, inklusive refererade innehållsfragment. Som standard inkluderas refererade fragment.

     >[!NOTE]
     >
     >Se [Information om inkluderade referenser](#details-concerning-included-references)

   * **Publiceringsklar**: Om du aktiverar den här växeln publiceras fragmenten automatiskt när starten befordras till källan.

   ![Information om ny start](/help/sites-cloud/administering/content-fragments/assets/cf-launches-create-launch-details.png)

1. **Spara** konfigurationen.

1. Du återgår till fliken **Startar** i konsolen för innehållsfragment, där:

   * din nya lansering visas nu
   * visas ett meddelande som bekräftar att startskapandet har startat:

      * **Jobbet började skapa en ny start, övervaka förloppet i AEM och ladda om sidan när det är klart.**

1. Välj **Visa** i meddelanderutan om du vill visa mer information i AEM-konsolen för [bakgrundsåtgärder](/help/operations/asynchronous-jobs.md).

   ![Ny start i konsolen](/help/sites-cloud/administering/content-fragments/assets/cf-launches-new-launch-in-console.png)

## Redigera startinnehåll {#edit-launch-content}

Så här redigerar du innehållsfragment vid start:

1. Navigera till konsolen Innehållsfragment.

1. Öppna fliken **Startar**.

1. Välj hur du startar om du vill visa verktygsfältets åtgärder.

1. Välj **Öppna start**.

   Din lansering visas tillsammans med de fragment som den innehåller.

   ![Redigera startinnehåll](/help/sites-cloud/administering/content-fragments/assets/cf-launches-edit-launch-content.png)

1. Välj **Redigera** för det fragment som du vill uppdatera. Det öppnas som vanligt i [fragmentredigeraren](/help/sites-cloud/administering/content-fragments/authoring.md).

## Hantera innehåll i en Launch {#manage-content-within-a-launch}

Så här hanterar du innehållsfragment när du startar och redigerar deras innehåll:

1. Navigera till konsolen Innehållsfragment.

1. Öppna fliken **Startar**.

1. Välj programstart.

1. Välj **Redigera källor**.

   Källfragmenten för din lansering visas.

   ![Redigera Source](/help/sites-cloud/administering/content-fragments/assets/cf-launches-edit-sources.png)

1. Du kan:

   1. **Lägg till källor** om du vill lägga till fler fragment vid starten.

      * Om **Inkludera referenser** är true för starten hämtas även alla refererade innehållsfragment till starten (om de inte redan finns).

   1. Välj **Redigera** för det källfragment som du vill uppdatera. Det öppnas som vanligt i [fragmentredigeraren](/help/sites-cloud/administering/content-fragments/authoring.md).

   1. Markera ett fragment och ta sedan bort fragmentet från programstarten med åtgärden **Ta bort källor** i verktygsfältet.

      * Om **Inkludera referenser** är true för starten tas även alla refererade innehållsfragment bort från starten, såvida de inte också refereras av andra innehållsfragment som fortfarande är i starten.

   >[!NOTE]
   >
   >Se [Information om inkluderade referenser](#details-concerning-included-references)

## Jämför start med Source {#compare-launch-to-source}

Vi rekommenderar att du alltid jämför källan och starten innan du utför någon Rebase- eller Promote-åtgärd för att bekräfta ändringarna och deras effekt på innehållet (båda åtgärderna skriver över målinnehållet):

1. Navigera till konsolen Innehållsfragment.

1. Öppna fliken **Startar**.

1. Välj programstart.

1. Välj **Jämför start med Source**.

   * Käll- och startfragmenten visas sida vid sida för att framhäva skillnaderna.
      * Source-fragment visas till vänster, Launch-fragment visas till höger.
      * Uppdateringar är markerade:
         * Source: blå
         * Launch: rosa
         * Konflikter: gult
   * Åtgärderna [Befordra](#promote-a-launch-to-source) och [Rebase](#rebase-a-launch-from-source) är tillgängliga från det övre högra hörnet.
   * **Uppdateringar hittades**: I det övre vänstra hörnet visas en sammanfattning av alla uppdateringar. Antalet källuppdateringar i blått, antalet startuppdateringar i rosa och uppdateringar av båda (konflikter) i gult.
      * Med ögonikonerna kan du visa eller dölja det faktiska innehållet uppdateras för att få en tydligare översikt.
   * Med **Inkludera**-skjutreglage kan du definiera de innehållsfragment som ska inkluderas i efterföljande Befordra- eller Rebase-åtgärd:
      * **Inkludera alla** längst upp till höger
      * **Inkludera** ovanför alla fragment i starten

     >[!NOTE]
     >
     >Skjutreglagen gäller bara för Befordra och Rebase-åtgärder som har tagits från Jämför-skärmen.

   * Fragmentinnehåll visas på fältnivå (Content Fragment element/datatype-level) med markeringar som anger ändringar.
   * Välj **Visa** om du vill beräkna om skillnaderna.

   ![Jämför Source och starta](/help/sites-cloud/administering/content-fragments/assets/cf-launches-compare.png)

## Rebase a Launch (från Source) {#rebase-a-launch-from-source}

När uppdateringar har gjorts av källfragmenten och du vill kopiera dessa ändringar till din start:

1. Navigera till konsolen Innehållsfragment.

1. Öppna fliken **Startar**.

1. Välj programstart och fragment.

1. Välj **Rebase**.

>[!NOTE]
>
>Du kan även **Rebase** starta från **[Jämför start med Source](#compare-launch-to-source)**.

## Promote a Launch (to Source) {#promote-a-launch-to-source}

När startprogrammet är klart att publiceras bör det kopieras till källan. Du kan antingen göra detta i konsolen eller konfigurera inställningarna så att det sker automatiskt vid ett visst datum och en viss tidpunkt.

### Befordra manuellt {#promote-manually}

När startprogrammet är klart att publiceras kan det kopieras till källan med den explicita åtgärden:

1. Navigera till konsolen Innehållsfragment.

1. Öppna fliken **Startar**.

1. Välj programstart och fragment.

1. Välj **Befordra**.

>[!NOTE]
>
>Du kan även **befordra** en start från **Jämför start till Source**.

### Befordra automatiskt {#promote-automatically}

För att en start ska befordras automatiskt vid ett angivet datum och klockslag måste du:

1. Definiera **Befordra datum** och tid på den högra panelen på fliken [Start](#launches-in-the-content-fragment-console).

1. Om innehållet kan publiceras när det befordras anger du **Publiceringsklar** när [startar](#create-a-launch) eller från den högra panelen på fliken [Start](#launches-in-the-content-fragment-console).

## Ta bort en start {#delete-a-launch}

När du har befordrat lanseringen eller beslutat att du inte längre behöver den kan du ta bort den:

1. Navigera till konsolen Innehållsfragment.

1. Öppna fliken **Startar**.

1. Välj programstart.

1. Välj **Ta bort start**.

   Du ombeds bekräfta åtgärden innan starten tas bort.

## Uppgifter om inkluderade referenser {#details-concerning-included-references}

För Startar beaktas följande Content Fragment-referenser, beroende på [datatyp](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#data-types):

* Datatypen **Fragmentreferens**, som används för både enskilda fragmentreferenser och fragmentreferenser för flera fält.
* Fragment som refereras inuti datatypen **Flera rader** när **RTF** används.

Alla punkter gäller även för fragment som refereras inom variationer

Följande beaktas inte:

* Fragment som refereras inuti innehållets referensdatatyper, både **Innehållsreferens** (sökvägsbaserad) och **Innehållsreferens (UUID)**.
* Fragment som refereras inuti datatypen **Fragment Reference (UUID)**.