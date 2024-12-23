---
title: Hur startar jag om AEM SDK?
description: De bästa sätten att starta om AEM SDK
role: Admin, Developer, User
feature: Adaptive Forms
exl-id: 5fec2a93-1dda-4240-8690-24a6afae5c2b
source-git-commit: 62be3c6e98df9002cdfbeef50dd5475c4daa1576
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 0%

---

# Starta om AEM SDK

Om du startar om AEM SDK genom att stoppa Java™-processerna kan det leda till inkonsekvenser i den AEM utvecklingsmiljön. Ett fel inträffar enligt följande:

`javax.jcr.RepositoryException: Applying repoinit operation failed despite retry; set loglevel to DEBUG to see all exceptions. Last exception message was: Failed to set ACL (javax.jcr.ValueFormatException: Invalid type: 0) AclLine ALLOW {principals=[forms-xfa-writers], privileges=[jcr:modifyProperties]} restrictions=[rep:glob=[*/jcr:content/*], rep:itemNames=[xfaForm], fd:condition=[xfaForm, 1]]`

![Restart-aem-sdk-error](/help/forms/assets/restart-sdk-error.png)

## Lösning

Om du vill starta om AEM SDK går du till det aktiva kommandofönstret och trycker på `Ctrl + C` för att starta om SDK.

Du bör använda kommandot Ctrl + C för att starta om SDK:n. Om du startar om AEM SDK med alternativa metoder, till exempel genom att stoppa Java™-processer, kan det leda till inkonsekvenser i den AEM utvecklingsmiljön.

## Se även

* [Konfigurera lokal utvecklingsmiljö för AEM Forms](/help/forms/setup-local-development-environment.md)
* [Aktivera adaptiva Forms Core-komponenter](/help/forms/enable-adaptive-forms-core-components.md)
