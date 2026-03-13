---
title: Ny videovisare
description: Nya Video Viewer i Dynamic Media ger en förbättrad videouppspelning
role: User
exl-id: null
source-git-commit: 32d3585c266aaadb8ec795330baae9b6e2654576
workflow-type: tm+mt
source-wordcount: '1443'
ht-degree: 0%

---


# Nytt visningsprogram för video i Dynamic Media {#new-video-viewer-dynamic-media}

Nya Video Viewer for Dynamic Media ger en moderniserad videouppspelning i Adobe Experience Manager (AEM). Programmet ger en enhetlig och utbyggbar upplevelse i alla miljöer där man skriver, förhandsgranskar och visar webbplatser, samtidigt som man fortsätter att arbeta med befintliga arbetsflöden för dynamiska media.

Befintliga videovisningsprogram i Dynamic Media har stöd för grundläggande uppspelningskrav men har begränsad utbyggbarhet och integrering på händelsenivå för moderna analyser och integreringsscenarier

Nya Video Viewer åtgärdar dessa begränsningar genom att:

* Ger en mer konsekvent uppspelningsupplevelse
* Tillåta explicit visningsprogramval
* Generera strukturerade uppspelningshändelser för programmatisk förbrukning
* stödja integrering med externa analyser och externa system

Visningsprogrammet är tillgängligt som ett extra alternativ och kräver ett explicit val där det stöds. Befintliga videovisningsprogram ersätts inte automatiskt.

Nya Video Viewer är avsedd för organisationer som behöver en förbättrad och utbyggbar videoupplevelse utan att störa befintliga implementeringar.

