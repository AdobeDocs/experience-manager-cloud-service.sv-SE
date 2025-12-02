---
title: Lägg till en domänmappning
description: Lär dig hur du lägger till en domänmappning för en Edge Delivery-webbplats eller en Cloud Manager-miljö.
solution: Experience Manager
feature: Cloud Manager, Developing
role: Admin, Developer
exl-id: 672513d7-ee0a-4f6e-9ef0-7a41fabbaf9a
source-git-commit: 4935fbf5f0eb10f2f17280fb32f07d99f69eb875
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 0%

---


# Om att lägga till en domänmappning {#add-domain-mapping}

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
   | Jag vill lägga till en CDN-konfiguration på en *befintlig* Edge Delivery-webbplats i Cloud Manager | a. Klicka på ikonen **Webbsidor** ![Edge Delivery Sites](https://spectrum.adobe.com/static/icons/workflow_18/Smock_WebPages_18_N.svg) på den vänstra menyn under **Tjänster**.<br>b. Klicka på ikonen ![Mer ](https://spectrum.adobe.com/static/icons/workflow_18/Smock_More_18_N.svg) i Edge Delivery-tabellen i slutet av en rad som inte har någon associerad domän.<br>c. Klicka på **Konfigurera CDN** . |
   | Jag vill lägga till en CDN-konfiguration i Cloud Manager | a. Klicka på **Ikonen för sociala nätverk** ![Domänmappningar](https://spectrum.adobe.com/static/icons/workflow_18/Smock_SocialNetwork_18_N.svg) på den vänstra menyn under **Tjänster**.<br>b. Klicka på **Lägg till** i det övre högra hörnet på sidan Domänmappningar. |

1. Välj någon av följande CDN-typer i dialogrutan **Koppla domän till CDN**:

   * **Hanterat CDN i Adobe (rekommenderas)** - Ett CDN som hanteras av Adobe används för den här konfigurationen. Den innehåller automatiserad installation och hantering samt inbyggda säkerhetsfunktioner.
   * **Annan CDN-provider** - Ett självhanterat CDN-providernätverk används för den här konfigurationen.

1. Baserat på den valda CDN-typen i föregående steg gör du följande:

   * **Hanterad CDN för Adobe**

     ![Dialogrutan Koppla domän till CDN med alternativknappen för hanterad CDN från Adobe markerad](/help/implementing/cloud-manager/assets/cdn/map-domain-to-cdn-adobe-managed.png)

      1. Välj något av följande i listrutan **Ursprung**:

         | Listrutan Ursprung | Beskrivning |
         | --- | --- |
         | Sites | Välj en Edge Delivery-webbplats. |
         | Miljö | Välj en specifik Cloud Service-miljö som du vill ha som mål i din AEM-konfiguration.<br>Välj något av följande i listrutan **Nivå**:<br> ・ Välj **Publicera** om du vill ange en aktiv produktionsmiljö där innehållet levereras till slutanvändarna som mål.<br> ・ Välj **Förhandsgranska** för miljöer där du testar ändringar innan de publiceras. |

      1. Välj det domännamn du vill använda i listrutan **Domän**.<br>Inga verifierade domäner är tillgängliga i listrutan? Se [Lägg till ett eget domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

      1. Välj ett certifikat som du vill använda i listrutan **SSL-certifikat**.<br>Inga SSL-certifikat är tillgängliga i listrutan? Se [Lägg till ett SSL-certifikat](/help/implementing/cloud-manager/managing-ssl-certifications/add-ssl-certificate.md).

      1. Klicka på **Spara**.

   * **Annan CDN-provider**

     ![Dialogrutan Koppla domän till CDN med alternativknappen för hanterad CDN från Adobe markerad](/help/implementing/cloud-manager/assets/cdn/map-domain-to-cdn-other-provider.png)

     Använd de angivna konfigurationsstegen för att tillämpa de nödvändiga inställningarna i CDN och bekräfta mappningen. Se även [Lägg till ett anpassat domännamn](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md).

      1. Klicka på **Jag har konfigurerat mitt CDN**.

   <!-- OLD IMAGE/UI (/help/implementing/cloud-manager/assets/configure-cdn-dialog.png)-->

   <!-- In the **Domain** field, enter the customer-facing hostname you want to serve (for example, `www.example.com`) -->

1. Adobe rekommenderar att du testar domänmappningen.

## Testa domänmappningen {#test-domain-mapping}

Du kan verifiera att en ny domänmappning är aktiv på det Adobe-hanterade CDN-nätverket utan att vänta på publik DNS-spridning.

Kör ett **curl**-kommando som åsidosätter DNS-upplösning och pekar direkt mot CDN-kanten:

```bash
curl -svo /dev/null https://www.example.com \
--resolve www.example.com:443:151.101.3.10
```

* Ersätt `www.example.com` med din domän.
* IP-adressen `151.101.3.10` är en av IP-adresserna som kan användas för att komma åt AEM Cloud-tjänsten. Se även [APEX-post](/help/implementing/cloud-manager/custom-domain-names/add-custom-domain-name.md#adobe-managed-cert-apex-record).

Flaggan `--resolve` tvingar begäran till den angivna IP-adressen och returnerar bara lyckade när certifikatet och routningen för din domän har installerats korrekt.

