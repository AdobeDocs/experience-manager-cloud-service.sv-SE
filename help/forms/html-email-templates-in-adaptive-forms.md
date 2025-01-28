---
title: HTML e-postmallar i adaptiv Forms på Forms as a Cloud Service
description: Lär dig använda e-postmallar med adaptiva formulär.
feature: Adaptive Forms, Core Components
role: User, Developer
hide: true
hidefromtoc: true
source-git-commit: b5340c23f0a2496f0528530bdd072871f0d70d62
workflow-type: tm+mt
source-wordcount: '756'
ht-degree: 0%

---

# E-postmallar i Adaptiv Forms

Med anpassningsbara Forms kan du använda e-postmallar för HTML och oformaterad text. Med HTML e-postmallar kan du skicka snygga, personliga och visuellt tilltalande e-postmeddelanden när ett formulär skickas. Dessa e-postmeddelanden kan anpassas med formulärdata och förbättras med olika e-posttaggar, som bilder och länkar. Med Adaptive Forms kan du antingen ladda upp en fil som innehåller en HTML-mall eller använda en vanlig textredigerare för att skapa mallarna.

![HTML e-postmallar](/help/forms/assets/html-email.png)

Den här artikeln hjälper dig att konfigurera och använda e-postmallar i Adaptive Forms. Till slut kan du

