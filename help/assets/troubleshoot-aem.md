---
title: Felsökning i AEM Assets
description: Felsök vanliga AEM Assets-problem med hjälp av artikellänkarna för viktiga AEM Assets=områden, som till exempel överföringar, metadata, sökning, leverans och så vidare.
hidefromtoc: true
hide: true
source-git-commit: 60667c265cf480521fe0c0d646c2665540f110d0
workflow-type: tm+mt
source-wordcount: '588'
ht-degree: 0%

---


# Felsökning i AEM Assets {#troubleshoot-aem-assets}

AEM Assets as a Cloud Service är en molnbaserad, PaaS-lösning för företag som inte bara arbetar med Digital Asset Management och Dynamic Media, utan även använder nästa generations smarta funktioner, som AI/ML. Allt från ett system som alltid är aktuellt, alltid tillgängligt och alltid är tillgängligt.

Det kan dock uppstå problem som påverkar överföringar av resurser, metadata, sökning eller leverans och andra nyckelområden i AEM Assets. I den här artikeln finns felsökningsanvisningar som hjälper dig att diagnostisera och lösa vanliga AEM Assets-problem.

<table>
  <tbody>
  <tr>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-27140">Återgivningar saknas i resurshämtning av ZIP-fil i AEM</a> </td>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26616">Innehållsfragment ingår inte i AEM Assets-licensen</a> </td>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26928">Kommentarerna är begränsade i Assets View trots läsåtkomst</a> </td> 
    </tr>
    <tr>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26715">(Dynamiska media) snurpuppsättningar har fastnat i bearbetningstillståndet i AEM Dynamic Media</a> </td>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26639">DAM-återgivningar (Digital Asset Management) matchar inte originalfilerna i AEM</a> </td>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26873">Återgivningar för smart beskärning har inte genererats i AEMaaCS</a> </td> 
    </tr>
    <tr>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26533">(Dynamiska media) Åtgärda problem med videoöverföring, bearbetning och återgivning i AEM</a> </td>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26922">(Resurslänk) Adobe Asset Link lämnar länkar i ett otillgängligt läge när InDesign används</a> </td>
    <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26677">Felmatchning av videominiatyr mellan Dynamic Media och DAM-kortvyn i AEMaaCS</a> </td> 
    </tr>
    <tr>
  <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26610">Resursbearbetningen misslyckades för stora MP4-filer i AEM as a Cloud Service</a></td>
  <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26871">(Dynamic Media) Dynamic Media-videospelaren fungerar inte i lägre miljöer</a></td>
  <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26103">(Dynamic Media med OpenAPI) Aktivera begränsad Assets-åtkomst till dynamiska media med öppna API:er baserat på IMS-användargrupper</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-23916">När en Tiff-fil med ZIP-komprimeringsformat överförs till AEM Assets genereras inga återgivningar</a></td>
  <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26785">AEM trunkerar extraherad text från stora PDF:er efter 100 kB-token</a></td>
  <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-17628">(Dynamic Media) Ändra URL för dynamiska media för DM Assets</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26655">Lösa problem med synlighet för metadatamatchning för icke-adminanvändare i AEMaaCS</a></td>
  <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26637">(Dynamic Media) Problem med färgändring i bakgrunden för TIFF bildåtergivningar i Dynamic Media</a></td>
  <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26528">AEMaaCS Resursrotationsproblem gör efterföljande rotationer osynliga</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26367">(Dynamic Media) Åtgärda problem med trasiga bilder med Smart Crop i Adobe Experience Manager 6.5 Dynamic Media</a></td>
  <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26450">Ökad överföringsgräns för en del av material för Photoshop Firefly API-integrering</a></td>
  <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26461">(Dynamic Media) Åtgärda skillnader i namn på dynamiska mediefiler i olika AEM-miljöer för PDF-filer</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26233">Vissa bilder visar inte miniatyrbildsrenderingar i Adobe Experience Manager (AEM) as a Cloud Service - Resurs</a></td>
  <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-25294">(Dynamic Media) Sidan Allmänna inställningar för dynamiska media öppnas inte</a></td>
  <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26197">(Dynamic Media) Åtgärda ljudproblem i videofiler med Dynamic Media i AEM</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-25925">Automatisk taggning av nyligen överförda resurser i AEM as a Cloud Service</a></td>
  <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-25889">Smarta taggar fungerar inte efter JWT till OAuth-migrering i AEM</a></td>
  <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-25903">Lös problem med delade länkar i AEM Managed Services</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-25607">(Dynamic Media) Fel vid tillgångsbearbetning i AEM Dynamic Media</a></td>
  <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-25885">(Dynamic Media) Fel vid resurssynkronisering i Adobe Experience Manager (AEM) Dynamic Media</a></td>
  <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-25829">Uppdatera anpassade miniatyrbilder för videoresurser i AEM as a Cloud Service</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-25828">Skillnad i bildmetadata i Adobe Experience Manager (AEM) Assets</a></td>
  <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-21865">Det går inte att dra och släppa en mapp med resurser till AEM Assets Web UI</a></td>
  <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-25525">(Dynamic Media) Lösa problem med materialbearbetning i AEM as a Cloud Service</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-25518">Begränsningar för textrahering för stora PDF-filer i Adobe Experience Manager as a Cloud Service</a></td>
  <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-25562">(Asset Link) Åtgärda problem med anslutning till Adobe Experience Manager (AEM)-resurser i InDesign</a></td>
  <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-25506">(Tillgångslänk) Adobe Asset Link-plugin-nätverksfel: Servern kan inte nås</a></td>
</tr>
<tr>
  <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-25471">(Dynamic Media) Användarrekommendationer för synkronisering av dynamiska media</a></td>
  <td><a href="https://experienceleague.adobe.com/sv/docs/experience-cloud-kcs/kbarticles/ka-26902">(Dynamic Media) Exportera resurser och metadata från Dynamic Media med API</a></td>
  <td></td>
</tr>

</tbody>
  <table>


