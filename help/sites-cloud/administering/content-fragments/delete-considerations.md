---
title: Innehållsfragment – ta bort överväganden
description: Granska dessa viktiga aspekter innan du definierar dina regler för borttagning av innehållsfragment i AEM. Content Fragments är ett kraftfullt verktyg för att leverera headless-innehåll, och konsekvenserna av att ta bort dem måste noggrant övervägas.
feature: Content Fragments
role: User, Developer, Architect
source-git-commit: 3d20f4bca566edcdb5f13eab581c33b7f3cf286d
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---


# Ta bort överväganden för innehållsfragment {#delete-considerations-content-fragments}

Granska dessa viktiga aspekter innan du definierar borttagningsprinciper för innehållsfragment i AEM. Content Fragments är ett kraftfullt verktyg för att leverera headless-innehåll, och konsekvenserna av att ta bort dem måste noggrant övervägas.

## Behörigheter - ta bort eller inte ta bort {#permissions-delete-or-not-delete}

Möjligheten att ta bort innehåll är kraftfull, men potentiellt känslig, och många branscher måste begränsa och styra hur dessa behörigheter distribueras.

När det gäller borttagningsbehörigheter måste innehållsfragment beaktas på två nivåer:

1. **Innehållsfragmentet som en enskild enhet.**

   * **Använd skiftläge**: En användare som behöver redigera/uppdatera ett innehållsfragment - **och ta bort ett helt fragment**.
   * **Behörigheter**: Behörigheten Ta bort kan tilldelas via användar- och/eller grupphantering.

2. **De flera underenheter som utgör ett innehållsfragment, till exempel variationer, undernoder.**

   Den grundläggande åtgärden i redigeraren för innehållsfragment kräver att sådana tillfälliga delelement kan tas bort. Till exempel när du ändrar variationer, även när du redigerar metadata eller hanterar associerat innehåll.

   * **Använd skiftläge**: En användare som behöver redigera/uppdatera ett innehållsfragment - **utan tillstånd att ta bort ett helt fragment**.
   * **Behörigheter**: Se [Behörigheter krävs endast för redigeringsfunktionen](#permissions-required-for-editor-functionality-only).

>[!NOTE]
>
>Se även Granska åtgärder för användarhantering i AEM.

## Behörigheter krävs endast för redigeringsfunktionen {#permissions-required-for-editor-functionality-only}

För användare som behöver redigera/uppdatera ett innehållsfragment, **utan att tillåta dem att ta bort ett helt fragment** måste specifika behörigheter tilldelas eftersom grundläggande åtgärder i redigeraren för innehållsfragment kräver att tillfälliga delelement kan tas bort.

Till exempel när du ändrar variationer, även när du redigerar metadata eller hanterar associerat innehåll.

>[!NOTE]
>
>De borttagningsbehörigheter som krävs för att redigera/uppdatera ett innehållsfragment ingår i borttagningsbehörigheten som tilldelats via användar- och/eller grupphantering.

Behörigheterna som behövs för att redigera/uppdatera ett fragment måste tillämpas på antingen noden som innehåller innehållsfragmentet eller en lämplig överordnad nod (på alla nivåer under `/content/dam`). När behörigheten tilldelas en sådan överordnad nod tillämpas den på alla noder i den grenen.

En mapp som innehåller alla innehållsfragment, till exempel:

* `/content/dam/contentfragments`

>[!CAUTION]
>
>Ange behörigheter för `/content/dam` är också möjligt eftersom alla innehållsfragment lagras här.
>
>Den här åtgärden använder dock samma borttagningsbehörigheter för *alla* även andra tillgångstyper.

Behörigheten som krävs för att en viss användare och/eller grupp ska kunna redigera/uppdatera ett innehållsfragment är:

>[!NOTE]
>
>I den här listan visas alla behörigheter som krävs, inte bara borttagningsbehörighet.

* För noderna eller mapparna för innehållsfragment:

   * `jcr:addChildNodes`, `jcr:modifyProperties`

* För `jcr:content`nod för alla innehållsfragment:

   * `jcr:addChildNodes`, `jcr:modifyProperties`och `jcr:removeChildNodes`

* För alla noder nedan `jcr:content` av alla innehållsfragment:

   * `jcr:addChildNodes`, `jcr:modifyProperties`och `jcr:removeChildNodes`, `jcr:removeNode`

