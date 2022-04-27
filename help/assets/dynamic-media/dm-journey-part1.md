---
title: Dynamic Media Journey, del I
description: 'Dynamic Media Journey beskriver grunderna i Dynamic Media, hur det fungerar, vad det kan göra för dig och vilket värde det ger både ditt arbete och dina kunder. '
contentOwner: Rick Brough
products: Experience Manager as a Cloud Service
topic-tags: introduction,administering
content-type: reference
feature: Image Profiles
role: User, Admin
mini-toc-levels: 4
hide: false
hidefromtoc: false
source-git-commit: dc290be237c938af59960834b32269a1f6c5bd97
workflow-type: tm+mt
source-wordcount: '3484'
ht-degree: 0%

---


# Dynamic Media Journey: Grunderna, del I {#dm-journey-part1}

Välkommen till Dynamic Media Journey.

Den här resan handlar om grunderna i Dynamic Media, hur det fungerar, vad det kan göra för er och vilket värde det ger ert arbete och era kunder.

**_Förutsättningar_**

* Grundläggande förståelse för bild- och videoformat
* Grundläggande förståelse för HTML och CSS
* Grundläggande förståelse för designverktyg som Adobe Illustrator, Adobe Photoshop, Adobe XD
* Det är praktiskt att ha tillgång till Dynamic Media på Experience Manager, men det krävs inte

**_Vad du kan förvänta dig att lära dig_**

*Del I*
* Vad är Dynamic Media och hur kan det hjälpa dig?
* Användningsexempel för Dynamic Media
* Hur en mediefil flödar genom Dynamic Media-systemet

*Del II*
* Anatomi av en Dynamic Media-URL och hur Dynamic Media levererar innehåll
* Grundläggande om att skapa bildförinställningar för att återge resurser
* Bilduppsättningar, snurruppsättningar och blandade medieuppsättningar

**_Målgrupp_**
Den målgrupp som bäst passar läsarna på den här resan är följande som är nya för Dynamic Media på Experience Manager:

* Administratör
* Affärsanalytiker
* Innehållsarkitekt
* Innehållsförfattare
* Designer
* Developer
* Marknadsföring
* Product Manager/Owner

## Vad är Dynamic Media och hur kan det hjälpa dig? {#dm-journey-a}

Dynamic Media hjälper er att leverera visuella marknadsförings- och marknadsföringsresurser on demand. Det hjälper dig också att skapa och leverera interaktiva visningsupplevelser som zoomning, 360-graders rotation och video. Dina resurser skalas dynamiskt för konsumtion på webben, mobiler och sociala webbplatser. Med hjälp av en uppsättning primära källresurser - som bilder, video och 3D - genererar och levererar Dynamic Media flera varianter av det här innehållsrika innehållet i realtid via sin globala, skalbara, prestandaoptimerade CDN (Content Delivery Network).

Dynamic Media införlivar arbetsflödena i Adobe Experience Manager Assets Digital Asset Management-lösningen för att förenkla och effektivisera hanteringen av digitala kampanjer.

### En fil med oändliga möjligheter

En av de viktigaste punkterna att förstå om Dynamic Media är konceptet *En primär resursfil med oändliga möjligheter*.

För att förstå detta koncept bättre bör du tänka på hur du traditionellt arbetar med en enda resurs, till exempel en bild eller en video. Du skapar vanligtvis en primär resurs. Sedan skapar du manuellt versioner av samma material för alla upplevelser, enheter som behövs, alla webbsidor och alla egenskaper där de används. Med tiden kan den enskilda resursen växa till 20, 30 eller fler versioner utan versionshistorik kopplad till sig. Tänk dig att göra det för alla bilder och filmer du har. Antalet versioner skulle snabbt bli överväldigande för att underhålla och uppdatera, för att inte tala om ökningen av lagringskostnaderna.

Dynamic Media skiljer sig dock i grunden från andra system eftersom du använder det för att leverera dina mediefiler *dynamiskt* från enskilda, primära resurser och URL-anrop. De Dynamic Media URL-sökvägar du begär innehåller instruktioner som talar om för Adobe-publiceringsservern hur resursen visas när den levereras till en kunds skärm. Om du till exempel använder samma primära resurs kan du få den direkt i obegränsat antal renderingar och ändra storlek, format, upplösning, vikt, färg, beskärning och effekter som en zoomvy.

