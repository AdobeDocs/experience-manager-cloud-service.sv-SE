---
title: Hur kan man förbättra prestanda för stora formulär med lat inläsningsarbete?
description: Lär dig hur du kan förbättra prestanda för stora formulär med lazy loading. Lazy loading förbättrar prestanda avsevärt för stora och komplexa adaptiva Forms genom att skjuta upp initieringen och inläsningen av formulärfragment tills de syns.
feature: Adaptive Forms
role: User
level: Intermediate
exl-id: 0cd38edb-2201-4ca6-8b84-6b5b7f76bd90
source-git-commit: ca0c9f102488c38dbe8c969b54be7404748cbc00
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 0%

---

# Förbättra prestanda för stora formulär med lat inläsningsverktyg{#improve-performance-of-large-forms-with-lazy-loading}

<span class="preview"> Adobe rekommenderar att man använder modern och utbyggbar datainhämtning [Kärnkomponenter](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html) for [skapa ny Adaptive Forms](/help/forms/creating-adaptive-form-core-components.md) eller [lägga till adaptiv Forms på AEM Sites-sidor](/help/forms/create-or-add-an-adaptive-form-to-aem-sites-page.md). De här komponenterna utgör ett betydande framsteg när det gäller att skapa adaptiva Forms-program, vilket ger imponerande användarupplevelser. I den här artikeln beskrivs det äldre sättet att skapa Adaptive Forms med grundläggande komponenter. </span>

| Version | Artikellänk |
| -------- | ---------------------------- |
| AEM 6.5 | [Klicka här](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-advanced-authoring/lazy-loading-adaptive-forms.html) |
| AEM as a Cloud Service | Den här artikeln |


## Introduktion till lazy loading {#introduction-to-lazy-loading}

När formuläret blir stort och komplext med hundratals och tusentals fält får slutanvändarna lång svarstid när de återger formulär vid körning. Med Adaptive Forms kan du minimera svarstiden genom att dela upp formulär i logiska fragment och konfigurera för att skjuta upp initiering eller inläsning av fragment tills fragmentet behöver vara synligt. Det kallas för lat inläsningsarbete. Dessutom tas de fragment som konfigurerats för lazy loading bort när användaren navigerar till andra avsnitt i formuläret och fragmenten inte längre visas.

Låt oss först förstå kraven och de förberedande stegen innan du konfigurerar lazy loading.

## Förbereder för att konfigurera lazy loading {#preparing-to-configure-lazy-loading}

Innan du konfigurerar lazy loading av fragment i ditt adaptiva formulär är det viktigt att du definierar strategier för att skapa fragment, identifiera värden som används i skript eller som refereras i andra fragment samt definierar regler för att styra visningen av fält i lagerinlästa fragment.

* **Identifiera och skapa fragment**
Du kan bara konfigurera adaptiva formulärfragment för lazy loading. Ett fragment är ett fristående segment som ligger utanför ett adaptivt formulär och kan återanvändas i olika formulär. Så det första steget mot att implementera lat inläsningsarbete är att identifiera logiska avsnitt i ett formulär och konvertera dem till fragment. Du kan skapa ett fragment från grunden eller spara en befintlig formulärpanel som fragment.

  <!--For more information about creating fragments, see [Adaptive Form Fragments](adaptive-form-fragments.md).-->

