---
title: Lägg till ett SSL-certifikat
description: Lär dig hur du lägger till ett eget SSL-certifikat eller ett Adobe-hanterat DV-certifikat (Domain Validation) med Cloud Manager självbetjäningsverktyg.
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 603602dc70f9d7cdf78b91b39e3b7ff5090a6bc0
workflow-type: tm+mt
source-wordcount: '1021'
ht-degree: 0%

---


# Lägg till ett SSL-certifikat {#add-ssl-cert}

Lär dig hur du lägger till ett eget SSL-certifikat eller ett Adobe-hanterat DV-certifikat (Domain Validation) med hjälp av molnet

>[!NOTE]
>
>Om du använder ett kundhanterat (OV/EV) SSL-certifikat och en kundhanterad CDN-leverantör, kan du hoppa över att lägga till ett SSL-certifikat och gå direkt till [Lägg till en domänmappning](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md) när det är klart.

Det kan ta flera dagar att etablera ett certifikat. Därför rekommenderar Adobe att du etablerar ditt eget certifikat långt före ett visst datum för deadline eller en viss tid för att undvika förseningar.

Mer information om hur du uppdaterar och hanterar dina SSL-certifikat i Cloud Manager finns i [Hantera SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md).

Om du har problem med att lägga till eller hantera certifikat kan du läsa [Felsöka SSL-certifikatfel](/help/implementing/cloud-manager/managing-ssl-certifications/troubleshoot-ssl-cert.md).


## Förutsättningar {#prerequisites}

