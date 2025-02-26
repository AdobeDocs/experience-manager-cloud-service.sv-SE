---
title: Tillförlitlig hantering av flera platser
description: Lär dig rekommendationer om hur du skapar ett projekt på ett problemfritt sätt med lokaliserade webbplatser som utnyttjar en enda kodbas, som alla administreras av Edge Delivery Services.
feature: Edge Delivery Services
role: Admin, Architect, Developer
exl-id: f6b861ed-18e4-4c81-92d2-49fadfe4669a
source-git-commit: c9d0d3cd7e18b56db36a379b63f8fb48e18a40db
workflow-type: tm+mt
source-wordcount: '1260'
ht-degree: 0%

---

# Tillförlitlig hantering av flera platser {#repoless-msm}

Lär dig rekommendationer om hur du skapar ett projekt på ett problemfritt sätt med lokaliserade webbplatser som utnyttjar en enda kodbas, som alla administreras av Edge Delivery Services.

## Ökning {#overview}

[Multi Site Manager (MSM)](/help/sites-cloud/administering/msm/overview.md) och dess Live Copy-funktioner gör att du kan använda samma webbplatsinnehåll på flera platser samtidigt som du kan använda olika varianter. Du kan skapa innehåll en gång och skapa Live-kopior. MSM upprätthåller live-relationer mellan källinnehållet och dess Live-kopior så att källmaterialet och Live-kopiorna kan synkroniseras när du ändrar källinnehållet.

Ni kan använda MSM för att skapa en hel innehållsstruktur för ert varumärke över olika språk och språkområden, och redigera innehållet centralt. Dina lokaliserade sajter kan sedan levereras av Edge Delivery Services, med en central kodbas.

## Krav {#requirements}

Om du vill konfigurera MSM i ett problemfritt fall måste du först utföra följande uppgifter:

* I det här dokumentet förutsätts att du redan har skapat en webbplats för ditt projekt baserat på guiden [Komma igång för utvecklare för WYSIWYG-redigering med Edge Delivery Services](/help/edge/wysiwyg-authoring/edge-dev-getting-started.md).
* Du måste redan ha [aktiverat den svarslösa funktionen för ditt projekt](/help/edge/wysiwyg-authoring/repoless.md).

## Användningsfall {#use-case}

Det här dokumentet förutsätter att du redan har skapat en grundläggande lokaliserad platsstruktur för ditt projekt. I exemplet används följande struktur för varumärket med närvaro i Schweiz och Tyskland.

```text
/content/wknd
/content/wknd/language-masters
/content/wknd/language-masters/en
/content/wknd/language-masters/de
/content/wknd/language-masters/fr
/content/wknd/language-masters/it
/content/wknd/ch
/content/wknd/ch/de
/content/wknd/ch/fr
/content/wknd/ch/it
/content/wknd/ch/en
/content/wknd/de
/content/wknd/de/de
/content/wknd/de/en
```

Innehåll i `language-masters` är källan till Live-kopior för de lokaliserade webbplatserna: Tyskland (`de`) och Schweiz (`ch`). Målet med det här dokumentet är att skapa Edge Delivery Services-webbplatser som alla använder samma kodbas för varje lokaliserad webbplats.

## Konfiguration {#configuration}

Det finns flera steg för att konfigurera MSM-användningsexemplet utan problem.

