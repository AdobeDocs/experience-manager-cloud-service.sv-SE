---
title: Återanvänd innehållsfragment med MSM och Live-kopior
description: Lär dig hur du använder funktionen Live Copy i MSM för att använda samma, eller liknande, innehåll i innehållsfragment på flera platser, samtidigt som du synkroniserar med källinnehållet.
source-git-commit: 3ce1a982055c2f9c900edbd88e079deb6d3a036a
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# Återanvänd innehållsfragment med MSM {#reuse-content-fragments-using-msm}

Med Multi Site Manager (MSM) och funktionen Live Copy kan du använda samma innehåll på flera platser samtidigt som du synkroniserar med källinnehållet.

* Med MSM Live-kopior kan du:
   * Skapa innehåll en gång och sedan
   * Återanvänd det här innehållet i andra områden på samma eller andra webbplatser eller i program.
* MSM upprätthåller sedan Live-relationerna mellan källinnehållet och dess Live-kopior så att:
   * När du ändrar källinnehållet synkroniseras källan och Live-kopior.
   * Du kan bara justera innehållet i Live-kopior genom att koppla från direktrelationen för enskilda undersidor och/eller komponenter.

En detaljerad översikt över MSM-koncept finns på [Återanvända innehåll: Multi Site Manager och Live Copy](/help/sites-cloud/administering/msm/overview.md).

>[!NOTE]
>
>[Multi Site Manager (MSM)](/help/sites-cloud/administering/msm/overview.md) med Adobe Experience Manager kan man återanvända material som skrivits en gång och sedan återanvänts på olika webbplatser.

Med MSM för innehållsfragment kan du:

* Skapa innehållsfragment en gång och gör sedan (länkade) kopior av dessa fragment för återanvändning i andra delar av webbplatsen eller programmet.
* Håll flera kopior synkroniserade genom att uppdatera källkopian en gång och sedan överföra ändringarna till (live) kopiorna.
* Gör lokala ändringar tillfälligt, eller permanent, och gör uppehåll i länken mellan överordnade och underordnade fragment, antingen helt eller för varianter eller fält.

MSM för innehållsfragment i kombination med funktioner i redigeraren för innehållsfragment gör att du kan bryta och återställa arv på fältnivå.

>[!CAUTION]
>
>MSM för innehållsfragment är bara tillgängligt när du använder innehållsfragment via **Resurser** konsol.
>
>MSM-funktionen är *not* är tillgängliga när du använder **Innehållsfragment** konsol.

## Använda {#how-to}

I följande dokumentation finns mer information om hur du använder MSM för innehållsfragment (gäller även för Assets):

* Så här använder du [MSM för innehållsfragment (och resurser)](/help/assets/reuse-assets-using-msm.md)

* [Skapa en Live Copy](/help/assets/reuse-assets-using-msm.md)

  >[!CAUTION]
  >
  >Om du vill använda MSM för att skapa kopior av innehållsfragment) kan du använda alla **Unik** begränsningar bör tas bort från alla datatyper som används i respektive [Modeller för innehållsfragment](/help/assets/content-fragments/content-fragments-models.md).

* [Visa egenskaper och status för källa och Live Copy](/help/assets/reuse-assets-using-msm.md#properties)
* [Sprid ändringar från källa till Live Copy](/help/assets/reuse-assets-using-msm.md#rollout-sync)
* Avbryt och återställ, arv för:
   * fält och variationer i [Innehållsfragmentsredigerare](/help/assets/content-fragments/content-fragments-variations.md#inheritance)
   * [metadata för relaterade resurser](/help/assets/content-fragments/content-fragments-variations.md#canceling-reenabling-inheritance-individual-items)
* [Pausa och återuppta relationen](/help/assets/reuse-assets-using-msm.md#suspend-resume)
* [Ta bort den aktiva relationen](/help/assets/reuse-assets-using-msm.md#detach)
* [Jämför MSM för innehållsfragment (och resurser) med MSM för webbplatser](/help/assets/reuse-assets-using-msm.md#comparison)

## Begränsningar {#limitations}

* Utlösare som inte ändrats och den associerade utrullningskonfigurationen finns inte för innehållsfragment.