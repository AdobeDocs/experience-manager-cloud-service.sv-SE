---
title: Lägga till ett SSL-certifikat - Hantera SSL-certifikat
description: Lägga till ett SSL-certifikat - Hantera SSL-certifikat
translation-type: tm+mt
source-git-commit: 9026befea071777dd2b97c16cdc5c623c86c1c8d
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---


# Lägga till ett SSL-certifikat {#adding-an-ssl-certificate}

>[!NOTE]
>Ett certifikat tar några dagar att etablera och vi rekommenderar att certifikatet etableras även månader i förväg. Gå till Så här hämtar du ett SSL-certifikat om du vill veta mer.INSERT LINK

## Certifikatformat {#certificate-format}

SSL-filer måste vara i PEM-format för att kunna installeras i Cloud Manager. Vanliga filtillägg i PEM-format är .pem, .crt, .cer och .cert.

Följ stegen nedan för att konvertera SSL-filernas format till PEM:

1. Konvertera PFX till PEM

`openssl pkcs12 -in certificate.pfx -out certificate.cer -nodes`

1. Konvertera P7B till PEM

`openssl pkcs7 -print_certs -in certificate.p7b -out certificate.cer`

1. Konvertera DER till PEM

`openssl x509 -inform der -in certificate.cer -out certificate.pem`

## Lägga till ditt certifikat {#adding-certificate}

>[!NOTE]
>* En användare måste ha rollen Business Owner eller Deployment Manager för att kunna installera ett SSL-certifikat i Cloud Manager.
>* Molnhanteraren tillåter vid en given tidpunkt maximalt 5 SSL-certifikat som kan kopplas till en eller flera miljöer i ditt program, även om ett certifikat har gått ut. Molnhanterarens användargränssnitt tillåter dock att upp till 50 SSL-certifikat installeras i programmet med den här begränsningen.


1. Logga in på Cloud Manager.
1. Navigera till miljöskärmen från sidan Översikt.
1. Navigera till SSL-certifikatskärmen på den vänstra navigeringsmenyn. En tabell med information om eventuella befintliga SSL-certifikat visas på den här skärmen.INSERT IMAGE
1. Välj knappen **Lägg till certifikat** när du vill starta en guide.
1. Ange ett namn för certifikatet. Det kan vara vilket namn som helst som gör det enkelt att referera till ditt certifikat.
1. Klistra in innehållet i Certifikat, Privat nyckel och Kedja i sina respektive fält. Använd ikonen Klistra in till höger om inmatningsrutan.
1. Välj **Spara**.

   >[!NOTE]
   >Alla fel som upptäcks visas. Du måste åtgärda alla fel innan certifikatet kan sparas. Mer information om hur du åtgärdar vanliga fel finns i INSERT LINK-fel för certifikat.

   När du har skickat certifikatet visas det som en ny rad i tabellen.

## Certifikatfel {#certificate-errors}

### Korrigera certifikatordning {#correct-certificate-order}

Den vanligaste orsaken till att en certifikatdistribution misslyckas är att de mellanliggande certifikaten eller kedjecertifikaten inte är i rätt ordning. De mellanliggande certifikatfilerna måste avslutas med det rotcertifikat eller certifikat som ligger närmast roten och vara i fallande ordning från certifikatet till roten `main/server` .

Du kan bestämma ordningen för de mellanliggande filerna med följande kommando:

`openssl crl2pkcs7 -nocrl -certfile $CERT_FILE | openssl pkcs7 -print_certs -noout`

Du kan kontrollera att den privata nyckeln och certifikatet matchar med `main/server` följande kommandon:

`openssl x509 -noout -modulus -in certificate.pem | openssl md5`

`openssl rsa -noout -modulus -in ssl.key | openssl md5`

>[!NOTE]
>Utdata för dessa två kommandon måste vara exakt likadana. Om du inte hittar någon matchande privat nyckel till ditt `main/server` certifikat måste du ange en ny nyckel för certifikatet genom att generera en ny CSR och/eller begära ett uppdaterat certifikat från din SSL-leverantör.

### Giltighetsdatum för certifikat {#certificate-validity-dates}

SSL-certifikatet förväntas vara giltigt i minst 90 dagar i framtiden

Kontrollera certifikatkedjans giltighet.
