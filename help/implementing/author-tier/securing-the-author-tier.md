---
title: Skydda författarnivån
description: Lär dig hur du konfigurerar nätverksprinciper för att skydda åtkomsten till din författarnivå.
exl-id: f5be90a4-266a-4d23-8e8b-94156f0264d5
source-git-commit: a77e5dc4273736b969e9a4a62fcac75664495ee6
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 30%

---

# Skydda författarnivån {#securing-the-author-tier}

När du skapar en miljö med AEM as a Cloud Service är den resulterande författarnivån som standard tillgänglig från Internet. Det går att konfigurera nätverksprinciperna ytterligare för att skydda åtkomsten till din författarnivå. Se [Använda IP Tillåtelselista](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/apply-allow-list.html) för mer information. Processen baseras på auktorisering av IP-intervall som beviljas nätverksåtkomst till författarmiljön.

Om du vill införa de här reglerna skickar du en supportanmälan till [Adobe Admin Console](https://adminconsole.adobe.com/) med den begärda informationen:

* program-ID
* miljö-ID
* IP-adressintervall att auktorisera