* En användare måste vara medlem i rollen **Business Owner** eller **Deployment Manager** för att lägga till ett SSL-certifikat.
* Om du installerar ditt eget certifikat kan du läsa **Certifikatkrav** i [Introduktion till hantering av SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md#requirements).

## Välja vilket SSL-certifikat som ska läggas till {#which-ssl-to-add}

När du har [lagt till ett anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) i AEM Cloud Manager beror nästa steg på om du väljer att använda ett Adobe-hanterat (DV) SSL-certifikat (rekommenderas) eller ett kundhanterat (OV/EV) SSL-certifikat.

* **För ett SSL-certifikat som hanteras av Adobe (DV):**
   * Domänvalideringsprocessen utförs när den anpassade domänen har lagts till och verifierats i Cloud Manager.
   * Nu måste du [lägga till ett Adobe-hanterat (DV) SSL-certifikat](#add-adobe-managed-ssl-cert).
När du har lagt till det i Cloud Manager väntar du tills Adobe har utfärdat och installerat DV SSL-certifikatet åt dig.
   * När certifikatet är aktivt är din anpassade domän klar att användas.

* **För ett SSL-certifikat som hanteras av en kund (OV/EV):**

   * Hämta ditt OV/EV SSL-certifikat från en certifikatutfärdare. Mer information finns i [kraven för kundhanterade OV/EV SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md#requirements).
   * [Lägg till information om ditt kundhanterade (OV/EV) SSL-certifikat &#x200B;](#add-customer-managed-ssl-cert) i Cloud Manager när certifikatet har förvärvats.
   * När du har lagt till det anpassade domännamnet markeras det som verifierat och SSL-certifikatet används.

I båda fallen är den anpassade domänen tillgänglig för säker användning i din miljö när certifikatet har verifierats och installerats. [Kontrollera domänens status](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md) i Cloud Manager-gränssnittet regelbundet för att kontrollera att allt fungerar som det ska.

Se även [Introduktion till SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md).

## Lägg till ett Adobe-hanterat (DV) SSL-certifikat {#add-adobe-managed-ssl-cert}

Behöver du hjälp med att välja om du vill använda ett Adobe-hanterat SSL-certifikat (rekommenderas) eller ett kundhanterat SSL-certifikat med din domän? Se [Välja vilket SSL-certifikat som ska läggas till](#which-ssl-to-add)

**Så här lägger du till ett Adobe-hanterat (DV) SSL-certifikat:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämpligt program.
1. Välj programmet på konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)**.
1. Klicka på ![Visa menyikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) i sidans övre vänstra hörn för att visa sidomenyn.

1. Under rubriken **Tjänster** klickar du på ![Lås stängda ikoner](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **SSL-certifikat**.

   ![Lägger till ett SSL-certifikat](/help/implementing/cloud-manager/assets/ssl/ssl-cert-add.png)

1. Klicka på **Lägg till SSL-certifikat** i det övre högra hörnet på sidan SSL-certifikat.

1. I dialogrutan **Lägg till SSL-certifikat**, baserat på [ditt användningsfall](#which-ssl-to-add), väljer du **Adobe Managed (DV)**.

   ![Lägg till ett DV-certifikat](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)

1. I fältet **Certifikatnamn** anger du ett namn som du vill associera med DV SSL-certifikatet.

1. I listrutan **Välj domäner** väljer du en eller flera verifierade domäner som du vill associera med DV SSL-certifikatet.
   * Inga domäner att välja? I så fall måste du först [lägga till ett anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) och kontrollera att det är verifierat innan du kan lägga till ett Adobe-hanterat SSL-certifikat.
   * När du är klar med att lägga till ett anpassat domännamn går du tillbaka till det här avsnittet och börjar på steg 1 igen.

1. Klicka på **Spara** i dialogrutans nedre högra hörn.

   När SSL-certifikatet har utfärdats visas det med en grön giltig bockmarkering i tabellen **SSL-certifikat** .

Du har nu lagt till ett fungerande Adobe-hanterat DV SSL-certifikat för ditt projekt. Det här steget är ofta det första som ställer in ett anpassat domännamn.

Du kan nu lägga till en [CDN-konfiguration](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md).

## Lägg till ett OV/ED-SSL-certifikat (Customer managed) {#add-customer-managed-ssl-cert}

<!-- IF THIS TOPIC GET UPDATED, REMEMBER TO UPDATE THE STEPS ALSO IN THE "MANAGE SSL CERTIFICATES TOPIC TOO -->

Behöver du hjälp med att välja om du vill använda ett Adobe-hanterat SSL-certifikat (rekommenderas) eller ett kundhanterat SSL-certifikat med din domän? Se [Välja vilket SSL-certifikat som ska läggas till](#which-ssl-to-add)

>[!IMPORTANT]
>
>När du lägger till eller uppdaterar ett SSL-certifikat ska du inte ta med det nya certifikatet i certifikatkedjan. Den förhindrar att överföringen slutförs korrekt.

**Så här lägger du till ett kundhanterat (OV/EV) SSL-certifikat:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämpligt program.

1. Välj programmet på konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)**.

1. Klicka på ![Visa menyikon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) i sidans övre vänstra hörn för att visa sidomenyn.

1. Under rubriken **Tjänster** klickar du på ![Lås stängda ikoner](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **SSL-certifikat**.

   ![Lägger till ett SSL-certifikat](/help/implementing/cloud-manager/assets/ssl/ssl-cert-add.png)

1. Klicka på **Lägg till SSL-certifikat** i det övre högra hörnet på sidan SSL-certifikat.

1. Välj **Kundhanterad (OV/EV)** i dialogrutan **Lägg till SSL-certifikat**, baserat på [ditt användningsfall](#which-ssl-to-add).

1. Ange ett namn för ditt certifikat i fältet **Certifikatnamn**.
Det här fältet är avsett endast som information och kan vara vilket namn som helst som gör det enkelt att referera till ditt SSL-certifikat.

1. Kopiera de obligatoriska värdena från OV- eller EV SSL-certifikatet i fälten **Certifikat**, **Privat nyckel** och **Certifikatkedja** och klistra in dem i respektive fält i dialogrutan.

   Alla identifierade fel i värden visas. Innan du kan spara certifikatet måste du åtgärda alla fel. Mer information om hur du felsöker vanliga fel finns i [Certifikatfel](#certificate-errors).

   ![Dialogrutan Lägg till SSL-certifikat](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)|

1. Klicka på **Spara** i dialogrutans nedre högra hörn.

   >[!NOTE]
   >
   >* Om du valde **Kundhanterat certifikat** när du [lade till ett anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) verifieras domänen ***efter*** att det kundhanterade (OV/EV) SSL-certifikatet har lagts till och sparats. Se även [Kontrollera status för ett anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#how-to).

   När SSL-certifikatet har utfärdats visas det med en grön verifierad bock i tabellen **SSL-certifikat** .

Du har nu lagt till ett fungerande SSL-certifikat för ditt projekt. Det här steget är ofta det första som ställer in ett anpassat domännamn.

Du kan nu lägga till en [CDN-konfiguration](/help/implementing/cloud-manager/domain-mappings/add-domain-mapping.md).























<!--
## Add an SSL certificate {#add-ssl-cert}

1. Log into Cloud Manager at [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) and select the appropriate program.
1. On the **[My Programs](/help/implementing/cloud-manager/navigation.md#my-programs)** console, select the program.
1. In the upper-left corner of the page, click ![Show menu icon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_ShowMenu_18_N.svg) to reveal the side menu. 
1. Under the **Services** heading, click ![Lock closed icon](https://spectrum.adobe.com/static/icons/workflow_18/Smock_LockClosed_18_N.svg) **SSL Certificates**. 

   ![Adding an SSL certificate](/help/implementing/cloud-manager/assets/ssl/ssl-cert-add.png)

1. Near the upper-right corner of the SSL Certificates page, click **Add SSL Certificate**.

1. In the **Add SSL certificate** dialog box, based on [your particular use case](/help/implementing/cloud-manager/managing-ssl-certifications/introduction-to-ssl-certificates.md), do one of the following:

    | | Use case | Steps |
    | --- | --- | --- |
    | 1 | **Add an Adobe managed (DV) certificate** | **To add an Adobe managed (DV) SSL certificate:**<br>a. In the **Add SSL Certificate** dialog box, select the certificate type **Adobe managed (DV)**.<br>![Add a DV certificate](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)<br>b. In the **Certificate name** field, enter a name you want associated with the certificate.<br>c. In the **Select domains** drop-down list, select one or more domains that you want associated with the DV SSL certificate.<br>No domains to select? If so, it means that you must first add a custom domain name and ensure it is verified before you can add an SSL certificate. See [Add a custom domain name](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). When you are finished adding a custom domain name, return to this topic and begin at step 1 again.<br>d. Continue to step 7. |
    | 2 | **Add a customer managed (OV/EV) certificate** | **To add a customer managed (OV/EV) SSL certificate:**<br>a. In the **Add SSL Certificate** dialog box, select the certificate type **Customer managed (OV/EV)**.<br>b. In the **Certificate name** field, enter a name for your certificate. This field is for informational purposes only and can be any name that helps you reference your SSL certificate easily.<br>c. In the **Certificate**, **Private key**, and **Certificate chain** fields, paste the required values into their respective fields.<br>![Add SSL certificate dialog box](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)<br>Any detected errors in values are displayed. Before you can save your certificate, you must address all errors. See [Certificate Errors](#certificate-errors) to learn more about troubleshooting common errors.<br>d. Continue to step 7. | 

1. In the lower-right corner of the dialog box, click **Save**.

    >[!NOTE]
    >
    >* If you selected **Adobe managed certificate** while [adding a custom domain name](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md), the domain is verified with the added certificate when the custom domain is added. 
    >
    >* If you selected **Customer managed certificate** while [adding a custom domain name](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md), the domain is verified ***after*** the customer managed (OV/EV) SSL certificate is added and saved. See also [Check the status of a custom domain name](/help/implementing/cloud-manager/custom-domain-names/check-domain-name-status.md#how-to).

    After the SSL certificate is successfully issued, it is displayed with a green verified check mark in the **SSL Certificates** table. 

    You now have added a working SSL certificate for your project. This step is often the first to set up a custom domain name. 
    

* To learn about updating and managing your SSL certificates in Cloud Manager, see [Manage SSL certificates](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md).

* If you are having issues adding or managing your certificates, see [Troubleshoot SSL certificate errors](/help/implementing/cloud-manager/managing-ssl-certifications/troubleshoot-ssl-cert.md). -->
