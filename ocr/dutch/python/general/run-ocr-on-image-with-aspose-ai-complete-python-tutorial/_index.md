---
category: general
date: 2026-07-18
description: Voer OCR uit op een afbeelding met Aspose OCR in Python. Leer platte
  tekst uit een afbeelding te extraheren, AI-nabewerking toe te passen en snel schone
  resultaten te krijgen.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- run OCR on image
- extract plain text from image
- Aspose OCR Python
- AI post‑processor OCR
- image text extraction
language: nl
lastmod: 2026-07-18
og_description: Voer OCR uit op een afbeelding met Aspose OCR en Python. Deze tutorial
  laat zien hoe je platte tekst uit een afbeelding kunt extraheren en de nauwkeurigheid
  kunt verbeteren met een AI‑nabewerker.
og_image_alt: Screenshot showing run OCR on image results in Python console
og_title: Voer OCR uit op afbeelding – Volledige Python-gids met Aspose AI
schemas:
- author: Aspose
  dateModified: '2026-07-18'
  description: Run OCR on image using Aspose OCR in Python. Learn to extract plain
    text from image, apply AI post‑processing, and get clean results fast.
  headline: Run OCR on Image with Aspose AI – Complete Python Tutorial
  type: TechArticle
tags:
- OCR
- Python
- Aspose
- AI
title: Voer OCR uit op afbeelding met Aspose AI – Complete Python‑tutorial
url: /nl/python/general/run-ocr-on-image-with-aspose-ai-complete-python-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR uitvoeren op afbeelding met Aspose AI – Complete Python‑tutorial

Heb je je ooit afgevraagd hoe je **OCR op afbeelding** kunt uitvoeren zonder te worstelen met low‑level API’s? Je bent niet de enige. In veel projecten—factuurverwerking, bonnen scannen of oude documenten digitaliseren—het verkrijgen van schone, doorzoekbare tekst uit een foto is de eerste, en vaak de moeilijkste, stap.

In deze gids lopen we een hands‑on voorbeeld door dat niet alleen **OCR op afbeelding** uitvoert, maar ook laat zien hoe je **plain text uit afbeelding** kunt extraheren met de OCR‑engine van Aspose, en vervolgens het resultaat verfijnt met een kleine AI‑post‑processor. Aan het einde heb je een kant‑klaar script, een duidelijk begrip van elk onderdeel, en een paar tips om veelvoorkomende valkuilen te vermijden.

![Run OCR on Image example](/images/run-ocr-on-image.png){: .align-center alt="OCR op afbeelding console‑output die originele en AI‑verbeterde tekst toont"}

## Wat je nodig hebt

Voordat we beginnen, zorg dat je het volgende hebt:

- Python 3.8+ geïnstalleerd (de code werkt op Windows, macOS en Linux).
- Een actieve Aspose OCR for Python‑licentie of een gratis proefversie (het pakket heet `aspose-ocr` op PyPI).
- Een voorbeeld‑afbeeldingsbestand (bijv. een gescande factuur of bon) lokaal opgeslagen.
- Optioneel: een GPU‑enabled machine als je later de `gpu_layers`‑instelling wilt aanpassen.

Dat is alles—geen zware OCR‑engines, geen externe cloud‑calls, alleen een enkele pip‑install en een paar regels code.

## Stap 1: Installeer het Aspose OCR‑pakket

Open een terminal en voer uit:

```bash
pip install aspose-ocr
```

Het pakket haalt de core OCR‑engine op plus de lichte `aspose.ocr`‑namespace die we door de hele tutorial heen gebruiken.

## Stap 2: Importeer vereiste klassen

We beginnen met het importeren van de twee hoofdklassen: `AsposeAI` voor AI‑verbeterde post‑processing en `OcrEngine` voor de feitelijke teksterkenning.

```python
# Step 1: Import required classes
from aspose.ocr import AsposeAI, OcrEngine
```

