---
title: Integrera med Adobe Campaign Classic
description: Lär dig hur du integrerar AEM as a Cloud Service med Adobe Campaign Classic för att skapa övertygande innehåll för era kampanjer.
feature: Administering
role: Admin
exl-id: 23874955-bdf3-41be-8a06-53d2afdd7f2b
source-git-commit: cab630838f5cce3c2a2749c61b0aa7504dc403f7
workflow-type: tm+mt
source-wordcount: '1302'
ht-degree: 0%

---

# Integrera med Adobe Campaign Classic {#integrating-campaign-classic}

Genom att integrera AEM as a Cloud Service med Adobe Campaign kan ni hantera e-postleveranser, innehåll och formulär direkt i AEM as a Cloud Service. Konfigurationssteg i både Adobe Campaign Classic och AEM as a Cloud Service krävs för att möjliggöra dubbelriktad kommunikation mellan lösningar.

Tack vare den här integreringen kan AEM as a Cloud Service och Adobe Campaign Classic användas oberoende av varandra. Marknadsförare kan skapa kampanjer och använda målinriktning i Adobe Campaign, medan innehållsskapare kan arbeta parallellt med innehållsdesign i AEM as a Cloud Service. Tack vare integreringen kan innehållet i och utformningen av kampanjen i AEM målinrikta och levereras av Campaign.

## Integreringssteg {#integration-steps}

Integrationen mellan AEM och Campaign kräver ett antal steg i båda lösningarna.

