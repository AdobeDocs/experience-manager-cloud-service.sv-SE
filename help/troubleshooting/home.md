---
title: Felsökning i AEM Assets och Forms
description: Felsök vanliga problem med AEM Assets och Forms med hjälp av artikellänkarna för nyckelområden som överföring, metadata, sökning, leverans, formulärframtagning, överföring och integrering.
hidefromtoc: true
hide: true
source-git-commit: 5074e777c68c51955b9ad8f055e04067163b9596
workflow-type: tm+mt
source-wordcount: '798'
ht-degree: 0%

---


# Felsöka problem med AEM Assets och Forms {#troubleshoot-aem-assets-forms}

AEM as a Cloud Service erbjuder omfattande lösningar för Digital Asset Management genom AEM Assets och kraftfulla funktioner för att skapa blanketter genom AEM Forms. Båda tjänsterna erbjuder molnbaserade lösningar för Adobe PaaS med nästa generations smarta funktioner, som AI/ML, allt i ett system som alltid är aktuellt, alltid tillgängligt och alltid är tillgängligt.

Komplexa företagsmiljöer kan dock stöta på olika tekniska utmaningar inom olika områden.

Denna omfattande felsökningsguide innehåller systematiska diagnostiska strategier, kategoriserade lösningar och steg-för-steg-lösningar för både AEM Assets och Forms. Varje avsnitt innehåller snabba referensguider, detaljerade felsökningsmetoder och omfattande resurslänkar som hjälper dig att lösa problem effektivt och optimera din AEM Cloud-tjänstmiljö.

## AEM Assets felsökning {#aem-assets-troubleshooting}

AEM Assets effektiviserar hanteringen, organisationen och leveransen av digitala resurser i olika upplevelser. Det kan dock uppstå problem som påverkar överföringar av resurser, metadata, integreringar eller leverans. I den här artikeln finns felsökningsanvisningar som hjälper dig att diagnostisera och lösa vanliga AEM Assets-problem. Genom att följa vägledningen här kan du återställa arbetsflöden effektivt och se till att resurserna är tillgängliga, korrekta och klara att användas i alla kanaler.

### Resurshantering och återgivning {#asset-processing-renditions-issues}

<table>
  <tbody>
  <tr>
    <td><strong>Överför och bearbetar</strong></td>
    <td><strong>Återgivningar</strong></td>
    <td><strong>PDF &amp; textextrahering</strong></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26610">Resursbearbetningen misslyckades för stora MP4-filer i AEM as a Cloud Service</a></td>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26639">DAM-återgivningar matchar inte originalfilerna</a></td>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26785">AEM trunkerar extraherad text från stora PDF:er efter 100 kB-token</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-23916">Tiff-fil med ZIP-komprimeringsöverföringar genererar inga renderingar</a></td>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26233">Bilder som inte visar miniatyrbildsrenderingar i AEM as a Cloud Service</a></td>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-25518">Begränsningar för textrahering för stora PDF-filer i AEM as a Cloud Service</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-21865">Det går inte att dra och släppa en mapp med resurser till AEM Assets Web UI</a></td>
    <td></td>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26528">Resursrotationsproblem gör efterföljande rotationer osynliga</a></td>
  </tr>
  <tr>
  <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26450">Ökad överföringsgräns för en del av material för Photoshop Firefly API-integrering</a></td>
  <td></td>
  <td></td>
  </tr>
  </tbody>
</table>

### Dynamiska medier {#dynamic-media-issues}

<table>
  <tbody>
  <tr>
    <td><strong>Video</strong></td>
    <td><strong>Snurra uppsättningar och smart beskärning</strong></td>
    <td><strong>Leverans och inställningar</strong></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26533">Åtgärda problem med videoöverföring, -bearbetning och -återgivning i AEM</a></td>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26715">Snurra uppsättningar som fastnat i bearbetningstillstånd</a></td>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-17628">Ändra URL för dynamiska media för resurser</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26677">Felaktig matchning av videominiatyrer mellan Dynamic Media och DAM-kortvyn</a></td>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26873">Återgivningar av Smart Crop som inte har genererats i AEM as a Cloud Service</a></td>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26367">Problem med trasig bildbeskärning i AEM 6.5</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26610">Fel vid bearbetning av resurser i AEM Dynamic Media</a></td>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26637">Problem med bakgrundsfärg för TIFF-återgivningar</a></td>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-25294">Sidan Allmänna inställningar för dynamiska media öppnas inte</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26197">Lös ljudproblem i videofiler med Dynamic Media</a></td>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-25885">Fel vid resurssynkronisering i Dynamic Media</a></td>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26461">Lös skillnader i resursnamn mellan miljöer</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26871">Dynamisk videospelare för media fungerar inte i lägre miljöer</a></td>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-25471">Användarrekommendationer för synkronisering av dynamiska media</a></td>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26902">Exportera resurser och metadata från Dynamic Media med API</a></td>
  </tr>
  </tbody>
</table>

### Metadata, taggning och delning {#metadata-tagging-sharing-issues}

<table>
  <tbody>
  <tr>
    <td><strong>Metadata</strong></td>
    <td><strong>Smarta taggar</strong></td>
    <td><strong>Åtkomst och delning</strong></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-25828">Skillnad i bildmetadata i AEM Assets</a></td>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-25925">Automatisk taggning av nyligen överförda resurser</a></td>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26928">Kommentarerna är begränsade i Assets View trots läsåtkomst</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26655">Lösa problem med synlighet för metadatamatchning för icke-adminanvändare</a></td>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-25889">Smarta taggar fungerar inte efter JWT till OAuth-migrering</a></td>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-25903">Lös problem med delade länkar i AEM Managed Services</a></td>
  </tr>

