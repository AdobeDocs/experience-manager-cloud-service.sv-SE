---
title: Konfigurera Translation Connector (AEM Sites)
description: Lär dig hur du ansluter AEM till en översättningstjänst.
index: true
hide: false
hidefromtoc: false
exl-id: d1a3eb42-e9e4-4118-9ff7-7aab5519cf0d
source-git-commit: bc3c054e781789aa2a2b94f77b0616caec15e2ff
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 0%

---

# Konfigurera översättningsanslutningen {#configure-connector}

Lär dig hur du ansluter AEM till en översättningstjänst.

## Story hittills {#story-so-far}

I det föregående dokumentet om AEM Sites översättningsresa [Kom igång med AEM Sites translation](learn-about.md) du lärde dig att ordna ditt innehåll och hur AEM översättningsverktyg fungerar, och du bör nu:

* Förstå hur viktig innehållsstrukturen är för översättning.
* Förstå hur AEM lagrar innehåll.
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

Det första steget är att välja vilken översättningstjänst du vill använda. Det finns många alternativ för översättningstjänster för människor och datorer som är tillgängliga för AEM. De flesta leverantörer erbjuder ett översättningspaket som ska installeras. Se [Ytterligare resurser](#additional-resources) för ett urval av tillgängliga alternativ.

>[!NOTE]
>
>Översättningsexperten ansvarar vanligtvis för att välja vilken översättningstjänst som ska användas, men administratören ansvarar vanligtvis för att installera det nödvändiga översättningsanslutningspaketet.

För den här resan använder vi Microsoft Translator som AEM tillhandahåller en körklar testlicens. Se [Ytterligare resurser](#additional-resources) för mer information om den här providern.

Om du väljer en annan provider måste administratören installera kopplingspaketet enligt översättningstjänstens instruktioner.

>[!NOTE]
>
>Om du använder den färdiga Microsoft Translator i AEM behöver du inte göra ytterligare inställningar och fungerar som det ska utan ytterligare anslutningskonfiguration.
>
>Om du väljer att använda Microsoft Translator-anslutningen för testning behöver du inte utföra stegen i de följande två avsnitten: [Skapa en konfiguration för översättningsintegrering](#create-config) och [Associera konfigurationen med ditt innehåll.](#associate) Du bör dock läsa dem så att du vet hur du gör när du behöver konfigurera den önskade anslutningen.
>
>Testversionen av Microsoft Translator Connector är inte avsedd för produktion och om du bestämmer dig för att licensiera den måste systemadministratören följa stegen som beskrivs i [Ytterligare resurser](#additional-resources) i slutet av det här dokumentet för att konfigurera licensen.

## Skapa en konfiguration för översättningsintegrering {#create-config}

När kopplingspaketet för den översättningstjänst du föredrar har installerats måste du skapa en konfiguration för översättningsintegreringsramverket för den tjänsten. Konfigurationen innehåller följande information:

* Vilken översättningstjänstleverantör som ska användas
* Om översättning till människa eller dator ska utföras
* Om annat innehåll som är associerat med sidorna ska översättas, till exempel taggar

Så här skapar du en översättningskonfiguration:

1. Välj **verktyg** > **Cloud Service** > **Cloud Service för översättning**.
1. Navigera till den plats där du vill skapa konfigurationen i innehållsstrukturen. Detta baseras ofta på ett visst projekt eller kan vara globalt.
   * I det här fallet kan till exempel en konfiguration göras globalt för att gälla allt innehåll, eller bara för WKND-projektet.

   ![Plats för översättningskonfiguration](assets/translation-configuration-location.png)

1. Välj **Skapa** i verktygsfältet för att skapa den nya konfigurationen.
1. Ange följande information i fälten och välj sedan **Skapa**.
   1. Välj **Konfigurationstyp** i listrutan. Välj **Översättningsintegrering** från listan.
   1. Ange en **Titel** för din konfiguration. The **Titel** identifierar konfigurationen i **Cloud Service** console och in page property drop-down lists.
   1. Om du vill kan du skriva **Namn** som ska användas för den databasnod som lagrar konfigurationen.

   ![Skapa översättningskonfiguration](assets/create-translation-configuration.png)

1. Välj **Skapa** och **Redigera konfiguration** visas där du kan konfigurera konfigurationsegenskaperna.

1. Eftersom ditt innehåll hanteras som webbplatser väljer du **Webbplatser** -fliken.

![Egenskaper för översättningskonfiguration](assets/translation-configuration.png)

1. Ange följande information.

   1. **Översättningsmetod** - Välj **Maskinöversättning** eller **Översättning av människor** beroende på översättningsleverantör. För den här resan antar vi maskinöversättning.
   1. **Översättningsproviders** - Välj den koppling du har installerat för översättningstjänsten i listan.
   1. **Innehållskategori** - Välj den kategori som bäst passar översättningen (endast för maskinöversättning).
   1. **Översätt sidresurser** - Välj **Använda arbetsflöde för översättning av webbplatser** för att översätta resurser som är kopplade till webbplatssidorna.
   1. **Översätt komponentsträngar** - Markera det här alternativet om du vill översätta komponentinformation.
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

1. Gå till den globala navigeringen och gå till **Navigering** > **Resurser** > **Filer**.
1. I resurskonsolen väljer du den språkrot som ska konfigureras och väljer **Egenskaper**.
1. Välj **Cloud Service** -fliken.
1. Under **Cloud Service Configurations** i **Lägg till konfiguration** väljer du din koppling. Den bör visas i listrutan när du har installerat paketet som [som beskrivits tidigare.](#connect-translation-provider)
1. Under **Cloud Service Configurations** i **Lägg till konfiguration** väljer du konfiguration.
1. Välj **Spara och stäng**.

![Välj molntjänstkonfigurationer](assets/select-cloud-service-configurations.png)

## What&#39;s Next {#what-is-next}

Nu när du är klar med den här delen av AEM Sites översättningsresa ska du:

* Förstå de viktiga parametrarna i översättningsintegreringsramverket i AEM.
* Du kan skapa en egen anslutning till översättningstjänsten.

Bygg vidare på den här kunskapen och fortsätt din översättning till AEM Sites genom att granska nästa gång dokumentet [Konfigurera översättningsregler,](translation-rules.md) där du lär dig definiera vilket innehåll som ska översättas.

## Ytterligare resurser {#additional-resources}

Vi rekommenderar att du går vidare till nästa del av översättningsresan genom att granska dokumentet [Konfigurera översättningsregler](translation-rules.md) Nedan följer ytterligare, valfria resurser som fördjupar sig i några koncept som nämns i det här dokumentet, men som inte behöver fortsätta på resan.

* [Konfigurera översättningsintegreringsramverket](/help/sites-cloud/administering/translation/integration-framework.md) - Granska en lista över valda översättningskopplingar och lär dig hur du konfigurerar översättningsintegreringsramverket så att det integreras med översättningstjänster från tredje part.
* [Ansluta till Microsoft Translator](/help/sites-cloud/administering/translation/connect-ms-translator.md) - AEM tillhandahåller en testversion av Microsoft Translation-kontot för testning.
