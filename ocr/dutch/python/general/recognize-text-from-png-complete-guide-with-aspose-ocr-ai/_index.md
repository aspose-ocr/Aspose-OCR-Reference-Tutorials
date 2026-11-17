---
category: general
date: 2026-06-22
description: herken tekst uit png‑bestanden met Aspose OCR in Python. Leer batch‑OCR‑afbeeldingen
  en stel GPU‑lagen in voor snelle verwerking.
draft: false
keywords:
- recognize text from png
- batch ocr images
- set gpu layers
- Aspose OCR Python
- GPU acceleration OCR
language: nl
og_description: herken tekst uit png‑bestanden met Aspose OCR in Python. Deze gids
  laat zien hoe je OCR‑afbeeldingen in batch verwerkt en GPU‑lagen instelt voor snelheid.
og_title: tekst herkennen uit PNG – Stapsgewijze Aspose OCR‑tutorial
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: recognize text from png files using Aspose OCR in Python. Learn batch
    OCR images and set GPU layers for fast processing.
  headline: recognize text from png – Complete Guide with Aspose OCR & AI
  type: TechArticle
- description: recognize text from png files using Aspose OCR in Python. Learn batch
    OCR images and set GPU layers for fast processing.
  name: recognize text from png – Complete Guide with Aspose OCR & AI
  steps:
  - name: '**Model download fails** – Ensure your environment can reach `https://huggingface.co`.
      A corporate proxy may need configuration (`https_proxy` env var).'
    text: '**Model download fails** – Ensure your environment can reach `https://huggingface.co`.
      A corporate proxy may need configuration (`https_proxy` env var).'
  - name: '**GPU not detected** – Verify that the `torch` library (installed as a
      dependency) sees the GPU: `import torch; print(torch.cuda.is_available())`.
      If it returns `False`, install the CUDA‑compatible PyTorch wheel.'
    text: '**GPU not detected** – Verify that the `torch` library (installed as a
      dependency) sees the GPU: `import torch; print(torch.cuda.is_available())`.
      If it returns `False`, install the CUDA‑compatible PyTorch wheel.'
  - name: '**Incorrect image path** – `Path.glob("*.png")` is case‑sensitive on Linux.
      Use `*.PNG` or `*.png` accordingly, or add `pathlib.Path(...).rglob("*.[pP][nN][gG]")`
      for safety.'
    text: '**Incorrect image path** – `Path.glob("*.png")` is case‑sensitive on Linux.
      Use `*.PNG` or `*.png` accordingly, or add `pathlib.Path(...).rglob("*.[pP][nN][gG]")`
      for safety.'
  - name: '**Post‑processor over‑corrects** – The simple replace may turn legitimate
      “0” characters into “o”. Test on a representative sample and adjust the logic
      as needed.'
    text: '**Post‑processor over‑corrects** – The simple replace may turn legitimate
      “0” characters into “o”. Test on a representative sample and adjust the logic
      as needed.'
  type: HowTo
tags:
- OCR
- Python
- AsposeAI
title: Tekst herkennen uit PNG – Complete gids met Aspose OCR & AI
url: /nl/python/general/recognize-text-from-png-complete-guide-with-aspose-ocr-ai/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# tekst herkennen uit png – Volledig‑uitgeruste Aspose OCR & AI‑handleiding

Altijd al **tekst herkennen uit png**‑bestanden willen, maar verstrikt geraakt in de installatie‑details? Je bent niet de enige. Of je nu bonnen digitaliseert, formulieren scant of screenshots omzet in doorzoekbare tekst, het beheersen van batch‑OCR‑afbeeldingen in Python kan je uren besparen.  

In deze gids lopen we een kant‑klaar voorbeeld door dat niet alleen **tekst herkennen uit png** doet, maar ook laat zien hoe je **GPU‑lagen kunt instellen** voor een merkbare snelheidsboost. Aan het einde heb je een zelfstandige script, een duidelijke uitleg van elke stap, en een reeks praktische tips die je kunt copy‑pasten in je eigen projecten.

## Wat deze tutorial behandelt

- Installeren van de Aspose OCR‑ en Aspose AI‑Python‑pakketten  
- Configureren van een AI‑model met automatische download van Hugging Face  
- Een kleine post‑processor maken die de meest voorkomende OCR‑typefouten corrigeert  
- Een **batch OCR‑images**‑lus uitvoeren over een volledige map met PNG’s  
- De **set GPU layers**‑optie gebruiken om je grafische kaart te benutten  
- Veilig opruimen van resources na verwerking  

Geen externe services, geen verborgen magie—alleen pure Python‑code die je in een `.py`‑bestand kunt plaatsen en uitvoeren.

![Diagram van tekst herkennen uit png workflow](workflow.png){alt="tekst herkennen uit png workflow diagram"}

## Vereisten