</tbody>
</table>

### Integrering och åtkomst {#integrations-access}

<table>
  <tbody>
    <tr>
      <td><strong>Resurslänk</strong></td>
      <td><strong>Licenser och anpassningar</strong></td>
    </tr>
    <tr>
      <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26922">Adobe Asset Link gör att länkar inte är tillgängliga i InDesign</a></td>
      <td>
        <a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26616">Innehållsfragment ingår inte i AEM Assets-licensen</a><br>
        </td>
    </tr>
    <tr>
      <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-25562">Lösa anslutningsproblem med AEM Asset Link i InDesign</a></td>
      <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-25525">Lösa problem med tillgångsbearbetning i AEM as a Cloud Service</a></td>
    </tr>
    <tr>
      <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-25506">Nätverksfel för Adobe Asset Link Plug-In: Servern kan inte nås</a></td>
      <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-25829">Uppdaterar anpassade miniatyrbilder för videoresurser i AEM as a Cloud Service</a>
      </td>
    </tr>
  </tbody>
</table>




## AEM Forms felsökning {#aem-forms-troubleshooting}

AEM Forms as a Cloud Service har kraftfulla funktioner för att skapa och hantera blanketter. Du kan dock stöta på problem under installations-, konfigurerings-, formulär- eller inskickningsprocesser. I det här avsnittet finns omfattande felsökningsanvisningar för vanliga AEM Forms-problem.

### Problem med installation och konfiguration

<table>
  <tbody>
  <tr>
    <td><strong>Konfiguration</strong></td>
    <td><strong>Problem med att skapa formulär</strong></td>
    <td><strong>Prestanda och cachelagring</strong></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-installation-and-configuration.md">Forms-alternativet är inte tillgängligt i Navigation</a></td>
    <td><a href="/help/forms/form-creation-failing.md">Formulärskapandet misslyckas efter mallpublicering</a></td>
    <td><a href="/help/forms/troubleshooting-caching-performance.md">Adaptiva problem med Forms-cachning</a></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-installation-and-configuration.md#build-pipeline-fails">Bygg fel i pipeline</a></td>
    <td><a href="/help/forms/form-creation-failing.md#cause-form-creation-fails">Problem med publiceringssekvenser för mallar</a></td>
    <td><a href="/help/forms/troubleshooting-caching-performance.md#images-videos-not-invalidated">Invalidering av Dispatcher-cache</a></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-installation-and-configuration.md#bundles-inactive-state">Problem med aktivering av programpaket</a></td>
    <td><a href="/help/forms/known-issues.md">Kända begränsningar för att skapa formulär</a></td>
    <td><a href="/help/forms/troubleshooting-caching-performance.md#cdn-caching-stops-working-after-300-seconds">CDN-cachningsfel</a></td>
  </tr>
  </tbody>
</table>

### Formulärinlämning och integreringsfrågor

<table>
  <tbody>
  <tr>
    <td><strong>Edge Delivery Services</strong></td>
    <td><strong>Anpassade skickaåtgärder</strong></td>
    <td><strong>Integreringsproblem</strong></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-403-forbidden-edge-delivery-form-submission.md">403 Otillåtna fel vid inlämning av formulär</a></td>
    <td><a href="/help/forms/custom-submit-action-troubleshooting.md">502 fel i anpassade skicka-åtgärder</a></td>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-27434">DRM-SAML-omdirigeringsfel</a></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-403-forbidden-edge-delivery-form-submission.md#cors-issues">CORS-konfigurationsproblem</a></td>
    <td><a href="/help/forms/custom-submit-action-troubleshooting.md#resolution">Ohanterad undantagshantering</a></td>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-27075">Skicka-knappen inaktiverad i AEM Sites</a></td>
  </tr>
  <tr>
    <td><a href="/help/forms/troubleshooting-403-forbidden-edge-delivery-form-submission.md#referrer-filter-issues">Refererarfilterkonfiguration</a></td>
    <td><a href="/help/forms/custom-submit-action-for-adaptive-forms-based-on-core-components.md">Bästa tillvägagångssätt för anpassade åtgärder</a></td>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26532">Synlighet för dolda fält efter uppgraderingar</a></td>
  </tr>
  </tbody>
</table>

### Designer och utvecklingsfrågor

<table>
  <tbody>
  <tr>
    <td><strong>AEM Forms Designer</strong></td>
    <td><strong>Utvecklingsmiljö</strong></td>
    <td><strong>Version och kompatibilitet</strong></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26558">Designer 6.5 öppnas inte efter uppgradering</a></td>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-27089">Platshållare kan inte starta med JDK 8/11</a></td>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26862">Visningsproblem för AEM Forms (AEMFD)-paket</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-21018">Fel i PDF Generator JPEG 2000</a></td>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-22689">Konfiguration av JBoss-loggsökväg</a></td>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26846">Felaktiga versionsnummer i Windows</a></td>
  </tr>
  <tr>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-27406">Knappen saknas i PDF-utdata</a></td>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-18084">Uppgraderingsfel för Configuration Manager</a></td>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-17339">Åtgärdsmål för indexskador</a></td>
  </tr>
  </tbody>
</table>