Denna unika leveransmetod säkerställer att enhetliga kvalitetsupplevelser skickas till alla skärmar, oavsett storlek och bandbredd. Filmer i fullstorlek optimeras också för alla skärmtyper och strömmas på ett adaptivt sätt för att säkerställa en konsekvent och högkvalitativ användarupplevelse.

<!-- As part of building and publishing assets with Dynamic Media, you visually configure the effects that you want to apply to assets. In so doing, you are literally building the URL that correctly tells the publish server how to deliver your primary asset to the screen.  -->

![Adobe Dynamic Media levererar samma primära bild till olika medier i olika storlekar och format.](/help/assets/dynamic-media/assets/dm-oneasset-multioutput.png)

*Adobe Dynamic Media ger enhetliga upplevelser av hög kvalitet för alla skärmar, oavsett storlek och bandbredd.*

När du läser vidare kommer du att lära dig mer om varför konceptet&quot;en primär resursfil, oändliga möjligheter&quot; är viktigt.

### The Content Delivery Network

När du är redo att publicera med en bildresurs eller en videoresurs stöds den av Dynamic Medias stamnät som består av ett kraftfullt leveransnätverk i toppskiktet. Nätverket betjänar hundratals klienter runt om i världen varje dag. Resurserna distribueras via Content Delivery Network - eller CDN - som Akamai är värd för. CDN är ett system med datortjänster som fungerar ihop och som på ett öppet sätt samarbetar för att leverera innehåll, särskilt omfattande mediematerial, till slutanvändarna.

I CDN-systemet lagras webbinnehåll i webbcacheminnen över Internet. Sedan levereras den från webbcachen till slutanvändarna för snabbare leverans. Så första gången någon hämtar en webbsida levereras de resurser som visas till ett CDN-cache. De lagras på servern så att samma cacheinnehåll levereras snabbare nästa gång någon i samma område öppnar webbsidan. Innehållet levereras snabbare eftersom det ligger närmare slutanvändaren. Ett CDN ger snabbare visning av webbsidor och ändå minskar behovet av bandbredd på den centrala servern eftersom innehållet levereras från ett cachenätverk, inte från en central server i varje instans. Detta optimerade flöde innebär en bättre användarupplevelse, vilket leder till ökad försäljning.

<!-- USE AN IMAGE HERE? ![Content delivery network](/help/assets/assets-dm/cdn.png) -->

Historiskt sett levererar CDN 3,5 petabyte trafik till kunderna varje månad. Systemet kan leverera 52 miljarder tillgångar på en enda dag. Detta motsvarar 864 000 bilder och videor som levererats till kunderna, *varje sekund*.

### Smart bildbehandling

Dynamic Media har redan gjort ett bra jobb med att optimera resurser och se till att varje resurs läses in snabbt på mobiler och datorer med CDN. För att detta ska hända används bildförinställningar i Dynamic Media för att definiera bildkvaliteten. De definierar också vilken typ av bild du skickar, dess skärpa och andra delar för olika delar av upplevelsen eller sidorna.

Men för att ytterligare öka värdet på Dynamic Media, utöver bildförinställningar, finns det *Smart bildbehandling*.

Smart Imaging ger ännu bättre prestanda vid leverans av bildresurser genom att automatiskt optimera bildens format och filstorlek baserat på kundens webbläsarkapacitet. Det fungerar med befintliga bildförinställningar (du kommer att läsa mer om bildförinställningar senare) och använder intelligens vid leverans.

Den här intelligensen minskar bildfilens storlek ytterligare baserat på webbläsarens och nätverkets anslutningshastighet. Eftersom bildobjekt utgör merparten av en sidas laddningstid kan prestandaförbättringarna få en genomgripande effekt på viktiga affärsindikatorer, som:

* Högre konvertering
* Tidsåtgång på webbplatsen
* Lägre avhoppsfrekvens för webbplats

Med smart bildbehandling kan du totalt sett förvänta dig en prestandaförbättring på 22 till 47 % beroende på dina befintliga förinställda bildinställningar och specifika egenskaper för slutanvändaren. Samtidigt som bildkvaliteten bibehålls som om den aldrig hade rörts.

