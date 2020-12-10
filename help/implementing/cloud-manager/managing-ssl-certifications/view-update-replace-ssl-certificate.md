---
title: 'Visa Uppdatera och ersätta ett SSL-certifikat - Hantera SSL '
description: Visa Uppdatera och ersätta ett SSL-certifikat - Hantera SSL-certifikat
translation-type: tm+mt
source-git-commit: 54171b90f99a14fd43c4dc01308264b9a954b927
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---


# Visa och uppdatera och ersätta ett SSL-certifikat {#view-update-replace-ssl-certificate}

## Visa och uppdatera ett SSL-certifikat {#view-update}

När du ska använda de här alternativen i användargränssnittet i Cloud Manager:

* Ett befintligt certifikat håller på att upphöra att gälla. Användaren har förnyat certifikatet med certifikatleverantören och vill ersätta det befintliga certifikatet som håller på att gå ut. Obs! Endast användare med rätt behörighet kan göra uppdateringar.
* Använd menyn **Visa och uppdatera** om du bara vill visa SSL-certifikatinformationen.
* Du kan också ändra namnet som har använts för att referera till ett certifikat från den här skärmen.
   >[!NOTE]
   >Endast användare med rätt behörighet kan göra uppdateringar.


## Uppdaterar ett SSL-certifikat som ska upphöra {#update-ssl-certificate}

>[!NOTE]
>När ett certifikat upphör att gälla fungerar inte längre domäner som används med det utgångna certifikatet. Om du vill uppdatera ett certifikat som har upphört att gälla måste du följa stegen nedan. Detta säkerställer att din domän fortsätter att fungera som du vill. Om du lägger till ett nytt certifikat måste du uppdatera det anpassade domännamnet med det nya certifikatet innan domänerna fungerar som du vill. Mer information finns i [Visa och uppdatera och ersätta ett anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/view-update-replace-custom-domain-name.md)för mer information

Följ stegen nedan för att uppdatera ett SSL-certifikat:

>[!NOTE]
>En användare måste ha rollen Business Owner eller Deployment Manager för att kunna uppdatera ett SSL-certifikat i Cloud Manager.

1. Navigera till SSL-certifikatsskärmen från sidan **Miljöer**.
1. En tabell med en rad för varje SSL-certifikat som har installerats i programmet visas.
1. Du kan komma åt menyalternativen för varje rad genom att markera de tre knapparna längst till höger på raden.
1. Välj **Visa och uppdatera**. Certifikatinformationen kan visas härifrån.

## Ersätta ett SSL-certifikat {#replace-ssl-certificate}

Följ stegen nedan för att ersätta ett SSL-certifikat:

1. Navigera till SSL-certifikatsskärmen från sidan **Miljöer**.
1. En tabell med en rad för varje SSL-certifikat som har installerats i programmet visas.
1. Du kan komma åt menyalternativen för varje rad genom att markera de tre knapparna längst till höger på raden.
1. Välj **Visa och uppdatera**.
1. Om du vill ersätta certifikatet klistrar du in det nya innehållet i motsvarande inmatningsfält och klickar på **Spara**. Du måste åtgärda eventuella fel som kan uppstå.

   Läs [Certifikatfel](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md#certificate-error) om du vill arbeta med vanliga problem.