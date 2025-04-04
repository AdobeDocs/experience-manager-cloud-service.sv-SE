---
title: Hur felsöker man fel vid formulärframtagning?
description: Felsöka fel när formulär skapas i AEM Forms as a Cloud Service-miljö.
feature: Adaptive Forms
role: User
exl-id: 169ea727-0941-4a1d-bc33-d9fe208b27ab
source-git-commit: 0b693cb51a96011235fa87a5899426c6b0c2509a
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---

# Problem vid publicering av formulär{#form-creation-fails}

När användare har uppdaterat till AEM Forms as a Cloud Service version `2024.5.16461`:

**Vissa användare** kan ha problem med att skapa formulär. Problemet är att när en användare skapar ett formulär visas följande felmeddelande i dialogrutan Skapa:

`A server error occurred. Try again after sometime.`

## Orsak {#cause-form-creation-fails}

Problemet inträffar eftersom författaren publicerar formuläret utan att **först publicera mallen** som används i det. Detta resulterar i att `jcr:uuid` och andra skyddade och systemgenererade egenskaper läggs till i noden `<template-path>/initial/jcr:content`, vilket orsakar fel vid efterföljande formulärskapande.

## Tillfällig lösning {#resolution-form-creation-fails}

Så här löser du problemet:

1. Kontrollera att mallen som du använder i formuläret inte har `jcr:uuid` och andra systemgenererade skyddade egenskaper på sökvägen `<template-path>/initial/jcr:content node`.
1. Publish mallen explicit med mallkonsolen.
1. När mallen har publicerats kan du testa att skapa nya formulär med hjälp av mallen.
1. Om mallen som du använde uppdaterar i de kommande versionerna, Publish mallen igen (som i steg 2) för att förhindra problem med att skapa formulär.


<!--

# Issue {#form-creation-fails}

After updating to AEM Forms as a Cloud Service version `2024.5.16461.20240524T172309Z`, When a user publishes a form using an unpublished template, it fails to create a form and shows an error:

`Property is protected: jcr:uuid = 09e0d6be-f619-4405-b021-27eb1c5326d3`

## Solution {#troubleshoot-form-creation-fails}

To resolve the issue, perform the following workaround steps:

1. Publish the template explicitly using the template console.
    
    >[!NOTE]
    > Prior to this step ensure that the (unpublished) template does not have `jcr:uuid` and other system generated properties under the initial content's `jcr:content node`. To sort out it, first, sanitize the template to publish it explicitly.

    >[!NOTE]
    > This action doesn't replicate the initial content node.
1. Now, when your template is published, try creating new forms using the template.
1. If the template is changed in the future, publish it again as mentioned in the step 1.

-->
