---
category: general
date: 2026-06-28
description: Hoe batch-OCR in Python te gebruiken — tekst extraheren uit afbeeldingen
  en gescande pagina's omzetten naar tekst met batch-OCR verwerking.
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert scanned pages to text
- batch OCR processing
language: nl
og_description: Leer hoe je batch‑OCR in Python kunt uitvoeren, tekst uit afbeeldingen
  kunt extraheren en gescande pagina’s naar tekst kunt omzetten met efficiënte batch‑OCR‑verwerking.
og_title: Hoe batch‑OCR in Python uit te voeren – Stapsgewijze gids
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: How to batch OCR in Python—extract text from images and convert scanned
    pages to text using batch OCR processing.
  headline: How to Batch OCR in Python – Complete Guide to Extract Text from Images
  type: TechArticle
tags:
- OCR
- Python
- Image Processing
title: Hoe batch-OCR in Python uit te voeren – Complete gids voor het extraheren van
  tekst uit afbeeldingen
url: /nl/python/general/how-to-batch-ocr-in-python-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hoe batch OCR in Python – Complete gids om tekst uit afbeeldingen te extraheren

Als je je afvraagt **hoe batch OCR in Python** werkt, ben je op de juiste plek. Deze tutorial laat je een snelle manier zien om **tekst uit afbeeldingen te extraheren** en **gescande pagina's naar tekst te converteren** met één OCR‑engine‑instantie. Niet langer één bestand na het andere kopiëren‑plakken—laat de code het zware werk doen.

We lopen alles door wat je nodig hebt: de bibliotheek installeren, een hele map met scans laden, batch‑OCR‑verwerking uitvoeren, en de resultaten netjes afhandelen. Aan het einde heb je een herbruikbaar script dat een stapel PNG‑ of JPEG‑bestanden in seconden omzet in doorzoekbare tekstbestanden.

## Wat je nodig hebt

* Python 3.9+ geïnstalleerd (de code werkt ook op 3.8, maar 3.9+ biedt de nieuwste typing‑features).
* Een moderne OCR‑bibliotheek—hier gebruiken we **Aspose.OCR for Python via .NET**, die de `OcrEngine`‑klasse blootlegt zoals in het oorspronkelijke fragment.  
  ```bash
  pip install aspose-ocr
  ```
* Een map met gescande pagina's (`page1.png`, `page2.png`, …). Alles wat Pillow kan openen werkt, dus PDF’s, TIFF’s of BMP’s zijn ook prima.
* Een beetje nieuwsgierigheid—als je nog nooit beeld‑naar‑tekst hebt geautomatiseerd, zul je zien waarom batch OCR een game‑changer is.

> **Pro tip:** Als je de voorkeur geeft aan een pure‑Python bibliotheek, vervang `OcrEngine` door `pytesseract.image_to_string`. De omliggende logica blijft identiek.

## Hoe batch OCR in Python – Stapsgewijze gids

Hieronder staat het volledige, uitvoerbare script. Elke regel is becommentarieerd zodat je kunt zien *waarom* elk onderdeel belangrijk is, niet alleen *wat* het doet.

```python
# batch_ocr.py
import os
from aspose.ocr import OcrEngine, Image  # Aspose OCR library
from typing import List

def load_images(folder: str) -> List[Image]:
    """
    Scan a directory and return a list of Aspose.Image objects.
    Supports PNG, JPEG, BMP, and TIFF out of the box.
    """
    supported_ext = {".png", ".jpg", ".jpeg", ".bmp", ".tif", ".tiff"}
    images = []
    for filename in sorted(os.listdir(folder)):
        _, ext = os.path.splitext(filename)
        if ext.lower() in supported_ext:
            path = os.path.join(folder, filename)
            try:
                img = Image.from_file(path)
                images.append(img)
            except Exception as e:
                print(f"⚠️  Could not load {filename}: {e}")
    return images

def batch_ocr_process(images: List[Image]) -> List[str]:
    """
    Perform OCR on the whole batch at once.
    Returns a list of recognized strings, one per image.
    """
    engine = OcrEngine()          # Step 1: create an OCR engine instance
    # The recognize_batch method is optimized for bulk work.
    return engine.recognize_batch(images)

def save_results(texts: List[str], output_folder: str):
    """
    Write each page's text to a separate .txt file.
    """
    os.makedirs(output_folder, exist_ok=True)
    for idx, page_text in enumerate(texts, start=1):
        out_path = os.path.join(output_folder, f"page_{idx}.txt")
        with open(out_path, "w", encoding="utf-8") as f:
            f.write(page_text)
        print(f"✅  Saved page {idx} → {out_path}")

def main():
    # -----------------------------------------------------------------
    # 1️⃣ Load the images you want to process
    # -----------------------------------------------------------------
    image_folder = "YOUR_DIRECTORY"          # <-- replace with your path
    images = load_images(image_folder)

    if not images:
        print("❌  No supported images found. Exiting.")
        return

    # -----------------------------------------------------------------
    # 2️⃣ Perform OCR on the whole batch at once
    # -----------------------------------------------------------------
    print(f"🔎  Running batch OCR on {len(images)} images...")
    page_texts = batch_ocr_process(images)

    # -----------------------------------------------------------------
    # 3️⃣ Output the recognized text for each page
    # -----------------------------------------------------------------
    for i, txt in enumerate(page_texts, start=1):
        print(f"\n--- Page {i} ---")
        print(txt[:200] + ("…" if len(txt) > 200 else ""))  # preview first 200 chars

    # -----------------------------------------------------------------
    # 4️⃣ (Optional) Save each page's text to a file
    # -----------------------------------------------------------------
    save_results(page_texts, "ocr_output")

if __name__ == "__main__":
    main()
```

