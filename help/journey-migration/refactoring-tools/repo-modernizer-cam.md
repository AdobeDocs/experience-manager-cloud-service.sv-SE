---
title: Databasmodernisering (CAM)
description: Lär dig hur du strukturerar om befintliga projektpaket och gör dem kompatibla med den projektstruktur som har definierats för Adobe Experience Manager as a Cloud Service.
feature: Migration
role: Admin
source-git-commit: 317ee65786d48d7b92d95c7c6b8782f617d6e346
workflow-type: tm+mt
source-wordcount: '1099'
ht-degree: 0%

---


# Databasmodernisering (CAM) {#repo-modernizer-cam}

Databasmodernisering är ett verktyg som utvecklats för att strukturera om befintliga projektpaket genom att dela upp innehåll och kod i separata paket som är kompatibla med den projektstruktur som definierats för Adobe Experience Manager as a Cloud Service.

## Introduktion {#introduction}

Adobe Experience Manager as a Cloud Service har många nya funktioner och möjligheter i dina AEM-projekt. Det krävs dock vissa ändringar i Adobe Experience Manager Maven-projekt för att de ska vara kompatibla med AEM Cloud-tjänsten. På en hög nivå kräver AEM en separation av **content** och **code** i diskreta delpaket för att respektera delningen mellan muterbart och oföränderligt innehåll. Mer information om den nya AEM-projektstrukturen för Cloud Service finns i [AEM Project Structure](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developing/aem-project-content-package-structure.html).

Databasmoderniseringen skapar en kompatibel projektstruktur för AEM Cloud-tjänsten genom att skapa följande distributionsstruktur:

- Paketet `ui.apps` distribueras till `/apps` och innehåller all kod

- Paketet `ui.content` distribuerar till områden som kan skrivas under vid körning (till exempel `/content`, `/conf`, `/home` eller något annat som inte är `/apps`) och innehåller allt innehåll och all konfiguration.

- Paketet `all` är ett behållarpaket som innehåller underpaketen `ui.apps` och `ui.content`.

