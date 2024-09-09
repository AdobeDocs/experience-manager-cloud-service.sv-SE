---
title: Lägg till ett SSL-certifikat
description: Lär dig hur du lägger till ett eget SSL- eller DV-certifikat (Domain Validation) med Cloud Manager självbetjäningsverktyg.
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: fcde1f323392362d826f9b4a775e468de9550716
workflow-type: tm+mt
source-wordcount: '966'
ht-degree: 0%

---


# Lägg till ett SSL-certifikat

Lär dig hur du lägger till ett kundhanterat SSL-certifikat eller ett Adobe-genererat och hanterat DV-certifikat (Domain Validation) med Cloud Manager självbetjäningsverktyg.


## Lägga till ett SSL- eller DV-certifikat {#adding-an-ssl-certificate}

Det kan ta några dagar innan ett certifikat etableras. Adobe rekommenderar därför att certifikatet etableras långt före ett datum för sista ansökningsdatum eller ett publiceringsdatum.

Kontrollera att du har granskat **certifikatkraven** i [Introduktion till hantering av SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md#requirements) för att se till att AEM as a Cloud Service har stöd för det certifikat som du vill lägga till.

En användare måste vara medlem i rollen **Affärsägare** eller **Distributionshanterare** för att den här aktiviteten ska kunna slutföras.

>[!NOTE]
>
>Kunder får inte överföra DV-certifikat (Domain Validation).

**Så här lägger du till ett SSL- eller DV-certifikat:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. Välj programmet på konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)**.

1. Navigera från sidan **Översikt** till skärmen **Miljö**.

1. Klicka på **SSL-certifikat** under **Tjänster** på den vänstra navigeringspanelen. Om du inte ser den vänstra navigeringspanelen som i följande bild, kan du behöva klicka på ikonen för hamburgaren i det övre vänstra hörnet.

   ![Lägger till ett SSL-certifikat](/help/implementing/cloud-manager/assets/ssl/ssl-cert-add.png)

1. Klicka på **Lägg till SSL-certifikat** i sidans övre högra hörn.

