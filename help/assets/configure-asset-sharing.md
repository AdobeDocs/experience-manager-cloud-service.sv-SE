---
title: Dela resurser, mappar och samlingar som en länk
description: I den här artikeln beskrivs hur du delar resurser, mappar och samlingar i Experience Manager Assets som en hyperlänk.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 82dd9bd69fe994f74c7be8a571e386f0e902f6a1

---


# Konfigurera delning av resurslänkar {#asset-link-sharing}

<!-- TBD: Web Console is not there so how to configure Day CQ email service? Or is it not required now? -->

Använd dialogrutan Länkdelning för att generera URL:en för resurser som du vill dela med användare. Användare med administratörsbehörighet eller läsbehörighet på `/var/dam/share` platsen kan visa de länkar som delas med dem. Att dela resurser via en länk är ett bekvämt sätt att göra resurser tillgängliga för externa parter utan att de först behöver logga in på AEM Assets.

>[!NOTE]
>
>Om du vill dela länkar från din AEM Author-instans till externa entiteter måste du se till att du bara visar följande URL:er för `GET` begäranden. Blockera andra URL:er för att säkerställa att din AEM Author-instans är säker.
>* `[aem_server]:[port]/linkshare.html`
>* `[aem_server]:[port]/linksharepreview.html`
>* `[aem_server]:[port]/linkexpired.html`


## Konfigurera CQ-e-posttjänst för dag {#configmailservice}

Konfigurera e-posttjänsten innan du kan dela resurser som länkar.

1. Click or tap the AEM logo, and then navigate to **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]**.
1. Leta upp **[!UICONTROL Dag CQ Mail Service]** i listan över tjänster.
1. Click the **[!UICONTROL Edit]** icon beside the service, and configure the following parameters for **Day CQ Mail Service]** with the details mentioned against their names:

   * Värdnamn för SMTP-server: värdnamn för e-postserver
   * SMTP-serverport: e-postserverport
   * SMTP-användare: e-postserverns användarnamn
   * SMTP-lösenord: e-postserverlösenord

1. Klicka/tryck på **Spara**.

## Konfigurera maximal datastorlek {#maxdatasize}

När du hämtar resurser från den länk som delas med funktionen Länkdelning komprimerar AEM resurshierarkin från databasen och returnerar sedan resursen i en ZIP-fil. I avsaknad av begränsningar för den mängd data som kan komprimeras i en ZIP-fil utsätts stora mängder data för komprimering, vilket leder till minnesfel i JVM. För att skydda systemet från en potentiell denial of service-attack på grund av den här situationen konfigurerar du maxstorleken med parametern **Max Content Size (okomprimerad)** för Day CQ DAM Adhoc Asset Share Proxy Servlet i Configuration Manager. Om resursens okomprimerade storlek överskrider det konfigurerade värdet, avvisas begäranden om hämtning av resurser. Standardvärdet är 100 MB.

1. Klicka/tryck på AEM-logotypen och gå sedan till **Verktyg** > **Åtgärder** > **Webbkonsol**.
1. På webbkonsolen går du till **Day CQ DAM Adhoc Asset Share Proxy Server** .
1. Öppna konfigurationen för **Day CQ DAM Adhoc Asset Share Proxy Server** i redigeringsläge och ändra värdet för parametern **Maximal innehållsstorlek (okomprimerat)**.
1. Spara ändringarna.

<!--
Add content or link about how to configure sharing via BP, DA, AAL, etc.
-->
