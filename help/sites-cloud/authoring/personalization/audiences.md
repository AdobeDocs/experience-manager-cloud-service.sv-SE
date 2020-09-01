---
title: Hantera målgrupper
description: Med Audiences-konsolen kan du skapa, ordna och hantera målgrupper för ditt Adobe Target-konto eller hantera segment för ContextHub
translation-type: tm+mt
source-git-commit: fee73b5f5ba69422494efe554ac5aa62c046ad86
workflow-type: tm+mt
source-wordcount: '975'
ht-degree: 11%

---


# Hantera målgrupper{#managing-audiences}

Med Audiences-konsolen kan du skapa, ordna och hantera målgrupper för ditt Adobe Target-konto eller hantera segment för ContextHub:

* Lägg till målgrupper - antingen Adobe Target målgrupper eller ContextHub-segment.
* Hantera målgrupper.

En Audience, som kallas *segment* i ContextHub, är en grupp besökare som definieras av specifika kriterier, som sedan avgör vem som ser en riktad aktivitet. När du riktar in dig på en aktivitet kan du antingen välja målgrupper direkt i målprocessen eller skapa nya i publikkonsolen.

I Audiences Console är målgrupperna ordnade efter varumärke.

Målgrupper är tillgängliga i målinriktat läge för [utveckling av riktat innehåll](/help/sites-cloud/authoring/personalization/targeted-content.md), där du också kan skapa målgrupper (men du måste skapa Adobe Target-målgrupper i publikkonsolen). Publiker som du skapar i målläge visas i publikkonsolen.

Publiken visas med en etikett som beskriver vilken typ av publik som definieras:

* CH - ContextHub-segment
* AT - Adobe Target

## Skapa ett ContextHub-segment i publikkonsolen {#creating-a-contexthub-segment-in-the-audiences-console}

Du kan skapa ett ContextHub-segment antingen i publikkonsolen eller under målinriktningsprocessen.

Så här skapar du ett ContextHub-segment i publikkonsolen:

1. In the Navigation console, click or tap **Personalization**. Klicka eller tryck på **Publiker**.
1. Tryck eller klicka på **Skapa ContextHub-segment**.

   ![Skapa ett segment](/help/sites-cloud/authoring/assets/audiences-create-segment.png)

1. Ange en titel i dialogrutan **Nytt ContextHub-segment** , justera förstärkningen och klicka på **Skapa**. Ditt nya ContextHub-segment visas i målgruppslistan.

   >[!NOTE]
   >
   >Du kan sortera den ändrade listan genom att trycka eller klicka på **Ändrad** och sortera i fallande ordning för att se alla nya målgrupper.

Mer information om hur du skapar segment med ContextHub finns i Configuring Segmentation with ContextHub-dokumentationen. <!--For further detail about creating segments using ContextHub, please see the [Configuring Segmentation with ContextHub](/help/sites-administering/segmentation.md) documentation.-->

## Skapa en Adobe Target-publik med hjälp av Audience Console {#creating-an-adobe-target-audience-using-the-audience-console}

Du kan skapa Adobe Target-målgrupper direkt i AEM med hjälp av publikkonsolen.

Målgrupper definieras av regler som bestämmer vem som ingår i en målaktivitet. En målgruppsdefinition kan innehålla flera regler och varje regel kan innehålla flera parametrar.

När du använder mer än en regel kombineras dessa regler av operatorn AND, vilket innebär att alla potentiella målgruppsmedlemmar måste uppfylla alla definierade villkor som ska inkluderas i aktiviteten. Om du till exempel definierar en OS-regel OCH en webbläsarregel inkluderas endast besökare som använder både det definierade operativsystemet OCH den definierade webbläsaren i aktiviteten.

>[!NOTE]
>
>Om du inte ser **Skapa målgrupp** på menyn **Skapa** har du inte de behörigheter som krävs för att skapa en målgrupp. Du måste ha skrivbehörighet för `/etc/segmentation` för att kunna skapa målgrupper. Gruppens innehållsförfattare har skrivbehörighet som standard.

Så här skapar du en Adobe Target-publik:

1. In the Navigation console, click or tap **Personalization**. Klicka eller tryck på **Publiker**.

   ![Navigera till målgrupper](/help/sites-cloud/authoring/assets/audiences-navigation.png)

