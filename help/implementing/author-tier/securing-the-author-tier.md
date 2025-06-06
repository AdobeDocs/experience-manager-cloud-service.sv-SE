---
title: Skydda författarnivån
description: Lär dig hur du konfigurerar nätverksprinciper för att skydda åtkomsten till din författarnivå.
exl-id: f5be90a4-266a-4d23-8e8b-94156f0264d5
feature: Configuring
role: Admin
source-git-commit: f66ea281e6abc373e9704e14c97b77d82c55323b
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 30%

---

# Skydda författarnivån {#securing-the-author-tier}

När du skapar en miljö med AEM as a Cloud Service är den resulterande redigeringsnivån som standard tillgänglig från Internet. Det går att konfigurera nätverksprinciperna ytterligare för att skydda åtkomsten till din författarnivå. Mer information finns i [Använda ett IP-Tillåtelselista](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/ip-allow-lists/apply-allow-list.html?lang=sv-SE). Processen baseras på auktorisering av IP-intervall som beviljas nätverksåtkomst till författarmiljön.

Om du vill tillämpa de här reglerna skickar du en supportanmälan från [Adobe Admin Console](https://adminconsole.adobe.com/) med den begärda informationen:

* program-ID
* miljö-ID
* IP-adressintervall att auktorisera