* [Konfigurera en HTML-mall för ett anpassat formulär](#configure-an-html-template-for-an-adaptive-form)
* [Konfigurera en e-postmall med oformaterad text för ett anpassat formulär](#configure-a-plain-text-template-for-an-adaptive-form)
* [Använd formulärdata i e-postmallar](#use-form-data-in-your-email-templates)


Här följer en kort översikt över de olika stegen:

1. Öppna det adaptiva formuläret för redigering.
1. Konfigurera sändningsåtgärden [Skicka e-post](/help/forms/configure-submit-action-send-email.md).
1. Markera eller överför en HTML-mall eller ange e-postmallen manuellt.
1. Testa din e-postkonfiguration.

## Konfigurera en HTML-mall för ett anpassat formulär

Du kan konfigurera ett anpassat formulär så att ett e-postmeddelande skickas när det skickas med [**Skicka e-post**-åtgärden ](/help/forms/configure-submit-action-send-email.md). Åtgärden innehåller två metoder för att konfigurera en HTML-mall:

### Alternativ 1: Markera en fil som innehåller HTML-mallen

Innan du fortsätter kontrollerar du att du har överfört HTML-mallen till din AEM Forms-miljö.

1. Öppna det adaptiva formuläret för redigering.
1. Gå till **Content Browser**, markera **Guide Container** och tryck på egenskapsikonen. En dialogruta med titeln `Adaptive Form Container` visas.
1. Gå till fliken **Skicka** och välj åtgärden **Skicka e-post**.

   ![Åtgärden Skicka e-post](/help/forms/assets/send-email-action.png)

1. Aktivera alternativet **Använd extern mall**.
1. Aktivera alternativet **Använd HTML-mall**.
1. Klicka på mappikonen för alternativet Extern mallsökväg och bläddra för att välja mallen för HTML.
1. Klicka på **Klar** för att spara konfigurationen.

Din HTML-mall har nu konfigurerats för det anpassade formuläret.

### Alternativ 2: Ange eller klistra in en HTML-mall manuellt

1. Öppna det adaptiva formuläret för redigering.
1. Gå till **Content Browser**, markera **Guide Container** och tryck på egenskapsikonen. En dialogruta med titeln `Adaptive Form Container` visas.
1. Gå till fliken **Skicka** och välj åtgärden **Skicka e-post**.
1. Aktivera alternativet **Använd HTML-mall**.
1. Skriv eller klistra in HTML-koden direkt i rutan **E-postmall** .


## Konfigurera en vanlig textmall för ett anpassat formulär

Du kan konfigurera ett anpassat formulär så att ett e-postmeddelande skickas när det skickas med [**Skicka e-post**-åtgärden ](/help/forms/configure-submit-action-send-email.md). Åtgärden innehåller två metoder för att konfigurera en oformaterad textmall:

### Alternativ 1: Välj en fil som innehåller mallen

Innan du fortsätter kontrollerar du att du har överfört HTML-mallen till din AEM Forms-miljö.

1. Öppna det adaptiva formuläret för redigering.
1. Gå till **Content Browser**, markera **Guide Container** och tryck på egenskapsikonen. En dialogruta med titeln `Adaptive Form Container` visas.
1. Gå till fliken **Skicka** och välj åtgärden **Skicka e-post**.
1. Aktivera alternativet **Använd extern mall**.
1. Klicka på mappikonen för alternativet **Extern mallsökväg** och bläddra till mallen för oformaterad text.
1. Klicka på Klar för att spara konfigurationen.

Din mall har nu konfigurerats för det adaptiva formuläret.

### Alternativ 2: Ange eller klistra in en HTML-mall manuellt

1. Öppna det adaptiva formuläret för redigering.
1. Gå till **Content Browser**, markera **Guide Container** och tryck på egenskapsikonen. En dialogruta med titeln `Adaptive Form Container` visas.
1. Gå till fliken **Skicka** och välj åtgärden **Skicka e-post**.
1. Skriv eller klistra in den oformaterade mallkoden direkt i rutan **E-postmall** .

## Använd formulärdata i dina e-postmallar

Du kan inkludera formulärdata i e-postmallar med hjälp av platshållare. Dessa platshållare ersätts dynamiskt med faktiska formulärfältsvärden när e-postmeddelandet skickas. Till exempel:

* ${name}: Värdet för fältet med namnet &quot;name&quot;.
* ${email}: Värdet för fältet med namnet &quot;email&quot;.
* ${message}: Värdet för fältet med namnet &quot;message&quot;.

### E-postmall för HTML som exempel

Här är ett exempel på en HTML-e-postmall som använder platshållare för formulärdata:

```HTML
    <!DOCTYPE html>
    <html>
    <head>
        <title>Form Submission</title>
        <style>
            body {
                font-family: Arial, sans-serif;
                line-height: 1.6;
                color: #333;
            }
            h2 {
                color: #0056b3;
            }
        </style>
    </head>
    <body>
        <h2>Thank You for Your Submission</h2>
        <p>Dear ${name},</p>
        <p>We have received your submission with the following details:</p>
        <ul>
            <li><strong>Email:</strong> ${email}</li>
            <li><strong>Phone Number:</strong> ${phone_number}</li>
            <li><strong>Message:</strong> ${message}</li>
        </ul>
        <p>We will get back to you soon!</p>
        <p>Best regards,</p>
        <p>Your Team</p>
    </body>
    </html>
```

### Exempelmall för e-post med oformaterad text

Här är ett exempel på en e-postmall med oformaterad text:

```TXT
    
    Subject: Thank You for Your Submission
    
    Dear ${name},
    
    We have received your submission with the following details:
    
    - Email: ${email}
    - Phone Number: ${phone_number}
    - Message: ${message}
    
    We will get back to you soon!
    
    Best regards,
    Your Team
```

## Bästa praxis för e-postmallar för HTML

* Se till att formaten är textbundna för bättre kompatibilitet med e-postklienter.
* Gör mallen responsiv för en bättre upplevelse på mobila enheter.
* Använd verktyg som Litmus eller Email on Acid för att förhandsgranska din e-post i olika e-postklienter.
* Kontrollera att platshållarnamnen matchar formulärfältsnamnen exakt.
* Kontrollera om taggarna saknas eller är felaktiga i HTML-mallen.
* Kontrollera att sändningsåtgärden [Skicka e-post](/help/forms/configure-submit-action-send-email.md) är korrekt konfigurerad.
