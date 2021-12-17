---
title: Post GoLive
description: Lär dig hur du övervakar problem och förbättrar prestanda
source-git-commit: c9143d77e70476beb7f7dd162c36aeda8d1be506
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 20%

---


# Post GoLive {#post-go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_troubleshooting"
>title="AEM"
>abstract="Granska metodtips för kontinuerlig utveckling och hantera loggar tillsammans med verktyg som Developer Console och CRXDE Lite för att få hjälp med felsökning av AEM"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/manage-logs.html" text="Komma åt och hantera loggar"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/developing/development-guidelines.html#aem-as-a-cloud-service-development-tools" text="AEM as a Cloud Service utvecklingsverktyg"

Detta är den sista delen av resan, så du får lära dig att övervaka problem och förbättra resultatet när migreringen är klar. Du bör se till att tillfälliga filer rensas, granska bästa praxis för kontinuerlig utveckling och hantera loggar.

## Story hittills {#story-so-far}

I det föregående steget av resan lärde du dig att utföra migreringen och [GoLive](/help/journey-migration/go-live.md) när koden och innehållet är klara att flyttas över till AEM as a Cloud Service.

## Syfte {#objective}

I det här dokumentet beskrivs de verktyg som är tillgängliga för att felsöka AEM as a Cloud Service miljöer:

* **Developer Console**
* **CRXDE Lite**
* **Hantera loggar**

## Developer Console {#developer-console}

Felsökning AEM as a Cloud Service utvecklingsmiljöer finns på Developer Console för utvecklings-, scen- och produktionsmiljöer.

Mer information om utvecklingsverktyg finns i [Implementera för AEM as a Cloud Service](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools).

## CRXDE Lite {#crxde-lite}

Som användare har du åtkomst till CRXDE Lite i utvecklingsmiljön, men inte i mellanlagring eller produktion.

>[!IMPORTANT]
>Skriva till oföränderliga databaser som `/libs` och `/apps` vid körning resulterar i fel. Dessutom har du inte tillgång till utvecklarverktyg för staging- och produktionsmiljöer.

Läs mer i [Utveckla med CRXDE Lite](/help/implementing/developing/tools/crxde.md) om du vill veta hur du utvecklar ditt AEM-program med CRXDE Lite.

## Hantera loggar {#managing-logs}

Användarna kan öppna en lista över tillgängliga loggfiler för den valda miljön.

Läs [Komma åt och hantera loggar](/help/implementing/cloud-manager/manage-logs.md) för att lära dig hur du får åtkomst till och hanterar loggar via användargränssnittet eller från API via Cloud Manager.

## Kontakta support {#contacting-support}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_support"
>title="Hjälp och support"
>abstract="Kontakta vårt AEM supportteam för att få klargöranden eller för att ta itu med eventuella frågor."
>additional-url="https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html" text="Stöd för Experience Cloud"

Om du har frågor om åtkomst till Cloud Service kan du kontakta din Adobe-representant eller [Stöd för Experience Cloud](https://helpx.adobe.com/enterprise/using/support-for-experience-cloud.html) för mer information.

## Dokumentinlärning {#document-learnings}

När migreringen är klar bör du dokumentera de kunskaper som förvärvats under den här processen. Några frågor som kan underlätta dokumentationsprocessen är:

* Vad fungerade bra och vad gjorde det inte?
* Vilka var de största smärtorna?
* Recommendations vid en framtida migrering.

Sedan bör ni dela dessa inlärningar med intressenter och team inom organisationen.

## Resan slutar - eller gör det? {#journey-ends}

Grattis! Du har slutfört den AEM as a Cloud Service migreringsresan! Du bör förstå hur du:

* Kom igång med att gå över till AEM as a Cloud Service
* Kontrollera om distributionen är klar att flyttas till AEM as a Cloud Service
* Gör koden och innehållet i molnet färdiga
* Utför migreringen
* Övervaka problem och förbättra prestanda
