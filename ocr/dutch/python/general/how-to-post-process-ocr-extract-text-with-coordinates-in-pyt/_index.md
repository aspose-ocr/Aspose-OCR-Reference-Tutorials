---
category: general
date: 2026-04-26
description: Hoe OCR‑resultaten post‑processen en tekst met coördinaten extraheren.
  Leer een stapsgewijze oplossing met gestructureerde output en AI‑correctie.
draft: false
keywords:
- how to post‑process OCR
- extract text with coordinates
- OCR structured output
- AI post‑processing OCR
- bounding box OCR
language: nl
og_description: Hoe OCR‑resultaten post‑processen en tekst met coördinaten extraheren.
  Volg deze uitgebreide tutorial voor een betrouwbare workflow.
og_title: Hoe OCR nabewerken – Complete gids
tags:
- OCR
- Python
- AI
- Text Extraction
title: Hoe OCR nabewerken – Tekst met coördinaten extraheren in Python
url: /nl/python/general/how-to-post-process-ocr-extract-text-with-coordinates-in-pyt/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe OCR na‑verwerken – Tekst met coördinaten extraheren in Python

Heb je ooit **hoe OCR na‑verwerken** moeten doen omdat de ruwe output ruisig of mis‑aligned was? Je bent niet de enige. In veel real‑world projecten—factuurscanning, bondigitalisatie, of zelfs het verrijken van AR‑ervaringen—geeft de OCR‑engine je ruwe woorden, maar moet je ze nog opschonen en bijhouden waar elk woord zich op de pagina bevindt. Dat is waar een gestructureerde output‑modus gecombineerd met een AI‑gedreven post‑processor schittert.

In deze tutorial lopen we een complete, uitvoerbare Python‑pipeline door die **tekst met coördinaten** uit een afbeelding haalt, een AI‑gebaseerde correctiestap uitvoert, en elk woord samen met zijn (x, y)‑positie afdrukt. Geen ontbrekende imports, geen vage “zie de docs” shortcuts—gewoon een zelfstandige oplossing die je vandaag nog in je project kunt gebruiken.

> **Pro tip:** Als je een andere OCR‑bibliotheek gebruikt, zoek dan naar een “structured” of “layout”‑modus; de concepten blijven hetzelfde.

---

## Vereisten

Voordat we beginnen, zorg dat je het volgende hebt:

| Vereiste | Waarom het belangrijk is |
|----------|--------------------------|
| Python 3.9+ | Moderne syntax en type hints |
| `ocr`‑bibliotheek die `OutputMode.STRUCTURED` ondersteunt (bijv. een fictieve `myocr`) | Nodig voor bounding‑box‑data |
| Een AI‑post‑processing module (kan OpenAI, HuggingFace, of een aangepast model zijn) | Verbetert de nauwkeurigheid na OCR |
| Een afbeeldingsbestand (`input.png`) in je werkmap | De bron die we gaan lezen |

Als een van deze onbekend klinkt, installeer dan de placeholder‑pakketten met `pip install myocr ai‑postproc`. De code hieronder bevat ook fallback‑stubs zodat je de flow kunt testen zonder de echte bibliotheken.

---

## Stap 1: Gestructureerde output‑modus inschakelen voor de OCR‑engine  

Het eerste wat we doen is de OCR‑engine vertellen meer dan alleen platte tekst te geven. Gestructureerde output levert elk woord samen met zijn omhullende rechthoek en confidence‑score, wat essentieel is voor **tekst met coördinaten extraheren** later.

```python
# step1_structured_output.py
import myocr as ocr  # fictional OCR library

# Initialize the engine (replace with your actual init code)
engine = ocr.Engine()

# Switch to structured mode – this makes the engine emit word‑level data
engine.set_output_mode(ocr.OutputMode.STRUCTURED)

print("✅ Structured output mode enabled")
```

*Waarom dit belangrijk is:* Zonder gestructureerde modus krijg je alleen een lange string, en verlies je de ruimtelijke informatie die je nodig hebt om tekst op afbeeldingen te overlayen of downstream layout‑analyse te voeren.

---

## Stap 2: De afbeelding herkennen en woorden, vakken en confidence vastleggen  

Nu voeren we de afbeelding in de engine. Het resultaat is een object dat een lijst van woordobjecten bevat, elk met `text`, `x`, `y`, `width`, `height` en `confidence`.

