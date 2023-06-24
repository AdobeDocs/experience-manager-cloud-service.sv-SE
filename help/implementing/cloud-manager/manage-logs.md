---
title: Komma åt och hantera loggar
description: Lär dig hur du får åtkomst till och hanterar loggar som hjälp i utvecklingsprocessen på AEM as a Cloud Service.
exl-id: f17274ce-acf5-4e7d-b875-75d4938806cd
source-git-commit: 7260649eaab303ba5bab55ccbe02395dc8159949
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 3%

---


# Komma åt och hantera loggar {#manage-logs}

Lär dig hur du får åtkomst till och hanterar loggar som hjälp i utvecklingsprocessen på AEM as a Cloud Service.

Du kan komma åt en lista över tillgängliga loggfiler för den valda miljön med **Miljö** från **Översikt** sida eller miljöinformationssida.

## Laddar ned loggar {#download-logs}

Så här hämtar du loggar:

1. Logga in i Cloud Manager på [my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com/) och välja lämplig organisation och lämpligt program.

1. Navigera till **Miljö** från **Översikt** sida.

1. Välj **Hämta loggar** på ellipsmenyn.

   ![Menyobjektet Hämta loggar](assets/download-logs1.png)

1. I **Hämta loggar** väljer du lämplig **Tjänst** i listrutan

   ![Dialogrutan Hämta loggar](assets/download-preview.png)

1. När du har valt tjänsten klickar du på nedladdningsikonen bredvid den logg du vill hämta.

Du kan även komma åt dina loggar från **Miljö** sida.

![Loggar från miljöskärmen](assets/download-logs.png)

## Loggar via API {#logs-through-api}

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

Mer information om API:t för Cloud Manager och Adobe Developer CLI finns i följande resurser:

* [API-dokumentation för Cloud Manager](https://developer.adobe.com/experience-cloud/cloud-manager/)
* [Adobe Developer CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager)