> **OBS!**
>
> Nya Video Viewer har en begränsad tillgänglighet. Du kan aktivera det genom att skapa en [supportanmälan](https://helpx.adobe.com/se/enterprise/using/support-for-experience-cloud.html).


## Så här fungerar nya Video Viewer {#how-it-works}

Det nya visningsprogrammet för video fungerar så här:

1. En videoresurs hämtas till en mapp som synkroniseras med Dynamic Media.
2. Videon kan förhandsgranskas från sidan med resursinformation med hjälp av **Video (ny)**.
3. Det nya visningsprogrammet för video kan väljas i komponenten **Dynamiska media** när du redigerar sidor på webbplatser.
4. Under uppspelningen skickar visningsprogrammet strukturerade händelser till det överordnade fönstret.
5. Valfria visningsmodifierare kan användas för att styra uppspelningsbeteendet.

## Viktiga skillnader jämfört med den befintliga Video Viewer {#key-differences}

| Område | Beskrivning |
|------|-------------|
| Tillgänglighet för visningsprogram | Visas som ett nytt alternativ med namnet **Video (ny)** |
| Val av visningsprogram | Måste vara explicit markerat |
| Utbyggbarhet | Skapar strukturerade uppspelningshändelser |
| Integrering | Fortsätter att arbeta med befintliga arbetsflöden för dynamiska media |

## Förutsättningar {#prerequisites}

Innan du använder det nya visningsprogrammet kontrollerar du att följande krav är uppfyllda:

| Krav | Beskrivning |
|------------|-------------|
| Dynamisk mediasynkronisering | Resursmappen måste synkroniseras med Dynamic Media. |
| Videoprofil | En videoprofil måste tillämpas på mappen. |
| Videoresurs | En video måste vara inkapslad i mappen. |

Det nya visningsprogrammet för video är tillgängligt från och med **AEM as a Cloud Service version 2025.7.0**.

Kontakta Adobe kundtjänst om du vill aktivera eller inaktivera den nya videovisningsprogrammet.

## Förhandsgranska den nya videovisningsprogrammet {#preview}

Utför följande steg om du vill förhandsgranska den nya videovisaren från sidan med resursinformation:

1. Navigera till **Assets** > **Filer** och öppna den mapp som innehåller videoresursen.
2. Klicka på videoresursen för att öppna sidan med resursinformation.
3. Klicka på **Visare** i den vänstra panelen.
4. Välj **Video (ny)** på panelen **Visare**.
5. Klicka på **URL** för att kopiera förhandsgranskningslänken.
   ![Kopiera URL](assets/Copy-url1.jpg)

## Använda den nya videovisningsprogrammet på webbplatser {#use-in-sites}

Det nya visningsprogrammet för video är tillgängligt via den befintliga komponenten **Dynamic Media** i AEM Sites.

### Lägg till komponenten Dynamic Media

Utför följande steg för att lägga till en video med komponenten Dynamic Media:

1. Öppna sidan i **webbplatsredigeraren**.
2. Dra **Dynamic Media**-komponenten till önskad plats på sidan.
3. Markera komponenten **Dynamiska media** på sidan.
4. Klicka på komponenten för att öppna resursväljaren.
5. Välj en videoresurs.

![Dra komponenten Dynamic Media](assets/drag-component.jpeg)

### Konfigurera visningsprogrammet

Gör så här för att konfigurera visningsförinställningen:

1. Markera komponenten **Dynamiska media** på sidan.
2. Klicka på **Konfigurera** i komponentens verktygsfält.
   ![Öppna inställningar för dynamiska media](assets/configure-asset.png)

3. I dialogrutan **Dynamiska mediainställningar** väljer du **Video (ny)** i listrutan **Visningsförinställning**.
   ![Välj visningsförinställning för video (ny)](assets/viewer-preset.jpeg)

4. Ange eventuella nödvändiga modifierare i fältet **Visningsredigerare** (till exempel `autoplay=true&muted=true`).
   ![Granskningsmodifierare](assets/additional-modifiers.jpeg)

5. Spara ändringarna.

Videon läses in på sidan med hjälp av den nya videovisningsprogrammet.

> **Obs!** Befintliga videoklipp ersätts inte automatiskt i det nya visningsprogrammet. Användarna måste manuellt välja **Video (ny)** i **visningsförinställningen** när de använder komponenten Dynamic Media, eller uppdatera direkta URL:er så att de pekar på den nya videovisaren där det behövs.

### Migrera videor med hjälp av direkta URL:er

Om du får åtkomst till dina videoklipp via direkta URL:er i stället för via komponenten Dynamic Media kan du växla dem till den nya videovisningsprogrammet genom att uppdatera URL:en. Till exempel: `https://s7d1.scene7.com/dmviewers/html5/VideoViewer.html?asset=<video-asset>`

## Modifierare för visningsprogram {#viewer-modifiers}

Med visningsmodifierare kan du styra inläsning av resurser, uppspelningsbeteende, val av direktuppspelningsformat och visning av visningsprogram.

| Modifierare | Beskrivning |
|--------|-------------|
| `asset` | Anger resurs-ID för videon eller den adaptiva videouppsättningen. |
| `posterimage` | Anger den bild som visas innan uppspelningen startar. |
| `serverurl` | Anger rotsökvägen för bildservern. |
| `contenturl` | Anger innehållets rotsökväg. |
| `videoserverurl` | Anger rotsökvägen för videoservern. |
| `sources.dash` | Anger DASH-manifestets URL för uppspelning. |
| `sources.hls` | Anger HLS manifest-URL för uppspelning. |
| `autoplay=true` | Startar uppspelningen automatiskt när videon läses in. |
| `controls=true/false` | Visar eller döljer videouppspelningskontrollerna. |
| `loop=true` | Startar om uppspelningen automatiskt när videon slutar. |
| `muted=true` | Startar uppspelningen i ett avstängt läge. |
| `playbackrates` | Anger tillgängliga alternativ för uppspelningshastighet. |
| `playback` | Anger direktuppspelningsformatet (auto, hls, dash eller progressiv). |
| `progressivebitrate` | Anger bithastigheten för progressiv uppspelning. |
| `initialbitrate` | Anger inledande bithastighet för adaptiv direktuppspelning. |
| `isletterboxed=true/false` | Styr om videon ska ha svarta fält eller inte. |
| `customcss` | Anger en anpassad CSS-fil för visningsprogramformat. |
| `transition` | Anger beteende för att visa eller dölja övergångar för visningsprogramkontroller. |

Modifierare anges som frågeparametrar i fältet **Viewer Modifiers**.

## Händelser som stöds {#supported-events}

Nya Video Viewer genererar följande händelser under uppspelning:

| Händelsetyp | Beskrivning |
|-----------|-------------|
| play | Videon börjar spelas upp |
| paus | Video pausas |
| seek | Användaren söker i videon |
| load | Video läses in |
| stäng | Spelaren är stängd |
| metadata | Metadata, t.ex. varaktighet |
| milstolpe | Uppspelningsmilstolpen har nåtts |
| aktuell_tid | Periodisk uppspelningsläge |
| helskärm | Ange helskärm |
| un_fullscreen | Avsluta helskärm |

## Hantera händelser i det överordnade fönstret {#handling-events}

Med det nya visningsprogrammet för video skickas uppspelningsrelaterade meddelanden till den överordnade sidan under videointeraktioner.

För att kunna hantera dessa händelser måste det överordnade programmet lyssna efter webbläsarmeddelandehändelser och validera meddelandets ursprung innan data bearbetas.

Händelsens nyttolast innehåller information som händelsetyp, uppspelningsläge, aktuell uppspelningstid och ytterligare metadata. Dessa händelser kan användas för att stödja analysspårning, anpassade interaktioner eller integrering med externa system

Adobe rekommenderar att du validerar meddelandets ursprung för att se till att händelser bara bearbetas från betrodda dynamiska mediedomäner.

## Video Engagement Report for the New Video Viewer {#video-engagement-report}

Video Engagement Report innehåller analysstatistik för videoklipp som spelats upp med nya Video Viewer i Dynamic Media. Rapporten levererar aggregerade resultatdata för den angivna månaden och stöder månadsrapportering.

Rapporter skapas på begäran. Om du vill begära en rapport skapar du en [supportanmälan](https://helpx.adobe.com/se/enterprise/using/support-for-experience-cloud.html) och anger följande information:

* Rapportmånad - Ange den månad som rapporten krävs för (till exempel januari 2026).
* E-postadress för leverans - e-postadress till gruppen (rekommenderas) eller den person som ska leverera rapporten

Rapporten innehåller interaktionsstatistik per video, inklusive vyer, visningar, bevakningstid, slutförandegrad och engagemangspoäng.

### Rapportformat

* Rapporterna levereras i CSV-format.
* Varje rad representerar en enda video.
* Mätvärden aggregeras för den valda rapporteringsperioden.
* Borttagna tillgångar tas inte med i rapporten.
* Stöder filtrering av `tenant_name`.

### Rapportfält

Videoengagemangsrapporten innehåller följande fält:

| Fält | Beskrivning | Beräkning |
|-------|------------|-------------|
| `video_id` | Unik videdentifierare. | NA |
| `video_name` | Namnet på videoresursen. | NA |
| `video_created_date` | Datum när videon skapades. | NA |
| `duration_in_seconds` | Videons längd i sekunder. | NA |
| `video_views` | Totalt antal videouppspelningshändelser under den valda rapporteringsperioden. | NA |
| `video_impressions` | Totalt antal gånger videon lästes in. | NA |
| `video_watched_seconds` | Totalt antal sekunder som bevakas över alla uppspelningshändelser. | Antal sekunder som bevakas över alla uppspelningshändelser |
| `play_rate` | Procentandel av videouppspelningen i förhållande till videoklippen. | (`video_views`‡ `video_impressions`) × 100 |
| `avg_time_watched_in_seconds` | Genomsnittligt antal sekunder per vy. | `video_watched_seconds`‡ `video_views` |
| `avg_completion_rate` | Procentandel av visningar som har nått fullständig videoslutförande. | (Slutförda vyer‡ `video_views`) × 100 |
| `engagement_score` | Genomsnittlig bevakningsprocent för alla uppspelningshändelser. | (Total procentandel av tidslinjen för video som visas i alla sessioner? `video_views`) |
| `tenant_name` | Identifierare för det företag eller den klientorganisation som är associerad med data. | NA |

## Frågor och svar {#faq-video-engagement}

+++Om en video är inställd på automatisk uppspelning, räknas den som en vy automatiskt eller först efter att användaren har tittat på den under en minimilängd?

Autostart räknas som en videovy. Uppspelning som startas automatiskt spelas in som en vy.

+++

+++Om en användare bara tittar på en del av en video (t.ex. de första 2 sekunderna och de sista 2 sekunderna av en 10-sekunders video), räknas den som en slutförd vy?

En vy räknas som slutförd när uppspelningen når slutet av tidslinjen, även om delar av videon hoppades över.

+++

+++Om en användare går bakåt och tittar på delar av videon igen, ökar det antalet video_views, engagement_score eller både och?

Delarna av videon som visas på nytt ökar inte antalet video_views. Ytterligare uppspelning bidrar till engagement_score.

+++

+++Om samma användare tittar på samma video flera gånger utan att läsa in sidan igen, hur beräknas video_views och engagement_score?

Upprepad uppspelning utan att sidan läses in igen ökar inte antalet video_views. Ytterligare uppspelning bidrar till engagement_score.

+++

+++Påverkar pausning och återupptagning av en video engagemangsspårning eller beräkning av slutförandefrekvens?

Att pausa och återuppta uppspelningen påverkar inte beräkningen av engagemangsspårning eller slutförandefrekvens.

+++
