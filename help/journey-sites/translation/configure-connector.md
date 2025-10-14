---
title: Konfigurera Translation Connector (AEM Sites)
description: Lär dig hur du ansluter AEM till en översättningstjänst.
index: true
hide: false
hidefromtoc: false
exl-id: d1a3eb42-e9e4-4118-9ff7-7aab5519cf0d
solution: Experience Manager Sites
feature: Translation
role: Admin
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 0%

---

# Konfigurera översättningsanslutningen {#configure-connector}

Lär dig hur du ansluter AEM till en översättningstjänst.

## Story hittills {#story-so-far}

I det tidigare dokumentet om översättningsresan för AEM Sites [Kom igång med AEM Sites &#x200B;](learn-about.md) lärde du dig att ordna ditt innehåll och hur AEM översättningsverktyg fungerar, och du bör nu:

* Förstå hur viktig innehållsstrukturen är för översättning.
* Förstå hur AEM lagrar innehåll.
* Bekanta dig med AEM översättningsverktyg.

Den här artikeln bygger på dessa grundläggande funktioner så att du kan ta det första konfigurationssteget och konfigurera en översättningstjänst som du sedan använder under resan för att översätta ditt innehåll.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur du konfigurerar en AEM till den översättningstjänst du valt. När du har läst bör du:

* Förstå de viktiga parametrarna i översättningsintegreringsramverket i AEM.
* Du kan skapa en egen anslutning till översättningstjänsten.

## Översättningsintegreringsramverket {#tif}

AEM Translation Integration Framework (TIF) kan integreras med översättningstjänster från tredje part för att samordna översättning av AEM. Det handlar om tre grundläggande steg.

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
>Om du använder den färdiga Microsoft Translator i AEM behöver du inte göra ytterligare inställningar och fungerar som det ska utan ytterligare anslutningskonfiguration.
>
>Om du väljer att använda Microsoft Translator-kopplingen för testning behöver du inte utföra stegen i de följande två avsnitten: [Skapa en konfiguration för översättningsintegrering](#create-config) och [Koppla konfigurationen till ditt innehåll](#associate). Du bör dock läsa dem så att du vet hur du gör när du behöver konfigurera den önskade anslutningen.
>
>Testversionen av Microsoft Translator Connector är inte avsedd för produktion och om du bestämmer dig för att licensiera den måste systemadministratören följa stegen som beskrivs i avsnittet [Ytterligare resurser](#additional-resources) i slutet av det här dokumentet för att konfigurera licensen.

## Skapa en konfiguration för översättningsintegrering {#create-config}

När kopplingspaketet för den översättningstjänst du föredrar har installerats måste du skapa en konfiguration för översättningsintegreringsramverket för den tjänsten. Konfigurationen innehåller följande information:

* Vilken översättningstjänstleverantör som ska användas
* Om översättning till människa eller dator ska utföras
* Om annat innehåll som är associerat med sidorna ska översättas, till exempel taggar

Så här skapar du en översättningskonfiguration:

1. På den globala navigeringsmenyn väljer du **Verktyg** > **Cloud Service** > **Cloud Service för översättning**.
1. Navigera till den plats där du vill skapa konfigurationen i innehållsstrukturen. Detta baseras ofta på ett visst projekt eller kan vara globalt.
   * I det här fallet kan till exempel en konfiguration göras globalt för att gälla allt innehåll, eller bara för WKND-projektet.

   ![Plats för översättningskonfiguration](assets/translation-configuration-location.png)

1. Välj **Skapa** i verktygsfältet för att skapa den nya konfigurationen.
1. Ange följande information i fälten och välj sedan **Skapa**.
   1. Välj **Konfigurationstyp** i listrutan. Välj **Översättningsintegrering** i listan.
   1. Ange en **titel** för din konfiguration. **Titel** identifierar konfigurationen i **Cloud Services**-konsolen och i listrutan för sidegenskaper.
   1. Du kan också ange ett **namn** som ska användas för databasnoden som lagrar konfigurationen.

   ![Skapa översättningskonfiguration](assets/create-translation-configuration.png)

1. Välj **Skapa** så visas fönstret **Redigera konfiguration** där du kan konfigurera konfigurationsegenskaperna.

1. Eftersom ditt innehåll hanteras som webbplatser väljer du fliken **Platser**.

![Konfigurationsegenskaper för översättning](assets/translation-configuration.png)

1. Ange följande information.

   1. **Översättningsmetod** - Välj **Maskinöversättning** eller **mänsklig översättning** beroende på översättningsleverantör. För den här resan antar vi maskinöversättning.
   1. **Översättningsproviders** - Välj den koppling du installerade för översättningstjänsten i listan.
   1. **Innehållskategori** - Välj den kategori som passar bäst för översättningen (endast för maskinöversättning).
   1. **Översätt sida Assets** - Välj **Använda arbetsflöde för översättning av webbplatser** för att översätta resurser som är associerade med webbplatssidorna.
   1. **Översätt komponentsträngar** - Markera detta om du vill översätta komponentinformation.
   1. **Översätt taggar** - Markera det här alternativet om du vill översätta taggar som är kopplade till sidan.
   1. **Automatisk översättning** - Markera den här egenskapen om du vill att översättningar ska skickas automatiskt till översättningstjänsten.

1. Välj **Spara och stäng**.

Du har nu konfigurerat kopplingen till översättningstjänsten.

## Associera konfigurationen med ditt innehåll {#associate}

AEM är ett flexibelt och kraftfullt verktyg som stöder flera samtidiga översättningstjänster via flera anslutningar och flera konfigurationer. Att konfigurera en sådan konfiguration ligger utanför den här kundresan. Den här flexibiliteten innebär dock att du måste ange vilka anslutningar och konfigurationer som ska användas för att översätta innehållet genom att koppla den här konfigurationen till innehållet.

Det gör du genom att navigera till innehållets språkrot. I våra exempel är detta

```text
/content/<your-project>/en
```

1. Gå till den globala navigeringen och gå till **Navigering** > **Assets** > **Filer**.
1. I resurskonsolen väljer du den språkrot som ska konfigureras och väljer **Egenskaper**.
1. Markera fliken **Cloud Service**.
1. Välj din koppling under **Konfigurationskonfigurationer** i listrutan **Lägg till Cloud Service**. Den ska visas i listrutan när du har installerat paketet som [beskrivet tidigare](#connect-translation-provider).
1. Under **Konfigurationskonfigurationer** i listrutan **Lägg till Cloud Service** väljer du även din konfiguration.
1. Välj **Spara och stäng**.

![Välj molntjänstkonfigurationer](assets/select-cloud-service-configurations.png)

## What&#39;s Next {#what-is-next}

Nu när du är klar med den här delen av AEM Sites översättningsresa ska du:

* Förstå de viktiga parametrarna i översättningsintegreringsramverket i AEM.
* Du kan skapa en egen anslutning till översättningstjänsten.

Bygg vidare på den här kunskapen och fortsätt din översättning till AEM Sites genom att gå igenom dokumentet [Konfigurera översättningsregler](translation-rules.md), där du får lära dig hur du definierar vilket innehåll som ska översättas.

## Ytterligare resurser {#additional-resources}

Vi rekommenderar att du går vidare till nästa del av översättningsresan genom att granska dokumentet [Konfigurera översättningsregler](translation-rules.md), men följande är ytterligare, valfria resurser som gör en djupdykning i vissa koncept som nämns i det här dokumentet, men de behöver inte fortsätta på resan.

* [Konfigurerar översättningsintegreringsramverket](/help/sites-cloud/administering/translation/integration-framework.md) - Granska en lista över valda översättningsanslutningar och lär dig hur du konfigurerar översättningsintegreringsramverket så att det integreras med översättningstjänster från tredje part.
* [Ansluter till Microsoft Translator](/help/sites-cloud/administering/translation/connect-ms-translator.md) - AEM tillhandahåller en testversion av Microsoft Translation-kontot för testning.
