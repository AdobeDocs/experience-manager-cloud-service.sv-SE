---
title: Hantera meddelanden
description: Övervaka åtgärderna som utförs på de resurser eller mappar som är tillgängliga i databasen med hjälp av vymeddelanden i Assets.
exl-id: 1fe6a845-37d5-43c2-bb96-c5b149c238ab
feature: Assets Essentials
role: User, Leader
source-git-commit: 4d31745d4ada9e68ffefbba3dc91995037f205b9
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 0%

---

# Titta på resurser, mappar och samlingar {#watch-assets-folders}

Med Assets-vymeddelanden kan du övervaka åtgärder som utförs på de resurser, mappar eller samlingar som är tillgängliga i databasen. Du måste välja och prenumerera på det innehåll som meddelandena skickas till dig för. Du kan också konfigurera de kategorier som meddelanden skickas till dig för.

## Prenumerera på meddelandekategorier {#subscribe-to-notification-categories}

Du kan välja och prenumerera från en lista med kategorier för att få meddelanden. I vyn Assets skickas endast meddelanden till dig för de kategorier som du väljer bland de tillgängliga alternativen:

<table>
    <tbody>
     <tr>
      <th><strong>Meddelandekategori</strong></th>
      <th><strong>Beskrivning</strong></th>
     </tr>
     <tr>
      <td>Begäranden</td>
      <td>När du tilldelar en uppgift till en användare får du meddelanden om när användaren har utfört åtgärder i den uppgiften.</td>
     </tr>
     <tr>
      <td>Tilldelad till mig</td>
      <td>Du får ett meddelande när en uppgift har tilldelats dig från en annan användare.</td>
     </tr>
     <tr>
      <td>Kommentera prenumererat innehåll</td>
      <td>Du får ett meddelande när en användare kommenterar din prenumerationsresurs.</td>
     </tr>
     <tr>
      <td>Borttagning av prenumererat innehåll</td>
      <td>Du får ett meddelande när en användare tar bort din prenumererade resurs, mapp eller samling.</td>
     </tr>
     <tr>
      <td>Extern andel av prenumererat innehåll</td>
      <td>Du får ett meddelande när en användare genererar en offentlig länk för din prenumererade resurs, mapp eller samling.</td>
     </tr>
     <tr>
      <td>Ändring av prenumererat innehåll</td>
      <td>Du får ett meddelande när en användare skapar en ny version för den prenumererade resursen.</td>
     </tr>
     <tr>
      <td>Flytta/byt namn på innehåll som prenumererar</td>
      <td>Du får ett meddelande när en användare flyttar eller byter namn på den prenumererade resursen eller mappen.</td>
     </tr>
     <tr>
      <td>Uppdateringar av prenumerationsmappar och samlingar</td>
      <td>Du får ett meddelande när en användare lägger till eller tar bort en resurs från en prenumerationsmapp eller samling.</td>
     </tr>    
    </tbody>
   </table>

Så här prenumererar du på meddelandekategorierna:

1. Klicka på ![klockikonen](assets/bell-icon.svg) till höger i menyraden i användargränssnittet för vyn i Assets.

1. Klicka på ![inställningsikonen](assets/settings-icon.svg) för att visa sidan [!UICONTROL Experience Cloud preferences].

1. Klicka på alternativet **[!UICONTROL Notifications]** i den vänstra rutan.

1. I avsnittet **[!UICONTROL Notifications]** går du till avsnittet [!UICONTROL Assets view] och ser till att växlingsalternativet är aktiverat.

   ![Meddelanden i Assets-vyn](assets/enable-notifications.png)

1. Klicka på **[!UICONTROL Customize]** om du vill visa meddelandekategorierna.
   ![Meddelanden i Assets-vyn](assets/enable-notification-categories.png)

1. Välj de meddelandekategorier för vilka du måste få meddelanden.

## Titta på och ta bort bevakade mappar, resurser och samlingar {#watch-unwatch-assets}

