---
title: Extern URL
description: Externalizer är en OSGi-tjänst som gör att du kan omvandla en resurssökväg programmatiskt till en extern och absolut URL.
exl-id: 06efb40f-6344-4831-8ed9-9fc49f2c7a3f
source-git-commit: c08e442e58a4ff36e89a213aa7b297b538ae3bab
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 0%

---

# Extern URL {#externalizing-urls}

AEM **Externalizer** är en OSGi-tjänst som gör att du kan omvandla en resurssökväg med programkod (t.ex. `/path/to/my/page`) till en extern och absolut URL (till exempel `https://www.mycompany.com/path/to/my/page`) genom att ange sökvägen som prefix med en förkonfigurerad DNS.

Eftersom en AEM as a Cloud Service instans inte kan känna till sin externt synliga URL och eftersom en länk ibland måste skapas utanför det begärda omfånget, tillhandahåller den här tjänsten en central plats för att konfigurera dessa externa URL:er och skapa dem.

I den här artikeln beskrivs hur du konfigurerar tjänsten Externalizer och hur du använder den. Tekniska detaljer om tjänsten finns i [Javadocs](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/Externalizer.html).

## Externalizerns standardbeteende och hur du åsidosätter {#default-behavior}

Externalizer-tjänsten har värden som `author-p12345-e6789.adobeaemcloud.com` och `publish-p12345-e6789.adobeaemcloud.com`.

Om du vill åsidosätta sådana värden använder du Cloud Managers miljövariabler enligt beskrivningen i artikeln [Konfigurera OSGi för AEM as a Cloud Service](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) och ange fördefinierade `AEM_CDN_DOMAIN_AUTHOR` och `AEM_CDN_DOMAIN_PUBLISH` variabler.

## Konfigurera tjänsten Externalizer {#configuring-the-externalizer-service}

Med tjänsten Externalizer kan du centralt definiera den domän som kan användas för att programmässigt prefix för resurssökvägar. Externalizer-tjänsten bör endast användas för program med en enda domän.

>[!NOTE]
>
>Som när du använder [OSGi-konfigurationer för AEM as a Cloud Service,](/help/implementing/deploying/overview.md#osgi-configuration) följande steg ska utföras på en lokal utvecklarinstans och sedan implementeras i projektkoden för distribution.

Så här definierar du en domänmappning för tjänsten Externalizer:

1. Navigera till Configuration Manager via:

   `https://<host>:<port>/system/console/configMgr`

1. Klicka **Day CQ Link Externalizer** för att öppna konfigurationsdialogrutan.

   ![Externalizer OSGi-konfigurationen](./assets/externalizer-osgi.png)

   >[!NOTE]
   >
   >Den direkta länken till konfigurationen är `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`

1. Definiera en **Domäner** mappning. En mappning består av ett unikt namn som kan användas i koden för att referera till domänen, ett blanksteg och domänen:

   `<unique-name> [scheme://]server[:port][/contextpath]`

   Var:

   * **`scheme`** är vanligtvis http eller https, men kan vara ett annat protokoll.

      * Vi rekommenderar att du använder https för att framtvinga https-länkar.
      * Den används om klientkoden inte åsidosätter schemat när en URL-adress ska utgöras.
   * **`server`** är värdnamnet (antingen ett domännamn eller en IP-adress).
   * **`port`** (valfritt) är portnumret.
   * **`contextpath`** (valfritt) anges bara om AEM har installerats som ett webbprogram under en annan kontextsökväg.

   Till exempel: `production https://my.production.instance`

   Följande mappningsnamn är fördefinierade och måste alltid anges som AEM är beroende av dem:

   * `local` - den lokala instansen
   * `author` - redigeringssystemets DNS
   * `publish` - den offentliga webbplatsens DNS

   >[!NOTE]
   >
   >Med en anpassad konfiguration kan du lägga till en ny kategori, till exempel `production`, `staging` eller till och med externa icke-AEM system som `my-internal-webservice`. Det är användbart att undvika hårdkodning av sådana URL:er på olika platser i ett projekts kodbas.

1. Klicka **Spara** för att spara ändringarna.

### Använda tjänsten Externalizer {#using-the-externalizer-service}

I det här avsnittet visas några exempel på hur Externalizer-tjänsten kan användas.

>[!NOTE]
>
>Inga absoluta länkar bör skapas i HTML. Denna funktion bör därför inte användas i sådana fall.

* **Så här gör du en extern sökväg med domänen &#39;publish&#39;:**

   ```java
   String myExternalizedUrl = externalizer.publishLink(resolver, "/my/page") + ".html";
   ```

   Anta domänmappningen:

   * `publish https://www.website.com`

   * `myExternalizedUrl` slutar med värdet:

   * `https://www.website.com/contextpath/my/page.html`

* **Så här gör du en extern sökväg med domänen &#39;författare&#39;:**

   ```java
   String myExternalizedUrl = externalizer.authorLink(resolver, "/my/page") + ".html";
   ```

   Anta domänmappningen:

   * `author https://author.website.com`

   * `myExternalizedUrl` slutar med värdet:

   * `https://author.website.com/contextpath/my/page.html`

* **Så här externaliserar du en sökväg med domänen&quot;local&quot;:**

   ```java
   String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
   ```

   Anta domänmappningen:

   * `local https://publish-3.internal`

   * `myExternalizedUrl` slutar med värdet:

   * `https://publish-3.internal/contextpath/my/page.html`

>[!TIP]
>
>Du hittar fler exempel i [Javadocs](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/Externalizer.html).
