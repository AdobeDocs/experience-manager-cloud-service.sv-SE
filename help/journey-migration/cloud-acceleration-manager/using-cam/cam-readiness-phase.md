---
title: Beredskapsfas i Cloud Acceleration Manager
description: På den här sidan finns en översikt över beredskapsfasen i Cloud Acceleration Manager.
exl-id: 2583985b-0358-433c-9d31-38e2c60dc3dc
feature: Migration
role: Admin
source-git-commit: 90f7f6209df5f837583a7225940a5984551f6622
workflow-type: tm+mt
source-wordcount: '1045'
ht-degree: 2%

---

# Beredskapsfas i Cloud Acceleration Manager {#readiness-phase-cam}

När du har skapat ett projekt i Cloud Acceleration Manager (CAM) kan du nu starta utvärderingen av din nuvarande implementering av Adobe Experience Manager (AEM) i beredskapsfasen.

Beredskapsfasen omfattar:

* [Best Practices Analysis](#best-practices-analysis)
* [Planering och installation](#planning-setup)

Följ stegen nedan för att navigera till beredskapsfasen:

1. Klicka på ditt projektkort.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/cam-landing1.png)

1. Navigera till avsnittet **Beredskap** på projektstartsidan, vilket visas i figuren nedan.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/readiness-1.png)

   >[!NOTE]
   >Mer information finns i Skapa och hantera ett projekt i Cloud Acceleration Manager.

## Använda analyskort för metodtips {#best-practices-analysis}

>[!CONTEXTUALHELP]
>id="aemcloud_cam_bpa"
>title="Analysrapport för bästa praxis"
>abstract="BPA-rapporten kan laddas upp till CAM för att ge en analys av den med avseende på migrering till AEM as a Cloud Service."
>additional-url="https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer" text="Använda Best Practices Analyzer"

1. Klicka på **Granska** på kortet **Best Practices Analysis**.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/readiness-2.png)

1. Hämta BPA (Best Practices Analyzer).

   >[!NOTE]
   >För att undvika att affärskritiska instanser påverkas rekommenderar Adobe att du kör BPA i en redigeringsmiljö. Miljön bör vara så nära produktionsmiljön som möjligt när det gäller anpassningar, konfigurationer, innehåll och användarapplikationer. Alternativt kan det köras på en klon av produktionsredigeringsmiljön.

   1. Navigera till portalen [Programvarudistribution](https://experience.adobe.com/#/downloads/content/software-distribution/en/aemcloud.html?fulltext=best*) och hämta Best Practices Analyzer som en zip-fil.

      >[!NOTE]
      >Granska [Använda Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html#imp-considerations) för att lära dig hur du kör BPA.

1. I CAM klickar du på **Hämta överföringsnyckel** så att du kan hämta nyckeln som används för att konfigurera systemet så att BPA-rapporter automatiskt överförs till CAM.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/readiness-3b.png)

   >[!IMPORTANT]
   >Rapporten kan fortfarande överföras manuellt, men med Överföringsnyckel effektiviseras åtgärden. Observera att rapporten inte kan överföras manuellt om du är i webbläsarens Incognito-läge.

1. När en ny rapport har överförts kan du se rapporten Best Practices Analysis i CAM.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/cam-bpareport.png)

   >[!NOTE]
   >Om flera olika rapporter överförs är rapporten som visas i detalj alltid den som har det senaste skapandedatumet (inte överföringsdatumet).

1. Granska och utforska kontrollpanelen Best Practices Analysis i CAM. Mer information finns i [Analysrapport om metodtips](#analysis-report).

   >[!NOTE]
   >När du överför en ny rapport återställs alla bedömningar om den är nyare än den tidigare inlästa rapporten.

### Använda Förhandsgranska {#print-preview-cam}

Du kan välja alternativet för förhandsgranskning i Cloud Acceleration Manager för att få en utskrivbar förhandsgranskning av rapporterna eller för att skriva ut rapporten i PDF-format för att underlätta fildelningen.

Följ stegen nedan:

1. Klicka på åtgärden **Förhandsgranska**.

   ![bild](/help/journey-migration/best-practices-analyzer/assets/bpa-printpreview1b.png)

1. Klicka på **Skriv ut** för att skriva ut rapporten i PDF-format på den nya fliken där rapporten visas i en förhandsgranskning som går att skriva ut.

   >[!IMPORTANT]
   >
   >* Alternativet **Spara som PDF** rekommenderas och stöds för ovanstående funktioner.
   >* Om webbläsarens utskriftsknapp används skrivs bara en sida ut.

   ![bild](/help/journey-migration/best-practices-analyzer/assets/bpa-printpreview2.png)

### Använda Visa trendlinje {#trendline-view-cam}

När du överför mer än en separat BPA-rapport (Best Practices Analyzer) till ett projekt kan du välja alternativet **Visa trendlinje** om du vill visa och jämföra resultat från historiska BPA-rapporter.

Följ stegen nedan för att visa rapporter från trendlinjealternativet:

>[!NOTE]
>När du överför mer än en distinkt BPA-rapport i ett projekt visas ikonen **..** . Rapporterna betraktas som samma (inte distinkta) om deras värdtid och skapandetid är desamma.

1. Navigera till ditt projekt och klicka på **Granska** på kortet **Best Practices Analysis** i fasen **Beredskap**.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1a.png)

