---
title: Konfigurera delade köer
seo-title: Configure shared queues
description: Lär dig hur du använder delade köer för Forms-centrerade arbetsflöden på [!DNL AEM Forms] på OSGi.
seo-description: Learn how to use shared queues for Forms-centric workflows on [!DNL AEM Forms] on OSGi.
topic-tags: process
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 1%

---


# Dela och begära åtkomst till inkorgsobjekt från en användare {#share-and-request-access}

En kö är en lista med objekt AEM en användares inkorg. Dessa kan vara objekt som tilldelats en användare eller objekt som delas med gruppen som en användare är medlem i. Du kan öppna Inkorgen för att visa och utföra åtgärder på Inkorgsobjektet. Du kan till exempel dela ett objekt med en annan användare.

Du kan också dela dina inkorgsobjekt med en annan användare. När en annan användare har åtkomst till dina inkorgsobjekt kan användaren göra anspråk på och vidta lämpliga åtgärder för delade objekt. På samma sätt kan du begära åtkomst till inkorgsobjekt från andra användare.

## Krav {#pre-requisites}

Den inloggade användaren måste vara medlem i [!DNL `workflow-users`] grupp. Användaren kan bara dela objekt eller begära åtkomst till objekt från de användare som den inloggade användaren har läsbehörighet till eller bara från de användare som har aktiverat den offentliga profilen.

## Dela en enskild eller alla objekt i inkorgen med en annan användare

Med AEM Inkorg kan du dela ett eller alla objekt i din inkorg med en annan användare.

### Dela alla inkorgsobjekt

Så här delar du alla objekt i en inkorg med en annan användare:

1. Logga in på din AEM. Tryck på ![Inkorg](assets/bell.svg) ikon och tryck **[!UICONTROL View All]**. En lista över dina inkorgsobjekt visas.
1. Tryck på ![Visa väljare](assets/viewlist.svg) eller ![Visa väljare](assets/calendar.svg) -ikonen bredvid **[!UICONTROL Create]** knapp och knacka **[!UICONTROL Settings]**. Dialogrutan Inställningar visas.
1. Öppna **[!UICONTROL Share]** i inställningsdialogrutan.
1. Ange namnet på en användare i **[!UICONTROL Grant access of your Inbox items]** textruta och tryck **[!UICONTROL Grant]**. Upprepa steget för att lägga till fler användare. Alla användare med åtkomst till dina objekt visas under **Användarnamn** -avsnitt.
1. Tryck på **[!UICONTROL Save]**.

>[!NOTE]
>
>(Endast för Forms-centrerade arbetsflödesobjekt) Aktivera **[Tillåt att den som ska tilldelas delar via Inkorgsdelning](aem-forms-workflow-step-reference.md)** alternativ för **Tilldela uppgift** i arbetsflödet. Endast objekt som har det ovannämnda alternativet aktiverat visas för andra användare.

### Dela enskilda objekt

Så här delar du ett Inkorgsobjekt med en annan användare:

1. Logga in på din AEM. Tryck på ![Inkorg](assets/bell.svg) ikon och tryck **[!UICONTROL View All]**. En lista över dina inkorgsobjekt visas.
1. Markera ett objekt och tryck **[!UICONTROL Share]**. En dialogruta visas.
1. Ange namnet på en användare i textrutan Lägg till användare för att dela det här objektet och tryck på **[!UICONTROL Add]**. Upprepa steget för att lägga till fler användare. Alla användare med åtkomst till dina objekt visas under **[!UICONTROL Username]** -avsnitt.
1. Tryck på **[!UICONTROL Save]**.


>[!NOTE]
>
>(Endast för Forms-centrerade arbetsflödesobjekt) Aktivera **[Tillåt att tilldelad delar explicit i Inkorgen](aem-forms-workflow-step-reference.md)** alternativ för **Tilldela uppgift** i arbetsflödet. Endast objekt som har det ovannämnda alternativet aktiverat visas för andra användare.

## Begär åtkomst till inkorgsobjekt {#request-access}

Du kan begära åtkomst till inkorgsobjekten för en annan användare. När åtkomsten har beviljats kan du visa, göra anspråk på och vidta lämpliga åtgärder för delade objekt. Utför följande steg för att begära åtkomst till inkorgsobjekt från en annan användare:

1. Logga in på din AEM. Tryck på ![Visa väljare](assets/bell.svg) ikon och tryck **[!UICONTROL View All]**.
1. Tryck på ![Visa väljare](assets/viewlist.svg) eller ![Visa väljare](assets/calendar.svg) -ikonen bredvid **[!UICONTROL Create]** knapp och knacka **[!UICONTROL Settings]**. Dialogrutan Inställningar visas.
1. Ange namnet på en användare i **[!UICONTROL Request access to Inbox items of the user]** textruta och tryck **[!UICONTROL Request]**. En begäran skickas till användaren och status för begäran visas mot användarens namn. Upprepa steget för att lägga till fler användare.
1. Tryck på **[!UICONTROL Save]**. Begäran skickas som ett inkorgsobjekt till användarna. Användaren kan markera objektet och trycka på Godkänn eller Avvisa för att bevilja eller avvisa åtkomsten.


## Göra anspråk på objekt som delas av andra användare {#claim-items}

Du kan bara börja arbeta med ett delat objekt efter att du har gjort anspråk på det. Det förhindrar att flera användare arbetar med ett enda objekt. Utför följande steg för att göra anspråk på ett objekt:

1. Logga in på din AEM. Tryck på inkorgen ![Inkorg](assets/bell.svg) ikon och tryck **[!UICONTROL View All]**.
1. Tryck på ![Endast innehåll](assets/railleft.svg) -ikonen för att öppna filterväljaren.
1. Tryck på **[!UICONTROL Select Assignee]** för att visa och välja användare som har delat sina inkorgsobjekt med dig.
1. Markera ett objekt och tryck **[!UICONTROL Claim]**. Objektet läggs till i din inkorg.

## Frisläpp begärda artiklar {#release-items}

Du kan bara arbeta med ett delat objekt efter att du har gjort anspråk på det. Andra användare kan inte se eller arbeta med objekt som du har gjort anspråk på. Om du inte kan fortsätta arbeta med ett objekt kan du släppa det i poolen igen.   När du har släppt objektet kan andra göra anspråk på och arbeta med det:

Utför följande steg för att frigöra ett objekt:

1. Logga in på din AEM. Tryck på inkorgen ![Inkorg](assets/bell.svg) ikon och tryck **[!UICONTROL View All]**. En lista över dina inkorgsobjekt visas.
1. Välj det objekt som ska frisläppas och tryck på **[!UICONTROL UnClaim]**. Objektet läggs till i poolen igen. Andra kan nu göra anspråk på objektet.

## Begränsningar {#limitations}

* Det går inte att dela objekt med en grupp.
* Delning av projektaktiviteter stöds inte.
