---
title: Hantera modeller för innehållsfragment
description: Lär dig hur du hanterar modeller för innehållsfragment. Dessa fungerar som en grund för dina innehållsfragment i AEM och gör att du kan skapa strukturerat innehåll som ska användas för rubrikfri leverans eller sidredigering.
feature: Content Fragments
role: User, Developer, Architect
solution: Experience Manager Sites
exl-id: f94f75c2-12fa-47c0-a71b-327f4210077d
source-git-commit: b8a56b73f8178c432941b50821be91777f203dec
workflow-type: tm+mt
source-wordcount: '2288'
ht-degree: 0%

---

# Hantera modeller för innehållsfragment {#managing-content-fragment-models}

Från konsolen Innehållsfragment kan du hantera dina modeller för innehållsfragment och sedan [öppna redigeraren](/help/sites-cloud/administering/content-fragments/content-fragment-models.md) för att definiera strukturen.

Content Fragment Models i Adobe Experience Manager (AEM) as a Cloud Service definierar strukturen för innehållet i dina [Content Fragments](/help/sites-cloud/administering/content-fragments/overview.md). Dessa fragment kan sedan användas som grund för ditt headless-innehåll eller för att skapa sidor.

>[!IMPORTANT]
>
>Olika funktioner i Content Fragment Console är tillgängliga via Early Adobe Program.
>
>Kontrollera [Versionsinformation](/help/release-notes/release-notes-cloud/release-notes-current.md) om du vill se status och hur du tillämpar den om du är intresserad.

>[!NOTE]
>
>Den här sidan täcker den del av konsolen som (endast) visar modeller för innehållsfragment. För andra paneler, se:
>
>* [Hantera innehållsfragment](/help/sites-cloud/administering/content-fragments/managing.md)
>* [Visa och hantera Assets i konsolen för innehållsfragment](/help/sites-cloud/administering/content-fragments/assets-content-fragments-console.md)

>[!NOTE]
>
>Innehållsfragment lagras som **Assets**. Modeller för innehållsfragment hanteras primärt från konsolen **Innehållsfragment**, men kan även hanteras från konsolen [Assets](/help/assets/content-fragments/content-fragments-managing.md) och det alternativ [Modeller för innehållsfragment](/help/assets/content-fragments/content-fragments-models.md) som är tillgängligt från **Verktyg** - **Allmänt** .

## Så här arbetar du med modeller för innehållsfragment {#how-to-work-with-content-fragment-models}

En mycket snabb översikt om hur du arbetar med Content Fragment Models:

1. [Aktivera funktionen Content Fragment Model för instansen](/help/sites-cloud/administering/content-fragments/setup.md)
1. [Skapa](#creating-a-content-fragment-model) din innehållsfragmentmodell.
   * Nu kan du även **aktivera** modellen (som kan användas när du skapar innehållsfragment).
1. [Definiera](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#defining-your-content-fragment-model) modellens struktur.
1. [Aktivera innehållsfragmentmodellen](#enabling-a-content-fragment-model) om det inte redan är gjort.
1. [Tillåt dina modeller för innehållsfragment i de nödvändiga Assets-mapparna](#allowing-content-fragment-models-assets-folder) genom att konfigurera **Profiler**.

## Grundläggande struktur och hantering av modeller för innehållsfragment i konsolen {#basic-structure-handling-content-fragment-models-console}

Du kan använda panelen längst till vänster i konsolen [Innehållsfragment](/help/sites-cloud/administering/content-fragments/overview.md#content-fragments-console) för att välja **Modeller för innehållsfragment** som resurstyp för att visa, bläddra och hantera:

![Konsolen för innehållsfragment - navigering](/help/sites-cloud/administering/content-fragments/assets/cf-console-models-navigation.png)

Då öppnas vyn för Content Fragment Models:

![Konsolen för innehållsfragment - Hantera modeller för innehållsfragment](assets/cf-managing-content-fragment-models.png)

Här ser du att det finns tre huvudområden:

* Det övre verktygsfältet
   * Tillhandahåller AEM standardfunktioner
   * Visar även din IMS-organisation
   * Tillhandahåller olika [åtgärder](#actions-unselected)
* Den vänstra panelen
   * Visar [sökvägarna till alla konfigurationer](/help/sites-cloud/administering/content-fragments/setup.md#enable-content-fragment-functionality-configuration-browser) som listas som mappar
   * Här kan du dölja eller visa mappträdet
   * Du kan välja en specifik mapp i trädet
   * Storleken kan ändras för att visa kapslade mappar (underkonfigurationer)
   * Förutom modeller för innehållsfragment kan du visa [innehållsfragment](/help/sites-cloud/administering/content-fragments/managing.md) eller [Assets](/help/sites-cloud/administering/content-fragments/assets-content-fragments-console.md). Du kan även komprimera, eller expandera, länkar till panelerna
* Den högra panelen - härifrån kan du:
   * Se listan över alla modeller för innehållsfragment som finns i den valda mappen:
      * Modeller för innehållsfragment från den valda mappen och alla undermappar visas:
         * Platsen anges av vägbeskrivningarna. Dessa kan även användas för att ändra platsen:
      * [Information om varje modell visas](#information-content-fragment-models)
         * [Du kan välja vilka kolumner som ska visas](#select-columns-console)
      * [Olika fält med information](#information-content-fragment-models) om en modell för innehållsfragment innehåller länkar. Beroende på fältet kan dessa:
         * Öppna lämplig modell i redigeraren
         * Visa information om sökvägen till konfigurationen
         * Visa information om modellens status
      * [Vissa andra fält med information](#information-content-fragments) om en innehållsfragmentmodell kan användas för [Snabb filtrering](#fast-filtering):
         * Markera ett värde i kolumnen så tillämpas det omedelbart som ett filter
         * Snabb filtrering stöds för kolumnerna **Ändrad av**, **Publicerad av** och **Status**.s
      * Genom att använda musen på kolumnrubrikerna visas en listruta med åtgärdsväljare och breddreglage. Med dessa kan du:
         * Sortera - välj lämplig åtgärd för antingen stigande eller fallande
Då sorteras hela tabellen efter den kolumnen. Sortering är bara tillgängligt för lämpliga kolumner.
         * Ändra storlek på kolumnen med antingen funktionsmakrot eller breddreglagen
      * Välj en eller flera modeller för ytterligare [åtgärd](#actions-selected-content-fragment-models)
   * Öppna [filterpanelen](#filter-content-fragment-models)
   * Det finns ett urval av [kortkommandon](/help/sites-cloud/administering/content-fragments/keyboard-shortcuts.md) som kan användas i den här konsolen

## Information om dina modeller för innehållsfragment {#information-content-fragment-models}

Huvudpanelen/den högra panelen (tabellvyn) i konsolen innehåller en rad information om dina modeller för innehållsfragment. Vissa objekt har också direkta länkar till ytterligare åtgärder och/eller information:

* **Namn**
   * Tillhandahåller en länk för att öppna modellen i redigeraren.
* Låst
   * När modellen är låst visas den med en hänglåsikon.
* **Sökväg**
   * Anger sökvägen som en länk för att öppna konfigurationen i konsolen.
Vid hovring över mappnamnet visas JCR-sökvägen.
* **Status**
   * Endast information.
   * Kan användas för [snabb filtrering](#fast-filtering)
* **Ändrad**
   * Endast information.
* **Ändrad av**
   * Endast information.
   * Kan användas för [snabb filtrering](#fast-filtering).
* **Taggar**
   * Endast information.
   * Visar alla taggar som är relaterade till modellen.
   * Kan användas för [snabb filtrering](#fast-filtering).
* **Publicerad**
   * Endast information.
* **Publicerad av**
   * Endast information.
   * Kan användas för [snabb filtrering](#fast-filtering).

## Modegenskaper {#model-properties}

När du väljer en viss modell visas modellens egenskaper (som de definieras när [modellen skapas](#creating-a-content-fragment-model)). Om modellen inte är **låst** kan vissa objekt uppdateras. Du kan också använda informationsikonen (bredvid modellen **Title**) för att öppna och stänga den här informationspanelen.

![Konsolen för innehållsfragment - Information för en vald modell för innehållsfragment](assets/cf-managing-content-fragment-models-selected.png)

* **[Sökväg](/help/sites-cloud/administering/content-fragments/setup.md#enable-content-fragment-functionality-configuration-browser)**
* **[Status](#enabling-a-content-fragment-model)**
* **Titel**
* **Taggar**
* **Beskrivning**
* **Förhandsgranska URL-mönster**

  Med Content Fragment Models kan författare **Förhandsgranska** sitt innehåll i ett externt klientprogram. När **förhandsgranskningstjänsten** har konfigurerats lägger du till URL:en för klientprogrammet.

  URL:en för förhandsgranskning bör följa detta mönster:
    `https://<preview_url>?param=${expression}`

  Tillgängliga uttryck är:

   * `${contentFragment.path}`
   * `${contentFragment.model.path}`
   * `${contentFragment.model.name}`
   * `${contentFragment.variation}`
   * `${contentFragment.id}`

<!-- CHECK: currently under FT -->
<!--
* **GraphQL**
  Define names relevant for GraphQL.
  Changing the GraphQL API Name, or Query field names will impact client applications.
  * **API Name**
    Represents the GraphQL type and query field names in the GraphQL schema.
  * **Single Query Field Name**
    Represents the GraphQL single query field name in the GraphQL schema.
  * **Multiple Query Field Name**
    Represents the GraphQL multiple query field name in the GraphQL schema.
-->

## Åtgärder {#actions}

När du har markerat en mapp (i den vänstra panelen) finns det en rad åtgärder som du kan använda, antingen direkt eller efter att du har valt en viss modell:

* Olika åtgärder är direkt [tillgängliga från konsolen](#actions-unselected)
* Du kan [välja en eller flera innehållsfragmentmodeller för att visa lämpliga åtgärder](#actions-selected-content-fragment)

### Åtgärder (omarkerade) {#actions-unselected}

Vissa åtgärder är tillgängliga från konsolen - efter att du har valt en mapp, men utan att välja en specifik modell för innehållsfragment:

* **[Skapa](#creating-a-content-fragment-model)** en ny (tom) modell

### Åtgärder för en innehållsfragmentmodell i konsolen för innehållsfragment {#actions-selected-content-fragment-models}

Om du väljer en viss modell öppnas ett verktygsfält som fokuserar på de åtgärder som är tillgängliga för den modellen. Du kan också välja flera modeller - de tillgängliga åtgärderna justeras därefter.

* **[Redigera](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)** om du vill definiera innehållsfragmentmodellen.
* **Publicera** på nivåerna [Publicera](/help/implementing/cloud-manager/manage-environments.md#environment-types) eller [Förhandsgranska](/help/implementing/cloud-manager/manage-environments.md#access-preview-service).
* **Lås**/**Lås upp** för att kontrollera om en användare får ändra modellen.
* **[Aktivera](#enabling-a-content-fragment-model)**/**[Inaktivera](#disabling-a-content-fragment-model)** för att kontrollera om en användare får skapa innehållsfragment baserat på den här modellen.

Om du väljer en enskild modell visas även [modellegenskaperna](#properties) i den högra panelen.

## Markera kolumner som visas i konsolen {#select-columns-console}

Precis som med andra konsoler kan du konfigurera de kolumner som är synliga och tillgängliga för åtgärder:

![Konsolen för innehållsfragment - kolumnkonfiguration](assets/cf-managing-console-column-icon.png)

Här visas en lista med kolumner som du kan dölja eller visa:

![Konsolen för innehållsfragment - kolumnkonfiguration](assets/cf-managing-content-fragment-models-column-selection.png)

## Filtrera fragmentmodeller för innehåll {#filter-content-fragment-models}

På panelen Filter finns:

* Ett urval av prediater.
   * inklusive statusfält, taggar, användare med flera
   * ett eller flera predikat kan markeras och kombineras för att skapa filtret

<!--
* the opportunity to **Save** your filter
* the option to retrieve a saved search filter for reuse
-->

När du har valt alternativet **Filtrera efter** visas alternativen (högst upp på huvudpanelen). De kan avmarkeras därifrån. Till exempel:

![Konsolen för innehållsfragment - filtrera modeller för innehållsfragment](assets/cf-managing-content-fragment-models-filter.png)

### Snabb filtrering {#fast-filtering}

Du kan också välja ett predikat genom att klicka på ett visst kolumnvärde i listan. Du kan välja ett eller flera värden för att kombinera predikat.

Välj till exempel **Aktiverad** i kolumnen **Status**. När du har valt det här alternativet visas det som ett filterpredikat och listan filtreras därefter.

>[!NOTE]
>
>Snabb filtrering stöds bara för kolumnerna **Status**, **Ändrad av**, **Taggar** och **Publicerad av**.

>[!NOTE]
>
>Snabb filtrering fungerar på samma sätt som för [innehållsfragment](/help/sites-cloud/administering/content-fragments/managing.md#fast-filtering) i konsolen.

## Skapa en innehållsfragmentmodell {#creating-a-content-fragment-model}

1. Navigera till den mapp som passar din [konfiguration eller underkonfiguration](/help/sites-cloud/administering/content-fragments/setup.md).
1. Använd **Skapa** för att öppna dialogrutan.

   >[!CAUTION]
   >
   >Alternativet **Skapa** är bara tillgängligt:
   >
   >* Om [användningen av Content Fragment Models har aktiverats](/help/sites-cloud/administering/content-fragments/setup.md)
   >* när du har valt den mapp där du vill skapa modellen.

1. Markera **sökvägen** till konfigurationen och ange **namnet**.

   >[!NOTE]
   >
   >Konfigurationen fylls i automatiskt med den aktuella konfigurationen (mappen du befinner dig i).
   >
   >Du kan också ändra konfigurationen genom att klicka på mappikonen.

   Du kan också definiera olika egenskaper:

   * **Titel**
Om du anger **Title** först genereras **Name** utifrån det.
   * en **beskrivning**
   * **Aktivera modellen** för att [aktivera modellen](#enabling-disabling-a-content-fragment-model)

   >[!NOTE]
   >
   >Mer information finns i [Modell för innehållsfragment - Egenskaper](#model-properties).

   ![Titel och beskrivning](assets/cf-managing-content-fragment-models-create.png)

1. Använd **Skapa** om du vill spara den tomma modellen eller **Skapa och öppna**.

### Aktivera en innehållsfragmentmodell {#enabling-a-content-fragment-model}

När en modell har skapats måste den aktiveras så att den:

* Kan markeras när du skapar ett innehållsfragment.
* Kan refereras inifrån en innehållsfragmentmodell.
* Är tillgängligt för GraphQL, så schemat genereras.

Du kan **aktivera** en modell:

* När en ny modell skapas
   * Ett alternativ visas i dialogrutan.
* När en modell specifikt har **inaktiverats**
   * När den obligatoriska modellen har valts är åtgärden **Aktivera** tillgänglig i det övre verktygsfältet.

### Inaktivera en innehållsfragmentmodell {#disabling-a-content-fragment-model}

En modell kan också inaktiveras så att:

* Modellen är inte längre tillgänglig som grund för att skapa *nya* innehållsfragment.
* Men:
   * GraphQL-schemat fortsätter att genereras och är fortfarande frågningsbart (för att inte påverka JSON-API:t).
   * Alla innehållsfragment som är baserade på modellen kan fortfarande efterfrågas och returneras från GraphQL slutpunkt.
* Det går inte att referera till modellen längre, men befintliga referenser behålls orörda och kan fortfarande läsas och returneras från GraphQL-slutpunkten.

Om du vill inaktivera en modell som är flaggad som **Aktiverad** använder du alternativet **Inaktivera** från:

* Det övre verktygsfältet när den obligatoriska modellen är markerad.

## Tillåt modeller för innehållsfragment i din Assets-mapp {#allowing-content-fragment-models-assets-folder}

Om du vill implementera innehållsstyrning kan du konfigurera **profiler** i Assets-mappen för att styra vilka innehållsfragmentmodeller som tillåts för att skapa fragment i den mappen.

>[!NOTE]
>
>Mekanismen liknar [tillåter sidmallar](/help/sites-cloud/authoring/page-editor/templates.md#allowing-a-template-author) för en sida och dess underordnade sidor i avancerade egenskaper för en sida.

Så här konfigurerar du **principer** för **Tillåtna modeller för innehållsfragment**:

1. Navigera och öppna **Egenskaper** för den Assets-mapp som krävs.

1. Öppna fliken **Profiler** där du kan konfigurera:

   * **Ärvd från`<folder>`**

     Principer ärvs automatiskt när nya underordnade mappar skapas. Principen kan konfigureras om (och arvet brytas) om undermappar måste tillåta modeller som skiljer sig från den överordnade mappen.

   * **Tillåtna modeller för innehållsfragment via sökväg**

     Flera modeller kan tillåtas.

   * **Tillåtna modeller för innehållsfragment efter tagg**

     Flera modeller kan tillåtas.

   ![Modellprincip för innehållsfragment](assets/cf-cfmodels-policy-assets-folder.png)

1. **Spara** eventuella ändringar.

De Content Fragment-modeller som tillåts för en mapp löses enligt följande:

* **Profiler** för **Tillåtna modeller för innehållsfragment**.
* Om den är tom kan du försöka identifiera principen med arvsreglerna.
* Om arvskedjan inte ger något resultat ska du titta på konfigurationen **Cloud Services** för den mappen (även först direkt och sedan via arv).
* Om inget av ovanstående ger några resultat finns det inga tillåtna modeller för den mappen.

<!--
## Deleting a Content Fragment Model {#deleting-a-content-fragment-model}

>[!CAUTION]
>
>Deleting a Content Fragment model can impact dependent fragments.

To delete a Content Fragment model:

1. Navigate to, and select your Content Fragment Model. You can select multiple models.

1. Select **Delete** from the toolbar.

   >[!NOTE]
   >
   >If the model is referenced a warning is given, so that you can take appropriate action.
-->

## Publicera en innehållsfragmentmodell {#publishing-a-content-fragment-model}

Content Fragment Models måste publiceras när/innan beroende Content Fragments publiceras.

Så här publicerar du en innehållsfragmentmodell:

1. Navigera till och markera innehållsfragmentmodellen. Du kan välja flera modeller.

1. Välj **Publicera** i verktygsfältet.

1. I dialogrutan Publicera väljer du **Mål**:

   * **Publiceringstjänst**
   * **Förhandsgranskningstjänst**

1. Arbetsflödet för publicering av de valda modellerna och deras referenser startas. Publiceringsstatusen visas sedan i konsolen.

<!--
## Unpublishing a Content Fragment Model {#unpublishing-a-content-fragment-model}

Content Fragment Models can be unpublished if they are not referenced by any fragments.

To unpublish a Content Fragment Model:

1. Navigate to, and select your Content Fragment Model.
1. Select **Unpublish** from the toolbar.
   The published status is indicated in the console. 

If you try to unpublish a model that is currently used by one or more fragments, then an error warning is shown. For example: 

![Content Fragment Model error message when unpublishing a model that is in use](assets/cf-cfmodels-unpublish-error.png)

The message suggests that you check the [References](/help/sites-cloud/authoring/basic-handling.md#references) panel to investigate further:

![Content Fragment Model in References](assets/cf-cfmodels-references.png)
-->

## Låsta modeller för innehållsfragment {#locked-content-fragment-models}

Med den här funktionen kan du styra om en modell kan uppdateras, men den tillhandahåller även styrning för publicerade modeller för innehållsfragment.

### Utmaningen {#the-challenge}

* Content Fragment Models bestämmer schemat för GraphQL-frågor i AEM.

   * AEM GraphQL-scheman skapas så snart en Content Fragment Model skapas, och de kan finnas både i skribent- och publiceringsmiljöer.

   * Publiceringsscheman är de viktigaste eftersom de utgör grunden för leverans av innehåll i innehållsfragment i JSON-format.

* Problem kan uppstå när modeller för innehållsfragment ändras, eller med andra ord redigeras. Det innebär att schemat ändras, vilket i sin tur kan påverka befintliga GraphQL-frågor.

* Att lägga till nya fält i en innehållsfragmentmodell bör (vanligtvis) inte ha några skadliga effekter. Om du ändrar befintliga datafält (t.ex. namn) eller tar bort fältdefinitioner kommer befintliga GraphQL-frågor att brytas när de begär dessa fält.

### Krav {#the-requirements}

* Att göra användarna medvetna om riskerna vid redigering av modeller som redan används för leverans av direktsänt innehåll, med andra ord, modeller som har publicerats).

* För att undvika oönskade ändringar.

Något av dessa villkor kan göra att frågor bryts om de ändrade modellerna publiceras på nytt.

### Lösningen {#the-solution}

För att åtgärda dessa problem är Content Fragment Models *låst* i READ-ONLY-läge när de har skapats - så snart de har publicerats. Den här statusen anges av **Låst**.

När modellen är **Låst** (i läget SKRIVSKYDDAD) kan du se innehållet och strukturen för modellerna, men du kan inte redigera dem.

Du kan hantera **låsta** modeller från konsolen eller modellredigeraren:

* Konsol

  Från konsolen kan du hantera läget SKRIVSKYDDAT med åtgärderna **Lås upp** och **Lås** i verktygsfältet.

   * Du kan **Lås upp** en modell om du vill aktivera redigeringar.

     Om du väljer **Lås upp** visas en varning och du måste bekräfta åtgärden **Lås upp**.

     Du kan sedan öppna modellen för redigering.

   * Du kan också **låsa** modellen i efterhand.
   * Om du publicerar om modellen återgår den omedelbart till läget **Låst** (SKRIVSKYDDAT).

* Modellredigerare

   * När du öppnar en låst modell får du en varning och tre åtgärder visas: **Avbryt**, **Visa skrivskyddad**, **Redigera**.

   * Om du väljer **Visa skrivskyddat** kan du se modellens innehåll och struktur.

   * Om du väljer **Redigera** kan du redigera och spara dina uppdateringar:

     ![Redigera - låst innehållsfragmentmodell](assets/cf-cfmodels-editor-locked-edit.png)

     >[!NOTE]
     >
     >Det kan fortfarande finnas en varning överst, men det är när modellen redan används av befintliga innehållsfragment.

   * **Avbryt** returnerar dig till konsolen.
