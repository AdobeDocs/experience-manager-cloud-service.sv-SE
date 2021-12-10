---
title: Konfigurera inställningar för frånvaro
seo-title: Configure Out of Office settings
description: Konfigurera inställningar för frånvaro
seo-description: Configure Out of Office settings
exl-id: c7e436f1-8e1c-4334-b3dc-ab9800695301
source-git-commit: 7163eb2551f5e644f6d42287a523a7dfc626c1c4
workflow-type: tm+mt
source-wordcount: '755'
ht-degree: 0%

---

# Konfigurera frånvaroinställningar {#configure-out-of-office-settings}

Om du tänker vara utanför kontoret kan du ange vad som ska hända med artiklar som har tilldelats dig för den perioden.

Du kan ange startdatum och -tid och slutdatum och sluttid så att dina inställningar som inte är på kontoret börjar gälla. Om du befinner dig i en annan tidszon än servern används den tidszon som klienten använder.

Du kan ange en standardperson som alla dina objekt skickas till. Du kan också ange undantag för objekt från specifika processer som ska skickas till en annan användare eller behållas i inkorgen tills du kommer tillbaka. Om den utsedda personen även är utanför kontoret, skickas objektet till användaren som han/hon har utsett. Om objektet inte kan tilldelas till en användare som inte är utanför kontoret finns objektet kvar i din inkorg.

Du kan dela upp objektdelegering baserat på arbetsflödesmodellerna. Du kan till exempel tilldela ett objekt som är relaterat till arbetsflöde A till användare A och tilldela ett objekt som är relaterat till arbetsflöde B till användare B.


>[!NOTE]
>
>* När du aktiverar inställningen Frånvarande finns alla objekt som är tillgängliga i Inkorgen, innan inställningen aktiveras, kvar i Inkorgen. Endast objekt som tagits emot efter att inställningen aktiverats delegeras.
>* När du inaktiverar inställningen Frånvarande tilldelas de delegerade objekten inte tillbaka till dig automatiskt. Du kan använda anspråksfunktionen för att tilldela objekt till dig.
>* När Användare A delegerar objekt till Användare B och Användare B delegerar vidare till Användare C, tilldelas objekten bara Användare C och inte Användare B.
>* När det finns en slinga i uppdraget stannar uppgifterna kvar hos den ursprungliga användaren. När Användare A till exempel delegerar objekt till Användare B till Användare C, Användare C delegerar till Användare D och Användare D delegerar till Användare B skapas en slinga. I sådana fall behålls objektet av den ursprungliga användaren. Användare A är ursprunglig användare i ovanstående exempel.


## Aktivera inställningen Frånvarande för ditt konto {#enable-out-of-office}

Utför följande steg för att aktivera inställningen Frånvarande för ditt konto och delegera dina inkorgsobjekt till en annan användare:

1. Logga in på din AEM. Tryck på ![Inkorg](assets/bell.svg) ikon och tryck **[!UICONTROL View All]**. En lista över dina inkorgsobjekt visas.
1. Tryck på ![Visa väljare](assets/viewlist.svg) eller ![Visa väljare](assets/calendar.svg) -ikonen bredvid **[!UICONTROL Create]** knapp och knacka **[!UICONTROL Settings]**. Dialogrutan Inställningar visas.
1. Öppna **[!UICONTROL Out of Office]** i inställningsdialogrutan.
1. Tryck på **[!UICONTROL Enable/Disable]** om du vill aktivera inställningen Frånvarande.
1. Ange **[!UICONTROL Start Time]**  och **[!UICONTROL End Time]** för inställningen. Objekten delegeras endast under den angivna perioden. Lämna **[!UICONTROL End Time]** fältet är tomt för att delegera objekt för en obestämd tidsperiod.
1. Välj **[!UICONTROL Forward my items during this period]** kryssrutan. Om du inte markerar alternativet och inte anger en tilldelad användare, vidarebefordras inte objekten till någon användare. Även om du är borta och inställningen är aktiverad finns objekten kvar i Inkorgen.
1. Tryck på **[!UICONTROL Add Assignee]**. Ange en användare i **[!UICONTROL Assignee]** fält som objekten ska delegeras till. Ange **[!UICONTROL Workflow Model]** för att delegera till den angivna användaren. Du kan välja mer än en arbetsflödesmodell.

   Om du dessutom vill tilldela alla objekt, oavsett arbetsflödesmodell, till en viss användare väljer du **[!UICONTROL All Workflows]** i listrutan Arbetsflödesmodell. <br>

   Om du vill tilldela objekt till en viss användare för alla arbetsflödesmodeller utom ett fåtal, väljer du **[!UICONTROL All Workflows]** i listrutan Arbetsflödesmodell: tryck **[!UICONTROL + Add Exceptions]**och ange vilka arbetsflödesmodeller som ska utelämnas.
   <br>

   Upprepa steget för att lägga till fler tilldelningar. <br>

   >[!NOTE]
   >
   >Tilldelningsordningen är viktig. När ett objekt tilldelas en användare som har aktiverat inställningen Frånvarande utvärderas objektet mot den angivna listan över tilldelningar i den ordning som tilldelningarna läggs till. När ett objekt matchar villkoret tilldelas det till den som tilldelats objektet och nästa tilldelande kontrolleras inte.

1. Tryck på **[!UICONTROL Save]**. Inställningen börjar gälla vid angivet startdatum och angiven starttid. Om du loggar in när du inte är på kontoret beaktas du inte på kontoret förrän du ändrar dina inställningar.

Nu tilldelas objekt som du har tilldelats under frånvaroperioden automatiskt till den angivna tilldelade personen.
![Utanför kontoret](assets/out-of-office.png)

>[!NOTE]
>
>(Endast för Forms-centrerade arbetsflödesobjekt) Aktivera **[!UICONTROL Allow assignee to delegate using 'Out of Office' settings]** alternativ för **[!UICONTROL Assign task]** i arbetsflödet. Endast objekt som har det ovannämnda alternativet aktiverat delegeras till andra användare.

## Begränsningar {#limitations}

* Det går inte att tilldela objekt till en grupp.
* Det går för närvarande inte att aktivera frånvaro för projektaktiviteter.
