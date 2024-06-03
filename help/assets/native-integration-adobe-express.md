---
title: AEM Assets inbyggda integrering med Adobe Express
description: Tack vare AEM Assets inbyggda integrering med Adobe Express får du direkt åtkomst till resurser som lagras i AEM Assets inifrån användargränssnittet för Adobe Expressen.
exl-id: d43e4451-da2a-444d-9aa4-4282130ee44f
source-git-commit: 4e33782dd8db0c1185b9a7733e7bcccfbcf3c3ba
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 0%

---

# Inbyggd integrering med Adobe Express {#native-integration-adobe-express}

AEM Assets kan integreras direkt med Adobe Express, vilket gör att du kan komma åt material som lagras i AEM Assets direkt inifrån användargränssnittet i Adobe Expressen. Du kan placera innehåll som hanteras i AEM Assets på arbetsytan Express och sedan spara nytt eller redigerat innehåll i en AEM Assets-databas. Integreringen ger följande viktiga fördelar:

* Större återanvändning av innehåll genom att redigera och spara nya resurser i AEM.

* Minskar den totala tiden och arbetet med att skapa nya resurser eller skapa nya versioner av befintliga resurser.

## Förutsättningar {#prerequisites}

Tillstånd att få tillgång till Adobe Express och minst en miljö i AEM Assets. Miljön kan vara någon av databaserna i Assets as a Cloud Service eller Assets Essentials.


## Använda AEM Assets i Adobe Express Editor {#use-aem-assets-in-express}

Så här börjar du använda AEM Assets i redigeraren:

1. Öppna Adobe Expressens webbprogram.

2. Öppna en ny tom arbetsyta genom att läsa in en ny mall eller ett projekt, eller genom att skapa en resurs.

3. Klicka **[!UICONTROL Assets]** finns i den vänstra navigeringsrutan. Adobe Express visar en lista över databaser som du har behörighet att komma åt tillsammans med en lista över resurser och mappar som är tillgängliga på rotnivå.

4. Bläddra bland eller sök resurser i databasen för att dra och släppa dem på arbetsytan. Du kan filtrera resurser med hjälp av olika tillgängliga filter, till exempel filtyp, MIME-typ och dimensioner.

   >[!NOTE]
   >
   >Filtrera efter dimension gäller inte videoklipp.

   ![Inkludera resurser från resurstillägg](assets/adobe-express-native-integration.png)


## Spara Adobe Expresser i AEM Assets {#save-express-projects-in-assets}

När du har infogat lämpliga ändringar på arbetsytan Express kan du spara dem i AEM Assets-databasen.

1. Klicka **[!UICONTROL Share]** för att öppna **[!UICONTROL Share]** -dialogrutan.

   ![Spara resurser i AEM](assets/adobe-express-share.png)

2. I avsnittet Lagring i den högra rutan väljer du **AEM Assets**. Adobe Expressen visar dialogrutan för överföring.
3. Välj antingen **Aktuell sida** eller **Alla sidor** sparalternativ. Markera **Aktuell sida** sparar filen i målmappen, men väljer **Alla sidor** skapar en ny mapp i målmappen för alla filer som inte är PDF och sparar dem som separata filer medan PDF-filer sparas som en enda fil i målmappen.
4. Ange ett namn och format för resursen. Du kan spara arbetsytans innehåll i PNG-, JPEG, PDF, MP4-, MP4+PNG- eller MP4+JPEG-format. Formatet justeras automatiskt baserat på tillgången/tillgångarna.
5. Klicka på mappikonen under **Målmapp** för att välja en plats och spara resursen/resurserna.

   ![Spara resurser i AEM](/help/assets/assets/page-selection-and-destination-folder.svg)

6. Valfritt: Du kan lägga till kampanjmetadata för överföringen med **Projekt- eller kampanjnamn** fält. Du kan använda ett befintligt namn eller skapa ett nytt. Du kan definiera flera projekt- eller kampanjnamn för överföringen. Registrera namnet genom att skriva namnet och trycka på Retur.
Som en god praxis rekommenderar Adobe att du anger värden i resten av fälten samt skapar en förbättrad sökupplevelse för dina överförda resurser.

7. Definiera på liknande sätt värden för **[!UICONTROL Keywords]** och **[!UICONTROL Channels]** fält.

8. Klicka **[!UICONTROL Upload]** om du vill överföra resurserna till AEM Assets.

## Begränsningar {#limitations}

1. För import och export är den videofiltyp som stöds MP4.

2. För MP4-videoimport:

   1. Den största filstorlek som stöds är 200 MB. Om gränsen överskrids visas ett varningsmeddelande.
   2. Den högsta upplösningen som stöds är 3 840 × 3 840 pixlar.
   3. Videor med genomskinliga bakgrunder (alfakanal) stöds inte.

3. För MP4-videoexport:

   1. Den största filstorlek som stöds är 200 MB. Om gränsen överskrids föreslår en varning att videon trimmas till 200 MB eller mindre, eller att den överförs manuellt till AEM Assets målmapp när den har laddats ned.



