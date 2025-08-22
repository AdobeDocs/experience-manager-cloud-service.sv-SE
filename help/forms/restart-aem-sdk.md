---
title: Hur startar jag om AEM SDK?
description: De bästa sätten att starta om AEM SDK
role: Admin, Developer, User
feature: Adaptive Forms
exl-id: 5fec2a93-1dda-4240-8690-24a6afae5c2b
source-git-commit: 16b1e7ffa4e3812e9207bb283c63029939f7d14e
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 0%

---

# Starta om AEM SDK

Om du startar om AEM SDK genom att stoppa Java™-processerna kan det leda till inkonsekvenser i AEM utvecklingsmiljö. Ett fel inträffar:

`javax.jcr.RepositoryException: Applying repoinit operation failed despite retry; set loglevel to DEBUG to see all exceptions. Last exception message was: Failed to set ACL (javax.jcr.ValueFormatException: Invalid type: 0) AclLine ALLOW {principals=[forms-xfa-writers], privileges=[jcr:modifyProperties]} restrictions=[rep:glob=[*/jcr:content/*], rep:itemNames=[xfaForm], fd:condition=[xfaForm, 1]]`

![Restart-aem-sdk-error](/help/forms/assets/restart-sdk-error.png)

## Lösning

Om du vill starta om AEM SDK går du till det aktiva kommandofönstret och trycker på `Ctrl + C` för att starta om SDK.

Du bör använda kommandot Ctrl + C för att starta om SDK. Om du startar om AEM SDK med alternativa metoder, till exempel genom att stoppa Java™-processer, kan det leda till inkonsekvenser i AEM utvecklingsmiljö.

## Se även

* [Konfigurera lokal utvecklingsmiljö för AEM Forms](/help/forms/setup-local-development-environment.md)

