---
title: Edge Delivery Services för ofta använda regex-uttryck i AEM Forms för validering av formulärfält
description: Edge Delivery Services för ofta använda regex-uttryck i AEM Forms för validering av formulärfält
feature: Edge Delivery Services
role: User
hide: true
hidefromtoc: true
exl-id: 5cfe23bb-155f-4639-b7b7-5edc172ba92a
source-git-commit: 4a8153ffbdbc4da401089ca0a6ef608dc2c53b22
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 0%

---

# Vanliga regex-uttryck för validering

Här är några reguljära uttryck som du kan använda för att förbättra formulärvalideringen utöver vad moderna webbläsare erbjuder:

## Starkt lösenord

```regex
^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)(?=.*[@$!%*?&])[A-Za-z\d@$!%*?&]{8,}$
```

Ser till minst 8 tecken med:

* Gemener (a-z)
* Versaler (A-Z)
* Siffra (0-9)
* Specialtecken (@$)%*?&amp;)


## E-postadress


```regex
^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$
```

Tillåter bokstäver, siffror och specialtecken i användarnamnet och domännamnet.


## Telefonnummer (US-format)

```regex
^\(?([0-9]{3})\)?[-. ]([0-9]{3})[-. ]([0-9]{4})$
```

Validerar telefonnummer i formatet (XXX) XXX-XXXX.



## URL

```regex
^(http|https)://.*$
```

Garanterar en giltig URL som börjar med http eller https.



## Datum (ÅÅÅ-MM-DD)

```regex
^\d{4}-(0[1-9]|1[0-2])-(0[1-9]|[12][0-9]|3[01])$
```

Validerar i formatet ÅÅÅ-MM-DD.


## Tid (TT:MM)

```regex
^([01][0-9]|2[0-3]):[0-5][0-9]$
```

Validerar tider i formatet HH:MM (24-timmarsformat).


## Postnummer (USA-format)

```regex
^\d{5}(?:[-\ ]\d{4})?$
```

Validerar femsiffriga amerikanska postnummer med bindestreck och fyrsiffrigt filtillägg.


## Användarnamn (alfanumeriskt och understreck)

```regex
^[a-zA-Z0-9_]+$
```

Tillåter bokstäver, siffror och understreck.


## Hex-kod för färg

```regex
^#[0-9a-fA-F]{6}$
```

Validerar sexsiffriga hexadecimala färgkoder. Exempel: #FFFFFF.


## IP-adress

```regex
^(25[0-5]|2[0-4][0-9]|1[0-9][0-9]|[0-9]{2,3})\.(25[0-5]|2[0-4][0-9]|1[0-9][0-9]|[0-9]{2,3})\.(25[0-5]|2[0-4][0-9]|1[0-9][0-9]|[0-9]{2,3})\.(25[0-5]|2[0-4][0-9]|1[0-9][0-9]|[0-9]{2,3})$
```

Validerar IPv4-adresser.



## Personnummer (US-format)

```regex
^\d{3}-\d{2}-\d{4}$
```



## Kreditkortsnummer

```regex
^(?:4[0-9]{12}(?:[0-9]{3})?|[25][1-7][0-9]{14}$
```

Validerar telefonnummer i formatet (XXX) XXX-XXXX.



## Telefonnummer (US-format):

```regex
^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$
```

Validerar telefonnummer i formatet (XXX) XXX-XXXX.
