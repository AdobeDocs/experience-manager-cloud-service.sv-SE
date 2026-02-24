---
title: Använda AJO Externa referenser för innehållsfragment
description: Läs mer om tillägget AJO External References i Content Fragment
feature: Content Fragments
role: User, Developer
solution: Experience Manager Sites
badgeSaas: label="AEM Sites" type="Positive" tooltip="Gäller AEM Sites)."
exl-id: 79c90e6b-91da-4f5a-ac96-a98ef7f8d4cd
source-git-commit: 98c0c9b6adbc3d7997bc68311575b1bb766872a6
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 0%

---

# AJO-tillägget Externa referenser för innehållsfragment {#content-fragment-external-references-extension}

Om du vill förhandsgranska upplevelser från AEM i en annan Adobe-produkt kan du aktivera UI-tillägget:

* **Externa referenser för AJO**

Tillägget AJO External References fungerar genom att hämta referenser till Content Fragment från alla organisationer och sandlådor som är associerade med fördefinierade taggar. Tillägget visar sedan information.

För en integrering med Adobe Journey Optimizer (AJO) beror till exempel detaljerna på om referensen är en kampanj, en resa eller en mall.

>[!NOTE]
>
>Mer information om hur du aktiverar tillägget finns i [Extension Manager i AEM Experience Manager.](https://developer.adobe.com/uix/docs/extension-manager/)

Så här använder du tillägget med AJO:

>[!NOTE]
>
>Se även [AJO-integrering](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/integrations/aem-fragments).

1. Öppna konsolen [Innehållsfragment](/help/sites-cloud/administering/content-fragments/overview.md#content-fragments-console).

1. Navigera till ditt innehållsfragment - fragmentet som skapades och användes i olika AJO-kanaler.

1. Öppna ditt innehållsfragment i [redigeraren](/help/sites-cloud/administering/content-fragments/managing.md#editing-the-content-of-your-fragment).

1. Tillägget Externa referenser i AJO är tillgängligt som en flik i den högra panelen. Välj fliken för att öppna tillägget:

   ![AJO-tillägg för externa referenser](/help/sites-cloud/administering/content-fragments/assets/cf-ajo-fragment-external-references-extension.png)

   När en referenstyp har valts visas motsvarande externa referenser som en tabell med kolumnerna:

   * **Namn**: namnet på referensen där innehållsfragmentet används
   * **Förhandsgranska** Välj den här länken för att starta förhandsgranskningen
   * **Status**: status för referensen

1. Du kan välja **referenstyp** i listrutan för att växla mellan tre referenstyper:

   * **Kampanj**
      * Visar en lista med alla kampanjer med länkar till det aktuella innehållsfragmentet.
      * Du kan sedan förhandsgranska en vald kampanj.
      * Standard
   * **Resa**
      * Visar den senaste resan.
      * Du kan sedan markera och förhandsvisa en markerad resa.
   * **Mall**
      * Visar mallar som hör till innehållsfragmentet.
      * Du kan sedan markera och förhandsgranska en vald mall.
