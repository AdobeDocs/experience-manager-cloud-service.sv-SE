---
title: Komma igång med HTML5-formulär
description: Börja med att distribuera AEM Forms tilläggspaket och importera befintliga HTML5-formulär till AEM.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: f276d150-8936-4bfb-8475-7ca36815b233
feature: HTML5 Forms,Mobile Forms
exl-id: a3245f05-6ea3-4f90-8981-bfa89d2e7335
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 22aeedaaf4171ad295199a989e659b6bf5ce9834
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 0%

---

# Komma igång med HTML5-formulär {#getting-started-with-html-forms}

<span class="preview"> Funktionen HTML5 Forms erbjuds som en del av programmet för tidig åtkomst. Om du vill begära åtkomst skickar du ett e-postmeddelande från din officiella (arbets) e-post till aem-forms-ea@adobe.com.
</span>

HTML5-blanketter har många funktioner som är mobilklara. Det hjälper er att utöka era nuvarande lösningar och arbetsflöden till surfplattor och smarttelefoner med HTML5-webbläsare. Några av funktionerna är:

* **HTML5-baserad återgivning av XFA-formulärmallar:** Förutom vanliga PDF forms kan du nu återge dina befintliga XFA-baserade formulär i HTML5-format. Det hjälper dig att utöka klientplattformen till mobila enheter (Apple iPad, Android-surfplatta, smarttelefoner och så vidare) som stöder HTML5 och som inte stöder Adobe Reader med XFA Forms. Mer information om HTML5-baserad återgivning finns i [Introduktion till HTML5-formulär](/help/forms/introductionhtml5.md).

* **Hantera Forms:** Dessutom innehåller AEM nya funktioner för att förenkla hanteringen av och organisera formulär. Du kan aktivera, inaktivera, publicera och förhandsgranska formulär.<!--For more information, see [Introduction to managing forms](/help/forms/using/introduction-managing-forms.md).-->

## Konfigurera miljön för HTML5-formulär {#installing-html-forms}

Så här aktiverar du formulärinskickning och korrekt återgivning av HTML5 Forms:

* **Lägg till dispatcherfilter:** Uppdatera `src/conf.dispatcher.d/filters/filters.any`-filen så att nödvändiga begäranden för HTML5 Forms tillåts. Lägg till följande filterregler:

  ```
  /0103 { /type "allow" /method '(HEAD|POST)' /url "/content/xfaforms/profiles/default.submit.html" }  # allow POSTs to form selectors under content
  /0104 { /type "allow" /method '(GET|HEAD|POST)' /url "/*.xdp.html" }
  ```

* **Lägg till ett paket som ska skickas:** I projektet lägger du till ett paket i mappen `src/main/content/jcr_root/content` som har stöd för formuläröverföringsfunktioner.

* **Importera HTML5 Forms:** Importera formulär från det lokala filsystemet till AEM Forms.
