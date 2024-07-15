---
title: Extern URL
description: Externalizer är en OSGi-tjänst som gör att du programmässigt kan omvandla en resurssökväg till en extern och absolut URL.
exl-id: 06efb40f-6344-4831-8ed9-9fc49f2c7a3f
feature: Developing
role: Admin, Architect, Developer
source-git-commit: 646ca4f4a441bf1565558002dcd6f96d3e228563
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 0%

---

# Extern URL {#externalizing-urls}

I AEM är **Externalizer** en OSGi-tjänst som gör att du programmässigt kan omvandla en resurssökväg (till exempel `/path/to/my/page`) till en extern och absolut URL (till exempel `https://www.mycompany.com/path/to/my/page`) genom att prefixera sökvägen med en förkonfigurerad DNS.

Eftersom en AEM as a Cloud Service-instans inte känner till sin externt synliga URL-adress och eftersom en länk ibland måste skapas utanför det begärda omfånget, utgör den här tjänsten en central plats för att konfigurera dessa externa URL-adresser och skapa dem.

I den här artikeln beskrivs hur du konfigurerar tjänsten Externalizer och hur du använder den. Mer teknisk information om tjänsten finns i [Javadocs](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/Externalizer.html).

## Externalizerns standardbeteende och hur du åsidosätter {#default-behavior}

Externalizer-tjänsten kopplar en handfull domänidentifierare till absoluta URL-prefix som matchar de AEM URL:er som har genererats för miljön, till exempel `author https://author-p12345-e6789.adobeaemcloud.com` och `publish https://publish-p12345-e6789.adobeaemcloud.com`. Bas-URL:erna för var och en av dessa standarddomäner läses från miljövariabler som definieras av Cloud Manager.

OSGi-standardkonfigurationen för `com.day.cq.commons.impl.ExternalizerImpl.cfg.json` är effektiv som referens:

```json
{
   "externalizer.domains": [
      "local $[env:AEM_EXTERNALIZER_LOCAL;default=http://localhost:4502]",
      "author $[env:AEM_EXTERNALIZER_AUTHOR;default=http://localhost:4502]",
      "publish $[env:AEM_EXTERNALIZER_PUBLISH;default=http://localhost:4503]",
      "preview $[env:AEM_EXTERNALIZER_PREVIEW;default=http://localhost:4503]"
   ]
}
```

>[!CAUTION]
>
>Standarddomänmappningarna `local`, `author`, `preview` och `publish` Externalizer i OSGi-konfigurationen måste behållas med de ursprungliga `$[env:...]`-värdena som anges ovan.
>
>Om du distribuerar en anpassad `com.day.cq.commons.impl.ExternalizerImpl.cfg.json`-fil till AEM as a Cloud Service som inte innehåller någon av dessa domänmappningar som inte är installerade, kan det leda till oförutsägbara programbeteenden.

Om du vill åsidosätta värdena `preview` och `publish` använder du Cloud Manager-miljövariabler enligt beskrivningen i artikeln [Konfigurera OSGi för AEM as a Cloud Service](/help/implementing/deploying/configuring-osgi.md#cloud-manager-api-format-for-setting-properties) och ange de fördefinierade variablerna `AEM_CDN_DOMAIN_PUBLISH` och `AEM_CDN_DOMAIN_PREVIEW`.

## Konfigurera tjänsten Externalizer {#configuring-the-externalizer-service}

Med tjänsten Externalizer kan du centralt definiera den domän som kan användas för att programmässigt prefix för resurssökvägar. Tjänsten Externalizer bör endast användas för program med en enda domän.

>[!NOTE]
>
>Precis som när du tillämpar en [OSGi-konfiguration för AEM as a Cloud Service ](/help/implementing/deploying/overview.md#osgi-configuration) ska följande steg utföras på en lokal utvecklarinstans och sedan implementeras i din projektkod för distribution.

Så här definierar du en domänmappning för tjänsten Externalizer:

1. Navigera till Configuration Manager via:

   `https://<host>:<port>/system/console/configMgr`

1. Klicka på **Day CQ Link Externalizer** för att öppna konfigurationsdialogrutan.

   ![OSIG-konfigurationen för Externalizer](./assets/externalizer-osgi.png)

   >[!NOTE]
   >
   >Den direkta länken till konfigurationen är `https://<host>:<port>/system/console/configMgr/com.day.cq.commons.impl.ExternalizerImpl`

1. Definiera en **domänmappning**. En mappning består av ett unikt namn som kan användas i koden för att referera till domänen, ett blanksteg och domänen:

   `<unique-name> [scheme://]server[:port][/contextpath]`

   Var:

   * **`scheme`** är vanligtvis http eller https, men kan vara ett annat protokoll.

      * Adobe rekommenderar att du använder https för att framtvinga https-länkar.
      * Det används om klientkoden inte åsidosätter schemat när en URL-adress ska utgöras.

   * **`server`** är värdnamnet (antingen ett domännamn eller en IP-adress).
   * **`port`** (valfritt) är portnumret.
   * **`contextpath`** (valfritt) anges bara om AEM har installerats som en webbapp under en annan kontextsökväg.

   Till exempel: `production https://my.production.instance`

   Följande mappningsnamn är fördefinierade och måste alltid anges som AEM är beroende av dem:

   * `local` - den lokala instansen
   * `author` - redigeringssystemets DNS
   * `publish` - den offentliga webbplatsens DNS

   >[!NOTE]
   >
   >Med en anpassad konfiguration kan du lägga till en ny kategori, till exempel `production`, `staging` eller till och med externa icke-AEM system som `my-internal-webservice`. Det är användbart att undvika hårdkodning av sådana URL:er på olika platser i ett projekts kodbas.

1. Klicka på **Spara** för att spara ändringarna.

### Använda tjänsten Externalizer {#using-the-externalizer-service}

I det här avsnittet visas några exempel på hur Externalizer-tjänsten kan användas.

>[!NOTE]
>
>Inga absoluta länkar bör skapas i HTML. Använd därför inte denna funktion i sådana fall.

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

* **Så här gör du en extern sökväg med domänen local:**

  ```java
  String myExternalizedUrl = externalizer.externalLink(resolver, Externalizer.LOCAL, "/my/page") + ".html";
  ```

  Anta domänmappningen:

   * `local https://publish-3.internal`

   * `myExternalizedUrl` slutar med värdet:

   * `https://publish-3.internal/contextpath/my/page.html`

>[!TIP]
>
>Fler exempel finns i [Javadocs](https://www.adobe.io/experience-manager/reference-materials/cloud-service/javadoc/com/day/cq/commons/Externalizer.html).
