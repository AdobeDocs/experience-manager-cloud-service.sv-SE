---
title: Skicka en AEM-anslutning
description: Skicka en AEM-anslutning
translation-type: tm+mt
source-git-commit: d4e376ab30bb3e1fb533ed32f6ac43580775787c
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 11%

---


Skicka en AEM-anslutning
===========================

Nedan finns användbar information om hur du skickar in AEM-kopplingar och den bör läsas tillsammans med artiklarna om [implementering](implement.md) och [underhåll](maintain.md) av kopplingar.

AEM Connectors listas på [Adobe Exchange](https://partners.adobe.com/exchangeprogram/experiencecloud).

I tidigare AEM lösningar användes Package Manager för att installera anslutningar på olika AEM instanser. Men med AEM som Cloud Service distribueras anslutningar under CI/CD-processen i Cloud Manager. För att anslutningarna ska kunna distribueras måste det finnas referenser till anslutningarna i maven-projektets pom.xml.

Det finns olika alternativ för hur paketen kan inkluderas i ett projekt:

1. Partnerns offentliga arkiv - en partner skulle vara värd för innehållspaketet i ett offentligt tillgängligt arkiv
1. Partnerns lösenordsskyddade arkiv - en partner lagrar innehållspaketet i en lösenordsskyddad maven-databas. Mer information finns i [lösenordsskyddade maven-databaser på](/help/onboarding/getting-access-to-aem-in-cloud/setting-up-project.md#password-protected-maven-repositories).
1. Paket med sammankopplade artefakter - i det här fallet inkluderas kopplingspaketet lokalt i kundens maven-projekt.

Oavsett var de finns måste paket refereras som beroenden i pom.xml, vilket tillhandahålls av leverantören.

```xml
<!-- UberJAR Dependency to be added to the project's Reactor pom.xml -->
<dependency>
  <groupId>com.partnername</groupId>
  <artifactId>my-artifact</artifactId>
  <version>V123</version> <!-- use the latest! -->
  <scope>provided</scope>
  <classifier>my_classifier</classifier>
</dependency>
```

Om ISV-partnern är värd för anslutningen på en Internet-åtkomlig (till exempel Cloud Manager-tillgänglig) maven-databas, bör ISV tillhandahålla den databaskonfiguration där pom.xml kan placeras, så att anslutningsberoendena (ovan) kan lösas vid byggtillfället (både lokalt och av Cloud Manager).

```xml
<repository>
    <id>the-repository</id>
    <name>The Repository Where the Connector is Hosted</name>
    <url>https://repo.partnername.com/repositories/aem_connector_repo</url>
    <releases>
        <enabled>true</enabled>
        <updatePolicy>never</updatePolicy>
    </releases>
    <snapshots>
        <enabled>false</enabled>
    </snapshots>
</repository>
```

Om ISV-partnern väljer att distribuera anslutningsprogrammet som hämtningsbara filer, ska ISV-partnern ge instruktioner om hur filerna kan distribueras till en lokal filsystemmaven-databas som måste checkas in i Git som en del av AEM, så att Cloud Manager kan lösa dessa beroenden.
