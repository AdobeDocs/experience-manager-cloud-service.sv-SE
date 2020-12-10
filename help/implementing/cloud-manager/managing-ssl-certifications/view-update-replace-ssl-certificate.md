---
title: 'Visa Uppdatera och ersätta ett SSL-certifikat - Hantera SSL '
description: Visa Uppdatera och ersätta ett SSL-certifikat - Hantera SSL-certifikat
translation-type: tm+mt
source-git-commit: d1301d4414f87b30f5ab732eacbb61c96f102262
workflow-type: tm+mt
source-wordcount: '338'
ht-degree: 0%

---


# Visa och uppdatera och ersätta ett SSL-certifikat {#view-update-replace-ssl-certificate}

## Visa och uppdatera ett SSL-certifikat {#view-update}

När du ska använda det här alternativet i användargränssnittet i Cloud Manager:

* Ett befintligt certifikat håller på att upphöra att gälla. Användaren har förnyat certifikatet med certifikatleverantören och vill ersätta det befintliga certifikatet som håller på att gå ut. Obs! Endast användare med rätt behörighet kan göra uppdateringar.
* Använd menyn Visa och uppdatera för att visa SSL-certifikatsinformationen.
* Du kan också ändra namnet som har använts för att referera till ett certifikat från den här skärmen.
   >[!NOTE]
   >Endast användare med rätt behörighet kan göra uppdateringar.


## Uppdaterar ett SSL-certifikat som ska upphöra {#update-ssl-certificate}


>[!NOTE]
>När ett certifikat upphör att gälla fungerar inte längre domäner som används med det utgångna certifikatet. Om du vill uppdatera ett certifikat som har upphört att gälla måste du följa stegen nedan. Detta säkerställer att din domän fortsätter att fungera som du vill. Om du lägger till ett nytt certifikat måste du uppdatera det anpassade domännamnet med det nya certifikatet innan domänerna fungerar som du vill. Mer information finns i Visa och uppdatera anpassat domännamn

Följ stegen nedan för att uppdatera ett SSL-certifikat:

>[!NOTE]
>En användare måste ha rollen Business Owner eller Deployment Manager för att kunna uppdatera ett SSL-certifikat i Cloud Manager.

1. Navigera till SSL-certifikatsskärmen från sidan **Miljöer**.
1. En tabell med en rad för varje SSL-certifikat som har installerats i programmet visas.
1. Du kan komma åt menyalternativen för varje rad genom att markera de tre knapparna längst till höger på raden. Här väljer du Visa och uppdatera. Certifikatinformationen kan visas härifrån enligt exemplet nedan.
1. Om du vill ersätta certifikatet klistrar du in det nya innehållet i motsvarande inmatningsfält och sparar. Du måste åtgärda eventuella fel som kan uppstå. Se avsnittet Certifikatfel om du vill arbeta med vanliga problem.