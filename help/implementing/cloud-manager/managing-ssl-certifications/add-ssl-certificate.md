---
title: Lägg till ett SSL-certifikat
description: Lär dig hur du lägger till ett eget SSL-certifikat med Cloud Manager självbetjäningsverktyg.
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 64aa010c3d840adad9e1ab6040a6d80c07cd8455
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---


# Lägg till ett SSL-certifikat {#adding-an-ssl-certificate}

Lär dig hur du lägger till ett eget SSL-certifikat med Cloud Manager självbetjäningsverktyg.

>[!TIP]
>
>Det kan ta några dagar innan ett certifikat etableras. Adobe rekommenderar därför att certifikatet tillhandahålls i god tid före en deadline eller ett öppningsdatum.

## Certifikatkrav {#certificate-requirements}

Granska **certifikatkraven** i [Introduktion till hantering av SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/introduction.md#requirements) för att se till att AEM as a Cloud Service har stöd för det certifikat som du vill lägga till.

## Lägg till ett certifikat {#adding-a-cert}

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation

1. Välj programmet på konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)**.

1. Gå till skärmen **Miljö** från sidan **Översikt**.

1. Klicka på **SSL-certifikat** under **Tjänster** på den vänstra navigeringspanelen. (Om det behövs kan du behöva klicka på hamburgikonen i det övre vänstra hörnet för att behöva navigeringspanelen. En tabell med information om eventuella befintliga SSL-certifikat visas.

   ![Lägger till ett SSL-certifikat](/help/implementing/cloud-manager/assets/ssl/ssl-cert-1.png)

1. Klicka på **Lägg till SSL-certifikat** för att öppna dialogrutan **Lägg till SSL-certifikat** .

   * Ange ett namn för ditt certifikat i **Certifikatnamn**. Det här fältet är avsett endast som information och kan vara vilket namn som helst som gör det enkelt att referera till ditt certifikat.
   * Klistra in värdena för **Certifikat**, **Privat nyckel** och **Certifikatkedja** i respektive fält. Alla tre fälten är obligatoriska.

   ![Dialogrutan Lägg till SSL-certifikat](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)

   * Alla identifierade fel i värden visas. Innan du kan spara certifikatet måste du åtgärda alla fel.
Mer information om hur du åtgärdar vanliga fel finns i [Certifikatfel](#certificate-errors).

1. Klicka på **Spara**.

![Sparat SSL-certifikat](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)Certifikatet visas nu som en ny rad i tabellen, ungefär som bilden ovan.

>[!NOTE]
>
>En användare måste vara medlem i rollen **Business Owner** eller **Deployment Manager** för att kunna installera ett SSL-certifikat i Cloud Manager.

## Certifikatfel {#certificate-errors}

Vissa fel kan uppstå om ett certifikat inte har installerats korrekt eller uppfyller kraven i Cloud Manager.

### Korrigera certifikatordning {#correct-certificate-order}

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

### Ta bort klientcertifikat {#client-certificates}

Om du får ett fel som liknar det här när du lägger till ett certifikat:

```text
The Subject of an intermediate certificate must match the issuer in the previous certificate. The SKI of an intermediate certificate must match the AKI of the previous certificate.
```

Du har antagligen inkluderat klientcertifikatet i certifikatkedjan. Kontrollera att kedjan inte innehåller klientcertifikatet och försök igen.

### Certifikatprincip {#certificate-policy}

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

### Giltighetsdatum för certifikat {#certificate-validity-dates}

Cloud Manager förväntar att SSL-certifikatet ska vara giltigt i minst 90 dagar från dagens datum. Kontrollera certifikatkedjans giltighet.

## Nästa steg {#next-steps}

Grattis! Du har nu ett fungerande SSL-certifikat för ditt projekt. Det här steget är ofta det första som ställer in ett anpassat domännamn.

* Mer information om hur du konfigurerar ett anpassat domännamn finns i [Lägg till ett anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).
* Mer information om hur du uppdaterar och hanterar dina SSL-certifikat i Cloud Manager finns i [Hantera SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md).