1. Gör något av följande i dialogrutan **Lägg till SSL-certifikat**, baserat på ditt specifika användningsfall:

   | Använd skiftläge | Steg |
   | --- | --- |
   | **Lägg till ett Adobe-hanterat certifikat (DV)** | **Så här lägger du till ett Adobe-hanterat certifikat (DV):**<br> a. Markera certifikattypen **Adobe hanterad (DV)**.<br>![Lägg till ett DV-certifikat](/help/implementing/cloud-manager/assets/ssl/add-dv-certificate.png)<br>b. I listrutan **Välj domäner** väljer du en eller flera domäner som du vill associera med DV-certifikatet.<br>Inga domäner att välja? I så fall måste du lägga till en anpassad domän. Se [Lägg till en anpassad domän](#add-custom-domain). När du är klar med att lägga till ett anpassat domännamn går du tillbaka till det här avsnittet och börjar på steg 1 igen.<br>d. Fortsätt till steg 7. |
   | **Lägg till ett kundhanterat certifikat (OV/EV)** | **Så här lägger du till ett kundhanterat certifikat (OV/EV):**<br> a. Välj certifikattypen **Kundhanterad (OV/EV)**.<br>b. Ange ett namn för ditt certifikat i fältet **Certifikatnamn** . Det här fältet är avsett endast som information och kan vara vilket namn som helst som gör det enkelt att referera till ditt certifikat.<br>c. I fälten **Certifikat**, **Privat nyckel** och **Certifikatkedja** klistrar du in de värden som krävs i respektive fält.<br>![Dialogrutan Lägg till SSL-certifikat](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)<br>Alla identifierade fel i värden visas. Innan du kan spara certifikatet måste du åtgärda alla fel. Mer information om hur du felsöker vanliga fel finns i [Certifikatfel](#certificate-errors).<br>d. Fortsätt till steg 7. |

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

   När certifikatet har utfärdats visas en grön bockmarkering enligt bilden ovan

   ![Utfärdat DV-certifikat](assets/issued-dv-certificate.png)

### Lägg till en anpassad domän {#add-custom-domain}

Innan du kan lägga till ett DV-certifikat (Domain Validated) som genererats och hanterats av Adobe måste du först lägga till en anpassad domän. Processen för att göra detta är nästan densamma som beskrivs i [Introduktion till anpassade domännamn](/help/implementing/cloud-manager/custom-domain-names/introduction.md) och [Lägg till ett anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). Funktionen är dock något utökad, vilket beskrivs nedan.

1. När du lägger till ett anpassat domännamn väljer du ett **Adobe-hanterat certifikat** i dialogrutan **Verifiera domän**.

   ![Välj Adobe-hanterad](assets/verify-domain-dialog.png)

1. I dialogrutan **Verifiera domän** lägger du till en CNAME-verifieringspost i din DNS.

   ![Lägg till CNAME-post](assets/verify-domain-dialog-adobe-managed.png)

1. När domänen har skapats klickar du på ellipsknappen i listan över domäner och väljer **Verifiera** för att verifiera domänen.

   ![Verifiera domän](assets/verify-domain.png)

1. Återuppta aktiviteten [Lägg till ett DV-certifikat](#adding-an-ssl-certificate).

### Felsöka certifikatfel {#certificate-errors}

Vissa fel kan uppstå om ett certifikat inte har installerats korrekt eller inte uppfyller kraven i Cloud Manager.

+++

* **Korrigera certifikatordning**

  Den vanligaste orsaken till att en certifikatdistribution misslyckas är att de mellanliggande certifikaten eller kedjecertifikaten inte är i rätt ordning.

  Mellanliggande certifikatfiler måste avslutas med rotcertifikatet eller det certifikat som ligger närmast roten. De måste vara i fallande ordning från certifikatet `main/server` till roten.

  Du kan ange ordningen för de mellanliggande filerna med följande kommando.

  ```shell
  openssl crl2pkcs7 -nocrl -certfile $CERT_FILE | openssl pkcs7 -print_certs -noout
  ```

  Du kan verifiera att den privata nyckeln och `main/server`-certifikatet matchar med följande kommandon.

  ```shell
  openssl x509 -noout -modulus -in certificate.pem | openssl md5
  ```

  ```shell
  openssl rsa -noout -modulus -in ssl.key | openssl md5
  ```

  >[!NOTE]
  >
  >Utdata för dessa två kommandon måste vara exakt likadana. Om du inte kan hitta en matchande privat nyckel för ditt `main/server`-certifikat måste du ange en ny nyckel för certifikatet genom att generera en ny CSR och/eller begära ett uppdaterat certifikat från din SSL-leverantör.

+++

+++

* **Ta bort klientcertifikat**

  Om du får ett fel som liknar det här när du lägger till ett certifikat:

  ```text
  The Subject of an intermediate certificate must match the issuer in the previous certificate. The SKI of an intermediate certificate must match the AKI of the previous certificate.
  ```

  Du har antagligen inkluderat klientcertifikatet i certifikatkedjan. Kontrollera att kedjan inte innehåller klientcertifikatet och försök igen.

+++

+++

* **Certifikatprincip**

  Om följande fel visas kontrollerar du certifikatets policy.

  ```text
  Certificate policy must conform with EV or OV, and not DV policy.
  ```

  Inbäddade OID-värden identifierar vanligtvis certifikatprinciper. Om du skriver ut ett certifikat till text och söker efter OID visas certifikatets profil.

  Du kan skriva ut din certifikatinformation som text med följande exempel som hjälp.

  ```text
  openssl x509 -in 9178c0f58cb8fccc.pem -text
  certificate:
      Data:
         Version: 3 (0x2)
         Serial Number:
             91:78:c0:f5:8c:b8:fc:cc
         Signature Algorithm: sha256WithRSAEncryption
         Issuer: C = US, ST = Arizona, L = Scottsdale, O = "GoDaddy.com, Inc.", OU = http://certs.godaddy.com/repository/, CN = Go Daddy Secure Certificate Authority - G2
          Validity
              Not Before: Nov 10 22:55:36 2021 GMT
              Not After : Dec  6 15:35:06 2022 GMT
          Subject: C = US, ST = Colorado, L = Denver, O = Alexandra Alwin, CN = adobedigitalimpact.com
          Subject Public Key Info:
  ...
  ```

  OID-mönstret i texten definierar certifikatets principtyp.

  | Mönster | Policy | Godtagbart i Cloud Manager |
  |---|---|---|
  | `2.23.140.1.1` | EV | Ja |
  | `2.23.140.1.2.2` | OV | Ja |
  | `2.23.140.1.2.1` | DV | Nej |

  Genom att `grep`pinga för OID-mönstren i utdatafälttexten kan du bekräfta din certifikatprincip.

  ```shell
  # "EV Policy"
  openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.1" -B5
  
  # "OV Policy"
  openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.2" -B5
  
  # "DV Policy - Not Accepted"
  openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.1" -B5
  ```

+++

+++

* **Certifikatets giltighetsdatum**

  Cloud Manager förväntar att SSL-certifikatet ska vara giltigt i minst 90 dagar från dagens datum. Kontrollera certifikatkedjans giltighet.

+++

## Nästa steg {#next-steps}

Du har nu lagt till ett fungerande SSL-certifikat för ditt projekt. Det här steget är ofta det första som ställer in ett anpassat domännamn.

* Mer information om hur du konfigurerar ett anpassat domännamn finns i [Lägg till ett anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).
* Mer information om hur du uppdaterar och hanterar dina SSL-certifikat i Cloud Manager finns i [Hantera SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md).