![Smart bildbehandling](/help/assets/dynamic-media/assets/dm-smart-imaging.png)
*Smart Imaging optimerar automatiskt bildens format och filstorlek baserat på kundens webbläsarkapacitet och nätverkshastighet.*

Smart bildbehandling är inte aktiverat som standard eftersom det kräver en samordnad insats mellan dig och Adobe Dynamic Media tekniska support. För att du ska kunna aktivera Smart Imaging måste du dessutom rensa CDN-cachen fullständigt, som sedan fylls på med tid. Om du är intresserad av att använda Smart Imaging kan du med Adobe aktivera det genom att skicka in en teknisk supportanmälan. Teknisk support ger dig sedan en URL-parameter som gör att du kan testa smarta bilder i förväg. Du kan testa det på alla dina webbsidor eller bilder så att du kan se prestanda och besparingarna. Du kan sedan aktivera smart bildåtergivning för hela webbplatsen.

Läs mer om [Smart bildbehandling](/help/assets/dynamic-media/imaging-faq.md)

### Adaptiva videouppsättningar

När det finns en video på en sida, eller en huvudsida, tenderar kunderna att interagera med innehållet längre och stanna kvar längre på sidan, vilket vanligtvis är bra. Detta beteende har visats genom analyser som Adobe har gjort. Men video kan vara komplicerad. För det första har du ofta en stor primär fil. Det är komplicerat att avgöra hur stor videon ska vara och hur den ska levereras för att säkerställa att upplevelsen fungerar smidigt oavsett vilken enhet den visas på och oavsett bandbredd.

För att lösa problemet ger Dynamic Media dig möjlighet att skapa *Adaptiva videouppsättningar*.

![Adaptiv videouppsättning](/help/assets/dynamic-media/assets/dm-smart-imaging.png)
*En adaptiv videouppsättning grupperar versioner av samma video som är kodade med olika bithastigheter och format.*

Du börjar med den ursprungliga primära videon som du överför till systemet. Dynamic Media storleksändras automatiskt, eller *transcodes*, videon till flera videor. När filmen levereras avgör den sedan på ett smart sätt vilken videoskärm, vilken kvalitet och vilket format som ska användas och skickar den till telefonen, surfplattan eller datorn.

På en mobilenhet från iOS upptäcker den till exempel en bandbredd som 4G, 5G eller Wi-Fi. Sedan väljs automatiskt rätt kodad video bland de olika videobithastigheterna i den adaptiva videouppsättningen. Videon strömmas till mobila enheter, surfplattor och datorer.

Dessutom ändras videokvaliteten dynamiskt automatiskt om nätverksförhållandena ändras. Och om kunden övergår till helskärmsläge på en stationär dator svarar Adaptive Video Set med en bättre upplösning, vilket förbättrar kundens tittarupplevelse.

Med adaptiva videouppsättningar får du en jämn, högkvalitativ uppspelning för kunder som spelar upp Dynamic Media-video på flera skärmar och enheter. Det tar verkligen bort komplexiteten i videon.

<!-- X-REF to videos chapter.  -->

## Användningsexempel för Dynamic Media {#dm-journey-b}

Nedan följer några vanliga användningsexempel och lösningar som Dynamic Media kan hjälpa er med att skapa ett positivt kundengagemang, lojalitet, konvertering och ökad avkastning.

### Användningsfall: Grundläggande filhantering

Ett av de viktigaste användningsområdena för Dynamic Media är också ett av de mest uppenbara. Det vill säga att minska vikten på sidor och upplevelser och storleken på innehållet, oavsett om det är en bild eller en video, som levereras.

Nedan visas en typisk upplevelse eller webbsida. Cirka 90 % av en sida består av multimedia, till exempel bilder och videor, som oftast är mycket tyngre filer.

![Innehållssidans bredd](/help/assets/dynamic-media/assets/dm-content-page-weight.png)
*Innehållssidans bredd för en vanlig webbsida.*

De återstående 10 % är HTML, CSS-kod och specifika taggar. Du vill optimera 90 % av den sidan så hjälper Dynamic Media till. Tidigare läste du om begreppet *En primär resursfil med oändliga möjligheter*. Detta är en viktig metod för att minska den totala sidbredden. Möjligheten att ta en primär resurs och använda den på en produktinformationssida, en miniatyrsida, kundvagnen och sökrutnätet är en utmärkt tidsbesparing. Och det säkerställer också enhetlighet mellan upplevelserna.