### Verwachte output

Het script uitvoeren op een map met drie PNG‑scans levert iets als volgt op:

```
🔎  Running batch OCR on 3 images...

--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit…

--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore…

--- Page 3 ---
Ut enim ad minim veniam, quis nostrud exercitation ullamco…
✅  Saved page 1 → ocr_output/page_1.txt
✅  Saved page 2 → ocr_output/page_2.txt
✅  Saved page 3 → ocr_output/page_3.txt
```

De preview toont de eerste 200 tekens van elke pagina, en de volledige tekst staat in de `ocr_output`‑directory.

## Tekst extraheren uit afbeeldingen met één engine

Waarom maken we **één** `OcrEngine` en hergebruiken we die? Het instantieren van de engine kan duur zijn omdat het taalpakketten en native DLL‑s laadt. Door dezelfde instantie over de batch te delen, krijg je:

* **Geheugen besparen** – er is slechts één set bronnen in RAM.
* **Snelheid verhogen** – de engine blijft warm, waardoor herhaalde initialisatie wordt vermeden.
* **Consistentie behouden** – dezelfde herkenningsinstellingen gelden voor elke pagina, wat essentieel is wanneer je **tekst uit afbeeldingen** wilt extraheren die dezelfde lay-out delen.

Als je de herkenning moet aanpassen (bijv. spell‑check inschakelen of de taal wijzigen), doe dat *voor* het aanroepen van `recognize_batch`. Alle volgende pagina's erven die instellingen automatisch.

## Gescande pagina's efficiënt naar tekst converteren

De kern van het probleem—**gescande pagina's naar tekst converteren**—wordt opgelost door `engine.recognize_batch(images)`. Onder de motorkap verwerkt de bibliotheek elke afbeelding in een achtergrond‑thread‑pool, zodat je bijna lineaire schaalbaarheid krijgt op multi‑core machines. Een paar zaken om in gedachten te houden:

* **Beeldkwaliteit is belangrijk** – 300 dpi of hoger levert de beste resultaten. Als je scans van lage resolutie zijn, overweeg dan up‑sampling met Pillow voordat je ze aan de engine geeft.
* **Kleur vs. grijswaarden** – OCR‑engines werken meestal sneller op 8‑bit grijswaarden. Je kunt een voorverwerkingsstap toevoegen:  
  ```python
  img = Image.from_file(path).convert_to_grayscale()
  ```
* **Taalondersteuning** – Aspose.OCR ondersteunt meer dan 40 talen. Stel `engine.language = "eng"` of `"fra"` in vóór de batch‑aanroep als je niet met Engels werkt.

## Beste praktijken voor batch OCR verwerking

Hoewel de bovenstaande code al beknopt is, vereist batch OCR op productieniveau vaak een paar extra waarborgen:

| Concern | Recommended Approach |
|---------|----------------------|
| **Grote batches ( > 500 bestanden )** | Verdeel in delen van 100–200 afbeeldingen om het geheugenverbruik bescheiden te houden. |
| **Beschadigde of niet‑ondersteunde bestanden** | De `load_images`‑helper vangt al uitzonderingen op en logt een waarschuwing; je kunt ook een fallback schrijven om slechte bestanden over te slaan of te verplaatsen. |
| **Voortgangsmonitoring** | Omwikkel `recognize_batch` in een lus die na elke afbeelding een yield geeft als de bibliotheek per‑afbeelding callbacks exposeert. |
| **Nabewerking** | Voer een spell‑check of regex‑opschoning uit op de resulterende strings om de zoekbaarheid downstream te verbeteren. |
| **Parallelisme** | Als je een multi‑node setup hebt, verdeel dan mappen over workers en voeg de `.txt`‑outputs aan het einde samen. |

Deze tips helpen je **batch OCR verwerking** op te schalen van een handvol pagina's tot duizenden zonder dat je script crasht.

## Veelgestelde vragen

**Q: Kan ik dit direct met PDF’s gebruiken?**  
A: Absoluut. Converteer eerst elke PDF‑pagina naar een afbeelding (bijv. met `pdf2image`) en geef de resulterende lijst door aan `recognize_batch`. De rest van de pipeline blijft ongewijzigd.

## Wat moet je hierna leren?

De volgende tutorials behandelen nauw verwante onderwerpen die voortbouwen op de technieken die in deze gids worden gedemonstreerd. Elke bron bevat volledige werkende code‑voorbeelden met stapsgewijze uitleg om je te helpen extra API‑functies onder de knie te krijgen en alternatieve implementatie‑benaderingen in je eigen projecten te verkennen.

- [Tekst extraheren uit afbeelding met Aspose OCR – Stapsgewijze gids](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Tekst extraheren uit afbeeldingen met OCR‑bewerking op mappen](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Hoe tekst extraheren uit ZIP‑archieven met Aspose.OCR voor .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}