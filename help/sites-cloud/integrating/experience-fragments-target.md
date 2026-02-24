---
title: Exportera Experience Fragments till Adobe Target
description: Lär dig hur du exporterar dina Experience Fragments till Adobe Target för att testa och personalisera upplevelser.
badgeSaas: label="AEM Sites" type="Positive" tooltip="Gäller AEM Sites)."
exl-id: 752d91f9-13a6-40c2-9425-7d18dafe9205
solution: Experience Manager Sites
feature: Integration
role: Admin
source-git-commit: 98c0c9b6adbc3d7997bc68311575b1bb766872a6
workflow-type: tm+mt
source-wordcount: '2198'
ht-degree: 0%

---

# Exportera Experience Fragments till Adobe Target{#exporting-experience-fragments-to-adobe-target}

>[!CAUTION]
>
>* AEM Experience Fragments exporteras till standardarbetsytan i Adobe Target.
>* AEM måste integreras med Adobe Target enligt instruktionerna under [Integrering med Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md).

Du kan exportera [Experience Fragments](/help/sites-cloud/authoring/fragments/content-fragments.md), som har skapats i Adobe Experience Manager as a Cloud Service (AEM), till Adobe Target (Target). De kan sedan användas som erbjudanden i Target-aktiviteter för att testa och personalisera upplevelser i stor skala.

Det finns tre alternativ för att exportera ett Experience Fragment till Adobe Target:

* HTML (standard): Stöd för leverans av webb- och hybridinnehåll
* JSON: Stöd för leverans av headless-innehåll
* HTML &amp; JSON

För att förbereda din instans för export av AEM Experience Fragments till Adobe Target måste du:

* [Integrera med Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md)
* [Lägg till molnkonfigurationen](#add-the-cloud-configuration)
* [Lägg till den äldre konfigurationen](#add-the-legacy-configuration)

Efter det kan du

* [Exportera en upplevelsefragment till Adobe Target](#exporting-an-experience-fragment-to-adobe-target)
* [Använd era upplevelsefragment i Adobe Target](#using-your-experience-fragments-in-adobe-target)
* Dessutom [Ta bort ett Experience Fragment som redan har exporterats till Adobe Target](#deleting-an-experience-fragment-already-exported-to-adobe-target)

Upplevelsefragment kan exporteras till standardarbetsytan i Adobe Target eller till användardefinierade arbetsytor för Adobe Target.

>[!NOTE]
>
>Adobe Target arbetsytor finns inte i själva Adobe Target. De definieras och hanteras i Adobe IMS (Identity Management System) och väljs sedan ut för användning i olika lösningar med Adobe Developer Console.

>[!NOTE]
>
>Adobe Target arbetsytor kan användas för att tillåta medlemmar i en organisation (grupp) att endast skapa och hantera erbjudanden och aktiviteter för den här organisationen, utan att ge åtkomst till andra användare. Till exempel landsspecifika organisationer inom ett globalt område.

>[!NOTE]
>
>Mer information finns i följande:
>
>* [Adobe Target-utveckling](https://developers.adobetarget.com/)
>* [Kärnkomponenter - Upplevelsefragment](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html)
>* [Adobe Target - Hur använder jag Adobe Experience Manager (AEM) Experience Fragments?](https://experienceleague.adobe.com/docs/target/using/experiences/offers/aem-experience-fragments.html)
>* [AEM 6.5 - Konfigurera integrationen med Adobe Target manuellt - Skapa en målmolnkonfiguration](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/target-configuring.html#creating-a-target-cloud-configuration)

## Förutsättningar {#prerequisites}

Du måste utföra olika åtgärder:

1. Du måste [integrera AEM med Adobe Target](/help/sites-cloud/integrating/integrating-adobe-target.md).

1. Experience Fragments exporteras från AEM-författarinstansen, så du måste [konfigurera AEM Link Externalizer](/help/implementing/developing/extending/experience-fragments.md#configuring-the-aem-link-externalizer) för författarinstansen för att se till att alla referenser i Experience Fragment är externaliserade för webbleverans.

   >[!NOTE]
   >
   >[Experience Fragment Link Rewriter-providern](/help/implementing/developing/extending/experience-fragments.md#the-experience-fragment-link-rewriter-provider-html) är tillgänglig för läntreskrivning som inte omfattas av standardinställningen. Med detta kan ni utveckla anpassade regler för er instans.

## Lägg till molnkonfigurationen {#add-the-cloud-configuration}

Innan du exporterar ett fragment måste du lägga till **molnkonfigurationen** för **Adobe Target** i fragmentet eller mappen. Detta gör även att du kan:

* ange de formatalternativ som ska användas för exporten
* välj en målarbetsyta som mål
* välj en externaliseringsdomän för att skriva om referenser i Experience Fragment (valfritt)

De obligatoriska alternativen kan väljas i **Sidegenskaper** för den obligatoriska mappen, eller i ett fragment, eller båda. Specifikationen ärvs om det behövs.

1. Navigera till konsolen **Experience Fragments**.

1. Öppna **Sidegenskaper** för rätt mapp eller fragment.

   >[!NOTE]
   >
   >Om du lägger till molnkonfigurationen i den överordnade Experience Fragment-mappen ärvs konfigurationen av alla underordnade.
   >
   >Om du lägger till molnkonfigurationen i själva Experience Fragment ärvs konfigurationen av alla variationer.

1. Välj fliken **Molntjänster**.

1. Under **Cloud Service Configuration** väljer du **Adobe Target** i listrutan.

   >[!NOTE]
   >
   >JSON-formatet i ett Experience Fragment-erbjudande kan anpassas. Om du vill göra det definierar du en Customer Experience Fragment-komponent och kommenterar sedan hur dess egenskaper ska exporteras i komponentens Sling Model.
   >
   >Visa kärnkomponenten: [Kärnkomponenter - Upplevelsefragment](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/experience-fragment.html)

1. Under **Adobe Target** väljer du:

   * lämplig konfiguration
   * det obligatoriska formatalternativet
   * en Adobe Target-arbetsyta
   * vid behov - externaliseringsdomänen

   >[!CAUTION]
   >
   >Externeringsdomänen är valfri.
   >
   > En AEM-externalisering konfigureras när du vill att det exporterade innehållet ska peka på en specifik *publiceringsdomän*. Mer information finns i [Konfigurera AEM Link Externalizer](/help/implementing/developing/extending/experience-fragments.md#configuring-the-aem-link-externalizer).
   >
   > Observera också att Externalizer-domäner bara är relevanta för innehållet i Experience Fragment som skickas till Target, och inte för metadata som Visa erbjudandeinnehåll.

   För en mapp:

   ![Mapp - molntjänster](assets/xf-target-integration-01.png "Mapp - molntjänster")

1. **Spara och stäng**.

## Lägg till den äldre konfigurationen {#add-the-legacy-configuration}

<!-- This is effectively the Manually Integrating with Adobe Target {#manually-integrating-with-adobe-target} section from 6.5 -->

>[!IMPORTANT]
>
>Att lägga till en ny äldre konfiguration är ett specialscenario som bara stöds för export av Experience Fragments.

När du har [lagt till molnkonfigurationen](#add-the-cloud-configuration) för att använda Launch från Adobe måste du även integrera AEM med Adobe Target manuellt med Adobe Target med en äldre konfiguration.

### Skapa en målmolnkonfiguration {#creating-a-target-cloud-configuration}

Om du vill att AEM ska kunna interagera med Adobe Target skapar du en Target-molnkonfiguration. Om du vill skapa konfigurationen anger du Adobe Target klientkod och inloggningsuppgifter.

Du skapar molnkonfigurationen för Target endast en gång eftersom du kan associera konfigurationen med flera AEM-kampanjer. Om du har flera Adobe Target-klientkoder skapar du en konfiguration för varje klientkod.

Du kan konfigurera molnkonfigurationen så att segment från Adobe Target synkroniseras. Om du aktiverar synkronisering importeras segment från Target i bakgrunden så snart molnkonfigurationen har sparats.

Gör så här för att skapa en Target-molnkonfiguration i AEM:

1. Navigera till **Äldre molntjänster** via **AEM-logotypen** > **Verktyg** > **Molntjänster** > **Äldre molntjänster**.
Till exempel: ([http://localhost:4502/libs/cq/core/content/tools/cloudservices.html](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html))

   Översiktssidan för **Adobe Experience Cloud** öppnas.

1. Klicka på **Konfigurera nu** i avsnittet **Adobe Target**.
1. I dialogrutan **Skapa konfiguration**:

   1. Ge konfigurationen en **titel**.
   1. Välj mallen **Adobe Target Configuration**.
   1. Klicka på **Skapa**.

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
   >1. Select **Save All**.

   -->

1. Ange värden för de här egenskaperna i dialogrutan **Adobe Target-inställningar**.

   * **Autentisering**: som standard används IMS (användarautentiseringsuppgifter är inaktuella)

   * **Klientkod**: Målkontots klientkod

   * **Klient-ID**: klientorganisations-ID

   * **IMS-konfiguration**: välj den konfiguration som krävs i listrutan

   * **API-typ**: standard är REST (XML är inaktuellt)

   * **A4T Analytics Cloud Configuration**: Välj den Analytics-molnkonfiguration som används för mål- och mätvärden för aktivitet. Du behöver detta om du använder Adobe Analytics som rapportkälla när du skapar innehåll för målgruppsanpassning.

     <!-- Is this needed?
     If you do not see your cloud configuration, see note in [Configuring A4T Analytics Cloud Configuration](#configuring-a-t-analytics-cloud-configuration).
     -->

   * **Använd korrekt målinriktning:** Som standard är den här kryssrutan markerad. Om du väljer det här alternativet väntar molntjänstkonfigurationen på att kontexten ska läsas in innan innehållet läses in. Se följande.

   * **Synkronisera segment från Adobe Target:** Välj det här alternativet om du vill hämta segment som har definierats i Target för att använda dem i AEM. Välj det här alternativet när API-typegenskapen är REST, eftersom textbundna segment inte stöds och du alltid måste använda segment från Target. (AEM-termen för segment motsvarar målgruppen.)

   * **Klientbibliotek:** som standard är AT.js (mbox.js är inaktuellt)

     >[!NOTE]
     >
     >Målbiblioteksfilen, [AT.JS](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/at-js/how-atjs-works.html), är ett nytt implementeringsbibliotek för Adobe Target som är utformat för både vanliga webbimplementeringar och enkelsidiga program.
     >
     >mbox.js har tagits bort och kommer att tas bort i ett senare skede.
     >
     >Adobe rekommenderar att du använder AT.js i stället för mbox.js som klientbibliotek.
     >
     >AT.js har flera förbättringar jämfört med mbox.js-biblioteket:
     >
     >* Förbättrade sidladdningstider för webbimplementeringar
     >* Förbättrad säkerhet
     >* Bättre implementeringsalternativ för ensidiga program
     >* AT.js innehåller komponenterna som ingick i target.js, så det finns inte längre något anrop till target.js
     >
     >Du kan välja AT.js eller mbox.js i listrutan **Klientbibliotek** .

   * **Använd Tag Management System för att leverera klientbibliotek** - Välj det här alternativet om du vill använda klientbiblioteket från Adobe Launch eller ett annat tagghanteringssystem (eller DTM, som är inaktuellt).

   * **Anpassad AT.js**: Bläddra för att överföra din anpassade AT.js. Lämna tomt om du vill använda standardbiblioteket.

     >[!NOTE]
     >
     >Som standard aktiveras korrekt målgruppsanpassning när du väljer att använda konfigurationsguiden för Adobe Target.
     >
     >Korrekt målinriktning innebär att molntjänstkonfigurationen väntar på att kontexten ska läsas in innan innehållet läses in. Därför kan en korrekt målinriktning, vad gäller prestanda, skapa en fördröjning på några millisekunder innan innehållet läses in.
     >
     >Korrekt målinriktning är alltid aktiverat på författarinstansen. På publiceringsinstansen kan du dock avaktivera korrekt målinriktning globalt genom att avmarkera kryssrutan intill Accurate Targeting i molntjänstkonfigurationen (**http://localhost:4502/etc/cloudservices.html**). Du kan även aktivera och inaktivera exakt målinriktning för enskilda komponenter, oavsett vilken inställning du har i molntjänstkonfigurationen.
     >
     >Om du redan har ***skapat*** målkomponenter och du ändrar den här inställningen påverkar ändringarna inte dessa komponenter. Du måste göra ändringar i den komponenten direkt.

1. Klicka på **Anslut till Adobe Target** för att initiera anslutningen med Target. Om anslutningen lyckas visas meddelandet **Anslutningen lyckades**. Klicka på **OK** i meddelandet och sedan på **OK** i dialogrutan.

### Lägga till ett målramverk {#adding-a-target-framework}

<!-- Is this section needed? -->

När du har konfigurerat molnkonfigurationen för Target lägger du till ett Target-ramverk. Ramverket identifierar de standardparametrar som skickas till Adobe Target från de tillgängliga [ContextHub](/help/implementing/developing/personalization/configuring-contexthub.md) -komponenterna. Target använder parametrarna för att fastställa vilka segment som gäller för den aktuella kontexten.

Du kan skapa flera ramverk för en enda Target-konfiguration. Flera ramverk är användbara när du behöver skicka en annan uppsättning parametrar till Target för olika delar av webbplatsen. Skapa ett ramverk för varje uppsättning parametrar som du måste skicka. Associera varje avsnitt på webbplatsen med rätt ramverk. Observera t*att en webbsida bara kan använda ett ramverk åt gången.

1. Klicka på **+** (plustecken) bredvid Tillgängliga konfigurationer på målkonfigurationssidan.

1. Ange en **titel** i dialogrutan Skapa ramverk, markera **Adobe Target Framework** och klicka på **Skapa**.

   <!-- ![config-target-framework-dialog](assets/config-target-framework-dialog.png) -->

   Ramverkssidan öppnas. Sidekick innehåller komponenter som representerar information från [ContextHub](/help/implementing/developing/personalization/configuring-contexthub.md) som du kan mappa.

   <!-- ![Framework](assets/chlimage_1-162.png) -->

1. Dra den klientkontextkomponent som representerar de data som du vill använda för mappning till släppmålet. Du kan också dra **ContextHub Store** -komponenten till ramverket.

   >[!NOTE]
   >
   >Vid mappning skickas parametrar till en mbox via enkla strängar. Du kan inte mappa arrayer från ContextHub.

   Om du till exempel vill använda **profildata** om webbplatsbesökarna för att styra målkampanjen drar du komponenten **profildata** till sidan. De profildatavariabler som är tillgängliga för mappning till Target-parametrar visas.

   <!-- ![Profile Data](assets/chlimage_1-163.png) -->

1. Markera de variabler som du vill göra synliga för Adobe Target-systemet genom att markera kryssrutan **Dela** i rätt kolumner.

   <!-- ![Share](assets/chlimage_1-164.png) -->

   >[!NOTE]
   >
   >Synkronisering av parametrar är bara ett sätt - från AEM till Adobe Target.

Ditt ramverk har skapats. Om du vill replikera ramverket till publiceringsinstansen använder du alternativet **Aktivera ramverk** från sidosparken.

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
1. Using either [quick actions](/help/sites-cloud/authoring/basic-handling.md#quick-actions) or [selection mode](/help/sites-cloud/authoring/basic-handling.md#selecting-resources), select **View Properties.**
1. Select the **Cloud Services** tab.
1. Select **Edit**.
1. Select **Add Configuration** under **Cloud Service Configurations** and select **Adobe Target**.

  ![Cloud Service Configuration](assets/chlimage_1-165.png)

1. Select the framework you want under **Configuration Reference**.

   >[!NOTE]
   >
   >Make sure that you select the specific **framework** that you created and not the Target cloud configuration under which it was created.

1. Select **Done**.
1. Activate the root page of the website to replicate it to the publish server. (See [How To Publish Pages](/help/sites-cloud/authoring/sites-console/publishing-pages.md).)

   >[!NOTE]
   >
   >If the framework you attached to the page was not activated yet, a wizard opens which lets you publish it as well.
-->

## Exportera ett Experience Fragment till Adobe Target {#exporting-an-experience-fragment-to-adobe-target}

>[!CAUTION]
>
>För medieresurser, till exempel bilder, exporteras bara en referens till Target. Resursen lagras i AEM Assets och levereras från AEM publiceringsinstans.
>
>Därför måste Experience Fragment, med alla relaterade resurser, publiceras innan du exporterar till Target.

Så här exporterar du ett upplevelsefragment från AEM till Target (efter att du har angett molnkonfigurationen):

1. Navigera till Experience Fragment-konsolen.
1. Välj den Experience Fragment som du vill exportera till mål.

   >[!NOTE]
   >
   >Det måste vara en webbvariant för Experience Fragment.

1. Välj **Exportera till Adobe Target**.

   >[!NOTE]
   >
   >Om Experience Fragment redan har exporterats väljer du **Uppdatera i Adobe Target**.

1. Välj **Exportera utan publicering** eller **Publicera** efter behov.

   >[!NOTE]
   >
   >Om du väljer **Publicera** publiceras upplevelsefragmentet direkt och skickas till Target.

1. Välj **OK** i bekräftelsedialogrutan.

   Ditt upplevelsefragment bör nu finnas i Target.

   >[!NOTE]
   >
   >[Olika detaljer](/help/sites-cloud/authoring/fragments/content-fragments.md#details-of-your-experience-fragment) i exporten visas i **listvyn** i konsolen och i **Egenskaper**.

   >[!NOTE]
   >
   >När du visar ett Experience Fragment i Adobe Target är det *senast ändrade*-datum som visas det datum då fragmentet senast ändrades i AEM, inte det datum då fragmentet senast exporterades till Adobe Target.

>[!NOTE]
>
>Du kan också exportera från sidredigeraren med jämförbara kommandon på menyn [Sidinformation](/help/sites-cloud/authoring/page-editor/introduction.md#page-information) .

## Använda dina upplevelsefragment i Adobe Target {#using-your-experience-fragments-in-adobe-target}

När du har utfört de föregående åtgärderna visas upplevelsefragmentet på sidan Erbjudanden i Target. Mer information om vad du kan uppnå där finns i [specifik måldokumentation](https://experiencecloud.adobe.com/resources/help/en_US/target/target/aem-experience-fragments.html).

>[!NOTE]
>
>När du visar ett Experience Fragment i Adobe Target är det *senast ändrade*-datum som visas det datum då fragmentet senast ändrades i AEM, inte det datum då fragmentet senast exporterades till Adobe Target.

## Ta bort ett Experience Fragment som redan har exporterats till Adobe Target {#deleting-an-experience-fragment-already-exported-to-adobe-target}

Om du tar bort ett Experience Fragment som redan har exporterats till Target kan det orsaka problem om fragmentet redan används i ett erbjudande i Target. Om du tar bort fragmentet blir erbjudandet oanvändbart eftersom fragmentinnehållet levereras av AEM.

För att undvika sådana situationer:

* Om Experience Fragment inte används för närvarande i en aktivitet kan AEM ta bort fragmentet utan ett varningsmeddelande.
* Om Experience Fragment används av en aktivitet i Target får AEM-användaren ett felmeddelande om eventuella konsekvenser som en borttagning av fragmentet kan ha för aktiviteten.

  Felmeddelandet i AEM förhindrar inte användaren från att (tvinga) ta bort Experience Fragment. Om Experience Fragment tas bort:

   * Target-erbjudandet med AEM Experience Fragment kan visa oönskat beteende

      * Erbjudandet kommer troligtvis fortfarande att återges eftersom Experience Fragment HTML skickades till Target
      * Eventuella referenser i Experience Fragment kanske inte fungerar korrekt om refererade resurser även har tagits bort i AEM.

   * Det är förstås inte möjligt att göra ytterligare ändringar i Experience Fragment eftersom Experience Fragment inte längre finns i AEM.
