---
title: Redigera i kontext med den universella redigeraren
description: Upptäck hur du kan använda den universella redigeraren för att redigera olika delar av innehållet på plats och i sitt sammanhang i alla implementeringar.
hidefromtoc: true
index: false
exl-id: a4854a56-9434-4d15-a56a-f1798f27263a
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '969'
ht-degree: 0%

---


# Redigera i kontext med den universella redigeraren {#editing-in-context}

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_edit_inline_universal_editor"
>title="Redigera i kontext med den universella redigeraren"
>abstract="Se hur era headless-appar kan utnyttja den universella redigeraren för att ge dina författare lättanvända kontextredigeringar."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_edit_inline_universal_editor_guide"
>title="Starta den universella redigeraren"
>abstract="I den här guiden ska vi utforska den universella redigeraren och se hur den gör det möjligt för alla att redigera alla delar av ditt innehåll i alla implementeringar, vilket leder till förbättrad innehållshastighet.<br><br>Starta den här modulen på en ny flik genom att klicka nedan och följ sedan den här guiden."

>[!CONTEXTUALHELP]
>id="aemcloud_sites_trial_edit_inline_universal_editor_guide_footer"
>title="I den här modulen lärde du dig att anpassa innehåll i sitt sammanhang och på plats med den universella redigeraren."
>abstract=""

## Redigera text i kontext {#edit-text}

Redigering på plats och i sitt sammanhang kan ofta vara fördelaktigt jämfört med strukturerad redigering av headless-innehåll, som i Content Fragment-redigeraren, som du såg i tidigare moduler.

>[!NOTE]
>
>Om du vill använda den universella redigeraren i den här testversionen måste du använda Chrome som webbläsare och inte i inkogenitläge. Detta är en begränsning av testversionen, inte av Universal Editor.

Med den universella redigeraren kan du smidigt redigera text både i sitt sammanhang och på plats, vilket gör det enkelt och intuitivt att skapa innehåll.

1. Redigeraren bör läsas in som standard i **Komponenter** läge. Om inte, tryck eller klicka på **Komponenter** i fältet mode till vänster om redigeraren.

1. Dubbeltryck eller klicka på titeln för den senaste artikeln för att redigera den.

   ![Universell redigerare](assets/do-not-localize/ue-component-mode.png)

1. Komponenten markeras enligt en blå kant med en tabb som anger att det är en textkomponent. Det finns en markör i kanten som väntar på textinmatning. Ändra texten till `Aloha Spirit in Lofoten`.

   ![Redigera text i den universella redigeraren](assets/do-not-localize/ue-edit-text-2.png)

1. Tryck på Enter eller tryck eller klicka utanför textkomponenten så sparas ändringarna automatiskt.

Den universella redigeraren sparar ändringarna automatiskt i redigeringsmiljön. Du måste fortfarande publicera dem så att läsarna kan se dem, vilket vi gör i ett senare steg.

## Redigera media i kontext {#edit-media}

Du kan också byta ut bilder samtidigt som du behåller innehållet genom att använda den universella redigeraren.

1. Återstår i **Komponenter** markerar du surfarens bild genom att trycka eller klicka på den.

1. I komponentspåret kan du se detaljerna för resursen. Tryck eller klicka på **Aktuell bild** miniatyrbild.

   ![Markera en bild som ska redigeras](assets/do-not-localize/ue-edit-media.png)

1. I **Välj resurser** bläddra nedåt och tryck eller klicka på `surfer-wave-02.JPG` för att markera den.

1. Tryck eller klicka **Välj** i **Välj resurser** -fönstret.

   ![Använda fönstret Välj resurs för att välja en bild](assets/do-not-localize/ue-select-asset.png)

Bilden ersätts med den bild du har markerat.

## Upplev ert innehåll som er Reader {#emulators}

Med den universella redigeraren kan du interagera med ditt innehåll i dess sammanhang och se innehållet så som det levereras till användarnas enheter.

1. Som standard återger redigeraren skrivbordsversionen av ditt innehåll. Tryck eller klicka på emulatorknappen längst upp till höger i redigeraren för att ändra målenheten.

   ![Emulatormenyalternativet](assets/do-not-localize/ue-emulator-1.png)

1. Reader kan finnas på olika enheter med olika proportioner, så redigeraren erbjuder emuleringslägen för att se hur sidan visas för användarna. Välj till exempel alternativet för mobil enhet i stående läge.

   ![Emulatormenyalternativet](assets/do-not-localize/ue-emulator-2.png)

1. Se innehållsändringen i redigeraren. Emulatorns ikon ändras också för att återspegla det läge emulatorn är i. Tryck eller klicka var som helst utanför emulatormenyn för att stänga den och interagera med innehållet.

1. Återställa emulatorn till skrivbordsläge.

Du kan också ange exakta dimensioner för emulatorn och rotera den emulerade enheten för att visa innehållet på valfri målenhet.

## Förhandsgranska och publicera {#preview}

Eftersom du behöver trycka eller klicka på innehållet för att markera det i redigeraren kan du inte följa länkar eller interagera med innehållet genom att trycka eller klicka när det är i redigeringsläge. I förhandsgranskningsläget kan du följa länkarna i ditt innehåll och uppleva det som användarna gör innan de publicerar det.

1. Tryck eller klicka i fältet mode till vänster om redigeraren **Förhandsgranska**.

1. Tryck eller klicka på **Läs mer** för huvudartikeln.

   ![Förhandsgranskningsläge](assets/do-not-localize/ue-preview-publish-1.png)

1. Bläddra i artikeln och använd sedan **Bakåt** för att gå tillbaka till huvudsidan.

   ![Återgå till huvudsidan med hjälp av länken Bakåt](assets/do-not-localize/ue-preview-publish-3.png)

1. Tryck eller klicka på **Publicera** längst upp till höger i redigeraren för att publicera ditt innehåll.

   ![Förhandsgranska och publicera menyalternativ](assets/do-not-localize/ue-preview-publish-4.png)

Ditt innehåll publiceras.

## Redigera innehållsfragment {#editing-fragments}

För att snabba upp redigeringen av innehåll när strukturerad redigering av headless-innehåll är mer fördelaktig än redigering på plats, ger den universella redigeraren snabb åtkomst även till Content Fragment-redigeraren.

1. Bläddra längre ned på sidan till sidan **Annonser** -avsnitt.

1. I fältet mode till vänster om redigeraren väljer du **Komponenter**. På så sätt kan du välja sidkomponenter i redigeraren.

1. Tryck eller klicka på något av äventyren som **Bali Surf Camp** för att markera den.

   * Observera den markerade komponentens blå kontur. Fliken ska visa namnet på innehållsfragmentet när ett innehållsfragment är markerat. I detta fall **Bali Surf Camp**.
   * Eftersom den universella redigeraren tillåter att du markerar ett objekt på sidan, kan komponenter som är delar av ett innehållsfragment också markeras individuellt. Tryck eller klicka där det visas på bilden för att markera hela komponenten för innehållsfragment.

1. The **Redigera** visas på komponenträlen. Tryck eller klicka på **Redigera** om du vill öppna redigeraren för innehållsfragment på en ny flik.

![Markera innehållsfragment i den universella redigeraren](assets/do-not-localize/ue-content-fragments.png)

På den nya fliken kan du nu redigera det innehållsfragment du har valt i den universella redigeraren.
