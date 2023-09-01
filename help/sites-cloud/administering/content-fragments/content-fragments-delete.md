---
title: Innehållsfragment – ta bort överväganden
description: Granska dessa viktiga aspekter innan du definierar dina regler för borttagning av innehållsfragment i AEM. Content Fragments är ett kraftfullt verktyg för att leverera headless-innehåll, och konsekvenserna av att ta bort dem måste noggrant övervägas.
feature: Content Fragments
role: User
hide: true
index: false
hidefromtoc: true
exl-id: f6698dd8-3e2a-44ac-b00f-df578aa85ffe
source-git-commit: 5ce5746026c5683e79cdc1c9dc96804756321cdb
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 9%

---

# Innehållsfragment – ta bort överväganden {#content-fragments-delete-considerations}

<!--
hide: yes
index: no
hidefromtoc: yes
-->

Granska dessa viktiga aspekter innan du definierar dina regler för borttagning av innehållsfragment i AEM. Content Fragments är ett kraftfullt verktyg för att leverera headless-innehåll, och konsekvenserna av att ta bort dem måste noggrant övervägas.

## Behörigheter - ta bort eller inte ta bort {#permissions-delete-or-not-delete}

Möjligheten att ta bort innehåll är kraftfull, men potentiellt känslig, och många branscher måste begränsa och styra hur dessa behörigheter distribueras.

När det gäller borttagningsbehörigheter måste innehållsfragment beaktas på två nivåer:

1. **Innehållsfragmentet som en enskild enhet.**

   * **Använd skiftläge**: En användare som behöver redigera/uppdatera ett innehållsfragment - **och ta bort ett helt fragment**.
   * **Behörigheter**: Behörigheten Ta bort kan tilldelas via användar- och/eller grupphantering. <!-- The [Delete](/help/sites-administering/security.md#actions) permission can be [assigned through User and/or Group Management](/help/sites-administering/security.md#managing-permissions). -->

2. **De flera underenheter som utgör ett innehållsfragment, till exempel variationer, undernoder.**

   Den grundläggande åtgärden i innehållsfragmentredigeraren kräver att sådana tillfälliga underelement kan tas bort. Till exempel när du ändrar variationer, även när du redigerar metadata eller hanterar associerat innehåll.

   * **Använd skiftläge**: En användare som behöver redigera/uppdatera ett innehållsfragment - **utan tillstånd att ta bort ett helt fragment**.
   * **Behörigheter**: Se [Behörigheter krävs endast för redigeringsfunktionen](#permissions-required-for-editor-functionality-only).

>[!NOTE]
>
>När en användare inte har någon borttagningsbehörighet fungerar redigeraren för innehållsfragment i *skrivskyddad* läge. <!-- When a user does not have any [Delete](/help/sites-administering/security.md#actions) permissions, the Content Fragment editor operates in *read-only* mode. -->

>[!NOTE]
>
>Se även Granska åtgärder för användarhantering i AEM. <!-- See also [How to Audit User Management Operations in AEM](/help/sites-administering/audit-user-management-operations.md). -->

## Behörigheter krävs endast för redigeringsfunktionen {#permissions-required-for-editor-functionality-only}

Användare som behöver redigera/uppdatera ett innehållsfragment, **utan att kunna ta bort ett helt fragment**, måste tilldelas specifika behörigheter, eftersom grundläggande användning av redigeraren för innehållsfragment kräver att tillfälliga underelement kan tas bort.

Till exempel när du ändrar variationer, även när du redigerar metadata eller hanterar associerat innehåll.

>[!NOTE]
>
>De borttagningsbehörigheter som krävs för att redigera/uppdatera ett innehållsfragment ingår i borttagningsbehörigheten som tilldelats via användar- och/eller grupphantering. <!-- The delete permissions, required to edit/update a Content Fragment, are included in the Delete permission [assigned through User and/or Group Management](/help/sites-administering/security.md#managing-permissions). -->

Behörigheterna som behövs för att redigera/uppdatera ett fragment måste tillämpas på antingen noden som innehåller innehållsfragmentet eller en lämplig överordnad nod (på alla nivåer under `/content/dam`). När behörigheten tilldelas en sådan överordnad nod tillämpas den på alla noder i den grenen.

En mapp som till exempel kommer att innehålla alla innehållsfragment, till exempel:

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

   * `jcr:addChildNodes`, `jcr:modifyProperties` och `jcr:removeChildNodes`

* För alla noder nedan `jcr:content` av alla innehållsfragment:

   * `jcr:addChildNodes`, `jcr:modifyProperties` och `jcr:removeChildNodes`, `jcr:removeNode`

<!-- There is no CRXDE Lite -->

<!--
These `remove` privileges must be [administered using Access Control Lists, within CRXDE Lite](/help/sites-administering/user-group-ac-admin.md#access-right-management). 

The `add` and `modify` privileges can also be administered in CRXDE Lite, or using the User Management console.

For example, the definition of the `remove` privileges for a group `content-authors-no-delete`:

![cf-delete-03](assets/cf-delete-03.png)
-->