1. [Uppdatera AEM webbplatskonfigurationer](#update-aem-configurations).
1. [Skapa nya Edge Delivery Services-webbplatser för dina lokaliserade sidor](#create-edge-sites).
1. [Uppdatera molnkonfigurationen i AEM för dina lokaliserade platser](#update-cloud-configurations).

### Uppdatera AEM webbplatskonfigurationer {#update-aem-configurations}

[Konfigurationer](/help/implementing/developing/introduction/configurations.md) kan ses som arbetsytor som kan användas för att samla in grupper med inställningar och deras associerade innehåll i organisatoriska syften. När du skapar en plats i AEM skapas en konfiguration automatiskt för den.

Du vill vanligtvis dela visst innehåll mellan webbplatser som:

* Mallar som har skapats från innehåll i ritningen
* Modeller för innehållsfragment, beständiga, frågor osv.

Du kan skapa ytterligare konfigurationer för att underlätta sådan delning. För det här fallet behöver vi konfigurationer för följande sökvägar.

```text
/content/wknd
/content/wknd/ch
/content/wknd/de
```

Det innebär att du kommer att ha en konfiguration för roten för det aktuella varumärkets innehåll (`/content/wknd`) som används av ritningarna och en konfiguration som används av varje lokaliserad plats (Schweiz och Tyskland).

1. Logga in på din AEM-redigeringsinstans.
1. Navigera till **Configuration Browser** genom att gå till **Tools** -> **General** -> **Configuration Browser**.
1. Välj den konfiguration som skapades automatiskt för ditt projekt (i det här fallet ) och tryck eller klicka sedan på **Skapa** i verktygsfältet.
1. I dialogrutan **Skapa konfiguration** anger du ett beskrivande **namn** för den lokaliserade platsen (till exempel `Switzerland`) och för **Rubrik** använder du samma namn för den lokaliserade storleken (i det här fallet `ch`).
1. Välj funktionen **Molnkonfiguration** och eventuella ytterligare funktioner som du kan behöva för ditt projekt, till exempel **Redigerbara mallar**.
1. Tryck eller klicka på **Skapa**.

Skapa konfigurationer för varje lokaliserad plats du behöver. Om det är fråga om wk måste du skapa en konfiguration för `de` samt tillsammans med `ch`-konfigurationen.

När konfigurationerna har skapats måste du se till att de lokaliserade platserna använder dem.

1. Logga in på din AEM-redigeringsinstans.
1. Navigera till **webbplatskonsolen** genom att gå till **Navigering** -> **Platser**.
1. Välj den lokaliserade platsen, till exempel `Switzerland`.
1. Tryck eller klicka på **Egenskaper** i verktygsfältet.
1. I fönstret för sidegenskaper väljer du fliken **Avancerat** och avmarkerar alternativet **Ärvd från /content/wknd** under rubriken **Konfiguration**, där `wknd` är platsroten.
1. I fältet **Molnkonfiguration** använder du sökvägsläsaren för att välja konfigurationen som du skapade för din lokaliserade plats, till exempel `Switzerland` under `/conf/wknd/ch`.
1. Tryck eller klicka på **Spara och stäng**.

Tilldela respektive konfigurationer till ytterligare lokaliserade platser. I fallet wk måste du även tilldela `/conf/wknd/de`-konfigurationen till Tysklands webbplats.

### Skapa nya Edge Delivery Services-sajter för lokaliserade sidor {#create-edge-sites}

Om du vill ansluta fler webbplatser till Edge Delivery Services för en flerspråkig webbplatskonfiguration måste du skapa en ny aem.live-webbplats för var och en av dina AEM MSM-webbplatser. Det finns en 1:1-relation mellan AEM MSM-webbplatser och Aem.live-webbplatser med en delad Git-databas och kodbas.

I det här exemplet skapar vi webbplatsen `wknd-ch` för den schweiziska närvaron av wknd, vars lokaliserade innehåll finns under AEM-sökvägen `/content/wknd/ch`.

1. Hämta din auth-token och programmets tekniska konto.
   * I dokumentet **Återanvända kod mellan platser** finns mer information om hur du [hämtar din åtkomsttoken](/help/edge/wysiwyg-authoring/repoless.md#access-token) och det [tekniska kontot](/help/edge/wysiwyg-authoring/repoless.md#access-control) för ditt program.
1. Skapa en ny plats genom att göra följande anrop till konfigurationstjänsten. Tänk på följande:
   * Projektnamnet i POST-URL:en måste vara det nya platsnamnet som du skapar. I det här exemplet är det `wknd-ch`.
   * Konfigurationen `code` ska vara densamma som du använde när du skapade det första projektet.
   * `content` > `source` > `url` måste anpassas till namnet på den nya platsen som du skapar. I det här exemplet är det `wknd-ch`.
   * Webbplatsnamnet i POST URL och `content` > `source` > `url` måste vara samma.
   * Anpassa `admin`-blocket för att definiera de användare som ska ha fullständig administrativ åtkomst till platsen.
      * Det är en matris med e-postadresser.
      * Jokertecknet `*` kan användas.
      * Mer information finns i dokumentet [Konfigurera autentisering för författare](https://www.aem.live/docs/authentication-setup-authoring#default-roles).

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/wknd-ch.json \
     --header 'Content-Type: application/json' \
     --header 'x-auth-token: <your-token>' \
     --data '{
       "code": {
           "owner": "<your-github-org>",
           "repo": "wknd",
           "source": {
               "type": "github",
               "url": "https://github.com/<your-github-org>/wknd"
           }
       },
       "content": {
           "source": {
               "url": "https://author-p<programID>-e<environmentID>.adobeaemcloud.com/bin/franklin.delivery/<your-github-org>/wknd-ch/main",
               "type": "markup",
               "suffix": ".html"
           }
       },
       "access": {
           "admin": {
               "role": {
                   "admin": [
                       "<email>@<domain>.<tld>"
                   ],
                   "config_admin": [
                       "<tech-account-id>@techacct.adobe.com"
                   ]
               },
               "requireAuth": "auto"
           }
       }
   }'
   ```

1. Lägg till sökvägsmappningen för den nya platsen genom att göra följande anrop till konfigurationstjänsten.

   ```text
   curl --request POST \
     --url https://admin.hlx.page/config/<your-github-org>/sites/wknd-ch/public.json \
     --header 'Content-Type: application/json' \
     --header 'x-auth-token: <your-token>' \
     --data '{
       "paths": {
           "mappings": [
               "/content/wknd/ch/:/"
           ],
           "includes": [
               "/content/wknd/ch/"
           ]
       }
   }'
   ```

1. Verifiera att den offentliga konfigurationen för den nya platsen fungerar genom att anropa `https://main--wknd-ch--<your-github-org>.aem.page/config.json` och verifiera innehållet i den returnerade JSON.

Upprepa stegen för att skapa ytterligare lokaliserade platser. Om du arbetar måste du skapa en `wknd-de`-webbplats för tysk närvaro.

### Uppdatera molnkonfigurationer i AEM för dina lokaliserade sidor {#update-cloud-configurations}

Dina sidor i AEM måste vara konfigurerade att använda de nya Edge Delivery Sites som du skapade i föregående avsnitt för din lokaliserade närvaro. I det här exemplet måste innehåll under `/content/wknd/ch` känna till för att kunna använda den `wknd-ch`-webbplats som du skapade. På liknande sätt måste innehåll under `/content/wknd/de` använda webbplatsen `wknd-de`.

1. Logga in på AEM författarinstans och gå till **Verktyg** -> **Cloud-tjänster** -> **Edge Delivery Services-konfiguration**.
1. Välj den konfiguration som skapades automatiskt för ditt projekt och sedan den mapp som skapades för den lokaliserade sidan. I det här fallet skulle det vara Schweiz (`ch`).
1. Tryck eller klicka på **Skapa** > **Konfiguration** i verktygsfältet.
1. I fönstret **Edge Delivery Services Configuration**:
   * Ange din GitHub-organisation i fältet **Organisation**.
   * Ändra platsnamnet till namnet på platsen som du skapade i föregående avsnitt. I det här fallet är det `wknd-ch`.
   * Ändra projekttypen till **aem.live med konfigurationen för den omvända konfigurationen**.
1. Tryck eller klicka på **Spara och stäng**.

## Verifiera installationen {#verify}

Nu när du har gjort alla nödvändiga konfigurationsändringar kontrollerar du att allt fungerar som det ska.

1. Logga in på din AEM-redigeringsinstans.
1. Navigera till **webbplatskonsolen** genom att gå till **Navigering** -> **Platser**.
1. Välj den lokaliserade platsen, till exempel `Switzerland`.
1. Tryck eller klicka på **Redigera** i verktygsfältet.
1. Kontrollera att sidan återges korrekt i Universellt redigeringsprogram och använder samma kod som platsroten.
1. Gör ändringar på sidan och publicera på nytt.
1. Besök din nya Edge Delivery Services-webbplats för den lokaliserade sidan på `https://main--wknd-ch--<your-github-org>.aem.page`.

Om du ser ändringarna som du har gjort fungerar MSM-konfigurationen som den ska.
