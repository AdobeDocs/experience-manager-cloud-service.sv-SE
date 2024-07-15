---
title: Integrera med Adobe Target
description: Integrera med Adobe Target
exl-id: 2b4cf35e-2b75-4303-8d09-f6644ad99274
source-git-commit: 876de632163c4a0952e238ac89577fa9f064b900
workflow-type: tm+mt
source-wordcount: '606'
ht-degree: 0%

---

# Integrera med Adobe Target{#integrating-with-adobe-target}

Som en del av Adobe Experience Cloud kan du med [Adobe Target](https://business.adobe.com/products/target/adobe-target.html) öka innehållets relevans genom att målinrikta och mäta i alla kanaler. Adobe Target används av marknadsförare för att utforma och genomföra onlinetester, skapa direktsända målgruppssegment (baserat på beteende) och automatisera målgruppsanpassningen av innehåll och onlineupplevelser. AEM as a Cloud Service har antagit målarbetsflödet som används i Adobe Target Standard. Om du använder Target är du bekant med målredigeringsmiljön i AEM as a Cloud Service.

Integrera era AEM med Adobe Target så att ni kan personalisera innehåll på era sidor:

* Implementera målinriktning av innehåll.
* Använd målgrupper för att skapa personaliserade upplevelser.
* Skicka kontextdata till Target när besökarna interagerar med era sidor.
* Spåra konverteringsgrader.

>[!NOTE]
>
>Kunder som inte har något befintligt Target-konto kan begära åtkomst till Target Foundation Pack för Experience Cloud. Foundation Pack ger begränsad volymanvändning av Target.


Utför följande uppgifter för att integrera med Target:

* [Utför nödvändiga uppgifter](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/target-requirements.html): Registrera dig hos Adobe Target och konfigurera vissa aspekter av AEM författarinstans. Ditt Adobe Target-konto måste ha minst behörighet på **godkännarnivå**. Dessutom måste du skydda aktivitetsinställningarna på publiceringsnoden så att den inte är tillgänglig för användarna.

* Launch by Adobe är de facto-verktyget för att instrumentera en AEM webbplats med Target-funktioner (JS-bibliotek). Att integrera AEM as a Cloud Service med Launch och Adobe Target går därför hand i hand (se länkarna nedan).

<!--   
  * [Integration with Adobe Target using Adobe I/O](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/integration-target-ims.html)
-->

* [Integrera Launch by Adobe](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-data-collection-tags/overview.html)
* [Integrera AEM med Adobe Launch via Adobe I/O](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-data-collection-tags/overview.html)
* [AEM integrering med Launch by Adobe, analys och mål](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/experience-platform-data-collection-tags/overview.html)

>[!NOTE]
>
>IMS-konfigurationen (tekniska konton) för Launch by Adobe är förkonfigurerad i AEM as a Cloud Service. Användare behöver inte skapa den här konfigurationen.

1. [Konfigurera aktiviteter](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/activitylib.html): Associera dina aktiviteter med målmolnkonfigurationen.

>[!CAUTION]
>
>I AEM as a Cloud Service är den replikeringsagent som synkroniserar erbjudanden och aktiviteter från AEM till Adobe Target inaktiverad som standard. Kontakta supportteamet på [Adobe](https://experienceleague.adobe.com/?support-solution=General#support) om du måste aktivera replikeringsagenten igen.

>[!NOTE]
>
>Om du använder Target med en anpassad proxykonfiguration måste du konfigurera både HTTP-klientproxykonfigurationer eftersom vissa funktioner i AEM använder 3.x-API:erna och andra 4.x-API:er:
>
>* 3.x har konfigurerats med [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x har konfigurerats med [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>

>[!CAUTION]
>
>Skydda aktivitetsinställningsnoden **cq:ActivitySettings** på publiceringsinstansen så att den inte är tillgänglig för vanliga användare. Noden för aktivitetsinställningar ska bara vara tillgänglig för tjänsten som hanterar aktivitetssynkroniseringen till Adobe Target.
>
>Mer information finns i [Förutsättningar för integrering med Adobe Target](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/target-requirements.html#securing-the-activity-settings-node).

När integreringen är klar kan du [skapa riktat innehåll](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/content-targeting-touch.html) som skickar besöksdata till Adobe Target. Sidkomponenter kräver specifik kod för att aktivera målinriktning av innehåll. (Se [Utveckla för riktat innehåll](https://experienceleague.adobe.com/docs/experience-manager-65/developing/personlization/target.html).

>[!NOTE]
>
>När du riktar in dig på en komponent i AEM författare gör komponenten ett antal serveranrop till Adobe Target för att registrera kampanjen, konfigurera erbjudanden och hämta Adobe Target-segment (om de är konfigurerade). Inga anrop på serversidan görs från AEM publicera till Adobe Target.

## Källor för bakgrundsinformation {#background-information-sources}

För att integrera AEM as a Cloud Service med Adobe Target krävs kunskap om Adobe Target, AEM och AEM. Du bör känna till följande information:

* Adobe Target (se [Adobe Target-dokumentationen](https://experienceleague.adobe.com/docs/target/using/target-home.html)).
* Konsolen AEM aktiviteter (se [Hantera aktiviteter](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/activitylib.html)).
* AEM målgrupper (se [Hantera målgrupper](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/managing-audiences.html)).

>[!NOTE]
>
>När du arbetar med Adobe Target är det högsta antalet artefakter som tillåts i en kampanj:
>
>* 50 platser
>* 2 000 upplevelser
>* 50-tal
>* 50 rapporteringssegment
