---
title: Skapa ett adaptivt formulär
description: Lär dig hur du skapar ett adaptivt formulär med [!DNL Experience Manager Forms]. Adaptiva Forms är responsiva HTML5-formulär som effektiviserar informationsinsamling och -bearbetning. Mer information om hur du skapar ett adaptivt formulär baserat på en formulärdatamodell och ett XML- eller JSON-schema.
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
exl-id: 1e812d93-4ba5-4589-b59b-2f564d754b0f
source-git-commit: 8ac35abd1335b4e31a6dc0d8812cc9df333e69a4
workflow-type: tm+mt
source-wordcount: '2174'
ht-degree: 0%

---

# Skapa ett adaptivt formulär {#creating-an-adaptive-form-core-components}

Med anpassningsbara Forms kan du skapa engagerande, responsiva, dynamiska och anpassningsbara formulär. AEM Forms har en användarvänlig guide för att snabbt skapa Adaptiv Forms. Guiden har en snabb fliknavigering där du enkelt kan välja förkonfigurerade mallar, format, fält och alternativ för att skicka formulär för att skapa ett adaptivt formulär.

Innan du börjar får du lära dig mer om vilken typ av Forms-komponenter du kan använda:

* [Adaptiva Forms Core-komponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=en): Dessa är standardiserade komponenter för datainhämtning. Dessa komponenter har anpassningsmöjligheter, kortare utvecklingstid och lägre underhållskostnader för era digitala registreringsupplevelser. En utvecklare kan enkelt anpassa och utforma dessa komponenter. Adobe rekommenderar att man utnyttjar dessa moderna och utbyggbara komponenter för att utveckla Adaptiv Forms.

* [Adaptiva Forms Foundation-komponenter](creating-adaptive-form.md): Dessa är klassiska (gamla) datainhämtningskomponenter. Du kan fortsätta att använda dessa för att redigera dina befintliga grundläggande komponentbaserade adaptiva formulär. Om du skapar nya formulär rekommenderar Adobe att du använder  [Adaptiva Forms Core-komponenter](creating-adaptive-form-core-components.md) för att skapa en adaptiv Forms.

![Guide för att skapa ett adaptivt formulär](/help/release-notes/assets/wizard.png)


## Krav

Du behöver följande för att skapa ett adaptivt formulär:

* **Aktivera adaptiva Forms Core-komponenter för din miljö**: När du skapar ett nytt program är de adaptiva Forms Core-komponenterna redan aktiverade för din miljö. Om du har en as a Cloud Service Forms-miljö baserad på Archetype 39 eller tidigare, [Aktivera adaptiva Forms Core-komponenter för din miljö](enable-adaptive-forms-core-components.md). När du aktiverar kärnkomponenterna för din miljö, **Adaptiv Forms (kärnkomponent)** mall- och arbetsytetemat läggs till i din miljö. Om din AEM SDK-version är äldre än 2023.02.0, [se till att du har `prerelease` flagga aktiverad i din miljö](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/release-notes/prerelease.html?lang=en#new-features) som adaptiva Forms Core Components ingick i förleasingen före version 2023.02.0.

* **En anpassad formulärmall**: En mall innehåller en grundläggande struktur och definierar utseendet (layouter och format) för ett adaptivt formulär. Den har förformaterade komponenter som innehåller vissa egenskaper och innehållsstruktur. Här finns också alternativ för att definiera ett tema och en skicka-åtgärd. Temat definierar utseendet, känslan och skickaåtgärden definierar vilken åtgärd som ska vidtas när ett adaptivt formulär skickas in. Du kan till exempel skicka insamlade data till en datakälla. Molntjänsten tillhandahåller en OOTB-mall med namnet blank:

   * The `blank` -mallar ingår i alla nya as a Cloud Service AEM Forms-program.
   * Du kan installera referenspaketet via Package Manager för att lägga till `blank` till ditt as a Cloud Service AEM Forms-program.
   * Du kan också [skapa en ny adaptiv Forms-mall (kärnkomponenter)](template-editor.md) från scratch.

* **Ett adaptivt formulärtema**: Ett tema innehåller formatinformation för komponenterna och panelerna. Format innehåller egenskaper som bakgrundsfärger, lägesfärger, genomskinlighet, justering och storlek. När du använder ett tema återspeglas det angivna formatet i motsvarande komponenter.  The `Canvas` -mallar ingår i alla nya as a Cloud Service AEM Forms-program.
  <!-- * You can install the reference package, via package manager, to add the `Canvas` template to your AEM Forms as a Cloud Service program.
    * You can also [create a new Adaptive Forms theme (Core Components)](template-editor.md) and deploy it to your AEM Forms as a Cloud Service program. -->

* **Behörigheter**: Lägg till dina användare i [!DNL forms-users] grupp. Medlemmarna i [!DNL forms-users] gruppen har behörighet att skapa ett adaptivt formulär. En detaljerad lista över formulärspecifika användargrupper finns i [Grupper och behörigheter](forms-groups-privileges-tasks.md).


## Skapa ett adaptivt formulär  {#create-an-adaptive-form-core-components}

1. Logga in på [!DNL Experience Manager Forms] Författarinstans. Det kan vara en molninstans eller en lokal utvecklingsinstans.

1. Ange dina uppgifter på inloggningssidan för Experience Manager. När du är inloggad trycker du på **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]**.