![Grundläggande filhantering](/help/assets/dynamic-media/assets/dm-onefile.png)
*En fil med flera renderingar direkt.*

Låt oss titta närmare på de problem som Dynamic Media löser med den enda filen och några av lösningarna på den metoden.

| **Problem** | **Dynamic Media** |
|---|---|
| Skapa och lagra alla resurser. | Använd en enda bildfil och skapa automatiskt de återgivningar som krävs endast i samband med leveransen. |
| Höga lagringskostnader. | Eliminerar behovet av att skapa och lagra flera renderingar av en mediefil. |
| Svårighet att upprätthålla vårdkedjan. | Garanterar leverans av enhetsoptimerade och enhetliga upplevelser. |
| Ingen versionshistorik. |  |
| Inkonsekventa varumärkesupplevelser på olika enheter. |  |
| Onödig kostnad för att skapa duplicerade resurser. |  |

När du tänker på en fil skapar du en resurs för alla typer av upplevelser. Du kanske har en startbild och sedan måste du skapa 20, 30 eller 40 varianter av den bilden, som du i slutändan måste lagra och betala för den lagringen.

Du måste också se till att rätt bild används och det kan påverka din förmåga att vara konsekvent mellan olika varumärken. Om du inte hittar någon bild måste du gå tillbaka och duplicera resurserna.

Med Dynamic Media kan du skapa varianter av bilder direkt från den startbilden. Du kan vara kreativ med den primära resursen och inte behöva gå fram och tillbaka med din grafiska designer eller fotostudio för att skapa ytterligare innehåll. Och det är pengar och tid sparat.

Med en enda filmetod använder du en enda primär fil. Skapa sedan de versioner eller renderingar som krävs på alla era webbplatser, samt egenskaper och upplevelser, endast när de levereras eller ses av en kund. Effektiviteten kan avsevärt minska mängden lagringsutrymme som krävs för dina resurser och minska arbetsflödets totala komplexitet. Och med Dynamic Medias leveranssystem garanterar det att alla bilder och filmer är optimerade, läses in snabbt och ser bra ut på alla skärmar och enheter.

### Användningsfall: Video

Ett annat användningsfall som Dynamic Media löser är video. Video är komplex. Det är svårt att hantera. Videofiler är svåra att lagra och flytta runt på grund av deras inbyggda filstorlek.

| **Problem** | **Dynamic Media** |
|---|---|
| Svårt att hantera och leverera video som är optimerad för olika enheter. | Använd en enda video som automatiskt storleksändras för alla enheter. |
| Videorna stannar kvar eller spelas upp med låg kvalitet på grund av att slutanvändaren har en tillgänglig bandbredd. | Leverera video via en HTML-spelare som automatiskt hittar tillgänglig bandbredd och anpassar kvaliteten för att säkerställa hög återgivning och jämn uppspelning. |
| Omöjligt och tidsödande att manuellt skapa alla versioner av en video för att säkerställa bra visning och uppspelning på alla enheter. | Eliminera timtals av mödosamt transkodningsarbete med ett förenklat arbetsflöde. |
|  | Frigör tid för mer värdefullt arbete. |

Kunder kommer till Dynamic Media med följande problem som de hoppas kunna lösa:

&quot;*Vi har videon och spenderade mycket pengar på att skapa den. Men vi slipper lägga in den på webbsidor eller leverera den, eftersom vi inte kan garantera kvaliteten på videon, eller om den verkligen kommer att spelas upp. Och i slutändan påverkar det våra varumärken och kanske vår roll till och med konverteringsgraden.*&quot;

Dynamic Medias lösning är att ta den primära videofilen och låta Dynamic Media göra alla storlekar genom sin transkodningsprocess. Koppla sedan ihop det med Dynamic Medias intelligenta videospelare. Detta arbetsflöde garanterar att videon, oavsett om du använder den på landningssidan eller på en kategori- eller produktinformationssida, är konsekvent hela tiden och levereras med hög kvalitet.

Här är några fler användningsområden att tänka på.

