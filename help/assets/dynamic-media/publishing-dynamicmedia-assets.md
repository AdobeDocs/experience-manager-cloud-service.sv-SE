---
title: Publicera Dynamic Media Assets
description: Lär dig hur du publicerar Dynamic Media-resurser.
contentOwner: Rick Brough
feature: Resurshantering
topic: Yrkesverksamma inom affärsverksamhet
role: Business Practitioner
exl-id: 8ee759dc-cb8f-4e80-8175-2c3ba06da862
translation-type: tm+mt
source-git-commit: 6b232ab512a6faaf075faa55c238dfb10c00b100
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 2%

---

# Publicera Dynamic Media Assets {#publishing-dynamic-media-assets}

Du publicerar dina Dynamic Media-resurser genom att välja de resurser du redan har överfört och trycka på **[!UICONTROL Publish]** eller **[!UICONTROL Quick Publish]**. När dina Dynamic Media-resurser har publicerats kan du inkludera dem på en webbsida via en URL eller genom att bädda in kod på sidan.

Du kan också publicera resurser som du överför direkt - utan att behöva göra något från användaren. Eller så kan du selektivt publicera dessa resurser. Se [Konfigurera Dynamic Media](config-dm.md). Eller så kan du selektivt publicera resurser på antingen Dynamic Media eller Adobe Experience Manager, som utesluter varandra, med **[!UICONTROL Selective Publish]** på mappnivå. Se [Arbeta med selektiv publicering i Dynamic Media](/help/assets/dynamic-media/selective-publishing.md).

I **[!UICONTROL Card View]** visas en liten globala ikon direkt under namnet på en resurs och till vänster om datumet och tiden för att ange att den publiceras. I **[!UICONTROL List View]** anger kolumnen **[!UICONTROL Published]** vilka resurser som har publicerats och inte.

>[!NOTE]
>
>Om en resurs redan är publicerad flyttar du resursen till en annan mapp och publicerar den på nytt från den nya platsen, är den ursprungliga publicerade resursplatsen fortfarande tillgänglig tillsammans med den nyligen publicerade resursen. Den ursprungliga publicerade resursen är dock&quot;förlorad&quot; för Experience Manager och kan inte avpubliceras. Därför bör du avpublicera resurser först innan du flyttar dem till en annan mapp.

Om du tänker publicera videomaterial direkt efter kodningen kontrollerar du att kodningen är klar. När videofilmer kodas talar systemet om för dig att ett arbetsflöde för videobearbetning pågår. När videokodningen är klar kan du förhandsgranska videoåtergivningarna. Då är det säkert att publicera videoklippen utan att det uppstår några publiceringsfel.

Se även [Länka URL:er till ditt webbprogram](linking-urls-to-yourwebapplication.md).

Se även [Bädda in Dynamic Media Video Viewer eller Image Viewer på en webbsida](embed-code.md).

>[!NOTE]
>
>* Resurser måste publiceras för att kunna använda URL:en. Om resurserna inte publiceras fungerar inte det att kopiera och klistra in URL-adressen i en webbläsare.
>* Bildförinställningar och visningsförinställningar måste aktiveras och publiceras för direktleverans.

>



Mer information om publicering av en uppsättning eller resurs finns i [Publicera resurser](/help/assets/manage-digital-assets.md).

## HTTP/2-leverans av Dynamic Media-resurser {#http-delivery-of-dynamic-media-assets}

Experience Manager stöder nu leverans av allt Dynamic Media-innehåll (bilder och video) via HTTP/2. Det betyder att en publicerad URL eller inbäddningskod för bilden eller videon är tillgänglig för integrering med alla program som accepterar en värdbaserad resurs. Den publicerade resursen levereras sedan via HTTP/2-protokollet. Den här leveransmetoden förbättrar kommunikationen mellan webbläsare och servrar, vilket ger bättre respons och laddningstider för alla dina Dynamic Media-resurser.

Se [HTTP/2-leverans av innehåll, vanliga frågor och svar](/help/assets/dynamic-media/http2faq.md).

<!--this md file used to reside under sites-administering-->
