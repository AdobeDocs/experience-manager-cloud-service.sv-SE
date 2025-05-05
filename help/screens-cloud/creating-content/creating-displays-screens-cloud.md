---
title: Skapa och hantera skärmar i Screens as a Cloud Service
description: På den här sidan beskrivs hur du skapar och hanterar visningar i Screens as a Cloud Service.
exl-id: 0f9faa4b-b50e-40f8-a8ed-280f8bd0a9b8
feature: Authoring Screens
role: Admin, Developer, User
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 2%

---

# Skapa och hantera skärmar i Screens as a Cloud Service {#create-displays-screens-cloud}

När du har publicerat kanalen är det nu dags att skapa din webbannonsering i Screens Services Provider.

En bildskärm är en virtuell gruppering av skärmar som vanligtvis placeras bredvid varandra. Bildskärmen är vanligtvis permanent när det gäller en installation. Det här objektinnehållet är det författare arbetar med och refererar alltid till som logisk visning i stället för deras fysiska motdelar.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur du skapar och hanterar visningar i Screens Services Provider. När du har läst bör du:

* Lär dig hur du skapar och tar bort skärmar
* Förstå hur du organiserar dina bildskärmar i mappar

## Steg för att skapa en visning {#create-display}

Följ stegen nedan för att skapa visningen från Screens tjänsteleverantör:

1. Gå till Screens Services Provider från din AEM Cloud Service-instans.
1. Välj **Visar** i den vänstra navigeringspanelen och klicka på **Skapa** i skärmens övre högra hörn.

   ![bild](/help/screens-cloud/assets/display/disp-1.png)

1. Välj **Visning** i åtgärdsfältet.

   ![bild](/help/screens-cloud/assets/display/disp-2.png)

1. Ange titeln som **LoopingChannelDisplay** i **Visningsnamn** och klicka på **Skapa**.

   ![bild](/help/screens-cloud/assets/display/disp3.png)

1. Visningen **LoopingChannelDisplay** visas nu i visningslistan.

   ![bild](/help/screens-cloud/assets/display/disp-4.png)

### Ta bort en visning {#deleting-display}

Du kan ta bort en visning från Screens Services Provider.

Markera visningen och klicka på **Ta bort** längst ned på panelen, vilket visas i bilden nedan.

![bild](/help/screens-cloud/assets/display/disp-5.png)

## Steg för att ordna visas i mappar {#organize-display}

## Växla mappvy {#toggle-rail}

Du kan växla mapplisten från att visa alla mappar till specifika mappar:

1. Navigera till lagervyn genom att klicka på knappen som är markerad nedan:

   ![bild](/help/screens-cloud/assets/display/display-inventory.png)

1. Mappens sidospår visas.

   ![bild](/help/screens-cloud/assets/display/toggle-rail.png)

1. Välj **Dölj mappar** om du vill stänga den igen.

## Skapa en mapp {#create-folder}

Du kan skapa mappar för att bättre ordna dina bildskärmar.

1. Navigera till lagervyn.
1. Se till att du inte befinner dig i en mapp:

   ![bild](/help/screens-cloud/assets/display/verify-view.png)

   Obs! **Alla bildskärmar** bör vara markerade i mappsidans rattar och navigeringen i vägbeskrivningar bör endast visa **bildskärmar**.

1. Klicka på knappen &quot;Skapa&quot; längst upp till höger och välj alternativet **Mapp**.

   ![bild](/help/screens-cloud/assets/display/Createfolder.png)

1. Fyll i den nya mappens namn och klicka på **Skapa**.

   ![bild](/help/screens-cloud/assets/display/Createfolder2.png)

## Skapa en kapslad mapp {#nested-folder}

1. Navigera till lagervyn.

1. Välj önskad överordnad mapp från mappens sidospår eller genom att bläddra i lagervyn.
1. Kontrollera att den önskade överordnade mappen är markerad.

   ![bild](/help/screens-cloud/assets/display/Nestedview.png)

   * Mappen ska vara markerad i mappen side rail.
   * Navigeringen i den synliga sökvägen bör visa det aktuella mappnamnet bredvid **Visar**.

1. Klicka på **Skapa** överst till höger och välj alternativet **Mapp** .

   ![bild](/help/screens-cloud/assets/display/Createfolder.png)

1. Fyll i den nya mappens namn och klicka på **Skapa**.

   ![bild](/help/screens-cloud/assets/display/Createfolder2.png)

## Flytta innehåll till en ny mapp {#move-folder}

Du kan flytta innehåll till dina nya mappar för att ordna dina bildskärmar bättre.

1. Navigera till lagervyn.

1. Välj önskad överordnad mapp från mappsidospåret eller genom att välja från lagervyn.

1. Kontrollera att du har valt den överordnade mappen.

![bild](/help/screens-cloud/assets/display/movetofolder.png)

**Obs!** Mappen ska markeras i mappsidofältet. Dessutom bör navigeringen i den synliga sökvägen visa det aktuella mappnamnet bredvid **Visar**.

## Ta bort innehåll från en mapp {#delete-folder}

Alla mappåtgärder är tillgängliga via markeringsåtgärdsfältet i lagervyn.

1. Navigera till den överordnade mappen eller markera den från sidospåret.

1. I lagervyn markerar du den underordnade mapp som du vill ta bort och ser till att den är tom.

1. Klicka på åtgärden **Ta bort** i markeringsåtgärdsfältet. Åtgärden är inaktiverad om mappen inte är tom.


## What&#39;s Next {#whats-next}

Nu när du har lärt dig hur du skapar och hanterar bildskärmar för ditt projekt bör du fortsätta din as a Cloud Service Screens-resa genom att nästa gång du granskar dokumentet [Tilldela kanal till en bildskärm i Screens as a Cloud Service](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/screens-as-cloud-service/create-content/assigning-channels-to-display.html?lang=sv-SE).
