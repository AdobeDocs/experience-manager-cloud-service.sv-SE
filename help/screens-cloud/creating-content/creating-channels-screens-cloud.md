---
title: Skapa och hantera kanaler på skärmar as a Cloud Service
description: På den här sidan beskrivs hur du skapar och hanterar kanaler på skärmar as a Cloud Service.
exl-id: 3b0bae7a-4a45-485a-ab04-604510ff6578
source-git-commit: 96a0dacf69f6f9c5744f224d1a48b2afa11fb09e
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 0%

---

# Skapa och hantera en kanal på skärmar as a Cloud Service {#creating-channels-screens-cloud}

När du har skapat ett AEM Screens-projekt måste du skapa kanaler.
***Kanaler***, visar en sekvens med innehåll (bilder och videoklipp), en webbplats eller ett ensidigt program.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur du skapar och hanterar kanaler för ditt AEM Screens-projekt i Screens Content Provider. När du har läst bör du:

* förstå hur du skapar kanaler för leverantörer av skärminnehåll
* hantera och redigera innehåll i era kanaler

## Steg för att skapa en ny sekvenskanal på skärmar-as a Cloud Service {#create-new-channel}

>[!NOTE]
>**Förutsättningar**
>Innan du börjar med det här avsnittet av handboken bör du granska [Skapa och hantera projekt på skärmar as a Cloud Service](/help/screens-cloud/creating-content/creating-projects-screens-cloud.md).

Följ stegen nedan för att skapa en ny sekvenskanal på as a Cloud Service Skärmar:

1. Navigera till Screens Content Provider.

1. Navigera till ditt AEM Screens-projekt, till exempel *FirstDigitalExperience*.

1. Välj **Kanaler** mapp från ditt projekt, till exempel **FirstDigitalExperience** —> **Kanaler** och klicka på **Skapa** i åtgärdsfältet.

   ![](/help/screens-cloud/assets/create-content/channel-create1.png)

1. Välj en mall, till exempel **Sekvenskanal** från **Skapa** guide och klicka på **Nästa**.

   ![](/help/screens-cloud/assets/create-content/channel-create2.png)
   >[!NOTE]
   > The **Skapa** Guiden innehåller olika typer av mallar när du skapar en kanal. Se avsnittet [Tillgängliga mallar](#available-templates) i Skapa guide för mer information.

1. Ange namnet på sekvenskanalen, till exempel **LoopingChannelOne** och klicka på **Skapa**.

   ![](/help/screens-cloud/assets/create-content/channel-create3.png)

   Nu kommer du att se **LoopingChannelOne** i din kanalmapp i ditt AEM Screens-projekt.

   När du har skapat kanalen kan du nu lägga till innehåll i kanalen. Se [Lägga till innehåll i en kanal](#add-content) om du vill lära dig hur du lägger till resurser (bilder/videor) i din kanal.

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

Följande mallar är tillgängliga när du använder **Skapa** kanalguide:

| Tillgängliga mallar | Beskrivning |
|--- |--- |
| Mappen Kanaler | Gör att du kan skapa en mapp för lagring av kanalsamlingar. |
| Sekvenskanal | Gör att du kan skapa en kanal som spelar upp komponenterna sekventiellt (en i taget i ett bildspel). |
| Vänster eller höger L-streckkanal för delad skärm | Innehållsförfattare kan visa olika typer av resurser i zoner med lämplig storlek. |


## What&#39;s Next {#whats-next}

Nu när du har konfigurerat en AEM Screens-kanal i ditt projekt måste du publicera din kanal. Se [Publicera kanaler på skärmar as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/create-content/manage-publish.html?lang=en) innan du hanterar dina spelare från Screens Services Provider.