1. I publikkonsolen: tryck eller klicka på **Skapa** och sedan **Skapa målpublik**.

   ![Skapa en målgrupp](/help/sites-cloud/authoring/assets/audiences-create-target.png)

1. I dialogrutan **Adobe Target-konfiguration** väljer du målkonfiguration och trycker eller klickar på **OK**.
1. I området Regel#1 trycker eller klickar du på attributtypen och anger eventuell attributinformation i fälten som är tillgängliga. När du är klar markerar du kryssrutan till höger om attributet för att spara det. Mer information om alla attribut finns i [Attribut och deras alternativ](#attributes-and-their-options) .
1. Klicka på **Lägg till regel** för att lägga till en regel. Ange så många regler som behövs. Reglerna kombineras med den booleska operatorn AND, vilket innebär att målgruppen måste uppfylla alla krav i alla regler för att kunna delta i en aktivitet.
1. Tryck eller klicka på **Nästa**.
1. Ange ett namn för målgruppen och tryck eller klicka på **Spara**.
1. Tryck eller klicka på **Spara**. Din publik listas i målgruppslistan.

### Attribut och deras alternativ {#attributes-and-their-options}

Du kan skapa målregler för följande attribut:

| **Attribut** | **Beskrivning** | **Mer information** |
|---|---|---|
| **Mobil** | Rikta mobila enheter baserat på parametrar som mobil enhet, typ av enhet, enhetsleverantör, skärmdimensioner (i pixlar) med mera. | Läs [Mobile-dokumentationen](https://docs.adobe.com/content/help/en/target/using/audiences/create-audiences/categories-audiences/mobile.html) på Adobe Target. |
| **Anpassat** | Egna parametrar är mbox-parametrar. Om du skickar några mbox-parametrar till mboxes, eller använder funktionen targetPageParams, visas de parametrarna här för användning i målgrupper. | Läs dokumentationen [om](https://docs.adobe.com/content/help/en/target/using/audiences/create-audiences/categories-audiences/custom-parameters.html) anpassade parametrar på Adobe Target. |
| **OS** | Du kan rikta in dig på besökare som använder ett visst operativsystem. | Användare som använder Linux, Macintosh eller Windows. |
| **Webbplatssidor** | Rikta in dig på besökare som befinner sig på en viss sida eller har en viss mbox-parameter. | Se [Dokumentation](https://docs.adobe.com/content/help/en/target/using/audiences/create-audiences/categories-audiences/site-pages.html) för webbplatssidor på Adobe Target. |
| **Webbläsare** | Du kan rikta in dig på användare som använder en viss webbläsare eller särskilda webbläsaralternativ när de besöker sidan. | Se dokumentationen [för](https://docs.adobe.com/help/en/target/using/audiences/create-audiences/categories-audiences/browser.html) webbläsaralternativ på Adobe Target. |
| **Besökarprofil** | Rikta besökarna mot specifika profilparametrar. | Se [Dokumentation](https://docs.adobe.com/content/help/en/target/using/audiences/visitor-profiles/visitor-profile.html) om besöksprofiler på Adobe Target. |
| **Trafikkällor** | Rikta besökarna baserat på den sökmotor eller landningssida som hänvisar dem till er webbplats. | Se [dokumentationen](https://docs.adobe.com/content/help/en/target/using/audiences/create-audiences/categories-audiences/traffic-sources.html) om trafikkällor på Adobe Target. |

## Ändra en publik i publikkonsolen {#modifying-an-audience-in-the-audiences-console}

>[!NOTE]
>
>Du kan bara redigera Adobe Target-målgrupper som har skapats i samma AEM som du redigerar. Målgrupper som skapats i olika AEM kan inte redigeras.

Du kan redigera alla ContextHub-målgrupper från publikkonsolen. Du kan också redigera Adobe Target-målgrupper, men bara de som har skapats i AEM:

1. In the Navigation console, click or tap **Personalization**. Klicka eller tryck på **Publiker**.
1. Tryck eller klicka på ikonen bredvid det ContextHub-segment som du vill redigera och tryck eller klicka på **Redigera**.
1. Gör eventuella redigeringar i segmentredigeraren. Mer information finns i ContextHub-dokumentationen. <!--See the [ContextHub](/help/sites-administering/contexthub-config.md) documentation for more information.-->