### Användningsfall: En enda källa till sanning

| **Problem** | **Dynamic Media** |
|---|---|
| Digitalt material som är utspridt i hela organisationen, isolerat i olika team eller affärsenheter. | Lagra och hantera alla digitala resurser på en central plats. |
| Teammedlemmar kan hämta och skapa lokala versioner. | Teammedlemmar använder en enda primär fil för att skapa *och* leverera alla nödvändiga versioner för olika skärmstorlekar och enheter. |
| Enkelt använda resurser som skapats för alla upplevelser och enheter. | Eliminerar resurser som används fristående, vilket sparar tid och pengar när du skapar dem. |

### Användningsfall: AI-baserad Smart Cropping för multimedia

| **Problem** | **Dynamic Media** |
|---|---|
| Tidsödande och arbetskrävande att manuellt rita, mäta och klippa bilder eller videor för att markera fokalpunkten och visa på rätt sätt på alla skärmstorlekar och enheter. | Använder Smart Crop i Dynamic Media, en AI-funktion från Adobe Sensei, för att automatiskt identifiera fokalpunkten i bilder och videoklipp och beskära för att behålla den. |
| Förlorad tid som skulle kunna användas bättre för att skapa slagkraftiga upplevelser. | Fångar den avsedda intressepunkten oavsett skärmstorlek. |
| Enkelt använda resurser som skapats för alla upplevelser och enheter. | Eliminerar långtråkiga manuella moment och levererar högkvalitativa, snabba bilder och video som ser bra ut på alla slags enheter och skärmar. |

### Användningsfall: Skapa interaktiva medier

| **Problem** | **Dynamic Media** |
|---|---|
| Plattformade och statiska kundupplevelser som inte engagerar, engagerar lojalitet eller driver konverteringsgraden. | Gör det möjligt för icke-tekniska användare att enkelt och smidigt lägga till interaktiva element som aktiveringspunkter, karuseller och snurra för mer dynamiska och engagerande upplevelser. |
| Begränsad avkastning på investeringar från digitala resurser och kluriga kundupplevelser. | Ökar konverteringsgraden och avkastningen på investeringar från multimedieupplevelser. |

## Hur en mediefil flödar genom Dynamic Media-systemet {#dm-journey-c}

Nedan visas ett typiskt arbetsflöde för Dynamic Media.

![Dynamic Media arbetsflöde](/help/assets/dynamic-media/assets/dm-workflow.png)
*Hur en mediefil flödar genom Dynamic Media-systemet.*

Du börjar med att skapa fasen med huvudmålet att ha den primära resursen i slutet. Dessa resurser kan komma från foton, från videoleverantörer eller vara några ljudfiler som du har skapat. Du kan använda Adobe Creative Suite-program som Adobe InDesign, Adobe Photoshop och Adobe Illustrator för att få hjälp med att lösa innehållet.

När delen är klar placerar du resursen i redigeringslösningen genom att överföra resursen till Dynamic Media. I Dynamic Media ser du till att du har rätt bildförinställningar och visningsprogram för dina olika webbsidor på din webbplats.

Och slutligen optimerar ni allt detta innehåll och publicerar det på Dynamic Media-servrar så att det blir tillgängligt för webben, utskrift, e-post, datorer och mobila enheter.

### Överföra resurser till Dynamic Media

När du är klar med att skapa en primär resurs överför du den till Dynamic Media. Den typ av fil som du överför samt filens format och storlek är viktiga attribut för Dynamic Media. Det är när överföringen görs som du vill vara säker på att du får ut maximalt värde av filstödet.

Den bevakade bilden nedan är till exempel 4 560 x 3 020 pixlar. Och även om du aldrig använder en bild med den storleken kan du ändå överföra den. Ju större bild, desto bättre kvalitet kan Dynamic Media leverera, även till miniatyrrenderingar. Kom ihåg: enkelt *minska* upplösningen för en befintlig bild. Men om du försöker *ökning* upplösningen i en bild, resultatet kommer troligen att bli otillfredsställande.

![Rekommenderade format att överföra till Dynamic Media](/help/assets/dynamic-media/assets/dm-upload-formats.png)
*Att tänka på vid överföringar av resurser.*