>[!NOTE]
>
> Projektstrukturen baseras på _Arketyp 48_ för paket och deras `pom.xml/filter.xml files`. Mer information finns i [Archetype 48](https://github.com/adobe/aem-project-archetype).

Databasmodernisering stöder nu även följande projekttyper:

- **MULTI_PROJECT**: Representerar ett flermodulsprojekt utan en gemensam överordnad POM, dispatcher och alla moduler.
- **SINGLE_PROJECT**: Representerar ett enskilt projekt.
- **NESTED_PROJECT**: Representerar ett flermodulsprojekt med en gemensam överordnad POM, dispatcher och alla moduler.
- **MONOLITHIC_PROJECT**: Representerar ett huvudprojekt med ett eller flera delprojekt.

## Använda Repository Modernizer {#using-repo-modernizer}

>[!VIDEO](https://video.tv.adobe.com/v/333057/?quality=12&learn=on)

- Databasuppdateringsfunktionen anropas nu automatiskt av omfaktoriseringstjänsten på fliken för omfaktoriseringsjobb. Kunderna behöver bara ladda upp sitt projekt och utlösa omfaktoriseringsjobbet - ingen ytterligare konfiguration krävs.

## Felkodreferens

Om du får en felkod när du använder Repository Modernizer kan du läsa tabellen nedan för mer information och rekommenderade åtgärder.

| Felkod | Meddelande | Beskrivning | Användaråtgärd krävs? |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------- | --------------------- |
| RM-100 | Ett fel uppstod när OSGi-konfigurationsfilen {0} konverterades till .cfg.json-format. Verifiera den befintliga konfigurationsfilen innan du försöker igen. | Det här felet inträffar när det uppstår ett fel under omvandlingen av en OSGi-konfigurationsfil till .cfg.json-formatet. | Ja |
| RM-101 | Ett fel uppstod vid försök att kopiera innehåll från: {0} | Det här felet inträffar när ett fel uppstår vid försök att kopiera innehåll från den angivna källan. | Nej |
| RM-102 | Det uppstod ett fel när filen {0} skulle flyttas från {1} till {2}. | Det här felet inträffar när det uppstår ett problem när en fil flyttas från en plats till en annan. | Nej |
| RM-103 | Det gick inte att matcha den angivna sökvägen till en giltig fil: {0} | Det här felet inträffar när filen inte hittas på den angivna platsen. | Nej |
| RM-104 | Det uppstod ett fel när innehållet i {0} itererades igenom. | Det här felet inträffar under genomgången av filer eller kataloger, vilket tyder på ett problem med åtkomst eller bearbetning av innehåll. | Nej |
| RM-105 | Ett fel uppstod när XML-filen skulle tolkas: {0}. Verifiera XML-filen innan du försöker igen. | Det här felet inträffar när det inte går att analysera XML-filen. | Ja |
| RM-106 | Det uppstod ett fel vid skrivning till XML-filen: {0}. | Det här felet inträffar när ett problem uppstår med att skriva till XML-filen. | Nej |
| RM-107 | Inga innehållspaket hittades i det befintliga projektet: {0}. Verifiera att rätt projekt har överförts. | Det här felet anger att inga innehållspaket hittades i det befintliga projektet. | Ja |
| RM-108 | Det gick inte att hitta POM-filen på den förväntade sökvägen: {0}. Projektets eller modulens POM-fil förväntas finnas direkt i sin katalog som en underordnad fil. | Det här felet inträffar när POM-filen inte hittas på den förväntade platsen. | Ja |
| RM-109 | Det uppstod ett fel när filen pom.xml skulle tolkas: {0}. Verifiera Tom-filen innan du försöker igen. | Det här felet inträffar när det uppstår ett problem när filen pom.xml analyseras. | Ja |
| RM-110 | Ett fel uppstod när filen pom.xml skrevs: {0}. | Det här felet inträffar när ett problem uppstår med att skriva till Tom-filen. | Nej |
| RM-111 | Fel vid skrivning till rapportfil. | Det här felet inträffar när ett fel uppstår under skrivning till rapportfilen. | Nej |
| RM-112 | Det gick inte att hitta {0} i databasens strukturrumsfil på ({1}) | Det här felet inträffar när den förväntade konfigurationen inte hittas i AEM projektarkivtypsmall. | Nej |
| RM-113 | Det uppstod ett fel när AEM Project Archetype-mallarna skulle kopieras till målet. | Det här felet inträffar när det uppstår ett problem när AEM Project Archetype-mallar kopieras till målet. | Nej |
| RM-115 | Ett fel uppstod vid försök att ansluta till Azure Blob Storage. | Det här felet inträffar när det uppstår ett problem med att ansluta till Azure Blob Storage. | Nej |
| RM-116 | Det uppstod ett fel när filen skulle överföras: {0} till Azure Blob Storage. | Det här felet inträffar när ett problem uppstår med att överföra en fil till Azure Blob Storage. | Nej |
| RM-117 | Ett fel uppstod vid försök att hämta filen: {0} från Azure Blob Storage. | Det här felet inträffar när ett problem uppstår med att hämta en fil från Azure Blob Storage. | Nej |
| RM-118 | I/O-fel uppstod vid hantering: {0}. | Det här felet inträffar när det uppstår ett problem med att läsa från eller skriva till en projektfil. | Nej |
| RM-119 | I/O-fel vid försök att arkivera resultaten för överföring till Azure. | Det här felet inträffar när ett fel inträffar när resultaten som genererats av processen arkiveras. | Nej |
| RM-120 | I/O-fel vid försök att ta bort arkivering av tjänstens zip-fil. Kontrollera om den angivna projektzippen är giltig. | Det här felet inträffar när ett fel inträffar när det angivna kundprojektet avarkiveras. | Ja |
| RM-121 | Ett fel uppstod när konfigurationsfilen skrevs. | Det här felet inträffar när ett fel uppstår under skrivning till konfigurationsfilen. | Nej |
| RM-122 | Begärandetypen stöds inte: {0}. | Det här felet inträffar när frågetypen inte stöds av systemet. Kontrollera begärandetypen och försök igen. | Nej |

## Förstå prioriteter för resultatrapport

När du hämtar den resultatrapport som genererats av verktyget Databasmodernisering tilldelas varje sökning en **prioritet**. Prioriteringarna hjälper er att förstå hur angeläget det är och vilken effekt varje enskild fråga har:

| Prioritet | Beskrivning |
| -------- | ----------------------------------------------------------------------------------------------- |
| CRITICAL | Måste lösas för att projektet ska kunna byggas. |
| HÖG | Ska åtgärdas för att säkerställa att funktionaliteten inte fungerar i AEM. |
| NORMAL | Bör lösas för att säkerställa den övergripande sundheten och fullständigheten hos en modernisering. |
| LÅG | För manuell verifiering är dessa brister informativa och kräver kanske inte omedelbara åtgärder. |

>[!NOTE]
> 
>Vi rekommenderar att man först åtgärdar högprioriterade brister för att säkerställa en smidig modernisering och driftsättningsprocess.
