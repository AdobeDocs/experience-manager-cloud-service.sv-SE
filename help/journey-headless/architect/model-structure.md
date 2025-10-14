---
title: Läs om hur du skapar innehållsfragmentmodeller i AEM
description: Lär dig mer om koncepten och mekanismerna i att modellera innehåll för din Headless CMS med Content Fragments Models.
exl-id: fdfa79d3-fbed-4467-a898-c1b2678fc0cb
solution: Experience Manager
feature: Headless, Content Fragments,GraphQL API
role: Admin, Architect, Developer
source-git-commit: 6306ad88b889197aff377dc0a72ea232cd76ff9c
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 0%

---

# Läs om hur du skapar innehållsfragmentmodeller i AEM {#architect-headless-content-fragment-models}

## Story hittills {#story-so-far}

I början av [AEM Headless Content Author &#x200B;](overview.md) innehöll [Grundläggande om innehållsmodellering för Headless med AEM](basics.md) grundläggande koncept och terminologi som är relevant för redigering utan rubrik.

Den här artikeln bygger på dessa principer så att du förstår hur du skapar egna modeller för innehållsfragment för AEM headless-projekt.

## Syfte {#objective}

* **Målgrupp**: Nybörjare
* **Mål**: koncept och mekanismer för att modellera innehåll för ditt Headless CMS med Content Fragments Models.

<!-- which persona does this? -->
<!-- and who allows the configuration on the folders? -->

<!--
## Enabling Content Fragment Models {#enabling-content-fragment-models}

At the very start you need to enable Content Fragment Models for your site, this is done in the Configuration Browser; under Tools > General > Configuration Browser. You can either select to configure the global entry, or create a configuration. For example:

![Define configuration](/help/sites-cloud/administering/content-fragments/assets/cfm-conf-01.png)

>[!NOTE]
>
>See Additional Resources - Content Fragments in the Configuration Browser
-->

## Skapa modeller för innehållsfragment {#creating-content-fragment-models}

Sedan kan du skapa modellerna för innehållsfragment och definiera strukturen.

1. På konsolen Innehållsfragment väljer du panelen för modeller för innehållsfragment.

1. Navigera till den mapp som passar din konfiguration eller underkonfiguration.

1. Använd **Skapa** för att öppna dialogrutan **Ny modell för innehållsfragment**.

   ![Titel och beskrivning](/help/sites-cloud/administering/content-fragments/assets/cf-managing-content-fragment-models-create.png)

1. Fyll i informationen

1. Använd **Skapa** om du vill spara den tomma modellen eller **Skapa och öppna**.

<!--
Then the Content Fragments Models can be created and the structure defined. This can be done under **Tools** > **General** > **Content Fragment Models**. 

![Content Fragment Models in Tools](assets/cfm-tools.png)

After selecting this you navigate to the location for your model and select **Create**. Here you can enter various key details.

The option **Enable model** is activated by default. This means that your model is available for use (in creating Content Fragments) as soon as you have saved it. You can deactivate this if you want - there are opportunities later to enable (or disable) an existing model.

![Create Content Fragment Model](/help/sites-cloud/administering/content-fragments/assets/cfm-models-02.png)

Confirm with **Create** and you can then **Open** your model to start defining the structure.
-->

## Definiera modeller för innehållsfragment {#defining-content-fragment-models}

När du först öppnar en ny modell visas ett stort tomt utrymme till vänster och en lång lista med **datatyper** till höger:

![Tom modell](/help/sites-cloud/administering/content-fragments/assets/cfm-models-03.png)

Så vad ska man göra?

Du kan dra instanser av **datatyperna** till vänster - du definierar redan modellen!

![Definierar fält](/help/sites-cloud/administering/content-fragments/assets/cfm-models-04.png)

När du har lagt till en datatyp måste du definiera **egenskaperna** för det fältet. Dessa egenskaper beror på vilken typ som används. Till exempel:

![Dataegenskaper](/help/sites-cloud/administering/content-fragments/assets/cfm-models-05.png)

Du kan lägga till så många fält du behöver. Till exempel:

![Modell för innehållsfragment](/help/sites-cloud/administering/content-fragments/assets/cfm-models-07.png)

### Dina innehållsförfattare {#your-content-authors}

Innehållsförfattarna kan inte se de faktiska datatyper och egenskaper som du har använt för att skapa modeller. Det innebär att du kan behöva ange hjälp och information om hur specifika fält fylls i. Grundläggande information får du om du använder fältetiketten och standardvärdet, men mer komplex ärendespecifik dokumentation kan behöva övervägas.

>[!NOTE]
>
>Se Ytterligare resurser - modeller för innehållsfragment.

## Hantera modeller för innehållsfragment {#managing-content-fragment-models}

<!-- needs more details -->

Hantera dina modeller för innehållsfragment inkluderar:

* Om du aktiverar (eller inaktiverar) dem blir de tillgängliga för författare när du skapar innehållsfragment.
* Borttagning - borttagning behövs alltid, men du måste vara medveten om att du tar bort en modell som redan används för innehållsfragment, särskilt fragment som redan är publicerade.

## Publicering {#publishing}

<!-- needs more details -->

Modeller för innehållsfragment måste publiceras när/innan beroende innehållsfragment publiceras.

>[!NOTE]
>
>Om en författare försöker publicera ett innehållsfragment för vilket modellen ännu inte har publicerats, visar en urvalslista detta och modellen publiceras med fragmentet.

Så snart en modell har publicerats är den *låst* i skrivskyddat läge vid författaren. Detta syftar till att förhindra ändringar som kan leda till fel i befintliga GraphQL-scheman och -frågor, särskilt i publiceringsmiljön. Den indikeras i konsolen av **Locked**.

När modellen är **Låst** (i SKRIVSKYDDAT läge) kan du se innehållet och strukturen för modeller, men du kan inte redigera dem direkt. Du kan dock hantera **låsta** modeller från antingen konsolen eller modellredigeraren.

## What&#39;s Next {#whats-next}

Nu när du har lärt dig grunderna är nästa steg att börja skapa egna modeller för innehållsfragment.

## Ytterligare resurser {#additional-resources}

* [Authoring Concepts](/help/sites-cloud/authoring/author-publish.md)

* [Grundläggande hantering](/help/sites-cloud/authoring/basic-handling.md) - Den här sidan är huvudsakligen baserad på konsolen **Platser**, men många/de flesta funktioner är också relevanta för att navigera till och vidta åtgärder på **modeller för innehållsfragment** under konsolen **Allmänt**.

* [Arbeta med innehållsfragment](/help/sites-cloud/administering/content-fragments/overview.md)

   * [Modeller för innehållsfragment](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md)

      * [Definiera innehållsfragmentmodellen](/help/sites-cloud/administering/content-fragments/content-fragment-models.md)

      * [Aktivera eller inaktivera en innehållsfragmentmodell](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#enabling-disabling-a-content-fragment-model)

      * [Tillåt modeller för innehållsfragment i din Assets-mapp](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#allowing-content-fragment-models-assets-folder)

      * [Ta bort en innehållsfragmentmodell](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#deleting-a-content-fragment-model)

      * [Publicera en innehållsfragmentmodell](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#publishing-a-content-fragment-model)

      * [Avpublicera en innehållsfragmentmodell](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#unpublishing-a-content-fragment-model)

      * [Låsta modeller för innehållsfragment](/help/sites-cloud/administering/content-fragments/managing-content-fragment-models.md#locked-content-fragment-models)

* Komma igång-guider

   * [Skapa rubrikfria innehållsfragmentsmodeller](/help/headless/setup/create-content-model.md)
