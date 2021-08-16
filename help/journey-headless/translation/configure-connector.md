---
title: Konfigurera översättningsanslutningen
description: Lär dig hur du ansluter AEM till en översättningstjänst.
index: false
hide: true
hidefromtoc: true
source-git-commit: 142c49b6b98dc78c3d36964dada1cfb900afee66
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 0%

---

# Konfigurera översättningsanslutningen {#configure-connector}

Lär dig hur du ansluter AEM till en översättningstjänst.

## Story hittills {#story-so-far}

I det föregående dokumentet på den AEM headless-översättningsresan [Kom igång med AEM headless translation](learn-about.md) lärde du dig att ordna ditt headless-innehåll och hur AEM översättningsverktygen fungerar, och du bör nu:

* Förstå hur viktig innehållsstrukturen är för översättning.
* Förstå hur AEM lagrar headless-innehåll.
* Bekanta dig med AEM översättningsverktyg.

Den här artikeln bygger på dessa grundläggande funktioner så att du kan ta det första konfigurationssteget och konfigurera en översättningstjänst som du sedan använder under resan för att översätta ditt innehåll.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur du konfigurerar en AEM till den översättningstjänst du valt. När du har läst bör du:

* Förstå de viktiga parametrarna i översättningsintegreringsramverket i AEM.
* Du kan skapa en egen anslutning till översättningstjänsten.

## Översättningsintegreringsramverket {#tif}

AEM Translation Integration Framework (TIF) integreras med översättningstjänster från tredje part för att samordna översättning av AEM. Det handlar om tre grundläggande steg.

1. Anslut till översättningstjänsten.
1. Skapa en konfiguration för Translation Integration Framework.
1. Koppla konfigurationen till ditt innehåll.

I följande avsnitt beskrivs dessa steg mer ingående.

## Ansluta till en översättningstjänstleverantör {#connect-translation-provider}

