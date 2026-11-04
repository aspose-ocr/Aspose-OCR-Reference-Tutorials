---
category: general
date: 2026-04-26
description: Maskeer creditcardnummers snel met AsposeAI OCR‑nabewerking. Leer PCI‑compliance,
  masking met reguliere expressies en gegevenssanitatie in een stapsgewijze tutorial.
draft: false
keywords:
- mask credit card numbers
- PCI compliance
- OCR post‑processing
- AsposeAI
- regular expression masking
- data sanitization
language: nl
og_description: Maskeer creditcardnummers in OCR‑resultaten met AsposeAI. Deze tutorial
  behandelt PCI‑naleving, maskering met reguliere expressies en gegevenssanitatie.
og_title: Creditcardnummers maskeren – Complete Python OCR-nabewerkingsgids
tags:
- OCR
- Python
- security
title: Maskeer creditcardnummers in OCR‑uitvoer – Complete Python‑gids
url: /nl/python/general/mask-credit-card-numbers-in-ocr-output-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Creditcardnummers maskeren – Complete Python-gids

Heb je ooit **creditcardnummers moeten maskeren** in tekst die rechtstreeks uit een OCR‑engine komt? Je bent niet de enige. In gereguleerde sectoren kan het blootstellen van een volledige PAN (Primary Account Number) je in de problemen brengen bij PCI‑compliance‑auditors. Het goede nieuws? Met een paar regels Python en de post‑processing‑hook van AsposeAI kun je automatisch de middelste acht cijfers verbergen en veilig blijven.

In deze tutorial lopen we door een real‑world scenario: OCR uitvoeren op een bonafbeelding, vervolgens een aangepaste **OCR post‑processing** functie toepassen die alle PCI‑gegevens sanitiseert. Aan het einde heb je een herbruikbare snippet die je in elke AsposeAI‑workflow kunt plaatsen, plus een reeks praktische tips voor het omgaan met randgevallen en het opschalen van de oplossing.

## Wat je zult leren

- Hoe je een aangepaste post‑processor registreert bij **AsposeAI**.
- Waarom een **regular expression masking** aanpak zowel snel als betrouwbaar is.
- De basisprincipes van **PCI compliance** met betrekking tot data‑sanitization.
- Manieren om het patroon uit te breiden voor meerdere kaartformaten of internationale nummers.
- Verwachte output en hoe je kunt verifiëren dat de maskering heeft gewerkt.

> **Prerequisites** – Je moet een werkende Python 3‑omgeving hebben, het Aspose.AI for OCR‑pakket geïnstalleerd (`pip install aspose-ocr`), en een voorbeeldafbeelding (bijv. `receipt.png`) die een creditcardnummer bevat. Er zijn geen andere externe services vereist.

---

## Stap 1: Definieer een post‑processor die creditcardnummers maskert

Het hart van de oplossing zit in een kleine functie die het OCR‑resultaat ontvangt, een **regular expression masking** routine uitvoert, en de gesaniteerde tekst retourneert.

```python
def mask_pci(data, settings):
    """
    Replace the middle 8 digits of any 16‑digit card number with asterisks.
    Keeps the first and last four digits visible for reference.
    """
    import re
    # Pattern captures groups: first 4 digits, middle 8, last 4
    pattern = r'(\d{4})\d{8}(\d{4})'
    # Replace middle portion with ****
    return re.sub(pattern, r'\1****\2', data.text)
```

**Waarom dit werkt:**  
- De regex `(\d{4})\d{8}(\d{4})` komt exact overeen met 16 opeenvolgende cijfers, het gangbare formaat voor Visa, MasterCard en vele anderen.  
- Door de eerste en laatste vier cijfers vast te leggen (`\1` en `\2`) behouden we voldoende informatie voor debugging, terwijl we voldoen aan **PCI compliance** regels die het opslaan van de volledige PAN verbieden.  
- De substitutie `\1****\2` verbergt de gevoelige middelste acht cijfers, waardoor `1234567812345678` wordt `1234****5678`.

> **Pro tip:** Als je 15‑cijferige American Express‑nummers moet ondersteunen, voeg dan een tweede patroon toe zoals `r'(\d{4})\d{6}(\d{5})'` en voer beide vervangingen opeenvolgend uit.

