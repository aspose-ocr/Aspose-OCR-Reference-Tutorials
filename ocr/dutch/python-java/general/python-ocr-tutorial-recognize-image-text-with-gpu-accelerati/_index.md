---
category: general
date: 2026-06-06
description: Python OCR-tutorial die laat zien hoe je afbeeldings­tekst herkent, OCR
  met hoge resolutie uitvoert en Spaanse tekst extraheert met GPU-versnelde OCR.
draft: false
keywords:
- python ocr tutorial
- recognize image text
- high resolution ocr
- gpu accelerated ocr
- extract spanish text
language: nl
og_description: Python OCR‑tutorial die je stap voor stap begeleidt bij het herkennen
  van tekst in afbeeldingen, OCR met hoge resolutie en het extraheren van Spaanse
  tekst met GPU‑versnelling.
og_title: Python OCR-tutorial – GPU-versnelde teksterkenning
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: Python OCR tutorial showing how to recognize image text, perform high
    resolution OCR and extract Spanish text using GPU accelerated OCR.
  headline: Python OCR Tutorial – Recognize Image Text with GPU Acceleration
  type: TechArticle
- description: Python OCR tutorial showing how to recognize image text, perform high
    resolution OCR and extract Spanish text using GPU accelerated OCR.
  name: Python OCR Tutorial – Recognize Image Text with GPU Acceleration
  steps:
  - name: Prerequisites
    text: '- Python 3.9+ (the code works on 3.10 and newer as well). - A CUDA‑compatible
      GPU (optional but highly recommended). - Basic familiarity with pip and virtual
      environments.'
  - name: 6.1 Fallback When No GPU Is Present
    text: "```python if not torch.cuda.is_available(): # Re‑initialize the reader
      without GPU to avoid hidden errors reader = Reader(lang_list=[\"es\"], gpu=False)
      print(\"\U0001F504 Re‑initialized reader for CPU execution.\") ```"
  - name: 6.2 Down‑sampling Very Large Images
    text: 'If your image is larger than 4000 × 4000 px, you might run out of GPU memory.
      Down‑sample proportionally while preserving DPI:'
  type: HowTo
tags:
- OCR
- Python
- Image Processing
- GPU
- Spanish
title: Python OCR‑tutorial – Herken afbeeldingstekst met GPU‑versnelling
url: /nl/python-java/general/python-ocr-tutorial-recognize-image-text-with-gpu-accelerati/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python OCR Tutorial – Herken afbeeldingstekst met GPU‑versnelling

Heb je je ooit afgevraagd hoe je **afbeeldingstekst** kunt herkennen in een Python‑script zonder uren te besteden aan het afstellen van instellingen? Je bent niet de enige. In deze **python ocr tutorial** laten we je een schone, end‑to‑end manier zien om Spaanse tekst uit een hoge‑resolutie foto te extraheren, en we voegen GPU‑versnelling toe zodat het proces bliksemsnel verloopt.

Beschouw het als een snelle koffiepauze‑demo die je later kunt uitbreiden tot een productie‑klare pipeline. Aan het einde van deze gids heb je een uitvoerbaar programma dat **high resolution OCR** uitvoert, een CUDA‑enabled GPU benut, en de exacte Spaanse tekens oplevert die je nodig hebt.

## Wat je zult leren

- Hoe je een moderne OCR‑bibliotheek installeert en importeert die GPU‑versnelling ondersteunt.  
- Hoe je een OCR‑engine‑instantie maakt en instelt om **afbeeldingstekst** in het Spaans te **herkennen**.  
- Hoe je **gpu accelerated OCR** inschakelt voor enorme snelheidswinst bij hoge‑resolutie bestanden.  
- Hoe je edge‑cases afhandelt, zoals ontbrekende CUDA‑drivers of een fallback naar CPU.  
- Tips om de nauwkeurigheid te verbeteren wanneer je **spanish text** moet **extraheren** uit ruisende scans.

### Vereisten

- Python 3.9+ (de code werkt ook op 3.10 en nieuwer).  
- Een CUDA‑compatibele GPU (optioneel maar sterk aanbevolen).  
- Basiskennis van pip en virtuele omgevingen.  

Als je een van deze mist, werkt de tutorial nog steeds — sla gewoon de GPU‑stap over en de bibliotheek valt automatisch terug op CPU.

---

## Python OCR Tutorial: Installeer de vereiste pakketten

Allereerst hebben we een degelijke OCR‑engine nodig. Voor deze tutorial gebruiken we het open‑source **`easyocr`**‑pakket, dat ingebouwde GPU‑ondersteuning biedt wanneer een compatibel apparaat wordt gedetecteerd.

```bash
# Create a fresh virtual environment (optional but tidy)
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows use `ocr-env\Scripts\activate`

# Install EasyOCR and its optional torch dependencies
pip install easyocr[torch]   # Installs both CPU and GPU builds of PyTorch
```

> **Pro tip:** Als je PyTorch al geïnstalleerd hebt, zorg er dan voor dat het overeenkomt met je CUDA‑versie (`pip install torch==2.2.0+cu121 -f https://download.pytorch.org/whl/torch_stable.html`). Mismatchende versies zijn een veelvoorkomende oorzaak van “GPU not found”‑fouten.

---

## Stap 1: Maak een OCR‑engine‑instantie

Nu starten we de engine. EasyOCR noemt zijn hoofdklasse `Reader`. De constructor accepteert een lijst met taalcodes; we geven `"es"` op voor Spaans.

```python
# Step 1: Initialize the OCR reader for Spanish
from easyocr import Reader

# The `gpu` flag tells EasyOCR to try using CUDA if it’s available.
reader = Reader(lang_list=["es"], gpu=True)
```

*Waarom dit belangrijk is:* Door de taal vooraf te declareren laadt de engine alleen de benodigde neurale‑netwerk‑gewichten, wat geheugen bespaart en de inferentie versnelt — vooral handig wanneer je later werkt met **high resolution OCR**.

---

## Stap 2: Bereid een hoge‑resolutie afbeelding voor

Hoge‑resolutie afbeeldingen geven het model meer pixels om mee te werken, wat meestal resulteert in betere tekenherkenning. Laten we aannemen dat je een bestand hebt genaamd `high_res_spanish.png` in een map genaamd `samples`.

```python
import os

# Construct an absolute path – keeps the script portable
image_path = os.path.join("samples", "high_res_spanish.png")

# Quick sanity check – raise a clear error if the file is missing
if not os.path.isfile(image_path):
    raise FileNotFoundError(f"Image not found at {image_path}")
```

Als je geen hoge‑resolutie voorbeeld bij de hand hebt, kun je er gratis een downloaden van Unsplash of een synthetische afbeelding genereren met Pillow. Het belangrijkste is om de DPI boven de 300 te houden voor de beste resultaten.

---

## Stap 3: Schakel GPU‑versnelling in (optioneel maar aanbevolen)

EasyOCR probeert al de GPU te gebruiken wanneer je `gpu=True` instelt. Het is echter goed om te verifiëren dat het apparaat daadwerkelijk wordt gebruikt, vooral op systemen met meerdere GPU’s.

```python
import torch

# Verify CUDA availability – helpful for debugging
if torch.cuda.is_available():
    print(f"✅ CUDA device detected: {torch.cuda.get_device_name(0)}")
else:
    print("⚠️ No CUDA device found – falling back to CPU. Performance will be slower.")
```

*Waarom dit controleren?* Als het script stilletjes terugvalt op CPU, vraag je je misschien af waarom een bewerking van 5 seconden ineens 30 seconden duurt. Deze kleine controle maakt het gedrag transparant en houdt je **gpu accelerated OCR**‑pipeline voorspelbaar.

---

## Stap 4: Voer high‑resolution OCR uit en herken afbeeldingstekst

Nu het leuke deel — het daadwerkelijk lezen van de tekst. EasyOCR’s `readtext`‑methode retourneert een lijst van tuples met de begrenzings‑box, de herkende string en een confidence‑score.

```python
# Step 4: Run OCR on the high‑resolution image
results = reader.readtext(image_path, detail=1, paragraph=False)

# `results` looks like:
# [
#   ([(x1, y1), (x2, y2), (x3, y3), (x4, y4)], 'Texto reconocido', 0.98),
#   ...
# ]
```

Als je de ruwe string zonder coördinaten nodig hebt, stel `detail=0` in. Voor de meeste **recognize image text**‑use‑cases geeft de standaard (`detail=1`) je genoeg context om later post‑processing toe te passen.

---

## Stap 5: Extraheer Spaanse tekst en maak de output schoon

Omdat we EasyOCR om Spaans hebben gevraagd, zijn de geretourneerde strings al in die taal. Toch wil je ze misschien concatenëren, witruimte verwijderen of low‑confidence detecties filteren.

```python
# Step 5: Consolidate high‑confidence Spanish strings
extracted_text = []
for bbox, text, conf in results:
    if conf > 0.85:                # Drop anything below 85 % confidence
        extracted_text.append(text)

# Join everything into a single block – perfect for further NLP tasks
final_text = "\n".join(extracted_text)

print("📝 Extracted Spanish text:")
print(final_text)
```

**Wat als de confidence laag is?** Je kunt de drempel verlagen (met risico op ruis) of de afbeelding voorbewerken (contrast verhogen, binariseren of rechtzetten). Deze trucjes zijn gebruikelijk bij **high resolution OCR** op gescande documenten.

---

## Stap 6: Edge‑cases en prestatie‑tweaks afhandelen

Zelfs de best getrainde modellen struikelen over een paar scenario’s. Hieronder staan een paar snelle oplossingen die je in het script kunt plakken.

### 6.1 Fallback wanneer er geen GPU aanwezig is

```python
if not torch.cuda.is_available():
    # Re‑initialize the reader without GPU to avoid hidden errors
    reader = Reader(lang_list=["es"], gpu=False)
    print("🔄 Re‑initialized reader for CPU execution.")
```

### 6.2 Down‑sampling van zeer grote afbeeldingen

Als je afbeelding groter is dan 4000 × 4000 px, kun je GPU‑geheugen tekortkomen. Down‑sample proportioneel terwijl je de DPI behoudt:

```python
from PIL import Image

def resize_if_needed(path, max_dim=3000):
    img = Image.open(path)
    if max(img.size) > max_dim:
        scale = max_dim / max(img.size)
        new_size = (int(img.width * scale), int(img.height * scale))
        img = img.resize(new_size, Image.LANCZOS)
        resized_path = path.replace(".png", "_resized.png")
        img.save(resized_path)
        return resized_path
    return path

image_path = resize_if_needed(image_path)
```

Deze snippets houden het script robuust, of je nu op een workstation of een bescheiden laptop werkt.

---

## Volledig werkend voorbeeld

Alles bij elkaar, hier is het complete script dat je direct kunt copy‑pasten en uitvoeren:

```python
# python_ocr_tutorial.py
import os
import torch
from PIL import Image
from easyocr import Reader

# ----------------------------------------------------------------------
# Helper: Resize very large images to avoid GPU OOM errors
def resize_if_needed(path, max_dim=3000):
    img = Image.open(path)
    if max(img.size) > max_dim:
        scale = max_dim / max(img.size)
        new_size = (int(img.width * scale), int(img.height * scale))
        img = img.resize(new_size, Image.LANCZOS)
        resized_path = path.replace(".png", "_resized.png")
        img.save(resized_path)
        return resized_path
    return path
# ----------------------------------------------------------------------

# 1️⃣ Verify CUDA availability (optional)
if torch.cuda.is_available():
    print(f"✅ CUDA device detected: {torch.cuda.get_device_name(0)}")
else:
    print("⚠️ No CUDA device – using CPU (expect slower performance).")

# 2️⃣ Initialize the OCR engine for Spanish (GPU if possible)
reader = Reader(lang_list=["es"], gpu=torch.cuda.is_available())

# 3️⃣ Path to the high‑resolution image
image_path = os.path.join("samples", "high_res_spanish.png")
if not os.path.isfile(image_path):
    raise FileNotFoundError(f"Image not found at {image_path}")

# 4️⃣ Resize if the image is gigantic
image_path = resize_if_needed(image_path)

# 5️⃣ Run OCR – this is the core **recognize image text** step
results = reader.readtext(image_path, detail=1, paragraph=False)

# 6️⃣ Filter and concatenate high‑confidence Spanish strings
extracted = []
for bbox, txt, conf in results:
    if conf > 0.85:
        extracted.append(txt)

final_text = "\n".join(extracted)

# 7️⃣ Output the result – **extract spanish text** ready for downstream processing
print("\n📝 Extracted Spanish text:")
print(final_text)
```

**Verwachte output (voorbeeld):**



## Wat kun je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stap‑voor‑stap uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [How to OCR Image Text with Language Using Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [How to Recognize Page Rectangles for OCR Text Recognition in Aspose.OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}