Du kan bevaka och ta bort bevakade mappar, resurser och samlingar för att hålla dig informerad, vilket ger bättre samarbete kring de resurser du övervakar.

När [du har prenumererat på meddelandekategorierna](#subscribe-to-notification-categories) måste du prenumerera på innehållet för att få meddelanden.

>[!NOTE]
>
>* För meddelandekategorierna **[!UICONTROL Requests]** och **[!UICONTROL Assigned to me]** behöver du inte prenumerera på innehållet efter att du har prenumererat på meddelandekategorierna. Meddelanden skickas automatiskt till dig för förfrågningar som du har skapat och när en uppgift har tilldelats dig.
>* I Assets-vyn skickas meddelanden endast när andra användare utför åtgärder på det prenumererade innehållet. Du får inga meddelanden om vilka åtgärder du utför på det prenumererade innehållet.

### Prenumerera på innehållet {#subscribe-to-content}

Så här prenumererar du på mappar, resurser och samlingar:

1. Bläddra i mappen, resursen eller samlingen som du vill prenumerera på och klicka på **[!UICONTROL Watch]**.

1. I Assets-vyn visas ett meddelande om att åtgärden lyckades. Du kan klicka på **[!UICONTROL Go to notification preferences]** i meddelandet om att du har lyckats redigera din [prenumeration till meddelandekategorier](#subscribe-to-notification-categories).

   ![Meddelanden i Assets-vyn](assets/watch-assets.png)

Assets-vyn kommer nu att skicka meddelanden för de prenumerationskategorier som används. Du kan också markera flera resurser, mappar eller samlingar och klicka på **[!UICONTROL Watch]** för att spara tid. Om du markerar flera objekt och vissa redan prenumererar visas dock inte alternativet **[!UICONTROL Watch]**.

### Visa prenumererat innehåll {#view-subscribed-content}

Följ de här stegen för att visa ditt prenumererade innehåll:

1. Navigera till **[!UICONTROL Watched Assets]** under [!UICONTROL Asset Management].

1. I Assets-vyn visas en lista med prenumererade resurser, inklusive namn, typ och sökväg. Välj en resurs, mapp eller samling från listan om du vill visa information, plats eller [avbryta prenumerationen](#unsubscribe-to-content).

   ![visa prenumererat innehåll](assets/view-watched-assets.png)

### Visa innehållsprenumeranter {#view-content-subscribers}

Följ de här stegen för att visa dina innehållsprenumeranter:

1. Navigera till mappen, resursen eller samlingen och välj **[!UICONTROL Details]**.

1. Klicka på ögonikonen![ögat](assets/do-not-localize/eye-icon.png) i den högra rutan om du vill visa en lista med bevakare för innehållet.

   Du kan också klicka på ikonen ![Kommentar](assets/do-not-localize/comment-icon.svg) i den högra rutan för att visa innehållsbevakare.

### Avbeställ utskick av innehållet {#unsubscribe-to-content}

Så här säger du upp prenumerationen:

1. Gå till **[!UICONTROL Watched Assets]** under [!UICONTROL Asset Management].

1. Markera resursen, mappen eller samlingen som du vill avbryta prenumerationen på och klicka på **[!UICONTROL Unwatch]**.

   ![avsluta prenumeration på innehåll](assets/unsubscribe-assets.png)

Du kan även bläddra i mappen, resursen eller samlingen under [!UICONTROL Asset Management]. Markera [prenumerationsresursen](#subscribe-to-content) och klicka på **[!UICONTROL Unwatch]**.

## Visa meddelanden {#view-notifications}

Meddelandena visas i den högra änden av menyraden i användargränssnittet i Assets-vyn.

![Meddelanden i Assets-vyn](assets/notifications-assets-essentials.png)

När du klickar på ett meddelande navigerar Assets-vyn till rätt resurs eller mapp som det hänvisas till i meddelandet.
