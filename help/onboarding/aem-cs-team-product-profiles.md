---
title: AEM as a Cloud Service Team- och produktprofiler
description: Läs om hur AEM as a Cloud Service team och produktprofiler kan ge och begränsa åtkomsten till era licensierade Adobe-lösningar.
exl-id: 7b1474c9-aca0-4354-8798-1abdcda2f6dd
feature: Onboarding
role: Admin, User, Developer
source-git-commit: 86bb2e020a003fd418f8b1cf7bdf55987a2eaf3d
workflow-type: tm+mt
source-wordcount: '2062'
ht-degree: 0%

---


# AEM as a Cloud Service Team- och produktprofiler {#product-profiles}

Läs om hur AEM as a Cloud Service team och produktprofiler kan ge och begränsa åtkomsten till era licensierade Adobe-lösningar.

## Produktprofiler {#profiles}

När du ger en användare åtkomst till en viss Adobe-lösning behöver du inte nödvändigtvis ge dem fullständig åtkomst. Med produktprofiler kan varje lösning ha en egen uppsättning användarbehörigheter. Dessa är tillgängliga och tillgängliga via [Admin Console](/help/journey-onboarding/admin-console.md).

Adobe Admin Console har en strukturerad hierarki av produkter, produktinstanser och produktprofiler där organisationens interna användare kan tilldelas medlemskap, vilket ger dem tillgång till lösningar och funktioner som licensierats.

<!-- Alexandru: Drafting for now 

Your AEM as a Cloud Service team members are added and assigned to one or more of the following product profiles via the Admin Console during onboarding.

* **AEM Administrators**: An AEM administrator is typically assigned to developers, in particular developers who need access to, for example, the development environments. The AEM administrator's product profile is used to grant administrator privileges in the associated AEM instance.

* **AEM Users**: AEM users are the users in your organization who use AEM as a Cloud Service generally to create content. These users need to access AEM to do their tasks. The AEM users product profile is typically assigned to an AEM content author who creates and reviews the content. This content can be of many types such as pages, assets, publications, and so on. The AEM users product profile shown below is assigned to these members.

![Product profiles](/help/onboarding/assets/admin-console-profiles.png) -->

## AEM as a Cloud Service produktprofiler {#aem-product-profiles}

AEM as a Cloud Service är ett fullständigt molnbaserat erbjudande som levererar AEM som en tjänst. Programmet levererar AEM på ett inbyggt sätt i molnet, med nya attribut som alltid är aktiverade, alltid aktuella, alltid säkra och alltid i stor skala. Samtidigt behåller Adobe det huvudsakliga mervärdet som AEM erbjuder som en anpassningsbar plattform för kunder och gör det möjligt för företagsgrupper att integrera i sina utvecklings- och leveransrutiner. Mer information om AEM as a Cloud Service finns i [Introduktion till Adobe Experience Manager as a Cloud Service](/help/overview/introduction.md).

### Produktinstanser på organisationsnivå {#org-level-product-instances}

