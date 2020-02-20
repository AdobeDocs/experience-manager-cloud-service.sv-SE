---
title: Publicera dynamiska medieresurser
description: Publicera dynamiska medieresurser
translation-type: tm+mt
source-git-commit: 218afb360ec3a13f2f4562a703ca3184083fa7f6

---


# Publishing Dynamic Media Assets {#publishing-dynamic-media-assets}

Du publicerar dina dynamiska medieresurser genom att välja resurserna och trycka på **[!UICONTROL Publicera]**. När dina dynamiska medieresurser har publicerats är de tillgängliga för dig så att du kan inkludera dem på en webbsida via URL eller genom att bädda in dem.

Du kan också publicera resurser som du överför direkt - utan att behöva göra något från användaren. See [Configuring Dynamic Media](config-dm.md).

I **[!UICONTROL kortvyn]** visas en liten globikon direkt under namnet på en resurs som anger att den är publicerad. I **[!UICONTROL listvyn]** visar en kolumn som är **[!UICONTROL Publicerad]** vilka resurser som är publicerade eller inte.

>[!NOTE]
>
>Om en resurs redan är publicerad använder du AEM för att flytta resursen till en annan mapp och publicera den på nytt från den nya platsen, är den ursprungliga publicerade resursplatsen fortfarande tillgänglig tillsammans med den nyligen publicerade resursen. Den ursprungliga publicerade resursen är dock&quot;förlorad&quot; för AEM och kan inte avpubliceras. Därför bör du avpublicera resurser först innan du flyttar dem till en annan mapp.

Om du tänker publicera videomaterial direkt efter kodningen bör du kontrollera att kodningen är helt klar. När videoklipp fortfarande kodas visas ett arbetsflöde för videobearbetning. När videokodningen är klar bör du kunna förhandsgranska videoåtergivningarna. Då är det säkert att publicera videoklippen utan att det uppstår några publiceringsfel.

See also [Linking URLs to your Web Application](linking-urls-to-yourwebapplication.md).

Se även [Bädda in videovisningsprogrammet på en webbsida.](embed-code.md)

>[!NOTE]
>
>* Resurser måste publiceras för att kunna använda URL:en. Om resurserna inte publiceras kommer det inte att gå att kopiera och klistra in URL-adressen i en webbläsare.
>* Bildförinställningar och visningsförinställningar måste aktiveras och publiceras för direktleverans.
>



Mer information om hur du publicerar en uppsättning eller resurs finns i [Publicera resurser.](/help/assets/manage-digital-assets.md)

## HTTP/2-leverans av Dynamic Media-resurser {#http-delivery-of-dynamic-media-assets}

AEM har nu stöd för leverans av allt dynamiskt medieinnehåll (bilder och video) via HTTP/2. Det betyder att en publicerad URL eller inbäddningskod för bilden eller videon är tillgänglig för integrering med alla program som accepterar en värdbaserad resurs. Den publicerade resursen levereras sedan via HTTP/2-protokollet. Den här leveransmetoden förbättrar sättet som webbläsare och servrar kommunicerar på, vilket ger bättre respons och laddningstider för alla dynamiska medieresurser.

Mer information finns i [HTTP/2-leverans av innehåll med vanliga frågor](/help/assets/dynamic-media/http2faq.md) .
<!--this md file used to reside under sites-administering-->