1. Tryck på **[!UICONTROL Create]**  > **[!UICONTROL Adaptive Forms]**. Guiden öppnas. Välj en mall på fliken Källa:

   ![Kärnkomponentmall](/help/forms/assets/core-components-template.png)

   När du väljer en mall väljs automatiskt ett tema och en skicka-åtgärd som anges i mallen, och **[!UICONTROL Create]** knappen är aktiverad. Du kan gå till **[!UICONTROL Style]** eller **[!UICONTROL Submission]** för att välja ett annat tema eller skicka-åtgärd. Om den valda mallen inte anger något tema förblir knappen Skapa inaktiverad. Du kan gå till **[!UICONTROL Styles]** om du vill välja ett tema manuellt.

   >[!NOTE]
   >
   >
   > Om du inte har det, **Adaptiv Forms (kärnkomponent)** mallar i din miljö, [Aktivera adaptiva Forms Core-komponenter för din miljö](setup-local-development-environment.md#enable-adaptive-forms-core-components-for-an-existing-aem-archetype-based-project). När du aktiverar kärnkomponenterna för din miljö, **Adaptiv Forms (kärnkomponent)** -mallen läggs till i din miljö.

1. I **[!UICONTROL Style]** väljer du ett tema:

   * När den valda mallen anger ett tema väljs temat automatiskt i guiden. Du kan också välja ett annat tema på fliken Format.

   * Om den valda mallen inte anger något tema kan du använda fliken Format för att välja ett tema. The **[!UICONTROL Create]** knappen aktiveras först när ett tema har valts.

1. (Valfritt) Välj en datamodell på fliken Data:

   * **Formulärdatamodell**: A [Formulärdatamodell](data-integration.md) Med kan ni integrera enheter och tjänster från olika datakällor i ett adaptivt formulär. Välj Formulärdatamodell om det adaptiva formulär du skapar inbegriper att hämta och skriva data från och till flera datakällor.

   * **JSON-schema**: [JSON-schema](adaptive-form-json-schema-form-model.md) Vår Core-Components-baserade adaptiva form möjliggör smidig integrering med företagets back-end-system genom att ge möjlighet att associera ett JSON-schema, som representerar strukturen för de data som produceras eller konsumeras. Den här kopplingen gör det möjligt för författare att dynamiskt lägga till innehåll i det adaptiva formuläret med elementen i schemat. Elementen i schemat är enkelt tillgängliga på fliken Datamodellsobjekt i innehållsläsaren under redigeringsprocessen, och alla fält läggs automatiskt till i alla nya adaptiva formulär.

   Som standard markeras alla fält i det associerade JSON-schemat automatiskt och konverteras till motsvarande adaptiva formulärkomponenter, vilket effektiviserar redigeringsprocessen. I guiden kan du välja vilka fält som ska inkluderas i det anpassade formuläret med hjälp av kryssrutor.

1. I **[!UICONTROL Submission]** väljer du en Skicka-åtgärd:

   * När du väljer en mall markeras åtgärden Skicka som anges i mallen automatiskt. Du kan välja en annan skickaåtgärd på fliken Skicka. The **[!UICONTROL  Submission]** på -fliken visas alla tillgängliga skicka-åtgärder.

   * När den valda mallen inte anger någon skicka-åtgärd kan du använda **[!UICONTROL Submission]** flik för att välja en skicka-åtgärd

1. (Valfritt) I dialogrutan **[!UICONTROL Delivery]** kan du ange ett publicerings- eller avpubliceringsdatum för ett adaptivt formulär.

1. Tryck på **[!UICONTROL Create]**. En dialogruta där du kan ange namn, namn och plats för att spara det adaptiva formuläret visas:

   * **[!UICONTROL Title]** Anger formulärets visningsnamn. Titeln hjälper dig att identifiera formuläret i [!DNL Experience Manager Forms] användargränssnitt.
   * **[!UICONTROL Name:]** Anger formulärets namn. En nod med det angivna namnet skapas i databasen. När du börjar skriva en titel genereras värdet för namnfältet automatiskt. Du kan ändra det föreslagna värdet. Namnfältet får endast innehålla alfanumeriska tecken, bindestreck och understreck. Alla ogiltiga indata ersätts med ett bindestreck.
   * **[!UICONTROL Path:]** Anger platsen där det adaptiva formuläret ska sparas. Du kan spara det anpassade formuläret direkt på `/content/dam/formsanddocuments` eller skapa en mapp som `/content/dam/formsanddocuments/adaptiveforms` för att spara ett adaptivt formulär. Se till att du skapar mappen innan du använder den i sökvägen. The **[!UICONTROL Path]** skapas ingen mapp automatiskt.

1. Tryck på **[!UICONTROL Create]**. Ett adaptivt formulär skapas och öppnas i den adaptiva Forms-redigeraren. Redigeraren visar det innehåll som är tillgängligt i mallen.  Baserat på typen av adaptiv form finns formulärelementen i den associerade <!--XFA form template, XML schema or --> JSON-schema eller formulärdatamodell visas i **[!UICONTROL Data Model Objects]** -fliken i **[!UICONTROL Content Browser]** i sidlisten. Du kan också dra och släppa dessa element för att skapa ett anpassat formulär.

Nu kan du dra och släppa [Adaptiva Forms Core-komponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) till Adaptiv Forms-behållare för att utforma och skapa formuläret. Du kan också besöka [https://aemcomponents.dev/](https://aemcomponents.dev/) för att se hur de tillgängliga kärnkomponenterna fungerar i praktiken.

## Konfigurera åtgärden Skicka för ett anpassat formulär {#configure-submit-action-for-form}

Med en Skicka-åtgärd kan du välja målet för data som har hämtats via ett anpassat formulär. Den aktiveras när en användare klickar på knappen Skicka på ett anpassat formulär. Anpassade formulär innehåller några av de åtgärder som har vidtagits för att skicka in. Du kan också utöka en standardåtgärd för att skicka för att skapa en egen anpassad åtgärd. Så här konfigurerar du en Skicka-åtgärd för formuläret:

1. Öppna innehållsläsaren och välj **[!UICONTROL Guide Container]** i din adaptiva form.
1. Klicka på egenskaperna för stödlinjebehållaren ![Stödlinjeegenskaper](/help/forms/assets/configure-icon.svg) ikon. Dialogrutan Adaptiv formulärbehållare öppnas.

1. Klicka på  **[!UICONTROL Submission]** -fliken.

   ![Klicka på skiftningsikonen för att öppna dialogrutan Adaptiv formulärbehållare och konfigurera en sändningsåtgärd](/help/forms/assets/adaptive-forms-submit-message.png)

1. Välj och konfigurera en **[!UICONTROL Submit action]**, baserat på era behov. Mer information om Skicka åtgärder finns i [Inlämningsåtgärd för anpassat formulär](/help/forms/configuring-submit-actions.md)

<!--
    
    ![Click the Wrench icon to open Adaptive Form Container dialog box to configure Data Models for the Adaptive Form Container component](/help/forms/assets/adaptive-forms-container.png)

-->

## Dirigera om användaren till en sida eller visa ett tackmeddelande när formuläret skickas

När du skickar ett formulär kan du dirigera om användaren till en annan webbsida eller ett meddelande. Så här omdirigerar du användaren eller konfigurerar tackmeddelandet:

1. Öppna innehållsläsaren och välj **[!UICONTROL Guide Container]** i din adaptiva form.
1. Klicka på egenskaperna för stödlinjebehållaren ![Stödlinjeegenskaper](/help/forms/assets/configure-icon.svg) ikon. Dialogrutan Adaptiv formulärbehållare öppnas.
1. Öppna **[!UICONTROL Submission]** -fliken.

   ![Klicka på ikonen för skiftnyckel för att öppna dialogrutan Adaptiv formulärbehållare för att konfigurera en omdirigeringssida eller ett tack för ditt meddelande](/help/forms/assets/adaptive-forms-redirect-message.png)

   * Om du vill konfigurera en omdirigerings-URL för alternativet Skicka väljer du **[!UICONTROL Redirect to URL]** och bläddra och markera en AEM Sites-sida, eller ange en URL-adress för en extern sida.

   * Om du vill konfigurera ett anpassat meddelande eller ett tackmeddelande väljer du alternativet Skicka i **[!UICONTROL Show Message]** och skriv ett meddelande i **[!UICONTROL Message content]** box. Det är en RTF-ruta som du kan använda helskärmsalternativet för att visa alla tillgängliga RTF-objekt.

## Konfigurera ett schema eller en formulärdatamodell för ett anpassat formulär{#configure-schema-or-data-model-for-form}

Du kan använda formulärdatamodellen för att ansluta ett formulär till en datakälla för att skicka och ta emot data baserat på användaråtgärder. Du kan också ansluta ett formulär till ett JSON-schema för att ta emot skickade data i ett fördefinierat format. Beroende på behovet kan du ansluta formuläret till ett JSON-schema eller en formulärdatamodell:

* [Skapa ett JSON-schema och överför det till din miljö](/help/forms/adaptive-form-json-schema-form-model.md)
* [Skapa en formulärdatamodell](/help/forms/create-form-data-models.md)

### Konfigurera ett JSON-schema eller en formulärdatamodell för formuläret

Så här konfigurerar du ett JSON-schema eller en formulärdatamodell för formuläret:

1. Öppna innehållsläsaren och välj **[!UICONTROL Guide Container]** i din adaptiva form.
1. Klicka på egenskaperna för stödlinjebehållaren ![Stödlinjeegenskaper](/help/forms/assets/configure-icon.svg) ikon. Dialogrutan Adaptiv formulärbehållare öppnas.
1. Öppna **[!UICONTROL Data Model]** -fliken.

   ![Klicka på ikonen för skiftnyckel för att öppna dialogrutan Adaptiv formulärbehållare för att konfigurera ett JSON-schema eller en formulärdatamodell](/help/forms/assets/adaptive-forms-select-form-data-model-or-json-schema.png)

1. Välj och konfigurera ett JSON-schema eller en formulärdatamodell utifrån dina krav:

   * När du väljer **[!UICONTROL Form Model]** , använd **[!UICONTROL Select Form Data Model]** för att välja en förkonfigurerad formulärdatamodell.
   * När du väljer **[!UICONTROL Schema]** , använd **[!UICONTROL Schema]** för att välja ett JSON-schema för formuläret.

1. Klicka på **[!UICONTROL Done]**.

## Konfigurera en förifyllningstjänst  {#configure-prefill-service-for-form}

Du kan använda förifyllningstjänsten för att autofylla fält i ett adaptivt formulär med befintliga data. När en användare öppnar ett formulär är värdena för dessa fält förifyllda. Du kan:

* [Skapa en anpassad förifyllningstjänst](/help/forms/prepopulate-adaptive-form-fields.md)
* [Använd förifyllningstjänsten för formulärdatamodell](#fdm-prefill-service)

### Använd förifyllningstjänsten för formulärdatamodell för att fylla i fält i ett adaptivt formulär i förväg {#fdm-prefill-service}

Du kan använda förifyllningstjänsten för formulärdatamodell för att fylla i fält i ett adaptivt formulär i förväg med hjälp av en formulärdatamodell eller en anpassad förifyllningstjänst. Tjänsten för förifyllnad av formulärdatamodell använder [Hämta tjänst för konfigurerad formulärdatamodell](work-with-form-data-model.md#add-data-model-objects-and-services-add-data-model-objects-and-services) för att hämta data. Så här använder du förifyllningstjänsten för formulärdatamodell för ett adaptivt formulär:

1. Öppna innehållsläsaren och välj **[!UICONTROL Guide Container]** i din adaptiva form.
1. Klicka på egenskaperna för stödlinjebehållaren ![Stödlinjeegenskaper](/help/forms/assets/configure-icon.svg) ikon. Dialogrutan Adaptiv formulärbehållare öppnas.
1. Klicka på egenskaperna för den adaptiva formulärbehållaren ![Egenskaper för adaptiv formulärbehållare](/help/forms/assets/configure-icon.svg) ikon. Dialogrutan Adaptiv formulärbehållare öppnas för att konfigurera datamodeller.
   ![Klicka på ikonen för skiftnyckel för att öppna dialogrutan Adaptiv formulärbehållare för att konfigurera en omdirigeringssida eller ett tack för ditt meddelande](/help/forms/assets/adaptive-forms-container-prefill-service.png)
1. Välj en formulärdatamodell. Öppna **[!UICONTROL Basic]** -fliken. I förifyllningstjänsten väljer du **[!UICONTROL Form Data Model Prefill Service]**.
1. Klicka på **[!UICONTROL Done]**. Ditt adaptiva formulär har nu konfigurerats för att använda förifyllning av formulärdatamodell. Nu kan du använda [regelredigerare](rule-editor.md) för att skapa regler för förifyllning av formulärfält.

## Redigera formulärmodellegenskaper för ett adaptivt formulär {#edit-form-model}

1. Markera det adaptiva formuläret och tryck på ![Sidinformation](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL Open Properties]**. Sidan Formuläregenskaper öppnas.

1. Gå till **[!UICONTROL Form Model]** och välj en formulärmodell. Om det adaptiva formuläret inte har någon formulärmodell kan du välja antingen ett JSON-schema eller en formulärdatamodell. Om det adaptiva formuläret däremot redan är baserat på en formulärmodell kan du växla till en annan formulärmodell av samma typ. Om formuläret till exempel använder ett JSON-schema kan du enkelt växla till ett annat JSON-schema, och på samma sätt kan du växla till en annan formulärdatamodell om formuläret använder en formulärdatamodell.

1. Tryck **[!UICONTROL Save]** för att spara egenskaperna.


## Se nästa

* [Skapa stilar eller teman för formulären](using-themes-in-core-components.md)
* [Lägga till dynamiskt beteende i formulär med regelredigeraren](rule-editor.md)
* [Ange formulärlayout för olika skärmstorlekar och enhetstyper](/help/sites-cloud/authoring/features/responsive-layout.md)


## Relaterad artikel {#related-article}

* [Skapa en fristående grundkomponentbaserad adaptiv form](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form-core-components.html)