| Vereiste | Waarom het belangrijk is |
|----------|--------------------------|
| Python 3.8+ | Aspose AI’s wheels richten zich op recente interpreters |
| Een CUDA‑compatibele GPU (optioneel) | Nodig als je **GPU‑lagen wilt instellen** voor versnelling |
| Internettoegang bij eerste uitvoering | Het model wordt automatisch gedownload van Hugging Face |
| `pip` geïnstalleerd | Om de Aspose‑pakketten op te halen |

Als je deze al hebt, prima—je bent klaar om te starten. Zo niet, dan leiden de installatie‑stappen hieronder je door de ontbrekende onderdelen.

---

## Stap 1: Installeer Aspose OCR‑ en Aspose AI‑pakketten

Eerst de bibliotheken van PyPI halen. Het onderstaande commando downloadt zowel de OCR‑engine als de AI‑helper in één keer.

```bash
pip install aspose-ocr aspose-ai
```

*Pro tip:* Gebruik een virtuele omgeving (`python -m venv .venv`) zodat de pakketten geïsoleerd blijven van je globale Python‑installatie.

---

## Stap 2: Maak en configureer de Aspose AI‑instantie

De AI‑component voedt de “intelligente” modus van de OCR‑engine. We wijzen hem op het model `Qwen/Qwen2.5-3B-Instruct-GGUF`, laten hem automatisch downloaden indien nodig, en **stellen GPU‑lagen in** op 30 (dit kun je later afstemmen).

```python
from aspose_ai import AsposeAI, AsposeAIModelConfig

# Initialize the AI wrapper
ai = AsposeAI()

# Build a model configuration
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",                     # Grab the model automatically
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",               # Smaller footprint, still accurate
    directory_model_path="YOUR_DIRECTORY/ai_models", # Where the model will live
    gpu_layers=30                                   # <-- set gpu layers for GPU acceleration
)

# Apply the configuration and spin up the model
ai.initialize(model_cfg)
```

**Waarom dit belangrijk is:**  
- `allow_auto_download` elimineert de handmatige stap van het ophalen van een ~2 GB model.  
- `gpu_layers=30` vertelt de onderliggende transformer om de eerste 30 lagen op de GPU uit te voeren, waardoor de inferentietijd drastisch wordt verkort wanneer er een compatibele GPU aanwezig is.  
- Het gebruik van `int8`‑kwantisatie houdt het geheugenverbruik laag zonder veel nauwkeurigheid op te offeren.

---

## Stap 3: Definieer een eenvoudige post‑processor om OCR‑fouten op te schonen

OCR is niet perfect—vooral bij lage‑resolutie PNG’s. Een snelle oplossing is het vervangen van tekens die vaak verkeerd worden gelezen. De volgende functie verwisselt “0” voor “o” en “1” voor “l”, een patroon dat we vaak zien in gescande facturen.

```python
def fix_common_errors(text, **_):
    """
    Post‑processor that corrects typical OCR mis‑recognitions.
    Feel free to extend this with regexes or custom dictionaries.
    """
    return text.replace("0", "o").replace("1", "l")
```

We koppelen dit aan de AI‑instantie in de volgende stap zodat elk herkenningsresultaat er automatisch doorheen gaat.

---

## Stap 4: Koppel de post‑processor en de OCR‑engine

Nu verbinden we alles: de OCR‑engine, het AI‑model en de post‑processor.

```python
import ocr  # Aspose OCR module

# Attach the post‑processor
ai.set_post_processor(fix_common_errors, {})

# Spin up the OCR engine and bind the AI
engine = ocr.OcrEngine()
engine.set_ai(ai)
```

**Wat gebeurt er op de achtergrond?**  
De `OcrEngine` delegeert het zware werk aan het AI‑model dat je hebt geconfigureerd. Nadat het model ruwe tekst teruggeeft, roept Aspose `fix_common_errors` aan om de output op te schonen voordat jij het ziet.

---

## Stap 5: Batch OCR‑images – Verwerk elke PNG in een map

Hier is het hart van de tutorial: een lus die door een directory loopt, elke `.png` laadt, OCR uitvoert en het opgeschoonde resultaat afdrukt. Dit patroon is de canonieke manier om **batch OCR‑images** efficiënt uit te voeren.

```python
from pathlib import Path

# Replace with the folder that holds your PNG files
image_folder = Path("YOUR_DIRECTORY")

# Iterate over every PNG file in the folder
for img_path in image_folder.glob("*.png"):
    # Load the image into the engine
    engine.load_image(str(img_path))

    # Perform recognition
    result = engine.recognize()

    # Output the filename and the extracted text
    print(f"[{img_path.name}] → {result.text}")
```

**Verwachte output** (voorbeeld voor een bon):

```
[receipt_001.png] → Total amount: $23.45
[receipt_002.png] → Item: Coffee, Price: $3.50
```

