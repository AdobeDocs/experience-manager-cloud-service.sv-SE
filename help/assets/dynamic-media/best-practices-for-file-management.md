---
title: Bästa tillvägagångssätt för att ordna digitala resurser för användning av Dynamic Media bildprofiler eller videoprofiler
description: Tips och tips för att namnge, ordna och hantera Dynamic Media bild- och videofiler.
translation-type: tm+mt
source-git-commit: 68cf71054b1cd7dfb2790122ba4c29854ffdf703
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---


# Bästa tillvägagångssätt för att ordna dina digitala resurser så att de kan använda bildprofiler eller videoprofiler{#best-practices-for-organizing-your-digital-assets-for-using-profiles}

Ett viktigt koncept när det gäller användning av Dynamic Media bildprofiler eller videoprofiler är att de tilldelas mappar. Inom en profil finns inställningar för en bild eller video. De här inställningarna bearbetar innehållet i en mapp tillsammans med någon av dess undermappar. Det innebär att hur du namnger filer och mappar, hur du ordnar undermappar och hur du hanterar filerna i dessa mappar har stor inverkan på hur dessa resurser bearbetas av profilen.

Genom att använda konsekventa och lämpliga namngivningsstrategier för filer och mappar tillsammans med god metadatapraxis kan du få ut det mesta av din digitala resurssamling och se till att rätt filer bearbetas med rätt profil.

Se [Om Dynamic Media bildprofil och videoprofiler](about-image-video-profiles.md).

Här följer några tips om hur du kan ordna dina digitala resursfiler.

* Ordna dina filer baserat på de metadata du lägger till dem i stället för på de mappar där de finns. Du kan uppnå detta genom att lägga till metadataprofiler.

   * Se [Metadataprofiler.](/help/assets/metadata-profiles.md)
   * Se [Metadata för hantering av digitala resurser](/help/assets/manage-metadata.md).

* I de flesta fall växer din samling av digitala resurser alltid. Därför är det viktigt att formalisera metadataanvändning, mappstruktur och filnamngivning bland alla dina överförda resurser. Genom att standardisera på dessa saker kan du säkerställa att när din pool med digitala resurser växer kan du använda bearbetningsprofiler på mappar med större precision och enhetlighet.
* Använd endast mappar för att få en enhetlig lagringsstruktur för dina digitala resurser. Mappstrukturer som kan hjälpa dig att förfina vilka profiler som ska tilldelas kan till exempel innehålla följande:

   * **Utvecklingsmappar**  - innehåller digitala resurser som du arbetar med just nu.
   * **Klientmappar**  - innehåller digitala resurser baserade på klienter eller projektnamn.
   * **Primära källmappar**  - innehåller digitala källresurser.
   * **Återgivningsmappar**  - innehåller återgivningar och kopior av det ursprungliga digitala källmaterialet.
   * **Filstorleksmappar**  - innehåller digitala resurser baserade på små, medelstora eller stora filstorlekar.
   * **Mellanlagringsmappar**  - innehåller digitala resurser som är klara att publiceras live på din webbplats.
   * **Mime-typsmappar**  - innehåller digitala resurser som är specifika för MIME-typer som bilder, dokument och multimedia.
   * **Arkivmappar**  - innehåller kasserade digitala resurser.
   * **Datumbaserade mappar**  - innehåller digitala resurser baserat på skapandedatum eller senaste ändringsdatum.

* Skapa en katalog med mappar som troligtvis inte ändras så att tilldelade profiler inte bryts.
* Om en resurs redan är publicerad använder du AEM för att flytta resursen till en annan mapp och publicera på nytt från den nya platsen, men den ursprungliga publicerade resursplatsen är fortfarande tillgänglig tillsammans med den nyligen publicerade resursen. Den ursprungliga publicerade resursen är dock&quot;förlorad&quot; för AEM och kan inte avpubliceras. Därför bör du avpublicera resurser först innan du flyttar dem till en annan mapp.

