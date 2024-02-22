---
title: Skapa och hantera kanaler på skärmar as a Cloud Service
description: På den här sidan beskrivs hur du skapar och hanterar kanaler på skärmar as a Cloud Service.
exl-id: 3b0bae7a-4a45-485a-ab04-604510ff6578
source-git-commit: f7ed7c63fd141c6a9817e4718edb31425b14a761
workflow-type: tm+mt
source-wordcount: '1103'
ht-degree: 1%

---

# Skapa och hantera en kanal på skärmar as a Cloud Service {#creating-channels-screens-cloud}

När du har skapat ett AEM Screens-projekt måste du skapa kanaler.
***Kanaler***, visar en sekvens med innehåll (bilder och videoklipp), en webbplats eller ett ensidigt program.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur du skapar och hanterar kanaler för ditt AEM Screens-projekt i Screens Content Provider. Efter läsning bör du:

* förstå hur du skapar kanaler för leverantörer av skärminnehåll
* hantera och redigera innehåll i era kanaler
* hantera tilldelnings- och aktiveringsschemat för era kanaler i [Tjänsteleverantör för skärmar](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/configure-screens-cloud/navigating-to-screens-services-provider.html?lang=en)

## Steg för att skapa en ny sekvenskanal på skärmar-as a Cloud Service {#create-new-channel}

>[!NOTE]
>**Förutsättningar**
>Innan du startar det här avsnittet av handboken bör du granska [Skapa och hantera projekt på skärmar as a Cloud Service](/help/screens-cloud/creating-content/creating-projects-screens-cloud.md).

Följ stegen nedan för att skapa en sekvenskanal på as a Cloud Service Skärmar:

1. Navigera till Screens Content Provider.

1. Navigera till ditt AEM Screens-projekt, till exempel *FirstDigitalExperience*.

1. Välj **Kanaler** mapp från ditt projekt, till exempel **FirstDigitalExperience** —> **Kanaler** och klicka **Skapa** i åtgärdsfältet.

   ![channel-create1](/help/screens-cloud/assets/create-content/channel-create1.png)

