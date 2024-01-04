---
title: Analyserar innehållsfragment
description: Förstå strukturen för de innehållsfragment som används för innehållsleverans. Detta ger information som är relevant för både headless-leverans och sidredigering.
feature: Content Fragments
role: User, Developer, Architect
exl-id: d9268c1a-bfe6-4df7-bad9-6007dd79e0aa
source-git-commit: 19685cb952a890731bd7d75a2adf3cfd841a465f
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 1%

---

# Analyserar strukturen för innehållsfragment {#analyzing-content-fragments-structure}

Innehållsfragment är utformade för [Headless-leverans med GraphQL](/help/sites-cloud/administering/content-fragments/content-delivery-with-graphql.md). Det innebär att de kan ha en struktur med flera lager.

I Experience Manager (AEM) finns flera metoder för att visa och analysera fragmentstrukturen.

## Referenser {#references}

Strukturen med flera lager byggs upp med hjälp av referenser:

* [Datatyper för referenser definieras i innehållsfragmentmodellen](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#using-references-to-form-nested-content)
* När du skriver kan du:
   * [Hantera dessa referenser](/help/sites-cloud/administering/content-fragments/authoring.md##manage-references)
   * [Sök efter överordnade referenser för ditt fragment](/help/sites-cloud/administering/content-fragments/managing.md#parent-references-fragment)

## Strukturträd {#structure-tree}

Öppna **Strukturträd** i redigeringsverktygsfältet för att visa den hierarkiska strukturen för innehållsfragmentet och dess referenser. Använd länkikonen för att öppna referenser.

Till exempel:

![Content Fragment Editor - strukturträd](assets/cf-authoring-structure-tree.png)