Heb je tientallen of honderden bestanden, dan verwerkt deze lus ze sequentieel, waarbij dezelfde AI‑instantie wordt hergebruikt om de overhead van herhaald model‑laden te vermijden.

---

## Stap 6: Opruimen – Vrijgeven van resources en de engine verwijderen

Wanneer je klaar bent, is het goed om GPU‑geheugen en andere native resources vrij te geven. Aspose biedt expliciete methoden hiervoor.

```python
# Release the AI model and any GPU buffers
ai.free_resources()

# Dispose of the OCR engine to close native handles
engine.dispose()
```

Het overslaan van deze stap kan leiden tot achtergebleven GPU‑geheugen, wat later tot out‑of‑memory‑fouten kan leiden.

---

## Bonus: GPU‑lagen afstemmen voor verschillende hardware

De `gpu_layers`‑waarde die je eerder instelde is een goede middenweg voor veel moderne GPU’s, maar je moet die mogelijk aanpassen:

| GPU‑geheugen (GB) | Aanbevolen `gpu_layers` |
|-------------------|--------------------------|
| 4 GB of minder    | 10‑15                    |
| 6‑8 GB            | 20‑30                    |
| 12 GB+            | 35‑45 (of hoger)         |

Als je het geheugen van je GPU overschrijdt, valt de engine automatisch terug op de CPU voor de resterende lagen, zodat je niet crasht—alleen langzamer. Experimenteer gerust en houd het gebruik in de gaten met `nvidia‑smi`.

---

## Veelvoorkomende valkuilen & hoe ze te vermijden

1. **Modeldownload mislukt** – Zorg dat je omgeving `https://huggingface.co` kan bereiken. Een bedrijfsproxy vereist mogelijk configuratie (`https_proxy`‑env‑var).  
2. **GPU niet gedetecteerd** – Controleer of de `torch`‑bibliotheek (geïnstalleerd als dependency) de GPU ziet: `import torch; print(torch.cuda.is_available())`. Als dit `False` oplevert, installeer dan het CUDA‑compatibele PyTorch‑wheel.  
3. **Onjuist afbeeldingspad** – `Path.glob("*.png")` is hoofdlettergevoelig op Linux. Gebruik `*.PNG` of `*.png` overeenkomstig, of voeg `pathlib.Path(...).rglob("*.[pP][nN][gG]")` toe voor extra zekerheid.  
4. **Post‑processor corrigeert te veel** – De eenvoudige replace kan legitieme “0”‑tekens omzetten in “o”. Test op een representatieve steekproef en pas de logica aan waar nodig.

---

## Volledig werkend voorbeeld (Klaar om te copy‑pasten)

```python
# recognize_text_from_png_batch.py
# -------------------------------------------------
# Author: Your Name
# Date:   2026‑06‑22
# -------------------------------------------------
from pathlib import Path
import ocr                      # Aspose OCR module
from aspose_ai import AsposeAI, AsposeAIModelConfig

# ----- Step 1: AI configuration -----
ai = AsposeAI()
model_cfg = AsposeAIModelConfig(
    allow_auto_download="true",
    hugging_face_repo_id="Qwen/Qwen2.5-3B-Instruct-GGUF",
    hugging_face_quantization="int8",
    directory_model_path="YOUR_DIRECTORY/ai_models",
    gpu_layers=30               # <-- set gpu layers
)
ai.initialize(model_cfg)

# ----- Step 2: Post‑processor -----
def fix_common_errors(text, **_):
    """Replace typical OCR mis‑reads."""
    return text.replace("0", "o").replace("1", "l")

ai.set_post_processor(fix_common_errors, {})

# ----- Step 3: OCR engine -----
engine = ocr.OcrEngine()
engine.set_ai(ai)

# ----- Step 4: Batch processing -----
image_folder = Path("YOUR_DIRECTORY")
for img_path in image_folder.glob("*.png"):
    engine.load_image(str(img_path))
    result = engine.recognize()
    print(f"[{img_path.name}] → {result.text}")

# ----- Step 5: Cleanup -----
ai.free_resources()
engine.dispose()
```

Voer het uit met:

```bash
python recognize_text_from_png_batch.py
```

Je zou elke PNG‑bestandsnaam gevolgd door de geëxtraheerde tekst moeten zien, precies zoals eerder gedemonstreerd.

---

## Conclusie

We hebben zojuist een compleet, productie‑klaar workflow doorlopen om **tekst te herkennen uit png**‑bestanden te gebruiken met Aspose OCR en Aspose AI in Python. Door de stappen in een schoon script te bundelen, kun je moeiteloos **batch OCR‑images** uitvoeren, en dankzij de `set gpu layers`‑optie profiteer je van je grafische kaart.

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids zijn gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementaties in je eigen projecten te verkennen.

- [How to Batch OCR Images with List in Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}