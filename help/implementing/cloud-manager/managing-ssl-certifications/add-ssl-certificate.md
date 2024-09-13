---
title: Lägg till ett SSL-certifikat
description: Lär dig hur du lägger till ett eget SSL- eller DV-certifikat (Domain Validation) med Cloud Manager självbetjäningsverktyg.
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: d2f05915c0bf0af073db7f070b83f13aeae55252
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 0%

---


# Lägg till ett SSL-certifikat {#add-ssl-cert}

Lär dig hur du lägger till ett kundhanterat SSL-certifikat eller ett Adobe-genererat och hanterat DV-certifikat (Domain Validation) med Cloud Manager självbetjäningsverktyg.

Se även [Felsöka SSL-certifikatfel](/help/implementing/cloud-manager/managing-ssl-certifications/troubleshoot-ssl-cert.md).

## Lägg till ett SSL-certifikat {#adding-an-ssl-certificate}

Det kan ta några dagar innan ett certifikat etableras. Adobe rekommenderar därför att certifikatet etableras långt före ett datum för sista ansökningsdatum eller ett publiceringsdatum.

Kontrollera att du har granskat **certifikatkraven** i [Introduktion till hantering av SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md#requirements) för att se till att AEM as a Cloud Service har stöd för det certifikat som du vill lägga till.

En användare måste vara medlem i rollen **Affärsägare** eller **Distributionshanterare** för att den här aktiviteten ska kunna slutföras.

>[!NOTE]
>
>Kunder får inte överföra DV-certifikat (Domain Validation).

**Så här lägger du till ett SSL-certifikat:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. Välj programmet på konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)**.

1. Navigera från sidan **Översikt** till skärmen **Miljö**.

1. Klicka på **SSL-certifikat** under **Tjänster** på den vänstra navigeringspanelen. Om du inte ser den vänstra navigeringspanelen som i följande bild, kan du behöva klicka på ikonen för hamburgaren i det övre vänstra hörnet.

   ![Lägger till ett SSL-certifikat](/help/implementing/cloud-manager/assets/ssl/ssl-cert-add.png)

1. Klicka på **Lägg till SSL-certifikat** i sidans övre högra hörn.

1. Gör något av följande i dialogrutan **Lägg till SSL-certifikat**, baserat på [ditt användningsfall](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md):

   | | Använd skiftläge | Steg |
   | --- | --- | --- |
   | 1 | **Lägg till ett Adobe-hanterat certifikat (DV)** | **Så här lägger du till ett Adobe-hanterat certifikat (DV):**<br> a. Markera certifikattypen **Adobe hanterad (DV)**.<br>![Lägg till ett DV-certifikat](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)<br>b. I listrutan **Välj domäner** väljer du en eller flera domäner som du vill associera med DV-certifikatet.<br>Inga domäner att välja? I så fall måste du lägga till en anpassad domän. Se [Lägg till ett eget domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). När du är klar med att lägga till ett anpassat domännamn går du tillbaka till det här avsnittet och börjar på steg 1 igen.<br>d. Fortsätt till steg 7. |
   | 2 | **Lägg till ett kundhanterat certifikat (OV/EV)** | **Så här lägger du till ett kundhanterat certifikat (OV/EV):**<br> a. Välj certifikattypen **Kundhanterad (OV/EV)**.<br>b. Ange ett namn för ditt certifikat i fältet **Certifikatnamn** . Det här fältet är avsett endast som information och kan vara vilket namn som helst som gör det enkelt att referera till ditt certifikat.<br>c. I fälten **Certifikat**, **Privat nyckel** och **Certifikatkedja** klistrar du in de värden som krävs i respektive fält.<br>![Dialogrutan Lägg till SSL-certifikat](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)<br>Alla identifierade fel i värden visas. Innan du kan spara certifikatet måste du åtgärda alla fel. Mer information om hur du felsöker vanliga fel finns i [Certifikatfel](#certificate-errors).<br>d. Fortsätt till steg 7. |

<!--
    **Add an SSL certificate:**
    1. Select the certificate type **Customer managed (OV/EV)**.
    1. In **Certificate name** field, enter a name for your certificate. This field is for informational purposes only and can be any name that helps you reference your certificate easily.
    1. In the **Certificate**, **Private key**, and **Certificate chain** fields, paste the required values into their respective fields.

        ![Add SSL certificate dialog box](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)
  
    Any detected errors in values are displayed. Before you can save your certificate, you must address all errors. See [Certificate errors](#certificate-errors) to learn more about troubleshooting common errors.

    **Add a DV certificate:**
    1. Select the certificate type **Adobe managed (DV)**.

        ![Adding a DC certificate](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)

    1. In the **Select domains** drop-down list, select one or more domains that you want associated with the DV certificate.

        No domains to select? If so, it means that you must add a custom domain. See [Add a custom domain](#add-custom-domain). When you are finished, resume the steps from the beginning again. -->

1. Klicka på **Spara** i dialogrutans nedre högra hörn.

   När certifikatet har utfärdats visas en grön bockmarkering i tabellen **SSL-certifikat**.

Du har nu lagt till ett fungerande SSL-certifikat för ditt projekt. Det här steget är ofta det första som ställer in ett anpassat domännamn.

* Mer information om hur du konfigurerar ett anpassat domännamn finns i [Lägg till ett anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).
* Mer information om hur du uppdaterar och hanterar dina SSL-certifikat i Cloud Manager finns i [Hantera SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md).

<!--
### Add a custom domain {#add-custom-domain}

Before you can add an Adobe generated and managed Domain Validated (DV) certificate, you must first add a custom domain. The process for doing so is nearly the same as detailed in [Introduction to custom domain names](/help/implementing/cloud-manager/custom-domain-names/introduction.md) and [Add a custom domain name](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). However, that functionality is now slightly expanded, as described below.

1. When adding a custom domain name, in the **Verify domain** dialog box, select an **Adobe managed certificate**.

    ![Choose Adobe-managed](assets/verify-domain-dialog.png)

1. In the **Verify domain** dialog box, add a CNAME verification record to your DNS.

    ![Add CNAME entry](assets/verify-domain-dialog-adobe-managed.png)

1. After the domain is created, click the ellipsis button in the list of domains and select **Verify** to verify the domain.

    ![Verify domain](assets/verify-domain.png) 

1. Resume the task [Add a DV certificate](#adding-an-ssl-certificate). -->


