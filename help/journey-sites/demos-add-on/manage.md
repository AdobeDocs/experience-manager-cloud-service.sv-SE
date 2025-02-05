---
title: Hantera dina demowebbplatser
description: Lär dig mer om de verktyg du kan använda för att hantera demowebbplatser och hur du tar bort dem.
exl-id: 988c6e09-c43e-415f-8d61-998c294c5a11
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 0%

---

# Hantera dina demowebbplatser {#manage-demo-sites}

Lär dig mer om de verktyg du kan använda för att hantera demowebbplatser och hur du tar bort dem.

## Story hittills {#story-so-far}

I det föregående dokumentet för AEM Reference Demos Add-On-resan, [Create Site](create-site.md), skapade du en ny demowebbplats baserat på mallarna för Reference Demo Add-On. Nu bör du:

* Lär dig hur du kommer åt AEM.
* Lär dig hur du skapar en webbplats baserad på en mall.
* Förstå grunderna för navigering i webbplatsstrukturen och redigering av en sida.

Om du även [har aktiverat AEM Screens för din demowebbplats](screens.md) bör du även:

* Lär dig grunderna i AEM Screens.
* Förstå demoinnehållet för We.Cafe.
* Lär dig konfigurera AEM Screens för We.Cafe.

Nu när du har en egen demosajt att utforska beskriver den här artikeln de verktyg som finns för att hantera dina demosajter och hur du tar bort dem.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur du kan hantera de demowebbplatser du har skapat. När du har läst bör du:

* Lär dig hur du får tillgång till självbetjäningsdemoverktygen.
* Ta reda på vilka verktyg som är tillgängliga för dig.
* Så här tar du bort en befintlig demowebbplats eller -mall.

## Åtkomst till självbetjäningsdemoverktyg {#accessing-utilities}

Nu när du har egna demosajter vill du antagligen veta hur du kan hantera dem. Det var inte bara webbplatsmallarna som distribuerades för att ge plats åt demonstrationssajterna, utan även en uppsättning verktyg för att hantera dessa sajter.

1. I det AEM globala navigeringsfältet väljer du **Verktyg** > **Referensdemonstrationer** > **Referensdemoverktyg**.

   ![Självbetjäningsdemoverktyg](assets/demo-utilities.png)

1. Demoverktyg för referens är en samling användbara funktioner som hjälper dig att installera och övervaka din Adobe Experience Manager-miljö. Den inledande vyn är **Dashboard** som fungerar som en statuskontroll av miljön och dess demofunktioner.

   ![Instrumentpanel](assets/dashboard.png)

Självbetjäningsdemoverktyg har flera verktyg.

* **Ta bort platser** - Markera den plats du vill ta bort i den här Adobe Experience Manager-instansen. Tänk på att detta är en destruktiv åtgärd som inte kan ångras när den väl har initierats.
* **Ta bort webbplatsmallar** - Markera den platsmall som du vill ta bort i den här Adobe Experience Manager-instansen. Innan du tar bort en platsmall kontrollerar du att även alla webbplatser som refererar till mallen tas bort. Tänk på att detta är en destruktiv åtgärd som inte kan ångras när den väl har initierats.
* **Prime Author Cache** - Detta hämtar flera resurser i Adobe Experience Manager-instansen, vilket snabbar upp hämtningstiden. Det kan ta flera sekunder.
* **Android App** - verktyg för att installera och starta demonstrationsappen för Android. Skapa en webbplats baserad på **WKND-appen för en sida** för att fylla i den här sidan. Använd från en Android-enhet, emulator eller Bluestacks.
* **Användarinställningar** - Inaktivera dialogrutor för självstudiekurser.
* **Konfigurera GraphQL** - Konfigurera snabbt den globala GraphQL-slutpunkten.

## Ta bort demowebbplatser och mallar {#deleting}

När du har testat en uppsättning AEM funktioner behöver du kanske inte längre demowebbplatsen eller ens den mall som den baseras på. Det är enkelt att ta bort både demowebbplatser och webbplatsmallar.

1. Gå till **Referensdemoverktyg** och välj **Ta bort platser**.

   ![Ta bort platser](assets/delete-sites.png)

1. De tillgängliga platserna visas i en lista. Kontrollera den eller de webbplatser som du vill ta bort och välj sedan **Ta bort**.

   >[!CAUTION]
   >
   >Borttagning av webbplats och mall är en destruktiv åtgärd och kan inte ångras när den har initierats.

1. Bekräfta borttagningen av platsen i dialogrutan.

   ![Bekräfta borttagning av webbplats](assets/confirm-site-delete.png)

1. AEM tar bort den eller de markerade platserna och visar förloppet där knappen **Ta bort** fanns tidigare.

   ![Ta bort förlopp](assets/delete-progress.png)

Webbplatsen har nu tagits bort.

Du kan ta bort mallar på samma sätt under rubriken **Ta bort webbplatsmallar** i **Referensdemoverktyg**.

>[!CAUTION]
>
>Innan du tar bort en platsmall kontrollerar du att även alla webbplatser som refererar till mallen tas bort.

## Slut på resan? {#end-of-journey}

Grattis! Du har slutfört AEM Reference Demos-tillägget! Nu bör du:

* Få en grundläggande förståelse för Cloud Manager och förstå hur rörledningar levererar innehåll och konfigurationer till AEM.
* Lär dig hur du använder Cloud Manager för att skapa ett program.
* Lär dig hur du aktiverar tillägget Referensdemonstrationer för det nya programmet och kan köra en pipeline för att distribuera tilläggsinnehållet.
* Lär dig hur du får åtkomst till AEM redigeringsmiljö för att skapa en plats som är baserad på en mall.
* Lär dig hur du får tillgång till självbetjäningsdemoverktygen.
* Lär dig hur du tar bort en befintlig demowebbplats eller demomall.

Du är nu redo att utforska möjligheterna att AEM med dina egna demosajter. AEM är dock ett kraftfullt verktyg och det finns många andra alternativ. Ta en titt på några av de ytterligare resurser som är tillgängliga i avsnittet [Ytterligare resurser](#additional-resources) om du vill veta mer om de funktioner du såg under den här resan.

## Ytterligare resurser {#additional-resources}

* [Cloud Manager-dokumentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/onboarding-concepts/cloud-manager-introduction.html) - Om du vill ha mer information om Cloud Manager funktioner kan det vara bra att läsa den detaljerade tekniska dokumentationen.
* [Skapa plats](/help/sites-cloud/administering/site-creation/create-site.md) - Lär dig hur du använder AEM för att skapa en webbplats med hjälp av webbplatsmallar för att definiera webbplatsens format och struktur.
* [AEM sidnamnkonventioner](/help/sites-cloud/authoring/sites-console/organizing-pages.md#page-name-restrictions-and-best-practices). - På den här sidan finns information om hur du organiserar AEM sidor.
* [AEM Grundläggande hantering](/help/sites-cloud/authoring/basic-handling.md) - Utforska det här dokumentet om du inte AEM förstå grundläggande begrepp som navigering och konsolorganisation.
* [AEM as a Cloud Service tekniska dokumentation](https://experienceleague.adobe.com/docs/experience-manager-cloud-service.html) - Om du redan har en god förståelse för AEM kan det vara bra att läsa de detaljerade tekniska dokumenten direkt.
* [Webbplatsmallar](/help/sites-cloud/administering/site-creation/site-templates.md) - Om du vill veta mer om strukturen för webbplatsmallar och hur de används för att skapa webbplatser läser du det här dokumentet.
