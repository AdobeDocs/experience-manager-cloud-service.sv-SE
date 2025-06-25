---
title: Aktivera funktionen Växla för att integrera tidiga Adobe- och prerelease-funktioner
description: Växla funktion är en funktion i AEM som gör att administratörer kan aktivera nya funktioner i en körningsmiljö.
feature: Adaptive Forms, Foundation Components, Core Components
role: User, Developer
source-git-commit: cc4fccc51f487170bf6c14e4b302a8d5912c33a0
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 0%

---

# Aktivera växling av funktioner i Adobe Experience Software Development Kit (AEM SDK)

Med Toggle för funktioner i AEM kan administratörer aktivera eller inaktivera funktioner vid körning som är idealiska för hantering av tidiga Adobe- och Prerelease-funktioner utan kodändringar. Den stöder gradvisa driftsättningar, A/B-testning och snabb inaktivering av instabila funktioner.

I den här artikeln beskrivs hur du aktiverar funktionsväxlingar i AEM Local SDK, som simulerar AEM as a Cloud Service med SDK och Dispatcher. Med den här installationen kan teamen testa i en produktionsliknande miljö innan de distribuerar till molnet.

## Varför ska du använda? Växlar i en AEM SDK-konfiguration?

När du arbetar i en AEM SDK-konfiguration växlar funktionen hjälpen i:

* Testa experimentella funktioner på ett säkert sätt.

* Nya komponenter rullas ut i faser.

* En och samma kodbas i olika miljöer.

* Minska riskerna vid driftsättning och uppgraderingar.

## Förutsättningar

Innan du aktiverar funktionsväxlingar i AEM SDK ska du kontrollera följande:

* Användaren är medlem i gruppen `forms-users`.

* Navigera till `http://<author-instance-url>:portnumber/system/console/bundles` och kontrollera om paketet **(com.adobe.granite.toggle.impl.dev-1.1.2.jar)** finns eller inte. Om det inte finns [hämtar du paketet från länken](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/hotfix/com.adobe.granite.toggle.impl.dev-1.1.2%20.jar).

  ![Växla funktion](/help/forms/assets/aem-web-console-bundle.png)

### Aktivera växling av funktioner

Följ de här stegen för att aktivera funktionsväxlingar i din AEM SDK-instans:

1. Logga in på din AEM Forms-instans.

1. Navigera till `http://author-instance-url:portnumber/system/console/configMgr`.

1. Sök efter dynamisk växlingsprovider för Adobe Granite i Configuration Manager.

   ![Växla funktion](/help/forms/assets/aem-web-console-confi.png)

1. Klicka på ikonen ✏️ .
1. Klicka på ➕ i avsnittet Aktiverade växlar.
1. Lägg till alternativknapps-ID för funktionen enligt bilden nedan.
   ![Växla funktion](/help/forms/assets/feature-toggle.png)

1. Klicka på Spara

>[!NOTE]
>
> Du kan hitta alternativknappen i dokumentet som är specifikt för de tidiga adopterfunktionerna.


### Inaktivera funktion, växla

Följ stegen nedan för att inaktivera funktionsknapparna för funktioner vars växlingsknappar är aktiverade:

1. Logga in på din AEM Forms-instans.
1. Navigera till `http://author-instance-url:portnumber/system/console/configMgr`.
1. Sök efter dynamisk växlingsprovider för Adobe Granite i Configuration Manager.
1. Klicka på ikonen ✏️.
1. Klicka på ➕ i avsnittet Inaktiverade växlar.
1. Lägg till växlingsnumret för den funktion som ska inaktiveras.

   ![Växla funktion](/help/forms/assets/disable-toggle-feature.png)

### Tekniska överväganden

Funktionsreglage hanteras under körning och passar bäst för utvecklings- och testinställningar. Kontrollera att växlarna är versionskontrollerade och synkroniserade med CI/CD i en installation av AEM SDK. Siduppdatering eller cacherensning kan behövas för att ändringarna ska speglas.

>[!NOTE]
>
> Kontakta Adobe Support-team om du vill aktivera växling av funktioner för produktionsmiljön.

