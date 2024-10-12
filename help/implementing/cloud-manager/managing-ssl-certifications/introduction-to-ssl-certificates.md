---
title: Introduktion till SSL-certifikat
description: Läs mer om de självbetjäningsverktyg som Cloud Manager tillhandahåller för att installera och hantera SSL-certifikat.
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
source-git-commit: fa99656e0dd02bb97965e8629d5fa657fbae9424
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 0%

---


# Introduktion till SSL-certifikat{#introduction}

Lär dig mer om de självbetjäningsverktyg som Cloud Manager tillhandahåller för att installera och hantera SSL-certifikat (Secure Socket Layer).

>[!CONTEXTUALHELP]
>id="aemcloud_golive_sslcert"
>title="Hantera SSL-certifikat"
>abstract="Läs om hur Cloud Manager förser dig med självbetjäningsverktyg för att installera och hantera SSL-certifikat för att skydda webbplatsen för dina användare. Cloud Manager använder en TLS-plattformstjänst för att hantera SSL-certifikat och privata nycklar som ägs av kunder och som erhållits från tredjepartscertifikatutfärdare."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates" text="Visa, uppdatera och ersätta ett SSL-certifikat"
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates" text="Kontrollera status för ett SSL-certifikat"

## Vad är SSL-certifikat? {#overview}

Företag och organisationer använder SSL-certifikat (Secure Socket Layer) för att skydda sina webbplatser och göra det möjligt för sina kunder att lita på dem. Om du vill använda SSL-protokollet måste en webbserver ha ett SSL-certifikat.

När en entitet, till exempel en organisation eller ett företag, begär ett certifikat från en certifikatutfärdare (CA) slutför certifikatutfärdaren en verifieringsprocess. Den här processen kan omfatta allt från verifiering av domännamnskontroll till insamling av registreringsdokument och prenumerationsavtal. När informationen för en entitet har verifierats signerar certifikatutfärdaren sin offentliga nyckel med hjälp av certifikatutfärdarens privata nyckel. Eftersom alla viktiga certifikatutfärdare har rotcertifikat i webbläsare länkas entitetens certifikat via en *förtroendekedja* och webbläsaren tolkar det som ett pålitligt certifikat.

>[!IMPORTANT]
>
>Cloud Manager tillhandahåller inte SSL-certifikat eller privata nycklar. Dessa delar måste hämtas från en certifikatutfärdare, en betrodd tredjepartsorganisation. Vissa välkända certifikatutfärdare inkluderar *DigiCert*, *Låt oss kryptera*, *GlobalSign*, *Entrust* och *Verisign*.

## Hantera certifikat med Cloud Manager {#cloud-manager}

Cloud Manager erbjuder självbetjäningsverktyg för att installera och hantera SSL-certifikat och säkerställa webbplatssäkerheten för dina användare. Cloud Manager stöder två modeller för hantering av dina certifikat.