>[!NOTE]
>
> Vissa produktinstanser och produktprofiler som beskrivs i den här artikeln kan endast visas för nyligen skapade miljöer. I avsnittet [Lägga till produktprofiler för befintliga miljöer](#adding-product-profiles-for-existing-environments) finns mer information om hur du moderniserar dina miljöer.

När Adobe behandlar licensieringen av en AEM-lösning för första gången visas två produktinstanser i Adobe Admin Console, under Adobe Experience Manager as a Cloud Service-produkten:

* **AEM organisationsnivå** - innehåller en eller flera produktprofiler som representerar åtkomst till funktioner som omfattar alla AEM-miljöer, i stället för bara en enda
* **Cloud Manager** - innehåller produktprofiler som motsvarar olika åtkomstnivåer för Cloud Manager-funktioner.

<!--
>[!NOTE]
>
>For existing programs, the AEM Org-Level Product Instance is created upon selecting the **Update product** profiles action for a given environment.
-->

![Produktinstanser på organisationsnivå](/help/onboarding/assets/orglevel.png)

I AEM produktinstans på organisationsnivå finns en produktprofil som heter AEM Org-Level Reporters, som inte används just nu, men som i framtiden kan återge åtkomst till hämtning av information om AEM produktlicenser.

När en Forms Communication Solution är licensierad visas även en motsvarande produktprofil under AEM produktinstans på organisationsnivå.

![Produktprofil för rapportörer](/help/onboarding/assets/org-level-reporters.png)

### Produktinstanser på miljö- och nivånivå {#environment-and-tier-level-product-instances}

När nya program etableras i en eller flera AEM-miljöer visas två produktinstanser per miljö, som innehåller produktprofiler för författare respektive publicering.

![Miljöproduktinstanser](/help/onboarding/assets/env-productinstances.png)

Nedan finns produktprofilerna i en produktinstans för en författare som har etablerat en miljö i ett program som innehåller AEM Sites:

![Webbplatsproduktinstanser](/help/onboarding/assets/sites-product-instances.png)

I följande tabell beskrivs en lista med möjliga produktprofiler under en produktinstans på miljönivå.

<table style="table-layout:auto">
    <tr>
        <th>Produktinstans</th>
        <th>Namngivningskonvention</th>
        <th>Standardtjänst</th>
        <th>Beskrivning</th>
    </tr>
    <tr>
        <td>AEM Author</td>
        <td>AEM Sites Content Managers - författare - Program <code>id</code> - Miljö <code>id</code></td>
        <td>AEM Sites Content Managers</td>
        <td>
            <ul>
                <li>Avsett för kontrollerad åtkomst till AEM Sites författarfunktioner i den här miljön. Användare i den här produktprofilen kommer att vara medlemmar i AEM Sites innehållsförfattare i AEM-gruppen, som automatiskt skapas i AEM. AEM-gruppbehörigheterna bör konfigureras i AEM med den önskade åtkomstnivån.</li><br>
                <li>Om standardtjänsten förblir markerad
                    <ul>
                        <li>användare i den här produktprofilen kommer också att vara medlemmar i AEM-gruppen"AEM Sites Content Managers - Service".</li>
                      <!--  <li>users in this product profile will have access to AEM Sites Content Management API.</li>
                        <li>an Adobe Developer Console API OAuth S2S project containing AEM Sites Content Management API can optionally be scoped to this environment.</li>-->
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM-administratörer - författare - program <code>id</code> - miljö <code>id</code></td>
        <td>AEM-administratörer</td>
        <td>
            <ul>
                <li>Avsett för obegränsad åtkomst till funktionerna för AEM författare och publiceringsmiljö. Användare i den här produktprofilen kommer att vara medlemmar i gruppen AEM Administrators författare i AEM som automatiskt skapas i AEM.</li><br>
                <li>Om standardtjänsten förblir markerad
                    <ul>
                        <li>användare i den här produktprofilen kommer också att vara medlemmar i AEM-gruppen"AEM Administrators - Service"</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Users - author - Program <code>id</code> - Environment <code>id</code></td>
        <td>AEM-användare</td>
        <td>
            <ul>
                <li>Avsett för mycket begränsad åtkomst till funktionerna i AEM redigeringsmiljö. Användare i den här produktprofilen blir medlemmar i AEM-gruppen"Medarbetare" som automatiskt skapas i AEM</li><br>
                <li>Om standardtjänsten förblir markerad
                    <ul>
                        <li>användare i den här produktprofilen kommer också att vara medlemmar i AEM-gruppen"AEM Users - Service"</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Reporters - author - Program <code>id</code> - Environment <code>id</code></td>
        <td>AEM Reporters</td>
        <td>
            <ul>
                <li>Används inte för närvarande, men i framtiden kan det ge åtkomst till rapportinformation om författarnivån för den här miljön.</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Assets Collaborator - författare - Program <code>id</code> - Miljö <code>id</code></td>
        <td>Användare av AEM Assets Collaborator</td>
        <td>
        <ul>
                <li>Avsett för skrivskyddad åtkomst till DAM. Användare i den här produktprofilen blir automatiskt medlemmar i AEM-gruppen"Medarbetare" som skapats i AEM.
                </li>
                <li>
                Dessutom innehåller det Adobe Express berättiganden för att skapa resursvariationer.
                </li>
          <ul>
    </tr>
    <tr>
        <td></td>
        <td>AEM Assets Power User - author - Program <code>id</code> - Environment <code>id</code></td>
        <td>AEM Assets Power Users</td>
<td>
        <ul>
                <li>Avsett för skrivskyddad åtkomst till DAM. Användare i den här produktprofilen blir automatiskt medlemmar i AEM-gruppen"Medarbetare" som skapats i AEM.
                </li>
                <li>
                Dessutom innehåller det Adobe Express berättiganden för att skapa resursvariationer.
                </li>
          <ul>
</td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Forms Content Managers - författare - Program <code>id</code> - Miljö <code>id</code></td>
        <td>AEM Forms Content Managers</td>
        <td>
            <ul>
                <li>Avsett för kontrollerad åtkomst till AEM Forms författarfunktioner i den här miljön. Användare i den här produktprofilen blir medlemmar i AEM-gruppen AEM Forms-användare som automatiskt skapas i AEM.</li><br>
                <li>Om standardtjänsten förblir markerad
                    <ul>
                        <li>användare i den här produktprofilen kommer också att vara medlemmar i AEM-gruppen"AEM Forms Content Managers - Service".</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Forms-utvecklare - författare - Program <code>id</code> - Miljö <code>id</code></td>
        <td>AEM Forms-utvecklare</td>
        <td>
            <ul>
                <li>Avsett för kontrollerad åtkomst till AEM Forms författarfunktioner i den här miljön. Användare i den här produktprofilen kommer att ingå i AEM Forms AEM-gruppen för blankettanvändare, som automatiskt skapas i AEM. Dessa användare har även behörighet att överföra XDP-filer och skapa formulärdatamodeller, utöver vanliga formulärredigeringsåtgärder.</li><br>
                <li>Om standardtjänsten förblir markerad
                    <ul>
                        <li>användare i den här produktprofilen kommer också att vara medlemmar i AEM-gruppen"AEM Forms Developers - Service".</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Forms Communications Service Users - författare - Program <code>id</code> - Miljö <code>id</code></td>
        <td>Användare av AEM Forms Communications Service</td>
        <td>
            <ul>
                <li>Avsett för kontrollerad åtkomst till AEM Forms Communications Services-funktioner i den här miljön. Användare i den här produktprofilen blir medlemmar i AEM-gruppen AEM Forms-användare som automatiskt skapas i AEM.</li><br>
                <li>Om standardtjänsten förblir markerad
                    <ul>
                        <li>användare i den här produktprofilen kommer också att vara medlemmar i AEM-gruppen"AEM Forms Communications Service Users - Service".</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>AEM Publish</td>
        <td>AEM-användare - publicera - program <code>id</code> - miljö <code>id</code></td>
        <td>AEM-användare</td>
        <td>
            <ul>
                <li>Avsett för mycket begränsad åtkomst till funktionerna i AEM redigeringsmiljö. Användare i den här produktprofilen blir medlemmar i AEM-gruppen"Contrib" som automatiskt skapas i AEM</li><br>
                <li>Om standardtjänsten förblir markerad
                    <ul>
                        <li>användare i den här produktprofilen kommer också att vara medlemmar i AEM-gruppen"AEM Users - Service".</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
    <tr>
        <td></td>
        <td>AEM Reporters - publish - Program <code>id</code> - Environment <code>id</code></td>
        <td>AEM Reporters</td>
        <td>
            <ul>
                <li>Används inte för närvarande, men i framtiden kan det ge åtkomst till rapportinformation om publiceringsnivån för den här miljön.</li>
            </ul>
        </td>
    </tr>
   <tr>
        <td></td>
        <td>AEM Forms Communications Service Users - publish - Program <code>id</code> - Environment <code>id</code></td>
        <td>Användare av AEM Forms Communications Service</td>
        <td>
            <ul>
                <li>Avsett för kontrollerad åtkomst till AEM Forms Communications Services-funktioner i den här miljön. Användare i den här produktprofilen blir medlemmar i AEM-gruppen AEM Forms-användare som automatiskt skapas i AEM.</li><br>
                <li>Om standardtjänsten förblir markerad
                    <ul>
                        <li>användare i den här produktprofilen kommer också att vara medlemmar i AEM-gruppen"AEM Forms Communications Service Users - Service".</li>
                    </ul>
                </li>
            </ul>
        </td>
    </tr>
</table>

Observera att varje produktprofil har en tillhörande produktprofiltjänst aktiverad som standard. Om du inte har komplexa åtkomstkrav rekommenderar vi att du bara väljer standardtjänsten. En motsvarande AEM-grupp skapas i AEM med namnkonventionen `<Product Profile Prefix> - Service` (till exempel **AEM Sites Content Managers - Service**) och användarna i de överordnade produktprofilerna blir automatiskt medlemmar i motsvarande AEM-grupp.

Den AEM-grupp i AEM som är kopplad till tjänsten kommer att ha den sammanställda uppsättningen användare som finns i alla tillhörande produktprofiler för den tjänsten för den aktuella kombinationen på miljönivå.

![Tjänster](/help/onboarding/assets/services.png)

Följande bild visar AEM-grupperna som återspeglar AEM Sites Content Managers författarnivå Produktprofil och tjänst.

![Mappning av AEM-grupp till tjänst](/help/onboarding/assets/profile-to-service-mapping.png)

>[!NOTE]
>
>Alla användare som tilldelats en AEM as a Cloud Service-produktprofil har skrivskyddad åtkomst till Cloud Manager via rollen **Cloud Manager-användare**.
>
>Användare med endast rollen **Cloud Manager-användare** kan logga in på Cloud Manager och navigera till AEM författarmiljöer (om sådana finns) med hjälp av menyalternativen på **Program** . Rollen **Cloud Manager-användare** har inte tillräcklig åtkomst till programinformation. Om sådan åtkomst behövs måste användarna tilldelas ytterligare roller av systemadministratören.

>[!WARNING]
>
>Produktprofilnamnet för **AEM-administratörer** får inte ändras. Om du ändrar namnet på produktprofilen **AEM Administrators** tas administratörsrättigheter bort från alla användare som tilldelats den profilen.

>[!TIP]
>
>* Mer information om AEM produktprofiler finns i [Tilldela AEM produktprofiler](/help/journey-onboarding/assign-profiles-aem.md).
>* Mer information om introduktionsprocessen finns i [Startresa](/help/journey-onboarding/overview.md).

### Lägga till produktprofiler för befintliga miljöer {#adding-product-profiles-for-existing-environments}

Miljöer som skapats före början av april 2024 kan sakna den produktinstans på organisationsnivå som beskrivs i avsnitten ovan samt vissa produktprofiler. Befintliga produktprofiler kommer också att sakna tjänstväxlarna. Vi rekommenderar att du uppdaterar dessa produktprofiler, vilket är en förutsättning för att få tillgång till vissa framtida API:er.

Om en eller flera miljöer i ett program behöver sina produktprofiler uppdaterade kommer Cloud Manager att visa meddelandet nedan. Observera att en miljö måste finnas i den senaste AEM-versionen innan produktprofilerna kan uppdateras.

![Modernisera produktprofiler](/help/onboarding/assets/modernize-product-profiles.png)

Om du klickar på knappen **Lägg till produktprofiler** öppnas en meny med alternativ för att lägga till nya produktprofiler i alla miljöer som är tillgängliga i programmet eller i enskilda miljöer.

![Ersätt miljöer](/help/onboarding/assets/choose-env-r.png)

Klicka på **Alla miljöer** för att lägga till de nya produktprofilerna i alla miljöer i programmet. Du kan också klicka på **Enskilda miljöer** om du vill lägga till de nya produktprofilerna i de valda miljöerna. Detta leder till en miljölistsida där en **Lägg till produktprofiler** -åtgärd kan väljas från ikonen **Fler alternativ** .

![Enskilda miljöer](/help/onboarding/assets/individual-environments.png)

Du kan också lägga till produktprofiler i utvalda miljöer genom att gå till avsnittet Programöversikt, klicka på ikonen Fler alternativ för en miljö och välja Lägg till produktprofiler.

Miljöns status visar Lägga till produktprofiler medan de nya produktprofilerna läggs till och sedan visas Körning när processen är klar.


## Cloud Manager produktprofiler {#cloud-manager-product-profiles}

Cloud Manager har förkonfigurerade produktprofiler som kan tolkas som rollbaserade behörigheter. Din systemadministratör ansvarar för att konfigurera ditt Cloud Manager-team genom att tilldela dem till dessa produktprofiler.

>[!TIP]
>
>Mer information finns i [Rollbaserade behörigheter i Cloud Manager](/help/onboarding/cloud-manager-introduction.md#role-based-permissions).

Var och en av produktprofilerna har särskilda behörigheter kopplade till sig.

* **Affärsägare**
   * I den här rollen har du behörighet att lägga till ett nytt program eller redigera ett program, lägga till eller uppdatera en miljö, distribuera kod i AEM-miljön eller utföra kodkvalitetskontroller.
   * Den här användaren ansvarar för att definiera KPI:er, godkänna produktionsdistributioner och åsidosätta viktiga 3-nivåfel vid behov.
* **Distributionshanteraren**
   * I den här rollen har du behörighet att lägga till eller uppdatera en miljö, köra valfri pipeline och distribuera kod till AEM-miljön eller utföra kodkvalitetskontroller.
   * Den här användaren hanterar driftsättningsåtgärder och använder Cloud Manager för att utföra mellanlagrings-/produktionsdistributioner, redigera CI/CD-pipelines, godkänna viktiga 3-skiktsfel vid behov och har åtkomst till Git-databasen.
* **Utvecklare**
   * I den här rollen har du behörighet att skapa personliga åtkomsttoken för åtkomst till Git.
   * Den här användaren utvecklar och testar anpassad programkod och använder främst Cloud Manager för att visa distributionsstatus och har åtkomst till Git-databasen för kodimplementeringar.
* **Programhanteraren**
   * I den här rollen har du behörighet att schemalägga pipelines, åsidosätta de tre skiktens kvalitetsgates och tillhandahålla produktionsgodkännande.
   * Den här användaren använder Cloud Manager för att utföra gruppkonfiguration, granska status, visa KPI:er och kan godkänna viktiga 3-nivåfel när det behövs.

En användare kan tilldelas till flera produktprofiler. Om du till exempel tilldelar en användare både rollen **Affärsägare** och rollen **Distributionshantering** r får användaren summan av dessa behörigheter.

Cloud Manager-teamet kommer att innehålla minst:

* En **Business Owner**, som vanligtvis också är systemadministratör, och som måste vara den första personen som loggar in och får åtkomst till Cloud Manager
* En **Distributionshanterare**
* En **utvecklare**

>[!NOTE]
>
>För att få åtkomst till AEM as a Cloud Service måste användarna tillhöra en av två produktprofiler: `AEM Users` eller `AEM Administrators`. Behörigheter att administrera Cloud Manager räcker inte.

>[!TIP]
>
>* Mer information om Cloud Manager produktprofiler finns i [Tilldela teammedlemmar till Cloud Manager produktprofiler](/help/journey-onboarding/assign-profiles-cloud-manager.md).
>* Mer information om introduktionsprocessen finns i [Startresa](/help/journey-onboarding/overview.md).
