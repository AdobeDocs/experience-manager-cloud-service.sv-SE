---
title: AEM as a Cloud Service säkerhetsfrågor
description: Läs om viktiga säkerhetsfrågor när du använder AEM as a Cloud Service.
hidefromtoc: true
hide: true
exl-id: d2dfde05-ce02-478e-8697-b939fb8740c3
source-git-commit: 678e81eb22cc1d7c239ac7a2594b39a3a60c51e2
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---

# AEM as a Cloud Service säkerhetsfrågor {#security-considerations}

## AEM Trust Store {#aem-trust-store}

För att stödja asymmetriska, kryptografiska åtgärder lagrar AEM certifikat inuti innehållsarkivet i en global betrodd lagringsplats. Innehållet är offentligt och är som standard anonymt tillgängligt för alla på utgivarinstanser.

### Egenskaper hos Trust Store {#truststore-characteristics}

* Förtroendearkivet finns nedan `/etc/truststore` och består av en Java™-nyckelfil, nyckelbehållarlösenordet och databasmetadata. Både lösenordet och nyckelbehållaren krypteras av tekniska skäl, även om de certifikat som finns som standard är tillgängliga för alla via API:t
* Innan i rutan används certifikaten endast för HTTPS- och SAML-stöd, och arkivet måste skapas manuellt först
* Kunderna kan använda den i sin egen kod via [API för nyckelbehållare](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/keystore/KeyStoreService.html#getTrustStore-org.apache.sling.api.resource.ResourceResolver-)
* Trust-butiken kan hanteras via användargränssnittet på **verktyg** - **Säkerhet** - **Trust Store** eller genom åtkomst *`https://serveraddress:serverport/libs/granite/security/content/truststore.html`*, enligt nedan:

  ![Hantering av betrodda arkiv](/help/security/assets/global-trust-store-modified.png)

* Åtkomsten till förtroendearkivet kan begränsas ytterligare av åtkomstkontrollen i databasen beroende på användningsfallet.

>[!NOTE]
>
>Adobe rekommenderar att standardåtkomstkontrollerna används för Trust Store, vilket betyder att den förblir tillgänglig för alla. För den säkraste konfigurationen kan du använda en nekandeprincip `jcr:all` för alla.

<!--
Commenting out section for now as requested by Lars

## Anonymous Permission Hardening Package {#anonymous-permission-hardening-package}

For more information on the Anonymous Hardening Package, see [Security Checklist](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-checklist.html#anonymous-permission-hardening-package).
-->