*Waarom dit belangrijk is*: `OcrEngine` doet het zware werk van het herkennen van glyphs, terwijl `AsposeAI` ons in staat stelt aangepaste logica—zoals het kapitaliseren van elk woord—toe te passen zonder de OCR‑core te herschrijven.

## Stap 3: Maak een AsposeAI‑instantie (optionele logger)

Als je uitgebreide logging wilt, kun je een aangepaste logger doorgeven, maar de standaard werkt prima voor de meeste gevallen.

```python
# Step 2: Create an AsposeAI instance (optional custom logger can be supplied)
ai = AsposeAI()
```

## Stap 4: Pas het onderliggende model aan (optioneel)

Aspose OCR wordt geleverd met een standaard taalmodel, maar je kunt het laten wijzen naar een HuggingFace‑repo of CPU‑executie forceren. Hieronder schakelen we automatische downloads in en selecteren we het kleine `gpt2`‑model—alleen om de knoppen te laten zien die je kunt draaien.

```python
# Step 3: (Optional) Adjust the underlying model configuration
ai.config.allow_auto_download = "true"          # permit automatic model download
ai.config.hugging_face_repo_id = "openai/gpt2"   # specify the HuggingFace model
ai.config.gpu_layers = 0                        # force CPU execution
```

> **Pro tip:** Als je een CUDA‑capabele GPU hebt, verhoog `gpu_layers` naar `1` of `2` voor een merkbare snelheidsboost.

## Stap 5: Registreer een eenvoudige post‑processor

Ons doel is om **plain text uit afbeelding** te extraheren en vervolgens netter te maken. Hier is een kleine functie die elk woord kapitaliseert. Je kunt deze vervangen door spell‑checking, taaldetectie, of zelfs een volledige LLM‑call.

```python
# Step 4: Register a simple post‑processor that capitalizes each word
def capitalize_words(text, settings):
    """Capitalize every word in the OCR output."""
    return " ".join(word.capitalize() for word in text.split())

# Attach the processor to the AsposeAI instance
ai.set_post_processor(capitalize_words, custom_settings={})
```

De `custom_settings`‑dict laat je later extra parameters doorgeven—handig wanneer je de processor verder ontwikkelt.

## Stap 6: Laad een afbeelding en voer OCR uit

Nu voeren we eindelijk **OCR op afbeelding** uit. We halen twee soorten output op:

1. **Plain text** – een ruwe string zonder lay‑outinformatie.
2. **Structured text** – lay‑out‑bewust, behoudt kolommen en tabellen.

```python
# Step 5: Load an image and obtain OCR results (plain and layout‑aware)
ocr_engine = OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

plain_text = ocr_engine.recognize()                     # raw text
structured_text = ocr_engine.recognize_structured()    # layout‑aware text
```

> **Waarom beide?** `plain_text` is perfect voor snelle zoekopdrachten, terwijl `structured_text` uitblinkt wanneer je tabellen moet herbouwen of kolomuitlijning wilt behouden.

## Stap 7: Verfijn de OCR‑uitvoer met de AI‑post‑processor

Met de OCR‑resultaten in de hand, geven we ze door aan `AsposeAI.run_postprocessor`. Hier wordt de eerder gedefinieerde `capitalize_words`‑functie uitgevoerd.

```python
# Step 6: Enhance the OCR outputs using the AI post‑processor
enhanced_plain = ai.run_postprocessor(plain_text)
enhanced_structured = ai.run_postprocessor(structured_text)
```

Als je later de post‑processor wilt vervangen door iets geavanceerders—bijv. een grammaticacontrole—vervang je simpelweg de functie in stap 5 en blijft de rest van de pipeline identiek.

## Stap 8: Bekijk de resultaten

Laten we alles naast elkaar afdrukken zodat je de ruwe OCR kunt vergelijken met de AI‑verbeterde versie.

```python
# Step 7: Display original and enhanced texts
print("Original plain text:", plain_text)
print("AI‑enhanced plain text:", enhanced_plain)

print("\nOriginal structured text:", structured_text)
print("AI‑enhanced structured text:", enhanced_structured)
```

### Verwachte output

