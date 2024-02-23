---
title: Använda Dölj villkor
description: Dölj villkor kan användas för att avgöra om en komponentresurs återges eller inte.
exl-id: 2a96f246-fb0f-4298-899e-ebbf9fc1c96f
source-git-commit: f6162dcbc5b7937d55922e8c963a402697110329
workflow-type: tm+mt
source-wordcount: '584'
ht-degree: 0%

---

# Använda Dölj villkor {#using-hide-conditions}

Dölj villkor kan användas för att avgöra om en komponentresurs återges eller inte. Ett exempel på detta är när en mallskapare konfigurerar kärnkomponenten [listkomponent](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/list.html) i [mallredigerare](/help/sites-cloud/authoring/sites-console/templates.md) och bestämmer sig för att inaktivera alternativen för att skapa listan baserat på underordnade sidor. Om du inaktiverar det här alternativet i designdialogrutan anges en egenskap så att när listkomponenten återges utvärderas dolda villkor och alternativet att visa underordnade sidor inte visas.

## Ökning {#overview}

Dialogrutor kan bli mycket komplexa med många alternativ för användaren, som kanske bara använder en del av de alternativ som finns till sitt förfogande. Detta kan leda till en överväldigande upplevelse av användargränssnittet.

Genom att använda dolda villkor kan administratörer, utvecklare och superanvändare dölja resurser baserat på en uppsättning regler. Med den här funktionen kan de bestämma vilka resurser som ska visas när en författare redigerar innehåll.

>[!NOTE]
>
>ACL-behörigheter ersätts inte när du döljer en resurs baserat på ett uttryck. Innehållet kan redigeras men visas inte.

## Implementerings- och användningsinformation {#implementation-and-usage-details}

`com.adobe.granite.ui.components.FilteringResourceWrapper` är ansvarig för att filtrera resurserna baserat på förekomsten och värdet av `granite:hide` -egenskap, som finns i det fält som ska filtreras. Genomförandet av `/libs/cq/gui/components/authoring/dialog/dialog.jsp` innehåller en instans av `FilteringResourceWrapper.`

Implementeringen utnyttjar Graniten [ELResolver API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/docs/server/el.html) och lägger till en `cqDesign` egen variabel via ExpressionCustomizer.

Här är några exempel på hur du döljer villkor i en designnod som finns under `etc/design` eller som en innehållsprincip.

```
${cqDesign.myProperty}
${!cqDesign.myProperty}
${cqDesign.myProperty == 'someText'}
${cqDesign.myProperty != 'someText'}
${cqDesign.myProperty == true}
${cqDesign.myProperty == true}
${cqDesign.property1 == 'someText' && cqDesign.property2 || cqDesign.property3 != 1 || header.myHeader}
```

När du definierar ditt dolda uttryck ska du tänka på:

* För att vara giltig måste omfånget som egenskapen hittas uttryckas (till exempel `cqDesign.myProperty`).
* Värdena är skrivskyddade.
* Funktioner (om det behövs) bör begränsas till en viss uppsättning som tillhandahålls av tjänsten.

## Exempel {#example}

Exempel på dolda villkor finns i hela AEM och [kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) särskilt. Tänk dig till exempel [listkärnkomponent](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/list.html) som implementerats i [WKND, genomgång](/help/implementing/developing/introduction/develop-wknd-tutorial.md).

[Använda mallredigeraren](/help/sites-cloud/authoring/sites-console/templates.md)kan mallskaparen i designdialogrutan definiera vilka alternativ för listkomponenten som är tillgängliga för sidförfattaren. Du kan till exempel välja om listan ska vara en statisk lista, en lista med underordnade sidor, en lista med taggade sidor och så vidare, eller om den ska aktiveras eller inaktiveras.

Om en mallskapare väljer att inaktivera alternativet med underordnade sidor, ställs en designegenskap in och ett dolt villkor utvärderas mot den, vilket gör att alternativet inte återges för sidförfattaren.

1. Som standard kan sidförfattaren använda listkärnkomponenten för att skapa en lista med underordnade sidor genom att välja alternativet **Underordnade sidor**.

   ![Inställningar för List-komponent](assets/hide-conditions-list-settings.png)

1. I designdialogrutan för listkärnkomponenten kan mallskaparen välja alternativet **Inaktivera underordnade** för att förhindra att alternativet att skapa en lista baserad på underordnade sidor visas för sidförfattaren.

   ![Designdialogruta för List-komponent](assets/hide-conditions-list-design.png)

1. En principnod skapas under `/conf/wknd/settings/wcm/policies/wknd/components/list` med en egenskap `disableChildren` ange till `true`.

   ![Nodstruktur för dolt villkor](assets/hide-conditions-node-structure.png)

1. Villkoret hide definieras som värdet för en `granite:hide` egenskap på egenskapsnoden dialog `/libs/core/wcm/components/list/v2/list/cq:dialog/content/items/tabs/items/listSettings/items/columns/items/column/items/listFrom/items/children`

   ![Utvärdering av dolt villkor](assets/hide-conditions-evaluation.png)

1. Värdet för `disableChildren` hämtas från designkonfigurationen och uttrycket `${cqDesign.disableChildren}` utvärderas till `false`, vilket innebär att alternativet inte återges som en del av komponenten.

1. Alternativet **Underordnade sidor** återges inte längre för sidförfattaren när listkomponenten används.

   ![List Component with child option disabled](assets/hide-conditions-child-disabled.png)
