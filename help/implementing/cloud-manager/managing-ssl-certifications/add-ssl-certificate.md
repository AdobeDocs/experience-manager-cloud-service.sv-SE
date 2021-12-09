---
title: Lägga till ett SSL-certifikat - Hantera SSL-certifikat
description: Lägga till ett SSL-certifikat - Hantera SSL-certifikat
exl-id: 104b5119-4a8b-4c13-99c6-f866b3c173b2
source-git-commit: 828490e12d99bc8f4aefa0b41a886f86fee920b4
workflow-type: tm+mt
source-wordcount: '686'
ht-degree: 0%

---

# Lägga till ett SSL-certifikat {#adding-an-ssl-certificate}

>[!NOTE]
>AEM as a Cloud Service godkänner endast certifikat som överensstämmer med OV- (Organization Validation) eller EV-principen (Extended Validation). DV-principen (Domain Validation) accepteras inte. Dessutom måste alla certifikat vara ett X.509 TLS-certifikat från en betrodd certifikatutfärdare (CA) med en matchande 2 048-bitars RSA privat nyckel. AEM as a Cloud Service godkänner SSL-jokertecken för en domän.

Ett certifikat tar några dagar att etablera och vi rekommenderar att certifikatet etableras även månader i förväg. Se [Hämta ett SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/get-ssl-certificate.md) för mer information.

## Certifikatformat {#certificate-format}

SSL-filer måste vara i PEM-format för att kunna installeras i Cloud Manager. Vanliga filtillägg i PEM-format är bland annat `.pem,` .`crt`, `.cer`och `.cert`.

Följ stegen nedan för att konvertera SSL-filernas format till PEM:

* Konvertera PFX till PEM

   `openssl pkcs12 -in certificate.pfx -out certificate.cer -nodes`

* Konvertera P7B till PEM

   `openssl pkcs7 -print_certs -in certificate.p7b -out certificate.cer`

* Konvertera DER till PEM

   `openssl x509 -inform der -in certificate.cer -out certificate.pem`

## Viktiga överväganden {#important-considerations}

* En användare måste ha rollen Business Owner eller Deployment Manager för att kunna installera ett SSL-certifikat i Cloud Manager.

* Molnhanteraren tillåter vid en given tidpunkt högst 10 SSL-certifikat som kan kopplas till en eller flera miljöer i ditt program, även om ett certifikat har gått ut. Molnhanterarens användargränssnitt tillåter dock att upp till 50 SSL-certifikat installeras i programmet med den här begränsningen. Ett certifikat kan vanligtvis omfatta flera domäner (upp till 100 SAN-nätverk). Överväg därför att gruppera flera domäner i samma certifikat för att hålla sig inom denna gräns.


## Lägga till ett certifikat {#adding-a-cert}

Följ stegen nedan för att lägga till ett certifikat:

1. Logga in på Cloud Manager.
1. Navigera till **Miljö** skärmbild från **Översikt** sida.
1. Klicka på **SSL-certifikat** från den vänstra navigeringsmenyn. En tabell med information om eventuella befintliga SSL-certifikat visas på den här skärmen.

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-1.png)

1. Klicka på **Lägg till SSL-certifikat** att öppna **Lägg till SSL-certifikat** -dialogrutan.

   * Ange ett namn för ditt certifikat i **Certifikatnamn**. Det kan vara vilket namn som helst som gör det enkelt att referera till ditt certifikat.
   * Klistra in **Certifikat**, **Privat nyckel** och **Certifikatkedja** till sina respektive fält. Använd ikonen Klistra in till höger om inmatningsrutan.
Alla tre fälten är inte valfria och måste inkluderas.

      ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)


      >[!NOTE]
      >Alla fel som upptäcks visas. Du måste åtgärda alla fel innan certifikatet kan sparas. Se [Certifikatfel](#certificate-errors) om du vill veta mer om hur du åtgärdar vanliga fel.

1. Klicka **Spara** för att skicka in ditt certifikat. Den visas som en ny rad i tabellen.

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)

## Certifikatfel {#certificate-errors}

### Certifikatprofil {#certificate-policy}

Om du ser felet &quot;Certifikatprincipen måste överensstämma med EV- eller OV-principen, och inte DV-principen&quot;, kontrollerar du certifikatets profil.

Vanligtvis identifieras certifikattyper av de OID-värden som är inbäddade i profiler. Dessa OID:n är unika och konverterar därför ett certifikat till ett textformulär. Om du söker efter OID:t bekräftas att certifikatet har en matchning.

Du kan visa din certifikatinformation på följande sätt.

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

Tabellen innehåller identifieringsmönster.

| Mönster | Certifikattyp | Godtagbart |
|---|---|---|
| `2.23.140.1.2.1` | DV | Nej |
| `2.23.140.1.2.2` | OV | Ja |
| `2.23.140.1.2.3` and `TLS Web Server Authentication` | IV-certifikat med behörighet att använda för https | Ja |

`grep`pinga efter mönstren, du kan bekräfta din certifikattyp.

```shell
# "EV Policy"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.1" -B5

# "OV Policy"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.2" -B5

# "DV Policy - Not Accepted"
openssl x509 -in certificate.pem -text grep "Policy: 2.23.140.1.2.1" -B5
```

### Korrigera certifikatordning {#correct-certificate-order}

Den vanligaste orsaken till att en certifikatdistribution misslyckas är att de mellanliggande certifikaten eller kedjecertifikaten inte är i rätt ordning. De mellanliggande certifikatfilerna måste avslutas med det rotcertifikat eller certifikat som ligger närmast roten och vara i fallande ordning från `main/server` certifikat till roten.

Du kan bestämma ordningen för de mellanliggande filerna med följande kommando:

`openssl crl2pkcs7 -nocrl -certfile $CERT_FILE | openssl pkcs7 -print_certs -noout`

Du kan verifiera att den privata nyckeln och `main/server` certifikatmatchning med följande kommandon:

`openssl x509 -noout -modulus -in certificate.pem | openssl md5`

`openssl rsa -noout -modulus -in ssl.key | openssl md5`

>[!NOTE]
>Utdata för dessa två kommandon måste vara exakt likadana. Om du inte kan hitta en matchande privat nyckel till `main/server` måste du ange ett nytt certifikat genom att generera ett nytt CSR och/eller begära ett uppdaterat certifikat från din SSL-leverantör.

### Giltighetsdatum för certifikat {#certificate-validity-dates}

SSL-certifikatet förväntas vara giltigt i minst 90 dagar framöver. Du bör kontrollera certifikatkedjans giltighet.
