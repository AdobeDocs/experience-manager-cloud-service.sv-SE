---
title: Hämta ett SSL-certifikat - Hantera SSL-certifikat
description: Hämta ett SSL-certifikat - Hantera SSL-certifikat
exl-id: a3a247e5-164a-4c9c-aeed-bde882635e6f
source-git-commit: 90de3cf9bf1c949667f4de109d0b517c6be22184
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 0%

---

# Hämta ett SSL-certifikat {#getting-an-ssl-certificate}

Företag använder SSL-certifikat för att skydda sina webbplatser och låta sina kunder lita på dem. För att SSL-protokollet ska kunna användas måste ett SSL-certifikat användas på en webbserver. Molnhanteraren tillhandahåller inte SSL-certifikat eller privata nycklar. Dessa måste hämtas från certifikatutfärdare.

När en entitet begär ett certifikat från en certifikatutfärdare slutför certifikatutfärdaren en verifieringsprocess. Detta kan omfatta allt från verifiering av domännamnskontroll till insamling av registreringsdokument och prenumerationsavtal. När informationen för en entitet har verifierats signerar certifikatutfärdaren sin offentliga nyckel med certifikatutfärdarens privata nyckel. Eftersom alla viktiga certifikatutfärdare har rotcertifikat i webbläsare länkas entitetens certifikat via en *förtroendekedja* och webbläsaren kommer att känna igen det som ett pålitligt certifikat.

>[!NOTE]
>AEM as a Cloud Service godkänner endast OV- (Organization Validation) eller EV-certifikat (Extended Validation). DV (domänvalidering) eller självsignerade certifikat accepteras inte. OV- och EV-certifikat ger användarna extra, CA-verifierad information som de kan använda för att avgöra om ägaren till en webbplats, avsändaren av ett e-postmeddelande eller den digitala undertecknaren av körbar kod eller PDF-dokument är betrodd. DV-certifikat är vanliga och billiga. De tillåter dock inte ägarskapsverifiering.
>Dessutom måste alla certifikat vara ett X.509 TLS-certifikat från en betrodd certifikatutfärdare (CA) med en matchande 2 048-bitars RSA privat nyckel.