Adobe rekommenderar att du överför resurser i ett förlustfritt format. I allmänhet är det bäst att undvika JPEG eftersom du, när du levererar JPEG eller när du fortsätter att spara JPEG, börjar tappa bildkvaliteten med tiden. Du vill börja med bilder med den högsta upplösningen i ett förlustfritt format som du kan använda. Formatet är vanligtvis en TIFF- eller PNG-fil.

När du tänker på en digital kanal eller webbvy kanske du tänker på RGB (röd, grön, blå).

De flesta skulle aldrig tänka på att leverera något i CMYK eller varför du kanske till och med vill leverera i CMYK. Orsaken är att den färgrymden oftast används för att leverera utskrivna objekt. Men Dynamic Media kan leverera i båda färgrymderna.

Det finns många kunder som fortfarande gör utskrifter, som till exempel detaljhandelsklubbar. Och det finns matbutiker som ofta skriver ut flygblad varje vecka. Dessa kunder kräver att deras bilder finns i båda färgrymderna. Det brukar kräva två olika bilder: en i RGB och en i CMYK. Du kan dock överföra CMYK-resurser direkt till Dynamic Media och låta Dynamic Media leverera RGB-resurser automatiskt via en bildförinställning eller via en färgprofil. Man behöver inte skapa flera versioner av en fil, vilket betyder att man kan behålla konceptet med *En primär resursfil med oändliga möjligheter*.

XREF FÖR ATT ÖVERFÖRA RESURSER I DYNAMIC MEDIA

<!-- **The Value of Renditioning??? or Demo portion** -->

### Publicera och förhandsgranska resurser

När du har överfört resurser till Dynamic Media är det en god vana att *publicera* genom att markera resurserna och sedan klicka på **[!UICONTROL Publish]** eller **[!UICONTROL Quick Publish]** i Dynamic Media. Det är nödvändigt att publicera resurser om du tänker använda dem i någon upplevelse. När resurserna har publicerats är de tillgängliga för dig så att du kan inkludera dem på en webbsida med en Dynamic Media-genererad URL som du kopierar, eller genom att bädda in kod på sidan.

Förutom att publicera resurser manuellt kan du konfigurera Dynamic Media så att du omedelbart publicerar resurser - utan att behöva göra något - när överföringen görs.

Se [Publicera Dynamic Media-resurser](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/dynamicmedia/publishing-dynamicmedia-assets.html?lang=en).

Efter överföring finns det olika sätt att förhandsgranska en resurs renderingar i Dynamic Media. Genom att förhandsgranska renderingar får du en uppfattning om vad en kund ser. En vanlig förhandsvisningsmetod är att välja en resurs och sedan visa återgivningarna genom att välja en *bildförinställning* enligt följande.

![Förhandsgranska en återgivning av en resurs baserat på förinställningen för stor bild](/help/assets/dynamic-media/assets/dm-image-preset-with-url.png)
*Förhandsgranska en återgivning av en resurs baserat på den valda förinställningen för&quot;stor&quot; bild. Klicka på URL-knappen. Den resulterande URL-sökvägen kan användas på en webbsida.*

URL:en ovan är live! [Prova](http://s7d1.scene7.com/is/image/jpearldemo/AdobeStock_28563982?$Large$).

Ett annat sätt att förhandsgranska en resurs är att välja bildresursen och sedan välja en *Tittare* förinställning enligt följande.

![Förhandsgranska en resurs baserat på förinställningen för Zooma vertikalt ljus i visningsprogrammet](/help/assets/dynamic-media/assets/dm-viewer-preset.png)
*Förhandsgranska en resurs baserat på den valda visningsförinställningen &quot;ZoomVertical_light&quot;. Muspekaren (`+`) flyttades över klockan för att zooma in. Lägg märke till knapparna URL och Bädda in.*

Återgivningen ovan är live! [Prova](https://s7d1.scene7.com/s7viewers/html5/ZoomVerticalViewer.html?asset=jpearldemo/AdobeStock_28563982&amp;config=jpearldemo/ZoomVertical_light).

Låt oss titta lite närmare på dessa URL:er så att du bättre kan förstå vad som pågår.

Ta mig till [Dynamic Media Journey: Grunderna, del II](/help/assets/dynamic-media/dm-journey-part2.md#dm-journey-d).





