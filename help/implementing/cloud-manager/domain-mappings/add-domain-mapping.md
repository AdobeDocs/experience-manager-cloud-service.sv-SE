---
title: Lägg till en domänmappning
description: Lär dig hur du lägger till en domänmappning för en Edge Delivery-webbplats eller en Cloud Manager-miljö.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Architect, Developer
exl-id: 672513d7-ee0a-4f6e-9ef0-7a41fabbaf9a
source-git-commit: c2229d040c8df7c9089d141d57ca59ff2f4ce8a7
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 0%

---


# Lägga till en domänmappning {#add-domain-mapping}

Om du vill länka en domän med ett SSL-certifikat i det Adobe-hanterade CDN-nätverket i ditt program måste du lägga till en CDN-konfiguration (Content Delivery Network).

För CDN:er som hanteras av Adobe tillåts endast webbplatser med ACME-validering när ett DV SSL-certifikat används.

>[!IMPORTANT]
>
>Har du [lagt till ett anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md) och [lagt till ett SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md)? Annars måste du utföra dessa två åtgärder innan du kan lägga till en CDN-konfiguration.

Se även [Hanterat CDN för Adobe](https://www.aem.live/docs/byo-cdn-adobe-managed).

**Så här lägger du till en domänmappning:**

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. Gör något av följande beroende på hur du använder dem:

   | Använd skiftläge | Steg |
   | --- | --- |
   | Jag vill lägga till en CDN-konfiguration på en *befintlig* Edge Delivery-webbplats i Cloud Manager | a. Klicka på ikonen ![Webbsidor](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) **Edge Delivery Sites** på den vänstra menyn under **Tjänster**.<br>b. Klicka på ikonen ![Mer ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) i Edge Delivery-tabellen i slutet av en rad som inte har någon associerad domän.<br>c. Klicka på **Konfigurera CDN** . |
   | Jag vill lägga till en CDN-konfiguration i Cloud Manager | a. Klicka på ![Ikonen för sociala nätverk](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) **Domänmappningar** på den vänstra menyn under **Tjänster**.<br>b. Klicka på **Lägg till** i det övre högra hörnet på sidan Domänmappningar. |

1. Välj något av följande i listrutan **Ursprung** i dialogrutan **Konfigurera CDN**:

   ![Konfigurera CDN-dialogruta](/help/implementing/cloud-manager/assets/configure-cdn-dialog.png)

   | Ursprung | Beskrivning |
   | --- | --- |
   | Sites | Välj en Edge Delivery-webbplats. |
   | Miljö | Välj en specifik Cloud Service-miljö som du vill ha som mål i din AEM-konfiguration.<br>Välj något av följande i listrutan **Nivå**:<br> ・ Välj **Publicera** om du vill ange en aktiv produktionsmiljö där innehållet levereras till slutanvändarna som mål.<br> ・ Välj **Förhandsgranska** för miljöer där du testar ändringar innan de publiceras. |

1. Välj CDN-typ och associerad konfiguration genom att välja något av följande:

   | CDN-typ | Konfigurationsinformation |
   | --- | --- |
   | Adobe hanterad CDN | Gör följande under **Konfigurationsinformation**:<br>a. Välj det domännamn du vill använda i listrutan **Domän** .<br>Inga verifierade domäner är tillgängliga i listrutan? Se [Lägg till ett eget domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).<br>b. Välj ett certifikat som du vill använda i listrutan **SSL-certifikat** .<br>Inga SSL-certifikat är tillgängliga i listrutan? Se [Lägg till ett SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md). |
   | Annan CDN-leverantör | Välj det här alternativet om du använder en egen CDN-leverantör och inte det CDN som hanteras av Adobe och som är tillgängligt för dig.<br>Under **Konfigurationsinformation** väljer du det domännamn du vill använda i listrutan **Domän**.<br>Inga verifierade domäner är tillgängliga i listrutan? Se [Lägg till ett eget domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md). |

1. Klicka på **Spara**.
