---
title: Hantera meddelanden
description: Övervaka åtgärderna som utförs på de resurser eller mappar som är tillgängliga i databasen med meddelanden i resursvyn.
source-git-commit: c3076ce35128c147ce2056d11d9305d9a9456636
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 0%

---

# Titta på resurser, mappar och samlingar {#watch-assets-folders}

Med meddelanden i resursvyn kan du övervaka åtgärder som utförs för resurser, mappar och samlingar som är tillgängliga i databasen. Du måste välja och prenumerera på det innehåll som meddelandena skickas till dig för. Du kan också konfigurera de kategorier som meddelanden skickas till dig för.

## Prenumerera på meddelandekategorier {#subscribe-to-notification-categories}

Du kan välja och prenumerera från en lista med kategorier för att få meddelanden. Resursvyn skickar endast meddelanden till dig för de kategorier som du väljer bland de tillgängliga alternativen:

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

1. Klicka ![klockikon](assets/bell-icon.svg) till höger i menyraden i användargränssnittet i resursvyn.

1. Klicka ![inställningsikon](assets/settings-icon.svg) för att visa [!UICONTROL Experience Cloud preferences] sida.

1. Klicka på **[!UICONTROL Notifications]** i den vänstra rutan.

1. I **[!UICONTROL Notifications]** -avsnittet, navigera till [!UICONTROL Assets view] och se till att växlingsalternativet är aktiverat.

   ![Meddelanden i resursvyn](assets/enable-notifications.png)

1. Klicka **[!UICONTROL Customize]** för att visa meddelandekategorierna.
   ![Meddelanden i resursvyn](assets/enable-notification-categories.png)

1. Välj de meddelandekategorier för vilka du måste få meddelanden.

## Titta på och ta bort bevakade mappar, resurser och samlingar {#watch-unwatch-assets}

Efter [prenumerera på meddelandekategorierna](#subscribe-to-notification-categories)måste du prenumerera på innehållet för att få meddelanden.

>[!NOTE]
>
>* För **[!UICONTROL Requests]** och **[!UICONTROL Assigned to me]** meddelandekategorier behöver du inte prenumerera på innehållet efter att du har prenumererat på meddelandekategorierna. Meddelanden skickas automatiskt till dig för förfrågningar som du har skapat och när en uppgift har tilldelats dig.
>* Resursvyn skickar endast meddelanden när andra användare utför åtgärder på det prenumererade innehållet. Du får inga meddelanden om vilka åtgärder du utför på det prenumererade innehållet.

Om du vill prenumerera på innehållet väljer du den mapp, resurs eller samling som du vill prenumerera på och klickar på **[!UICONTROL Watch]**.

Resursvyn visar ett meddelande om att åtgärden lyckades. Klicka **[!UICONTROL Go to notification preferences]** finns i meddelandet om att åtgärden lyckades redigera [prenumeration på meddelandekategorier](#subscribe-to-notification-categories).

![Meddelanden i resursvyn](assets/watch-assets.png)

Resursvyn skickar nu meddelanden för de prenumererade kategorierna. Du kan också markera flera resurser, mappar eller samlingar och klicka på **[!UICONTROL Watch]** för att spara tid. Om du väljer flera enheter som några av dem redan prenumererat på, kan du **[!UICONTROL Watch]** alternativet visas inte.

Om du vill avbryta prenumerationen markerar du resursen, mappen eller samlingen som du prenumererar på och klickar på **[!UICONTROL Unwatch]**.

## Visa meddelanden {#view-notifications}

Meddelandena visas i den högra änden av menyraden i användargränssnittet i resursvyn.

![Meddelanden i resursvyn](assets/notifications-assets-essentials.png)

När du klickar på ett meddelande navigerar resursvyn till lämplig resurs eller mapp som refereras till i meddelandet.
