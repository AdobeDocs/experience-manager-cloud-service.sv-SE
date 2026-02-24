---
title: Mallar för att skapa sidor som är redigerbara med den universella redigeraren
description: Lär dig hur du skapar mallar som kan användas för att skapa sidor som kan redigeras i den universella redigeraren, vilket sparar tid och säkerställer enhetlig profilering.
solution: Experience Manager Sites
feature: Authoring
role: User
badgeSaas: label="AEM Sites" type="Positive" tooltip="Gäller AEM Sites)."
exl-id: f0d60086-e92e-4492-ad50-bef84fed2a82
source-git-commit: 98c0c9b6adbc3d7997bc68311575b1bb766872a6
workflow-type: tm+mt
source-wordcount: '769'
ht-degree: 0%

---


# Mallar för att skapa sidor som är redigerbara med den universella redigeraren {#page-templates}

Lär dig hur du skapar mallar som kan användas för att skapa sidor som kan redigeras i den universella redigeraren, vilket sparar tid och säkerställer enhetlig profilering.

>[!NOTE]
>
>[Mallar är också tillgängliga för att skapa sidor som kan redigeras med sidredigeraren](/help/sites-cloud/authoring/page-editor/templates.md).

## Vad är sidmallar? {#what-are}

Riktlinjer för varumärken och marknadsföring styr ofta särskilda layouter för dina innehållssidor. Det är också ofta en praktisk verklighet att många av dina sidor har samma struktur och layout. Om du vill spara tid för innehållsförfattarna kan du skapa sidor från mallar.

Sidmallar fungerar som mallkopior av sidlayouterna. När du skapar en sida från en mall kopieras det ursprungliga innehållet i mallen till den nya sidan, vilket hjälper dig att fördefiniera den grundläggande layouten och innehållet på sidan för innehållsförfattaren, vilket sparar tid.

## Aktivera sidmallar {#enabling-templates}

Om du vill använda mallar för att skapa sidor som är redigerbara med den universella redigeraren måste du aktivera alternativet.

Aktivera först redigerbara mallar för platsens konfiguration.

1. Använd konsolen **Platser** och [välj platsroten](/help/sites-cloud/authoring/sites-console/introduction.md#selecting-resources).
1. När platsroten har valts trycker eller klickar du på ikonen [**Egenskaper** &#x200B;](/help/sites-cloud/authoring/sites-console/page-properties.md) i verktygsfältet.
1. På fliken **Avancerat** i egenskapsdialogrutan kan du notera värdet i fältet **Cloud-konfiguration**.
1. I huvudnavigeringen väljer du **Verktyg** -> **Allmänt** -> **Konfigurationsläsaren**.
1. I **[Konfigurationsläsaren](/help/implementing/developing/introduction/configurations.md)** markerar du den konfiguration du angav i föregående steg och trycker eller klickar på **Egenskaper** i verktygsfältet.
1. I fönstret **Konfigurationsegenskaper** markerar du alternativet **Redigerbara mallar**.
1. Tryck eller klicka på **Spara och stäng**.

När konfigurationen är aktiverad måste du tillåta mallar för platsen.

1. Använd konsolen **Platser** och [välj platsroten](/help/sites-cloud/authoring/sites-console/introduction.md#selecting-resources).
1. När platsroten har valts trycker eller klickar du på ikonen [**Egenskaper** &#x200B;](/help/sites-cloud/authoring/sites-console/page-properties.md) i verktygsfältet.
1. Tryck eller klicka på knappen **Lägg till** på fliken **Avancerat** i dialogrutan för egenskaper under avsnittet **Mallinställningar** .
1. Lägg till sökvägen **i det nya, tomma fältet som visas under** Tillåtna mallar`/conf/<site>/settings/wcm/templates/.*`.
1. Tryck eller klicka på **Spara och stäng**.

Nu kan du använda mallar för att skapa sidor för din webbplats. Den här uppgiften får bara utföras en gång för varje plats/konfiguration där du vill använda mallar när du skapar sidor som kan redigeras med den universella redigeraren.

## Skapa en ny mall {#create-new}

Du kan antingen [skapa en ny sida](/help/sites-cloud/authoring/sites-console/creating-pages.md) som ska fungera som en mall eller använda en befintlig sida som bas för en mall.

1. Använd konsolen **Platser** för att [navigera till den nya eller befintliga sidan](/help/sites-cloud/authoring/sites-console/introduction.md#selecting-resources) som du vill använda som mall och markera den genom att trycka eller klicka på den.

1. När sidan har valts trycker eller klickar du på ikonen [**Egenskaper** &#x200B;](/help/sites-cloud/authoring/sites-console/edit-page-properties.md) i verktygsfältet.

1. På fliken **Avancerat** i egenskapsdialogrutan under avsnittet **Mallinställningar** väljer du alternativet **Använd sida som mall**.

1. Tryck eller klicka på **Spara och stäng**.

Den nya sidan kan nu användas som mall när nya sidor skapas.

## Skapa en sida från en mall {#creating-from-template}

Att skapa en sida från en mall som kan redigeras med den universella redigeraren är samma arbetsflöde som att [skapa en annan sida](/help/sites-cloud/authoring/sites-console/creating-pages.md).

1. Använd konsolen **Platser** för att [navigera till platsen](/help/sites-cloud/authoring/sites-console/introduction.md#selecting-resources) där du vill skapa den nya sidan.

1. Tryck eller klicka på **Skapa** -> **Sida**.

1. På fliken **Mall** i guiden **Skapa sida** kan du välja vilken mall du vill basera den nya sidan på. Tryck eller klicka på önskad mall för att markera den och tryck eller klicka sedan på **Nästa**.

Slutför guiden på samma sätt som du gör för andra sidor och du har skapat den nya sidan baserat på den valda mallen.

## Sidor och mallar {#pages-vs-templates}

Sidmallar definierar bara sidornas ursprungliga innehåll. Sidorna är sedan helt redigerbara med den universella redigeraren.

* Sidor som skapas från sidmallar är oberoende kopior av mallen.
* Om mallen ändras ändras inte de befintliga sidorna som är baserade på den mallen.
* Innehållsförfattaren kan ändra och uppdatera innehållet på den slutliga sidan efter behov utan begränsningar från mallen.

## Redigerbara mallar {#editable-templates}

Sidor som skapas med [sidredigeraren](/help/sites-cloud/authoring/page-editor/introduction.md) kan också baseras på mallar. Mallar som används för att skapa sidor för den universella redigeraren och sidredigeraren använder båda AEM [redigerbara mallar](/help/implementing/developing/components/templates.md).

Mallar som används för att skapa sidor som kan redigeras med sidredigeraren använder alla funktioner i redigerbara mallar. Mallar som används för att skapa sidor som kan redigeras med den universella redigeraren använder bara den ursprungliga innehållsfunktionen.
