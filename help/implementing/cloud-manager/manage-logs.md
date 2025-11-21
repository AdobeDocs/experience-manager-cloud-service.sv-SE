---
title: Åtkomst och hantering av loggar
description: Lär dig hur du får åtkomst till och hanterar loggar som hjälp i utvecklingsprocessen i AEM as a Cloud Service.
exl-id: f17274ce-acf5-4e7d-b875-75d4938806cd
solution: Experience Manager
feature: Log Files, Developing
role: Admin, Developer
source-git-commit: 2c863e0cfad3211e811665a5169def7705e8b907
workflow-type: tm+mt
source-wordcount: '344'
ht-degree: 0%

---


# Få åtkomst till och hantera loggar {#manage-logs}

Lär dig hur du får åtkomst till och hanterar loggar som hjälp i utvecklingsprocessen i AEM as a Cloud Service.

Du kan komma åt en lista över tillgängliga loggfiler för den valda miljön med hjälp av kortet **Environment** på sidan **Översikt** eller sidan Miljöinformation.

Loggar sparas i sju dagar.

## Hämtningsloggar {#download-logs}

1. Logga in på Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välj lämplig organisation.

1. Välj programmet på konsolen **[Mina program](/help/implementing/cloud-manager/navigation.md#my-programs)**.

1. Gå till **miljökortet** från sidan **Översikt**.

1. Välj **Hämta loggar** på ellipsmenyn.

   ![Menyobjektet Hämta loggar](assets/download-logs1.png)

1. I dialogrutan **Hämta loggar** väljer du lämplig **tjänst** i listrutan

   ![Dialogrutan Hämta loggar](assets/download-preview.png)

   Om [Ytterligare publiceringsregioner](/help/operations/additional-publish-regions.md) är aktiverade för din miljö kan du markera varje region och hämta dess loggar separat, vilket visas nedan:

   ![Hämta loggar för ytterligare publiceringsregioner](assets/download-publish-region-logs.png)

1. När du har valt tjänsten klickar du på nedladdningsikonen bredvid den logg du vill hämta.

Du kan även komma åt dina loggar från sidan **Miljö**.

![Loggar från miljöskärmen](assets/download-logs.png)

## Loggar genom API:t {#logs-through-api}

Förutom att hämta loggar via användargränssnittet är loggar tillgängliga via API:t och kommandoradsgränssnittet.

Om du vill hämta loggfilerna för en viss miljö ser kommandot ut ungefär så här.

```shell
$ aio cloudmanager:download-logs --programId 5 1884 author aemerror
```

Du kan också avsluta loggar via kommandoradsgränssnittet.

```shell
$ aio cloudmanager:tail-log --programId 5 1884 author aemerror
```

Om du vill hämta miljö-ID (1884 i det här exemplet) och tillgängliga service- eller loggnamnsalternativ kan du använda följande kommandon.

```shell
$ aio cloudmanager:list-environments
Environment Id Name                     Type  Description                          
1884           FoundationInternal_dev   dev   Foundation Internal Dev environment  
1884           FoundationInternal_stage stage Foundation Internal STAGE environment
1884           FoundationInternal_prod  prod  Foundation Internal Prod environment
 
 
$ aio cloudmanager:list-available-log-options 1884
Environment Id Service    Name         
1884           author     aemerror     
1884           author     aemrequest   
1884           author     aemaccess    
1884           publish    aemerror     
1884           publish    aemrequest   
1884           publish    aemaccess    
1884           dispatcher httpderror   
1884           dispatcher aemdispatcher
1884           dispatcher httpdaccess
```

### Ytterligare resurser {#resources}

>[!TIP]
>
>Kolla in [den här videokursen](https://app.frame.io/reviews/28cdf463-b7fc-443b-a54a-93cb7da6567e/dbf158f1-568b-4efc-8fbc-3b241561cbab) om du vill veta mer om felsökning av AEM as a Cloud Service.

Läs mer om Cloud Manager API och Adobe I/O CLI i följande resurser:

* [Cloud Manager API-dokumentation](https://developer.adobe.com/experience-cloud/cloud-manager/)
* [Adobe I/O CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager)

Mer information om loggfiler i AEM as a Cloud Service finns i följande resurser:

* [Cloud 5 AEM-loggfiler](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/expert-resources/cloud-5/cloud5-aem-log-files#)
* [Felsöka AEM as a Cloud Service med loggar](https://experienceleague.adobe.com/en/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/logs#)
