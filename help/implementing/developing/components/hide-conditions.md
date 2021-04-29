---
title: Använda Dölj villkor
description: Dölj villkor kan användas för att avgöra om en komponentresurs återges eller inte.
exl-id: 2a96f246-fb0f-4298-899e-ebbf9fc1c96f
translation-type: tm+mt
source-git-commit: fa3280defb2a97954c5ab1b70e7600382e370606
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 1%

---

# Använda Dölj villkor {#using-hide-conditions}

Dölj villkor kan användas för att avgöra om en komponentresurs återges eller inte. Ett exempel på detta är när en mallskapare konfigurerar listkomponenten [](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/list.html) i [mallredigeraren](/help/sites-cloud/authoring/features/templates.md) och bestämmer sig för att inaktivera alternativen för att skapa listan baserat på underordnade sidor. Om du inaktiverar det här alternativet i designdialogrutan anges en egenskap så att när listkomponenten återges utvärderas dolda villkor och alternativet att visa underordnade sidor inte visas.

## Översikt {#overview}

Dialogrutor kan bli mycket komplexa med många alternativ för användaren, som kanske bara använder en del av de alternativ som finns till sitt förfogande. Detta kan leda till en överväldigande upplevelse av användargränssnittet.

Genom att använda dolda villkor kan administratörer, utvecklare och superanvändare dölja resurser baserat på en uppsättning regler. Med den här funktionen kan de bestämma vilka resurser som ska visas när en författare redigerar innehåll.

>[!NOTE]
>
>ACL-behörigheter ersätts inte när du döljer en resurs baserat på ett uttryck. Innehållet kan redigeras men visas inte.

## Implementerings- och användningsinformation {#implementation-and-usage-details}

`com.adobe.granite.ui.components.FilteringResourceWrapper` är ansvarig för att filtrera resurserna baserat på  `granite:hide` egenskapens existens och värde, som finns i det fält som ska filtreras. Implementeringen av `/libs/cq/gui/components/authoring/dialog/dialog.jsp` innehåller en instans av `FilteringResourceWrapper.`

Implementeringen använder Granite [ELResolver API](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/docs/server/el.html) och lägger till en `cqDesign` anpassad variabel via ExpressionCustomizer.

Här är några exempel på hur du döljer villkor i en designnod som antingen finns under `etc/design` eller som en innehållsprincip.

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

* För att vara giltig måste det omfång i vilket egenskapen hittas uttryckas (t.ex. `cqDesign.myProperty`).
* Värdena är skrivskyddade.
* Funktioner (om det behövs) bör begränsas till en viss uppsättning som tillhandahålls av tjänsten.

## Exempel {#example}

Exempel på dolda villkor finns i AEM och i [kärnkomponenterna](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/introduction.html). Anta till exempel att [listkärnkomponenten](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/components/list.html) är implementerad i [WKND-självstudien.](/help/implementing/developing/introduction/develop-wknd-tutorial.md)

[Med mallredigeraren](/help/sites-cloud/authoring/features/templates.md) kan mallskaparen i designdialogrutan definiera vilka alternativ för listkomponenten som är tillgängliga för sidförfattaren. Alternativ som om listan ska kunna vara en statisk lista, en lista med underordnade sidor, en lista med taggade sidor osv. kan aktiveras eller inaktiveras.

Om en mallskapare väljer att inaktivera alternativet för underordnade sidor, ställs en designegenskap in och ett dolt villkor utvärderas mot den, vilket gör att alternativet inte återges för sidförfattaren.

1. Som standard kan sidförfattaren använda listkärnkomponenten för att skapa en lista med underordnade sidor genom att välja alternativet **Underordnade sidor**.

   ![Inställningar för listkomponent](assets/hide-conditions-list-settings.png)

1. I designdialogrutan för listkärnkomponenten kan mallskaparen välja alternativet **Inaktivera underordnade** för att förhindra att alternativet att generera en lista baserad på underordnade sidor visas för sidförfattaren.

   ![Designdialogruta för List-komponent](assets/hide-conditions-list-design.png)

1. En principnod skapas under `/conf/wknd/settings/wcm/policies/wknd/components/list` med egenskapen `disableChildren` inställd på `true`.

   ![Nodstruktur för dolt villkor](assets/hide-conditions-node-structure.png)

1. Villkoret hide definieras som värdet för en `granite:hide`-egenskap i egenskapsnoden `/libs/core/wcm/components/list/v2/list/cq:dialog/content/items/tabs/items/listSettings/items/columns/items/column/items/listFrom/items/children`

   ![Utvärdering av dolt villkor](assets/hide-conditions-evaluation.png)

1. Värdet `disableChildren` hämtas från designkonfigurationen och uttrycket `${cqDesign.disableChildren}` utvärderas till `false`, vilket innebär att alternativet inte återges som en del av komponenten.

1. Alternativet **Underordnade sidor** återges inte längre för sidförfattaren när listkomponenten används.

   ![List Component with child option disabled](assets/hide-conditions-child-disabled.png)