## Stap 2: Initialise de AsposeAI‑engine

Voordat we onze post‑processor kunnen koppelen, hebben we een instantie van de OCR‑engine nodig. AsposeAI bundelt het OCR‑model en een eenvoudige API voor aangepaste verwerking.

```python
from aspose.ocr import AsposeAI

# Initialise the AI engine – it will handle image loading, recognition, and post‑processing
ai = AsposeAI()
```

**Waarom hier initialiseren?**  
Het één keer aanmaken van het `AsposeAI`‑object en hergebruiken ervan over meerdere afbeeldingen vermindert overhead. De engine cachet ook taalmodellen, wat latere oproepen versnelt—handig wanneer je batches bonnen scant.

## Stap 3: Registreer de aangepaste maskeringsfunctie

AsposeAI biedt een `set_post_processor`‑methode die je in staat stelt elke callable in te pluggen. We geven onze `mask_pci`‑functie door samen met een optioneel instellingen‑dictionary (nu leeg).

```python
# Register our masking routine; custom_settings can hold flags like "log_masked" if you expand later
ai.set_post_processor(mask_pci, custom_settings={})
```

**Wat gebeurt er achter de schermen?**  
Wanneer je later `run_postprocessor` aanroept, geeft AsposeAI het ruwe OCR‑resultaat door aan `mask_pci`. De functie ontvangt een lichtgewicht object (`data`) dat de herkende tekst bevat, en je retourneert een nieuwe string. Dit ontwerp houdt de kern‑OCR onaangeroerd terwijl je **data sanitization**‑beleid op één plek kunt afdwingen.

## Stap 4: Voer OCR uit op de bonafbeelding

Nu de engine weet hoe de output te reinigen, voeren we een afbeelding in. Voor deze tutorial gaan we ervan uit dat je al een `engine`‑object hebt geconfigureerd met de juiste taal‑ en resolutie‑instellingen.

```python
# Assume `engine` is a pre‑configured OCR object (e.g., with language='en')
ocr_engine = engine
raw_result = ocr_engine.recognize_image("receipt.png")
```

**Tip:** Als je geen vooraf geconfigureerd object hebt, kun je er een maken met:

```python
from aspose.ocr import OcrEngine
ocr_engine = OcrEngine(language='en')
```

De `recognize_image`‑aanroep retourneert een object waarvan het `text`‑attribuut de ruwe, niet‑gemaskeerde string bevat.

## Stap 5: Pas de geregistreerde post‑processor toe

Met de ruwe OCR‑data in de hand, geven we deze door aan de AI‑instantie. De engine voert automatisch de `mask_pci`‑functie uit die we eerder hebben geregistreerd.

```python
# This triggers the post‑processor and returns a new result object
final_result = ai.run_postprocessor(raw_result)
```

**Waarom `run_postprocessor` gebruiken in plaats van de functie handmatig aan te roepen?**  
Dit houdt de workflow consistent, vooral wanneer je meerdere post‑processors hebt (bijv. spell‑checking, language detection). AsposeAI plaatst ze in de volgorde waarin je ze registreert, wat een deterministische output garandeert.

## Stap 6: Verifieer de gesaniteerde output

Laten we tenslotte de gesaniteerde tekst afdrukken en bevestigen dat eventuele creditcardnummers correct gemaskeerd zijn.

```python
print(final_result.text)
```

**Verwachte output** (excerpt):

```
Purchase at Café Latte – Total: $4.75
Card: 1234****5678
Date: 2026-04-25
Thank you!
```

Als de bon geen kaartnummer bevatte, blijft de tekst ongewijzigd—niets te maskeren, niets om je zorgen over te maken.

## Randgevallen en veelvoorkomende variaties afhandelen

### Meerdere kaartnummers in één document
Als een bon meer dan één PAN bevat (bijv. een loyaliteitskaart plus een betaalkaart), voert de regex globaal uit en maskert automatisch alle overeenkomsten. Geen extra code nodig.

### Niet‑standaard opmaak
Soms voegt OCR spaties of streepjes in (`1234 5678 1234 5678` of `1234-5678-1234-5678`). Breid het patroon uit om die tekens te negeren:

