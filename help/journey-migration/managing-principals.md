---
title: Hantera huvudkonton
description: Hantera huvudmål för migrering, med Admin Console
source-git-commit: 5bf497fb2122cc3d3ff0903aeb680a35e90f33b0
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---


# Hantera huvudkonton {#managing-principals}

>[!CONTEXTUALHELP]
>id="aemcloud_ctt_managingprincipals"
>title="Hantera huvudkonton"
>abstract="Läs vad som behöver göras för att hantera användare under eller efter en innehållsmigrering"

Innan innehåll överförs till AEM as a Cloud Service molnmiljö finns det några uppgifter som kan utföras på Admin Console.  De är: skapa användare, skapa grupper och tilldela användare till grupper. Dessa användare och grupper finns i IMS, Adobe Identity Management Service, som används för att hantera användare och grupper för alla molnbaserade Adobe-tjänster.

### Skapa grupper och deras användare i Admin Console

[Om du använder Admin Console för AEM iOS](https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/security/ims-support#how-to-set-up) får du detaljerade anvisningar om hur du skapar användare och grupper i IMS och hur du lägger till användare i grupperna samtidigt eller senare.  Dokumentet innehåller tre alternativ för att skapa dem: Manuellt via Admin Console, via CSV-överföring via Admin Console och via ett användarsynkroniseringsverktyg.

Med det manuella alternativet kan du skapa en grupp eller användare åt gången, med CSV-överföringen kan du skapa och länka flera användare och grupper samtidigt och med verktyget för användarsynkronisering kan du använda en befintlig IDP för att skapa och hantera IMS-användare och -grupper.

När en användare använder IMS för att logga in AEM skapas en AEM av användaren.  Dessutom kommer alla IMS-grupper som användaren ingår i att ha motsvarande AEM i AEM.  Dessa IMS-skapade AEM-användare och grupper hanteras fortfarande huvudsakligen med Admin Console.

När innehållsmigreringen är klar behöver IMS-grupper vanligtvis ha ytterligare konfigurationer så att användarna kan komma åt det migrerade innehållet.  Se [Migrera huvudmål efter migrering](/help/journey-migration/managing-principals-after-migration.md)

Se även [Självstudiekurs, AEM användare, grupper och behörigheter](https://experienceleague.adobe.com/sv/docs/experience-manager-learn/cloud-service/accessing/aem-users-groups-and-permissions) om du vill veta mer om hur AEM och IMS-användare och IMS-grupper integreras och administreras.