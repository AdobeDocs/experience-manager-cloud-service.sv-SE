---
title: Skapa och hantera kanaler i Screens as a Cloud Service
description: På den här sidan beskrivs hur du skapar och hanterar kanaler i Screens as a Cloud Service.
exl-id: 3b0bae7a-4a45-485a-ab04-604510ff6578
feature: Authoring Screens
role: Admin, Developer, User
source-git-commit: 6719e0bcaa175081faa8ddf6803314bc478099d7
workflow-type: tm+mt
source-wordcount: '1102'
ht-degree: 1%

---

# Skapa och hantera en kanal i Screens as a Cloud Service {#creating-channels-screens-cloud}

När du har skapat ett AEM Screens-projekt måste du skapa kanaler.
***Kanaler***, visa en innehållssekvens (bilder och videoklipp), en webbplats eller ett ensidigt program.

## Syfte {#objective}

Det här dokumentet hjälper dig att skapa och hantera kanaler för ditt AEM Screens-projekt i Screens Content Provider. Efter läsning bör du:

* förstå hur man skapar kanaler till Screens Content Provider
* hantera och redigera innehåll i era kanaler
* hantera tilldelning och aktiveringsschema för dina kanaler i [Screens tjänsteleverantör](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/configure-screens-cloud/navigating-to-screens-services-provider.html?lang=en)

## Steg för att skapa en ny sekvenskanal i Screens as a Cloud Service {#create-new-channel}

>[!NOTE]
>**Förutsättningar**
>Granska [Skapa och hantera projekt i Screens as a Cloud Service](/help/screens-cloud/creating-content/creating-projects-screens-cloud.md) innan du startar det här avsnittet av handboken.

Följ stegen nedan för att skapa en sekvenskanal i Screens as a Cloud Service:

1. Gå till Screens Content Provider.

1. Navigera till ditt AEM Screens-projekt, till exempel *FirstDigitalExperience*.

1. Välj mappen **Kanaler** i ditt projekt, till exempel **FirstDigitalExperience** —> **Kanaler**, och klicka på **Skapa** i åtgärdsfältet.

   ![channel-create1](/help/screens-cloud/assets/create-content/channel-create1.png)