```python
# step2_recognize.py
from pathlib import Path

# Path to your image
image_path = Path("YOUR_DIRECTORY/input.png")

# Perform OCR – returns a StructuredResult with .words collection
structured_result = engine.recognize_image(str(image_path))

print(f"🔎 Detected {len(structured_result.words)} words")
```

*Randgeval:* Als de afbeelding leeg of onleesbaar is, zal `structured_result.words` een lege lijst zijn. Het is goed om dat te controleren en netjes af te handelen.

---

## Stap 3: AI‑gebaseerde post‑processing uitvoeren terwijl posities behouden blijven  

Zelfs de beste OCR‑engines maken fouten—denk aan “O” vs. “0” of ontbrekende diakritische tekens. Een AI‑model getraind op domeinspecifieke tekst kan die fouten corrigeren. Cruciaal is dat we de oorspronkelijke coördinaten behouden zodat de ruimtelijke lay-out intact blijft.

```python
# step3_ai_postprocess.py
import ai_postproc as ai  # placeholder for your AI module

# The AI post‑processor expects the structured result and returns a new one
corrected_result = ai.run_postprocessor(structured_result)

print("🤖 AI post‑processing complete")
```

*Waarom we coördinaten behouden:* Veel downstream‑taken (bijv. PDF‑generatie, AR‑labeling) vertrouwen op exacte plaatsing. De AI wijzigt alleen het `text`‑veld, en laat `x`, `y`, `width`, `height` onaangeroerd.

---

## Stap 4: Over de gecorrigeerde woorden itereren en hun tekst met coördinaten weergeven  

Tot slot lopen we door de gecorrigeerde woorden en printen elk woord samen met zijn linkerbovenhoek `(x, y)`. Dit voldoet aan het doel **tekst met coördinaten extraheren**.

```python
# step4_display.py
for recognized_word in corrected_result.words:
    # Using f‑string for clean formatting
    print(f"{recognized_word.text} (x:{recognized_word.x}, y:{recognized_word.y})")
```

**Verwachte output (voorbeeld):**

```
Invoice (x:45, y:112)
Number (x:120, y:112)
12345 (x:190, y:112)
Total (x:45, y:250)
$ (x:120, y:250)
199.99 (x:130, y:250)
```

Elke regel toont het gecorrigeerde woord en de exacte locatie op de originele afbeelding.

---

## Volledig werkend voorbeeld  

Hieronder staat één script dat alles samenbrengt. Je kunt het kopiëren‑plakken, de import‑statements aanpassen aan je eigen bibliotheken, en direct uitvoeren.

```python
# ocr_postprocess_demo.py
"""
Complete demo: how to post‑process OCR and extract text with coordinates.
Works with any OCR library exposing a structured output mode and an AI post‑processor.
"""

import sys
from pathlib import Path

# ----------------------------------------------------------------------
# 1️⃣ Imports – replace these with your real packages
# ----------------------------------------------------------------------
try:
    import myocr as ocr               # OCR engine with structured output
    import ai_postproc as ai          # AI correction module
except ImportError:  # Fallback stubs for quick testing
    class DummyWord:
        def __init__(self, text, x, y, w, h, conf):
            self.text = text
            self.x = x
            self.y = y
            self.width = w
            self.height = h
            self.confidence = conf

    class DummyResult:
        def __init__(self, words):
            self.words = words

    class StubEngine:
        class OutputMode:
            STRUCTURED = "structured"

        def set_output_mode(self, mode):
            print(f"[Stub] set_output_mode({mode})")

        def recognize_image(self, path):
            # Very simple fake OCR output
            sample = [
                DummyWord("Invoice", 45, 112, 60, 20, 0.98),
                DummyWord("Number", 120, 112, 55, 20, 0.96),
                DummyWord("12345", 190, 112, 40, 20, 0.97),
                DummyWord("Total", 45, 250, 50, 20, 0.99),
                DummyWord("$", 120, 250, 10, 20, 0.95),
                DummyWord("199.99", 130, 250, 55, 20, 0.94),
            ]
            return DummyResult(sample)

    class StubAI:
        @staticmethod
        def run_postprocessor(structured_result):
            # Pretend we corrected "12345" to "12346"
            for w in structured_result.words:
                if w.text == "12345":
                    w.text = "12346"
            return structured_result

    engine = StubEngine()
    ai = StubAI

# ----------------------------------------------------------------------
# 2️⃣ Enable structured output
# ----------------------------------------------------------------------
engine.set_output_mode(ocr.Engine.OutputMode.STRUCTURED)

# ----------------------------------------------------------------------
# 3️⃣ Recognize image
# ----------------------------------------------------------------------
image_path = Path("YOUR_DIRECTORY/input.png")
if not image_path.is_file():
    print(f"⚠️  Image not found at {image_path}. Using stub data.")
structured_result = engine.recognize_image(str(image_path))

# ----------------------------------------------------------------------
# 4️⃣ AI post‑processing
# ----------------------------------------------------------------------
corrected_result = ai.run_postprocessor(structured_result)

# ----------------------------------------------------------------------
# 5️⃣ Display results
# ----------------------------------------------------------------------
print("\n🗒️  Final OCR output with coordinates:")
for word in corrected_result.words:
    print(f"{word.text} (x:{word.x}, y:{word.y})")
```

