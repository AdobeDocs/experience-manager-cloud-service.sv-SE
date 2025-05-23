---
title: Post GoLive
description: Lär dig hur du övervakar problem och förbättrar prestanda.
exl-id: 487f0b51-501b-48fc-a796-3cb8a6d64462
feature: Migration
role: Admin
source-git-commit: bb2688701b80a560ea9078c2b7b6594ff55ce824
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 4%

---

# Post GoLive {#post-go-live}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_troubleshooting"
>title="Felsökning av AEM"
>abstract="Granska metodtips för kontinuerlig utveckling och hantering av loggar. Läs om verktyg som Developer Console och CRXDE Lite som hjälper dig att felsöka problem med AEM."
>additional-url="https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/manage-logs" text="Åtkomst till och hantering av loggar"
>additional-url="https://experienceleague.adobe.com/sv/docs/experience-manager-cloud-service/content/implementing/developing/development-guidelines#aem-as-a-cloud-service-development-tools" text="AEM as a Cloud Service utvecklingsverktyg"

Den här resan är den sista delen, så du får lära dig att övervaka problem och förbättra resultatet när migreringen är klar. Se till att tillfälliga filer rensas, granska vedertagna metoder för kontinuerlig utveckling och hantera loggar.

## Story hittills {#story-so-far}

I det föregående steget av resan lärde du dig att utföra migreringen och [gå live](/help/journey-migration/go-live.md) när koden och innehållet var klara att flyttas över till AEM as a Cloud Service.

## Syfte {#objective}

I det här dokumentet beskrivs de verktyg som är tillgängliga för att felsöka AEM as a Cloud Service-miljöer:

* **Developer Console**
* **CRXDE Lite**
* **Hantera loggar**

## Developer Console {#developer-console}

Det går att felsöka AEM as a Cloud Service utvecklingsmiljöer i Developer Console för utvecklings-, scen- och produktionsmiljöer.

Mer information om utvecklingsverktyg finns i [Implementera för AEM as a Cloud Service](/help/implementing/developing/introduction/development-guidelines.md#aem-as-a-cloud-service-development-tools).

## CRXDE Lite {#crxde-lite}

Som användare har du åtkomst till CRXDE Lite i utvecklingsmiljön, men inte till scenen eller produktionen.

>[!IMPORTANT]
>Skrivning till oföränderliga databaser, som `/libs` och `/apps` vid körning, resulterar i fel. Du har inte heller tillgång till utvecklarverktyg för staging- och produktionsmiljöer.

Mer information om hur du utvecklar AEM-program med CRXDE Lite finns i [Utveckla med CRXDE Lite](/help/implementing/developing/tools/crxde.md).

## Hantera loggar {#managing-logs}

Användarna kan öppna en lista över tillgängliga loggfiler för den valda miljön.

Mer information om hur du får åtkomst till och hanterar loggar finns i [Åtkomst till och hantering av loggar](/help/implementing/cloud-manager/manage-logs.md) via användargränssnittet eller från API:t via Cloud Manager.

## Kontakta support {#contacting-support}

>[!CONTEXTUALHELP]
>id="aemcloud_golive_support"
>title="Hjälp och support"
>abstract="Kontakta Adobe AEM Support-team för att få klargöranden eller för att ta itu med eventuella problem."
>additional-url="https://helpx.adobe.com/se/enterprise/using/support-for-experience-cloud.html" text="Stöd för Experience Cloud"

Om du har frågor om Cloud Service kontaktar du Adobe eller [Support för Experience Cloud](https://helpx.adobe.com/se/enterprise/using/support-for-experience-cloud.html) om du vill ha mer information.

## Dokumentinlärning {#document-learnings}

När migreringen är klar dokumenterar du de kunskaper som förvärvats under den här processen. Några frågor som kan underlätta dokumentationsprocessen är:

* Vad fungerade bra och vad gjorde det inte?
* Vilka var de största smärtorna?
* Rekommendationer om det finns en framtida migrering.

Dela med dig av detta material till intressenter och team inom organisationen.

## Resan slutar - eller gör det? {#journey-ends}

Grattis! Du har slutfört AEM as a Cloud Service migreringsresa! Du bör förstå hur man gör:

* Kom igång med att byta till AEM as a Cloud Service
* Kontrollera om distributionen är klar att flyttas till AEM as a Cloud Service
* Gör koden och innehållet i molnet färdiga
* Utför migreringen
* Övervaka problem och förbättra prestanda
