---
title: Metodtips för Assets
description: Beroende på hur AEM Resurser är driftsatta och vilka funktioner du använder för materialintag, generering av återgivning och metadataextrahering, kan du identifiera och följa bästa praxis inom olika områden och förbättra systemets stabilitet och prestanda under inläsning avsevärt.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 991d4900862c92684ed92c1afc081f3e2d76c7ff

---


# Metodtips för Assets {#best-practices-for-assets}

Adobe Experience Manager Assets (AEM) Assets är en viktig del i att leverera digitala marknadsföringsupplevelser av hög kvalitet som bidrar till att uppnå affärsmålen genom att öka innehållets hastighet. Om du arbetar med ett stort antal resurser i AEM Assets eller regelbundet/regelbundet överför flera resurser, inklusive videor och dynamiska media, är det viktigt att optimera din digitala resurshantering för att systemet ska bli effektivt.

Beroende på hur du har positionerat AEM Assets för din organisation och vilka funktioner du använder när det gäller tillgångsintag, återgivningsgenerering och metadataextrahering, kan det vara bra att identifiera och följa vedertagna metoder inom olika områden, vilket förbättrar systemets stabilitet och prestanda vid inläsning.

När du har granskat följande riktlinjer får du de kunskaper och verktyg du behöver för att skapa och hantera ett resurshanteringssystem för företag som passar dina behov:

* Vägledning om prestandajustering av resurser: En uppsättning metodtips som kan följas när som helst i implementeringen, även när du är klar, för att säkerställa att du får ut så mycket som möjligt av systemet.
* The Assets Sizing guide: När du skapar uppskattningar för en resursimplementering är det viktigt att se till att det finns tillräckliga resurser tillgängliga när det gäller lagring av resurser, processor, minne, IO och nätverksgenomströmning. Om du ändrar storlek på många av dessa objekt måste du förstå hur många resurser som läses in i systemet. Den här guiden innehåller metodtips som hjälper dig att fastställa effektiva mått för beräkning av den infrastruktur och de resurser som krävs för att driftsätta AEM Assets samt ett storleksbedömningsverktyg.
* Handboken för [resursmigrering](/help/assets/assets-migration-guide.md): Om du vill migrera resurser från ditt äldre system till AEM Resurser finns det flera steg som ska övervägas för att effektivisera migreringsprocessen. Migreringsguiden innehåller metodtips för de uppgifter du utför för att överföra resurserna till AEM på ett fasvis sätt. Detta inkluderar att lägga till metadata, generera återgivningar och aktivera resurserna för att publicera instanser.
* Dokumentet [Assets Network Considerations](/help/assets/assets-network-considerations.md): När du hanterar AEM-instanser är det viktigt att förstå nätverkstopologin för att förstå nätverksprestanda, identifiera kontrollpunkter och beskriva den förväntade användarupplevelsen. Dokumentet Assets Network Considerations behandlar nätverksaspekter när du utformar din AEM Asset-distribution.
* The Assets Monitoring Guide: När din AEM-instans har distribuerats bör du övervaka vissa uppgifter och systemet i allmänhet för att säkerställa systemintegriteten och effektiviteten i åtgärderna. Övervakningsguiden innehåller bästa praxis för övervakning av olika aspekter av ditt system.
* [AEM-skrivbordsappens bästa praxis](https://helpx.adobe.com/experience-manager/desktop-app/aem-desktop-app-best-practices.html): AEM-datorprogrammet länkar din DAM-lösning (Digital Asset Management) till din dator så att du kan öppna de filer som finns i AEM-webbgränssnittet direkt på skrivbordet. Skrivbordsappens lättanvända arbetsflöde aktiveras med hjälp av nätverksdelningsteknik från operativsystemen på datorn. I den här guiden förklaras de viktigaste funktionerna och den rekommenderade användningen av AEM-datorprogrammet.
* [Bästa praxis](/help/assets/aem-cc-integration-best-practices.md)för integrering av AEM och Creative Cloud: Du kan integrera din AEM-instans med Creative Cloud på flera sätt. Om du följer några metodtips för att effektivisera arbetsflödena för integrering och överföring av resurser blir det effektivare. Den här guiden innehåller metodtips om hur du integrerar AEM Assets med Adobe Creative Cloud.
