---
title: Felsöka Dynamic Media
description: Felsökningstips när du använder Dynamic Media.
topic: "Administrator,Business Practitioner"
role: Administrator,Business Practitioner
exl-id: 3e8a085f-57eb-4009-a5e8-1080b4835ae2
translation-type: tm+mt
source-git-commit: 6b232ab512a6faaf075faa55c238dfb10c00b100
workflow-type: tm+mt
source-wordcount: '993'
ht-degree: 1%

---

# Felsöka Dynamic Media {#troubleshooting-dynamic-media-scene-mode}

I följande avsnitt beskrivs felsökning för Dynamic Media.

## Ny Dynamic Media-konfiguration {#new-dm-config}

Se [Felsöka en ny Dynamic Media-konfiguration](/help/assets/dynamic-media/config-dm.md#troubleshoot-dm-config).

## Allmänt (alla resurser) {#general-all-assets}

Här följer några allmänna tips och tricks för alla resurser.

### Egenskaper för resurssynkroniseringsstatus {#asset-synchronization-status-properties}

Följande resursegenskaper kan granskas i CRXDE Lite för att bekräfta att resursen har synkroniserats från Adobe Experience Manager till Dynamic Media:

| **Egenskap** | **Exempel** | **Beskrivning** |
|---|---|---|
| `<object_node>/jcr:content/metadata/dam:scene7ID` | **`a|364266`** | En allmän indikator på att noden är länkad till Dynamic Media. |
| `<object_node>/jcr:content/metadata/dam:scene7FileStatus` | **Feltext** för PublishComplete | Status för överföring av resurs till Dynamic Media. |
| `<object_node>/jcr:content/metadata/dam:scene7File` | **myCompany/myAssetID** | Måste fyllas i för att URL:er ska kunna genereras till Dynamic Media fjärråtkomst. |
| `<object_node>/jcr:content/dam:lastSyncStatus` | **** efterföljande  **misslyckades:`<error text>`** | Synkroniseringsstatus för uppsättningar (snurra uppsättningar, bilduppsättningar o.s.v.), bildförinställningar, visningsförinställningar, uppdateringar av bildscheman för en resurs eller bilder som har redigerats. |

### Synkroniseringsloggning {#synchronization-logging}

Synkroniseringsfel och problem loggas i `error.log` (Experience Manager-serverkatalog `/crx-quickstart/logs/`). Tillräcklig loggning finns för att fastställa orsaken till de flesta problemen, men du kan öka loggningen till DEBUG för `com.adobe.cq.dam.ips`-paketet via Sling Console ([https://localhost:4502/system/console/slinglog](https://localhost:4502/system/console/slinglog)) för att samla in mer information.

### Versionskontroll {#version-control}

När du ersätter en befintlig Dynamic Media-resurs (samma namn och plats) kan du behålla båda resurserna eller ersätta/skapa en version:

* Om du behåller båda skapas en resurs med ett unikt namn för den publicerade resursens URL. Till exempel är `image.jpg` den ursprungliga resursen och `image1.jpg` den nyligen överförda resursen.

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
       <li>Kontrollera om förinställningen i JCR <code>/etc/dam/presets/viewer/&lt;preset&gt; has lastReplicationAction</code> har definierats. Den här platsen gäller om du har uppgraderat från Experience Manager 6.x till 6.4 och valt att inte migrera. Annars är platsen <code>/conf/global/settings/dam/dm/presets/viewer</code>.</li>
       <li>Kontrollera att resursen i JCR har <code>dam:scene7FileStatus</code><strong> </strong>under Metadata visas som <code>PublishComplete</code>.</li>
      </ul> </li>
    </ol> </td>
   <td><p>Uppdatera sida/navigera till en annan sida och gå tillbaka (JSP för sidorälar måste kompileras om)</p> <p>Om det inte fungerar:</p>
    <ul>
     <li>Publicera resurs.</li>
     <li>Ladda upp resursen igen och publicera den.</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Carousel hotspot flyttas runt efter växling mellan bildrutor</td>
   <td><p>Kontrollera att alla bildrutor har samma storlek.</p> </td>
   <td><p>Använd endast bilder med samma storlek för karusellen.</p> </td>
  </tr>
  <tr>
   <td>Bilden förhandsvisas inte med Dynamic Media Viewer</td>
   <td><p>Kontrollera att resursen innehåller <code>dam:scene7File</code> i metadataegenskaperna (CRXDE Lite)</p> </td>
   <td><p>Kontrollera att alla resurser har avslutat bearbetningen.</p> </td>
  </tr>
  <tr>
   <td>Den överförda resursen visas inte i resursväljaren</td>
   <td><p>Kontrollresursen har egenskapen <code>jcr:content</code> &gt; <strong><code>dam:assetState</code></strong> = <code>processed</code> (CRXDE Lite)</p> </td>
   <td><p>Kontrollera att alla resurser har avslutat bearbetningen.</p> </td>
  </tr>
  <tr>
   <td>På kortvyn visas <strong>Nytt</strong> när resursen inte har börjat bearbeta</td>
   <td>Kontrollera resursen <code>jcr:content</code> &gt; <code>dam:assetState</code> = om <code>unprocessed</code> inte har hämtats av arbetsflödet.</td>
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
     <li>Kontrollera att videon har bearbetats klart genom att bekräfta <code>dam:scene7FileAvs</code> av <code>dam:scene7File</code> i metadata.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Tilldela en videoprofil till mappen.</li>
     <li>Redigera videoprofilen så att den innehåller fler än en kodningsförinställning.</li>
     <li>Vänta tills videon har bearbetats klart.</li>
     <li>Innan du läser in videon igen bör du kontrollera att arbetsflödet för Dynamic Media Encode Video inte körs.<br/> </li>
     <li>Ladda upp videon igen.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Video är inte kodad</td>
   <td>
    <ul>
     <li>Kontrollera om Dynamic Media Cloud Service är konfigurerad.</li>
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
     <li>Kontrollera videostatusen <code>https://localhost:4502/crx/de/index.jsp#/content/dam/folder/videomp4/jcr%3Acontent</code> &gt; <code>dam:assetState</code></li>
    </ul> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Videoåtergivning saknas</td>
   <td><p>När video överförs, men det inte finns några kodade återgivningar:</p>
    <ul>
     <li>Kontrollera att mappen har tilldelats en videoprofil.</li>
     <li>Kontrollera att videon har behandlats färdigt genom att bekräfta <code>dam:scene7FileAvs</code> i metadata.</li>
    </ul> </td>
   <td>
    <ol>
     <li>Tilldela en videoprofil till mappen.</li>
     <li>Vänta på att videon ska bearbetas färdigt.<br /> </li>
    </ol> </td>
  </tr>
 </tbody>
</table>

## Visare {#viewers}

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
   <td><p>Gå till diagnostiksidan för provhanteraren: <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></p> <p>Lägg märke till beräknade värden. När du arbetar korrekt ser du:</p> <p><code>_DMSAMPLE status: 0 unsyced assets - activation not necessary
       _OOTB status: 0 unsyced assets - 0 unactivated assets</code></p> <p><strong>Obs</strong>: Det kan ta ca 10 minuter efter konfigureringen av Dynamic Media molninställningar för de visningsprogramresurser som ska synkroniseras.</p> <p>Om det finns oaktiverade resurser kvar klickar du på någon av <strong>Visa alla oaktiverade resurser</strong>-knapparna för att visa information.</p> </td>
   <td>
    <ol>
     <li>Navigera till förinställningslistan för visningsprogrammet i administratörsverktygen: <code>https://localhost:4502/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code></li>
     <li>Välj alla förinställningar för visningsprogram och klicka sedan på <strong>Publicera</strong>.</li>
     <li>Navigera tillbaka till exempelhanteraren och observera att antalet oaktiverade resurser nu är noll.</li>
    </ol> </td>
  </tr>
  <tr>
   <td>Bilder med visningsförinställningar returnerar 404 från förhandsgranskningen i resursinformationen eller kopierar URL/inbäddningskod</td>
   <td><p>Gör följande i CRXDE Lite:</p>
    <ol>
     <li>Navigera till mappen <code>&lt;sync-folder&gt;/_CSS/_OOTB</code> i Dynamic Media synkroniseringsmapp (t.ex. <code>/content/dam/_CSS/_OOTB</code>),</li>
     <li>Hitta metadatanoden för den problematiska resursen (till exempel <code>&lt;sync-folder&gt;/_CSS/_OOTB/CarouselDotsLeftButton_dark_sprite.png/jcr:content/metadata/</code>).</li>
     <li>Kontrollera om det finns <code>dam:scene7*</code>-egenskaper. Om resursen synkroniserades och publicerades korrekt ser du att <code>dam:scene7FileStatus</code> är <strong>PublishComplete</strong>.</li>
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
     <li>Navigera till <code>/libs/dam/gui/content/s7dam/samplemanager/samplemanager.html</code>
     </li>
     <li>Välj följande åtgärder i ordning:
      <ol>
       <li>Ta bort synkroniseringsmappar.</li>
       <li>Ta bort förinställningsmappen (under <code>/conf</code>).
       <li>Utlös DM Setup Async Job.</li>
      </ol> </li>
     <li>Vänta på meddelande om att synkroniseringen har slutförts i Inkorgen för Experience Manager.
     </li>
    </ol> </td>
  </tr>
 </tbody>
</table>
