---
title: Felsöka Dynamic Media
description: Felsöka Dynamic Media.
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6
workflow-type: tm+mt
source-wordcount: '1157'
ht-degree: 1%

---


# Felsöka Dynamic Media {#troubleshooting-dynamic-media-scene-mode}

I följande dokument beskrivs felsökning för Dynamic Media.

## Allmänt (alla resurser) {#general-all-assets}

Här följer några allmänna tips och tricks för alla resurser.

### Egenskaper för resurssynkroniseringsstatus {#asset-synchronization-status-properties}

Följande resursegenskaper kan granskas i CRXDE Lite för att bekräfta den lyckade synkroniseringen av resursen från AEM till Dynamic Media:

| **Egenskap** | **Exempel** | **Beskrivning** |
|---|---|---|
| `<object_node>/jcr:content/metadata/dam:scene7ID` | **`a|364266`** | En allmän indikator på att noden är länkad till Dynamic Media. |
| `<object_node>/jcr:content/metadata/dam:scene7FileStatus` | **PublishComplete** eller feltext | Status för överföring av resurs till Dynamic Media. |
| `<object_node>/jcr:content/metadata/dam:scene7File` | **myCompany/myAssetID** | Måste fyllas i för att URL:er ska kunna genereras till en fjärrresurs av Dynamic Media. |
| `<object_node>/jcr:content/dam:lastSyncStatus` | **lyckades** eller **misslyckades:`<error text>`** | Synkroniseringsstatus för uppsättningar (snurra uppsättningar, bilduppsättningar o.s.v.), bildförinställningar, visningsförinställningar, uppdateringar av bildscheman för en resurs eller bilder som har redigerats. |

### Synkroniseringsloggning {#synchronization-logging}

