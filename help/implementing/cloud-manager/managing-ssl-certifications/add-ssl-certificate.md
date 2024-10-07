---
title: Lägg till ett SSL-certifikat
description: Lär dig hur du lägger till ett eget SSL-certifikat eller ett Adobe-hanterat DV-certifikat (Domain Validation) med Cloud Manager självbetjäningsverktyg.
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 493c5729c3107f151685a243006b17196b74c1bd
workflow-type: tm+mt
source-wordcount: '541'
ht-degree: 0%

---


# Lägg till ett SSL-certifikat {#add-ssl-cert}

Lär dig hur du lägger till ett eget SSL-certifikat eller ett Adobe-hanterat DV-certifikat (Domain Validation) med hjälp av molnet

>[!TIP]
>
>Det kan ta några dagar innan ett certifikat etableras. Därför rekommenderar Adobe att du, om du tillhandahåller ditt eget certifikat, måste få det etablerat långt före ett datum för deadline eller en publiceringsdag.

## Förutsättningar {#prerequisites}

* En användare måste vara medlem i rollen **Business Owner** eller **Deployment Manager** för att kunna lägga till ett certifikat.
* Om du installerar ditt eget certifikat ska du kontrollera **certifikatkraven** i [Introduktion till hantering av SSL-certifikat.](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md#requirements)

## Lägga till ett SSL-certifikat {#add-certificate}

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämpligt program.
1. Välj programmet på konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)**.
1. Klicka på ![Visa menyikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) i sidans övre vänstra hörn för att visa sidomenyn.
1. Under rubriken **Tjänster** klickar du på ![Lås stängda ikoner](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **SSL-certifikat**.

   ![Lägger till ett SSL-certifikat](/help/implementing/cloud-manager/assets/ssl/ssl-cert-add.png)

1. Klicka på **Lägg till SSL-certifikat** i det övre högra hörnet på sidan SSL-certifikat.

1. Gör något av följande i dialogrutan **Lägg till SSL-certifikat**, baserat på [ditt användningsfall](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md):

   | | Använd skiftläge | Steg |
   | --- | --- | --- |
   | 1 | **Lägg till ett DV-certifikat (Adobe managed)** | **Så här lägger du till ett DV-certifikat (Adobe managed):**<br> a. I dialogrutan **Lägg till SSL-certifikat** väljer du certifikattypen **Adobe hanterad (DV)** .<br>![Lägg till ett DV-certifikat](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)<br>b. I fältet **Certifikatnamn** anger du ett namn som du vill associera med certifikatet.<br>c. I listrutan **Välj domäner** väljer du en eller flera domäner som du vill associera med DV-certifikatet.<br>Inga domäner att välja? I så fall måste du lägga till en anpassad domän. Se [Lägg till ett eget domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). När du är klar med att lägga till ett anpassat domännamn går du tillbaka till det här avsnittet och börjar på steg 1 igen.<br>d. Fortsätt till steg 7. |
   | 2 | **Lägg till ett kundhanterat (OV/EV) certifikat** | **Så här lägger du till ett kundhanterat (OV/EV) certifikat:**<br> a. I dialogrutan **Lägg till SSL-certifikat** väljer du certifikattypen **Kundhanterad (OV/EV)**.<br>b. Ange ett namn för ditt certifikat i fältet **Certifikatnamn** . Det här fältet är avsett endast som information och kan vara vilket namn som helst som gör det enkelt att referera till ditt certifikat.<br>c. I fälten **Certifikat**, **Privat nyckel** och **Certifikatkedja** klistrar du in de värden som krävs i respektive fält.<br>![Dialogrutan Lägg till SSL-certifikat](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)<br>Alla identifierade fel i värden visas. Innan du kan spara certifikatet måste du åtgärda alla fel. Mer information om hur du felsöker vanliga fel finns i [Certifikatfel](#certificate-errors).<br>d. Fortsätt till steg 7. |

1. Klicka på **Spara** i dialogrutans nedre högra hörn.

När certifikatet har utfärdats visas det med en grön bockmarkering i tabellen **SSL-certifikat** .

Du har nu lagt till ett fungerande SSL-certifikat för ditt projekt. Det här steget är ofta det första som ställer in ett anpassat domännamn.

* Mer information om hur du konfigurerar ett anpassat domännamn finns i [Lägg till ett anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).
* Mer information om hur du uppdaterar och hanterar dina SSL-certifikat i Cloud Manager finns i [Hantera SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md).

>[!TIP]
>
>Om du har problem med att lägga till eller hantera certifikat läser du dokumentet [Felsöka SSL-certifikatfel.](/help/implementing/cloud-manager/managing-ssl-certifications/troubleshoot-ssl-cert.md)
