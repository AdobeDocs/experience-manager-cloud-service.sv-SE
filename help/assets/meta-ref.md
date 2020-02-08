---
title: Metadata Schema Reference
description: 'Lär dig mer om standardkonventioner för att beskriva metadata för resurser, inklusive Dublin Core, IPTC och andra metadatamatchningar. '
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Metadata Schema Reference {#metadata-schemata-reference}

Följande referens innehåller information om en viss metadataram (i alfabetisk ordning) samt en lista över egenskaper och deras definitioner.

## Dublin Core {#dublin-core}

Dublin Core-metadata innehåller en standardiserad uppsättning konventioner för att beskriva resurser så att de blir lättare att hitta. I AEM Assets beskriver Dublin Core digitala resurser som video, ljud, bilder och dokument.

Den enkla DCMES-uppsättningen (Dublin Core Metadata Element Set) innehåller 15 metadataelement som listas i följande tabell. Varje Dublin Core-element är valfritt och kan upprepas. Du kan lägga till eller ta bort metadata för Dublin Core på samma sätt som du gör för medietypsspecifika metadata.

Förutom DCMES finns det andra metadataelement som skapats av Dublin Core Initiative. Mer information finns i [Dublin Core Initiative](https://dublincore.org/) .

<table>
 <tbody>
  <tr>
   <td><strong>Egenskap</strong></td> 
   <td><strong>Beskrivning</strong></td> 
  </tr>
  <tr>
   <td>medverkande</td> 
   <td>Den person eller det företag som är ansvarigt för att bidra till innehållet.</td> 
  </tr>
  <tr>
   <td>täckning</td> 
   <td>Den geografiska plats eller tidsperiod som tillgången täcker.<br /> </td> 
  </tr>
  <tr>
   <td>skapare</td> 
   <td>Den person eller det företag som ansvarar för att skapa innehållet.</td> 
  </tr>
  <tr>
   <td>date</td> 
   <td>Datum eller tidsperiod som är associerad med tillgången.<br /> </td> 
  </tr>
  <tr>
   <td>description</td> 
   <td>Mer information om resursen.</td> 
  </tr>
  <tr>
   <td>format</td> 
   <td>Filformat, fysiskt medium eller dimensioner för resursen. AEM använder <code>dc:format</code> för att beteckna resursens mime-typ.<br /> </td> 
  </tr>
  <tr>
   <td>identifierare</td> 
   <td>En unik referens till tillgången.</td> 
  </tr>
  <tr>
   <td>language</td> 
   <td>Språket för resursen (t.ex. en för engelska).</td> 
  </tr>
  <tr>
   <td>utgivare</td> 
   <td>Den person eller det företag som ansvarar för att göra tillgången tillgänglig.</td> 
  </tr>
  <tr>
   <td>relation</td> 
   <td>En relaterad tillgång.</td> 
  </tr>
  <tr>
   <td>rättigheter</td> 
   <td>Information om vem som har behörighet till den här resursen.</td> 
  </tr>
  <tr>
   <td>source</td> 
   <td>En relaterad tillgång som tillgången härrör från.</td> 
  </tr>
  <tr>
   <td>ämne</td> 
   <td>Tillgångens ämne.<br /> </td> 
  </tr>
  <tr>
   <td>title</td> 
   <td>Ett namn för resursen.</td> 
  </tr>
  <tr>
   <td>type</td> 
   <td>Tillgångens art eller genre.</td> 
  </tr>
 </tbody>
</table>

## IPTC {#iptc}

IPTC (International Press Telecommunications Council) är ett konsortium av nyhetsbyråer över hela världen - ett av målen är att utveckla och underhålla tekniska standarder. IPTC definierade en uppsättning metadatastandarder för foton som är nästan allmänt accepterade bland fotografer. Dessa metadatastandarder ingick i den bredare standarden IPTC Information Interchange Model (IIM) som skapades på 1990-talet.

Även om IPTC-huvudinformationen till största delen har ersatts av XMP finns det ett IPTC-kärnschema och ett tilläggsschema för XMP. I bildprogram synkroniseras både XMP- och IPTC-egenskaper.
