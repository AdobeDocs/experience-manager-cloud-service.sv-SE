---
title: Lägg till en CDN-konfiguration
description: Lär dig hur du lägger till en CDN-konfiguration för en Edge Delivery-webbplats eller en Cloud Manager-miljö.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 672513d7-ee0a-4f6e-9ef0-7a41fabbaf9a
source-git-commit: bc9aa376a402a55191e153f662262ff65df32f5e
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---


# Lägga till en CDN-konfiguration {#add-cdn}

Om du vill länka en domän med ett SSL-certifikat på det Adobe-hanterade CDN-nätverket i ditt program måste du lägga till en CDN-konfiguration (Content Delivery Network).

För CDN som hanteras av Adobe tillåts endast webbplatser med ACME-validering när DV-certifikat används.

>[!IMPORTANT]
>
>Har du [lagt till ett anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) och [lagt till ett SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)? Annars måste du utföra dessa två åtgärder innan du kan lägga till en CDN-konfiguration.

**Så här lägger du till en CDN-konfiguration:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. Klicka på **CDN-konfigurationer** under **Tjänster** i den vänstra navigeringspanelen.

1. Klicka på **Lägg till** i det övre högra hörnet på sidan CDN-konfigurationer.

   ![Konfigurera CDN-dialogruta](/help/implementing/cloud-manager/assets/configure-cdn-dialog.png)

1. Välj något av följande i listrutan **Ursprung** i dialogrutan **Konfigurera CDN**:

   | Ursprung | Beskrivning |
   | --- | --- |
   | Sites | Välj en Edge Delivery-webbplats. |
   | Miljö | Markera en specifik målgruppsmiljö i AEM.<br>I listrutan **Nivå** väljer du något av följande:<br> ・ Välj **Publish** om du vill ha en aktiv produktionsmiljö där innehållet levereras till slutanvändarna.<br> ・ Välj **Förhandsgranska** för miljöer där du testar ändringar innan de publiceras. |

1. Välj CDN-typ och associerad konfiguration genom att välja något av följande:

   | CDN-typ | Konfigurationsinformation |
   | --- | --- |
   | CDN hanterad i Adobe | Gör följande under **Konfigurationsinformation**:<br>a. Välj det domännamn du vill använda i listrutan **Domän** .<br>Inga verifierade domäner är tillgängliga i listrutan? Se [Lägg till ett eget domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).<br>b. Välj ett certifikat som du vill använda i listrutan **SSL-certifikat** .<br>Inga SSL-certifikat är tillgängliga i listrutan? Se [Lägg till ett SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md). |
   | Annan CDN-leverantör | Välj det här alternativet om du använder en egen CDN-leverantör och inte det CDN-nätverk som hanteras av Adobe som är tillgängligt för dig.<br>Under **Konfigurationsinformation** väljer du det domännamn du vill använda i listrutan **Domän**.<br>Inga verifierade domäner är tillgängliga i listrutan? Se [Lägg till ett eget domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). |

1. Klicka på **Spara**.
