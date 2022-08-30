---
title: Lägga till ett SSL-certifikat
description: Lär dig hur du lägger till ett eget SSL-certifikat med hjälp av självbetjäningsverktygen i Cloud Manager.
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
source-git-commit: 14e0255b3ce2ca44579b9fc3de6c7b7f5d8f34b6
workflow-type: tm+mt
source-wordcount: '579'
ht-degree: 0%

---

# Lägga till ett SSL-certifikat {#adding-an-ssl-certificate}

Lär dig hur du lägger till ett eget SSL-certifikat med hjälp av självbetjäningsverktygen i Cloud Manager.

>[!TIP]
>
>Det kan ta några dagar innan ett certifikat etableras. Adobe rekommenderar därför att certifikatet tillhandahålls i god tid i förväg.

## Certifikatformat {#certificate-format}

SSL-certifikatfiler måste vara i PEM-format för att kunna installeras med Cloud Manager. Vanliga filtillägg för PEM-formatet är bland annat `.pem,` .`crt`, `.cer`och `.cert`.

Följande `openssl` -kommandon kan användas för att konvertera certifikat som inte är PEM-certifikat.

* Konvertera PFX till PEM

   ```shell
   openssl pkcs12 -in certificate.pfx -out certificate.cer -nodes
   ```

* Konvertera P7B till PEM

   ```shell
   openssl pkcs7 -print_certs -in certificate.p7b -out certificate.cer
   ```

* Konvertera DER till PEM

   ```shell
   openssl x509 -inform der -in certificate.cer -out certificate.pem
   ```

## Lägga till ett certifikat {#adding-a-cert}

Följ de här stegen för att lägga till ett certifikat med hjälp av Cloud Manager.

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Navigera till **Miljö** från **Översikt** sida.

1. Klicka på **SSL-certifikat** från den vänstra navigeringspanelen. En tabell med information om eventuella befintliga SSL-certifikat visas på huvudskärmen.

   ![Lägga till ett SSL-certifikat](/help/implementing/cloud-manager/assets/ssl/ssl-cert-1.png)

1. Klicka på **Lägg till SSL-certifikat** att öppna **Lägg till SSL-certifikat** -dialogrutan.

   * Ange ett namn för ditt certifikat i **Certifikatnamn**.
      * Detta är endast avsett som information och kan vara vilket namn som helst som gör det enkelt att referera till ditt certifikat.
   * Klistra in **Certifikat**, **Privat nyckel** och **Certifikatkedja** värden i sina respektive fält. Alla tre fälten är obligatoriska.

   ![Dialogrutan Lägg till SSL-certifikat](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)

   * Alla fel som upptäcks visas.
      * Du måste åtgärda alla fel innan certifikatet kan sparas.
      * Se [Certifikatfel](#certificate-errors) om du vill veta mer om hur du åtgärdar vanliga fel.


1. Klicka **Spara** för att spara ditt certifikat.

När certifikatet har sparats visas det som en ny rad i tabellen.

![Sparat SSL-certifikat](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)

>[!NOTE]
>
>En användare måste vara medlem i **Företagsägare** eller **Distributionshanteraren** roll för att installera ett SSL-certifikat i Cloud Manager.

## Certifikatfel {#certificate-errors}

Vissa fel kan uppstå om ett certifikat inte har installerats korrekt eller uppfyller kraven för Cloud Manager.

### Certifikatprofil {#certificate-policy}

Om följande fel visas kontrollerar du certifikatets policy.

```text
Certificate policy must conform with EV or OV, and not DV policy.
```

Certifikatprofiler identifieras normalt av inbäddade OID-värden. Om du skriver ut ett certifikat till text och söker efter OID:t visas certifikatets profil.

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

Av `grep`pinga efter OID-mönstren i utdatafältstexten, du kan bekräfta din certifikatprincip.

```shell
# "EV Policy"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.1" -B5

# "OV Policy"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.2" -B5

# "DV Policy - Not Accepted"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.1" -B5
```

### Korrigera certifikatordning {#correct-certificate-order}

Den vanligaste orsaken till att en certifikatdistribution misslyckas är att de mellanliggande certifikaten eller kedjecertifikaten inte är i rätt ordning.

Mellanliggande certifikatfiler måste avslutas med rotcertifikatet eller det certifikat som ligger närmast roten. De måste vara i fallande ordning från `main/server` certifikat till roten.

Du kan ange ordningen för de mellanliggande filerna med följande kommando.

```shell
openssl crl2pkcs7 -nocrl -certfile $CERT_FILE | openssl pkcs7 -print_certs -noout
```

Du kan verifiera att den privata nyckeln och `main/server` certifikatmatchning med följande kommandon.

```shell
openssl x509 -noout -modulus -in certificate.pem | openssl md5
```

```shell
openssl rsa -noout -modulus -in ssl.key | openssl md5
```

>[!NOTE]
>
>Utdata för dessa två kommandon måste vara exakt likadana. Om du inte kan hitta någon matchande privat nyckel för `main/server` måste du ange ett nytt certifikat genom att generera ett nytt CSR och/eller begära ett uppdaterat certifikat från din SSL-leverantör.

### Giltighetsdatum för certifikat {#certificate-validity-dates}

SSL-certifikatet förväntas vara giltigt i minst 90 dagar från dagens datum. Du bör kontrollera certifikatkedjans giltighet.
