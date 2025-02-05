---
title: Konfigurera översättningsintegreringsramverket
description: Lär dig hur du konfigurerar TLF (Translation Integration Framework) för integrering med översättningstjänster från tredje part.
feature: Language Copy
role: Admin
exl-id: 6e74cdee-7965-4087-a733-e9d81c4aa7c2
solution: Experience Manager Sites
source-git-commit: 10580c1b045c86d76ab2b871ca3c0b7de6683044
workflow-type: tm+mt
source-wordcount: '1447'
ht-degree: 0%

---

# Konfigurera översättningsintegreringsramverket {#configuring-the-translation-integration-framework}

Översättningsintegreringsramverket integreras med översättningstjänster från tredje part för att samordna översättningen av AEM. Det handlar om tre grundläggande steg.

1. [Anslut till översättningstjänsten](#connecting-to-a-translation-service-provider).
1. [Skapa en konfiguration för översättningsintegreringsramverket](#creating-a-translation-integration-configuration).
1. [Associera molnkonfigurationerna med dina sidor](#configuring-pages-for-translation).

En översikt över funktionerna för översättning av innehåll i AEM finns i [Översätta innehåll för flerspråkiga platser](overview.md).

>[!TIP]
>
>Om du inte är van vid att översätta innehåll läser du [Platsöversättningsresa](/help/journey-sites/translation/overview.md), som är en guidad väg genom att översätta ditt AEM Sites-innehåll med hjälp av AEM kraftfulla översättningsverktyg, som är idealisk för dem som saknar AEM eller översättningsupplevelse.

## Ansluta till en översättningstjänstleverantör {#connecting-to-a-translation-service-provider}

Skapa en molnkonfiguration som ansluter AEM till översättningstjänstleverantören.

AEM innehåller möjligheten att [ansluta till Microsoft® Translator](connect-ms-translator.md) som standard. Andra översättningsteknikleverantörer med AEM anslutningar som är medlemmar i partnerprogrammet för Adobe Exchange finns [här](https://exchange.adobe.com/apps/browse/ec?page=1&amp;partnerLevel=All&amp;product=AEM&amp;q=experience+manager+translation&amp;sort=RELEVANCE).

När du har installerat ett kopplingspaket kan du skapa en molnkonfiguration för anslutningen. Vanligtvis måste du ange dina autentiseringsuppgifter för autentisering med översättningstjänsten. Mer information om hur du lägger till en molnkonfiguration för Microsoft® Translator-anslutningen finns i [Integrera med Microsoft® Translator](connect-ms-translator.md).

Du kan skapa flera molnkonfigurationer för samma anslutning om det behövs. Skapa till exempel en konfiguration för varje konto eller projekt som du har med samma leverantör.

När du har konfigurerat en anslutning kan du skapa den konfiguration av översättningsintegreringsramverket som använder den.

## Skapa en konfiguration för översättningsintegrering {#creating-a-translation-integration-configuration}

Skapa en ramverkskonfiguration för översättningsintegrering så att du kan ange hur innehållet ska översättas. Konfigurationen innehåller följande information:

* Vilken översättningstjänstleverantör som ska användas
* Om översättning till människa eller dator ska utföras
* Om annat innehåll som är associerat med en sida eller resurs ska översättas, till exempel taggar

När du har skapat en ramverkskonfiguration associerar du molnkonfigurationen med de sidor som du vill översätta enligt konfigurationen. När översättningsprocessen startas fortsätter översättningsarbetsflödet enligt den associerade ramverkskonfigurationen.

Om olika delar av webbplatsen har olika översättningskrav skapar du flera ramverkskonfigurationer utifrån detta. En flerspråkig webbplats kan t.ex. innehålla engelska, spanska och japanska språkkopior. Webbplatsägaren använder två olika översättningstjänstleverantörer för spanska och japanska översättningar. Därför är två konfigurationer av ramverket konfigurerade. Varje konfiguration använder en annan översättningstjänstleverantör.

När du har konfigurerat ett ramverk för översättningsintegrering kan du [associera det med sidorna](preparation.md) som använder det.

>[!TIP]
>
>En översikt över funktionerna för översättning av innehåll i AEM finns i [Översätta innehåll för flerspråkiga platser](overview.md).

En enda konfiguration av ramverket styr hur sidinnehåll och resurser översätts. Så här skapar du en översättningskonfiguration:

1. På den [globala navigeringsmenyn](/help/sites-cloud/authoring/basic-handling.md#global-navigation) väljer du **Verktyg > Cloud Service och översättningsmeny**.
1. Navigera till den plats där du vill skapa konfigurationen i innehållsstrukturen. Detta baseras ofta på en viss webbplats eller kan vara globalt.
1. Ange följande information i fälten och välj sedan **Skapa**:
   1. Välj **Konfigurationstyp** i listrutan.
   1. Ange en **titel** för din konfiguration. **Titel** identifierar konfigurationen i **Cloud Services**-konsolen och i listrutan för sidegenskaper.
   1. Du kan också ange ett **namn** som ska användas för databasnoden som lagrar konfigurationen.
1. Konfigurera egenskaperna på flikarna **Platser** och **Assets** i fönstret **Redigera konfiguration** och välj sedan **Spara och stäng**.

### Egenskaper för platskonfiguration {#sites-configuration-properties}

Fliken **Platser** styr hur översättning av sidinnehåll utförs.

![Översättningskonfiguration för platser](../assets/translation-configuration.png)

| Egenskap | Beskrivning |
|---|---|
| Översättningsmetod | Den här egenskapen definierar översättningsmetoden som utförs i ramverket för webbplatsinnehåll:<br>- Maskinöversättning: Översättningsprovidern utför översättningen med maskinöversättning i realtid.<br> - Personlig översättning: Innehållet skickas till översättningsleverantören för översättning av översättare.<br>- Översätt inte: Innehållet skickas inte för översättning. Detta är för att hoppa över vissa innehållsgrenar som inte skulle översättas, men som skulle kunna uppdateras med det senaste innehållet. |
| Översättningsprovider | This property define the translation provider to perform the translation. En provider visas i listan när dess motsvarande koppling är installerad. |
| Innehållskategori | (Endast maskinöversättning) Den här egenskapen är en kategori som beskriver innehållet som du översätter. Kategorin kan påverka valet av terminologi och fraser när innehåll översätts. |
| Översätt taggar | Det här alternativet aktiverar översättning av taggar som är kopplade till sidan. |
| Översätt sida Assets | Den här egenskapen definierar hur resurser som har lagts till i komponenter från filsystemet eller som refereras från resurser: <br>- Översätt inte: Sidresurser översätts inte.<br> - Använda arbetsflöde för översättning av webbplatser: Assets hanteras enligt konfigurationsegenskaperna på fliken **Platser**.<br> - Använda arbetsflöde för översättning av resurser: Assets hanteras enligt de egenskaper som konfigurerats på fliken **Assets** . |
| Automatisk översättning | Aktivera den här egenskapen för att köra översättningsjobb automatiskt efter att översättningsprojekt har skapats. Du har inte möjlighet att granska och omsluta översättningsjobbet när du väljer det här alternativet. |
| Inaktivera översättning med endast uppdatering | När det här alternativet är markerat skickas alla översättningsbara fält för översättning när översättningsprojektet uppdateras, inte bara de som ändrats sedan den senaste översättningen. |

### Egenskaper för Assets-konfiguration {#assets-configuration-properties}

Assets-egenskaper styr hur resurser konfigureras. Mer information om översättning av resurser finns i [Skapa språkkopior för Assets](/help/assets/translate-assets.md).

![Översättningskonfiguration för platser](../assets/translation-configuration-assets.png)

| Egenskap | Beskrivning |
|---|---|
| Översättningsmetod | Den här egenskapen väljer typen av översättning som ramverket utför för resurserna:<br>- Maskinöversättning: Översättningsprovidern utför översättningen omedelbart med maskinöversättning.<br> - Personlig översättning: Innehållet skickas automatiskt till översättningsleverantören för manuell översättning.<br>-Översätt inte: Assets skickas inte för översättning. |
| Översättningsprovider | This property define the translation provider to perform the translation. En provider visas i listan när dess motsvarande koppling är installerad. |
| Innehållskategori | (Endast maskinöversättning) Den här egenskapen beskriver innehållet som du översätter. Kategorin kan påverka valet av terminologi och fraser när innehåll översätts. |
| Översätt Assets | Aktivera den här egenskapen för att inkludera resurser i översättningsprojektet. |
| Översätt metadata | Aktivera den här egenskapen så att du kan översätta metadata för resursen. |
| Översätt taggar | Aktivera den här egenskapen så att du kan översätta taggar som är kopplade till resursen. |
| Automatisk översättning | Välj den här egenskapen så att du kan köra översättningsjobb automatiskt efter att översättningsprojekt har skapats. Du har inte möjlighet att granska eller omsluta översättningsjobbet när du väljer det här alternativet. |
| Inaktivera översättning med endast uppdatering | När det här alternativet är markerat skickas alla översättningsbara fält för översättning när översättningsprojektet uppdateras, inte bara de som ändrats sedan den senaste översättningen. |
| Aktivera fält för innehållsmodell för översättning | Om du aktiverar det här alternativet används fältet **Översättningsbar** i [modeller för innehållsfragment](/help/sites-cloud/administering/content-fragments/content-fragment-models.md#properties) för att avgöra om fältet är översatt och [översättningsregler](rules.md) skapas automatiskt. Det här alternativet ersätter eventuella översättningsregler som du har skapat. |

## Konfigurera sidor för översättning {#configuring-pages-for-translation}

Om du vill konfigurera översättning av källsidor till andra språk associerar du sidorna med följande molnkonfigurationer:

* Den molnkonfiguration som ansluter AEM till översättningsleverantören.
* Översättningsintegrationsramverket som konfigurerar informationen för översättningen.

Konfigurationen av översättningsintegreringsramverket i molnet identifierar den molnkonfiguration som ska användas för att ansluta till tjänstleverantören. När du associerar en källsida med en ramverkets molnkonfiguration måste sidan associeras med tjänstleverantörens molnkonfiguration som används i ramverkets molnkonfiguration.

När du associerar en sida med en molnkonfiguration ärver de underordnade sidorna kopplingen. Om du till exempel har kopplat sidan `/content/wknd/language-masters/en/magazine` till ett Translation Integration Framework, översätts sidan `magazine` och underordnade sidor nedanför den enligt ramverket.

Vid behov kan du åsidosätta associationen på en underordnad sida. Innehållet på en webbplats handlar till exempel mest om resor och livsstil. En av sidorna beskriver dock företaget. I så fall kan platsens rotsida vara kopplad till ett Translation Integration Framework som anger maskinöversättning med kategorin Livsstil. Den gren som beskriver företaget använder ett ramverk som utför maskinöversättning med kategorin Allmänt.

### Koppla en sida till en översättningsleverantör {#associating-a-page-with-a-translation-provider}

Koppla en sida till översättningsleverantören som du använder för att översätta sidan och underordnade sidor.

1. På webbplatskonsolen markerar du sidan som ska konfigureras och väljer **Visa egenskaper**.
1. Markera fliken **Cloud Service**.
1. Välj konfigurationen i listrutan **Lägg till konfiguration**.
1. Välj **Spara och stäng**.

### Associera sidor med ett översättningsintegreringsramverk {#associating-pages-with-a-translation-integration-framework}

Koppla en sida till översättningsintegreringsramverket som definierar hur du vill översätta sidan och underordnade sidor.

1. På webbplatskonsolen markerar du sidan som ska konfigureras och väljer **Visa egenskaper**.
1. Markera fliken **Cloud Service**.
1. Välj konfigurationen i listrutan **Lägg till konfiguration**.
1. Välj **Spara och stäng**.
