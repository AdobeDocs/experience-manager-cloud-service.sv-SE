---
title: Introduktion till hantering av SSL-certifikat
description: Lär dig hur Cloud Manager förser dig med självbetjäningsverktyg för att installera SSL-certifikat.
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: fcde1f323392362d826f9b4a775e468de9550716
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 0%

---


# Introduktion till hantering av SSL-certifikat{#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_sslcert"
>title="Hantera SSL-certifikat"
>abstract="Läs om hur Cloud Manager förser dig med självbetjäningsverktyg för att installera och hantera SSL-certifikat för att skydda webbplatsen för dina användare. Cloud Manager använder en TLS-plattformstjänst för att hantera SSL-certifikat och privata nycklar som ägs av kunder och som erhållits från tredjepartscertifikatutfärdare."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates" text="Visa, uppdatera och ersätta ett SSL-certifikat"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates" text="Kontrollera status för ett SSL-certifikat"


Cloud Manager erbjuder självbetjäningsverktyg för att installera och hantera SSL-certifikat (Secure Socket Layer), vilket garanterar webbplatssäkerheten för dina användare. Följande två användningsområden stöds:

<!-- CQDOC-21758, #1 -->

* **Använd fall 1:** Cloud Manager använder en TLS-tjänst (Transport Layer Security) för att hantera kundägda SSL-certifikat och privata nycklar från tredjepartscertifikatutfärdare, som *Låt oss kryptera*.
* **Använd fall 2:** Med Cloud Manager kan användare konfigurera ett DV-certifikat (Domain Validation) som kommer från Adobe för snabb domänkonfiguration. DV-certifikat är den mest grundläggande nivån för SSL-certifiering och används ofta för testning eller för att skydda webbplatser med grundläggande kryptering. DV-certifikat är tillgängliga i både [produktion och sandlådeprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md).

  >
  >
  >Kunder får inte överföra DV-certifikat (Domain Validation).


## Introduktion till certifikat {#certificates}

Företag och organisationer använder SSL-certifikat för att skydda sina webbplatser och låta sina kunder lita på dem. Om du vill använda SSL-protokollet måste ett SSL-certifikat användas på en webbserver.

När en enhet, till exempel en organisation eller ett företag, begär ett certifikat från en certifikatutfärdare (certifikatutfärdare), slutför certifikatutfärdaren en verifieringsprocess. Den här processen kan omfatta allt från verifiering av domännamnskontroll till insamling av registreringsdokument och prenumerationsavtal. När informationen för en entitet har verifierats signerar certifikatutfärdaren sin offentliga nyckel med hjälp av certifikatutfärdarens privata nyckel. Eftersom alla viktiga certifikatutfärdare har rotcertifikat i webbläsare länkas entitetens certifikat via en *förtroendekedja* och webbläsaren tolkar det som ett pålitligt certifikat.

>[!IMPORTANT]
>
>Cloud Manager tillhandahåller inte SSL-certifikat eller privata nycklar. Dessa saker måste hämtas från en certifikatutfärdare, en betrodd tredjepartsorganisation. Vissa välkända certifikatutfärdare inkluderar *DigiCert*, *Låt oss kryptera*, *GlobalSign*, *Entrust* och *Verisign*.

## Cloud Manager SSL-hanteringsfunktioner {#features}

Cloud Manager stöder följande alternativ för användning av SSL-certifikat.

* Flera miljöer kan använda ett SSL-certifikat. Det innebär att den kan läggas till en gång, men användas flera gånger.
* Varje Cloud Manager-miljö kan använda flera certifikat.
* En privat nyckel kan utfärda flera SSL-certifikat.
* Varje certifikat innehåller vanligtvis flera domäner.
* Plattformens TLS-tjänst skickar förfrågningar till kundens CDN-tjänst baserat på det SSL-certifikat som används för att avsluta och den CDN-tjänst som är värd för den domänen.
* AEM as a Cloud Service godkänner SSL-jokertecken för en domän.

## Recommendations {#recommendations}

AEM as a Cloud Service stöder bara säkra `https`-platser.

* Kunder med flera anpassade domäner vill inte överföra ett certifikat varje gång de lägger till en domän.
* Sådana kunder tjänar på att skaffa ett certifikat med flera domäner.

## Certifikatkrav {#requirements}

* AEM as a Cloud Service godkänner certifikat som överensstämmer med OV- (Organization Validation), EV- (Extended Validation) eller DV-principen (Domain Validation). <!-- CQDOC-21758, #2 -->
* Alla certifikat måste vara ett X.509 TLS-certifikat från en betrodd certifikatutfärdare med en matchande 2 048-bitars RSA privat nyckel.
* Självsignerade certifikat accepteras inte.

OV- och EV-certifikat innehåller CA-validerad information. Sådan information hjälper användarna att bedöma om webbplatsägaren, e-postavsändaren eller den digitala signeraren av kod eller PDF kan betraktas som tillförlitliga. DV-certifikat tillåter inte sådan ägarskapsverifiering.

### Certifikatformat som hanteras av kund {#certificate-format}

<!-- CQDOC-21758, #3 -->

SSL-certifikatfiler måste vara i PEM-format för att kunna installeras med Cloud Manager. Vanliga filtillägg för PEM-formatet är `.pem,`. `crt`, `.cer` och `.cert`.

Följande `openssl`-kommandon kan användas för att konvertera certifikat som inte är PEM-certifikat.

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

## Begränsningar {#limitations}

Vid en given tidpunkt tillåter Cloud Manager högst 50 installerade SSL-certifikat. Dessa certifikat kan kopplas till en eller flera miljöer i hela programmet och kan även innehålla certifikat som gått ut.

Om du har nått gränsen kan du granska dina certifikat och överväga:

* Tar bort certifikat som gått ut.
* Gruppera flera domäner i samma certifikat eftersom ett certifikat kan omfatta flera domäner (upp till 100 SAN).

## Läs mer {#learn-more}

En användare med nödvändig behörighet kan använda Cloud Manager för att hantera SSL-certifikat för ett program. Mer information om hur du använder dessa funktioner finns i följande dokument.

* [Lägg till ett SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) <!--CQDOC-21758, #4 -->
* [Hantera SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md) <!--CQDOC-21758, #4 -->

