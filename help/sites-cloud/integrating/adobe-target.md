---
title: Integrera med Adobe Target
description: Integrera med Adobe Target
exl-id: 2b4cf35e-2b75-4303-8d09-f6644ad99274
source-git-commit: 65e1ede4cdc8035657e8b37fe206ebed4ab7bb24
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 1%

---

# Integrera med Adobe Target{#integrating-with-adobe-target}

Som en del av Adobe Marketing Cloud kan du med [Adobe Target](http://www.adobe.com/solutions/testing-targeting/testandtarget.html) öka innehållets relevans genom att målinrikta och mäta i alla kanaler. Adobe Target används av marknadsförare för att utforma och genomföra onlinetester, skapa direktsända målgruppssegment (baserat på beteende) och automatisera målgruppsanpassningen av innehåll och onlineupplevelser. AEM som Cloud Service har antagit målarbetsflödet som används i Adobe Target Standard. Om du använder Target kommer du att känna till målredigeringsmiljön i AEM som en Cloud Service.

Integrera era AEM med Adobe Target för att personalisera innehåll på era sidor:

* Implementera målinriktning av innehåll.
* Använd målgrupper för att skapa personaliserade upplevelser.
* Skicka kontextdata till Target när besökarna interagerar med era sidor.
* Spåra konverteringsgrader.

>[!NOTE]
>
>Adobe Experience Manager som Cloud Service-kunder som inte har något befintligt Target-konto kan begära åtkomst till Target Foundation Pack för Experience Cloud.  Foundation Pack ger begränsad volymanvändning av Target.


Utför följande uppgifter för att integrera med Target:

* [Utför nödvändiga uppgifter](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/target-requirements.html): Registrera dig hos Adobe Target och konfigurera vissa aspekter av AEM författarinstans. Ditt Adobe Target-konto måste ha minst **godkännarbehörighet**. Dessutom måste du skydda aktivitetsinställningarna på publiceringsnoden så att den inte är tillgänglig för användarna.

* Launch by Adobe är de facto-verktyget för att instrumentera en AEM webbplats med Target-funktioner (JS-bibliotek). Att integrera AEM som Cloud Service med Launch och Adobe Target går därför hand i hand (se länkarna nedan).

   * [Integrering med Adobe Target med Adobe I/O](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/integration-ims-adobe-io.html)
   * [Integrera Launch by Adobe](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
   * [Integrera AEM med Adobe Launch via Adobe I/O](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html)
   * [Förstå AEM integrering med Launch by Adobe, analys och mål](https://helpx.adobe.com/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)

>[!NOTE]
>
>IMS-konfigurationen (tekniska konton) för Launch by Adobe är förkonfigurerad i AEM som en Cloud Service. Användare behöver inte skapa den här konfigurationen.

1. [Konfigurera aktiviteter](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/activitylib.html): Associera dina aktiviteter med målmolnkonfigurationen.

>[!CAUTION]
>
>I AEM som Cloud Service är den replikeringsagent som synkroniserar erbjudanden och aktiviteter från AEM till Adobe Target inaktiverad som standard. Kontakta [Adobe Support](https://helpx.adobe.com/contact/enterprise-support.ec.html#experience-manager)-teamet om du behöver aktivera replikeringsagenten igen.

>[!NOTE]
>
>Om du använder Target med en anpassad proxykonfiguration måste du konfigurera både HTTP-klientproxykonfigurationer eftersom vissa funktioner i AEM använder 3.x-API:erna och andra 4.x-API:er:
>
>* 3.x har konfigurerats med [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x har konfigurerats med [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)

>



>[!CAUTION]
>
>Du måste skydda aktivitetsinställningsnoden **cq:ActivitySettings** på publiceringsinstansen så att den inte är tillgänglig för vanliga användare. Noden för aktivitetsinställningar ska bara vara tillgänglig för tjänsten som hanterar aktivitetssynkroniseringen till Adobe Target.
>
>Mer information finns i [Förutsättningar för integrering med Adobe Target](https://experienceleague.adobe.com/docs/experience-manager-65/administering/integration/target-requirements.html#securing-the-activity-settings-node).

När integreringen är klar kan du [redigera riktat innehåll](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/content-targeting-touch.html) som skickar besöksdata till Adobe Target. Observera att sidkomponenter kräver specifik kod för att aktivera målinriktning av innehåll. (Se [Utveckla för riktat innehåll](https://experienceleague.adobe.com/docs/experience-manager-65/developing/personlization/target.html).

>[!NOTE]
>
>När du riktar in dig på en komponent i AEM författare gör komponenten ett antal serveranrop till Adobe Target för att registrera kampanjen, konfigurera erbjudanden och hämta Adobe Target-segment (om de är konfigurerade). Inga serversamtal görs från AEM publicera till Adobe Target.

## Källor för bakgrundsinformation {#background-information-sources}

Att integrera AEM som en Cloud Service med Adobe Target kräver kunskaper om Adobe Target, AEM och AEM. Du bör känna till följande information:

* Adobe Target (se [Adobe Target dokumentation](https://experienceleague.adobe.com/docs/target/using/target-home.html)).
* Konsolen AEM aktiviteter (se [Hantera aktiviteter](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/activitylib.html).
* AEM målgrupper (se [Hantera målgrupper](https://experienceleague.adobe.com/docs/experience-manager-65/authoring/personalization/managing-audiences.html).

>[!NOTE]
>
>När du arbetar med Adobe Target är det högsta antalet artefakter som tillåts i en kampanj:
>
>* 50 platser
>* 2 000 upplevelser
>* 50-tal
>* 50 rapporteringssegment

