---
title: Lägg till en CDN-konfiguration
description: Lär dig hur du lägger till en CDN-konfiguration för en Edge Delivery-webbplats eller en Cloud Manager-miljö.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 672513d7-ee0a-4f6e-9ef0-7a41fabbaf9a
source-git-commit: b222b4384b1c2a21ecbb244d149ce7e51cc7990f
workflow-type: tm+mt
source-wordcount: '445'
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

1. Gör något av följande beroende på hur du använder dem:

   | Använd skiftläge | Steg |
   | --- | --- |
   | Jag vill lägga till en CDN-konfiguration på en *befintlig* Edge Delivery-webbplats i Cloud Manager | a. Klicka på **Edge Delivery Sites** under **Tjänster** i den vänstra navigeringspanelen.<br>b. I Edge Delivery-tabellen klickar du på ellipsen i slutet av en rad som inte har någon associerad domän.<br>c. Klicka på **Konfigurera CDN** .  ![Klicka på Konfigurera CDN för en Edge Delivery-webbplats](/help/implementing/cloud-manager/assets/cm-eds-config-cdn.png) |
   | Jag vill lägga till en CDN-konfiguration i Cloud Manager | a. Klicka på **CDN-konfigurationer** under **Tjänster** i den vänstra navigeringspanelen.<br>b. Klicka på **Lägg till** i det övre högra hörnet på sidan CDN-konfigurationer. |

1. Välj något av följande i listrutan **Ursprung** i dialogrutan **Konfigurera CDN**:

   ![Konfigurera CDN-dialogruta](/help/implementing/cloud-manager/assets/configure-cdn-dialog.png)

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
