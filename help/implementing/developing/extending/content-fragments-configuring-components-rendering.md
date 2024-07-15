---
title: Innehållsfragment Konfigurera komponenter för återgivning
description: Innehållsfragment Konfigurera komponenter för återgivning
exl-id: 6606dc3b-f1b8-4941-8fd0-f69cbd414afa
feature: Developing, Content Fragments
role: Admin, Architect, Developer
source-git-commit: bdf3e0896eee1b3aa6edfc481011f50407835014
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---

# Innehållsfragment Konfigurera komponenter för återgivning{#content-fragments-configuring-components-for-rendering}

Det finns flera [avancerade tjänster](#definition-of-advanced-services-that-need-configuration) som är relaterade till återgivningen av innehållsfragment. För att kunna använda dessa tjänster måste resurstyperna för sådana komponenter göra sig kända för innehållsfragmentets ramverk.

Detta görs genom att konfigurera [OSGi-tjänsten - komponentkonfigurationen för innehållsfragment](#osgi-service-content-fragment-component-configuration).

Denna information krävs när

* Du måste implementera en egen innehållsfragmentbaserad komponent,
* Och måste använda de avancerade tjänsterna.

Adobe rekommenderar att du använder kärnkomponenterna.

>[!CAUTION]
>
>* **Om du inte behöver de [avancerade tjänster](#definition-of-advanced-services-that-need-configuration)** som beskrivs nedan kan du ignorera den här konfigurationen.
>
>* **När du utökar eller använder körklara komponenter** bör du inte ändra OSGi-konfigurationen.
>
>* **Du kan skriva en helt ny komponent som endast använder API:t för innehållsfragment, utan några avancerade tjänster**. I så fall måste du dock utveckla komponenten så att den hanterar lämplig bearbetning.
>
>Därför bör du använda kärnkomponenterna.

## Definition av avancerade tjänster som behöver konfigureras {#definition-of-advanced-services-that-need-configuration}

De tjänster som kräver registrering av en komponent är:

* Kontrollera beroenden korrekt under publiceringen (d.v.s. se till att fragment och modeller kan publiceras automatiskt med en sida om de har ändrats sedan den senaste publiceringen).
* Stöd för innehållsfragment vid fulltextsökning.
* Hantering/hantering av *mellanliggande innehåll.*
* Hantering/hantering av *blandade medieresurser.*
* Dispatcher rensar för refererade fragment (om en sida som innehåller ett fragment publiceras om).
* Använda styckebaserad återgivning.

Om du behöver en eller flera av de här funktionerna är det (oftast) enklare att använda de avancerade tjänsterna som är färdiga i stället för att utveckla dem från grunden.

## OSGi-tjänst - Konfiguration av komponent för innehållsfragment {#osgi-service-content-fragment-component-configuration}

Konfigurationen måste vara bunden till OSGi-tjänsten **Konfiguration av komponent för innehållsfragment**:

`com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl`

>[!NOTE]
>
>Mer information finns i [OSGi-konfiguration](/help/implementing/deploying/overview.md#osgi-configuration).

Till exempel:

![Konfiguration av komponent för OSGi-konfigurationsfragment](assets/cf-component-configuration-osgi.png)

OSGi-konfigurationen är:

<table>
 <thead>
  <tr>
   <td>Etikett</td>
   <td>OSGi-konfiguration<br /> </td>
   <td>Beskrivning</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><strong>Resurstyp</strong></td>
   <td><code>dam.cfm.component.resourceType</code></td>
   <td>Resurstypen som ska registreras, till exempel <br /> <p><span class="cmp-examples-demo__property-value"><code>core/wcm/components/contentfragment/v1/contentfragment</code></code></p> </td>
  </tr>
  <tr>
   <td><strong>Referensegenskap</strong></td>
   <td><code>dam.cfm.component.fileReferenceProp</code></td>
   <td>Namnet på egenskapen som innehåller referensen till fragmentet, till exempel <code>fragmentPath</code> eller <code>fileReference</code></td>
  </tr>
  <tr>
   <td><strong>Elementegenskap(er)</strong></td>
   <td><code>dam.cfm.component.elementsProp</code></td>
   <td>Namnet på den egenskap som innehåller namnen på elementen som ska återges, till exempel<code>elementName</code></td>
  </tr>
  <tr>
   <td><strong>Variationsegenskap</strong><br /> </td>
   <td><code>dam.cfm.component.variationProp</code></td>
   <td>Namnet på den egenskap som innehåller namnet på variationen som ska återges, till exempel<code>variationName</code></td>
  </tr>
 </tbody>
</table>

För vissa funktioner måste komponenten följa fördefinierade konventioner. Följande tabell visar vilka egenskaper som måste definieras, av komponenten, för varje stycke (det vill säga `jcr:paragraph` för varje komponentinstans) så att tjänsterna kan identifiera och bearbeta dem korrekt.

<table>
 <thead>
  <tr>
   <td>Egenskapsnamn</td>
   <td>Beskrivning</td>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><code>paragraphScope</code></td>
   <td><p>En strängegenskap som definierar hur stycken ska skrivas ut i <em>renderingsläget för ett element</em>.</p> <p>Värden:</p>
    <ul>
     <li><code>all</code> : för att återge alla stycken</li>
     <li><code>range</code> : för att återge styckeintervallet från <code>paragraphRange</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphRange</code></td>
   <td><p>En strängegenskap som definierar det intervall med stycken som ska skrivas ut i <em>renderingsläget för ett element</em>.</p> <p>Format:</p>
    <ul>
     <li><code>1</code> eller <code>1-3</code> eller <code>1-3;6;7-8</code> eller <code>*-3;5-*</code>
     <ul>
       <li><code>-</code> intervallindikator</li>
       <li><code>;</code> listavgränsare</li>
       <li><code>*</code> jokertecken</li>
     </ul>
     </li>
     <li>endast utvärderat om <code>paragraphScope</code> är inställt på <code>range</code></li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>paragraphHeadings</code></td>
   <td>En boolesk egenskap som definierar om rubriker (till exempel <code>h1</code>, <code>h2</code>, <code>h3</code>) räknas som stycken (<code>true</code>) eller inte (<code>false</code>)</td>
  </tr>
 </tbody>
</table>

## Exempel {#example}

Se följande (i en AEM som inte finns i kartongen):

```
/apps/core/wcm/config/com.adobe.cq.dam.cfm.impl.component.ComponentConfigImpl-core-comp-v1.config
```

Detta innehåller:

```
dam.cfm.component.resourceType="core/wcm/components/contentfragment/v1/contentfragment"
dam.cfm.component.fileReferenceProp="fragmentPath"
dam.cfm.component.elementsProp="elementName"
dam.cfm.component.variationProp="variationName"
```
