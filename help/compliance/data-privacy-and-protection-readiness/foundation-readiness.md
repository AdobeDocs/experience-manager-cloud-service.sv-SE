---
title: Dataskydd och dataintegritet - Adobe Experience Manager as a Cloud Service Foundation-beredskap
description: Läs mer om Adobe Experience Manager as a Cloud Service Foundation-stöd för de olika dataskydds- och datasekretessreglerna. I denna artikel ingår EU:s allmänna dataskyddsförordning (GDPR), Kaliforniens konsumentintegritetslag (Privacy Act) och hur man följer den när man genomför ett nytt AEM as a Cloud Service-projekt.
exl-id: 3a4b9d00-297d-4b1d-ae57-e75fbd5c490c
feature: Compliance
role: Admin, Architect, Developer, Leader
source-git-commit: f9ba9fefc61876a60567a40000ed6303740032e1
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 0%

---

# Adobe Experience Manager as a Cloud Service Foundation Readiness for Data Protection and Data Privacy Regulations {#aem-foundation-readiness-for-data-protection-and-data-privacy-regulations}

>[!WARNING]
>
>Innehållet i detta dokument utgör inte juridisk rådgivning och är inte avsett som ersättning för juridisk rådgivning.
>
>Kontakta företagets juridiska avdelning för råd om dataskydd och dataintegritet.

>[!NOTE]
>
>Mer information om Adobe svar på sekretessfrågor och vad det innebär för dig som Adobe-kund finns i [Adobe Privacy Center](https://www.adobe.com/privacy.html).

## Stöd för AEM Foundation Data Privacy and Protection {#aem-foundation-data-privacy-and-protection-support}

På AEM Foundation-nivå lagras de personuppgifter som lagras i användarprofilen. Därför handlar informationen i den här artikeln främst om hur du får åtkomst till och tar bort användarprofiler, så att du kan hantera förfrågningar om åtkomst respektive borttagning.

## Åtkomst till en användarprofil {#accessing-a-user-profile}

### Manuella steg {#manual-steps}

1. Öppna konsolen för användaradministration genom att bläddra till **[!UICONTROL Tools - Security - Users]** eller genom att bläddra direkt till `https://<serveraddress>:<serverport>/security/users.html`

<!--
   ![useradmin2](assets/useradmin2.png)
-->

1. Sök sedan efter användaren genom att skriva namnet i sökfältet högst upp på sidan:

   ![sök efter konto](assets/dpp-foundation-01.png)

1. Öppna sedan användarprofilen genom att klicka på den och kontrollera den på fliken **[!UICONTROL Details]**.

   ![användarprofil](assets/dpp-foundation-02.png)

### HTTP-API {#http-api}

Som vi nämnt tillhandahåller Adobe API:er för åtkomst av användardata, för att underlätta automatisering. Det finns flera typer av API:er som du kan använda:

**API för användaregenskaper**

```shell
curl -u user:password http://localhost:4502/libs/granite/security/search/profile.userproperties.json\?authId\=cavery
```

**Sling API**

**Identifierar användarens startsida:**

```xml
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

**Hämtar användardata:**

Använda nodsökvägen från egenskapen home för JSON-nyttolasten som returneras från ovanstående kommando:

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile.-1.json'
```

```shell
curl -u user:password  'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profiles.-1.json'
```

## Inaktivera en användare och ta bort associerade profiler {#disabling-a-user-and-deleting-the-associated-profiles}

### Inaktivera användare {#disable-user}

1. Öppna konsolen för användaradministration och sök efter användaren i fråga enligt beskrivningen ovan.
2. Håll pekaren över användaren och klicka på markeringsikonen. Profilen blir grå vilket anger att den är markerad.

3. Klicka på **Inaktivera** i den övre menyn för att inaktivera (inaktivera) användaren:

   ![inaktivera konto](assets/dpp-foundation-03.png)

4. Slutligen bekräftar du åtgärden.

   Användargränssnittet anger att användarkontot har inaktiverats genom att ett lås har lagts till i profilkortet:

   ![kontot är inaktiverat](assets/dpp-foundation-04.png)

### Ta bort användarprofilinformation {#delete-user-profile-information}

>[!NOTE]
>
>För AEM as a Cloud Service finns det ingen manuell procedur i användargränssnittet för att ta bort en användarprofil eftersom CRXDE inte är tillgängligt.

### HTTP-API {#http-api-1}

Följande procedurer använder kommandoradsverktyget `curl` för att illustrera hur du inaktiverar användaren med **[!UICONTROL cavery]** `userId` och tar bort användarens profiler som finns på standardplatsen.

**Identifierar användarens startsida:**

```shell
curl -g -u user:password 'http://localhost:4502/libs/granite/security/search/authorizables.json?query={"condition":[{"named":"cavery"}]}'
     {"authorizables":[{"type":"user","authorizableId_xss":"cavery","authorizableId":"cavery","name_xss":"Carlene Avery","name":"Carlene Avery","home":"/home/users/we-retail/DSCP-athB1NYLBXvdTuN"}],"total":1}
```

**Inaktiverar användaren:**

Använda nodsökvägen från egenskapen home för JSON-nyttolasten som returneras från ovanstående kommando:

```shell
curl -X POST -u user:password -FdisableUser="describe the reasons for disabling this user (Data Privacy in this case)" 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN.rw.userprops.html'
```

**Tar bort användarprofiler**

Använd nodsökvägen från egenskapen home för JSON-nyttolasten som returneras från kontoidentifieringskommandot och den kända out-of-box-profilnodplatsen:

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```

```shell
curl -X POST -u user:password -H "Accept: application/json,**/**;q=0.9" -d ':operation=delete' 'http://localhost:4502/home/users/we-retail/DSCP-athB1NYLBXvdTuN/profile'
```
