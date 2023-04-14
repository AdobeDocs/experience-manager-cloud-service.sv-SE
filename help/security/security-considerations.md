---
title: AEM as a Cloud Service säkerhetsfrågor
description: Läs om viktiga säkerhetsfrågor när du använder AEM as a Cloud Service
hidefromtoc: true
hide: true
source-git-commit: 39ffd826f5d1e9cea2e6a03a74f39c16647b45fa
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---


# AEM as a Cloud Service säkerhetsfrågor {#security-considerations}

## AEM Trust Store {#aem-trust-store}

För att stödja asymmetriska kryptografiska åtgärder lagrar AEM certifikat inuti innehållsarkivet i ett globalt förtroendearkiv. Innehållet är offentligt och är som standard anonymt tillgängligt för alla på utgivarinstanser.

### Egenskaper hos Trust Store {#truststore-characteristics}

* Förtroendearkivet finns nedan `/etc/truststore` och består av en Java-nyckelfil, nyckelbehållarlösenordet och databasmetadata. Observera att både lösenordet och själva nyckelbehållaren är krypterade av tekniska skäl, även om de certifikat som finns som standard är tillgängliga för alla via API:t
* Innan i rutan används certifikaten endast för HTTPS- och SAML-stöd, och arkivet måste skapas manuellt först
* Kunderna kan använda den i sin egen kod via [API för nyckelbehållare](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/adobe/granite/keystore/KeyStoreService.html#getTrustStore-org.apache.sling.api.resource.ResourceResolver-)
* Trust-butiken kan hanteras via användargränssnittet på **verktyg** - **Säkerhet** - **Trust Store** eller genom åtkomst *`https://serveraddress:serverport/libs/granite/security/content/truststore.html`*, enligt nedan:

   ![Hantering av betrodda arkiv](/help/security/assets/global-trust-store-modified.png)

* Åtkomsten till förtroendearkivet kan begränsas ytterligare av åtkomstkontrollen i databasen beroende på användningsfallet.

>[!NOTE]
>
>Adobe rekommenderar att standardåtkomstkontrollerna används för Trust Store, vilket betyder att den förblir tillgänglig för alla. För den säkraste konfigurationen kan du använda en princip för att neka jcr:all för alla.

<!--
Commenting out section for now as requested by Lars

## Anonymous Permission Hardening Package {#anonymous-permission-hardening-package}

For more information on the Anonymous Hardening Package, please see the [Security Checklist](https://experienceleague.adobe.com/docs/experience-manager-65/administering/security/security-checklist.html#anonymous-permission-hardening-package).
-->
