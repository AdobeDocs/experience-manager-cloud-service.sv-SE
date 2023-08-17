---
title: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
description: Aktuell underhållsanvisning för [!DNL Adobe Experience Manager] as a Cloud Service.
exl-id: eee42b4d-9206-4ebf-b88d-d8df14c46094
source-git-commit: 25af1b0d99f7c5971245f99a95c74d04ca943936
workflow-type: tm+mt
source-wordcount: '661'
ht-degree: 0%

---

# Versionsinformation om underhåll {#maintenance-release-notes}

I följande avsnitt beskrivs den tekniska versionsinformationen för den aktuella underhållsutgåvan av Experience Manager as a Cloud Service.

## Utgåva 13099 {#release-13099}

Nedan sammanfattas de kontinuerliga förbättringarna av underhållsutgåvan 13099, som offentliggjordes den 15 augusti 2023. Den här underhållsversionen är en uppdatering från den tidigare underhållsversionen 12874.

2023.8.0 Funktionsaktivering innehåller alla funktioner som finns i den här underhållsversionen. Se [Roadmap för lanseringar av Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/update-releases-roadmap.html) för mer information.

### Förbättringar {#enhancements-13099}

- SITES-13906: GraphQL - uppgradera till graphql-java 20.1.
- SITES-8972: GraphQL - Lägg till alternativetikett i JSON för datatypen Enumeration.
- SITES-9689: GraphQL - Lägg till rubrik och beskrivning i JSON för datatypen Content Reference.
- SITES-13052: Content Fragments - Export Content Fragments to Adobe Target.

### Åtgärdade problem {#fixed-issues-13099}

- SITES-14937: MSM - Värdet Inherit Rollout Configs from Parent växlar när Spara och stäng slås på live-kopior.
- SITES-14847: Content Fragments - Content Fragment Links are are not marked.
- SITES-11620: Content Fragments - References path is some cut in the UI.
- SITES-14171: GraphQL - Cirkelreferenser bryts inte för cachelagrade data i vissa fall.
- SITES-14577: Experience Fragments - Bulk publish is not working for live copies.
- SITES-14341: Administratörsgränssnitt - Inkonsekvent beteende för knappen Egenskaper när borttagningsbehörigheter tas bort.
- SITES-11000: Administratörsgränssnitt - Referenser: Inkommande länkar saknas på vissa sidor.
- SITES-11559: Administratörsgränssnitt - Referenser: Inkommande länkar visar fel sidor.
- SITES-14337: Administratörsgränssnitt - Öppningsredigeringssidan genererar ett fel i specifika fall.
- SITES-13425: ContextHub - Menu Bar visas inte när du klickar på ContextHub-knappen.
- FORMS-9971: När ett adaptivt formulär återges på ett annat språk tolkas och tillämpas komponenternas synlighet felaktigt.
- FORMS-9888: När ett adaptivt formulär är inställt på att dirigera om till en extern URL (tack) när formuläret skickas, dirigeras det inte om till den externa URL:en.
- FORMS-9845: När du har rensat en listruta med regelredigeraren behålls de värden som tidigare tillhandahållits, trots att de ska tas bort.
- FORMS-9263: När kryssrutans etikett innehåller specialtecken och en användare klickar i kryssrutan, markeras inte kryssrutan.
- FORMS-9254: När en användare bläddrar genom texten i villkorskomponenten aktiveras kryssrutan i komponenten automatiskt innan användaren har bläddrat igenom hela texten.
- FORMS-9045: Skripttaggen löser inte externa fragmentreferenser i bas-XDP.
- FORMS-9026: När du försöker skapa ett adaptivt formulär med hjälp av ett JSON-schema som innehåller uppräkningar med tomma strängar och validerar utan fel, resulterar processen i ett fel. Därefter går det inte att läsa in formuläret korrekt när sidan uppdateras. Ett tomt formulär visas tillsammans med ett fel i loggarna.
- FORMS-8964: I Android™ Chrome/Firefox går det inte att redigera text i textrutekomponenten om den maximala teckengränsen uppnås.
- FORMS-8668: För många Java™-stackar dumpas i felloggar, trots funktionell formuläråtergivning, vilket orsakar att loggfilen blottar.
- FORMS-8554: Adaptiv Forms med lazy loading aktiverat fungerar inte i förhandsgranskningsläget för författarinstansen.
- FORMS-8177: När formulärtjänsten är aktiv är undantaget&quot;com.adobe.aem.formsndocuments.publish.AssetReferenceProvider Det gick inte att hämta resursberoenden.&quot; inträffar. Felet försvinner när formulärtjänsten inaktiveras.
- FORMS-3691: Vissa objekt saknar IFE-omfång (omedelbart anropat funktionsuttryck). Det främsta syftet med att använda en IIFE är att skapa ett omfång för variabler i funktionen, vilket förhindrar att dessa variabler förorenar det globala omfånget.


### Kända fel {#known-issues-13099}

- SITES-15359: Content Fragments - Variantnamnsmönstret matchar inte varianter som har ```'_'``` i sina resursnamn.
- SITES-15463: Sites Templates - Templates kan inte publiceras (tillfällig lösning: använd distributionskonsolen).
- CQ-4354191: Arbetsflöden - Anpassad startfunktion kan utlösas många gånger på grund av replikeringsmetadata som finns på nod:ostrukturerade noder (tillfällig lösning: startprogram för uppdatering som exkluderar egenskaper för replikeringsmetadata för att undvika överlappning).

### Inbäddade tekniker {#embedded-tech-13099}

| Teknik | Version | Länk |
|---|---|---|
| AEM | 1.52-T20230629133256-25c01b8 | [API för Oak API 1.52.0](https://www.javadoc.io/doc/org.apache.jackrabbit/oak-api/1.52.0/index.html) |
| AEM SLING API | Version 2.27.2 | [API för Apache Sling 2.27.2](https://www.javadoc.io/doc/org.apache.sling/org.apache.sling.api/latest/index.html) |
| AEM HTML | Version 1.4.20-1.4.0 | [HTML-mallens språkspecifikation](https://github.com/adobe/htl-spec) |
| Grundläggande komponenter i AEM | Version 2.23.2 | [AEM WCM-kärnkomponenter](https://github.com/adobe/aem-core-wcm-components) |
