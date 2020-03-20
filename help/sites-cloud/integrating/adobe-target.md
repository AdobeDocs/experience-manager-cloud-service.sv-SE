---
title: Integrera med Adobe Target
description: 'Integrera med Adobe Target '
translation-type: tm+mt
source-git-commit: 5a7f2d603952b2c5f92363888efedb482d8efea3

---


# Integrera med Adobe Target{#integrating-with-adobe-target}

Som en del av Adobe Marketing Cloud gör [Adobe Target](http://www.adobe.com/solutions/testing-targeting/testandtarget.html) att ni kan öka innehållets relevans genom målinriktning och mätning i alla kanaler. Adobe Target används av marknadsförare för att utforma och genomföra onlinetester, skapa direktsända målgruppssegment (baserat på beteende) och automatisera målgruppsanpassningen av innehåll och onlineupplevelser. AEM som molntjänst har antagit målarbetsflödet som används i Adobe Target Standard. Om du använder Target kommer du att känna till målredigeringsmiljön i AEM som en molntjänst.

Integrera era AEM-sajter med Adobe Target för att personalisera innehåll på era sidor:

* Implementera målinriktning av innehåll.
* Använd målgrupper för att skapa personaliserade upplevelser.
* Skicka kontextdata till Target när besökarna interagerar med era sidor.
* Spåra konverteringsgrader.

>[!NOTE]
>
>Adobe Experience Manager som molntjänstkunder som inte har något befintligt Target-konto kan begära åtkomst till Target Foundation Pack för Experience Cloud.  Foundation Pack ger begränsad volymanvändning av Target.


Utför följande uppgifter för att integrera med Target:

* [Utför nödvändiga uppgifter](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/target-requirements.html): Registrera dig hos Adobe Target och konfigurera vissa aspekter av AEM-författarinstansen. Ditt Adobe Target-konto måste ha **minst behörigheter på** godkännarnivå. Dessutom måste du skydda aktivitetsinställningarna på publiceringsnoden så att den inte är tillgänglig för användarna.

* Launch från Adobe är de facto-verktyget för att skapa en AEM-webbplats med Target-funktioner (JS-bibliotek). Integrering av AEM som en molntjänst med Launch och Adobe Target går därför hand i hand (se länkarna nedan).

   * [Integrering med Adobe Target med Adobe I/O](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/integration-ims-adobe-io.html)
   * [Integrera Launch från Adobe](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/integrations/adobe-launch-integration-tutorial-understand.html)
   * [Integrera AEM med Adobe Launch via Adobe I/O](https://helpx.adobe.com/experience-manager/using/aem_launch_adobeio_integration.html)
   * [Om AEM-integrering med Launch från Adobe, Analytics och Target](https://helpx.adobe.com/experience-manager/kt/integration/using/aem-launch-integration-tutorial-understand.html)

>[!NOTE]
>
>IMS-konfigurationen (tekniska konton) för Launch från Adobe är förkonfigurerad i AEM som en molntjänst. Användare behöver inte skapa den här konfigurationen.

1. [Konfigurera aktiviteter](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/activitylib.html): Associera dina aktiviteter med målmolnkonfigurationen.

>[!CAUTION]
>
>&quot;I AEM som en molntjänst är den replikeringsagent som synkroniserar erbjudanden och aktiviteter från AEM till Adobe Target inaktiverad som standard. Kontakta [Adobe Support](https://helpx.adobe.com/contact/enterprise-support.ec.html#target) om du behöver aktivera replikeringsagenten igen.&quot;

>[!NOTE]
>
>Om du använder Target med en anpassad proxykonfiguration måste du konfigurera både HTTP-klientproxykonfigurationer eftersom vissa funktioner i AEM använder 3.x-API:erna och några andra 4.x-API:er:
>
>* 3.x är konfigurerat med [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)
>* 4.x är konfigurerat med [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)
>



>[!CAUTION]
>
>Du måste skydda aktivitetsinställningsnoden **cq:ActivitySettings** i publiceringsinstansen så att den inte är tillgänglig för vanliga användare. Noden för aktivitetsinställningar ska endast vara tillgänglig för tjänsten som hanterar aktivitetssynkroniseringen till Adobe Target.
>
>Mer information finns i [Förutsättningar för att integrera med Adobe Target](https://docs.adobe.com/content/help/en/experience-manager-65/administering/integration/target-requirements.html#securing-the-activity-settings-node) .

När integreringen är klar kan du [skapa riktat innehåll](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/content-targeting-touch.html) som skickar besöksdata till Adobe Target. Observera att sidkomponenter kräver specifik kod för att aktivera målinriktning av innehåll. (Se [Utveckla för riktat innehåll](https://docs.adobe.com/content/help/en/experience-manager-65/developing/personlization/target.html).

>[!NOTE]
>
>När du riktar in dig på en komponent i AEM-författaren gör komponenten ett antal serveranrop till Adobe Target för att registrera kampanjen, konfigurera erbjudanden och hämta Adobe Target-segment (om de är konfigurerade). Inga serversamtal görs från AEM-publicering till Adobe Target.

## Källor för bakgrundsinformation {#background-information-sources}

Att integrera AEM som en molntjänst med Adobe Target kräver kunskap om Adobe Target, AEM Activity Management och AEM Audiences Management. Du bör känna till följande information:

* Adobe Target (se dokumentationen [till](https://marketing.adobe.com/resources/help/en_US/target/)Adobe Target).
* AEM Activity console (Se [Hantera aktiviteter](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/activitylib.html)).
* AEM-målgrupper (Se [Hantera målgrupper](https://docs.adobe.com/content/help/en/experience-manager-65/authoring/personalization/managing-audiences.html).

>[!NOTE]
>
>När du arbetar med Adobe Target är det högsta antalet artefakter som tillåts i en kampanj:
>
>* 50 platser
>* 2 000 upplevelser
>* 50-tal
>* 50 rapporteringssegment
>


