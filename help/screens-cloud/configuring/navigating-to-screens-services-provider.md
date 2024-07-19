---
title: Navigera till Screens Services Provider
description: På den här sidan beskrivs hur du navigerar till Screens Services Provider.
exl-id: 9eff6fe8-41d4-4cf3-b412-847850c4e09c
feature: Administering Screens
role: Admin, Developer, User
source-git-commit: f91166ca0349636386aa8721ded5b3bbda1cdb51
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Navigera till Screens Services Provider {#setup-screens-services-provider}

## Introduktion {#introduction}

**Screens Services Provider** tillåter innehållsförfattaren, utvecklare och administratörer att hantera skärmar och spelare för uppspelning av innehåll när innehållet har lagts till i kanalerna. När användarna har fått tillgång till AEM Cloud Service bör de kunna logga in på Screens tjänsteleverantör.

I det här avsnittet beskrivs hur du konfigurerar Screens Services Provider.


## Syfte {#objective}

Följande avsnitt visar hur du konfigurerar och konfigurerar Screens Services Provider.

## Steg för att konfigurera Screens Services Provider {#screens-services-provider}

Följ stegen nedan för att konfigurera Screens Services Provider:

1. Navigera till Screens Services Provider från [här](https://experience.adobe.com/screens).

   >[!CAUTION]
   >Om du har tillgång till flera organisationer måste du se till att du har loggat in på rätt organisation. Om du vill ändra organisation klickar du på organisationsnamnet i det övre högra hörnet av skärmen och väljer den organisation som du behöver åtkomst till.

1. Klicka på kugghjulsikonen bredvid Projekt (övre vänstra hörnet)

   ![bild](/help/screens-cloud/assets/configure/configure-screens0.png)

1. Ange följande information i dialogrutan Redigera inställningar.
   * **Publish-URL** - AEM publicerings-URL (till exempel `https://publish-p12345-e12345.adobeaemcloud.com`)
   * **Skapad av-URL** - AEM författarens URL (till exempel `https://author-p12345-e12345.adobeaemcloud.com`)

   >[!NOTE]
   >Se till att du skapar och publicerar minst en AEM skärmkanal innan du konfigurerar AEM under Screens tjänsteleverantör. Om du vill skapa en kanal går du till /screens.html hos din innehållsleverantör.

   ![bild](/help/screens-cloud/assets/configure/configure-screens4.png)

1. Klicka på **Spara** för att ansluta till Screens innehållsleverantör.

1. Om du har konfigurerat den AEM publiceringsinstansen så att den bara tillåter åtkomst till betrodda IP-adresser via funktionen Cloud Manager IP Tillåtelselista, måste du konfigurera en rubrik med ett nyckelvärde i dialogrutan med inställningar som visas nedan.
De IP-adresser som behöver vitlistas måste också flyttas till konfigurationsfilen och måste vara [otillämpade](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/apply-allow-list) från Cloud Manager-inställningarna.

   ![bild](/help/screens-cloud/assets/configure/configure-screens20.png)

Samma nyckel måste konfigureras AEM CDN-konfigurationen.  Du bör inte placera rubrikvärdet direkt i GITHub och använda en [hemlig referens](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/implementing/content-delivery/cdn-credentials-authentication#rotating-secrets).
Nedan visas ett exempel på [CDN-konfiguration](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/security/traffic-filter-rules-including-waf):

    typ: &quot;CDN&quot;
    version: &quot;1&quot;
    metadata:
    envTypes: [&quot;dev&quot;, &quot;stage&quot;, &quot;prod&quot;]
    data:
    trafikFilters:
    rules:
    - name: &quot;block-request-from-not-allowed-ips&quot;
    när:
    allOf:
    }- reqProperty: clientIp
    notIn: [&quot;101.41.112.0/24&quot;]
    - reqProperty: tier
    equals: publish
    action: block
    - name: &quot;allow-requests-with-header&quot;
    when:
    allOf:
    - rerererec qProperty: tier
    equals: publish
    - reqProperty: path
    equals: /screens/channels.json
    - reqHeader: x-screens-tillåtelselista-key
    equals: ${\
    {CDN_HEADER_KEY}
    action:
    type: allow

1. Välj **Kanaler** i det vänstra navigeringsfältet och klicka på **öppna i innehållsleverantören**.

   ![bild](/help/screens-cloud/assets/configure/configure-screens1.png)

1. Screens Content Provider öppnas på en annan flik där du kan skapa ditt innehåll.

   ![bild](/help/screens-cloud/assets/configure/configure-screens2.png)

## What&#39;s Next {#whats-next}

När du har lärt dig hur du konfigurerar Screens Services Provider går du till [Använda Screens Content Provider](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/screens-as-cloud-service/configure-screens-cloud/using-screens-content-provider.html#screens-content-provider) för mer information.