1. Klicka på **Trendlinjerapport** i listrutan **Visa**, vilket visas i figuren nedan.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1b.png)

1. Om du klickar på **Trendlinjerapport** öppnas trendlinjevyn för rapporten.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view3a.png)


   >[!NOTE]
   >Trendlinjerapporten visar resultaten från de historiska BPA-rapporterna i en grafisk representation.
   >
   >Du ser två diagram som visar trenden för:
   > 
   >1. **Rapportera resultattrend**
   >1. **Anpassade komponenter och malltrend**
   >
   >Du kan lägga till eller ändra den grafiska vyn med hjälp av listrutan, vilket visas i bilden nedan:
   >![bild](/help/journey-migration/cloud-acceleration-manager/assets/reports-bpa1.png)


### Analysrapport om metodtips för granskning {#analysis-report}

Utforska följande kort som finns på sidan Best Practices Analysis Report:

![bild](/help/journey-migration/cloud-acceleration-manager/assets/cam-bpareport.png)

>[!NOTE]
> Med varje kort kan man
>
>* öppna tillhörande flik
>* bokmärk alla rapportflikar (inklusive filtrering) för delning eller framtida hämtning
>* använda informationsikonen för att visa information om varje rapportsökning

#### Rapportegenskaper {#report-properties}

Kortet **Rapportegenskaper** innehåller information om rapportegenskaper som rapportdatum, varaktighet, filter, överföringsdatum och Adobe Experience Manager-information (AEM).

![bild](/help/journey-migration/cloud-acceleration-manager/assets/report-properties.png)

#### Rapportöversikt {#report-overview}

Kortet **Rapportöversikt** innehåller rapportresultat och allvarlighetsnivåer som gäller vid bedömning av om du är redo att flytta till AEM as a Cloud Service, vilket visas i bilden nedan.

![bild](/help/journey-migration/cloud-acceleration-manager/assets/report-overview.png)

Om du klickar på den här rapporten öppnas fliken **Rapport**.

![bild](/help/journey-migration/cloud-acceleration-manager/assets/report-overview2.png)

Du kan filtrera rapporten baserat på prioritet, undertyp eller antal.

![bild](/help/journey-migration/cloud-acceleration-manager/assets/report-overview3.png)

>[!NOTE]
>Läs [Tolka rapporten om Best Practices Analyzer](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-migration/best-practices-analyzer/using-best-practices-analyzer.html) om du vill veta mer om kategorier och prioritetsnivåer.

#### Utvärdering av bästa praxis {#best-practices-assessment}

Alternativet Best Practices Assessment (Utvärdering av bästa praxis) ger en bedömning av din aktuella AEM och ger vägledning om nästa steg för att anta AEM bästa praxis. Du kan granska följande information på den här fliken:

* AEM - översikt
* Anpassade komponenter och mallar
* Ytterligare resultat
* Långsamma frågor
* Underhållsaktiviteter

#### Utvärdering av migreringskomplexitet {#migration-complexity-assessment}

Med alternativet Utvärdering av migreringskomplexitet kan du bedöma hur komplicerat det är att migrera den befintliga AEM till AEM as a Cloud Service.

Du kan granska följande information på den här fliken:

* AEM - översikt
* Utvärdering
* Överväganden vid innehållsmigrering

  ![bild](/help/journey-migration/cloud-acceleration-manager/assets/migration-complexity-1.png)

## Använda Planera och konfigurera kort {#planning-setup}

1. Klicka på **Visa** på kortet **Planering och installation**. Det här kortet innehåller allt relevant innehåll som hjälper dig att planera och konfigurera AEM migrering.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/readiness-view.png)

1. En innehållskarusell visar all relevant information för den här fasen av migreringsresan.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/readiness-5-planning.png)

### Ta bort en analysrapport om bästa praxis från trendlinjevyn {#delete-trendline}

>[!IMPORTANT]
>En rapport kan bara tas bort när mer än en rapport har överförts till ett projekt.

1. Navigera till ditt projekt och klicka på **Granska** på kortet **Best Practices Analysis** i fasen **Beredskap**.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1a.png)

1. Klicka på **..**.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1.png)

1. Klicka på **Visa trendlinje** i listrutan, vilket visas i figuren nedan.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view1b.png)

1. Klicka på ikonen Ta bort på skärmen **Trendlinjerapport**.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view5a.png)

1. Klicka på **Ta bort** för att bekräfta borttagningen.

   ![bild](/help/journey-migration/cloud-acceleration-manager/assets/trendline-view6a.png)

## What&#39;s Next {#whats-next}

När du har lärt dig hur du loggar in på Cloud Acceleration Manager och hur du skapar ett projekt är du nu redo att gå vidare till nästa steg i [implementeringsfasen](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/migration-journey/cloud-acceleration-manager/using-cam/cam-implementation-phase.html).
