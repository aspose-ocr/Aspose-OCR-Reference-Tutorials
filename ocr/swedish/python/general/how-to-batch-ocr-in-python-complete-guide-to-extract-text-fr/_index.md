---
category: general
date: 2026-06-28
description: Hur man batch-OCR:ar i Python – extrahera text från bilder och konvertera
  skannade sidor till text med batch‑OCR‑behandling.
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert scanned pages to text
- batch OCR processing
language: sv
og_description: Lär dig hur du batchar OCR i Python, extraherar text från bilder och
  konverterar skannade sidor till text med effektiv batch‑OCR‑behandling.
og_title: Hur man batchar OCR i Python – Steg‑för‑steg‑guide
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
title: Hur man batchar OCR i Python – Komplett guide för att extrahera text från bilder
url: /sv/python/general/how-to-batch-ocr-in-python-complete-guide-to-extract-text-fr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Hur man batch‑OCR:ar i Python – Komplett guide för att extrahera text från bilder

Om du undrar **hur man batch‑OCR:ar i Python**, är du på rätt plats. Denna handledning visar ett snabbt sätt att **extrahera text från bilder** och **konvertera skannade sidor till text** med en enda OCR‑motorinstans. Inga fler kopierings‑och‑klistra‑operationer fil för fil – låt koden göra det tunga arbetet.

Vi går igenom allt du behöver: installera biblioteket, läsa in en hel mapp med skanningar, köra batch‑OCR‑bearbetning och hantera resultaten på ett smidigt sätt. När du är klar har du ett återanvändbart skript som förvandlar en hög av PNG‑ eller JPEG‑filer till sökbara textfiler på sekunder.

## Vad du behöver

Innan vi dyker ner, se till att du har:

* Python 3.9+ installerat (koden fungerar även på 3.8, men 3.9+ ger dig de senaste typningsfunktionerna).
* Ett modernt OCR‑bibliotek – här använder vi **Aspose.OCR for Python via .NET**, som exponerar `OcrEngine`‑klassen som visas i originalsnutten.  
  ```bash
  pip install aspose-ocr
  ```
* En mapp med skannade sidor (`page1.png`, `page2.png`, …). Allt som Pillow kan öppna fungerar, så PDF‑, TIFF‑ eller BMP‑filer går också bra.
* En liten dos nyfikenhet – om du aldrig automatiserat bild‑till‑text tidigare, kommer du snart att se varför batch‑OCR är en spelväxlare.

> **Proffstips:** Om du föredrar ett rent Python‑bibliotek, byt ut `OcrEngine` mot `pytesseract.image_to_string`. Den omgivande logiken förblir identisk.

## Hur man batch‑OCR:ar i Python – Steg‑för‑steg‑guide

Nedan är det kompletta, körbara skriptet. Varje rad är kommenterad så att du kan se *varför* varje del är viktig, inte bara *vad* den gör.

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

### Förväntad output

Att köra skriptet mot en mapp med tre PNG‑skanningar ger ungefär följande:

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

Förhandsgranskningen visar de första 200 tecknen på varje sida, och den fullständiga texten lagras i katalogen `ocr_output`.

## Extrahera text från bilder med en enda motor

Varför skapar vi **en** `OcrEngine` och återanvänder den? Att instansiera motorn kan vara dyrt eftersom den laddar språkpaket och inhemska DLL‑filer. Genom att dela samma instans över batchen får du:

* **Spara minne** – endast ett set resurser finns i RAM.
* **Öka hastigheten** – motorn hålls varm och undviker upprepad initialisering.
* **Behålla konsistens** – samma igenkänningsinställningar gäller för varje sida, vilket är avgörande när du vill **extrahera text från bilder** med samma layout.

Om du behöver justera igenkänning (t.ex. aktivera stavningskontroll eller byta språk), gör det *innan* du anropar `recognize_batch`. Alla efterföljande sidor ärver automatiskt de inställningarna.

## Konvertera skannade sidor till text på ett effektivt sätt

Kärnan i problemet – **konvertera skannade sidor till text** – löses av `engine.recognize_batch(images)`. Under huven bearbetar biblioteket varje bild i en bakgrundstrådpool, så du får nästan linjär skalning på maskiner med flera kärnor. Några saker att ha i åtanke:

* **Bildkvalitet är viktigt** – 300 dpi eller högre ger bästa resultat. Om dina skanningar har låg upplösning, överväg att uppskalera med Pillow innan du matar dem till motorn.
* **Färg vs. gråskala** – OCR‑motorer arbetar oftast snabbare på 8‑bits gråskala. Du kan lägga till ett förbehandlingssteg:
  ```python
  img = Image.from_file(path).convert_to_grayscale()
  ```
* **Språkstöd** – Aspose.OCR stödjer över 40 språk. Sätt `engine.language = "eng"` eller `"fra"` innan batch‑anropet om du inte arbetar med engelska.

## Bästa praxis för batch‑OCR‑bearbetning

Även om koden ovan redan är kortfattad, kräver produktionsklar batch‑OCR ofta några extra skyddsåtgärder:

| Problem | Rekommenderad åtgärd |
|---------|----------------------|
| **Stora batcher ( > 500 filer )** | Dela upp i delar om 100–200 bilder för att hålla minnesfotavtrycket litet. |
| **Korrupta eller ej stödjade filer** | Hjälpfunktionen `load_images` fångar redan undantag och loggar en varning; du kan också lägga till en fallback för att hoppa över eller flytta dåliga filer. |
| **Övervakning av framsteg** | Wrappa `recognize_batch` i en loop som returnerar efter varje bild om biblioteket erbjuder per‑bild‑callback. |
| **Efterbehandling** | Kör en stavningskontroll eller regex‑rengöring på de resulterande strängarna för att förbättra sökbarheten i efterföljande steg. |
| **Parallellism** | Om du har en multi‑node‑miljö, distribuera mappar över arbetare och slå ihop `.txt`‑utdata i slutet. |

Dessa tips hjälper dig att skala **batch‑OCR‑bearbetning** från några få sidor till tusentals utan att ditt skript kraschar.

## Vanliga frågor

**Q: Kan jag använda detta direkt med PDF‑filer?**  
A: Absolut. Konvertera varje PDF‑sida till en bild först (t.ex. med `pdf2image`) och skicka den resulterande listan till `recognize_batch`. Resten av pipeline förblir oförändrad.


## Vad bör du lära dig härnäst?


Följande handledningar täcker närbesläktade ämnen som bygger på teknikerna som demonstreras i den här guiden. Varje resurs innehåller kompletta fungerande kodexempel med steg‑för‑steg‑förklaringar för att hjälpa dig bemästra ytterligare API‑funktioner och utforska alternativa implementationsmetoder i dina egna projekt.

- [Extract Text from Image with Aspose OCR – Step‑by‑Step Guide](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extract Text from Images Using OCR Operation on Folders](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}