1. Välj mallen, till exempel **Sekvenskanal**, i guiden **Skapa** och klicka på **Nästa**.

   ![channel-create2](/help/screens-cloud/assets/create-content/channel-create2.png)

   >[!NOTE]
   > Guiden **Skapa** innehåller olika typer av mallar när du skapar en kanal. Mer information finns i [Tillgängliga mallar](#available-templates) i guiden Skapa.

1. Ange namnet på sekvenskanalen, till exempel **LoopingChannelOne**, och klicka på **Skapa**.

   ![channel-create3](/help/screens-cloud/assets/create-content/channel-create3.png)

   Nu visas en **LoopingChannelOne** i din kanalmapp i ditt AEM Screens-projekt.

   När du har skapat kanalen kan du nu lägga till innehåll i kanalen. Se [Lägga till innehåll i en kanal](#add-content) för att lära dig hur du lägger till resurser (bilder/videor) i din kanal.

## Hantera en kanal {#managing-channels}

Du kan redigera, visa egenskaper och kontrollpanel, kopiera, förhandsgranska och ta bort en kanal.

Navigera till kanalen från ditt projekt och markera kanalen enligt bilden nedan. Nu kan du välja alternativ som att redigera kanalen, visa egenskaper, förhandsgranska innehåll, hantera publicering eller ta bort kanalen från åtgärdsfältet.

![channelProp1](/help/screens-cloud/assets/create-content/channelprop1.png)

### Lägga till innehåll i en kanal {#add-content}

Följ stegen nedan om du vill lägga till eller redigera innehåll i en kanal:

1. Markera kanalen som du vill redigera, enligt bilden nedan. Klicka på **Redigera** i åtgärdsfältets övre vänstra hörn för att öppna redigeraren.

   ![edit-channel1](/help/screens-cloud/assets/create-content/edit-channel1.png)

1. Med redigeraren kan du lägga till resurser/komponenter i kanalen som du vill publicera.

1. Dra och släpp resurserna från den vänstra rutan och lägg till dem i redigeraren.

   ![edit-channel2](/help/screens-cloud/assets/create-content/edit-channel2.png)

   >[!NOTE]
   >Klicka på **Förhandsgranska** om du vill förhandsgranska innehållet i kanalen.
   >![edit-channelPreview](/help/screens-cloud/assets/create-content/edit-channelpreview.png)

## Tillgängliga mallar i guiden Skapa {#available-templates}

Följande mallar är tillgängliga när du använder kanalguiden **Skapa**:

| Tillgängliga mallar | Beskrivning |
|--- |--- |
| Mappen Kanaler | Gör att du kan skapa en mapp för lagring av kanalsamlingar. |
| Sekvenskanal | Skapa en kanal som spelar upp komponenterna sekventiellt (en i taget i ett bildspel). |
| Vänster eller höger L-streckkanal för delad skärm | Innehållsförfattare kan visa olika typer av resurser i zoner med lämplig storlek. |

## Använd standardtilldelningsinformation för kanaler {#default-channels}

Med den här funktionen kan du definiera ett standardaktiveringsschema för en kanal och använda det som standard för varje tilldelning för en visning. Detta innehåller en metod så att den krångliga schemadefinitionen inte behöver upprepas.

1. Gå till [Screens Services Provider](https://experience.adobe.com/screens).

### Skapa standardtilldelningsinformation för en kanal {#create-default}

1. Navigera till informationssidan för kanalen som du vill konfigurera.
1. Leta reda på rutan **Standardtilldelningsinformation** på sidan.

   ![bild](/help/screens-cloud/assets/display/Assignment1.png)

1. Klicka på **Ange standardinformation**.
1. Konfigurera kanalens standardtilldelningsinformation, inklusive prioritet, start- och slutdatum samt upprepningsmönster, och klicka sedan på **Tilldela**.

   ![bild](/help/screens-cloud/assets/display/Assignments2.png)

1. Observera att information om tilldelningen visas i rutan **Standardtilldelningsinformation**:

   ![bild](/help/screens-cloud/assets/display/Assignments3.png)

Den här rutan visar följande information:
* Kanalens standardprioritet i visningen.
* Start- och slutdatum för aktiveringen när kanalen är schemalagd att spelas upp.
* Syntetisk vy av upprepningen (varje timme/dag/vecka/varje månad/år och namn som angetts för upprepningen).

### Använd standarduppdragsinformationen när du tilldelar till en skärm {#default-display}

Kanaler som har standardtilldelningsinformation kan tilldelas till visar på samma sätt som vanliga kanaler, med alternativet att lägga till som standardtilldelningsinformation i stället för att manuellt definiera anpassade kanaler varje gång.

1. Navigera till sidan med visningsinformation som du vill tilldela kanalen till och klicka på **Tilldela kanal**.
Du kan också markera önskad visning i vyn [lager](https://experience.adobe.com/screens/displays) och klicka på **Tilldela kanal**.
1. Dialogrutan för kanaltilldelning öppnas.

   ![bild](/help/screens-cloud/assets/display/Assignments4.png)

1. Välj den kanal som har standardtilldelningsinformationen från kanalväljaren.
1. Lägg märke till att dialogrutan för kanaltilldelning ändras så att du kan välja standardtilldelningsinformation, eller välja anpassade:

   ![bild](/help/screens-cloud/assets/display/Assignments5.png)

1. Klicka på **Tilldela** om du vill slutföra tilldelningen eller klicka på **Ange anpassad tilldelningsinformation** om du föredrar att åsidosätta standardvärdena med vissa andra värden i den specifika visningen.

   ![bild](/help/screens-cloud/assets/display/Assignments6.png)

1. Observera att rutan **Tilldelade kanaler** uppdateras med den nya tilldelningen:

   ![bild](/help/screens-cloud/assets/display/Assignments7.png)

1. Observera att kanalerna kommer att ha en annan ikon beroende på om de använder anpassade scheman (klockikonen) eller ärver standardinformationen (klockikonen). Om du klickar på dessa kommer schemaläggningsinformationen att visas.
1. Observera också att de tillgängliga åtgärderna för varje typ kommer att vara olika.

   ![bild](/help/screens-cloud/assets/display/Assignments8.png)

**Obs!** En kanaltilldelning som använder standardtilldelningsinformationen kan inte redigeras i visningssammanhanget.

* Om du måste ändra det till ett anpassat uppdrag tar du först bort det och lägger sedan till det igen med alternativet **Ange anpassad uppdragsinformation** .
* Om du måste ändra egenskaperna för standarduppdragsinformationen gör du det direkt från sidan med kanalinformation.

### Ta bort information om standardtilldelning från en kanal {#remove-display}

1. Navigera till informationssidan för kanalen som du vill ta bort standardtilldelningsinformationen för.
1. Leta reda på rutan **Standardtilldelningsinformation** på sidan
1. Klicka på **Ta bort standard**.

   ![bild](/help/screens-cloud/assets/display/Assignments9.png)

1. En bekräftelsedialogruta visas och detaljerna matchar något av följande villkor:
   **a.** Kanalen används inte i någon visning.

   ![bild](/help/screens-cloud/assets/display/Assignments10.png)

**b.** Kanalen används i en enda skärm.

![bild](/help/screens-cloud/assets/display/Assignment11.png)

**c.** Kanalen används på flera skärmar.

![bild](/help/screens-cloud/assets/display/Assignments12.png)

1. Klicka på *Ta bort* för att validera ändringen.

**Obs!** Om du tar bort standardtilldelningsinformationen från en kanal tas matchande tilldelningar bort på alla skärmar som använder den.
Detta kan leda till tomma skärmar om det inte finns något alternativt innehåll att spela upp på dessa skärmar.

## What&#39;s Next {#whats-next}

Nu när du har konfigurerat en AEM Screens-kanal i ditt projekt måste du publicera din kanal. Se [Publicera kanaler i Screens as a Cloud Service](manage-publish.md) innan du hanterar dina spelare från Screens Services Provider.
