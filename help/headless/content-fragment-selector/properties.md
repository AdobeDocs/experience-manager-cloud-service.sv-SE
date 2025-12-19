---
title: Egenskaper för väljaren för innehållsfragment i mikrofon för Adobe Experience Manager as a Cloud Service
description: Egenskaper för att konfigurera Micro-Frontend Content Fragment Selector för att söka, hitta och hämta innehållsfragment från programmet.
role: Admin, User
exl-id: c81b5256-09fb-41ce-9581-f6d1ad316ca4
source-git-commit: 74b9493fc3cdba4a1fc64d1137f5c50c6bebca0a
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 0%

---

# Innehållsfragmentväljare - relaterade egenskaper {#content-fragment-selector-related-properties}

Med väljaren för innehållsfragment på mikrofronten kan du bläddra bland eller söka efter innehållsfragment i databasen och använda dem i programmet.

Du kan använda följande egenskaper för att anpassa hur väljaren för innehållsfragment återges och hur den kan användas:

## Egenskaper för väljaren för innehållsfragment {#content-fragment-selector-properties}

| Egenskap | Typ | Obligatoriskt | Standard | Beskrivning |
|--- |--- |--- |--- |--- |
| `ref` | FragmentSelectorRef | | | Referens till instansen `ContentFragmentSelector` som tillåter åtkomst till tillhandahållna funktioner som `reload`. |
| `imsToken` | string | Nej | | IMS-token används för autentisering. Om inget anges initieras IMS-inloggningsflödet. |
| `repoId` | string | Nej | | Databas-ID som används för fragmentväljaren. När det finns en sådan anslutning ansluter väljaren automatiskt till den angivna databasen och listrutan för databasen döljs. Om det inte anges kan användaren välja en databas i listan över tillgängliga databaser som de har åtkomst till. |
| `defaultRepoId` | string | Nej | | Databas-ID som väljs som standard när databasväljaren visas. Används endast när `repoId` inte har angetts. Om `repoId` anges döljs databasväljaren och det här värdet ignoreras. |
| `orgId` | string | Nej | | Organisations-ID som används för autentisering. Om det inte anges kan användaren välja en databas från olika organisationer som de har åtkomst till. Om användaren inte har åtkomst till någon databas eller organisation läses innehållet inte in. |
| `locale` | string | Nej | `en-US` | Språk. |
| `env` | string | Nej | | Distributionsmiljö. Se typen `Env` för tillåtna miljönamn. |
| `filters` | FragmentFilter | Nej | `{ folder: "/content/dam" }` | Filter som ska tillämpas på listan med innehållsfragment. Som standard visas fragment under `/content/dam`. |
| `isOpen` | boolesk | Nej | `false` | Flagga för att styra om väljaren är öppen eller stängd. |
| `noWrap` | boolesk | Nej | `false` | Avgör om fragmentväljaren återges utan någon omslutningsdialogruta. När värdet är `true` bäddas fragmentväljaren in direkt i den överordnade behållaren. Användbar för att integrera väljaren i anpassade layouter eller arbetsflöden. |
| `onSelectionChange` | ({ contentFragments: `ContentFragmentSelection`, domainName?: `string`, tenantInfo?: `string`, repoId?: `string`, deliveryRepos?: `DeliveryRepository[]` }) => void | Nej | | Återanropsfunktionen aktiveras när valet av innehållsfragment ändras. Tillhandahåller de markerade fragmenten, domännamnet, innehavarinformationen, databas-ID och leveransdatabaserna. |
| `onDismiss` | () => void | Nej | | Callback-funktionen aktiveras när dismiss-åtgärden utförs, till exempel när väljaren stängs. |
| `onSubmit` | ({ contentFragments: `ContentFragmentSelection`, domainName?: `string`, tenantInfo?: `string`, repoId?: `string`, deliveryRepos?: `DeliveryRepository[]` }) => void | Nej | | Återanropsfunktionen aktiveras när användaren bekräftar sitt val. Tar emot valda innehållsfragment, domännamn, innehavarinformation, databas-ID och leveransdatabaser. |
| `theme` | &quot;light&quot; eller &quot;dark&quot; | Nej | | Tema för fragmentväljaren. Som standard är den inställd på unifiedShell-miljötemat. |
| `selectionType` | &quot;single&quot; eller &quot;multiple&quot; | Nej | `single` | Markeringstypen kan användas för att begränsa markeringen för fragmentväljaren. |
| `dialogSize` | &quot;fullscreen&quot; eller &quot;fullscreenTakeover&quot; | Nej | `fullscreen` | Valfri prop för att styra storleken på dialogrutan. |
| `runningInUnifiedShell` | boolesk | Nej | | Anger om DestinationSelector körs under UnifiedShell eller fristående. |
| `readonlyFilters` | ResourceReadonlyFiltersField[] | Nej | | Skrivskyddade filter som tillämpas på listan med innehållsfragment. Dessa filter kan inte tas bort av användaren. |
| `selectedFragments` | ContentFragmentIdentifier[] | Nej | `[]` | Ursprungligt urval av innehållsfragment som ska vara förmarkerat när väljaren öppnas. |
| `hipaaEnabled` | boolesk | Nej | `false` | Anger om HIPAA-kompatibilitet är aktiverad. |
| `inventoryView` | InventoryViewType | Nej | `table` | Lagerstandardvytyp som ska användas i väljaren. |
| `inventoryViewToggleEnabled` | boolesk | Nej | `false` | Anger om lagervyns växlingsknapp är aktiverad så att användaren kan växla mellan tabell- och stödrastervyer. |

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
