---
title: Post GoLive
description: Lär dig hur du övervakar problem och förbättrar prestanda
exl-id: 487f0b51-501b-48fc-a796-3cb8a6d64462
source-git-commit: a3e79441d46fa961fcd05ea54e84957754890d69
workflow-type: tm+mt
source-wordcount: '482'
ht-degree: 9%

---

# Post GoLive {#post-go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_troubleshooting"
>title="AEM"
>abstract="Granska metodtips för kontinuerlig utveckling och hantera loggar tillsammans med verktyg som Developer Console och CRXDE Lite för att få hjälp med felsökning av AEM"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-logs.html" text="Komma åt och hantera loggar"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools" text="AEM as a Cloud Service utvecklingsverktyg"

Den här resan är den sista delen, så du lär dig att övervaka problem och förbättra resultatet när migreringen är klar. Du bör se till att tillfälliga filer rensas, granska bästa praxis för kontinuerlig utveckling och hantera loggar.

## Story hittills {#story-so-far}

I det föregående steget av resan lärde du dig att utföra migreringen och [GoLive](/help/journey-migration/go-live.md) när koden och innehållet är klara att flyttas över till AEM as a Cloud Service.

## Syfte {#objective}

I det här dokumentet beskrivs de verktyg som är tillgängliga för att felsöka AEM as a Cloud Service miljöer:

* **Developer Console**
* **CRXDE Lite**
* **Hantera loggar**

## Developer Console {#developer-console}

Felsökning AEM as a Cloud Service utvecklingsmiljöer finns på Developer Console för utvecklings-, scen- och produktionsmiljöer.

Se [Implementera för AEM as a Cloud Service](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools) om du vill veta mer om utvecklingsverktyg.

## CRXDE Lite {#crxde-lite}

Som användare har du åtkomst till CRXDE Lite i utvecklingsmiljön, men inte i mellanlagring eller produktion.

>[!IMPORTANT]
>Skriva till oföränderliga databaser som `/libs` och `/apps` vid körning resulterar i fel. Du har inte heller tillgång till utvecklarverktyg för staging- och produktionsmiljöer.

Se [Utveckla med CRXDE Lite](/help/implementing/developing/tools/crxde.md) om du vill ha mer information om hur du utvecklar AEM med CRXDE Lite.

## Hantera loggar {#managing-logs}

Användarna kan öppna en lista över tillgängliga loggfiler för den valda miljön.

Se [Åtkomst till och hantering av loggar](/help/implementing/cloud-manager/manage-logs.md) om du vill lära dig hur du får åtkomst till och hanterar loggar via användargränssnittet eller från API:n med hjälp av Cloud Manager.

## Kontakta support {#contacting-support}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_support"
>title="Hjälp och support"
>abstract="Kontakta Adobe AEM supportteam för att få klargöranden eller ta itu med eventuella problem."
>additional-url="https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html" text="Stöd för Experience Cloud"

Om du har frågor om åtkomst till Cloud Service kan du kontakta din Adobe-representant eller [Stöd för Experience Cloud](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html) för mer information.

## Dokumentinlärning {#document-learnings}

När migreringen är klar dokumenterar du de kunskaper som förvärvats under den här processen. Några frågor som kan underlätta dokumentationsprocessen är:

* Vad fungerade bra och vad gjorde det inte?
* Vilka var de största smärtorna?
* Recommendations om det finns en framtida migrering.

Dela med dig av detta material till intressenter och team inom organisationen.

## Resan slutar - eller gör det? {#journey-ends}

Grattis! Du har slutfört den AEM as a Cloud Service migreringsresan! Du bör förstå hur man gör:

* Kom igång med att gå över till AEM as a Cloud Service
* Kontrollera om distributionen är klar att flyttas till AEM as a Cloud Service
* Gör koden och innehållet i molnet färdiga
* Utför migreringen
* Övervaka problem och förbättra prestanda
