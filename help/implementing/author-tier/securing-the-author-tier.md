---
title: Skydda författarnivån
description: Skydda författarnivån
exl-id: f5be90a4-266a-4d23-8e8b-94156f0264d5
source-git-commit: f7525b6b37e486a53791c2331dc6000e5248f8af
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 52%

---

# Skydda författarnivån {#securing-the-author-tier}

När du skapar en ny miljö med AEM as a Cloud Service är den resulterande författarnivån som standard tillgänglig via internet. Det går att konfigurera nätverksprinciperna ytterligare för att skydda åtkomsten till din författarnivå. Se [Använda ett IP-Tillåtelselista](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/apply-allow-list.html?lang=en) för mer information. Processen baseras på auktorisering av IP-intervall som beviljas nätverksåtkomst till författarmiljön.

Om du vill införa de här reglerna skickar du en supportanmälan till [Adobe Admin Console](https://adminconsole.adobe.com/) med den begärda informationen:

* program-ID
* miljö-ID
* IP-adressintervall att auktorisera

