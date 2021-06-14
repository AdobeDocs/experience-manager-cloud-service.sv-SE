---
title: Tilldela kanal till en skärm på skärmar som en Cloud Service
description: På den här sidan beskrivs hur du tilldelar en kanal till en skärm på skärmar som en Cloud Service.
hide: true
hidefromtoc: true
index: false
source-git-commit: c65eeaf74ddfd81d37eb7090b84c8bf6f876dc72
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 1%

---


# Tilldela kanal till en skärm på skärmar som en Cloud Service {#assign-channel-displays-screens-cloud}

När projektkonfigurationen är klar måste du tilldela kanalen till en skärm för att kunna visa innehållet.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur du tilldelar en kanal till en bildskärm när bildskärmen är klar och du har lagt till innehåll i kanalen och publicerat den. När du har läst bör du kunna förstå hur du tilldelar en kanal till en skärm från leverantören av skärmtjänster.

## Förutsättningar {#prerequisites}

Innan du utför stegen nedan för att tilldela en kanal till en skärm måste du ha lärt dig:

* Skapa och hantera skärmar
* Skapa och hantera kanaler

## Steg för att tilldela en kanal till en visning {#assign-channel-to-display}

Följ stegen nedan för att tilldela en kanal till en skärm:

1. Navigera till Screens Services Provider och välj **Visar** i den vänstra navigeringspanelen.

1. Klicka på **Tilldela kanal** till visningen.

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
   >Du kan lägga till flera återkommande scheman i din kanal. I scheman för återkommande aktiviteter introduceras DayParting, som gör att du kan ställa in ett globalt schema med flera kanaler som körs vid specifika tidpunkter på dagen, och återanvända inställningen för alla skärmar samtidigt.

   Du kan ange följande alternativ:

   * **Namn**: Namn på ditt återkommande schema.
   * **Upprepa**: Välj om schemat ska köras varje dag, varje vecka, varje månad eller varje år.
   * **Start**: Starttiden för ditt schema.
   * **Slut**: Sluttiden för ditt schema. Du kan ställa in den efter tid eller varaktighet.
   * **Tid**: Schemat avslutas vid en angiven tidpunkt.
   * **Varaktighet**: Schemat körs för en viss tidsperiod i timmar eller minuter.

1. Klicka på **Skapa** så ser du nu att en kanal har tilldelats för den visningen, vilket visas i bilden nedan.

   ![bild](/help/screens-cloud/assets/display/assignchannel-3.png)


## What&#39;s Next {#whats-next}

Nu när du har tilldelat kanalen till en skärm bör du fortsätta att använda Cloud Servicen som en skärmresa genom att nästa gång du granskar dokumentet **Installera och konfigurera skärmspelaren för AEM som en Cloud Service**.
