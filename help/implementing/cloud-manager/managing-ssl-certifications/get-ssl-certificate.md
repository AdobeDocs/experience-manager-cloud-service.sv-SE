---
title: Hämta ett SSL-certifikat - Hantera SSL-certifikat
description: Hämta ett SSL-certifikat - Hantera SSL-certifikat
translation-type: tm+mt
source-git-commit: fecbd0b4d5cfd8aa970c235c79158bea44403c09
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 0%

---


# Hämtar ett SSL-certifikat {#getting-an-ssl-certificate}

Företag använder SSL-certifikat för att skydda sina webbplatser och låta sina kunder lita på dem. För att SSL-protokollet ska kunna användas måste ett SSL-certifikat användas på en webbserver. Molnhanteraren tillhandahåller inte SSL-certifikat eller privata nycklar. Dessa måste hämtas från certifikatutfärdare.

När en entitet begär ett certifikat från en certifikatutfärdare slutför certifikatutfärdaren en verifieringsprocess. Detta kan omfatta allt från verifiering av domännamnskontroll till insamling av registreringsdokument och prenumerationsavtal. När informationen för en entitet har verifierats signerar certifikatutfärdaren sin offentliga nyckel med certifikatutfärdarens privata nyckel. Eftersom alla viktiga certifikatutfärdare har rotcertifikat i webbläsare länkas entitetens certifikat via en *förtroendekedja* och webbläsaren identifierar det som ett betrott certifikat.

>[!NOTE]
>AEM som Cloud Service accepterar endast OV- (Organization Validation) eller EV-certifikat (Extended Validation). DV (domänvalidering) eller självsignerade certifikat accepteras inte. OV- och EV-certifikat ger användarna extra, CA-verifierad information som de kan använda för att avgöra om ägaren till en webbplats, avsändaren av ett e-postmeddelande eller den digitala undertecknaren av körbar kod eller PDF-dokument är betrodd. DV-certifikat är vanliga och billiga. De tillåter dock inte ägarskapsverifiering.