* **Identifiera och markera globala värden**
Forms-baserade transaktioner innefattar dynamiska element för att hämta in relevanta data från användarna och bearbeta dem för att förenkla ifyllandet av formulär. Formuläret har till exempel fält A i fragment X vars värde bestämmer giltigheten för fält B i ett annat fragment. Om fragment X i det här fallet har markerats för lazy loading måste värdet i fält A vara tillgängligt för att validera fält B även när fragment X inte har lästs in. För att uppnå detta kan du markera fält A som globalt, vilket garanterar att dess värde är tillgängligt för validering av fält B när fragment X inte har lästs in.

  Mer information om hur du gör ett fältvärde globalt finns i [Konfigurerar lazy loading](lazy-loading-adaptive-forms.md#p-configuring-lazy-loading-p).

* **Skriv regler för att kontrollera synligheten för fält**
Forms innehåller fält och avsnitt som inte är tillämpliga för alla användare och under alla förhållanden. Forms författare och utvecklare använder synlighets- eller visningsregler för att styra synligheten baserat på användarindata. Fältet Kontorsadress visas t.ex. inte för användare som väljer Arbetslösa i fältet Anställningsstatus i ett formulär. Mer information om hur du skriver regler finns i [Använda regelredigeraren](rule-editor.md).

  Du kan använda synlighetsregler i de lagerinlästa fragmenten så att villkorsfält bara visas när de är obligatoriska. Markera dessutom det villkorliga fältet globalt så att det refererar till det i synlighetsuttrycket för det lagerinlästa fragmentet.

## Konfigurerar lazy loading {#configuring-lazy-loading}

Utför följande steg för att aktivera lazy loading på ett adaptivt formulärfragment:

1. Öppna det adaptiva formuläret i det redigeringsläge som innehåller det fragment som du vill aktivera för lazy loading.
1. Markera det adaptiva formulärfragmentet och tryck på ![konfigurera](assets/configure-icon.svg).
1. Aktivera **[!UICONTROL Load fragment lazily]** och trycka **Klar**.

   ![Aktivera lazy loading för det anpassade formulärfragmentet](assets/lazy-loading-fragment.png)

   Fragmentet är nu aktiverat för lazy loading.

Du kan markera objektvärden i det lagerinlästa fragmentet som globala så att de är tillgängliga för användning i skript när det innehållande fragmentet inte läses in. Gör följande:

1. Öppna det adaptiva formulärfragmentet i redigeringsläge.
1. Tryck på fältet vars värde du vill markera som globalt och tryck sedan på ![konfigurera](assets/configure-icon.svg).
1. Aktivera **[!UICONTROL Use value during lazy loading]**.

   ![Lazy loading field in sidebar](assets/enable-lazy-loading.png)

   Värdet är nu markerat som globalt och är tillgängligt för användning i skript även när det innehållande fragmentet är inaktiverat.

## Överväganden och bästa praxis för konfiguration av lat inläsningsarbete {#considerations-and-best-practices-for-configuring-lazy-loading}

Vissa begränsningar, rekommendationer och viktiga punkter som du bör tänka på när du arbetar med lazy loading är följande:

* Vi rekommenderar att du använder XSD-schemabaserad Adaptiv Forms över XFA-baserad Adaptiv Forms för att konfigurera lat inläsande på stora formulär. Prestandavinster på grund av lazy loading-implementering i XFA-baserad Adaptive Forms är relativt mindre än förstärkning i XSD-baserad Adaptive Forms.
* Konfigurera inte lazy loading på fragment i ett adaptivt formulär som använder **[!UICONTROL Responsive -everything on one page without navigation]** rotpanelens layout. Som ett resultat av layoutkonfigurationen Responsiv läses alla fragment in samtidigt i en adaptiv form. Det kan också leda till försämrade prestanda.
* Vi rekommenderar att du inte konfigurerar lazy loading på fragment på den första panelen som återges när det adaptiva formuläret läses in.
* Lazy loading stöds upp till två nivåer i fragmenthierarkin.
* Se till att fält som markerats som globala är unika i ett adaptivt formulär.
* Överväg att skriva synlighetsregler för fragment som ska visas eller döljas baserat på ett villkor. Du kan till exempel visa eller dölja fragmentet med information om make/maka baserat på den civilstånd som anges av en användare.
* Komponenter för bifogade filer och villkor stöds inte i lagerinlästa fragment.

### Bästa skriptpraxis för konfigurering av lazy loading {#scripting-best-practices-for-configuring-lazy-loading}

Viktiga punkter att tänka på när du utvecklar skript för lazy loading-paneler är följande:

* Se till att initiera och beräkna skript som används på fälten i ett lazy loaded fragment är idempotenta till sin natur. Idempotenta skript är sådana som har samma effekt även efter flera exekveringar.
* Använd den globalt tillgängliga egenskapen för fält för att göra värden för fält som finns i en lat inläsningspanel tillgängliga för alla andra paneler i ett formulär.
* Vidarebefordra inte referensvärdet för ett fält i en lat panel oavsett om fältet markeras globalt över fragment eller inte.
* Använd panelåterställningsfunktionen för att återställa allt som visas på panelen med följande klickuttryck.\
  guideBridge.resolveNode(guideBridge.getFocus({&quot;focusOption&quot;): &quot;navigablePanel&quot;}).resetData()
