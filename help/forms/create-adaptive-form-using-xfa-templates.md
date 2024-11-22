---
title: Hur skapar man ett adaptivt formulär baserat på kärnkomponenter med hjälp av XFA-formulärmallar?
description: Lär dig hur du skapar ett adaptivt formulär med  [!DNL Experience Manager Forms] hjälp av XFA-formulärmallar eller XDP-filer.
feature: Adaptive Forms, Core Components
role: User, Developer
level: Beginner
exl-id: f3c9b798-8b20-4674-9b96-a3a0b143d947
source-git-commit: 10de700e5e4b352051b8b77dfd0825bb9b6e0219
workflow-type: tm+mt
source-wordcount: '699'
ht-degree: 0%

---

# Skapa ett adaptivt formulär (kärnkomponenter) baserat på XFA-formulärmallar

<span class="preview"> Funktionen är tillgänglig i ett program för tidig användning. Du kan skriva till aem-forms-ea@adobe.com från ditt officiella e-post-id för att gå med i det tidiga adopterprogrammet och begära åtkomst till funktionen. </span>

AEM as a Cloud Service ger användarna möjlighet att skapa adaptiv Forms baserat på kärnkomponenter med hjälp av XFA-formulärmallar (XML Forms Architecture) eller `*.XDP`-filer (XML Data Package). Med den här funktionen kan användare spara tid genom att migrera fält från XFA-formulärmallar eller XDP-filer direkt till Adaptiv Forms.

Du kan återanvända formulärmallar från XFA eller XDP-filer för att skapa adaptiva Forms baserade på kärnkomponenter. Om du vill återanvända, överför och associerar du en XFA-formulärmall eller XDP-filer med ett adaptivt formulär. Elementen i XFA-formulärmallen eller XDP-filer blir tillgängliga för användning i innehållssökaren vid redigering av adaptiva formulär. I Innehållssökaren kan du dra och släppa formulärmallselementen i formuläret.

## Fördelar med att skapa formulär baserade på XFA-formulärmallar eller XDP-filer

Några av fördelarna med att skapa formulär baserade på XFA-formulärmallar eller XDP-filer är:

* **Tidsbesparingar**: Du kan snabbt återanvända befintliga XFA-formulärmallar (XDP-filer) utan att behöva återskapa formulärstrukturen, vilket sparar tid och arbete under redigeringsprocessen.
* **Smidig migrering**: Om du redan har XFA-formulärmallar i användning är det här alternativet en enkel migreringsväg till Adaptive Forms, vilket gör att du kan dra nytta av fördelarna med moderna AEM Core Components utan att förlora befintliga formulärdata och logik.
* **Förbättrad användarupplevelse**: Adaptiv Forms är mer responsiv och anpassningsbar än XFA-formulär. Genom att gå över till Adaptiv Forms kan du skapa en användarvänlig upplevelse för olika enheter och skärmstorlekar.
* **Förbättrad integrering**: Adaptiv Forms är bättre integrerat med andra funktioner, som arbetsflöden, databindning och formulärinskickning, vilket ger smidigare arbetsflöden och bättre övergripande formulärhantering.

## Krav

Du behöver följande för att skapa ett adaptivt formulär baserat på kärnkomponenter med hjälp av XFA-formulärmallar eller XDP-filer:

* [Aktivera adaptiva Forms Core-komponenter för din miljö](enable-adaptive-forms-core-components.md).
* Du bör känna till följande områden:
   * Skapa ett anpassat formulär
   * XFA (XML Forms Architecture)

## Hur skapar man ett adaptivt formulär med XFA-formulärmallar eller XDP-filer?

Så här skapar du ett adaptivt formulär med hjälp av XFA- eller XDP-formulärmallar:

1. Logga in på din [!DNL Experience Manager Forms]-författarinstans.
1. Ange dina uppgifter på inloggningssidan för Experience Manager. När du är inloggad väljer du **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms & Documents]** i det övre vänstra hörnet.

   ![Forms och dokument](/help/forms/assets/create-fdm.png)

1. Välj **[!UICONTROL Create]** > **[!UICONTROL Adaptive Forms]**.

   ![Skapa anpassat formulär](/help/forms/assets/create-af.png)

   Guiden Skapa formulär öppnas.
1. På fliken **Source** väljer du en mall baserad på kärnkomponenter.

   ![Välj mall](/help/forms/assets/select-template.png)

   När du väljer en mall markeras automatiskt ett tema och en skicka-åtgärd som anges i mallen och knappen **[!UICONTROL Create]** aktiveras.

   ![Välj tema](/help/forms/assets/select-form-theme.png)

1. Välj **[!UICONTROL Create]**. En dialogruta med namn, namn och plats för att spara det anpassade formuläret visas.
1. Ange titel, namn och plats.
1. Välj **[!UICONTROL Create]**.
   ![Ange namn och titel](/help/forms/assets/create-form.png)

   Ett adaptivt formulär skapas och öppnas i den adaptiva Forms-redigeraren. Redigeraren visar det innehåll som är tillgängligt i mallen.
1. Välj ![Sidinformation](/help/forms/assets/Smock_Properties_18_N.svg) > **[!UICONTROL Open Properties]**.

   ![Öppna egenskaper](/help/forms/assets/form-properties.png)

   Sidan Formuläregenskaper öppnas.
1. Gå till fliken **[!UICONTROL Form Model]** och välj **Formulärmallar**.
1. Välj XDP-filen i listrutan.

   ![Välj XDP-fil](/help/forms/assets/select-xdp-file.png)

   En varningsdialogruta visas på skärmen. Klicka på **OK** om du vill fortsätta.

   ![Varningsdialogruta](/help/forms/assets/fdm-warning.png)

1. Välj **[!UICONTROL Save & Close]** om du vill spara egenskaperna.

   >[!NOTE]
   >
   > När du har valt **Formulärmallar** på fliken **Formulärmodell** kan du inte ändra den.


Ett adaptivt formulär skapas och öppnas i den adaptiva Forms-redigeraren. Redigeraren visar det innehåll som är tillgängligt i mallen.  Baserat på typen av anpassat formulär visas formulärelementen i den associerade XFA-formulärmallen på fliken **[!UICONTROL Data Model Objects]** i **[!UICONTROL Content Browser]** i sidlisten. Du kan också dra och släppa dessa element för att skapa ett anpassat formulär.

>[!NOTE]
>
> Du kan inaktivera skript för XDP-formulärfält med panelens verktygsfält i det tillagda fältet. Skapa logik för de tillagda fälten med [redigeraren för visuell regel](/help/forms/rule-editor-core-components.md).

## Se även

{{see-also}}
* [Lägga till dynamiskt beteende i formulär med regelredigeraren](/help/forms/rule-editor-core-components.md)
