---
title: Skicka en AEM
description: Lär dig hur du refererar till och distribuerar anslutningar på rätt sätt i Adobe Experience Manager (AEM) as a Cloud Service.
exl-id: 9be1f00e-3666-411c-9001-c047e90b6ee5
feature: Operations
role: Admin
source-git-commit: 0e328d013f3c5b9b965010e4e410b6fda2de042e
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 0%

---

# Skicka en AEM

Nedan finns användbar information om hur du skickar Adobe Experience Manager (AEM) Connectors och den bör läsas med artiklar om [implementering](implement.md) och [underhåll](maintain.md).

AEM Connectors listas på [Adobe Exchange](https://partners.adobe.com/technologyprogram/experiencecloud.html).

I tidigare AEM användes [Package Manager](/help/implementing/developing/tools/package-manager.md) för att installera anslutningar på olika AEM instanser. Men med AEM as a Cloud Service driftsätts anslutningar under CI/CD-processen i Cloud Manager. För att anslutningarna ska kunna distribueras måste det finnas referenser till anslutningarna i maven-projektets pom.xml.

Det finns olika alternativ för hur paketen kan inkluderas i ett projekt:

1. Partnerns offentliga arkiv - en partner skulle vara värd för innehållspaketet i ett offentligt tillgängligt arkiv
1. Partnerns lösenordsskyddade arkiv - en partner lagrar innehållspaketet i en lösenordsskyddad maven-databas. Mer information finns i [lösenordsskyddade maven-databaser](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/create-application-project/setting-up-project.html#password-protected-maven-repositories).
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

Om ISV-partnern är värd för anslutningen på en Internet-tillgänglig (t.ex. Cloud Manager-tillgänglig) mapdatabas, bör ISV-partnern tillhandahålla den databaskonfiguration där `pom.xml` kan placeras. Orsaken är att anslutningsberoendena (ovan) kan lösas vid byggtillfället, både lokalt och av Cloud Manager.

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

Om ISV-partnern väljer att distribuera anslutningsprogrammet som hämtningsbara filer bör ISV-partnern ge instruktioner. Instruktionen bör beskriva hur filerna kan distribueras till en lokal filsystemdatabas som måste checkas in i Git som en del av AEM. Detta garanterar att Cloud Manager kan lösa dessa beroenden.
