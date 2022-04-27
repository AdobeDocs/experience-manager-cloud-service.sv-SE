---
title: Konfigurera översättningsintegreringsramverket
description: Lär dig hur du konfigurerar TLF (Translation Integration Framework) för integrering med översättningstjänster från tredje part.
feature: Language Copy
role: Admin
exl-id: 6e74cdee-7965-4087-a733-e9d81c4aa7c2
source-git-commit: 3c37b66b63ed19635854cf277aaf7d5f2a7c1fe8
workflow-type: tm+mt
source-wordcount: '1522'
ht-degree: 0%

---

# Konfigurera översättningsintegreringsramverket {#configuring-the-translation-integration-framework}

Översättningsintegreringsramverket integreras med översättningstjänster från tredje part för att samordna översättningen av AEM. Det handlar om tre grundläggande steg.

1. [Anslut till översättningstjänsten.](#connecting-to-a-translation-service-provider)
1. [Skapa en konfiguration för Translation Integration Framework.](#creating-a-translation-integration-configuration)
1. [Associera molnkonfigurationerna med sidorna.](#configuring-pages-for-translation)

En översikt över funktionerna för innehållsöversättning i AEM finns på [Översätta innehåll för flerspråkiga webbplatser](overview.md).

>[!TIP]
>
>Om du är nybörjare på att översätta innehåll kan du läsa [Sites Translation Journey,](/help/journey-sites/translation/overview.md) som vägleder dig genom att översätta ditt AEM Sites-innehåll med AEM kraftfulla översättningsverktyg, idealiskt för dem som saknar AEM eller översättningsupplevelse.

## Ansluta till en översättningstjänstleverantör {#connecting-to-a-translation-service-provider}

Skapa en molnkonfiguration som ansluter AEM till översättningstjänstleverantören. AEM kan [ansluta till Microsoft Translator](connect-ms-translator.md) som standard.

Följande översättningsleverantörer tillhandahåller en implementering av AEM API för översättningsprojekt.

* [Microsoft Translator](connect-ms-translator.md)
* [Translations.com](https://exchange.adobe.com/experiencecloud.details.90104.globallink-connect-plus-for-aem.html) (Adobe Exchange Premier Partner)
* [Clay Tablet Technologies](https://exchange.adobe.com/experiencecloud.details.90064.clay-tablet-translation-for-experience-manager.html)
* [Lionbridge](https://exchange.adobe.com/experiencecloud.details.100064.lionbridge-connector-for-experience-manager-63.html)
* [Memsource](https://exchange.adobe.com/experiencecloud.details.103166.memsource-connector-for-adobe-experience-manager.html)
* [Molnord](https://exchange.adobe.com/experiencecloud.details.90019.html)
* [XTM Cloud](https://exchange.adobe.com/experiencecloud.details.105037.xtm-connect-for-adobe-experience-manager.html)
* [Lingotek](https://exchange.adobe.com/experiencecloud.details.90088.lingotek-collaborative-translation-platform.html)
* [RWS](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108277.html)
* [Smartling](https://exchange.adobe.com/experiencecloud.details.90101.smartling-connector-for-adobe-experience-manager.html)
* [Systran](https://exchange.adobe.com/experiencecloud.details.90233.systran-for-adobe-experience-manager.html)

När du har installerat ett anslutningspaket kan du skapa en molnkonfiguration för anslutaren. Vanligtvis måste du ange dina autentiseringsuppgifter för autentisering med översättningstjänsten. Mer information om hur du lägger till en molnkonfiguration för Microsoft Translator-anslutningen finns i [Integrera med Microsoft Translator](connect-ms-translator.md).

Du kan skapa flera molnkonfigurationer för samma anslutning om det behövs. Skapa till exempel en konfiguration för varje konto eller projekt som du har med samma leverantör.

När du har konfigurerat en anslutning kan du skapa den konfiguration av översättningsintegreringsramverket som använder den.

## Skapa en konfiguration för översättningsintegrering {#creating-a-translation-integration-configuration}

Skapa en konfiguration för ramverk för översättningsintegrering som anger hur ditt innehåll ska översättas. Konfigurationen innehåller följande information:

* Vilken översättningstjänstleverantör som ska användas
* Om översättning till människa eller dator ska utföras
* Om annat innehåll som är associerat med en sida eller resurs ska översättas, till exempel taggar

När du har skapat en ramverkskonfiguration associerar du molnkonfigurationen med de sidor som du vill översätta enligt konfigurationen. När översättningsprocessen startas fortsätter översättningsarbetsflödet enligt den associerade ramverkskonfigurationen.

Om olika delar av webbplatsen har olika översättningskrav skapar du flera ramverkskonfigurationer utifrån detta. En flerspråkig webbplats kan till exempel innehålla engelska, spanska och japanska språkkopior. Webbplatsägaren använder två olika översättningstjänstleverantörer för spanska och japanska översättningar. Därför är två konfigurationer av ramverket konfigurerade. Varje konfiguration använder en annan översättningstjänstleverantör.

När du har konfigurerat ett ramverk för översättningsintegrering kan du [associera den med sidorna](preparation.md) som använder den.

>[!TIP]
>
>En översikt över funktionerna för innehållsöversättning i AEM finns på [Översätta innehåll för flerspråkiga webbplatser](overview.md).

En enda konfiguration av ramverket styr hur sidinnehåll och resurser översätts. Så här skapar du en ny översättningskonfiguration:

1. I [global navigeringsmeny,](/help/sites-cloud/authoring/getting-started/basic-handling.md#global-navigation) klicka eller trycka **Verktyg -> Cloud Services - och översättnings-Cloud Services**.
1. Navigera till den plats där du vill skapa konfigurationen i innehållsstrukturen. Detta baseras ofta på en viss webbplats eller kan vara globalt.
1. Ange följande information i fälten och klicka eller tryck sedan på **Skapa**.:
   1. Välj **Konfigurationstyp** i listrutan.
   1. Ange **Titel** för din konfiguration. The **Titel** identifierar konfigurationen i **Cloud Services** Console samt i listrutor för sidegenskaper.
   1. Du kan även skriva en **Namn** som ska användas för den databasnod som lagrar konfigurationen.
1. I **Redigera konfiguration** fönster, konfigurera egenskaperna för **Webbplatser** och **Resurser** och sedan klicka eller trycka på **Spara och stäng**.

### Egenskaper för platskonfiguration {#sites-configuration-properties}

The **Webbplatser** -fliken styr hur sidinnehållet ska översättas.

![Översättningskonfiguration för platser](../assets/translation-configuration.png)

| Egenskap | Beskrivning |
|---|---|
| Översättningsmetod | Den här egenskapen definierar den översättningsmetod som ramverket utför för webbplatsinnehåll:<br>- Maskinöversättning: Översättningsprovidern utför översättningen med maskinöversättning i realtid.<br>- mänsklig översättning: Innehållet skickas till översättningsleverantören för översättning av översättare.<br>- Översätt inte: Innehåll skickas inte för översättning. Detta är för att hoppa över vissa innehållsgrenar som inte skulle översättas, men som skulle kunna uppdateras med det senaste innehållet. |
| Översättningsprovider | This property define the translation provider to perform the translation. En provider visas i listan när dess motsvarande koppling är installerad. |
| Innehållskategori | (Endast maskinöversättning) Den här egenskapen är en kategori som beskriver innehållet som du översätter. Kategorin kan påverka valet av terminologi och fraser när innehåll översätts. |
| Översätt taggar | Det här alternativet aktiverar översättning av taggar som är kopplade till sidan. |
| Översätt sidresurser | Den här egenskapen definierar hur resurser som läggs till i komponenter från filsystemet eller som refereras från resurser ska översättas:<br>- Översätt inte: Sidresurser översätts inte.<br>- Använda arbetsflöde för översättning av webbplatser: Resurserna hanteras enligt konfigurationsegenskaperna i **Webbplatser** -fliken.<br>- Använda arbetsflöde för översättning av resurser: Resurserna hanteras enligt de egenskaper som konfigurerats på **Resurser** -fliken. |
| Automatisk översättning | Aktivera den här egenskapen för att köra översättningsjobb automatiskt efter att översättningsprojekt har skapats. Du har inte möjlighet att granska och omsluta översättningsjobbet när du väljer det här alternativet. |
| Inaktivera översättning med endast uppdatering | När det här alternativet är markerat skickas alla översättningsbara fält för översättning när översättningsprojektet uppdateras, inte bara de som ändrats sedan den senaste översättningen. |

### Egenskaper för resurskonfiguration {#assets-configuration-properties}

Resursegenskaperna styr hur resurser konfigureras. Mer information om översättning av resurser finns i [Skapa språkkopior för resurser](/help/assets/translate-assets.md).

![Översättningskonfiguration för platser](../assets/translation-configuration-assets.png)

| Egenskap | Beskrivning |
|---|---|
| Översättningsmetod | Den här egenskapen väljer typen av översättning som ramverket utför för resurser:<br>- Maskinöversättning: Översättningsprovidern utför översättningen omedelbart med maskinöversättning.<br>- mänsklig översättning: Innehållet skickas automatiskt till översättningsleverantören för manuell översättning.<br>-Do Not Translate: Resurser skickas inte för översättning. |
| Översättningsprovider | This property define the translation provider to perform the translation. En provider visas i listan när dess motsvarande koppling är installerad. |
| Innehållskategori | (Endast maskinöversättning) Den här egenskapen beskriver innehållet som du översätter. Kategorin kan påverka valet av terminologi och fraser när innehåll översätts. |
| Översätt resurser | Aktivera den här egenskapen för att inkludera resurser i översättningsprojektet. |
| Översätt metadata | Aktivera den här egenskapen för att översätta metadata för resurser. |
| Översätt taggar | Aktivera den här egenskapen för att översätta taggar som är kopplade till resursen. |
| Automatisk översättning | Välj den här egenskapen om du vill köra översättningsjobb automatiskt efter att översättningsprojekt har skapats. Du har inte möjlighet att granska eller omsluta översättningsjobbet när du väljer det här alternativet. |
| Inaktivera översättning med endast uppdatering | När det här alternativet är markerat skickas alla översättningsbara fält för översättning när översättningsprojektet uppdateras, inte bara de som ändrats sedan den senaste översättningen. |
| Aktivera fält för innehållsmodell för översättning | Om du aktiverar det här alternativet används **Översättningsbar** fält på [Modeller för innehållsfragment](/help/assets/content-fragments/content-fragments-models.md#properties) för att avgöra om fältet är översatt och automatiskt skapar [översättningsregler](rules.md) i enlighet med detta. Det här alternativet ersätter eventuella översättningsregler som du har skapat. |

## Konfigurera sidor för översättning {#configuring-pages-for-translation}

Om du vill konfigurera översättning av källsidor till andra språk associerar du sidorna med följande molnkonfigurationer:

* Den molnkonfiguration som ansluter AEM till översättningsleverantören.
* Översättningsintegrationsramverket som konfigurerar informationen för översättningen.

Observera att molnkonfigurationen för översättningsintegreringsramverket identifierar den molnkonfiguration som ska användas för att ansluta till tjänstleverantören. När du associerar en källsida med en ramverkets molnkonfiguration måste sidan associeras med tjänstleverantörens molnkonfiguration som används i ramverkets molnkonfiguration.

När du associerar en sida med en molnkonfiguration ärver de underordnade sidorna kopplingen. Om du till exempel associerar `/content/wknd/language-masters/en/magazine` sida med ett Translation Integration Framework, `magazine` sidor och underordnade sidor under den översätts enligt ramverket.

Vid behov kan du åsidosätta associationen på en underordnad sida. Innehållet på en webbplats handlar till exempel mest om resor och livsstil. En av sidorna beskriver dock företaget. I så fall kan webbplatsens rotsida vara kopplad till ett Translation Integration Framework som anger maskinöversättning med kategorin Livsstil, medan den gren som beskriver företaget använder ett ramverk som utför maskinöversättning med kategorin Allmänt.

### Koppla en sida till en översättningsleverantör {#associating-a-page-with-a-translation-provider}

Koppla en sida till översättningsleverantören som du använder för att översätta sidan och underordnade sidor.

1. I webbplatskonsolen väljer du den sida som ska konfigureras och klickar på eller trycker **Visa egenskaper**.
1. Klicka eller tryck på **Cloud Services** -fliken.
1. I **Lägg till konfiguration** väljer du konfigurationen.
1. Klicka eller tryck **Spara och stäng**.

### Associera sidor med ett översättningsintegreringsramverk {#associating-pages-with-a-translation-integration-framework}

Koppla en sida till översättningsintegreringsramverket som definierar hur du vill översätta sidan och underordnade sidor.

1. I webbplatskonsolen väljer du den sida som ska konfigureras och klickar på eller trycker **Visa egenskaper**.
1. Klicka eller tryck på **Cloud Services** -fliken.
1. I **Lägg till konfiguration** väljer du konfigurationen.
1. Klicka eller tryck **Spara och stäng**.
