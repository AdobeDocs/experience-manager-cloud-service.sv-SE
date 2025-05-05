---
title: Felsöka SSL-certifikatproblem
description: Lär dig hur du felsöker SSL-certifikatproblem genom att identifiera vanliga orsaker så att du kan upprätthålla säkra anslutningar.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: 1017f84564cedcef502b017915d370119cd5a241
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 0%

---


# Felsöka SSL-certifikatproblem {#certificate-problems}

Lär dig hur du felsöker SSL-certifikatproblem genom att identifiera vanliga orsaker så att du kan upprätthålla säkra anslutningar.

+++**Ogiltigt certifikat**

## Ogiltigt certifikat {#invalid-certificate}

Det här felet inträffar eftersom kunden använde en krypterad privat nyckel och angav nyckeln i DER-format.

+++

+++**Den privata nyckeln måste vara PKCS 8-format**

## Den privata nyckeln måste vara PKCS 8-format {#pkcs-8}

Det här felet inträffar eftersom kunden använde en krypterad privat nyckel och angav nyckeln i DER-format.

+++

+++**Korrigera certifikatordning**

## Korrigera certifikatordning {#certificate-order}

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

+++**Ta bort klientcertifikat**

## Ta bort klientcertifikat {#client-certificates}

Om du får ett fel som liknar det här när du lägger till ett certifikat:

```text
The Subject of an intermediate certificate must match the issuer in the previous certificate. The SKI of an intermediate certificate must match the AKI of the previous certificate.
```

Du har antagligen inkluderat klientcertifikatet i certifikatkedjan. Kontrollera att kedjan inte innehåller klientcertifikatet och försök igen.

+++

+++**Certifikatprincip**

## Certifikatprincip {#policy}

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

++**Certifikatets giltighet

## Certifikatets giltighet {#validity}

Cloud Manager förväntar att SSL-certifikatet ska vara giltigt i minst 90 dagar från dagens datum. Kontrollera certifikatkedjans giltighet.

+++

++**Fel SAN-certifikat används på min domän

## Fel SAN-certifikat används på min domän {#wrong-san-cert}

Säg att du vill länka `dev.yoursite.com` och `stage.yoursite.com` till din icke-produktionsmiljö och `prod.yoursite.com` till din produktionsmiljö.

Om du vill konfigurera CDN för dessa domäner måste du ha ett certifikat installerat för varje, så du måste installera ett certifikat som omfattar `*.yoursite.com` för dina icke-produktionsdomäner och ett annat som även omfattar `*.yoursite.com` för dina produktionsdomäner.

Den här konfigurationen är giltig. När du uppdaterar ett av certifikaten, eftersom båda certifikaten omfattar samma SAN-post, kommer CDN att installera det senaste certifikatet på alla tillämpliga domäner, vilket kan verka oväntat.

Även om detta kan vara oväntat är detta inte ett fel och är standardbeteendet för det underliggande CDN. Om du har två eller flera SAN-certifikat som täcker samma SAN-domänpost, och om den domänen täcks av ett certifikat och det andra uppdateras, kommer den senare nu att installeras för domänen.

+++
