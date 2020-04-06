---
title: Hantera loggar - molntjänst
description: Hantera loggar - molntjänst
translation-type: tm+mt
source-git-commit: 81f993325b80c0de17d6032a45ebd61c22169d39

---


# Komma åt och hantera loggar {#manage-logs}

Användare kan komma åt en lista över tillgängliga loggfiler för den valda miljön med hjälp av miljökortet.  Användarna kan komma åt en lista över tillgängliga loggfiler för den valda miljön.

De här filerna kan hämtas via användargränssnittet, antingen från **översiktssidan** .

![](assets/manage-logs1.png)

Eller **miljösidan** :

![](assets/manage-logs2.png)

>[!Note]
>Oavsett var den öppnas visas samma dialogruta så att du kan hämta en enskild loggfil.

![](assets/manage-logs3.png)


## Loggar via API {#logs-thorugh-api}

Förutom att hämta loggar via användargränssnittet är loggar tillgängliga via API:t och kommandoradsgränssnittet.

Om du till exempel vill hämta loggfilerna för en viss miljö, skulle kommandot vara något alldeles för stort som raderna i

```java
$ aio cloudmanager:download-logs --programId 5 1884 author aemerror
```

Med följande kommando kan du anpassa loggar:

```java
$ aio cloudmanager:tail-log --programId 5 1884 author aemerror
```

För att få tillgång till miljö-ID (1884 i det här fallet) och tillgängliga service- eller loggnamnsalternativ kan du använda:

```java
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

>[!Note]
>Det går att hämta **loggfiler** både via användargränssnittet och API:t, men **loggspårning** är bara API/CLI.