Synkroniseringsfel och problem loggas in `error.log` (AEM-serverkatalog `/crx-quickstart/logs/`). Tillräcklig loggning finns för att fastställa orsaken till de flesta problemen, men du kan öka loggningen till DEBUG på `com.adobe.cq.dam.ips` paketet via Sling Console ([https://localhost:4502/system/console/slinglog](https://localhost:4502/system/console/slinglog)) för att samla in mer information.

### Flytta, kopiera, ta bort {#move-copy-delete}

Gör följande innan du utför någon av åtgärderna Flytta, Kopiera eller Ta bort:

* För bilder och videoklipp bekräftar du att ett `<object_node>/jcr:content/metadata/dam:scene7ID` värde finns innan du utför åtgärderna flytta, kopiera eller ta bort.
* För bild- och visningsprogramförinställningar måste du bekräfta att det finns ett `https://<server>/crx/de/index.jsp#/etc/dam/presets/viewer/testpreset/jcr%3Acontent/metadata` värde innan du utför åtgärderna flytta, kopiera eller ta bort.
* Om ovanstående metadatavärde saknas måste du överföra resurser på nytt innan du flyttar, kopierar eller tar bort åtgärder.

### Versionskontroll {#version-control}

När du ersätter en befintlig Dynamic Media-resurs (samma namn och plats) kan du behålla båda resurserna eller ersätta/skapa en version:

* Om båda behålls skapas en ny resurs med ett unikt namn för den publicerade resursens URL. Exempel: `image.jpg` är den ursprungliga resursen och `image1.jpg` är den nyligen överförda resursen.

* Det går inte att skapa en version i Dynamic Media. Den nya versionen ersätter den befintliga mediefilen som levereras.

## Bilder och uppsättningar {#images-and-sets}

Om du har problem med bilder och uppsättningar kan du läsa följande felsökningsguide.

<table>
 <tbody>
  <tr>
   <td><strong>Problem</strong></td>
   <td><strong>Felsöka</strong></td>
   <td><strong>Lösning</strong></td>
  </tr>
  <tr>
   <td>Det går inte att komma åt knappen för kopiera URL/bädda in i resursens detaljvy</td>
   <td>
    <ol>
     <li><p>Gå till CRX/DE:</p>
      <ul>
       <li>Kontrollera om förinställningen i den JCR- <code>/etc/dam/presets/viewer/&lt;preset&gt; has lastReplicationAction</code> definition som används. Observera att den här platsen gäller om du uppgraderade från AEM 6.x till 6.4 och avanmälde dig från migrering. I annat fall är platsen <code>/conf/global/settings/dam/dm/presets/viewer</code>.</li>
       <li>Kontrollera att resursen i JCR-filen har <code>dam:scene7FileStatus</code><strong> under Metadata shows som </strong><code>PublishComplete</code>.</li>
      </ul> </li>
    </ol> </td>
   <td><p>Uppdatera sida/navigera till en annan sida och gå tillbaka (JSP för sidorälar måste kompileras om)</p> <p>Om det inte fungerar:</p>
    <ul>
     <li>Publicera resurs.</li>
     <li>Ladda upp resursen igen och publicera den.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Resursväljaren i set editor fastnade i permanent inläsning</td>
   <td><p>Känt fel som ska åtgärdas i 6.4</p> </td>
   <td><p>Stäng väljaren och öppna den igen.</p> </td>
  </tr>
  <tr>
   <td><strong>Markeringsknappen är inte aktiv när du har valt en resurs som en del av redigeringen av en uppsättning</strong></td>
   <td><p> </p> <p>Känt fel som ska åtgärdas i 6.4</p> <p> </p> </td>
   <td><p>Klicka först på en annan mapp i Resursväljaren och gå tillbaka och välj resursen.</p> </td>
  </tr>
  <tr>
   <td>Carousel hotspot flyttas runt efter växling mellan bildrutor</td>
   <td><p>Kontrollera att alla bildrutor har samma storlek.</p> </td>
   <td><p>Använd endast bilder med samma storlek för karusellen.</p> </td>
  </tr>
  <tr>
   <td>Bilden förhandsvisas inte med Dynamic Media Viewer</td>
   <td><p>Kontrollera att resursen innehåller metadataegenskaper <code>dam:scene7File</code> (CRXDE Lite)</p> </td>
   <td><p>Kontrollera att alla resurser har avslutat bearbetningen.</p> </td>
  </tr>
  <tr>
   <td>Den överförda resursen visas inte i resursväljaren</td>
   <td><p>Kontrollera resurs har egenskap <code>jcr:content</code> &gt; <strong><code>dam:assetState</code></strong> = <code>processed</code> (CRXDE Lite)</p> </td>
   <td><p>Kontrollera att alla resurser har avslutat bearbetningen.</p> </td>
  </tr>
  <tr>
   <td>Banderoll på kortvyn visar <strong>Nytt</strong> när resursen inte har börjat bearbeta</td>
   <td>Kontrollera resurs <code>jcr:content</code> &gt; <code>dam:assetState</code> = om <code>unprocessed</code> den inte har hämtats av arbetsflödet.</td>
   <td>Vänta tills resursen har hämtats av arbetsflödet.</td>
  </tr>
  <tr>
   <td>Bilder eller uppsättningar visar inte visningsprogrammets URL eller inbäddningskod</td>
   <td>Kontrollera om visningsförinställningen har publicerats.</td>
   <td><p>Gå till <strong>Verktyg</strong> &gt; <strong>Resurser</strong> &gt; <strong>Visningsförinställningar</strong> och publicera visningsförinställningen.</p> </td>
  </tr>
 </tbody>
</table>

## Video {#video}

Om du har problem med video kan du läsa följande felsökningsguide.

<table>
 <tbody>
  <tr>
   <td><strong>Problem</strong></td>
   <td><strong>Felsöka</strong></td>
   <td><strong>Lösning</strong></td>
  </tr>
  <tr>
   <td>Videon kan inte förhandsgranskas</td>
   <td>
    <ul>
     <li>Kontrollera att mappen har tilldelats en videoprofil (om filformatet inte stöds). Om det inte stöds visas bara en bild.</li>
     <li>Videoprofilen måste innehålla mer än en kodningsförinställning för att generera en AVS-uppsättning (en kodning behandlas som videoinnehåll för MP4-filer). för filer som inte stöds, behandlas på samma sätt som obearbetade).</li>
     <li>Kontrollera att videon har bearbetats klart genom att bekräfta <code>dam:scene7FileAvs</code> i <code>dam:scene7File</code> metadata.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Tilldela en videoprofil till mappen.</li>
     <li>Redigera videoprofilen så att den innehåller fler än en kodningsförinställning.</li>
     <li>Vänta tills videon har bearbetats klart.</li>
     <li>Kontrollera att arbetsflödet Dynamic Media Encode Video inte körs när du läser in videon igen.<br/> </li>
     <li>Ladda upp videon igen.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Video är inte kodad</td>
   <td>
    <ul>
     <li>Kontrollera om molntjänsten Dynamic Media är konfigurerad.</li>
     <li>Kontrollera om en videoprofil är kopplad till mappen för överföring.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Kontrollera att Dynamic Media Configuration under Cloud Services är korrekt konfigurerad.</li>
     <li>Kontrollera att mappen har en videoprofil. Kontrollera även videoprofilen.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Videobearbetning tar för lång tid</td>
   <td><p>Så här avgör du om videokodning fortfarande pågår eller om den har försatts i ett feltillstånd:</p>
    <ul>
     <li>Kontrollera videostatus <code>https://localhost:4502/crx/de/index.jsp#/content/dam/folder/videomp4/jcr%3Acontent</code> &gt; <code>dam:assetState</code></li>
     <li>Övervaka videon från arbetsflödeskonsolen <code>https://localhost:4502/libs/cq/workflow/content/console.html</code> &gt; Flikarna Instanser, Arkiv och Fel.</li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Videoåtergivning saknas</td>
   <td><p>När video överförs, men det inte finns några kodade återgivningar:</p>
    <ul>
     <li>Kontrollera att mappen har tilldelats en videoprofil.</li>
     <li>Kontrollera att videon har bearbetats klart genom att bekräfta <code>dam:scene7FileAvs</code> i metadata.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Tilldela en videoprofil till mappen.</li>
     <li>Vänta tills videon har bearbetats klart.<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## Tittare {#viewers}

Om du har problem med visningsprogram kan du läsa följande felsökningsguide.

<table>
 <tbody>
  <tr>
   <td><strong>Problem</strong></td>
   <td><strong>Felsöka</strong></td>
   <td><strong>Lösning</strong></td>
  </tr>
  <tr>
   <td>Visningsförinställningar publiceras inte</td>
   <td><p>Gå till diagnostiksidan för provhanteraren: <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></p> <p>Lägg märke till beräknade värden. När du arbetar korrekt bör du se:</p> <p><code>_DMSAMPLE status: 0 unsyced assets - activation not necessary
       _OOTB status: 0 unsyced assets - 0 unactivated assets</code></p> <p><strong>Obs</strong>: Det kan ta ca 10 minuter efter konfigurationen av inställningarna för Dynamic Media-molnet för de visningsprogramresurser som ska synkroniseras.</p> <p>Om det finns oaktiverade resurser kvar klickar du på någon av knapparna <strong>Visa alla oaktiverade resurser</strong> för att visa information.</p> </td>
   <td>
    <ol>
     <li>Navigera till förinställningslistan för visningsprogrammet i administratörsverktygen: <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></li>
     <li>Markera alla förinställningar för visningsprogram och klicka sedan på <strong>Publicera</strong>.</li>
     <li>Navigera tillbaka till exempelhanteraren och observera att antalet oaktiverade resurser nu är noll.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Bilder med visningsförinställningar returnerar 404 från förhandsgranskningen i resursinformationen eller kopierar URL/inbäddningskod</td>
   <td><p>Gör följande i CRXDE Lite:</p>
    <ol>
     <li>Navigera till <code>&lt;sync-folder&gt;/_CSS/_OOTB</code> en mapp i Synkroniseringsmappen för dynamiska media (till exempel <code>/content/dam/_CSS/_OOTB</code>),</li>
     <li>Hitta metadatanoden för den problematiska resursen (till exempel <code>&lt;sync-folder&gt;/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png/jcr:content/metadata/</code>).</li>
     <li>Kontrollera om det finns <code>dam:scene7*</code> egenskaper. Om resursen synkroniserades och publicerades ser du att uppsättningen är <code>dam:scene7FileStatus</code> till <strong>PublishComplete</strong>.</li>
     <li>Försök att begära teckningen direkt från Dynamic Media genom att sammanfoga värdena för följande egenskaper och stränglitteraler
      <ul>
       <li><code>dam:scene7Domain</code></li>
       <li><code>"is/content"</code></li>
       <li><code>dam:scene7Folder</code></li>
       <li><code>&lt;asset-name&gt;</code></li>
       <li>Exempel: <code>https://&lt;server&gt;/is/content/myfolder/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png</code></li>
      </ul> </li>
    </ol> </td>
   <td><p>Om exempelmaterialet eller den förinställda teckningen i visningsprogrammet inte har synkroniserats eller publicerats startar du om hela kopierings-/synkroniseringsprocessen:</p>
    <ol>
     <li>Navigera till CRXDE Lite.
      <ul>
       <li>Ta bort <code>&lt;sync-folder&gt;/_CSS/_OOTB</code>.</li>
      </ul> </li>
     <li>Navigera till CRX-pakethanteraren: <code>https://localhost:4502/crx/packmgr/</code><a href="https://localhost:4502/crx/packmgr/"></a>
      <ol>
       <li>Sök efter visningsprogrampaket i listan (börjar med <code>cq-dam-scene7-viewers-content</code>)</li>
       <li>Klicka på <strong>Installera</strong>om.</li>
      </ol> </li>
     <li>Gå till sidan Dynamisk mediekonfiguration under Cloud Services och öppna sedan konfigurationsdialogrutan för din Dynamic Media - S7-konfiguration.
      <ul>
       <li>Klicka på <strong>Spara</strong>om du inte vill göra några ändringar. Detta utlöser logiken igen för att skapa och synkronisera exempelresurserna, CSS för visningsförinställningar och teckningar.<br />  </li>
      </ul> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