1. [Installera AEM integreringspaket i Campaign.](#install-package)
1. [Skapa en operator för AEM i Campaign](#create-operator)
1. [Konfigurera Campaign-integrering i AEM](#campaign-integration)
1. [Konfigurera AEM](#externalizer)
1. [Konfigurera kampanjfjärranvändaren i AEM](#configure-user)
1. [Konfigurera det AEM externa kontot i Campaign](#acc-setup)

Det här dokumentet leder dig igenom dessa steg i detalj

## Förutsättningar {#prerequisites}

* Administratörsåtkomst till Adobe Campaign Classic
   * För att kunna utföra integreringen behöver du en fungerande Adobe Campaign Classic-instans, inklusive en konfigurerad databas.
   * Om du vill ha mer information om hur du konfigurerar och konfigurerar Adobe Campaign Classic kan du läsa [Adobe Campaign Classic dokumentation,](https://experienceleague.adobe.com/docs/campaign-classic/using/campaign-classic-home.html) särskilt i installations- och konfigureringshandboken.

* Administratörsåtkomst till AEM as a Cloud Service

## Installera AEM integreringspaket i Campaign {#install-package}

The **AEM** i Adobe Campaign innehåller ett antal standardkonfigurationer som krävs för att ansluta till AEM.

1. Som administratör loggar du in på Adobe Campaign-instansen med klientkonsolen.

1. Välj **verktyg** > **Avancerat** > **Importera paket...**.

   ![Importera paket](assets/import-package.png)

1. Klicka **Installera ett standardpaket** och sedan klicka **Nästa**.

1. Kontrollera **AEM** paket.

   ![Installera ett standardpaket](assets/select-package.png)

1. Klicka **Nästa** och sedan **Starta** för att starta installationen.

   ![Installationsförlopp](assets/installation.png)

1. Klicka **Stäng** när installationen är klar.

Integrationspaketet är nu installerat.

## Skapa en operator för AEM i Campaign {#create-operator}

Integrationspaketet skapar automatiskt `aemserver` som AEM använder för att ansluta till Adobe Campaign. Du måste definiera en säkerhetszon för den här operatorn och ange dess lösenord.

1. Logga in på Adobe Campaign som administratör med klientkonsolen.

1. Välj **verktyg** -> **Utforskaren** på menyraden.

1. I Utforskaren går du till **Administration** > **Åtkomsthantering** > **Operatorer** nod.

1. Välj `aemserver` -operator.

1. På **Redigera** -operatorfliken väljer du **Åtkomsträttigheter** underfliken och klicka sedan på **Redigera åtkomstparametrar...** länk.

   ![Ange säkerhetszon](assets/access-rights.png)

1. Välj lämplig säkerhetszon och definiera den betrodda IP-masken efter behov.

1. Klicka **Spara**.

1. Logga ut från Adobe Campaign-klienten.

1. På Adobe Campaign-serverns filsystem går du till installationsplatsen för Campaign och redigerar `serverConf.xml` som administratör. Den här filen finns vanligtvis under:
   * `C:\Program Files\Adobe\Adobe Campaign Classic v7\conf` i Windows.
   * `/usr/local/neolane/nl6/conf/eng` i Linux.

1. Sök efter `securityZone` och se till att följande parametrar ställs in för AEM säkerhetszon.

   * `allowHTTP="true"`
   * `sessionTokenOnly="true"`
   * `allowUserPassword="true"`.

1. Spara filen.

1. Se till att säkerhetszonen inte skrivs över av respektive inställning i dialogrutan `config-<server name>.xml` -fil.

   * Om konfigurationsfilen innehåller en separat inställning för säkerhetszon ändrar du `allowUserPassword` attribut till `true`.

1. Om du vill ändra serverporten för Adobe Campaign Classic ersätter du `8080` med önskad port.

>[!CAUTION]
>
>Som standard finns ingen säkerhetszon konfigurerad för operatorn. För att AEM ska kunna ansluta till Adobe Campaign måste du välja en zon enligt beskrivningen i föregående steg.
>
>Adobe rekommenderar starkt att du skapar en säkerhetszon som ska AEM för att undvika säkerhetsproblem. Mer information om detta finns i [Adobe Campaign Classic dokumentation.](https://experienceleague.adobe.com/docs/campaign-classic/using/installing-campaign-classic/additional-configurations/security-zones.html)

1. Gå tillbaka till Campaign-klienten `aemserver` och väljer **Allmänt** -fliken.

1. Klicka på **Återställ lösenord...** länk.

1. Ange ett lösenord och lagra det på en säker plats för framtida bruk.

1. Klicka **OK** för att spara lösenordet för `aemserver` -operator.

## Konfigurera kampanjintegrering i AEM {#campaign-integration}

AEM [operatorn som du redan har ställt in i Campaign](#create-operator) för att kommunicera med Campaign

1. Logga in som administratör i din AEM.

1. Välj **verktyg** > **Cloud Services** > **Äldre Cloud Services** > **Adobe Campaign** och sedan klicka **Konfigurera nu**.

   ![Konfigurera Adobe Campaign](assets/configure-campaign-service.png)

1. I dialogrutan skapar du en konfiguration för Campaign-tjänsten genom att ange en **Titel** och klicka **Skapa**.

   ![Konfigurera Campaign-dialogrutan](assets/configure-campaign-dialog.png)

1. Ett nytt fönster och en ny dialogruta öppnas där du kan redigera konfigurationen. Tillhandahåll nödvändig information.

   * **Användarnamn** - Det här är [paketoperatorn Adobe Campaign AEM Integration som skapades i föregående steg.](#create-operator) Som standard är det `aemserver`.
   * **Lösenord** - Det här är lösenordet för [paketoperatorn Adobe Campaign AEM Integration som skapades i föregående steg.](#create-operator)
   * **API-slutpunkt** - Detta är Adobe Campaign instans-URL:en.

   ![Konfigurera Adobe Campaign i AEM](assets/configure-campaign.png)

1. Välj **Anslut till Adobe Campaign** för att bekräfta anslutningen och sedan klicka på **OK**.

AEM kan nu kommunicera med Adobe Campaign.

>[!NOTE]
>
>Se till att din Adobe Campaign-server är tillgänglig via Internet. AEM as a Cloud Service har inte åtkomst till privata nätverk.

## Konfigurera AEM Externalizer {#externalizer}

Externalizer är en OSGi-tjänst i AEM som omvandlar en resurssökväg till en extern och absolut URL-adress, vilket är nödvändigt för att AEM ska kunna hantera innehåll som Campaign kan använda.

1. Logga in som administratör i AEM.
1. Bekräfta publiceringsinstansen i Externalizer-konfigurationen genom att kontrollera statusdumpen för OSGi-tjänsterna i [utvecklarkonsol.](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/debugging/debugging-aem-as-a-cloud-service/developer-console.html#osgi-services)
1. Om den inte är korrekt gör du de nödvändiga ändringarna i motsvarande instans-Git-databas och sedan [distribuera konfigurationen med hjälp av molnhanteraren.](/help/implementing/cloud-manager/deploy-code.md)

```text
Service 3310 - [com.day.cq.commons.externalizer] (pid: com.day.cq.commons.impl.externalizerImpl)",
"  from Bundle 420 - Day Communique 5 Commons Library (com.day.cq.cq-commons), version 5.12.16",
"    component.id: 2149",
"    component.name: com.day.cq.commons.impl.externalizerImpl",
"    externalizer.contextpath: ",
"    externalizer.domains: [local https://author-p17558-e33255-cmstg.adobeaemcloud.com, author https://author-p17558-e33255-cmstg.adobeaemcloud.com,
     publish https://publish-p17558-e33255-cmstg.adobeaemcloud.com]",
"    externalizer.encodedpath: false",
"    externalizer.host: ",
"    feature-origins: [com.day.cq:cq-quickstart:slingosgifeature:cq-platform-model_quickstart_author:6.6.0-V23085]",
"    service.bundleid: 420",
"    service.description: Creates absolute URLs",
"    service.scope: bundle",
"    service.vendor: Adobe Systems Incorporated",
```

>[!NOTE]
>
>Publiceringsinstansen måste kunna nås från Adobe Campaign-servern.

## Konfigurera användaren på AEM {#configure-user}

För att Campaign ska kunna kommunicera med AEM måste du ange ett lösenord för `campaign-remote` användare i AEM.

1. Logga in AEM som administratör.
1. På huvudnavigeringskonsolen klickar du på **verktyg** till vänster.
1. Klicka sedan på **Säkerhet** -> **Användare** för att öppna användaradministrationskonsolen.
1. Leta reda på `campaign-remote` användare.
1. Välj `campaign-remote` användare och klicka **Egenskaper** för att redigera användaren.
1. I **Redigera användarinställningar** fönster, klicka **Ändra lösenord**.
1. Ange ett nytt lösenord för användaren och notera lösenordet på en säker plats för framtida bruk.
1. Klicka **Spara** för att spara lösenordsändringen.
1. Klicka **Spara och stäng** för att spara ändringarna i `campaign-remote` användare.

## Konfigurera det AEM externa kontot i Campaign {#acc-setup}

När [installera **AEM** paket i Campaign,](#install-package) ett externt konto skapas för AEM. Genom att konfigurera det här externa kontot kan Adobe Campaign ansluta till AEM as a Cloud Service, vilket möjliggör tvåvägskommunikation mellan lösningarna.

1. Logga in på Adobe Campaign som administratör med klientkonsolen.

1. Välj **verktyg** -> **Utforskaren** på menyraden.

1. I Utforskaren går du till **Administration** > **Plattform** > **Externa konton** nod.

   ![Externa konton](assets/external-accounts.png)

1. Leta reda på det externa AEM. Som standard har den värdena:

   * **Typ** - AEM
   * **Etikett** - AEM instans
   * **Internt namn** - aemInstance

1. På **Allmänt** fliken för det här kontot anger du användarinformationen som du har definierat i [Ange användarlösenord för fjärrkampanj](#set-campaign-remote-password) steg.

   * **Server** - AEM författarserveradress
      * AEM författarserver måste kunna nås från Adobe Campaign Classic serverinstans.
      * Kontrollera att serveradressen **not** i ett avslutande snedstreck.
   * **Konto** - Som standard är detta `campaign-remote` användare som du anger i AEM [Ange användarlösenord för fjärrkampanj](#set-campaign-remote-password) steg.
   * **Lösenord** - Det här lösenordet är samma som `campaign-remote` användare som du anger i AEM [Ange användarlösenord för fjärrkampanj](#set-campaign-remote-password) steg.

1. Välj **Aktiverad** kryssrutan.

1. Klicka **Spara**.

Adobe Campaign kan nu kommunicera med AEM.

## Nästa steg {#next-steps}

När både Adobe Campaign Classic och AEM är as a Cloud Service konfigurerade är integreringen nu klar.

Nu kan du lära dig skapa nyhetsbrev i Adobe Experience Manager genom att fortsätta med [det här dokumentet.](/help/sites-cloud/authoring/campaign/creating-newsletters.md)
