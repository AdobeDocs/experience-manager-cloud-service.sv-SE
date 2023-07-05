---
title: Exportera Experience Fragments till Adobe Target
description: Exportera Experience Fragments till Adobe Target
exl-id: 752d91f9-13a6-40c2-9425-7d18dafe9205
source-git-commit: 7905f21e70f373150775fe90d5faf02db4a59c32
workflow-type: tm+mt
source-wordcount: '2245'
ht-degree: 0%

---

# Exportera Experience Fragments till Adobe Target{#exporting-experience-fragments-to-adobe-target}

>[!CAUTION]
>
>* AEM Experience Fragments exporteras till standardarbetsytan i Adobe Target.
>* AEM måste integreras med Adobe Target enligt instruktionerna i [Integrera med Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md).

Du kan exportera [Upplevelsefragment](/help/sites-cloud/authoring/fundamentals/experience-fragments.md), som har skapats i Adobe Experience Manager as a Cloud Service (AEM), till Adobe Target (Target). De kan sedan användas som erbjudanden i Target-aktiviteter för att testa och personalisera upplevelser i stor skala.

Det finns tre alternativ för att exportera ett Experience Fragment till Adobe Target:

* HTML (standard): Stöd för leverans av webb- och hybridinnehåll
* JSON: Stöd för leverans av headless-material
* HTML &amp; JSON

För att förbereda din instans för export AEM Experience Fragments till Adobe Target måste du:

* [Integrera med Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md)
* [Lägg till molnkonfigurationen](#add-the-cloud-configuration)
* [Lägg till den äldre konfigurationen](#add-the-legacy-configuration)

Efter det kan du

* [Exportera en upplevelsefragment till Adobe Target](#exporting-an-experience-fragment-to-adobe-target)
* [Använd era upplevelsefragment i Adobe Target](#using-your-experience-fragments-in-adobe-target)
* Och [Ta bort ett Experience Fragment som redan har exporterats till Adobe Target](#deleting-an-experience-fragment-already-exported-to-adobe-target)

Upplevelsefragment kan exporteras till standardarbetsytan i Adobe Target eller till användardefinierade arbetsytor för Adobe Target.

>[!NOTE]
>
>Adobe Target arbetsytor finns inte i själva Adobe Target. De definieras och hanteras i Adobe IMS (Identity Management System) och väljs sedan ut för användning i olika lösningar med Adobe Developer Console.

>[!NOTE]
>
>Adobe Target arbetsytor kan endast användas för att tillåta medlemmar i en organisation (grupp) att skapa och hantera erbjudanden och aktiviteter för denna organisation. utan att ge åtkomst till andra användare. Till exempel landsspecifika organisationer inom ett globalt område.

>[!NOTE]
>
>Mer information finns i följande:
>
>* [Utveckling av Adobe Target](https://developers.adobetarget.com/)
>* [Kärnkomponenter - Upplevelsefragment](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)
>* [Adobe Target - Hur använder jag Adobe Experience Manager (AEM) Experience Fragments?](https://experienceleague.adobe.com/docs/target/using/experiences/offers/aem-experience-fragments.html?lang=en)
>* [AEM 6.5 - Konfigurera integrationen med Adobe Target manuellt - Skapa en målmolnkonfiguration](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/target-configuring.html#creating-a-target-cloud-configuration)

## Förutsättningar {#prerequisites}

Du måste utföra olika åtgärder:

1. Du måste [integrera AEM med Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md).

1. Experience Fragments exporteras från AEM författarinstans, så du måste [Konfigurera AEM Link Externalizer](/help/implementing/developing/extending/experience-fragments.md#configuring-the-aem-link-externalizer) på författarinstansen för att säkerställa att alla referenser i Experience Fragment är externaliserade för webbleverans.

   >[!NOTE]
   >
   >För ländrörning som inte omfattas av standardinställningen används [Experience Fragment Link Rewriter-provider](/help/implementing/developing/extending/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html) är tillgängligt. Med detta kan ni utveckla anpassade regler för er instans.

## Lägg till molnkonfigurationen {#add-the-cloud-configuration}

Innan du exporterar ett fragment måste du lägga till **Molnkonfiguration** for **Adobe Target** till fragmentet eller mappen. Detta gör även att du kan:

* ange de formatalternativ som ska användas för exporten
* välj en målarbetsyta som mål
* välj en externaliseringsdomän för att skriva om referenser i Experience Fragment (valfritt)

De obligatoriska alternativen kan väljas i **Sidegenskaper** av den mapp eller det fragment som krävs, eller båda, specifikationen ärvs vid behov.

1. Navigera till **Upplevelsefragment** konsol.

1. Öppna **Sidegenskaper** för rätt mapp eller fragment.

   >[!NOTE]
   >
   >Om du lägger till molnkonfigurationen i den överordnade Experience Fragment-mappen ärvs konfigurationen av alla underordnade.
   >
   >Om du lägger till molnkonfigurationen i själva Experience Fragment ärvs konfigurationen av alla variationer.

1. Välj **Cloud Services** -fliken.

1. Under **Konfiguration av Cloud Service**, markera **Adobe Target** i listrutan.

   >[!NOTE]
   >
   >JSON-formatet i ett Experience Fragment-erbjudande kan anpassas. Om du vill göra det definierar du en Customer Experience Fragment-komponent och kommenterar sedan hur dess egenskaper ska exporteras i komponentens Sling Model.
   >
   >Se kärnkomponenten: [Kärnkomponenter - Upplevelsefragment](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/experience-fragment.html)

1. Under **Adobe Target** välj:

   * lämplig konfiguration
   * det obligatoriska formatalternativet
   * en Adobe Target-arbetsyta
   * om det behövs - externaliseringsdomänen

   >[!CAUTION]
   >
   >Externeringsdomänen är valfri.
   >
   > En AEM externaliserare konfigureras när du vill att det exporterade innehållet ska peka mot en viss *publicera* domän. Mer information finns i [Konfigurera AEM Link Externalizer](/help/implementing/developing/extending/experience-fragments.md#configuring-the-aem-link-externalizer).
   >
   > Observera också att Externalizer-domäner bara är relevanta för innehållet i Experience Fragment som skickas till Target, och inte för metadata som Visa erbjudandeinnehåll.

   För en mapp:

   ![Mapp - Cloud Services](assets/xf-target-integration-01.png "Mapp - Cloud Services")

1. **Spara och stäng**.

## Lägg till den äldre konfigurationen {#add-the-legacy-configuration}

<!-- This is effectively the Manually Integrating with Adobe Target {#manually-integrating-with-adobe-target} section from 6.5 -->

>[!IMPORTANT]
>
>Att lägga till en ny äldre konfiguration är ett specialscenario som bara stöds för export av Experience Fragments.

Efter [lägga till molnkonfigurationen](#add-the-cloud-configuration) för att kunna använda Launch by Adobe måste du, för att kunna integrera AEM med Adobe Target, även manuellt integrera med Adobe Target med en äldre konfiguration.

### Skapa en målmolnkonfiguration {#creating-a-target-cloud-configuration}

Om du vill att AEM ska kunna interagera med Adobe Target skapar du en Target-molnkonfiguration. Om du vill skapa konfigurationen anger du Adobe Target klientkod och inloggningsuppgifter.

Du skapar bara målmolnkonfigurationen en gång eftersom du kan associera konfigurationen med flera AEM kampanjer. Om du har flera Adobe Target-klientkoder skapar du en konfiguration för varje klientkod.

Du kan konfigurera molnkonfigurationen så att segment från Adobe Target synkroniseras. Om du aktiverar synkronisering importeras segment från Target i bakgrunden så snart molnkonfigurationen har sparats.

Använd följande procedur för att skapa en Target-molnkonfiguration i AEM:

1. Navigera till **Äldre Cloud Services** via **AEM logotyp** > **verktyg** > **Cloud Services** > **Äldre Cloud Services**.
Till exempel: ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html))

   The **Adobe Experience Cloud** översiktssidan öppnas.

1. I **Adobe Target** avsnitt, klicka **Konfigurera nu**.
1. I **Skapa konfiguration** dialog:

   1. Ge konfigurationen en **Titel**.
   1. Välj **Adobe Target Configuration** mall.
   1. Klicka **Skapa**.

Nu kan du välja den nya konfigurationen för redigering.

1. Dialogrutan Redigera öppnas.

   ![config-target-settings-dialog](assets/config-target-settings-dialog.png)

   <!-- Can this still occur?

   >[!NOTE]
   >
   >When configuring A4T with AEM, you may see a Configuration reference missing entry. To be able to select the analytics framework, do the following:
   >
   >1. Navigate to **Tools** &gt; **General** &gt; **CRXDE Lite**.
   >1. Navigate to **/libs/cq/analytics/components/testandtargetpage/dialog/items/tabs/items/tab1_general/items/a4tAnalyticsConfig**
   >1. Set the property **disable** to **false**.
   >1. Tap or click **Save All**.

   -->

1. I **Adobe Target-inställningar** anger du värden för dessa egenskaper.

   * **Autentisering**: detta är standardvärdet för IMS (användarens inloggningsuppgifter är inaktuella)

   * **Klientkod**: målkontots klientkod

   * **Klient-ID**: innehavar-ID

   * **IMS-konfiguration**: välj önskad konfiguration i listrutan

   * **API-typ**: standard är REST (XML är inaktuellt)

   * **A4T Analytics Cloud-konfiguration**: Välj den Analytics-molnkonfiguration som används för målaktivitetsmål och -mått. Du behöver detta om du använder Adobe Analytics som rapportkälla när du skapar innehåll för målgruppsanpassning.

     <!-- Is this needed?
     If you do not see your cloud configuration, see note in [Configuring A4T Analytics Cloud Configuration](#configuring-a-t-analytics-cloud-configuration).
     -->

   * **Använd exakt målgruppsanpassning:** Som standard är den här kryssrutan markerad. Om du väljer det här alternativet väntar molntjänstkonfigurationen på att kontexten ska läsas in innan innehållet läses in. Se följande.

   * **Synkronisera segment från Adobe Target:** Välj det här alternativet om du vill hämta segment som har definierats i Target för att använda dem i AEM. Du måste välja det här alternativet när API-typegenskapen är REST, eftersom infogade segment inte stöds och du alltid måste använda segment från Target. (Observera att den AEM termen segment motsvarar målgruppen.)

   * **Klientbibliotek:** this default to AT.js (mbox.js is deprecated)

     >[!NOTE]
     >
     >Målbiblioteksfilen, [AT.JS](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/at-js/how-atjs-works.html), är ett nytt implementeringsbibliotek för Adobe Target som är utformat för både vanliga webbimplementeringar och ensidiga program.
     >
     >mbox.js har tagits bort och kommer att tas bort i ett senare skede.
     >
     >Adobe rekommenderar att du använder AT.js i stället för mbox.js som klientbibliotek.
     >
     >AT.js har flera förbättringar jämfört med mbox.js-biblioteket:
     >
     >* Förbättrade sidladdningstider för webbimplementeringar
     >* Förbättrad säkerhet
     >* Bättre implementeringsalternativ för single-page-applikationer
     >* AT.js innehåller komponenterna som ingick i target.js, så det finns inte längre något anrop till target.js
     >
     >Du kan välja AT.js eller mbox.js i **Klientbibliotek** nedrullningsbar meny.

   * **Använd Tag Management System för att leverera klientbibliotek** - Välj det här alternativet om du vill använda klientbiblioteket från Adobe Launch eller något annat tagghanteringssystem (eller DTM, som är inaktuellt).

   * **Anpassad AT.js**: Bläddra för att ladda upp din anpassade AT.js. Lämna tomt om du vill använda standardbiblioteket.

     >[!NOTE]
     >
     >Som standard aktiveras korrekt målgruppsanpassning när du väljer att använda konfigurationsguiden för Adobe Target.
     >
     >Korrekt målinriktning innebär att molntjänstkonfigurationen väntar på att kontexten ska läsas in innan innehållet läses in. Därför kan en korrekt målinriktning i fråga om prestanda skapa en fördröjning på några millisekunder innan innehållet läses in.
     >
     >Korrekt målinriktning är alltid aktiverat på författarinstansen. På publiceringsinstansen kan du dock välja att inaktivera korrekt målanpassning globalt genom att avmarkera kryssrutan bredvid Korrekt målanpassning i molntjänstkonfigurationen (**http://localhost:4502/etc/cloudservices.html**). Du kan även aktivera och inaktivera exakt målinriktning för enskilda komponenter, oavsett vilken inställning du har i molntjänstkonfigurationen.
     >
     >Om du har ***redan*** har skapat riktade komponenter och du ändrar den här inställningen påverkar inte ändringarna dessa komponenter. Du måste göra ändringar i den komponenten direkt.

1. Klicka **Anslut till Adobe Target** för att initiera anslutningen med Target. Om anslutningen lyckas visas meddelandet **Anslutningen lyckades** visas. Klicka **OK** i meddelandet och sedan **OK** i dialogrutan.

### Lägga till ett målramverk {#adding-a-target-framework}

<!-- Is this section needed? -->

När du har konfigurerat molnkonfigurationen för Target lägger du till ett Target-ramverk. Ramverket identifierar de standardparametrar som skickas till Adobe Target från de tillgängliga [ContextHub](/help/implementing/developing/personalization/configuring-contexthub.md) -komponenter. Target använder parametrarna för att fastställa vilka segment som gäller för den aktuella kontexten.

Du kan skapa flera ramverk för en enda Target-konfiguration. Flera ramverk är användbara när du behöver skicka en annan uppsättning parametrar till Target för olika delar av webbplatsen. Skapa ett ramverk för varje uppsättning parametrar som du måste skicka. Associera varje avsnitt på webbplatsen med rätt ramverk. Observera t*att en webbsida bara kan använda ett ramverk åt gången.

1. Klicka på knappen **+** (plustecken) bredvid Tillgängliga konfigurationer.

1. I dialogrutan Skapa ramverk anger du en **Titel** väljer du **Adobe Target Framework** och klicka **Skapa**.

   <!-- ![config-target-framework-dialog](assets/config-target-framework-dialog.png) -->

   Ramverkssidan öppnas. Sidekick tillhandahåller komponenter som representerar information från [ContextHub](/help/implementing/developing/personalization/configuring-contexthub.md) som du kan mappa.

   <!-- ![Framework](assets/chlimage_1-162.png) -->

1. Dra den klientkontextkomponent som representerar de data som du vill använda för mappning till släppmålet. Du kan också dra i **ContextHub Store** till ramverket.

   >[!NOTE]
   >
   >Vid mappning skickas parametrar till en mbox via enkla strängar. Du kan inte mappa arrayer från ContextHub.

   Använd till exempel **Profildata** om webbplatsbesökarna för att styra er Target-kampanj drar du **Profildata** till sidan. De profildatavariabler som är tillgängliga för mappning till Target-parametrar visas.

   <!-- ![Profile Data](assets/chlimage_1-163.png) -->

1. Markera variablerna som du vill göra synliga för Adobe Target-systemet genom att markera **Dela** -kryssrutan i rätt kolumner.

   <!-- ![Share](assets/chlimage_1-164.png) -->

   >[!NOTE]
   >
   >Synkronisering av parametrar är bara ett sätt - från AEM till Adobe Target.

Ditt ramverk skapas. Om du vill replikera ramverket till publiceringsinstansen använder du **Aktivera ramverk** från sidosparken.

<!--
### Associating Activities With the Target Cloud Configuration  {#associating-activities-with-the-target-cloud-configuration}

Associate your [AEM activities](/help/sites-cloud/authoring/personalization/activities.md) with your Target cloud configuration so that you can mirror the activities in [Adobe Target](https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html).

>[!NOTE]
>
>What types of activities are available is determined by the following:
>
>* If the **xt_only** option is enabled on the Adobe Target tenant (clientcode) used on the AEM side to connect to Adobe Target, then you can create **only** XT activities in AEM.
>
>* If the **xt_only** options is **not** enabled on the Adobe Target tenant (clientcode), then you can create **both** XT and A/B activities in AEM.
>
>**Additional note:** **xt_only** options is a setting applied on a certain Target tenant (clientcode) and can only be modified directly in Adobe Target. You cannot enable or disable this option in AEM.
-->

<!--
### Associating the Target Framework With Your Site {#associating-the-target-framework-with-your-site}

After you create a Target framework in AEM, associate your web pages with the framework. The targeted components on the pages send the framework-defined data to Adobe Target for tracking. (See [Content Targeting](/help/sites-cloud/authoring/personalization/targeted-content.md).)

When you associate a page with the framework, the child pages inherit the association.

1. In the **Sites** console, navigate to the site that you want to configure.
1. Using either [quick actions](/help/sites-cloud/authoring/getting-started/basic-handling.md#quick-actions) or [selection mode](/help/sites-cloud/authoring/getting-started/basic-handling.md#selecting-resources), select **View Properties.**
1. Select the **Cloud Services** tab.
1. Tap/click **Edit**.
1. Tap/click **Add Configuration** under **Cloud Service Configurations** and select **Adobe Target**.

  ![Cloud Service Configuration](assets/chlimage_1-165.png)

1. Select the framework you want under **Configuration Reference**.

   >[!NOTE]
   >
   >Make sure that you select the specific **framework** that you created and not the Target cloud configuration under which it was created.

1. Tap/click **Done**.
1. Activate the root page of the website to replicate it to the publish server. (See [How To Publish Pages](/help/sites-cloud/authoring/fundamentals/publishing-pages.md).)

   >[!NOTE]
   >
   >If the framework you attached to the page was not activated yet, a wizard opens which allows you to publish it as well.
-->

## Exportera ett Experience Fragment till Adobe Target {#exporting-an-experience-fragment-to-adobe-target}

>[!CAUTION]
>
>För medieresurser, till exempel bilder, exporteras bara en referens till Target. Resursen lagras i AEM Assets och levereras från den AEM publiceringsinstansen.
>
>På grund av detta måste Experience Fragment, med alla relaterade resurser, publiceras före export till Target.

Så här exporterar du ett upplevelsefragment från AEM till mål (efter att du har angett molnkonfigurationen):

1. Navigera till Experience Fragment-konsolen.
1. Välj den Experience Fragment som du vill exportera till mål.

   >[!NOTE]
   >
   >Det måste vara en webbvariant för Experience Fragment.

1. Tryck/klicka **Exportera till Adobe Target**.

   >[!NOTE]
   >
   >Om Experience Fragment redan har exporterats väljer du **Uppdatera i Adobe Target**.

1. Tryck/klicka **Exportera utan publicering** eller **Publicera** efter behov.

   >[!NOTE]
   >
   >Markera **Publicera** publicerar upplevelsefragmentet direkt och skickar det till Target.

1. Tryck/klicka **OK** i bekräftelsedialogrutan.

   Ditt upplevelsefragment bör nu finnas i Target.

   >[!NOTE]
   >
   >[Olika detaljer](/help/sites-cloud/authoring/fundamentals/experience-fragments.md#details-of-your-experience-fragment) av exporten visas i **Listvy** av konsolen och **Egenskaper**.

   >[!NOTE]
   >
   >När du visar ett Experience Fragment i Adobe Target *senast ändrad* datum som visas är det datum då fragmentet senast ändrades i AEM, inte det datum då fragmentet senast exporterades till Adobe Target.

>[!NOTE]
>
>Du kan också exportera från sidredigeraren med jämförbara kommandon i [Sidinformation](/help/sites-cloud/authoring/fundamentals/environment-tools.md#page-information) -menyn.

## Använda dina upplevelsefragment i Adobe Target {#using-your-experience-fragments-in-adobe-target}

När du har utfört de föregående åtgärderna visas upplevelsefragmentet på sidan Erbjudanden i Target. Se [specifik Target-dokumentation](https://experiencecloud.adobe.com/resources/help/en_US/target/target/aem-experience-fragments.html) om du vill veta vad du kan uppnå där.

>[!NOTE]
>
>När du visar ett Experience Fragment i Adobe Target *senast ändrad* datum som visas är det datum då fragmentet senast ändrades i AEM, inte det datum då fragmentet senast exporterades till Adobe Target.

## Ta bort ett Experience Fragment som redan har exporterats till Adobe Target {#deleting-an-experience-fragment-already-exported-to-adobe-target}

Om du tar bort ett Experience Fragment som redan har exporterats till Target kan det orsaka problem om fragmentet redan används i ett erbjudande i Target. Om du tar bort fragmentet blir erbjudandet oanvändbart eftersom fragmentinnehållet levereras av AEM.

För att undvika sådana situationer:

* Om Experience Fragment inte används för närvarande i en aktivitet kan AEM användaren ta bort fragmentet utan ett varningsmeddelande.
* Om Experience Fragment används för närvarande av en aktivitet i Target får AEM ett felmeddelande om eventuella konsekvenser som en borttagning av fragmentet kan ha för aktiviteten.

  Felmeddelandet i AEM förhindrar inte användaren från att (tvinga) ta bort Experience Fragment. Om Experience Fragment tas bort:

   * Målerbjudandet med AEM Experience Fragment kan visa oönskat beteende

      * Erbjudandet kommer troligtvis fortfarande att återges eftersom Experience Fragment HTML flyttades till Target
      * Eventuella referenser i Experience Fragment kanske inte fungerar korrekt om refererade resurser också tas bort i AEM.

   * Det är förstås inte möjligt att göra ytterligare ändringar i Experience Fragment eftersom Experience Fragment inte längre finns i AEM.
