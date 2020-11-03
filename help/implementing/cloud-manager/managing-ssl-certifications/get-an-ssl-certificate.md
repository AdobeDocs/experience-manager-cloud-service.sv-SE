---
title: Hämta ett SSL-certifikat - Hantera SSL-certifikat
description: Hämta ett SSL-certifikat - Hantera SSL-certifikat
translation-type: tm+mt
source-git-commit: b0162640b6d85291aba9c926138f39a0433c0a6e
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 0%

---


# Hämta ett SSL-certifikat {#getting-an-ssl-certificate}

Företag använder SSL-certifikat för att skydda sina webbplatser och låta sina kunder lita på dem. För att SSL-protokollet ska kunna användas måste ett SSL-certifikat användas på en webbserver. Molnhanteraren tillhandahåller inte SSL-certifikat eller privata nycklar. Dessa måste hämtas från certifikatutfärdare.

När en entitet begär ett certifikat från en certifikatutfärdare (CA) slutför certifikatutfärdaren en verifieringsprocess. Detta kan omfatta allt från verifiering av domännamnskontroll till insamling av registreringsdokument och prenumerationsavtal.

När informationen för en entitet har verifierats signerar certifikatutfärdaren sin offentliga nyckel med certifikatutfärdarens privata nyckel. Eftersom alla viktiga certifikatutfärdare har rotcertifikat i webbläsare kommer entitetens certifikat att länkas via en *förtroendekedja* och webbläsaren kommer att känna igen det som ett pålitligt certifikat.