Det första steget är att välja vilken översättningstjänst du vill använda. Det finns många alternativ för översättningstjänster för människor och datorer som är tillgängliga för AEM. De flesta leverantörer erbjuder ett översättningspaket som ska installeras. Avsnittet [Ytterligare resurser](#additional-resources) innehåller ett urval av tillgängliga alternativ.

>[!NOTE]
>
>Översättningsexperten ansvarar vanligtvis för att välja vilken översättningstjänst som ska användas, men administratören ansvarar vanligtvis för att installera det nödvändiga översättningsanslutningspaketet.

För den här resan använder vi Microsoft Translator som AEM tillhandahåller en körklar testlicens. Mer information om den här providern finns i avsnittet [Ytterligare resurser](#additional-resources).

Om du väljer en annan provider måste administratören installera kopplingspaketet enligt översättningstjänstens instruktioner.

>[!NOTE]
>
>Om du använder den färdiga versionen av Microsoft Translator i AEM krävs ingen ytterligare konfiguration och fungerar som den ska utan ytterligare anslutningskonfiguration.
>
>Om du väljer att använda Microsoft Translator-anslutningen för testning behöver du inte utföra stegen i de följande två avsnitten: [Skapa en konfiguration för översättningsintegrering](#create-config) och [Associera konfigurationen med ditt innehåll.](#associate) Du bör dock läsa dem så att du känner till hur du gör när du behöver konfigurera den önskade anslutningen.
>
>Testversionen av Microsoft Translator Connector är inte avsedd för produktion och om du bestämmer dig för att licensiera den måste systemadministratören följa stegen som anges i [avsnittet Ytterligare resurser](#additional-resources) i slutet av det här dokumentet för att konfigurera licensen.

## Skapa en konfiguration för översättningsintegrering {#create-config}

När kopplingspaketet för den översättningstjänst du föredrar har installerats måste du skapa en konfiguration för översättningsintegreringsramverket för den tjänsten. Konfigurationen innehåller följande information:

* Vilken översättningstjänstleverantör som ska användas
* Om översättning till människa eller dator ska utföras
* Om annat innehåll som är associerat med innehållsfragmentet ska översättas, t.ex. taggar

Så här skapar du en ny översättningskonfiguration:

1. Klicka eller tryck på **Verktyg** -> **Cloud Services** -> **Cloud Services** på den globala navigeringsmenyn.
1. Navigera till den plats där du vill skapa konfigurationen i innehållsstrukturen. Detta baseras ofta på ett visst projekt eller kan vara globalt.
   * I det här fallet kan till exempel en konfiguration göras globalt för att gälla allt innehåll, eller bara för WKND-projektet.

   ![Plats för översättningskonfiguration](assets/translation-configuration-location.png)

1. Ange följande information i fälten och klicka eller tryck sedan på **Skapa**.
   1. Välj **Konfigurationstyp** i listrutan. Välj **Översättningsintegrering** i listan.
   1. Ange en **titel** för din konfiguration. **Titel** identifierar konfigurationen i **Cloud Servicens**-konsolen samt i listrutan för sidegenskaper.
   1. Du kan också skriva ett **namn** som ska användas för databasnoden som lagrar konfigurationen.

   ![Skapa översättningskonfiguration](assets/create-translation-configuration.png)

1. Tryck eller klicka på **Skapa** så visas fönstret **Redigera konfiguration** där du kan konfigurera konfigurationsegenskaperna.

1. Kom ihåg att innehållsfragment lagras som resurser i AEM. Tryck eller klicka på fliken **Resurser**.

![Egenskaper för översättningskonfiguration](assets/translation-configuration.png)

1. Ange följande information.

   1. **Översättningsmetod**  - Välj  **maskinöversättning** eller  **mänsklig** översättning beroende på översättningsleverantör. För den här resan antar vi maskinöversättning.
   1. **Översättningsproviders**  - Välj den koppling du installerade för översättningstjänsten i listan.
   1. **Innehållskategori**  - Välj den kategori som passar bäst för översättningen (endast för maskinöversättning).
   1. **Översätt resurser**  för innehållsfragment - Markera det här alternativet om du vill översätta resurser som är kopplade till innehållsfragment.
   1. **Översätt resurser**  - Markera detta för att översätta resurserna.
   1. **Översätt metadata**  - Markera detta om du vill översätta metadata för resurser.
   1. **Översätt taggar**  - Markera det här alternativet om du vill översätta taggar som är kopplade till resursen.
   1. **Automatisk översättning**  - Markera den här egenskapen om du vill att översättningar ska skickas automatiskt till översättningstjänsten.

1. Tryck eller klicka på **Spara och stäng**.

Du har nu konfigurerat kopplingen till översättningstjänsten.

## Associera konfigurationen med ditt innehåll {#associate}

AEM är ett flexibelt och kraftfullt verktyg som stöder flera samtidiga översättningstjänster via flera anslutningar och flera konfigurationer. Att konfigurera en sådan konfiguration ligger utanför den här kundresan. Den här flexibiliteten innebär dock att du måste ange vilka anslutningar och konfigurationer som ska användas för att översätta innehållet genom att koppla den här konfigurationen till innehållet.

Det gör du genom att navigera till innehållets språkrot. I våra exempel är detta

```text
/content/dam/<your-project>/en
```

1. Gå till den globala navigeringen och gå till **Navigering** -> **Resurser** -> **Filer**.
1. I resurskonsolen väljer du den språkrot som ska konfigureras och klickar eller trycker på **Egenskaper**.
1. Tryck eller klicka på fliken **Cloud Services**.
1. Under **Cloud Service Configurations** i listrutan **Lägg till konfiguration** väljer du din koppling. Den ska visas i listrutan när du har installerat paketet som [beskrivet tidigare.](#connect-translation-provider)
1. Under **Cloud Service Configurations** i listrutan **Lägg till konfiguration** väljer du även din konfiguration.
1. Tryck eller klicka på **Spara och stäng**.

![Välj molntjänstkonfigurationer](assets/select-cloud-service-configurations.png)

## What&#39;s Next {#what-is-next}

Nu när du är klar med den här delen av den headless översättningsresan ska du:

* Förstå de viktiga parametrarna i översättningsintegreringsramverket i AEM.
* Du kan skapa en egen anslutning till översättningstjänsten.

Bygg vidare på den här kunskapen och fortsätt din AEM översättningsresa genom att gå igenom dokumentet [Konfigurera översättningsregler](translation-rules.md) där du får lära dig hur du definierar vilket innehåll som ska översättas.

## Ytterligare resurser {#additional-resources}

Vi rekommenderar att du går vidare till nästa del av den headless-översättningsresan genom att granska dokumentet [Konfigurera översättningsregler](translation-rules.md). Följande är ytterligare, valfria resurser som gör en djupdykning i vissa koncept som nämns i det här dokumentet, men de behöver inte fortsätta den headless-resan.

* [Configuring the Translation Integration Framework](/help/sites-cloud/administering/translation/integration-framework.md)  - Granska en lista över valda översättningskopplingar och lär dig hur du konfigurerar översättningsintegreringsramverket för integrering med översättningstjänster från tredje part.
* [Ansluta till Microsoft Translator](/help/sites-cloud/administering/translation/connect-ms-translator.md) - AEM tillhandahåller ett Microsoft Translation-konto för testning.
