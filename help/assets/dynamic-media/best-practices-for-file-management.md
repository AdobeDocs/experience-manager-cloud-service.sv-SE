---
title: Bästa metoderna för att ordna dina digitala resurser för att använda profiler
description: Tips och vedertagna metoder för att namnge, ordna och hantera metadata för filer med digitala resurser.
translation-type: tm+mt
source-git-commit: 6224d193adfb87bd9b080f48937e0af1f03386d6

---


# Bästa tillvägagångssätt för att organisera digitala resurser så att de använder profiler {#best-practices-for-organizing-your-digital-assets-for-using-profiles}

Ett viktigt koncept när det gäller användningen av profiler i AEM Resurser är att de tilldelas mappar. I en profil finns inställningar i form av metadataprofiler, tillsammans med videoprofiler eller bildprofiler. De här inställningarna bearbetar innehållet i en mapp tillsammans med någon av dess undermappar. Därför har hur du namnger filer och mappar, hur du ordnar undermappar och hur du hanterar filerna i dessa mappar stor betydelse för hur resurserna bearbetas av en profil.

Genom att använda konsekventa och lämpliga namngivningsstrategier för filer och mappar tillsammans med god metadatapraxis kan du få ut det mesta av din digitala resurssamling och se till att rätt filer bearbetas med rätt profil.

Se [Profiler för att bearbeta video, metadata och bilder](processing-profiles.md).

Här följer några tips om hur du kan ordna dina digitala resursfiler.

* Ordna dina filer baserat på de metadata du lägger till dem i stället för på de mappar där de finns. Du kan uppnå detta genom att lägga till metadataprofiler.

   * Se [Metadataprofiler.](/help/assets/metadata-profiles.md)
   * Se [Metadata för hantering](/help/assets/manage-metadata.md)av digitala resurser.

* I de flesta fall växer din samling av digitala resurser alltid. Därför är det viktigt att formalisera metadataanvändning, mappstruktur och filnamngivning bland alla dina överförda resurser. Genom att standardisera på dessa saker kan du säkerställa att när din pool med digitala resurser växer kan du använda bearbetningsprofiler på mappar med större precision och enhetlighet.
* Använd endast mappar för att få en enhetlig lagringsstruktur för dina digitala resurser. Mappstrukturer som kan hjälpa dig att förfina vilka profiler som ska tilldelas kan till exempel innehålla följande:

   * **Utvecklingsmappar** - innehåller digitala resurser som du för närvarande arbetar med.
   * **Klientmappar** - innehåller digitala resurser baserade på klienter eller projektnamn.
   * **Huvudmappar** - innehåller digitala källresurser.
   * **Återgivningsmappar** - innehåller återgivningar och kopior av det ursprungliga digitala källmaterialet.
   * **Filstorleksmappar** - innehåller digitala resurser baserade på små, medelstora eller stora filstorlekar.
   * **Mellanlagringsmappar** - innehåller digitala resurser som är klara att publiceras live på din webbplats.
   * **Mime-typsmappar** - innehåller digitala resurser som är specifika för MIME-typer som bilder, dokument och multimedia.
   * **Arkivmappar** - innehåller kasserade digitala resurser.
   * **Datumbaserade mappar** - innehåller digitala resurser baserat på skapandedatum eller senaste ändringsdatum.

* Skapa en katalog med mappar som troligtvis inte ändras så att tilldelade profiler inte bryts.
* Om en resurs redan är publicerad använder du AEM för att flytta resursen till en annan mapp och publicera den på nytt från den nya platsen, är den ursprungliga publicerade resursplatsen fortfarande tillgänglig tillsammans med den nyligen publicerade resursen. Den ursprungliga publicerade resursen är dock&quot;förlorad&quot; för AEM och kan inte avpubliceras. Därför bör du avpublicera resurser först innan du flyttar dem till en annan mapp.

