---
title: Beredningsfas i molnaccelerationshanteraren
description: Den här sidan innehåller en översikt över beredskapsfasen i Cloud Acceleration Manager.
source-git-commit: 177e24d20bc97e4a7f2be749771463d7e79005c4
workflow-type: tm+mt
source-wordcount: '670'
ht-degree: 5%

---


# Beredningsfas i molnaccelerationshanteraren {#readiness-phase-cam}

När du har skapat ett projekt i Cloud Acceleration Manager kan du nu starta utvärderingen av den aktuella AEM-implementeringen i beredskapsfasen.

Beredskapsfasen omfattar:

* [Best Practices Analysis](#best-practices-analysis)
* [Planering och installation](#planning-setup)

Följ stegen nedan för att gå till beredskapsfasen:

1. Klicka på projektkortet för att öppna projektstartsidan.

   ![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/cam-landing1.png)

1. Navigera till avsnittet **Beredskap**, som visas i figuren nedan.

   ![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-1.png)

   >[!NOTE]
   >Mer information finns i Skapa och hantera ett projekt i Cloud Acceleration Manager.

## Använda analyskort för metodtips {#best-practices-analysis}

Följ stegen nedan för att använda Best Practices Analysis-kortet:

1. Klicka på knappen **Granska** på **Best Practices Analysis**-kortet.

   ![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-2.png)

1. Följ de här stegen för att hämta BPA (Best Practices Analyzer).

   >[!NOTE]
   >För att undvika att affärskritiska instanser påverkas rekommenderar vi att du kör BPA i en redigeringsmiljö som är så nära produktionsmiljön som möjligt när det gäller anpassningar, konfigurationer, innehåll och användarprogram. Alternativt kan det köras på en klon av författarmiljön i produktion.

   1. Navigera till [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html)-portalen och hämta Best Practices Analyzer som en zip-fil.

      >[!NOTE]
      >Granska [Använda Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en#imp-considerations) för att lära dig hur du kör BPA.

   1. Exportera rapporten i CSV-format

1. Klicka på **Överför ny rapport** för att överföra BPA-rapporten i CAM.

   ![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-3.png)

1. När du har överfört en ny rapport visas rapporten Best Practices Analysis.

   ![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/cam-bpareport.png)

1. Granska och utforska kontrollpanelen Best Practices Analysis i CAM. Mer information finns i avsnittet [Analysrapport om metodtips](#analysis-report) nedan.

   >[!NOTE]
   >När du överför en ny rapport återställs alla bedömningar.

### Analysrapport om metodtips för granskning {#analysis-report}

Utforska följande kort som finns på sidan Best Practices Analysis Report:

![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/cam-bpareport.png)

>[!NOTE]
> Med varje kort kan du
>* klicka på varje kort för att öppna den tillhörande fliken
>* bokmärk alla rapportflikar (inklusive filtrering) för delning eller framtida hämtning
>* använda informationsikonen för att visa information om varje rapportsökning


#### Rapportegenskaper {#report-properties}

Kortet **Rapportegenskaper** innehåller information om rapportegenskaper som rapportdatum, varaktighet, filter, överföringsdatum och information om Adobe Experience Manager (AEM).

![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-properties.png)

#### Rapportöversikt {#report-overview}

Detta **rapportöversiktskort** innehåller rapportresultat och allvarlighetsnivåer som gäller vid bedömning av om AEM kan flyttas som en Cloud Service, vilket visas i figuren nedan.

![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-overview.png)

Om du klickar på den här rapporten öppnas fliken **Rapport**.

![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-overview2.png)

Du kan filtrera rapporten baserat på prioritet, undertyp eller antal.

![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/report-overview3.png)

>[!NOTE]
>Läs [Tolka rapporten Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html?lang=en) om du vill veta mer om felkategorier och prioritetsnivåer.

#### Utvärdering av bästa praxis {#best-practices-assessment}

Alternativet Best Practices Assessment (Utvärdering av bästa praxis) ger en bedömning av din aktuella AEM och ger vägledning om nästa steg för att anta AEM bästa praxis. Du kan granska följande information på den här fliken:

* Översikt över AEM
* Anpassade komponenter och mallar
* Ytterligare resultat
* Långsamma frågor
* Underhållsåtgärder

#### Utvärdering av migreringskomplexitet {#migration-complexity-assessment}

Med alternativet Utvärdering av migreringskomplexitet kan du bedöma hur komplicerat det är att migrera den befintliga AEM till AEM som en Cloud Service.

Du kan granska följande information på den här fliken:

* Översikt över AEM
* Bedömning
* Överväganden vid innehållsmigrering

   ![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/migration-complexity-1.png)

## Använda Planera och konfigurera kort {#planning-setup}

Följ det här avsnittet för att utforska aktivitetskortet Planning and Setup.

1. Klicka på knappen **Visa** på **Planering och inställningar**-kortet. Det här kortet innehåller allt relevant innehåll som hjälper dig att planera och konfigurera din AEM migrering.

   ![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-view.png)

1. En innehållskarusell visar all relevant information för den här fasen av migreringsresan.

   ![bild](/help/move-to-cloud-service/cloud-acceleration-manager/assets/readiness-5-planning.png)

## What&#39;s Next {#whats-next}

När du har lärt dig hur du loggar in i Cloud Acceleration Manager och hur du skapar ett projekt är du nu redo att gå vidare till nästa steg i [implementeringsfasen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/moving/cloud-acceleration-manager/using-cam/cam-implementation-phase.html?lang=en).