**Het script uitvoeren**

```bash
python ocr_postprocess_demo.py
```

Als je de echte bibliotheken geïnstalleerd hebt, verwerkt het script je `input.png`. Anders laat de stub‑implementatie je de verwachte flow en output zien zonder externe afhankelijkheden.

---

## Veelgestelde vragen (FAQ)

| Vraag | Antwoord |
|-------|----------|
| *Werkt dit met Tesseract?* | Tesseract zelf biedt geen gestructureerde modus out‑of‑the‑box, maar wrappers zoals `pytesseract.image_to_data` geven bounding boxes terug die je kunt gebruiken met dezelfde AI‑post‑processor. |
| *Wat als ik de rechteronderhoek in plaats van linkerbovenhoek nodig heb?* | Elk woordobject levert ook `width` en `height`. Bereken `x2 = x + width` en `y2 = y + height` om de tegenovergestelde hoek te krijgen. |
| *Kan ik meerdere afbeeldingen in batch verwerken?* | Zeker. Plaats de stappen in een `for image_path in Path("folder").glob("*.png"):`‑lus en verzamel resultaten per bestand. |
| *Hoe kies ik een AI‑model voor correctie?* | Voor generieke tekst werkt een kleine GPT‑2 die is gefinetuned op OCR‑fouten. Voor domeinspecifieke data (bijv. medische recepten) train je een sequence‑to‑sequence‑model op gekoppelde noisy‑clean data. |
| *Is de confidence‑score nuttig na AI‑correctie?* | Je kunt de oorspronkelijke confidence behouden voor debugging, maar de AI kan zijn eigen confidence teruggeven als het model dat ondersteunt. |

---

## Randgevallen & Best Practices  

1. **Lege of corrupte afbeeldingen** – controleer altijd dat `structured_result.words` niet leeg is voordat je verder gaat.  
2. **Niet‑Latijnse scripts** – zorg dat je OCR‑engine is geconfigureerd voor de doeltaal; de AI‑post‑processor moet op hetzelfde script getraind zijn.  
3. **Prestaties** – AI‑correctie kan duur zijn. Cache resultaten als je dezelfde afbeelding opnieuw gebruikt, of voer de AI‑stap asynchroon uit.  
4. **Coördinatensysteem** – OCR‑bibliotheken kunnen verschillende oorsprongen gebruiken (linkerboven vs. linksonder). Pas dit aan bij het overlayen op PDF’s of canvassen.  

---

## Conclusie  

Je hebt nu een solide, end‑to‑end recept voor **hoe OCR na‑verwerken** en betrouwbaar **tekst met coördinaten extraheren**. Door gestructureerde output in te schakelen, het resultaat door een AI‑correctielaag te voeren, en de oorspronkelijke bounding boxes te behouden, kun je ruisige OCR‑scans omzetten in schone, ruimtelijk‑bewuste tekst die klaar is voor downstream‑taken zoals PDF‑generatie, data‑invoer‑automatisering, of augmented‑reality overlays.

Klaar voor de volgende stap? Probeer de stub‑AI te vervangen door een OpenAI `gpt‑4o‑mini`‑call, of integreer de pipeline in een FastAPI

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}