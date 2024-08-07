---
title: Analyserar innehållsfragment
description: Förstå strukturen för dina innehållsfragment. Detta ger information som är relevant för både headless-leverans och sidredigering.
feature: Content Fragments
role: User, Developer, Architect
exl-id: d9268c1a-bfe6-4df7-bad9-6007dd79e0aa
solution: Experience Manager Sites
source-git-commit: f66ea281e6abc373e9704e14c97b77d82c55323b
workflow-type: tm+mt
source-wordcount: '128'
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

Öppna fliken **Strukturträd** i redigeringsverktygsfältet för att visa den hierarkiska strukturen för innehållsfragmentet och dess referenser. Använd länkikonen för att öppna referenser.

Till exempel:

![Redigera innehållsfragment - strukturträdet](assets/cf-authoring-structure-tree.png)
