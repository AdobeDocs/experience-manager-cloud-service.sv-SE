---
title: Introduktion till SSL-certifikat
description: Läs mer om de självbetjäningsverktyg som Cloud Manager tillhandahåller för att installera och hantera SSL-certifikat.
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
source-git-commit: b94debebf36f379fc2cb2f193a244fe154c77537
workflow-type: tm+mt
source-wordcount: '1260'
ht-degree: 0%

---


# Introduktion till SSL-certifikat{#introduction}

Lär dig mer om de självbetjäningsverktyg som Cloud Manager tillhandahåller för att installera och hantera SSL-certifikat (Secure Socket Layer).

>[!CONTEXTUALHELP]
>id="aemcloud_golive_sslcert"
>title="Hantera SSL-certifikat"
>abstract="Läs om hur Cloud Manager har självbetjäningsverktyg för att installera och hantera SSL-certifikat för att skydda din webbplats för dina användare. Cloud Manager använder en TLS-plattformstjänst för att hantera SSL-certifikat och privata nycklar som ägs av kunder och som erhållits från tredjepartscertifikatutfärdare."
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
| A | **[Adobe-hanterat SSL-certifikat (DV)](#adobe-managed)** | Med Cloud Manager kan användare konfigurera DV-certifikat (Domain Validation) som tillhandahålls av Adobe för snabb domänkonfiguration. |
| B | **[Kundhanterat SSL-certifikat (OV/EV)](#customer-managed)** | Cloud Manager erbjuder en TLS-tjänst (Transport Layer Security) för att du ska kunna hantera OV- och EV SSL-certifikat som du äger och privata nycklar från tredjepartscertifikatutfärdare, som *Låt oss kryptera*. |

Båda modellerna har följande allmänna funktioner för att hantera dina certifikat:

* Varje Cloud Manager-miljö kan använda flera certifikat.
* En privat nyckel kan utfärda flera SSL-certifikat.
* Plattformens TLS-tjänst skickar förfrågningar till kundens CDN-tjänst baserat på det SSL-certifikat som används för att avsluta och den CDN-tjänst som är värd för den domänen.

>[!IMPORTANT]
>
>[Om du vill lägga till och associera en anpassad domän med miljön &#x200B;](/help/implementing/cloud-manager/custom-domain-names/introduction.md) måste du ha ett giltigt SSL-certifikat som omfattar domänen.

### Adobe-hanterade (DV) SSL-certifikat {#adobe-managed}

DV-certifikat är den mest grundläggande nivån för SSL-certifiering och används ofta för testning eller för att skydda webbplatser med grundläggande kryptering. DV-certifikat är tillgängliga i både [produktionsprogram och sandlådeprogram](/help/implementing/cloud-manager/getting-access-to-aem-in-cloud/program-types.md).

När DV-certifikatet har skapats förnyas det automatiskt var tredje månad, såvida det inte tas bort.

>[!IMPORTANT]
>
>Om din miljö använder (DV) SSL-certifikat med en CNAME-baserad validering, ska du tänka på att om du tar bort CNAME-posten innan den automatiska certifikatförnyelsen sker kan förnyelsen misslyckas. Borttagningen kan leda till att certifikatet upphör att gälla och att tjänsten avbryts. För att undvika detta bör du kontrollera att CNAME-posten finns kvar under hela förnyelseprocessen. Förnyelseprocessen beror på att CNAME-posten finns tillgänglig för validering av domänägarskap.

### SSL-certifikat som hanteras av kund (OV/EV) {#customer-managed}

OV- och EV-certifikat innehåller CA-validerad information. Sådan information hjälper användarna att bedöma om webbplatsägaren, e-postavsändaren eller den digitala signeraren av kod eller PDF-dokument kan betraktas som tillförlitliga. DV-certifikat tillåter inte sådan ägarskapsverifiering.

OV och EV erbjuder dessutom dessa funktioner jämfört med DV-certifikat i Cloud Manager.

* Flera miljöer kan använda ett OV/EV-certifikat. Det innebär att den kan läggas till en gång, men användas flera gånger.
* Varje OV/EV-certifikat innehåller vanligtvis flera domäner.
* Cloud Manager godkänner OV-/EV-certifikat med jokertecken för en domän.

>[!TIP]
>
>Om du har flera anpassade domäner kanske du inte vill överföra ett certifikat varje gång du lägger till en ny domän. I så fall kan du ha nytta av att skaffa ett enda certifikat som omfattar flera domäner.

#### Krav för kundhanterade OV/EV SSL-certifikat {#requirements}

Om du väljer att lägga till ett eget kundhanterat SSL-certifikat måste det uppfylla följande uppdaterade krav:

* DV-certifikat (Domain Validation) och självsignerade certifikat stöds inte.
* Certifikatet måste följa OV-profiler (Organization Validation) eller EV-profiler (Extended Validation).
* Certifikatet måste vara ett X.509 TLS-certifikat utfärdat av en betrodd certifikatutfärdare (CA).
* Följande kryptografiska nyckeltyper stöds:

   * 2048-bitars RSA, standardstöd.
RSA-nycklar som är större än 2048 bitar (till exempel 3072-bitars eller 4096-bitars RSA-nycklar) stöds inte för närvarande.
   * Elliptiska kurvnycklar (EC) `prime256v1` (`secp256r1`) och `secp384r1`
   * ECDSA-certifikat (Elliptic Curve Digital Signature Algorithm). Sådana certifikat rekommenderas av Adobe framför RSA för bättre prestanda, säkerhet och effektivitet.

* Certifikat måste vara korrekt formaterade för att validering ska kunna utföras. Privata nycklar måste ha formatet `PKCS#8`.

>[!NOTE]
>Om din organisation kräver efterlevnad med 3072-bitars RSA-nycklar rekommenderar Adobe att du använder ECDSA-certifikat (`secp256r1` eller `secp384r1`).


#### Bästa tillvägagångssätt för certifikatshantering

* **Undvik överlappande certifikat:**

   * Undvik att distribuera överlappande certifikat som matchar samma domän för att få en smidig certifikatshantering. Om du till exempel har ett jokertecken (*.example.com) bredvid ett visst certifikat (dev.example.com) kan det leda till förvirring.
   * TLS-lagret prioriterar det mest specifika och nyligen distribuerade certifikatet.

  Exempelscenarier:

   * &quot;Dev Certificate&quot; omfattar `dev.example.com` och distribueras som en domänmappning för `dev.example.com`.
   * &quot;Stage Certificate&quot; omfattar `stage.example.com` och distribueras som en domänmappning för `stage.example.com`.
   * Om &quot;Stage Certificate&quot; distribueras/uppdateras *efter* &quot;Dev Certificate&quot; används även begäranden för `dev.example.com`.

     För att undvika sådana konflikter måste du se till att certifikaten noggrant omfattar de domäner de är avsedda för.

* **Jokertecken:**

  Jokertecken (till exempel `*.example.com`) stöds, men de bör bara användas när det behövs. Vid överlappning har det mer specifika certifikatet företräde. Det specifika certifikatet visar till exempel `dev.example.com` i stället för jokertecknet (`*.example.com`).

* **Validering och felsökning:**
Innan du försöker installera ett certifikat med Cloud Manager rekommenderar Adobe att du validerar certifikatets integritet lokalt med verktyg som `openssl` . Exempel:

  `openssl verify -untrusted intermediate.pem certificate.pem`


<!--
>[!NOTE]
>
>If two certificates cover the same domain are installed, the one that is more exact is applied.
>
>For example, if your domain is `dev.adobe.com` and you have one certificate for `*.adobe.com` and another for `dev.adobe.com`, the more specific one (`dev.adobe.com`) is used.
-->

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

## Begränsningar {#limitations}

### Antal installerade SSL-certifikat {#number-installed-ssl-certs}

Cloud Manager har stöd för upp till 70 installerade certifikat vid en given tidpunkt. Dessa certifikat kan kopplas till en eller flera miljöer i hela programmet och kan även innehålla certifikat som gått ut.

Om du har nått gränsen kan du granska dina certifikat och ta bort certifikat som har gått ut. Eller gruppera flera domäner i samma certifikat eftersom ett certifikat kan omfatta flera domäner (upp till 100 SAN-nätverk).

### Låt oss kryptera hastighetsbegränsningar för Adobe-hanterade DV-certifikat

Adobe-hanterade DV-certifikat förlitar sig på Låt oss kryptera. Förutom Cloud Manager-gränsen för installerade certifikat tillämpar vi våra krypteringar sina egna hastighetsbegränsningar. En nyckelgräns är **Nya certifikat per exakt uppsättning identifierare**: upp till 5 certifikat kan utfärdas för samma uppsättning värdnamn inom en 7-dagarsperiod. Om den här gränsen uppnås visas ett fel i Cloud Manager och det går inte att skapa fler certifikat för värdnamnet förrän hastighetsbegränsningsfönstret har återställts. Information om de senaste värdena och andra relaterade begränsningar finns i dokumentationen om [Låt oss kryptera hastighetsbegränsningar](https://letsencrypt.org/docs/rate-limits/#new-certificates-per-exact-set-of-identifiers).

## Läs mer {#learn-more}

En användare med nödvändig behörighet kan använda Cloud Manager för att hantera SSL-certifikat för ett program. Mer information om hur du använder dessa funktioner finns i följande dokument.

* [Lägg till ett SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) <!--CQDOC-21758, #4 -->
* [Hantera SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md) <!--CQDOC-21758, #4 -->

