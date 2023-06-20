---
title: Introduktion till hantering av SSL-certifikat
description: Lär dig hur du får tillgång till självbetjäningsverktyg i Cloud Manager för att installera SSL-certifikat.
exl-id: 0d41723c-c096-4882-a3fd-050b7c9996d8
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '632'
ht-degree: 0%

---


# Introduktion till hantering av SSL-certifikat{#introduction}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_sslcert"
>title="Hantera SSL-certifikat"
>abstract="Läs om hur du får tillgång till självbetjäningsverktyg i Cloud Manager för att installera och hantera SSL-certifikat för att skydda din webbplats för användarna. Cloud Manager använder en TLS-plattformstjänst för att hantera SSL-certifikat och privata nycklar som ägs av kunder och som erhållits från tredjepartscertifikatutfärdare."
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates.html" text="Visa, uppdatera och ersätta ett SSL-certifikat"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/managing-certificates.html" text="Kontrollera status för ett SSL-certifikat"

Med Cloud Manager får du tillgång till självbetjäningsverktyg för att installera och hantera SSL-certifikat så att du kan skydda din webbplats för användarna. Cloud Manager använder en TLS-plattformstjänst för att hantera SSL-certifikat och privata nycklar som ägs av kunder och som erhållits från tredjepartscertifikatutfärdare, till exempel Let&#39;s Encrypt.

## Introduktion till certifikat {#certificates}

Företag använder SSL-certifikat för att skydda sina webbplatser och låta sina kunder lita på dem. Om du vill använda SSL-protokollet måste ett SSL-certifikat användas på en webbserver.

När en entitet begär ett certifikat från en certifikatutfärdare slutför certifikatutfärdaren en verifieringsprocess. Detta kan omfatta allt från verifiering av domännamnskontroll till insamling av registreringsdokument och prenumerationsavtal. När informationen för en entitet har verifierats signerar certifikatutfärdaren sin offentliga nyckel med certifikatutfärdarens privata nyckel. Eftersom alla viktiga certifikatutfärdare har rotcertifikat i webbläsare länkas entitetens certifikat via en *förtroendekedja* och webbläsaren kommer att känna igen det som ett pålitligt certifikat.

>[!IMPORTANT]
>
>Molnhanteraren tillhandahåller inte SSL-certifikat eller privata nycklar. Dessa måste hämtas från certifikatutfärdare.

## SSL-hanteringsfunktioner i molnhanteraren {#features}

Cloud Manager stöder följande användningsalternativ för SSL-certifikat från kund.

* Ett SSL-certifikat kan användas i flera miljöer. Det kan alltså läggas till en gång och användas flera gånger.
* Varje Cloud Manager-miljö kan använda flera certifikat.
* En privat nyckel kan utfärda flera SSL-certifikat.
* Varje certifikat innehåller vanligtvis flera domäner.
* Plattformens TLS-tjänst skickar förfrågningar till kundens CDN-tjänst baserat på det SSL-certifikat som används för att avsluta och den CDN-tjänst som är värd för den domänen.
* AEM as a Cloud Service godkänner SSL-jokertecken för en domän.

## Recommendations {#recommendations}

AEM as a Cloud Service stöder endast `https` webbplatser.

* Kunder med flera anpassade domäner vill inte överföra ett certifikat varje gång de lägger till en domän.
* Sådana kunder tjänar på att skaffa ett certifikat med flera domäner.

## Krav {#requirements}

* AEM as a Cloud Service godkänner endast certifikat som överensstämmer med OV- (Organization Validation) eller EV-principen (Extended Validation).
* Alla certifikat måste vara ett X.509 TLS-certifikat från en betrodd certifikatutfärdare (CA) med en matchande 2 048-bitars RSA privat nyckel.
* DV-principen (Domain Validation) accepteras inte.
* Självsignerade certifikat accepteras inte.

OV- och EV-certifikat ger användarna extra, CA-validerad information som kan användas för att avgöra om ägaren till en webbplats, avsändaren av ett e-postmeddelande eller den digitala undertecknaren av körbar kod eller PDF-dokument är betrodd. DV-certifikat tillåter inte sådan ägarskapsverifiering.

## Begränsningar {#limitations}

Vid en given tidpunkt tillåter Cloud Manager att högst 50 SSL-certifikat installeras. Dessa kan kopplas till en eller flera miljöer i programmet och även omfatta certifikat som gått ut.

Om du har nått gränsen kan du granska dina certifikat och överväga:

* Tar bort certifikat som gått ut.
* Gruppera flera domäner i samma certifikat eftersom ett certifikat kan omfatta flera domäner (upp till 100 SAN-nätverk).

## Läs mer {#learn-more}

En användare med nödvändig behörighet kan använda Cloud Manager för att hantera SSL-certifikat för ett program. Mer information om hur du använder dessa funktioner finns i följande dokument.

* [Lägga till ett SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)
* [Visa, uppdatera eller ersätta ett SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
* [Ta bort ett SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/managing-certificates.md)
