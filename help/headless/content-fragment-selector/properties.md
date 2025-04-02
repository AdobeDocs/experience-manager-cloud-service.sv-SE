---
title: Egenskaper för väljaren för innehållsfragment i mikrofon för Adobe Experience Manager as a Cloud Service
description: Egenskaper för att konfigurera Micro-Frontend Content Fragment Selector för att söka, hitta och hämta innehållsfragment från programmet.
role: Admin, User
exl-id: c81b5256-09fb-41ce-9581-f6d1ad316ca4
source-git-commit: a3d8961b6006903c42d983c82debb63ce8abe9ad
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 0%

---

# Innehållsfragmentväljare - relaterade egenskaper {#content-fragment-selector-related-properties}

Med väljaren för innehållsfragment på mikrofronten kan du bläddra bland eller söka efter innehållsfragment i databasen och använda dem i programmet.

Du kan använda följande egenskaper för att anpassa hur väljaren för innehållsfragment återges och hur den kan användas:

## Egenskaper för väljaren för innehållsfragment {#content-fragment-selector-properties}

| Egenskap | Typ | Obligatoriskt | Standard | Beskrivning |
|--- |--- |--- |--- |--- |
| `imsToken` | string | Nej | | IMS-token används för autentisering. |
| `repoId` | string | Nej | | Databas-ID som används för autentisering. |
| `orgId` | string | Ja | | Organisations-ID som används för autentisering. |
| `locale` | string | Nej | | Språkdata. |
| `env` | Miljö | Nej | | Distributionsmiljö för Content Fragment Selector. |
| `filters` | FragmentFilter | Nej | | Filter som ska användas för listan med innehållsfragment. Som standard visas fragment under `/content/dam`. Standardvärde: `{ folder: "/content/dam" }` |
| `isOpen` | boolesk | Ja | `false` | Flagga som utlöser öppning eller stängning av väljaren. |
| `onDismiss` | () => void | Ja | | Funktion som ska anropas när **Dismiss** har valts. |
| `onSubmit` | ({ contentFragments: `{id: string, path: string}[]`, domainNames: `string[]` }) => void | Ja | | Funktion som ska anropas när **Select** används efter att ett eller flera innehållsfragment har markerats. <br><br>Funktionen får:<br><ul><li> de markerade innehållsfragmenten med `id` och `path` fält</li><li>och domännamn relaterade till databasens program-ID och miljö-ID, som har status `ready` och `tier` Publish</li></ul><br>Om det inte finns några domännamn kommer den att användas som en reservdomän. |
| `theme` | &quot;light&quot; eller &quot;dark&quot; | Nej | | Temat för väljaren för innehållsfragment. Standardtemat är inställt på temat för UnifiedShell-miljön. |
| `selectionType` | &quot;single&quot; eller &quot;multiple&quot; | Nej | `single` | Markeringstyp som kan användas för att begränsa markering för FragmentSelector. |
| `dialogSize` | &quot;fullscreen&quot; eller &quot;fullscreenTakeover&quot; | Nej | `fullscreen` | Valfri egenskap som styr dialogstorleken. |
| `waitForImsToken` | boolesk | Nej | `false` | Anger om väljaren för innehållsfragment återges i kontexten för SUSI-flödet och måste vänta tills `imsToken` är klar. |
| `imsAuthInfo` | ImsAuthInfo | Nej | | Objekt som innehåller IMS-autentiseringsinformation för den inloggade användaren. |
| `runningInUnifiedShell` | boolesk | Nej | | Anger om väljaren för innehållsfragment körs under UnifiedShell eller fristående. |
| `readonlyFilters` | ResursSkrivskyddadFilterFält | Nej | | Skrivskyddade filter som kan användas för innehållslistan och som inte kan tas bort. |

## Egenskaper för ImsAuthProps {#imsauthprops-properties}

Egenskaperna `ImsAuthProps` definierar autentiseringsinformationen och det flöde som väljaren för innehållsfragment använder för att hämta en `imsToken`. Genom att ange dessa egenskaper kan du styra hur autentiseringsflödet ska fungera och registrera avlyssnare för olika autentiseringshändelser.