| | Modell | Beskrivning |
| --- | --- | --- |
| A | **[SSL-certifikat som hanteras av Adobe (DV)](#adobe-managed)** | Med Cloud Manager kan användare konfigurera DV-certifikat (Domain Validation) som tillhandahålls av Adobe för snabb domänkonfiguration. |
| B | **[Kundhanterat SSL-certifikat (OV/EV)](#customer-managed)** | Cloud Manager erbjuder en TLS-tjänst (Transport Layer Security) för att du ska kunna hantera OV- och EV SSL-certifikat som du äger och privata nycklar från tredjepartscertifikatutfärdare, som *Låt oss kryptera*. |

Båda modellerna har följande allmänna funktioner för att hantera dina certifikat:

* Varje Cloud Manager-miljö kan använda flera certifikat.
* En privat nyckel kan utfärda flera SSL-certifikat.
* Plattformens TLS-tjänst skickar förfrågningar till kundens CDN-tjänst baserat på det SSL-certifikat som används för att avsluta och den CDN-tjänst som är värd för den domänen.

>[!IMPORTANT]
>
>[Om du vill lägga till och associera en anpassad domän med miljön ](/help/implementing/cloud-manager/custom-domain-names/introduction.md) måste du ha ett giltigt SSL-certifikat som omfattar domänen.

### SSL-certifikat som hanteras av Adobe (DV) {#adobe-managed}

DV-certifikat är den mest grundläggande nivån för SSL-certifiering och används ofta för testning eller för att skydda webbplatser med grundläggande kryptering. DV-certifikat är tillgängliga i både [produktionsprogram och sandlådeprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md).

När DV-certifikatet har skapats förnyas det automatiskt i Adobe var tredje månad, såvida det inte tas bort.

### Kundhanterade OV/EV SSL-certifikat {#customer-managed}

OV- och EV-certifikat innehåller CA-validerad information. Sådan information hjälper användarna att bedöma om webbplatsägaren, e-postavsändaren eller den digitala signeraren av kod eller PDF kan betraktas som tillförlitliga. DV-certifikat tillåter inte sådan ägarskapsverifiering.

OV och EV erbjuder dessutom dessa funktioner jämfört med DV-certifikat i Cloud Manager.

* Flera miljöer kan använda ett OV/EV-certifikat. Det innebär att den kan läggas till en gång, men användas flera gånger.
* Varje OV/EV-certifikat innehåller vanligtvis flera domäner.
* Cloud Manager godkänner OV-/EV-certifikat med jokertecken för en domän.

>[!TIP]
>
>Om du har flera anpassade domäner kanske du inte vill överföra ett certifikat varje gång du lägger till en ny domän. I så fall kan du ha nytta av att skaffa ett enda certifikat som omfattar flera domäner.

>[!NOTE]
>
>Om två certifikat omfattar samma domän installeras, tillämpas det mer exakta certifikatet.
>
>Om din domän till exempel är `dev.adobe.com` och du har ett certifikat för `*.adobe.com` och ett annat för `dev.adobe.com`, används det mer specifika (`dev.adobe.com`).

#### Krav för kundhanterade OV/EV SSL-certifikat {#requirements}

Om du väljer att lägga till ett eget OV/EV SSL-certifikat som hanteras av kunden måste det uppfylla följande krav:

* AEM as a Cloud Service godkänner certifikat som överensstämmer med OV- (Organization Validation) eller EV-principen (Extended Validation).
   * Cloud Manager stöder inte tillägg av egna DV-certifikat (domänvalidering).
* Alla certifikat måste vara ett X.509 TLS-certifikat från en betrodd certifikatutfärdare med en matchande 2 048-bitars RSA privat nyckel.
* Självsignerade certifikat accepteras inte.

#### Format för kundhanterade certifikat {#certificate-format}

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

>[!TIP]
>
>Adobe rekommenderar att du validerar integriteten för ditt certifikat lokalt med ett verktyg som `openssl verify -untrusted intermediate.pem certificate.pem` innan du försöker installera det med Cloud Manager.

## Begränsning av antalet installerade SSL-certifikat {#limitations}

Vid en given tidpunkt tillåter Cloud Manager högst 50 installerade SSL-certifikat. Dessa certifikat kan kopplas till en eller flera miljöer i hela programmet och kan även innehålla certifikat som gått ut.

Om du har nått gränsen kan du granska dina certifikat och ta bort certifikat som har gått ut. Eller gruppera flera domäner i samma certifikat eftersom ett certifikat kan omfatta flera domäner (upp till 100 SAN-nätverk).

## Läs mer {#learn-more}

En användare med nödvändig behörighet kan använda Cloud Manager för att hantera SSL-certifikat för ett program. Mer information om hur du använder dessa funktioner finns i följande dokument.

* [Lägg till ett SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) <!--CQDOC-21758, #4 -->
* [Hantera SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md) <!--CQDOC-21758, #4 -->

