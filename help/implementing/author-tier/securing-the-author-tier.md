---
title: Skydda författarnivån
description: Skydda författarnivån
exl-id: f5be90a4-266a-4d23-8e8b-94156f0264d5
source-git-commit: d436dea08fff8b18573bd7eba308e6b3370e11ef
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Skydda författarnivån {#securing-the-author-tier}

När du skapar en ny miljö med AEM as a Cloud Service är den resulterande författarnivån som standard tillgänglig via internet. Det går att konfigurera nätverksprinciperna ytterligare för att skydda åtkomsten till författarnivån. Mer information finns i [Använda en IP-Tillåtelselista](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/ip-allow-lists/apply-allow-list.html?lang=en).

Processen baseras på auktorisering av IP-intervall som beviljas nätverksåtkomst till författarmiljön.

Om du vill införa dessa regler måste du skicka in en supportanmälan från [Adobe Admin Console](https://adminconsole.adobe.com/) med den begärda informationen:

* program-ID
* miljö-ID
* IP-adressintervall att auktorisera