1. Välj en mall, till exempel **Sekvenskanal** från **Skapa** guide och klicka **Nästa**.

   ![channel-create2](/help/screens-cloud/assets/create-content/channel-create2.png)

   >[!NOTE]
   > The **Skapa** Guiden innehåller olika typer av mallar när du skapar en kanal. Se [Tillgängliga mallar](#available-templates) i Skapa guide för mer information.

1. Ange namnet på sekvenskanalen, till exempel **LoopingChannelOne** och klicka **Skapa**.

   ![channel-create3](/help/screens-cloud/assets/create-content/channel-create3.png)

   Nu kommer du att se **LoopingChannelOne** i din kanalmapp i ditt AEM Screens-projekt.

   När du har skapat kanalen kan du nu lägga till innehåll i kanalen. Se [Lägga till innehåll i en kanal](#add-content) om du vill lära dig hur du lägger till resurser (bilder/videor) i din kanal.

## Hantera en kanal {#managing-channels}

Du kan redigera, visa egenskaper och kontrollpanel, kopiera, förhandsgranska och ta bort en kanal.

Navigera till kanalen från ditt projekt och markera kanalen enligt bilden nedan. Nu kan du välja alternativ som att redigera kanalen, visa egenskaper, förhandsgranska innehåll, hantera publicering eller ta bort kanalen från åtgärdsfältet.

![kanelprop1](/help/screens-cloud/assets/create-content/channelprop1.png)

### Lägga till innehåll i en kanal {#add-content}

Följ stegen nedan om du vill lägga till eller redigera innehåll i en kanal:

1. Markera kanalen som du vill redigera, enligt bilden nedan. Klicka **Redigera** i åtgärdsfältets övre vänstra hörn för att öppna redigeraren.

   ![edit-channel1](/help/screens-cloud/assets/create-content/edit-channel1.png)

1. Med redigeraren kan du lägga till resurser/komponenter i kanalen som du vill publicera.

1. Dra och släpp resurserna från den vänstra rutan och lägg till dem i redigeraren.

   ![edit-channel2](/help/screens-cloud/assets/create-content/edit-channel2.png)

   >[!NOTE]
   >Klicka **Förhandsgranska** för att förhandsgranska innehållet i kanalen.
   >![edit-channel-preview](/help/screens-cloud/assets/create-content/edit-channelpreview.png)

## Tillgängliga mallar i guiden Skapa {#available-templates}

Följande mallar är tillgängliga när du använder **Skapa** kanalguide:

| Tillgängliga mallar | Beskrivning |
|--- |--- |
| Mappen Kanaler | Gör att du kan skapa en mapp för lagring av kanalsamlingar. |
| Sekvenskanal | Skapa en kanal som spelar upp komponenterna sekventiellt (en i taget i ett bildspel). |
| Vänster eller höger L-streckkanal för delad skärm | Innehållsförfattare kan visa olika typer av resurser i zoner med lämplig storlek. |

## Använd standardtilldelningsinformation för kanaler {#default-channels}

Med den här funktionen kan du definiera ett standardaktiveringsschema för en kanal och använda det som standard för varje tilldelning för en visning. Detta innehåller en metod så att den krångliga schemadefinitionen inte behöver upprepas.

1. Navigera till Screens Services Provider från [här](https://experience.adobe.com/screens).

### Skapa standardtilldelningsinformation för en kanal {#create-default}

1. Navigera till informationssidan för kanalen som du vill konfigurera.
1. Leta reda på **Standardinformation om tilldelning** på sidan.

   ![bild](/help/screens-cloud/assets/display/Assignment1.png)

1. Klicka **Ange standardinformation**.
1. Konfigurera standardinformation om tilldelning, inklusive prioritet, start- och slutdatum samt återkommande mönster för kanalen, och klicka sedan på **Tilldela**.

   ![bild](/help/screens-cloud/assets/display/Assignments2.png)

1. Observera att information om uppdraget visas i **Standardinformation om tilldelning** platta:

   ![bild](/help/screens-cloud/assets/display/Assignments3.png)

Den här rutan visar följande information:
* Kanalens standardprioritet i visningen.
* Start- och slutdatum för aktiveringen när kanalen är schemalagd att spelas upp.
* Syntetisk vy av upprepningen (varje timme/dag/vecka/varje månad/år och namn som angetts för upprepningen).

### Använd standarduppdragsinformationen när du tilldelar till en skärm {#default-display}

Kanaler som har standardtilldelningsinformation kan tilldelas till visar på samma sätt som vanliga kanaler, med alternativet att lägga till som standardtilldelningsinformation i stället för att manuellt definiera anpassade kanaler varje gång.

1. Navigera till sidan med visningsinformation som du vill tilldela kanalen till och klicka på **Tilldela kanal**.
Du kan också välja önskad visning i [lager](https://experience.adobe.com/screens/displays) visa och klicka på **Tilldela kanal**.
1. Dialogrutan för kanaltilldelning öppnas.

   ![bild](/help/screens-cloud/assets/display/Assignments4.png)

1. Välj den kanal som har standardtilldelningsinformationen från kanalväljaren.
1. Lägg märke till att dialogrutan för kanaltilldelning ändras så att du kan välja standardtilldelningsinformation, eller välja anpassade:

   ![bild](/help/screens-cloud/assets/display/Assignments5.png)

1. Klicka **Tilldela** för att slutföra uppdraget eller klicka på **Ange information om anpassad tilldelning** om du föredrar att åsidosätta standardvärdena med vissa andra värden i det aktuella visningssammanhanget.

   ![bild](/help/screens-cloud/assets/display/Assignments6.png)

1. Lägg märke till **Tilldelade kanaler** plattan uppdateras med det nya uppdraget:

   ![bild](/help/screens-cloud/assets/display/Assignments7.png)

1. Observera att kanalerna kommer att ha en annan ikon beroende på om de använder anpassade scheman (klockikonen) eller ärver standardinformationen (klockikonen). Om du klickar på dessa kommer schemaläggningsinformationen att visas.
1. Observera också att de tillgängliga åtgärderna för varje typ kommer att vara olika.

   ![bild](/help/screens-cloud/assets/display/Assignments8.png)

**Obs!** En kanaltilldelning som använder standardtilldelningsinformationen kan inte redigeras i visningssammanhanget.

* Om du måste ändra det till ett anpassat uppdrag tar du först bort det och lägger sedan till det igen med **Ange information om anpassad tilldelning** alternativ.
* Om du måste ändra egenskaperna för standarduppdragsinformationen gör du det direkt från sidan med kanalinformation.

### Ta bort information om standardtilldelning från en kanal {#remove-display}

1. Navigera till informationssidan för kanalen som du vill ta bort standardtilldelningsinformationen för.
1. Leta reda på **Standardinformation om tilldelning** sida vid sida
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

Nu när du har konfigurerat en AEM Screens-kanal i ditt projekt måste du publicera din kanal. Se [Publicera kanaler på skärmar as a Cloud Service](manage-publish.md) innan du hanterar dina spelare från Screens Services Provider.
