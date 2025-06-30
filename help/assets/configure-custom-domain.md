---
title: Konfigurera en anpassad domän för publiceringsnivån
description: Lär dig hur du konfigurerar en anpassad domän för publiceringsskikt i Adobe Cloud Manager.
exl-id: cc71c8c5-cf42-4092-b0e0-646a2ed0ee54
source-git-commit: 32fdbf9b4151c949b307d8bd587ade163682b2e5
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# Konfigurera en anpassad domän för publiceringsskiktet{#configure-custom-domain}

I Adobe Cloud Manager kan du få din webbplats att sticka ut genom att lägga till en anpassad domän. När AEM as a Cloud Service har en standarddomän kan du anpassa den efter dina behov.

## Innan du börjar

* Du måste ha ett TLS- eller SSL-certifikat för flera SAN-nätverk (Subject Alternative Name).
* SSL-certifikatet ska ha distinkta SAN-nätverk jämfört med certifikatet som är mappat för publiceringsnivån inom samma domän.
* Certifikatprofilen måste följa antingen Utökad validering (EV) eller Organisationsvalidering (OV) och inte Domänvalidering (DV).


## Konfigurera en anpassad domän för publiceringsskiktet

1. Gå till **[!UICONTROL Adobe Cloud Manager]** > **[!UICONTROL Program Overview]** > **[!UICONTROL SSL Certificates]** och lägg till ditt SSL-certifikat.
   ![bild](/help/assets/assets/ssl-certificate.png)
Lär dig hur du lägger till [ SSL-certifikat ](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md) i Adobe Cloud Manager.

1. När du har lagt till SSL-certifikatet lägger du till en anpassad domän. Klicka på **[!UICONTROL Domain Settings]** och ange den anpassade domänen mot alternativet **[!UICONTROL Publish service]**.
Läs mer om [anpassad domän](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

1. Lägg till två [CNAME-poster](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) i din DNS-post som motsvarar publiceringsdomäner.
DNS-verifiering kan ta några timmar att behandla på grund av fördröjd DNS-spridning.

1. Logga ett supportärende för att underlätta konfigurationen av den anpassade domänen och se till att den dirigeras till leveransnivån.

>[!NOTE]
>
>Lägg till den anpassade domänen i listan över tillåtna omdirigerings-URL:er. Listan finns i IMS-klienten för resursväljaren.<br>Koordinera med respektive Adobe-team för att utföra den här åtgärden genom att ange den anpassade domänsträngen.
