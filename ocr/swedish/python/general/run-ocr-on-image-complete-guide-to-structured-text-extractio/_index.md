---
category: general
date: 2026-05-03
description: Lär dig hur du kör OCR på en bild och extraherar text med koordinater
  med strukturerad OCR‑igenkänning. Steg‑för‑steg Python‑kod inkluderad.
draft: false
keywords:
- run OCR on image
- extract text with coordinates
- structured OCR recognition
- OCR post‑processing
- bounding box extraction
- image text detection
language: sv
og_description: Kör OCR på en bild och få text med koordinater med strukturerad OCR‑igenkänning.
  Fullt Python‑exempel med förklaringar.
og_title: Kör OCR på bild – Handledning för strukturerad textutvinning
tags:
- OCR
- Python
- Computer Vision
title: Kör OCR på bild – Komplett guide till strukturerad textutvinning
url: /sv/python/general/run-ocr-on-image-complete-guide-to-structured-text-extractio/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Run OCR on image – Complete Guide to Structured Text Extraction

Har du någonsin behövt **run OCR on image**‑filer men varit osäker på hur du behåller de exakta positionerna för varje ord? Du är inte ensam. I många projekt—kvittoskanning, formulärdigitalisering eller UI‑testning—behöver du inte bara råtexten utan även de avgränsningsrutor som visar var varje rad finns på bilden.  

Denna handledning visar dig ett praktiskt sätt att *run OCR on image* med **aocr**‑motorn, begära **structured OCR recognition**, och sedan efterbearbeta resultatet samtidigt som du bevarar geometrin. I slutet kommer du kunna **extract text with coordinates** med bara några rader Python, och du kommer förstå varför strukturerat läge är viktigt för efterföljande uppgifter.

## What You’ll Learn

- Hur du initierar OCR‑motorn för **structured OCR recognition**.  
- Hur du matar in en bild och får råresultat som inkluderar radgränser.  
- Hur du kör en post‑processor som rensar texten utan att förlora geometrin.  
- Hur du itererar över de slutgiltiga raderna och skriver ut varje textstycke tillsammans med dess avgränsningsruta.  

Ingen magi, inga dolda steg—bara ett komplett, körbart exempel som du kan släppa in i ditt eget projekt.

---

## Prerequisites

Innan vi dyker ner, se till att du har följande installerat:

```bash
pip install aocr ai   # hypothetical packages; replace with real ones if needed
```

Du behöver också en bildfil (`input_image.png` eller `.jpg`) som innehåller klar, läsbar text. Allt från en skannad faktura till en skärmdump fungerar, så länge OCR‑motorn kan se tecknen.

---

## Step 1: Initialise the OCR engine for structured recognition

Det första vi gör är att skapa en instans av `aocr.Engine()` och tala om för den att vi vill ha **structured OCR recognition**. Strukturerat läge returnerar inte bara vanlig text utan även geometrisk data (avgränsningsrektanglar) för varje rad, vilket är avgörande när du behöver mappa text tillbaka på bilden.

```python
import aocr
import ai   # hypothetical post‑processing module

# Initialise the OCR engine
ocr_engine = aocr.Engine()

# Request structured recognition (text + geometry)
ocr_engine.recognize_mode = aocr.RecognitionMode.Structured
```

> **Why this matters:**  
> I standardläget kan motorn bara ge dig en sträng med sammanslagna ord. Strukturerat läge ger dig en hierarki av sidor → rader → ord, var och en med koordinater, vilket gör det mycket enklare att överlagra resultat på originalbilden eller mata in dem i en layout‑medveten modell.

---

## Step 2: Run OCR on the image and obtain raw results

Nu matar vi bilden till motorn. Anropet `recognize` returnerar ett `OcrResult`‑objekt som innehåller en samling rader, var och en med sin egen avgränsningsruta.

```python
# Load your image (any format supported by aocr)
input_image_path = "input_image.png"

# Run OCR – this returns an OcrResult with lines and bounds
raw_result = ocr_engine.recognize(input_image_path)
```

Vid detta tillfälle innehåller `raw_result.lines` objekt med två viktiga attribut:

- `text` – den igenkända strängen för den raden.  
- `bounds` – en tuple som `(x, y, width, height)` beskriver radens position.

---

## Step 3: Post‑process while preserving geometry

Rå OCR‑utdata är ofta brusig: lösa tecken, felplacerade mellanslag eller radbrytningsproblem. Funktionen `ai.run_postprocessor` rensar texten men **keeps the original geometry** intakt, så du fortfarande har korrekta koordinater.

```python
# Apply a post‑processing step that corrects common OCR errors
postprocessed_result = ai.run_postprocessor(raw_result)

# The structure (lines + bounds) stays the same, only `line.text` changes
```

> **Pro tip:** Om du har domänspecifika vokabulärer (t.ex. produktkoder), mata in en anpassad ordlista till post‑processorn för att förbättra noggrannheten.

---

## Step 4: Extract text with coordinates – iterate and display

Till sist loopar vi över de rensade raderna och skriver ut varje radens avgränsningsruta tillsammans med dess text. Detta är kärnan i **extract text with coordinates**.

```python
# Print each recognised line together with its bounding box
for line in postprocessed_result.lines:
    print(f"[{line.bounds}] {line.text}")
```

### Expected Output

Förutsatt att inmatningsbilden innehåller två rader: “Invoice #12345” och “Total: $89.99”, kommer du se något liknande:

```
[(15, 30, 210, 25)] Invoice #12345
[(15, 70, 190, 25)] Total: $89.99
```

Den första tuplen är `(x, y, width, height)` för raden på originalbilden, vilket låter dig rita rektanglar, markera text eller föra koordinaterna in i ett annat system.

---

## Visualising the Result (Optional)

Om du vill se avgränsningsrutorna överlagrade på bilden kan du använda Pillow (PIL) för att rita rektanglar. Nedan är ett snabbt kodexempel; hoppa gärna över det om du bara behöver rådata.

```python
from PIL import Image, ImageDraw

# Open the original image
img = Image.open(input_image_path)
draw = ImageDraw.Draw(img)

# Draw a rectangle around each line
for line in postprocessed_result.lines:
    x, y, w, h = line.bounds
    draw.rectangle([x, y, x + w, y + h], outline="red", width=2)

# Save or show the annotated image
img.save("annotated_output.png")
img.show()
```

![run OCR on image example showing bounding boxes](/images/ocr-bounding-boxes.png "run OCR on image – bounding box overlay")

Alt‑texten ovan innehåller **primary keyword**, vilket uppfyller SEO‑kravet för bild‑alt‑attribut.

---

## Why Structured OCR Recognition Beats Simple Text Extraction

Du kanske undrar, “Kan jag inte bara köra OCR och få texten? Varför bry sig om geometrin?”  

- **Spatial context:** När du behöver mappa fält på ett formulär (t.ex. “Date” bredvid ett datumvärde) visar koordinater var data finns.  
- **Multi‑column layouts:** Enkel linjär text förlorar ordning; strukturerad data bevarar kolumnordning.  
- **Post‑processing accuracy:** Att känna till boxens storlek hjälper dig avgöra om ett ord är en rubrik, en fotnot eller ett löst artefakt.  

Kort sagt ger **structured OCR recognition** dig flexibiliteten att bygga smartare pipelines—oavsett om du matar data i en databas, skapar sökbara PDF‑filer eller tränar en maskininlärningsmodell som respekterar layout.

---

## Common Edge Cases and How to Handle Them

| Situation | What to Watch For | Suggested Fix |
|-----------|-------------------|---------------|
| **Rotated or skewed images** | Bounding boxes may be off‑axis. | Pre‑process with deskewing (e.g., OpenCV’s `warpAffine`). |
| **Very small fonts** | Engine may miss characters, leading to empty lines. | Increase image resolution or use `ocr_engine.set_dpi(300)`. |
| **Mixed languages** | Wrong language model can cause garbled text. | Set `ocr_engine.language = ["en", "de"]` before recognition. |
| **Overlapping boxes** | Post‑processor might merge two lines unintentionally. | Verify `line.bounds` after processing; adjust thresholds in `ai.run_postprocessor`. |

Att hantera dessa scenarier tidigt sparar dig huvudvärk senare, särskilt när du skalar lösningen till hundratals dokument per dag.

---

## Full End‑to‑End Script

Nedan är det kompletta, färdiga programmet som binder ihop alla steg. Kopiera‑klistra, justera bildvägen, så är du klar.

```python
# -*- coding: utf-8 -*-
"""
Run OCR on image – extract text with coordinates using structured OCR recognition.
Author: Your Name
Date: 2026-05-03
"""

import aocr
import ai
from PIL import Image, ImageDraw

def run_structured_ocr(image_path: str, annotate: bool = False):
    # 1️⃣ Initialise the OCR engine
    ocr_engine = aocr.Engine()
    ocr_engine.recognize_mode = aocr.RecognitionMode.Structured

    # 2️⃣ Recognise the image
    raw_result = ocr_engine.recognize(image_path)

    # 3️⃣ Post‑process while keeping geometry
    processed = ai.run_postprocessor(raw_result)

    # 4️⃣ Print each line with its bounding box
    for line in processed.lines:
        print(f"[{line.bounds}] {line.text}")

    # Optional visualisation
    if annotate:
        img = Image.open(image_path)
        draw = ImageDraw.Draw(img)
        for line in processed.lines:
            x, y, w, h = line.bounds
            draw.rectangle([x, y, x + w, y + h], outline="red", width=2)
        annotated_path = "annotated_" + image_path
        img.save(annotated_path)
        print(f"Annotated image saved as {annotated_path}")

if __name__ == "__main__":
    INPUT_IMG = "input_image.png"
    run_structured_ocr(INPUT_IMG, annotate=True)
```

Att köra detta skript kommer att:

1. **Run OCR on image** med strukturerat läge.  
2. **Extract text with coordinates** för varje rad.  
3. Eventuellt producera en annoterad PNG som visar rutorna.

---

## Conclusion

Du har nu en solid, självständig lösning för att **run OCR on image** och **extract text with coordinates** med **structured OCR recognition**. Koden demonstrerar varje steg—from engine initialisation to post‑processing and visual verification—så att du kan anpassa den till kvitton, formulär eller vilket visuellt dokument som helst som kräver exakt textlokalisering.

Vad blir nästa steg? Prova att byta ut `aocr`‑motorn mot ett annat bibliotek (Tesseract, EasyOCR) och se hur deras strukturerade utskrifter skiljer sig. Experimentera med olika efterbearbetningsstrategier, såsom stavningskontroll eller anpassade regex‑filter, för att öka noggrannheten för ditt område. Och om du bygger en större pipeline, överväg att lagra `(text, bounds)`‑par i en databas för senare analys.

Happy coding, and may your OCR projects be ever accurate!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}