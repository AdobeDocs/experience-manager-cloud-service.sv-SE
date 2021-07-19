---
title: Konfigurera översättningskoppling
description: Lär dig hur du ansluter AEM till en översättningstjänst.
source-git-commit: 22ca7c01bfddb407c119de7d9a4d105941772664
workflow-type: tm+mt
source-wordcount: '1083'
ht-degree: 0%

---

# Konfigurera översättningskoppling {#configure-connector}

Lär dig hur du ansluter AEM till en översättningstjänst.

## Story hittills {#story-so-far}

I det tidigare dokumentet av den AEM headless-lokaliseringsresan [Kom igång med AEM headless-lokalisering](learn-about.md) lärde du dig att ordna ditt headless-innehåll och hur AEM lokaliseringsverktygen fungerar, och du bör nu:

* Förstå hur viktig innehållsstrukturen är för lokaliseringen.
* Förstå hur AEM lagrar headless-innehåll.
* Bekanta dig med AEM lokaliseringsverktyg.

Den här artikeln bygger på dessa grundläggande funktioner så att du kan ta det första konfigurationssteget och konfigurera en översättningstjänst som du sedan använder under resan för att översätta ditt innehåll.

## Syfte {#objective}

Det här dokumentet hjälper dig att förstå hur du konfigurerar en AEM till den översättningstjänst du valt. När du har läst bör du:

* Förstå de viktiga parametrarna i översättningsintegreringsramverket i AEM.
* Du kan skapa en egen anslutning till översättningstjänsten.

## Översättningsintegreringsramverket {#tif}

AEM Integrationsramverk för översättning kan integreras med översättningstjänster från tredje part för att samordna översättning av AEM. Det handlar om tre grundläggande steg.

1. Anslut till översättningstjänsten.
1. Skapa en konfiguration för Translation Integration Framework.
1. Koppla konfigurationen till ditt innehåll.

## Ansluta till en översättningstjänstleverantör {#connect-translation-provider}

Det första steget är att välja vilken översättningstjänst du vill använda. Det finns många alternativ för översättningstjänster för människor och datorer som är tillgängliga för AEM. Avsnittet [Ytterligare resurser](#additional-resources) innehåller ett urval av tillgängliga alternativ.

De flesta leverantörer kommer att erbjuda ett översättningspaket som ska installeras. För den här resan använder vi Microsoft Translator som AEM tillhandahåller en körklar testlicens. Mer information om den här providern finns i avsnittet [Ytterligare resurser](#additional-resources).

Om du väljer en annan leverantör måste du installera kopplingspaketet enligt översättningstjänstens instruktioner.

>[!NOTE]
>
>Om du använder den färdiga versionen av Microsoft Translator i AEM krävs ingen ytterligare konfiguration och fungerar som den ska utan ytterligare anslutningskonfiguration.
>
>Om du väljer att använda Microsoft Translator-anslutningen för testning behöver du inte utföra stegen i de två följande avsnitten, men du bör läsa dem så att du känner till när du behöver ansluta den anslutning du föredrar.
>
>Testversionen av Microsoft Translator Connector är inte avsedd för produktion och om du bestämmer dig för att licensiera den måste du följa de steg som beskrivs i [Additional Resources](#additional-resources) i slutet av det här dokumentet för att konfigurera licensen.

## Skapa en konfiguration för översättningsintegrering {#create-config}

Först måste du skapa en ramverkskonfiguration för översättningsintegrering som anger hur innehållet ska översättas. Konfigurationen innehåller följande information:

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

   1. **Översättningsmetod**  - Välj  **maskinöversättning** eller  **mänsklig** översättning beroende på översättningsleverantör. För den här resan ska vi anta maskinöversättning.
   1. **Översättningsproviders**  - Välj den koppling du installerade för översättningstjänsten i listan.
   1. **Innehållskategori**  - Välj den kategori som passar bäst för översättningen (endast för maskinöversättning).
   1. **Vill du översätta Content Fragment Assets**  - ????
   1. **Översätt resurser**  - Markera detta för att översätta resurserna.
   1. **Översätt metadata**  - Markera detta om du vill översätta metadata för resurser.
   1. **Översätt taggar**  - Markera det här alternativet om du vill översätta taggar som är kopplade till resursen.
   1. **Automatisk översättning**  - Markera den här egenskapen om du vill att översättningar ska skickas automatiskt till översättningstjänsten.

1. Tryck eller klicka på **Spara och stäng**.

Du har nu konfigurerat kopplingen till översättningstjänsten.

## Associera konfigurationen med ditt innehåll {#associate}

AEM är ett flexibelt och kraftfullt verktyg som stöder flera samtidiga översättningstjänster via flera anslutningar och flera konfigurationer. Att konfigurera detta ligger utanför räckvidden för den här resan, men innebär att du måste ange vilka kopplingar och konfigurationer som ska användas för att översätta ditt innehåll.

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

Nu när du är klar med den här delen av den headless lokaliseringsresan bör du:

* Förstå de viktiga parametrarna i översättningsintegreringsramverket i AEM.
* Du kan skapa en egen anslutning till översättningstjänsten.

Bygg vidare på den här kunskapen och fortsätt din AEM vanliga lokaliseringsresa genom att nästa gång du granskar dokumentet [Konfigurera översättningsregler](translation-rules.md) där du får lära dig hur du definierar vilket innehåll som ska översättas.

## Ytterligare resurser {#additional-resources}

Vi rekommenderar att du går vidare till nästa del av den headless-baserade lokaliseringsresan genom att granska dokumentet [Konfigurera översättningsregler](translation-rules.md). Följande är ytterligare, valfria resurser som gör en djupdykning i vissa koncept som nämns i det här dokumentet, men de behöver inte fortsätta den headless-resan.

* [Configuring the Translation Integration Framework](/help/sites-cloud/administering/translation/integration-framework.md)  - Lär dig hur du konfigurerar översättningsintegreringsramverket för integrering med översättningstjänster från tredje part.
* [Ansluta till Microsoft Translator](/help/sites-cloud/administering/translation/connect-ms-translator.md) - AEM tillhandahåller ett Microsoft Translation-konto för testning.