```
Original plain text: invoice #12345 date 01/02/2024 total $123.45
AI‑enhanced plain text: Invoice #12345 Date 01/02/2024 Total $123.45

Original structured text: invoice #12345
date 01/02/2024
total $123.45
AI‑enhanced structured text: Invoice #12345
Date 01/02/2024
Total $123.45
```

Merk op hoe de AI‑post‑processor alle kleine letters heeft omgezet in kapitalen, waardoor de tekst veel leesbaarder wordt. Je kunt elke gewenste transformatie toepassen—dit is slechts een proof of concept.

## Stap 9: Ruim bronnen op

Aspose laadt zware modelbestanden in het geheugen. Wanneer je klaar bent, maak je ze vrij om geheugenlekken te voorkomen, vooral in langdurige services.

```python
# Step 8: Release model resources when done
ai.free_resources()
```

## Veelgestelde vragen & randgevallen

| Vraag | Antwoord |
|-------|----------|
| **Kan ik OCR op meerdere afbeeldingen in een loop uitvoeren?** | Absoluut. Instantieer `OcrEngine` één keer, roep `load_image` aan binnen de loop, en hergebruik dezelfde `AsposeAI`‑instantie voor post‑processing. |
| **Wat als de afbeelding een lage resolutie heeft?** | Pre‑process met OpenCV (bijv. `cv2.resize` en `cv2.threshold`) voordat je het aan `OcrEngine` doorgeeft. |
| **Heb ik een GPU nodig?** | Niet vereist. De standaard CPU‑modus werkt prima voor de meeste documenten. Stel `ai.config.gpu_layers` > 0 alleen in als je een compatibele GPU hebt en snelheid nodig hebt. |
| **Hoe extraheer ik plain text uit afbeelding in andere talen?** | Verander `ocr_engine.language = "fr"` (of een andere ISO‑639‑1‑code) vóór het aanroepen van `recognize`. Dezelfde post‑processor blijft werken, maar je hebt mogelijk taalspecifieke logica nodig. |

## Volledig werkend script

Alles samengevoegd, hier is het complete, kant‑klaar programma:

```python
# Full script: run OCR on image, extract plain text, and apply AI post‑processing

from aspose.ocr import AsposeAI, OcrEngine

# 1️⃣ Initialize AsposeAI
ai = AsposeAI()
ai.config.allow_auto_download = "true"
ai.config.hugging_face_repo_id = "openai/gpt2"
ai.config.gpu_layers = 0   # set >0 for GPU

# 2️⃣ Register post‑processor (capitalizes each word)
def capitalize_words(text, settings):
    return " ".join(word.capitalize() for word in text.split())

ai.set_post_processor(capitalize_words, custom_settings={})

# 3️⃣ Load image and run OCR
ocr_engine = OcrEngine()
ocr_engine.load_image("YOUR_DIRECTORY/sample_invoice.png")

plain_text = ocr_engine.recognize()
structured_text = ocr_engine.recognize_structured()

# 4️⃣ Enhance outputs
enhanced_plain = ai.run_postprocessor(plain_text)
enhanced_structured = ai.run_postprocessor(structured_text)

# 5️⃣ Print results
print("Original plain text:", plain_text)
print("AI‑enhanced plain text:", enhanced_plain)

print("\nOriginal structured text:", structured_text)
print("AI‑enhanced structured text:", enhanced_structured)

# 6️⃣ Clean up
ai.free_resources()
```

Sla dit op als `run_ocr_on_image.py`, vervang het placeholder‑pad door je eigen afbeelding, en voer `python run_ocr_on_image.py` uit. Je zou de voor‑/na‑output moeten zien zoals in het voorbeeld hierboven.

## Conclusie

We hebben met succes **OCR op afbeelding** uitgevoerd met Aspose OCR, laten zien hoe je **plain text uit afbeelding** kunt extraheren, en een lichte manier gedemonstreerd om de leesbaarheid te verhogen met een AI‑post‑processor. Het kernpatroon—OCR

## Wat kun je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}