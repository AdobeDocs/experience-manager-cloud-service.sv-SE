---
title: Lägga till ett SSL-certifikat - Hantera SSL-certifikat
description: Lägga till ett SSL-certifikat - Hantera SSL-certifikat
translation-type: tm+mt
source-git-commit: 4ab944ad15390f9399138672a024aa30cf4aede8
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---


# Lägger till ett SSL-certifikat {#adding-an-ssl-certificate}

>[!NOTE]
>AEM som Cloud Service accepterar endast OV- (Organization Validation) eller EV-certifikat (Extended Validation). DV-certifikat (domänvalidering) godkänns inte.

Ett certifikat tar några dagar att etablera och vi rekommenderar att certifikatet etableras även månader i förväg. Mer information finns i [Hämta ett SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/get-ssl-certificate.md).

## Certifikatformat {#certificate-format}

SSL-filer måste vara i PEM-format för att kunna installeras i Cloud Manager. Vanliga filtillägg i PEM-format är `.pem,`.`crt`,  `.cer`och  `.cert`.

Följ stegen nedan för att konvertera SSL-filernas format till PEM:

* Konvertera PFX till PEM

   `openssl pkcs12 -in certificate.pfx -out certificate.cer -nodes`

* Konvertera P7B till PEM

   `openssl pkcs7 -print_certs -in certificate.p7b -out certificate.cer`

* Konvertera DER till PEM

   `openssl x509 -inform der -in certificate.cer -out certificate.pem`

## Viktiga överväganden {#important-considerations}

* En användare måste ha rollen Business Owner eller Deployment Manager för att kunna installera ett SSL-certifikat i Cloud Manager.

* Molnhanteraren tillåter vid en given tidpunkt högst 10 SSL-certifikat som kan kopplas till en eller flera miljöer i ditt program, även om ett certifikat har gått ut. Molnhanterarens användargränssnitt tillåter dock att upp till 50 SSL-certifikat installeras i programmet med den här begränsningen.

## Lägger till ett certifikat {#adding-a-cert}

Följ stegen nedan för att lägga till ett certifikat:

1. Logga in på Cloud Manager.
1. Navigera till **Miljöer** från sidan **Översikt**.
1. Klicka på **SSL-certifikat** i den vänstra navigeringsmenyn. En tabell med information om eventuella befintliga SSL-certifikat visas på den här skärmen.

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-1.png)

1. Klicka på **Lägg till SSL-certifikat** för att öppna dialogrutan **Lägg till SSL-certifikat**.

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-02.png)

   1. Ange ett namn för ditt certifikat i **Certifikatnamn**. Det kan vara vilket namn som helst som gör det enkelt att referera till ditt certifikat.
   1. Klistra in **certifikatet**, **den privata nyckeln** och **certifikatkedjan** i respektive fält. Använd ikonen Klistra in till höger om inmatningsrutan.
Alla tre fälten är inte valfria och måste inkluderas.

1. Klicka på **Spara** för att skicka certifikatet. Den visas som en ny rad i tabellen.

   ![](/help/implementing/cloud-manager/assets/ssl/ssl-cert-3.png)
   >[!NOTE]
   >Alla fel som upptäcks visas. Du måste åtgärda alla fel innan certifikatet kan sparas. Mer information om hur du åtgärdar vanliga fel finns i [certifikatfel](#certificate-errors).

## Certifikatfel {#certificate-errors}

### Korrigera certifikatordning {#correct-certificate-order}

Den vanligaste orsaken till att en certifikatdistribution misslyckas är att de mellanliggande certifikaten eller kedjecertifikaten inte är i rätt ordning. De mellanliggande certifikatfilerna måste avslutas med det rotcertifikat eller certifikat som ligger närmast roten och vara i fallande ordning från `main/server`-certifikatet till roten.

Du kan bestämma ordningen för de mellanliggande filerna med följande kommando:

`openssl crl2pkcs7 -nocrl -certfile $CERT_FILE | openssl pkcs7 -print_certs -noout`

Du kan verifiera att den privata nyckeln och `main/server`-certifikatet matchar med följande kommandon:

`openssl x509 -noout -modulus -in certificate.pem | openssl md5`

`openssl rsa -noout -modulus -in ssl.key | openssl md5`

>[!NOTE]
>Utdata för dessa två kommandon måste vara exakt likadana. Om du inte kan hitta en matchande privat nyckel till ditt `main/server`-certifikat måste du ange en ny nyckel för certifikatet genom att generera en ny CSR och/eller begära ett uppdaterat certifikat från din SSL-leverantör.

### Certifikatets giltighetsdatum {#certificate-validity-dates}

SSL-certifikatet förväntas vara giltigt i minst 90 dagar framöver. Du bör kontrollera certifikatkedjans giltighet.