```python
pattern = r'(\d{4})[ -]?\d{4}[ -]?\d{4}[ -]?\d{4}'
```

De toegevoegde `[ -]?` staat optionele spaties of streepjes tussen cijferblokken toe.

### Internationale kaarten
Voor 19‑cijferige PAN's die in sommige regio's worden gebruikt, kun je het patroon verbreden:

```python
pattern = r'(\d{4})\d{11,15}(\d{4})'
```

Onthoud wel dat **PCI compliance** nog steeds vereist dat de middelste cijfers worden gemaskeerd, ongeacht de lengte.

### Gemaskeerde waarden loggen (optioneel)
Als je audit‑trails nodig hebt, geef dan een vlag door via `custom_settings` en pas de functie aan:

```python
def mask_pci(data, settings):
    import re, logging
    pattern = r'(\d{4})\d{8}(\d{4})'
    def repl(match):
        masked = f"{match.group(1)}****{match.group(2)}"
        if settings.get('log'):
            logging.info(f"Masked PAN: {masked}")
        return masked
    return re.sub(pattern, repl, data.text)
```

Registreer vervolgens met:

```python
ai.set_post_processor(mask_pci, custom_settings={'log': True})
```

## Volledig werkend voorbeeld (klaar om te kopiëren en plakken)

```python
# ------------------------------------------------------------
# Mask Credit Card Numbers in OCR Output – Complete Example
# ------------------------------------------------------------
import re
from aspose.ocr import AsposeAI, OcrEngine

# 1️⃣ Define the post‑processor
def mask_pci(data, settings):
    """
    Hide the middle eight digits of any 16‑digit credit‑card number.
    """
    pattern = r'(\d{4})\d{8}(\d{4})'          # keep first & last 4 digits
    return re.sub(pattern, r'\1****\2', data.text)

# 2️⃣ Initialise the OCR engine and AsposeAI wrapper
ocr_engine = OcrEngine(language='en')       # configure as needed
ai = AsposeAI()

# 3️⃣ Register the masking function
ai.set_post_processor(mask_pci, custom_settings={})

# 4️⃣ Run OCR on a sample receipt
raw_result = ocr_engine.recognize_image("receipt.png")

# 5️⃣ Apply post‑processing (masking)
final_result = ai.run_postprocessor(raw_result)

# 6️⃣ Display sanitized text
print("Sanitized OCR output:")
print(final_result.text)
```

Het uitvoeren van dit script op een bon die `4111111111111111` bevat, zal produceren:

```
Sanitized OCR output:
Purchase at Bookstore – $12.99
Card: 4111****1111
Date: 2026-04-26
```

Dat is de volledige pipeline—van ruwe OCR tot **data sanitization**—verpakt in een paar nette regels Python.

## Conclusie

We hebben je net laten zien hoe je **creditcardnummers kunt maskeren** in OCR‑resultaten met behulp van de post‑processing‑hook van AsposeAI, een beknopte regular‑expression‑routine, en een reeks best‑practice‑tips voor **PCI compliance**. De oplossing is volledig zelfstandig, werkt met elke afbeelding die de OCR‑engine kan lezen, en kan worden uitgebreid om complexere kaartformaten of logvereisten te dekken.

Klaar voor de volgende stap? Probeer deze maskering te koppelen aan een **database‑invoeg**‑routine die alleen de laatste vier cijfers opslaat voor referentie, of integreer een **batch‑processor** die ’s nachts een hele map bonnen scant. Je kunt ook andere **OCR post‑processing**‑taken verkennen, zoals adresstandaardisatie of taaldetectie—elk volgt hetzelfde patroon dat we hier hebben gebruikt.

Heb je vragen over randgevallen, prestaties, of hoe je de code kunt aanpassen voor een andere OCR‑bibliotheek? Laat een reactie achter hieronder, en laten we het gesprek voortzetten. Veel plezier met coderen, en blijf veilig!

![Diagram dat laat zien hoe het maskeren van creditcardnummers werkt in een OCR‑pipeline](https://example.com/images/ocr-mask-flow.png "Diagram van OCR post‑processing maskeringsstroom")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}