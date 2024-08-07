---
title: Tilldela kanal till en skärm i Screens as a Cloud Service
description: På den här sidan beskrivs hur du tilldelar en kanal till en visning i Screens as a Cloud Service.
exl-id: ba001c18-7b05-4ae2-aa7f-9ebb320fedd0
feature: Authoring Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '444'
ht-degree: 0%

---

# Tilldela kanal till en skärm i Screens as a Cloud Service {#assign-channel-displays-screens-cloud}

När projektkonfigurationen är klar måste du tilldela kanalen till en skärm för att kunna visa innehållet.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur du tilldelar en kanal till en bildskärm när bildskärmen är klar och du har lagt till innehåll i kanalen och publicerat den. Efter läsningen bör du förstå hur du tilldelar en kanal till en skärm från Screens Services Provider.

## Förutsättningar {#prerequisites}

Innan du utför stegen nedan för att tilldela en kanal till en skärm måste du ha lärt dig:

* Skapa och hantera skärmar
* Skapa och hantera kanaler

## Steg för att tilldela en kanal till en visning {#assign-channel-to-display}

Följ stegen nedan för att tilldela en kanal till en skärm:

1. Navigera till Screens Services Provider och välj **Visar** i den vänstra navigeringspanelen.

1. Klicka på **Tilldela kanal** för att visa.

   ![bild](/help/screens-cloud/assets/display/assignchannel-1.png)

1. Fyll i följande fält från dialogrutan **Tilldela en kanal**.

   ![bild](/help/screens-cloud/assets/display/assignchannel-2.png)

   1. Välj kanalnamnet i listrutan.
   1. Välj prioritet.

      >[!NOTE]
      >Prioritet används för att ordna tilldelningarna om flera matchar uppspelningsvillkoren. Den som har det högsta värdet har alltid företräde framför de lägre värdena. Om det till exempel finns två kanaler A och B. A har prioriteten 1 och B har prioriteten 2, och sedan visas kanal B eftersom den har högre prioritet än A.

   1. Välj startdatum och slutdatum från **Aktivering**.

1. Klicka på **+ Lägg till upprepning** för att lägga till ett upprepningsschema för kanalen.

   ![bild](/help/screens-cloud/assets/create-content/recurrence-1.png)

   >[!NOTE]
   >Du kan lägga till flera återkommande scheman i din kanal. Upprepningsscheman introducerar DayParting som gör att du kan ställa in ett globalt schema med flera kanaler som körs vid specifika tidpunkter på dagen och återanvända det som är inställt för alla skärmar samtidigt.

   Du kan ange följande alternativ:

   * **Namn**: Rubrik för upprepningsschemat.
   * **Upprepa**: Välj om schemat ska köras varje dag, varje vecka, varje månad eller varje år.
   * **Start**: Starttiden för schemat.
   * **Slut**: Sluttiden för schemat. Du kan ange den efter tid eller varaktighet.
   * **Tid**: Schemat avslutas vid en angiven tidpunkt.
   * **Varaktighet**: Schemat körs för en viss tid i timmar eller minuter.

1. Klicka på **Skapa**. Du ser att en kanal har tilldelats för den visningen, vilket visas i bilden nedan.

   ![bild](/help/screens-cloud/assets/display/assignchannel-3.png)


## What&#39;s Next {#whats-next}

Nu när du har tilldelat kanalen till en skärm bör du fortsätta din as a Cloud Service Screens-resa genom att gå igenom dokumentet [Installera och konfigurera Screens Player för AEM as a Cloud Service](/help/screens-cloud/managing-players-registration/installing-screens-cloud-player.md) nästa gång.
