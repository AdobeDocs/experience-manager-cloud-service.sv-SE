---
title: Skapa och hantera kanaler på skärmar som en Cloud Service
description: På den här sidan beskrivs hur du skapar och hanterar kanaler på skärmar som en Cloud Service.
hide: true
hidefromtoc: true
index: false
source-git-commit: ece3fae8b65b4dbdc38e63a211a3f55f4eb91333
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 0%

---


# Skapa och hantera kanaler på skärmar som en Cloud Service {#creating-channels-screens-cloud}

När du har skapat ett AEM Screens-projekt måste du skapa kanaler.
***Kanaler***, visa en innehållssekvens (bilder och videoklipp), en webbplats eller ett ensidigt program.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur du skapar och hanterar kanaler för ditt AEM Screens-projekt i Screens Content Provider. När du har läst bör du:

* Lär dig hur du skapar kanaler för leverantörer av skärminnehåll.
* Hantera era kanaler i ett AEM Screens-projekt utifrån deras omfattning.

## Steg för att skapa en ny sekvenskanal i skärmar som en Cloud Service {#create-new-channel}

>[!NOTE]
>**Förutsättningar**
>Innan du startar det här avsnittet av handboken bör du granska [Skapa och hantera projekt på skärmar som en Cloud Service](/help/screens-cloud/creating-content/creating-projects-screens-cloud.md).

Följ stegen nedan för att skapa en ny sekvenskanal i Skärmar som en Cloud Service:

1. Navigera till Screens Content Provider.

1. Navigera till ditt AEM Screens-projekt, till exempel *FirstDigitalExperience*.

1. Välj mappen **Kanaler** i ditt projekt, till exempel **FirstDigitalExperience** —> **Kanaler** och klicka på **Skapa** i åtgärdsfältet.

   ![](/help/screens-cloud/assets/create-content/channel-create1.png)

1. Välj mallen, till exempel **Sekvenskanal** i guiden **Skapa** och klicka på **Nästa**.

   ![](/help/screens-cloud/assets/create-content/channel-create2.png)
   >[!NOTE]
   > Guiden **Skapa** innehåller olika typer av mallar när du skapar en kanal. Mer information finns i avsnittet Tillgängliga mallar i guiden Skapa.

1. Ange namnet på sekvenskanalen, till exempel **LoopingChannelOne** och klicka på **Create**.

   ![](/help/screens-cloud/assets/create-content/channel-create3.png)

   Nu visas en **LoopingChannelOne** i din kanalmapp i ditt AEM Screens-projekt.

1. När du har skapat kanalen kan du nu lägga till innehåll i kanalen. Mer information om hur du lägger till resurser (bilder/videor) i kanalen finns i [Lägga till innehåll i en kanal](#add-content).

## Hantera en kanal {#managing-channels}

Du kan redigera, visa egenskaper och kontrollpanel, kopiera, förhandsgranska och ta bort en kanal.

Navigera till kanalen från ditt projekt och markera kanalen enligt bilden nedan. Nu kan du välja alternativ som att redigera kanalen, visa egenskaper, förhandsgranska innehåll, hantera publicering eller ta bort kanalen från åtgärdsfältet.

![](/help/screens-cloud/assets/create-content/channelprop1.png)

### Lägga till innehåll i en kanal {#add-content}

Följ stegen nedan om du vill lägga till eller redigera innehåll i en kanal:

1. Markera kanalen som du vill redigera, enligt bilden nedan. Klicka på **Redigera** i åtgärdsfältets övre vänstra hörn för att öppna redigeraren.

   ![](/help/screens-cloud/assets/create-content/edit-channel1.png)

1. Med redigeraren kan du lägga till resurser/komponenter i kanalen som du vill publicera.

1. Dra och släpp resurserna från den vänstra rutan och lägg till dem i redigeraren.

   ![](/help/screens-cloud/assets/create-content/edit-channel2.png)

   >[!NOTE]
   >Klicka på **Förhandsgranska** för att förhandsgranska innehållet i kanalen.
   >![](/help/screens-cloud/assets/create-content/edit-channelpreview.png)

## Tillgängliga mallar i guiden Skapa {#available-templates}

Följande mallar är tillgängliga när du använder kanalguiden för **Create**, till exempel:

| Tillgängliga mallar | Beskrivning |
|--- |--- |
| Mappen Kanaler | Gör att du kan skapa en mapp för lagring av kanalsamlingar. |
| Sekvenskanal | Gör att du kan skapa en kanal som spelar upp komponenterna sekventiellt (en i taget i ett bildspel). |
| Vänster eller höger L-streckkanal för delad skärm | Innehållsförfattare kan visa olika typer av resurser i zoner med lämplig storlek. |


## What&#39;s Next {#whats-next}

Nu när du har konfigurerat en AEM Screens-kanal i ditt projekt måste du publicera din kanal. Se [Publiceringskanaler på skärmar som en Cloud Service](/help/screens-cloud/creating-content/manage-publish.md) innan du hanterar dina spelare från Screens Services Provider.