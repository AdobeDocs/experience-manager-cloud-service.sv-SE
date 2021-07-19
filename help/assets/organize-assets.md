---
title: Ordna digitala resurser
description: Organisera dina digitala resurser med hjälp av olika metoder i Adobe Experience Manager Assets.
contentOwner: AG
feature: Resurshantering,Taggar,Resursdistribution
role: User
exl-id: 6b3ce076-2dd9-47f6-9b68-4fa52bfedd42
source-git-commit: 00bea8b6a32bab358dae6a8c30aa807cf4586d84
workflow-type: tm+mt
source-wordcount: '445'
ht-degree: 0%

---

# Ordna digitala resurser {#organize-digital-assets}

Alla digitala resurser, metadata och innehåll i Microsoft Office- och PDF-dokument extraheras och görs sökbara. Sökning möjliggör avancerad filtrering av resurser och respekterar helt rätt behörigheter. Metadata beskrivs i detalj i Metadata i Digital Asset Management.

AEM Assets har stöd för flera sätt att ordna innehåll. Du kan ordna dem hierarkiskt med hjälp av mappar eller så kan du ordna dem på ett oordnat, tillfälligt sätt, t.ex. med hjälp av taggar. Användare kan redigera taggar i DAM-redigeraren för mediefiler där underresurser, återgivningar och metadata visas.

## Skapa mappar {#create-folders}

När du organiserar en samling resurser, till exempel alla *Natur*-bilder, kan du skapa mappar som håller ihop dem. Du kan använda mappar för att kategorisera och ordna dina resurser. AEM Assets kräver inte att du ordnar resurser i mappar för att fungera bättre.

>[!NOTE]
>
>Det går inte att dela en resursmapp (i Marketing Cloud) av typen `sling:OrderedFolder`. Om du vill dela en mapp ska du inte välja Ordnad när du skapar en mapp.

1. Navigera till den plats i mappen med digitala resurser där du vill skapa en ny mapp.
1. Klicka på **[!UICONTROL Create]** på menyn. Välj **[!UICONTROL New Folder]**.
1. Ange ett mappnamn i fältet **[!UICONTROL Title]**. Som standard använder DAM den titel som du angav som mappnamn. När mappen har skapats kan du åsidosätta standardmappen och ange ett annat mappnamn.
1. Klicka på **[!UICONTROL Create]**. Mappen visas i mappen med digitala resurser.

## Lägga till CUG-egenskaper i mappar {#add-cug-properties-to-folders}

Du kan begränsa vem som kan få åtkomst till vissa mappar i Resurser genom att göra mappen till en sluten användargrupp (CUG). Så här gör du en mapp till en CUG-fil:

1. Högerklicka på den mapp som du vill lägga till slutna användargruppsegenskaper för i Resurser och välj **Egenskaper**.
1. Klicka på fliken **CUG**.
1. Markera kryssrutan **Aktiverad** om du vill att mappen och dess resurser endast ska vara tillgängliga för en stängd användargrupp.
1. Bläddra till inloggningssidan, om det finns någon, för att lägga till den informationen. Lägg till godkända grupper genom att klicka på **Lägg till objekt**. Lägg till sfären om det behövs. Klicka på **OK** för att spara ändringarna.

## Använd taggar för att ordna resurser {#use-tags-to-organize-assets}

Du kan använda mappar eller taggar, eller båda, för att ordna resurser. Om du lägger till taggar i resurser blir det enklare att hämta dem vid en sökning. Så här lägger du till taggar i en resurs:

1. Öppna resursen genom att dubbelklicka på den i Digital Asset Manager.
1. I området **Taggar** öppnar du menyn för att visa de tillgängliga taggarna. Välj taggar efter behov. Om du vill ta bort en tagg håller du pekaren över taggen och klickar på `X` för att ta bort den.
1. Klicka på **Spara** för att spara alla taggar du har lagt till.