| Egenskapsnamn | Beskrivning |
|--- |--- |
| `imsClientId` | Ett strängvärde som representerar det IMS-klient-ID som används för autentisering. Detta värde tillhandahålls av Adobe och är specifikt för din Adobe AEM CS-organisation. |
| `imsScope` | Beskriver de scope som används vid autentisering. Omfattningarna avgör vilken åtkomstnivå programmet har till organisationens resurser. Flera omfång kan avgränsas med kommatecken. |
| `redirectUrl` | Representerar den URL där användaren omdirigeras efter autentiseringen. Det här värdet ställs vanligtvis in på programmets aktuella URL. Om `redirectUrl` inte anges kommer `ImsAuthService` att använda den redirectUrl som används för att registrera `imsClientId` |
| `modalMode` | Ett booleskt värde som anger om autentiseringsflödet ska visas i ett modalt (popup) eller inte. Om värdet är `true` visas autentiseringsflödet i ett popup-fönster. Om värdet är `false` visas autentiseringsflödet i en helsidesinläsning.<br>**Obs!** För bättre användargränssnitt kan du dynamiskt styra det här värdet om användaren har inaktiverat popup-fönster för webbläsare. |
| `onImsServiceInitialized` | En callback-funktion som anropas när Adobe IMS-autentiseringstjänsten initieras. Den här funktionen har en parameter, `service`, som är ett objekt som representerar Adobe IMS-tjänsten. Mer information finns i [`ImsAuthService`](#imsauthservice-ims-auth-service). |
| `onAccessTokenReceived` | En återanropsfunktion som anropas när en `imsToken` tas emot från Adobe IMS-autentiseringstjänsten. Den här funktionen tar en parameter, `imsToken`, som är en sträng som representerar åtkomsttoken. |
| `onAccessTokenExpired` | En återanropsfunktion som anropas när en åtkomsttoken har upphört att gälla. Den här funktionen används vanligtvis för att utlösa ett nytt autentiseringsflöde för att erhålla en ny åtkomsttoken. |
| `onErrorReceived` | En återanropsfunktion som anropas när ett fel inträffar under autentiseringen. Den här funktionen har två parametrar: feltypen och felmeddelandet. Feltypen är en sträng som representerar feltypen och felmeddelandet är en sträng som representerar felmeddelandet. |

## Egenskaper för ImsAuthService {#imsauthservice-properties}

Klassen `ImsAuthService` hanterar autentiseringsflödet för väljaren för innehållsfragment. Det ansvarar för att erhålla en `imsToken` från Adobe IMS-autentiseringstjänsten. `imsToken` används för att autentisera användaren och ge behörighet till Adobe Experience Manager (AEM) CS-databasen. ImsAuthService använder egenskaperna `ImsAuthProps` för att styra autentiseringsflödet och registrera avlyssnare för olika autentiseringshändelser. Du kan använda den praktiska funktionen `registerContentFragmentSelectorAuthService` för att registrera instansen `ImsAuthService` med väljaren för innehållsfragment. Följande funktioner är tillgängliga för klassen `ImsAuthService`. Om du använder funktionen `registerContentFragmentSelectorAuthService` behöver du dock inte anropa dessa funktioner direkt.

| Funktionsnamn | Beskrivning |
|--- |--- |
| `isSignedInUser` | Avgör om användaren är inloggad på tjänsten och returnerar ett booleskt värde i enlighet med detta. |
| `getImsToken` | Hämtar autentiseringen `imsToken` för den inloggade användaren, som kan användas för att autentisera begäranden till andra tjänster, som att generera resursen _rendering._ |
| `signIn` | Initierar inloggningsprocessen för användaren. Den här funktionen använder `ImsAuthProps` för att visa autentisering i antingen ett popup-fönster eller en fullständig sidinläsning. |
| `signOut` | Signerar användaren från tjänsten, gör sin autentiseringstoken ogiltig och kräver att han/hon loggar in igen för att få åtkomst till skyddade resurser. Om du anropar den här funktionen läses den aktuella sidan in igen. |
| `refreshToken` | Uppdaterar autentiseringstoken för den inloggade användaren, vilket förhindrar att den upphör att gälla och säkerställer oavbruten åtkomst till skyddade resurser. Returnerar en ny autentiseringstoken som kan användas för efterföljande begäranden. |
