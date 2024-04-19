---
title: Konfigurera anpassad domän för publiceringsnivå
description: Lär dig hur du konfigurerar anpassad domän för publiceringsnivå i Adobe Cloud Manager.
role: null
source-git-commit: 0ad9f349c997c35862e4f571b4741ed4c0c947e2
workflow-type: tm+mt
source-wordcount: '255'
ht-degree: 0%

---


# Konfigurera anpassad domän för publiceringsnivå{#configure-custom-domain}

I Adobe Cloud Manager kan du få din webbplats att sticka ut genom att lägga till en anpassad domän. När AEM as a Cloud Service har en standarddomän kan du anpassa den efter dina behov.
<!-- For example, AEM sites can use `sites.custom_domain.com`, and the AEM publish domain can be accessed via `assets.custom_domain.com`. Additionally, getting an SSL certificate for assets.pmi.com with a SAN entry for `delivery.custom_domain.com` improves security and trustworthiness. -->

## Innan du börjar

* Du måste ha ett TLS- eller SSL-certifikat för flera SAN-nätverk (Subject Alternative Name).
* SSL-certifikatet ska ha distinkta SAN-nätverk jämfört med certifikatet som är mappat för publiceringsnivån inom samma domän.
* Certifikatprofilen måste följa antingen Utökad validering (EV) eller Organisationsvalidering (OV) och inte Domänvalidering (DV).


## Lägg till anpassad domän

Så här konfigurerar du en anpassad domän för publiceringsnivån:

1. Gå till **[!UICONTROL Adobe Cloud Manager]** > **[!UICONTROL Program Overview]** > **[!UICONTROL SSL Certificates]**och lägg till ditt SSL-certifikat.
   ![image](/help/assets/assets/ssl-certificate.png)
Lär dig hur du lägger till [SSL-certifikat](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-ssl-certificates/add-ssl-certificate.html?lang=en) i Adobe Cloud Manager.

1. När du har lagt till SSL-certifikatet lägger du till en anpassad domän. Klicka **[!UICONTROL Domain Settings]** och ange den anpassade domänen mot **[!UICONTROL Publish service]** alternativ.
   <br> Läs mer om [anpassad domän](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name.html?lang=en).

1. Lägg till två CNAME-poster i din DNS-post som motsvarar publiceringsdomäner.
   <br> DNS-verifiering kan ta några timmar att behandla på grund av fördröjd DNS-spridning.

1. Logga ett supportärende för att underlätta konfigurationen av den anpassade domänen och se till att den dirigeras till leveransnivån.

>[!NOTE]
>
> Se till att lägga till den anpassade domänen i listan över tillåtna omdirigerings-URL:er i IMS-klienten för resursväljaren.<br>Koordinera med respektive Adobe-team för att utföra den här åtgärden genom att ange den anpassade domänsträngen.
