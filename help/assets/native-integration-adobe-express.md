---
title: Integrering med Adobe Express
description: Tack vare AEM Assets inbyggda integrering med Adobe Express får du direkt tillgång till resurser som lagras i AEM Assets inifrån Adobe Express användargränssnitt.
exl-id: d43e4451-da2a-444d-9aa4-4282130ee44f
feature: Collaboration
role: User
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '629'
ht-degree: 0%

---

# Inbyggd integrering med Adobe Express {#native-integration-adobe-express}

AEM Assets är integrerat med Adobe Express, som gör att du kan komma åt material som lagras i AEM Assets direkt inifrån Adobe Express användargränssnitt. Du kan placera innehåll som hanteras i AEM Assets på arbetsytan Express och sedan spara nytt eller redigerat innehåll i en AEM Assets-databas. Integreringen ger följande viktiga fördelar:

* Ökad återanvändning av innehåll genom att redigera och spara nya resurser i AEM.

* Minskar den totala tiden och arbetet med att skapa nya resurser eller skapa nya versioner av befintliga resurser.

## Förutsättningar {#prerequisites}

Tillstånd att få tillgång till Adobe Express och minst en miljö i AEM Assets. Miljön kan vara någon av databaserna i Assets as a Cloud Service eller Assets Essentials.


## Använda AEM Assets i Adobe Express Editor {#use-aem-assets-in-express}

Så här börjar du använda AEM Assets i Adobe Express Editor:

1. Öppna Adobe Express webbprogram.

2. Öppna en ny tom arbetsyta genom att läsa in en ny mall eller ett projekt, eller genom att skapa en resurs.

3. Klicka på **[!UICONTROL Assets]** i den vänstra navigeringsrutan. Adobe Express visar en lista över databaser som du har behörighet att komma åt tillsammans med en lista över resurser och mappar som är tillgängliga på rotnivå.

4. Bläddra bland eller sök resurser i databasen för att dra och släppa dem på arbetsytan. Du kan filtrera resurser med hjälp av olika tillgängliga filter, till exempel filtyp, MIME-typ och dimensioner.

   >[!NOTE]
   >
   >Filtrera efter dimension gäller inte videoklipp.

   ![Inkludera resurser från Assets-tillägg](assets/adobe-express-native-integration.png)


## Spara Adobe Express-projekt i AEM Assets {#save-express-projects-in-assets}

När du har infogat lämpliga ändringar på arbetsytan Express kan du spara dem i AEM Assets-databasen.

1. Klicka på **[!UICONTROL Share]** för att öppna dialogrutan **[!UICONTROL Share]**.

   ![Spara resurser i AEM](assets/adobe-express-share.png)

2. Välj **AEM Assets** i lagringsavsnittet i den högra rutan. Adobe Express visar dialogrutan för överföring.
3. Välj antingen **Aktuell sida** eller **Alla sidor**. Ange ett namn och format för de resurser som ska exporteras. Du kan exportera arbetsytans innehåll i PNG-, JPEG-, PDF-, MP4-, MP4+PNG- eller MP4+JPEG-format. Formatet justeras automatiskt baserat på resursen/resurserna på arbetsytans sida/sidor.
Om du väljer **Aktuell sida** sparas resursen på den aktuella sidan i målmappen. Om du väljer **Alla sidor** och exportformatet inte är PDF, sparas alla sidor på arbetsytan som separata filer i en ny mapp i målmappen. Om exportformatet är PDF sparas alla arbetsytesidor som en enda PDF-fil i målmappen.

4. Klicka på mappikonen under **Målmapp** för att välja en plats och spara resurserna.

   ![Spara resurser i AEM](/help/assets/assets/page-selection-and-destination-folder.svg)

5. Valfritt: Du kan lägga till kampanjmetadata för överföringen med fältet **Projekt eller kampanjnamn**. Du kan använda ett befintligt namn eller skapa ett nytt. Du kan definiera flera projekt- eller kampanjnamn för överföringen. Registrera namnet genom att skriva namnet och trycka på Retur.
Adobe rekommenderar att du anger värden i resten av fälten och skapar en förbättrad sökupplevelse för dina överförda resurser.

6. Definiera värden för fälten **[!UICONTROL Keywords]** och **[!UICONTROL Channels]**.

7. Klicka på **[!UICONTROL Upload]** för att överföra resurserna till AEM Assets.

## Begränsningar {#limitations}

1. För import och export är den videofiltyp som stöds MP4.

2. För MP4-videoimport:

   1. Den största filstorlek som stöds är 200 MB. Om gränsen överskrids visas ett varningsmeddelande.
   2. Den högsta upplösningen som stöds är 3 840 × 3 840 pixlar.
   3. Videor med genomskinliga bakgrunder (alfakanal) stöds inte.

3. För MP4-videoexport:

   1. Den största filstorlek som stöds är 200 MB. Om gränsen överskrids föreslår en varning att videon trimmas till 200 MB eller mindre, eller att den överförs manuellt till AEM Assets målmapp när den har laddats ned.



